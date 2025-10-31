#!/bin/bash

# ======================================
# سكريبت حماية Anti-DDoS للـ VPS
# يجب تشغيله كـ root
# ======================================

echo "========================================="
echo "  تثبيت حماية Anti-DDoS للسيرفر"
echo "========================================="

# التحقق من صلاحيات root
if [ "$EUID" -ne 0 ]; then 
    echo "يرجى تشغيل السكريبت بصلاحيات root"
    exit 1
fi

# متغيرات قابلة للتعديل
SAMP_PORT=7777
SSH_PORT=22
MAX_CONN_PER_IP=3
RATE_LIMIT=50

# ======================================
# 1. تثبيت الأدوات المطلوبة
# ======================================

echo "[1/6] تثبيت الأدوات الأساسية..."
apt-get update -qq
apt-get install -y iptables iptables-persistent fail2ban ufw > /dev/null 2>&1

# ======================================
# 2. إعداد UFW (Firewall بسيط)
# ======================================

echo "[2/6] إعداد UFW..."
ufw --force disable
ufw --force reset

# السماح بالمنافذ الأساسية
ufw default deny incoming
ufw default allow outgoing
ufw allow $SSH_PORT/tcp comment 'SSH'
ufw allow $SAMP_PORT/udp comment 'SA-MP Server'

# تفعيل UFW
ufw --force enable

# ======================================
# 3. إعداد iptables المتقدمة
# ======================================

echo "[3/6] إعداد iptables للحماية المتقدمة..."

# مسح القواعد القديمة
iptables -F
iptables -X
iptables -t nat -F
iptables -t nat -X
iptables -t mangle -F
iptables -t mangle -X

# السياسة الافتراضية
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# السماح بـ localhost
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT

# السماح بالاتصالات المؤسسة مسبقاً
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# ======================================
# 4. الحماية من هجمات DDoS
# ======================================

echo "[4/6] تطبيق قواعد Anti-DDoS..."

# حماية من SYN flood
iptables -A INPUT -p tcp --syn -m limit --limit 1/s --limit-burst 3 -j ACCEPT
iptables -A INPUT -p tcp --syn -j DROP

# حماية من UDP flood على منفذ SA-MP
iptables -A INPUT -p udp --dport $SAMP_PORT -m state --state NEW -m recent --set
iptables -A INPUT -p udp --dport $SAMP_PORT -m state --state NEW -m recent --update --seconds 1 --hitcount $RATE_LIMIT -j DROP
iptables -A INPUT -p udp --dport $SAMP_PORT -j ACCEPT

# حماية من ICMP flood (ping)
iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP

# حماية من port scanning
iptables -N port-scanning
iptables -A port-scanning -p tcp --tcp-flags SYN,ACK,FIN,RST RST -m limit --limit 1/s --limit-burst 2 -j RETURN
iptables -A port-scanning -j DROP

# حد الاتصالات المتزامنة من نفس IP
iptables -A INPUT -p tcp --syn --dport $SAMP_PORT -m connlimit --connlimit-above $MAX_CONN_PER_IP -j REJECT
iptables -A INPUT -p udp --dport $SAMP_PORT -m connlimit --connlimit-above $MAX_CONN_PER_IP -j DROP

# حماية SSH
iptables -A INPUT -p tcp --dport $SSH_PORT -m state --state NEW -m recent --set
iptables -A INPUT -p tcp --dport $SSH_PORT -m state --state NEW -m recent --update --seconds 60 --hitcount 4 -j DROP
iptables -A INPUT -p tcp --dport $SSH_PORT -j ACCEPT

# منع IP spoofing
iptables -A INPUT -s 10.0.0.0/8 -j DROP
iptables -A INPUT -s 172.16.0.0/12 -j DROP
iptables -A INPUT -s 192.168.0.0/16 -j DROP
iptables -A INPUT -s 224.0.0.0/4 -j DROP
iptables -A INPUT -s 240.0.0.0/5 -j DROP

# حماية من fragmented packets
iptables -A INPUT -f -j DROP

# منع invalid packets
iptables -A INPUT -m state --state INVALID -j DROP

# ======================================
# 5. حفظ القواعد
# ======================================

echo "[5/6] حفظ قواعد iptables..."
iptables-save > /etc/iptables/rules.v4
netfilter-persistent save > /dev/null 2>&1

# ======================================
# 6. إعداد Fail2Ban
# ======================================

echo "[6/6] إعداد Fail2Ban..."

# إنشاء ملف تكوين Fail2Ban لـ SA-MP
cat > /etc/fail2ban/filter.d/samp.conf << 'EOF'
[Definition]
failregex = ^.*\[.*\] Incoming connection: <HOST>:\d+.*$
            ^.*Connection attempt from <HOST> blocked.*$
ignoreregex =
EOF

# إضافة jail لـ SA-MP
cat >> /etc/fail2ban/jail.local << EOF

[samp-ddos]
enabled = true
port = $SAMP_PORT
filter = samp
logpath = /path/to/samp/server_log.txt
maxretry = 10
findtime = 60
bantime = 3600
EOF

# إعادة تشغيل Fail2Ban
systemctl restart fail2ban
systemctl enable fail2ban

# ======================================
# تأكيد الاكتمال
# ======================================

echo ""
echo "========================================="
echo "  ✓ تم تثبيت الحماية بنجاح!"
echo "========================================="
echo ""
echo "ملخص الإعدادات:"
echo "  - منفذ SA-MP: $SAMP_PORT"
echo "  - منفذ SSH: $SSH_PORT"
echo "  - حد الاتصالات لكل IP: $MAX_CONN_PER_IP"
echo "  - حد الحزم في الثانية: $RATE_LIMIT"
echo ""
echo "الأدوات المفعلة:"
echo "  ✓ UFW Firewall"
echo "  ✓ iptables المتقدمة"
echo "  ✓ Fail2Ban"
echo ""
echo "أوامر مفيدة:"
echo "  - عرض قواعد iptables: iptables -L -n -v"
echo "  - حالة Fail2Ban: fail2ban-client status"
echo "  - إضافة IP للقائمة البيضاء: iptables -I INPUT -s IP_ADDRESS -j ACCEPT"
echo "  - حظر IP: iptables -A INPUT -s IP_ADDRESS -j DROP"
echo ""
echo "تحذير: تأكد من أن منفذ SSH ($SSH_PORT) مفتوح قبل قطع الاتصال!"
echo "=====================================
