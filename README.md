<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HOSTING NEXUS - استضافة محمية بالكامل</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0a0e27 0%, #1a1f3a 100%);
            color: #fff;
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header */
        header {
            background: rgba(10, 14, 39, 0.95);
            backdrop-filter: blur(10px);
            padding: 20px 0;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            box-shadow: 0 2px 20px rgba(0, 194, 255, 0.1);
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 28px;
            font-weight: bold;
            background: linear-gradient(45deg, #00c2ff, #0066ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .shield-icon {
            width: 35px;
            height: 35px;
            background: linear-gradient(45deg, #00c2ff, #0066ff);
            border-radius: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
        }

        nav ul {
            display: flex;
            list-style: none;
            gap: 30px;
        }

        nav a {
            color: #fff;
            text-decoration: none;
            transition: color 0.3s;
            font-weight: 500;
        }

        nav a:hover {
            color: #00c2ff;
        }

        /* Hero Section */
        .hero {
            padding: 150px 0 100px;
            text-align: center;
        }

        .hero h1 {
            font-size: 48px;
            margin-bottom: 20px;
            background: linear-gradient(45deg, #00c2ff, #0066ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: fadeInUp 1s ease;
        }

        .hero p {
            font-size: 20px;
            color: #b0b8d4;
            margin-bottom: 40px;
            animation: fadeInUp 1s ease 0.2s backwards;
        }

        .cta-button {
            display: inline-block;
            padding: 15px 40px;
            background: linear-gradient(45deg, #00c2ff, #0066ff);
            color: #fff;
            text-decoration: none;
            border-radius: 50px;
            font-weight: bold;
            font-size: 18px;
            transition: transform 0.3s, box-shadow 0.3s;
            animation: fadeInUp 1s ease 0.4s backwards;
        }

        .cta-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(0, 194, 255, 0.4);
        }

        /* Features Section */
        .features {
            padding: 80px 0;
            background: rgba(26, 31, 58, 0.5);
        }

        .section-title {
            text-align: center;
            font-size: 36px;
            margin-bottom: 60px;
            color: #00c2ff;
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
        }

        .feature-card {
            background: rgba(10, 14, 39, 0.8);
            padding: 30px;
            border-radius: 15px;
            border: 1px solid rgba(0, 194, 255, 0.2);
            transition: transform 0.3s, box-shadow 0.3s;
            text-align: center;
        }

        .feature-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 40px rgba(0, 194, 255, 0.3);
            border-color: #00c2ff;
        }

        .feature-icon {
            font-size: 48px;
            margin-bottom: 20px;
        }

        .feature-card h3 {
            color: #00c2ff;
            margin-bottom: 15px;
            font-size: 22px;
        }

        /* DDoS Protection Section */
        .ddos-section {
            padding: 80px 0;
            text-align: center;
        }

        .ddos-box {
            background: linear-gradient(135deg, rgba(0, 194, 255, 0.1), rgba(0, 102, 255, 0.1));
            border: 2px solid #00c2ff;
            border-radius: 20px;
            padding: 50px;
            margin: 40px 0;
            position: relative;
            overflow: hidden;
        }

        .ddos-box::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(0, 194, 255, 0.1), transparent);
            animation: rotate 4s linear infinite;
        }

        @keyframes rotate {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .ddos-content {
            position: relative;
            z-index: 1;
        }

        .ddos-box h2 {
            font-size: 40px;
            margin-bottom: 20px;
            color: #00c2ff;
        }

        .ddos-stats {
            display: flex;
            justify-content: center;
            gap: 50px;
            margin-top: 40px;
            flex-wrap: wrap;
        }

        .stat {
            text-align: center;
        }

        .stat-number {
            font-size: 48px;
            font-weight: bold;
            color: #00c2ff;
            display: block;
        }

        .stat-label {
            color: #b0b8d4;
            font-size: 18px;
        }

        /* Server Info Box */
        .server-info-box {
            background: rgba(10, 14, 39, 0.9);
            border: 2px solid #00c2ff;
            border-radius: 20px;
            padding: 40px;
            margin-top: 40px;
            text-align: center;
        }

        .server-info-box h3 {
            font-size: 28px;
            color: #00c2ff;
            margin-bottom: 30px;
        }

        .server-details {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            flex-wrap: wrap;
        }

        .ip-display {
            background: rgba(0, 194, 255, 0.1);
            padding: 20px 30px;
            border-radius: 15px;
            border: 1px solid rgba(0, 194, 255, 0.3);
        }

        .ip-label {
            display: block;
            color: #b0b8d4;
            font-size: 14px;
            margin-bottom: 8px;
        }

        .ip-value {
            font-size: 28px;
            font-weight: bold;
            color: #00c2ff;
            font-family: 'Courier New', monospace;
            letter-spacing: 2px;
        }

        .copy-btn {
            background: linear-gradient(45deg, #00c2ff, #0066ff);
            color: #fff;
            border: none;
            padding: 15px 30px;
            border-radius: 10px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
        }

        .copy-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(0, 194, 255, 0.4);
        }

        .copy-btn:active {
            transform: translateY(-1px);
        }

        .server-note {
            margin-top: 20px;
            color: #b0b8d4;
            font-size: 16px;
        }

        /* Pricing Section */
        .pricing {
            padding: 80px 0;
            background: rgba(26, 31, 58, 0.5);
        }

        .pricing-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
            margin-top: 50px;
        }

        .pricing-card {
            background: rgba(10, 14, 39, 0.9);
            border-radius: 20px;
            padding: 40px;
            border: 2px solid rgba(0, 194, 255, 0.2);
            transition: transform 0.3s, border-color 0.3s;
            text-align: center;
        }

        .pricing-card:hover {
            transform: translateY(-10px);
            border-color: #00c2ff;
        }

        .pricing-card.featured {
            border-color: #00c2ff;
            background: linear-gradient(135deg, rgba(0, 194, 255, 0.1), rgba(0, 102, 255, 0.1));
            transform: scale(1.05);
        }

        .plan-name {
            font-size: 24px;
            color: #00c2ff;
            margin-bottom: 20px;
            font-weight: bold;
        }

        .plan-price {
            font-size: 48px;
            font-weight: bold;
            margin-bottom: 10px;
        }

        .plan-price span {
            font-size: 20px;
            color: #b0b8d4;
        }

        .plan-features {
            list-style: none;
            margin: 30px 0;
            text-align: right;
        }

        .plan-features li {
            padding: 10px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            color: #b0b8d4;
        }

        .plan-features li::before {
            content: "✓ ";
            color: #00c2ff;
            font-weight: bold;
            margin-left: 10px;
        }

        .plan-button {
            display: block;
            width: 100%;
            padding: 15px;
            background: linear-gradient(45deg, #00c2ff, #0066ff);
            color: #fff;
            text-decoration: none;
            border-radius: 10px;
            font-weight: bold;
            transition: transform 0.3s;
        }

        .plan-button:hover {
            transform: translateY(-3px);
        }

        /* Contact Section */
        .contact {
            padding: 80px 0;
        }

        .contact-form {
            max-width: 600px;
            margin: 50px auto;
            background: rgba(10, 14, 39, 0.8);
            padding: 40px;
            border-radius: 20px;
            border: 1px solid rgba(0, 194, 255, 0.2);
        }

        .form-group {
            margin-bottom: 25px;
        }

        .form-group label {
            display: block;
            margin-bottom: 10px;
            color: #00c2ff;
            font-weight: bold;
        }

        .form-group input,
        .form-group textarea {
            width: 100%;
            padding: 15px;
            background: rgba(26, 31, 58, 0.8);
            border: 1px solid rgba(0, 194, 255, 0.3);
            border-radius: 10px;
            color: #fff;
            font-size: 16px;
            transition: border-color 0.3s;
        }

        .form-group input:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: #00c2ff;
        }

        .form-group textarea {
            min-height: 150px;
            resize: vertical;
        }

        .submit-button {
            width: 100%;
            padding: 15px;
            background: linear-gradient(45deg, #00c2ff, #0066ff);
            color: #fff;
            border: none;
            border-radius: 10px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: transform 0.3s;
        }

        .submit-button:hover {
            transform: translateY(-3px);
        }

        /* Footer */
        footer {
            background: rgba(10, 14, 39, 0.95);
            padding: 40px 0;
            text-align: center;
            border-top: 1px solid rgba(0, 194, 255, 0.2);
        }

        footer p {
            color: #b0b8d4;
        }

        /* Animations */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .hero h1 {
                font-size: 32px;
            }

            .pricing-card.featured {
                transform: scale(1);
            }

            nav ul {
                display: none;
            }
        }
    </style>
</head>
<body>
    <header>
        <nav class="container">
            <div class="logo">
                <div class="shield-icon">🛡️</div>
                HOSTING NEXUS
            </div>
            <ul>
                <li><a href="#home">الرئيسية</a></li>
                <li><a href="#features">المميزات</a></li>
                <li><a href="#pricing">الأسعار</a></li>
                <li><a href="#contact">اتصل بنا</a></li>
            </ul>
        </nav>
    </header>

    <section id="home" class="hero">
        <div class="container">
            <h1>استضافة VPS محمية بالكامل</h1>
            <p>خوادم افتراضية قوية مع حماية متقدمة ضد هجمات DDoS</p>
            <a href="#pricing" class="cta-button">ابدأ الآن</a>
        </div>
    </section>

    <section id="features" class="features">
        <div class="container">
            <h2 class="section-title">لماذا تختارنا؟</h2>
            <div class="features-grid">
                <div class="feature-card">
                    <div class="feature-icon">⚡</div>
                    <h3>أداء فائق</h3>
                    <p>خوادم SSD بسرعات عالية وأداء متميز</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">🛡️</div>
                    <h3>حماية DDoS</h3>
                    <p>حماية متقدمة من جميع أنواع الهجمات</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">🚀</div>
                    <h3>نشر فوري</h3>
                    <p>تفعيل السيرفر خلال دقائق</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">💻</div>
                    <h3>لوحة تحكم سهلة</h3>
                    <p>إدارة كاملة من لوحة تحكم بسيطة</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">🔒</div>
                    <h3>أمان عالي</h3>
                    <p>تشفير وحماية متعددة الطبقات</p>
                </div>
                <div class="feature-card">
                    <div class="feature-icon">📞</div>
                    <h3>دعم 24/7</h3>
                    <p>فريق دعم جاهز على مدار الساعة</p>
                </div>
            </div>
        </div>
    </section>

    <section class="ddos-section">
        <div class="container">
            <div class="ddos-box">
                <div class="ddos-content">
                    <h2>🛡️ حماية DDoS متقدمة</h2>
                    <p style="font-size: 20px; color: #b0b8d4; margin: 20px 0;">نحمي خوادمك من أقوى الهجمات</p>
                    <div class="ddos-stats">
                        <div class="stat">
                            <span class="stat-number">500+</span>
                            <span class="stat-label">Gbps حماية</span>
                        </div>
                        <div class="stat">
                            <span class="stat-number">99.9%</span>
                            <span class="stat-label">وقت التشغيل</span>
                        </div>
                        <div class="stat">
                            <span class="stat-number">24/7</span>
                            <span class="stat-label">مراقبة مستمرة</span>
                        </div>
                    </div>
                </div>
            </div>

            <div class="server-info-box">
                <h3>🌐 معلومات الاتصال بالسيرفر</h3>
                <div class="server-details">
                    <div class="ip-display">
                        <span class="ip-label">عنوان IP والبورت:</span>
                        <span class="ip-value" id="serverIP">188.87.86.97:7777</span>
                    </div>
                    <button class="copy-btn" onclick="copyIP()">
                        <span id="copyText">📋 نسخ</span>
                    </button>
                </div>
                <p class="server-note">استخدم هذا العنوان للاتصال بخوادمنا</p>
            </div>
        </div>
    </section>

    <section id="pricing" class="pricing">
        <div class="container">
            <h2 class="section-title">خطط الأسعار</h2>
            <div class="pricing-grid">
                <div class="pricing-card">
                    <h3 class="plan-name">الباقة الأساسية</h3>
                    <div class="plan-price">$15<span>/شهرياً</span></div>
                    <ul class="plan-features">
                        <li>2 CPU Cores</li>
                        <li>4 GB RAM</li>
                        <li>80 GB SSD</li>
                        <li>2 TB نقل البيانات</li>
                        <li>حماية DDoS أساسية</li>
                        <li>دعم فني</li>
                    </ul>
                    <a href="#contact" class="plan-button">اطلب الآن</a>
                </div>

                <div class="pricing-card featured">
                    <h3 class="plan-name">⭐ VIP</h3>
                    <div class="plan-price">50<span> DH/شهرياً</span></div>
                    <ul class="plan-features">
                        <li>4 CPU Cores</li>
                        <li>8 GB RAM</li>
                        <li>160 GB SSD</li>
                        <li>4 TB نقل البيانات</li>
                        <li>حماية DDoS متقدمة</li>
                        <li>نسخ احتياطي يومي</li>
                        <li>دعم ذو أولوية</li>
                    </ul>
                    <a href="#contact" class="plan-button">اطلب الآن</a>
                </div>

                <div class="pricing-card">
                    <h3 class="plan-name">باقة الأعمال</h3>
                    <div class="plan-price">$70<span>/شهرياً</span></div>
                    <ul class="plan-features">
                        <li>8 CPU Cores</li>
                        <li>16 GB RAM</li>
                        <li>320 GB SSD</li>
                        <li>8 TB نقل البيانات</li>
                        <li>حماية DDoS قصوى</li>
                        <li>نسخ احتياطي كل ساعة</li>
                        <li>دعم VIP</li>
                        <li>IP مخصص</li>
                    </ul>
                    <a href="#contact" class="plan-button">اطلب
