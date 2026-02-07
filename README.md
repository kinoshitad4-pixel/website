<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>北大心理ゼミ - 学問の実践</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Kaisei+Decol:wght@700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary-color: #0071E3;
            --primary-light: #E8F4FF;
            --text-dark: #1D1D1F;
            --text-light: #F5F5F7;
            --gray-light: #E0E0E0;
            --gray-medium: #6E6E73;
            --success-color: #34C759;
            --error-color: #FF3B30;
            --warning-color: #FF9500;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: "Hiragino Kaku Gothic ProN", "Noto Sans JP", sans-serif;
            color: var(--text-dark);
            line-height: 1.6;
            background-color: #fff;
        }

        /* ==================== ナビゲーション ==================== */
        header {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            height: 70px;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid rgba(0, 0, 0, 0.1);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 40px;
            z-index: 1000;
            transition: all 0.3s ease;
        }

        header.scrolled {
            background: rgba(255, 255, 255, 0.98);
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
        }

        .logo {
            font-size: 24px;
            font-weight: 700;
            color: #003366;
            text-decoration: none;
            display: flex;
            align-items: center;
            gap: 10px;
            font-family: 'Kaisei Decol', 'HGP行書体', 'MS P行書', cursive;
        }

        .logo-img {
            width: 40px;
            height: 40px;
            border-radius: 8px;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .logo-img img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        nav {
            display: flex;
            gap: 40px;
        }

        nav a {
            color: var(--text-dark);
            text-decoration: none;
            font-size: 14px;
            font-weight: 500;
            transition: color 0.3s ease;
            position: relative;
        }

        nav a:hover {
            color: var(--primary-color);
        }

        nav a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--primary-color);
            transition: width 0.3s ease;
        }

        nav a:hover::after {
            width: 100%;
        }

        .hamburger {
            display: none;
            flex-direction: column;
            cursor: pointer;
            gap: 5px;
        }

        .hamburger span {
            width: 25px;
            height: 2px;
            background: var(--text-dark);
            transition: all 0.3s ease;
        }

        /* ==================== ボディ部 ==================== */
        main {
            margin-top: 70px;
        }

        .hero {
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
            background: linear-gradient(135deg, var(--primary-color), var(--primary-light));
        }

        .hero::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 120" preserveAspectRatio="none"><path d="M0,50 Q300,0 600,50 T1200,50 L1200,120 L0,120 Z" fill="rgba(255,255,255,0.1)"/><path d="M0,60 Q300,10 600,60 T1200,60 L1200,120 L0,120 Z" fill="rgba(255,255,255,0.15)" style="animation: wave 20s infinite;"/></svg>') repeat-x;
            background-size: 600px 120px;
            animation: wave 15s linear infinite;
            opacity: 0.6;
        }

        @keyframes wave {
            0% { background-position: 0 0; }
            100% { background-position: 600px 0; }
        }

        .hero-content {
            position: relative;
            z-index: 10;
            text-align: center;
            color: white;
            animation: fadeInUp 1s ease;
        }

        .hero-content h1 {
            font-size: 216px;
            font-weight: 700;
            margin-bottom: 20px;
            animation: fadeIn 1s ease 0.2s both;
            color: #FFFFFF;
            line-height: 1;
            -webkit-text-stroke: 3px #000000;
            text-stroke: 3px #000000;
            text-shadow: 
                3px 3px 0 #000,
                -3px -3px 0 #000,
                3px -3px 0 #000,
                -3px 3px 0 #000;
        }

        .hero-content p {
            font-size: 28px;
            font-weight: 300;
            margin-top: 30px;
            animation: fadeIn 1s ease 0.4s both;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

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

        .scroll-indicator {
            position: absolute;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 11;
            animation: bounce 2s infinite;
        }

        .scroll-indicator svg {
            width: 30px;
            height: 30px;
            stroke: white;
            fill: none;
            stroke-width: 2;
        }

        @keyframes bounce {
            0%, 100% { transform: translateX(-50%) translateY(0); }
            50% { transform: translateX(-50%) translateY(10px); }
        }

        /* ==================== セクション共通 ==================== */
        section {
            padding: 80px 40px;
            max-width: 1400px;
            margin: 0 auto;
        }

        .section-title {
            font-size: 48px;
            font-weight: 700;
            text-align: center;
            margin-bottom: 60px;
            color: var(--text-dark);
        }

        .section-title::after {
            content: '';
            display: block;
            width: 60px;
            height: 4px;
            background: var(--primary-color);
            margin: 15px auto 0;
            border-radius: 2px;
        }

        /* ==================== 活動セクション ==================== */
        .activities-section {
            background: white;
        }

        .activities-list {
            display: flex;
            flex-direction: column;
            gap: 50px;
        }

        .activity-item {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 40px;
            align-items: center;
            opacity: 0;
            animation: slideUp 0.8s ease forwards;
        }

        .activity-item:nth-child(1) { animation-delay: 0.1s; }
        .activity-item:nth-child(2) { animation-delay: 0.2s; }
        .activity-item:nth-child(3) { animation-delay: 0.3s; }

        .activity-item:nth-child(even) {
            grid-template-columns: 1fr 1fr;
            direction: rtl;
        }

        .activity-item > * {
            direction: ltr;
        }

        .activity-image {
            width: 100%;
            height: 300px;
            background: linear-gradient(135deg, var(--primary-color), var(--primary-light));
            border-radius: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 14px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }

        .activity-item:hover .activity-image {
            transform: translateY(-8px);
        }

        .activity-content h3 {
            font-size: 36px;
            font-weight: 700;
            margin-bottom: 20px;
            color: var(--text-dark);
        }

        .activity-content p {
            font-size: 16px;
            color: var(--gray-medium);
            line-height: 1.8;
            margin-bottom: 20px;
        }

        .btn {
            display: inline-block;
            padding: 12px 30px;
            background: var(--primary-color);
            color: white;
            text-decoration: none;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 600;
            transition: all 0.3s ease;
            border: 2px solid var(--primary-color);
            cursor: pointer;
        }

        .btn:hover {
            background: white;
            color: var(--primary-color);
        }

        .btn-secondary {
            background: transparent;
            color: var(--primary-color);
            border: 2px solid var(--primary-color);
        }

        .btn-secondary:hover {
            background: var(--primary-color);
            color: white;
        }

        /* ==================== 魅力ポイント ==================== */
        .features {
            background: var(--text-light);
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 30px;
        }

        .feature-tile {
            aspect-ratio: 1;
            background: white;
            border-radius: 16px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 30px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            position: relative;
            overflow: hidden;
            opacity: 0;
            animation: scaleUp 0.6s ease forwards;
        }

        .feature-tile:nth-child(1) { animation-delay: 0s; }
        .feature-tile:nth-child(2) { animation-delay: 0.1s; }
        .feature-tile:nth-child(3) { animation-delay: 0.2s; }
        .feature-tile:nth-child(4) { animation-delay: 0.3s; }
        .feature-tile:nth-child(5) { animation-delay: 0.4s; }

        @keyframes scaleUp {
            from {
                opacity: 0;
                transform: scale(0.8);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(40px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .feature-tile:hover {
            transform: translateY(-12px);
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.15);
        }

        .feature-tile::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(0, 113, 227, 0.1) 0%, transparent 70%);
            transition: transform 0.3s ease;
        }

        .feature-tile:hover::before {
            transform: translate(25%, 25%);
        }

        .feature-icon {
            width: 80px;
            height: 80px;
            background: linear-gradient(135deg, var(--primary-color), var(--primary-light));
            border-radius: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 15px;
            font-size: 40px;
            color: white;
            position: relative;
            z-index: 1;
        }

        .feature-tile h4 {
            font-size: 18px;
            font-weight: 600;
            color: var(--text-dark);
            position: relative;
            z-index: 1;
        }

        /* ==================== カレンダーセクション ==================== */
        .calendar-section {
            background: white;
        }

        .calendar-container {
            background: var(--text-light);
            border-radius: 16px;
            padding: 40px;
            text-align: center;
        }

        .calendar-placeholder {
            width: 100%;
            height: 500px;
            background: linear-gradient(135deg, var(--primary-color), var(--primary-light));
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 18px;
            margin-bottom: 20px;
        }

        .download-btn {
            display: inline-block;
            padding: 12px 30px;
            background: var(--primary-color);
            color: white;
            text-decoration: none;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 600;
            transition: all 0.3s ease;
        }

        .download-btn:hover {
            box-shadow: 0 8px 20px rgba(0, 113, 227, 0.3);
            transform: translateY(-2px);
        }

        /* ==================== CTA セクション ==================== */
        .cta-section {
            background: linear-gradient(135deg, var(--primary-color), var(--primary-light));
            color: white;
            text-align: center;
            padding: 80px 40px;
        }

        .cta-section h2 {
            font-size: 48px;
            font-weight: 700;
            margin-bottom: 30px;
        }

        .cta-section p {
            font-size: 18px;
            margin-bottom: 40px;
            opacity: 0.95;
        }

        .social-links {
            display: flex;
            gap: 20px;
            justify-content: center;
            margin-bottom: 40px;
        }

        .social-icon {
            width: 60px;
            height: 60px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
            color: white;
            font-size: 28px;
        }

        .social-icon:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: translateY(-4px);
        }

        /* ==================== フッター ==================== */
        footer {
            background: var(--text-dark);
            color: white;
            padding: 60px 40px 20px;
            text-align: center;
        }

        .footer-content {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 40px;
            margin-bottom: 40px;
            text-align: left;
        }

        .footer-section h4 {
            font-size: 16px;
            font-weight: 600;
            margin-bottom: 15px;
        }

        .footer-section ul {
            list-style: none;
        }

        .footer-section ul li {
            margin-bottom: 10px;
        }

        .footer-section a {
            color: rgba(255, 255, 255, 0.7);
            text-decoration: none;
            transition: color 0.3s ease;
        }

        .footer-section a:hover {
            color: white;
        }

        .copyright {
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            padding-top: 20px;
            font-size: 14px;
            color: rgba(255, 255, 255, 0.6);
        }

        /* ==================== ページ管理 ==================== */
        .page {
            display: none;
        }

        .page.active {
            display: block;
        }

        /* ==================== レスポンシブ ==================== */
        @media (max-width: 768px) {
            header {
                padding: 0 20px;
            }

            nav {
                display: none;
                position: absolute;
                top: 70px;
                left: 0;
                right: 0;
                flex-direction: column;
                background: white;
                padding: 20px;
                gap: 0;
                box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            }

            nav.active {
                display: flex;
            }

            nav a {
                padding: 15px 0;
                border-bottom: 1px solid var(--gray-light);
            }

            .hamburger {
                display: flex;
            }

            .hero-content h1 {
                font-size: 144px;
                color: #FFFFFF;
                -webkit-text-stroke: 2px #000000;
                text-stroke: 2px #000000;
                text-shadow: 
                    2px 2px 0 #000,
                    -2px -2px 0 #000,
                    2px -2px 0 #000,
                    -2px 2px 0 #000;
            }

            .hero-content p {
                font-size: 20px;
            }

            section {
                padding: 60px 20px;
            }

            .section-title {
                font-size: 36px;
            }

            .activity-item {
                grid-template-columns: 1fr;
                gap: 20px;
            }

            .activity-item:nth-child(even) {
                direction: ltr;
            }

            .features-grid {
                grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            }

            .footer-content {
                grid-template-columns: 1fr;
                text-align: center;
            }
        }

        /* ==================== その他ページ用スタイル ==================== */
        .breadcrumb {
            padding: 20px 40px;
            font-size: 14px;
            color: var(--gray-medium);
            max-width: 1400px;
            margin: 0 auto;
        }

        .breadcrumb a {
            color: var(--primary-color);
            text-decoration: none;
        }

        .content-section {
            max-width: 1200px;
            margin: 0 auto;
            padding: 40px;
        }

        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 25px;
            margin-top: 40px;
        }

        .card {
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .card:hover {
            transform: translateY(-8px);
            box-shadow: 0 12px 30px rgba(0, 0, 0, 0.15);
        }

        .card-image {
            width: 100%;
            height: 200px;
            background: linear-gradient(135deg, var(--primary-color), var(--primary-light));
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
        }

        .card-body {
            padding: 20px;
        }

        .card-title {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 10px;
            color: var(--text-dark);
        }

        .card-text {
            font-size: 14px;
            color: var(--gray-medium);
            line-height: 1.6;
        }

        /* ==================== フォーム ==================== */
        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--text-dark);
        }

        .required::after {
            content: '*';
            color: var(--error-color);
            margin-left: 4px;
        }

        input[type="email"],
        input[type="text"],
        select,
        textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid var(--gray-light);
            border-radius: 8px;
            font-family: inherit;
            font-size: 14px;
            transition: border-color 0.3s ease;
        }

        input[type="email"]:focus,
        input[type="text"]:focus,
        select:focus,
        textarea:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(0, 113, 227, 0.1);
        }

        textarea {
            resize: vertical;
            min-height: 150px;
        }

        .char-count {
            font-size: 12px;
            color: var(--gray-medium);
            margin-top: 5px;
        }

        .error-message {
            color: var(--error-color);
            font-size: 12px;
            margin-top: 5px;
            display: none;
        }

        .error-message.show {
            display: block;
        }

        .accordion {
            border: 1px solid var(--gray-light);
            border-radius: 8px;
            margin-bottom: 15px;
            overflow: hidden;
        }

        .accordion-header {
            background: var(--text-light);
            padding: 20px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: background 0.3s ease;
            font-weight: 600;
            user-select: none;
        }

        .accordion-header:hover {
            background: var(--gray-light);
        }

        .accordion-icon {
            transition: transform 0.3s ease;
            font-size: 20px;
        }

        .accordion.active .accordion-icon {
            transform: rotate(180deg);
        }

        .accordion-body {
            display: none;
            padding: 20px;
            background: white;
        }

        .accordion.active .accordion-body {
            display: block;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 2000;
            align-items: center;
            justify-content: center;
        }

        .modal.active {
            display: flex;
            animation: fadeIn 0.3s ease;
        }

        .modal-content {
            background: white;
            padding: 40px;
            border-radius: 16px;
            max-width: 500px;
            width: 90%;
            text-align: center;
            animation: slideUp 0.3s ease;
        }

        .modal-icon {
            font-size: 48px;
            margin-bottom: 20px;
        }

        .modal-title {
            font-size: 24px;
            font-weight: 700;
            margin-bottom: 15px;
            color: var(--text-dark);
        }

        .modal-message {
            font-size: 16px;
            color: var(--gray-medium);
            margin-bottom: 30px;
        }

        .spinner {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(0, 113, 227, 0.3);
            border-radius: 50%;
            border-top-color: var(--primary-color);
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .sidebar {
            position: fixed;
            left: 0;
            top: 70px;
            width: 250px;
            background: var(--text-light);
            height: calc(100vh - 70px);
            padding: 30px 20px;
            display: none;
        }

        .sidebar.active {
            display: block;
        }

        .sidebar-item {
            padding: 12px 15px;
            margin-bottom: 8px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            color: var(--text-dark);
        }

        .sidebar-item:hover,
        .sidebar-item.active {
            background: var(--primary-light);
            color: var(--primary-color);
            font-weight: 600;
        }

        .organization-chart {
            background: var(--text-light);
            padding: 40px;
            border-radius: 16px;
            text-align: center;
            margin-bottom: 60px;
        }

        .chart-level {
            margin-bottom: 40px;
        }

        .chart-boxes {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
            margin-top: 20px;
        }

        .chart-box {
            background: white;
            padding: 20px;
            border-radius: 8px;
            min-width: 150px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .chart-box:hover {
            background: var(--primary-light);
            transform: translateY(-4px);
        }

        .connecting-line {
            width: 2px;
            height: 30px;
            background: var(--gray-light);
            margin: -5px auto 0;
        }
    </style>
</head>
<body>
    <!-- ==================== ヘッダー ==================== -->
    <header>
        <div class="logo">
            <div class="logo-img">
                <img src="logo.jpg" alt="心理ゼミロゴ">
            </div>
            <span>Knowledge to Action</span>
        </div>
        <nav id="nav">
            <a href="#" onclick="showPage('home', event)">ホーム</a>
            <a href="#" onclick="showPage('activities', event)">活動内容</a>
            <a href="#" onclick="showPage('organization', event)">組織体制</a>
            <a href="#" onclick="showPage('join', event)">講義・イベント・PJ参加</a>
            <a href="#" onclick="showPage('contact', event)">お問い合わせ</a>
        </nav>
        <div class="hamburger" id="hamburger">
            <span></span>
            <span></span>
            <span></span>
        </div>
    </header>

    <!-- ==================== メインコンテンツ ==================== -->
    <main>
        <!-- ==================== トップページ ==================== -->
        <div id="home" class="page active">
            <!-- ヒーローセクション -->
            <section class="hero">
                <div class="hero-content">
                    <h1>心理ゼミ</h1>
                    <p>学問の実践<br>～知識を行動に変え、未来を発掘する～</p>
                </div>
                <div class="scroll-indicator">
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
                        <polyline points="18 15 12 21 6 15"></polyline>
                    </svg>
                </div>
            </section>

            <!-- 活動セクション -->
            <section class="activities-section">
                <h2 class="section-title">主な活動</h2>
                <div class="activities-list">
                    <div class="activity-item">
                        <div class="activity-image" id="img1">
                            <img src="image1.JPG" alt="心理ゼミ講義" style="width: 100%; height: 100%; object-fit: cover; border-radius: 16px;">
                        </div>
                        <div class="activity-content">
                            <h3>心理ゼミ講義</h3>
                            <p>心理学の論文を基に、今すぐにでも使える心理テクニックを学ぶ講座です。理論と実践を組み合わせた学習経験をお提供します。</p>
                            <a href="#" onclick="showPage('activities', event)" class="btn">詳しく見る</a>
                        </div>
                    </div>
                    <div class="activity-item">
                        abc<div class="activity-image" id="img2">
                            <img src="image2.JPG" alt="部活動" style="width: 100%; height: 100%; object-fit: cover; border-radius: 16px;">
                        </div>abc
                        <div class="activity-content">
                            <h3>部活動</h3>
                            <p>学問の実践の一歩手前で、誰もが気軽に小さな挑戦を始めることができる場です。多様な部活動からお選びいただけます。</p>
                            <a href="#" onclick="showPage('activities', event)" class="btn">詳しく見る</a>
                        </div>
                    </div>
                    <div class="activity-item">
                        <div class="activity-image" id="img3">
                            <img src="image3.JPG" alt="プロジェクト" style="width: 100%; height: 100%; object-fit: cover; border-radius: 16px;">
                        </div>
                        <div class="activity-content">
                            <h3>プロジェクト</h3>
                            <p>心理学の知識に基づいたテクニックをメンバーで共有し、実践するためのプロジェクトです。実践的な学習機会を提供します。</p>
                            <a href="#" onclick="showPage('activities', event)" class="btn">詳しく見る</a>
                        </div>
                    </div>
                </div>
            </section>

            <!-- 魅力ポイント -->
            <section class="features">
                <h2 class="section-title">心理ゼミの魅力</h2>
                <div class="features-grid">
                    <div class="feature-tile">
                        <div class="feature-icon">📚</div>
                        <h4>実践的な学び</h4>
                    </div>
                    <div class="feature-tile">
                        <div class="feature-icon">🎯</div>
                        <h4>多様な活動</h4>
                    </div>
                    <div class="feature-tile">
                        <div class="feature-icon">⭐</div>
                        <h4>自主性の尊重</h4>
                    </div>
                    <div class="feature-tile">
                        <div class="feature-icon">🤝</div>
                        <h4>充実したサポート</h4>
                    </div>
                    <div class="feature-tile">
                        <div class="feature-icon">🌍</div>
                        <h4>コミュニティ形成</h4>
                    </div>
                </div>
            </section>

            <!-- カレンダーセクション -->
            <section class="calendar-section">
                <h2 class="section-title">イベントカレンダー</h2>
                <div class="calendar-container">
                    <div style="width: 100%; background: white; border-radius: 12px; overflow: hidden; box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);">
                        <img src="calendar1.jpg" alt="イベントカレンダー" style="width: 100%; height: auto; display: block;">
                    </div>
                    <a href="calendar1.jpg" download="calendar1.jpg" class="download-btn" style="display: inline-flex; align-items: center; gap: 8px; margin-top: 20px;">
                        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                            <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
                            <polyline points="7 10 12 15 17 10"/>
                            <line x1="12" y1="15" x2="12" y2="3"/>
                        </svg>
                        カレンダーをダウンロード
                    </a>
                </div>
            </section>

            <!-- CTA セクション -->
            <section class="cta-section">
                <h2>心理ゼミに参加しませんか？</h2>
                <p>未来を一緒に発掘しましょう</p>
                <div class="social-links">
                    <a href="https://twitter.com/tan2_rational" target="_blank" class="social-icon" title="X">𝕏</a>
                    <a href="https://instagram.com/tan1_is_rational" target="_blank" class="social-icon" title="Instagram">📷</a>
                </div>
                <a href="#" onclick="showPage('join', event)" class="btn">講義・イベント・PJ参加を見る</a>
            </section>
        </div>

        <!-- ==================== 活動詳細ページ ==================== -->
        <div id="activities" class="page">
            <div class="breadcrumb">
                <a href="#" onclick="showPage('home', event)">ホーム</a> > 活動内容
            </div>

            <div class="content-section">
                <h1 class="section-title">主な活動</h1>

                <!-- 心理ゼミ講義 -->
                <h2 style="font-size: 36px; margin-top: 60px; margin-bottom: 30px;">心理ゼミ講義</h2>
                <div id="img4" style="width: 100%; height: 300px; border-radius: 16px; display: flex; align-items: center; justify-content: center; color: white; margin-bottom: 30px; overflow: hidden;">
                    <img src="image4.JPG" alt="心理ゼミ講義ヘッダー" style="width: 100%; height: 100%; object-fit: cover;">
                </div>
                <p style="font-size: 18px; color: var(--gray-medium); margin-bottom: 20px;">心理学の論文を基に今すぐにでも使える心理テクニックを学ぶ</p>
                <div style="background: var(--text-light); padding: 30px; border-radius: 12px; margin-bottom: 40px;">
                    <h3 style="margin-bottom: 20px;">講義の進め方</h3>
                    <ul style="list-style: none; color: var(--gray-medium);">
                        <li style="margin-bottom: 10px;">📖 毎週の論文紹介と解説</li>
                        <li style="margin-bottom: 10px;">🧠 心理学の基礎から応用まで</li>
                        <li style="margin-bottom: 10px;">💡 実践的なテクニックの習得</li>
                        <li>👥 グループディスカッション</li>
                    </ul>
                    <h3 style="margin-top: 30px; margin-bottom: 20px;">過去の講義テーマ例</h3>
                    <ul style="list-style: none; color: var(--gray-medium);">
                        <li>・認知バイアスと意思決定</li>
                        <li>・人間関係構築のテクニック</li>
                        <li>・動機づけの心理学</li>
                        <li>・ストレスマネジメント</li>
                    </ul>
                    <h3 style="margin-top: 30px; margin-bottom: 10px;">開催頻度</h3>
                    <p>毎週火曜日 19:00～</p>
                </div>

                <!-- 部活 -->
                <h2 style="font-size: 36px; margin-top: 60px; margin-bottom: 30px;">部活</h2>
                <div id="img5" style="width: 100%; height: 300px; border-radius: 16px; display: flex; align-items: center; justify-content: center; color: white; margin-bottom: 30px; overflow: hidden;">
                    <img src="image5.JPG" alt="部活ヘッダー" style="width: 100%; height: 100%; object-fit: cover;">
                </div>
                <p style="font-size: 18px; color: var(--gray-medium); margin-bottom: 40px;">学問の実践の一歩手前で誰もが気軽に小さな挑戦を始めることができる場</p>

                <div class="card-grid">
                    <div class="card">
                        <div class="card-image" id="img6">
                            <img src="image6.JPG" alt="読書部" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div class="card-title">読書部</div>
                            <div class="card-text">心理学関連書籍を読み、理解を深める部活動です。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img7">
                            <img src="image7.JPG" alt="心理シェア部" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div class="card-title">心理シェア部</div>
                            <div class="card-text">日常の心理現象を共有し、学びを深めます。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img8">
                            <img src="image8.JPG" alt="すこやか部" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div class="card-title">すこやか部</div>
                            <div class="card-text">健康とウェルネスに関する活動を行います。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img9">
                            <img src="image9.JPG" alt="ラジオ部" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div class="card-title">ラジオ部</div>
                            <div class="card-text">ラジオ番組の企画・制作・放送に携わります。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img10">
                            <img src="image10.JPG" alt="ふらっと部" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div class="card-title">ふらっと部</div>
                            <div class="card-text">気軽に参加できるカジュアルな部活動です。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img11">
                            <img src="image11.JPG" alt="ノンアルカクテル部" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div class="card-title">ノンアルカクテル部 ー旋ー</div>
                            <div class="card-text">カクテル文化を通じた交流の場です。</div>
                        </div>
                    </div>
                </div>

                <!-- プロジェクト -->
                <h2 style="font-size: 36px; margin-top: 60px; margin-bottom: 30px;">プロジェクト</h2>
                <div id="img12" style="width: 100%; height: 300px; border-radius: 16px; display: flex; align-items: center; justify-content: center; color: white; margin-bottom: 30px; overflow: hidden;">
                    <img src="image12.JPG" alt="プロジェクトヘッダー" style="width: 100%; height: 100%; object-fit: cover;">
                </div>
                <p style="font-size: 18px; color: var(--gray-medium); margin-bottom: 40px;">心理学の知識に基づいたテクニックをメンバーで共有し、実践するためのプロジェクト</p>

                <div class="card-grid">
                    <div class="card">
                        <div class="card-image" id="img13">
                            <img src="image13.JPG" alt="実験再現プロジェクト" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div class="card-title">実験再現プロジェクト</div>
                            <div class="card-text">心理学の著名な実験を再現・検証します。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img14">
                            <img src="image14.JPG" alt="運動プロジェクト" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div class="card-title">運動プロジェクト</div>
                            <div class="card-text">身体活動と心理的効果の関連を探ります。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img15">
                            <img src="image15.JPG" alt="瞑想習慣化プロジェクト" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div class="card-title">瞑想習慣化プロジェクト</div>
                            <div class="card-text">瞑想の習慣化と心理的変化を研究します。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img16">
                            <img src="image16.JPG" alt="快眠プロジェクト" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div class="card-title">快眠プロジェクト</div>
                            <div class="card-text">睡眠の質向上に向けた心理学的アプローチ。</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- ==================== 組織紹介ページ ==================== -->
        <div id="organization" class="page">
            <div class="breadcrumb">
                <a href="#" onclick="showPage('home', event)">ホーム</a> > 組織体制
            </div>

            <div class="content-section">
                <h1 class="section-title">組織体制</h1>

                <!-- 組織図 -->
                <div class="organization-chart">
                    <h3 style="margin-bottom: 30px;">北大心理ゼミの構成</h3>
                    <div class="chart-level">
                        <div class="chart-boxes">
                            <div class="chart-box" onclick="document.querySelector('.role-section').scrollIntoView({behavior:'smooth'})">
                                北大心理ゼミ
                            </div>
                        </div>
                        <div class="connecting-line"></div>
                    </div>
                    <div class="chart-level">
                        <div class="chart-boxes">
                            <div class="chart-box">心理ゼミ運営部</div>
                            <div class="chart-box">心理ゼミ企画部</div>
                            <div class="chart-box">基層メンバー</div>
                        </div>
                    </div>
                </div>

                <!-- 運営部 -->
                <h2 style="font-size: 36px; margin-top: 60px; margin-bottom: 30px;" class="role-section">心理ゼミ運営部</h2>
                <div id="img17" style="width: 100%; height: 300px; border-radius: 16px; display: flex; align-items: center; justify-content: center; color: white; margin-bottom: 30px; overflow: hidden;">
                    <img src="image17.JPG" alt="心理ゼミ運営部ヘッダー" style="width: 100%; height: 100%; object-fit: cover;">
                </div>
                <div style="background: var(--text-light); padding: 30px; border-radius: 12px; margin-bottom: 40px;">
                    <h3 style="margin-bottom: 20px;">何のためのチーム？</h3>
                    <p style="color: var(--gray-medium); line-height: 1.8;">北大心理ゼミの「理念」を達成する上で、様々な課題が存在します。これらの課題を解決し、心理ゼミの発展と持続を願うチームです。</p>
                    <h3 style="margin-top: 30px; margin-bottom: 20px;">何をするチーム？</h3>
                    <p style="color: var(--gray-medium); margin-bottom: 20px;">以下の5つの役職から構成されます。</p>
                </div>

                <div class="card-grid">
                    <div class="card">
                        <div class="card-image" id="img24">
                            <img src="image24.JPG" alt="代表" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div style="font-size: 24px; font-weight: 700; color: var(--primary-color); margin-bottom: 10px;">1</div>
                            <div class="card-title">代表</div>
                            <p style="font-size: 12px; color: var(--primary-color); margin-bottom: 10px;">運営部及び心理ゼミの長</p>
                            <div class="card-text">運営部及び心理ゼミの長であり、顔。心理ゼミ全体のマネジメントや団体の方向性の決定を司る。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img18">
                            <img src="image18.JPG" alt="秘書" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div style="font-size: 24px; font-weight: 700; color: var(--primary-color); margin-bottom: 10px;">2</div>
                            <div class="card-title">秘書</div>
                            <p style="font-size: 12px; color: var(--primary-color); margin-bottom: 10px;">「時間・行動」の課題を解決</p>
                            <div class="card-text">スケジュールやタスクを取りまとめ、活動全体のスピードをコントロール。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img19">
                            <img src="image19.JPG" alt="統括" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div style="font-size: 24px; font-weight: 700; color: var(--primary-color); margin-bottom: 10px;">3</div>
                            <div class="card-title">統括</div>
                            <p style="font-size: 12px; color: var(--primary-color); margin-bottom: 10px;">「多様性・仲間」の課題を解決</p>
                            <div class="card-text">コミュニケーションを促進し、人と人の繋がりを作ります。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img20">
                            <img src="image20.JPG" alt="広報" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div style="font-size: 24px; font-weight: 700; color: var(--primary-color); margin-bottom: 10px;">4</div>
                            <div class="card-title">広報</div>
                            <p style="font-size: 12px; color: var(--primary-color); margin-bottom: 10px;">「情報・表現」の課題を解決</p>
                            <div class="card-text">情報を取りまとめ、創造力を使ってツールや手順に工夫を凝らします。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-image" id="img21">
                            <img src="image21.JPG" alt="補佐" style="width: 100%; height: 100%; object-fit: cover;">
                        </div>
                        <div class="card-body">
                            <div style="font-size: 24px; font-weight: 700; color: var(--primary-color); margin-bottom: 10px;">5</div>
                            <div class="card-title">補佐</div>
                            <p style="font-size: 12px; color: var(--primary-color); margin-bottom: 10px;">「運営部」の課題を解決</p>
                            <div class="card-text">多角的な視点から、様々な問題や困難にサポートします。</div>
                        </div>
                    </div>
                </div>

                <!-- 企画部 -->
                <h2 style="font-size: 36px; margin-top: 60px; margin-bottom: 30px;">心理ゼミ企画部</h2>
                <div id="img22" style="width: 100%; height: 300px; border-radius: 16px; display: flex; align-items: center; justify-content: center; color: white; margin-bottom: 30px; overflow: hidden;">
                    <img src="image22.JPG" alt="心理ゼミ企画部ヘッダー" style="width: 100%; height: 100%; object-fit: cover;">
                </div>
                <p style="font-size: 18px; color: var(--gray-medium); margin-bottom: 40px;">PJや部活を運営するアクティブなメンバーの集合体</p>

                <!-- 基層メンバー -->
                <h2 style="font-size: 36px; margin-top: 60px; margin-bottom: 30px;">基層メンバー</h2>
                <div id="img23" style="width: 100%; height: 300px; border-radius: 16px; display: flex; align-items: center; justify-content: center; color: white; margin-bottom: 30px; overflow: hidden;">
                    <img src="image23.JPG" alt="基層メンバーヘッダー" style="width: 100%; height: 100%; object-fit: cover;">
                </div>
                <div style="background: var(--text-light); padding: 30px; border-radius: 12px;">
                    <p style="color: var(--gray-medium); margin-bottom: 15px;">心理ゼミにて開催されるPJやイベントへの参加者</p>
                    <p style="color: var(--gray-medium); margin-bottom: 10px;">部員数（随時更新）</p>
                    <p style="color: var(--text-dark); font-weight: 600;">北海道大学の学生が中心に活動しています</p>
                </div>
            </div>
        </div>

        <!-- ==================== 講義・イベント・PJ参加ページ ==================== -->
        <div id="join" class="page">
            <div class="breadcrumb">
                <a href="#" onclick="showPage('home', event)">ホーム</a> > 講義・イベント・PJ参加
            </div>

            <div class="content-section">
                <h1 class="section-title">講義・イベント・PJ参加</h1>

                <div style="width: 100%; height: 300px; background: linear-gradient(135deg, var(--primary-color), var(--primary-light)); border-radius: 16px; display: flex; align-items: center; justify-content: center; color: white; margin-bottom: 30px;">
                    ヘッダー画像を挿入
                </div>

                <div class="card-grid">
                    <div class="card">
                        <div class="card-body">
                            <div class="card-title">初心者歓迎</div>
                            <div class="card-text">常に活動内容は変化し続けているのでむしろほとんどが初心者です。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-body">
                            <div class="card-title">理念への共感</div>
                            <div class="card-text">心理学への興味や「学問の実践」という理念に共感できる方もお待ちしています。</div>
                        </div>
                    </div>
                    <div class="card">
                        <div class="card-body">
                            <div class="card-title">経験不問</div>
                            <div class="card-text">特別な経験やスキルは不要です。あっても邪魔なだけです。</div>
                        </div>
                    </div>
                </div>

                <!-- イベント情報 -->
                <h2 style="font-size: 36px; margin-top: 60px; margin-bottom: 30px;">定期イベント</h2>
                
                <div style="background: var(--text-light); padding: 30px; border-radius: 12px; margin-bottom: 40px;">
                    <h3 style="margin-bottom: 20px;">心理学講義</h3>
                    <p style="color: var(--gray-medium); margin-bottom: 20px;">定期的に開催される心理学の講座です。初心者から上級者まで参加できます。</p>
                    
                    <h3 style="margin-top: 30px; margin-bottom: 20px;">部活動</h3>
                    <p style="color: var(--gray-medium); margin-bottom: 20px;">各部活ごとに定期開催されています。興味のある部活に自由に参加できます。</p>
                </div>

                <!-- 新歓イベント -->
                <h3 style="font-size: 24px; margin-bottom: 20px;">新歓期イベント</h3>
                <div class="accordion">
                    <div class="accordion-header">
                        <span>オンライン新歓</span>
                        <span class="accordion-icon">＋</span>
                    </div>
                    <div class="accordion-body">
                        <p>オンラインで心理ゼミについて知ることができるイベントです。気軽にご参加ください。</p>
                    </div>
                </div>
                <div class="accordion">
                    <div class="accordion-header">
                        <span>履修相談会</span>
                        <span class="accordion-icon">＋</span>
                    </div>
                    <div class="accordion-body">
                        <p>心理学や関連科目の履修についてのアドバイスを受けられます。</p>
                    </div>
                </div>
                <div class="accordion">
                    <div class="accordion-header">
                        <span>新歓パーティ</span>
                        <span class="accordion-icon">＋</span>
                    </div>
                    <div class="accordion-body">
                        <p>既存メンバーと新入生が交流できるカジュアルなイベントです。</p>
                    </div>
                </div>
                <div class="accordion">
                    <div class="accordion-header">
                        <span>長橋合宿</span>
                        <span class="accordion-icon">＋</span>
                    </div>
                    <div class="accordion-body">
                        <p>年に一度の合宿で、深い交流と学びの時間を共有します。</p>
                    </div>
                </div>

                <!-- FAQ -->
                <h2 style="font-size: 36px; margin-top: 60px; margin-bottom: 30px;">よくある質問</h2>
                
                <div class="accordion">
                    <div class="accordion-header">
                        <span>心理学の知識がなくても参加できますか？</span>
                        <span class="accordion-icon">＋</span>
                    </div>
                    <div class="accordion-body">
                        <p>はい、どなたでも参加できます。開催されるイベントは心理学に関わるものに留まりません。初心者向けの講座も多数用意しています。</p>
                    </div>
                </div>
                <div class="accordion">
                    <div class="accordion-header">
                        <span>活動頻度はどのくらいですか？</span>
                        <span class="accordion-icon">＋</span>
                    </div>
                    <div class="accordion-body">
                        <p>定例会、講義、各部活動があり、参加したい活動を選択できます。無理のないペースでご参加ください。</p>
                    </div>
                </div>
                <div class="accordion">
                    <div class="accordion-header">
                        <span>費用はかかりますか？</span>
                        <span class="accordion-icon">＋</span>
                    </div>
                    <div class="accordion-body">
                        <p>参加するイベントによります。基本的な活動は無料ですが、合宿や特別イベントについては別途費用が発生する場合があります。</p>
                    </div>
                </div>
                <div class="accordion">
                    <div class="accordion-header">
                        <span>北大生以外でも参加できますか？</span>
                        <span class="accordion-icon">＋</span>
                    </div>
                    <div class="accordion-body">
                        <p>基本的には北大生を対象としていますが、ご質問があればお気軽にお問い合わせください。</p>
                    </div>
                </div>

                <!-- 次のステップ -->
                <div style="text-align: center; margin-top: 60px;">
                    <h3 style="font-size: 28px; margin-bottom: 30px;">質問やご不明な点はお気軽にお尋ねください</h3>
                    <a href="#" onclick="showPage('contact', event)" class="btn" style="padding: 15px 40px; font-size: 16px;">お問い合わせ</a>
                </div>

                <div style="text-align: center; margin-top: 40px;">
                    <h4 style="margin-bottom: 20px;">SNSフォロー</h4>
                    <div class="social-links" style="justify-content: center;">
                        <a href="https://twitter.com/tan2_rational" target="_blank" class="social-icon" title="X">𝕏</a>
                        <a href="https://instagram.com/tan1_is_rational" target="_blank" class="social-icon" title="Instagram">📷</a>
                    </div>
                </div>
            </div>
        </div>

        <!-- ==================== お問い合わせページ ==================== -->
        <div id="contact" class="page">
            <div class="breadcrumb">
                <a href="#" onclick="showPage('home', event)">ホーム</a> > お問い合わせ
            </div>

            <div class="content-section" style="max-width: 700px;">
                <h1 class="section-title">お問い合わせ</h1>

                <!-- フォーム -->
                <form id="contactForm" style="background: var(--text-light); padding: 40px; border-radius: 12px;">
                    <div class="form-group">
                        <label for="email" class="required">メールアドレス</label>
                        <input type="email" id="email" name="email" placeholder="your-email@example.com" required>
                        <div class="error-message" id="emailError"></div>
                    </div>

                    <div class="form-group">
                        <label for="affiliation" class="required">所属</label>
                        <select id="affiliation" name="affiliation" required>
                            <option value="">選択してください</option>
                            <option value="hokudai-student">北海道大学学生</option>
                            <option value="other-student">他大学学生</option>
                            <option value="highschool">高校生</option>
                            <option value="company">企業</option>
                            <option value="other">その他</option>
                        </select>
                        <div class="error-message" id="affiliationError"></div>
                    </div>

                    <div class="form-group">
                        <label for="message" class="required">お問い合わせ内容</label>
                        <textarea id="message" name="message" placeholder="お問い合わせ内容をご記入ください" maxlength="1000" required></textarea>
                        <div class="char-count"><span id="charCount">0</span>/1000</div>
                        <div class="error-message" id="messageError"></div>
                    </div>

                    <button type="submit" class="btn" style="width: 100%; padding: 15px; font-size: 16px;">送信する</button>
                </form>

                <!-- その他の連絡方法 -->
                <div style="margin-top: 60px;">
                    <h2 style="font-size: 28px; margin-bottom: 30px;">その他の連絡方法</h2>
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
                        <a href="https://twitter.com/tan2_rational" target="_blank" style="display: flex; align-items: center; gap: 15px; padding: 20px; background: var(--text-light); border-radius: 12px; text-decoration: none; color: var(--text-dark); transition: all 0.3s ease;" onmouseover="this.style.background='var(--primary-light)'" onmouseout="this.style.background='var(--text-light)'">
                            <div style="font-size: 32px;">𝕏</div>
                            <div>
                                <div style="font-weight: 600;">X (Twitter)</div>
                                <div style="font-size: 12px; color: var(--gray-medium);">@tan2_rational</div>
                            </div>
                        </a>
                        <a href="https://instagram.com/tan1_is_rational" target="_blank" style="display: flex; align-items: center; gap: 15px; padding: 20px; background: var(--text-light); border-radius: 12px; text-decoration: none; color: var(--text-dark); transition: all 0.3s ease;" onmouseover="this.style.background='var(--primary-light)'" onmouseout="this.style.background='var(--text-light)'">
                            <div style="font-size: 32px;">📷</div>
                            <div>
                                <div style="font-weight: 600;">Instagram</div>
                                <div style="font-size: 12px; color: var(--gray-medium);">@tan1_is_rational</div>
                            </div>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <!-- ==================== フッター ==================== -->
    <footer>
        <div class="footer-content">
            <div class="footer-section">
                <h4>心理ゼミについて</h4>
                <p>北海道大学心理ゼミは、学問の実践を通じて、学生の成長と未来の発掘をサポートします。</p>
            </div>
            <div class="footer-section">
                <h4>ナビゲーション</h4>
                <ul>
                    <li><a href="#" onclick="showPage('home', event)">ホーム</a></li>
                    <li><a href="#" onclick="showPage('activities', event)">活動内容</a></li>
                    <li><a href="#" onclick="showPage('organization', event)">組織体制</a></li>
                    <li><a href="#" onclick="showPage('join', event)">講義・イベント・PJ参加</a></li>
                    <li><a href="#" onclick="showPage('contact', event)">お問い合わせ</a></li>
                </ul>
            </div>
            <div class="footer-section">
                <h4>SNS</h4>
                <ul>
                    <li><a href="https://twitter.com/tan2_rational" target="_blank">X (Twitter)</a></li>
                    <li><a href="https://instagram.com/tan1_is_rational" target="_blank">Instagram</a></li>
                </ul>
            </div>
        </div>
        <div class="copyright">
            <p>&copy; 2026 北大心理ゼミ All rights reserved.</p>
        </div>
    </footer>

    <!-- ==================== モーダル ==================== -->
    <div id="successModal" class="modal">
        <div class="modal-content">
            <div class="modal-icon">✅</div>
            <div class="modal-title">送信完了</div>
            <div class="modal-message">お問い合わせをお送りいただきありがとうございます。<br>確認後、ご連絡させていただきます。</div>
            <button class="btn" onclick="closeModal()">閉じる</button>
        </div>
    </div>

    <script>
        // ==================== ナビゲーション ==================== 
        const hamburger = document.getElementById('hamburger');
        const nav = document.getElementById('nav');

        hamburger.addEventListener('click', () => {
            nav.classList.toggle('active');
        });

        // ==================== ページ切り替え ==================== 
        function showPage(pageId, event) {
            if (event) event.preventDefault();
            
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            
            document.getElementById(pageId).classList.add('active');
            nav.classList.remove('active');
            window.scrollTo(0, 0);
        }

        // ==================== ヘッダースクロール効果 ==================== 
        window.addEventListener('scroll', () => {
            const header = document.querySelector('header');
            if (window.scrollY > 50) {
                header.classList.add('scrolled');
            } else {
                header.classList.remove('scrolled');
            }
        });

        // ==================== スクロールアニメーション ==================== 
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -100px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = '1';
                    entry.target.style.transform = 'translateY(0)';
                }
            });
        }, observerOptions);

        document.querySelectorAll('.activity-item, .feature-tile').forEach(el => {
            observer.observe(el);
        });

        // ==================== アコーディオン ==================== 
        document.querySelectorAll('.accordion-header').forEach(header => {
            header.addEventListener('click', () => {
                const accordion = header.closest('.accordion');
                accordion.classList.toggle('active');
            });
        });

        // ==================== フォーム処理 ==================== 
        const contactForm = document.getElementById('contactForm');
        const charCount = document.getElementById('charCount');
        const messageField = document.getElementById('message');

        messageField.addEventListener('input', () => {
            charCount.textContent = messageField.value.length;
        });

        contactForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            
            // バリデーション
            let isValid = true;
            const email = document.getElementById('email').value;
            const affiliation = document.getElementById('affiliation').value;
            const message = document.getElementById('message').value;

            // メール検証
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (!emailRegex.test(email)) {
                document.getElementById('emailError').textContent = '有効なメールアドレスを入力してください';
                document.getElementById('emailError').classList.add('show');
                isValid = false;
            } else {
                document.getElementById('emailError').classList.remove('show');
            }

            // 所属検証
            if (!affiliation) {
                document.getElementById('affiliationError').textContent = '所属を選択してください';
                document.getElementById('affiliationError').classList.add('show');
                isValid = false;
            } else {
                document.getElementById('affiliationError').classList.remove('show');
            }

            // メッセージ検証
            if (!message || message.length === 0) {
                document.getElementById('messageError').textContent = 'お問い合わせ内容を入力してください';
                document.getElementById('messageError').classList.add('show');
                isValid = false;
            } else {
                document.getElementById('messageError').classList.remove('show');
            }

            if (isValid) {
                // フォーム送信（実際のサーバー処理は省略）
                const submitBtn = contactForm.querySelector('button');
                submitBtn.innerHTML = '<span class="spinner"></span> 送信中...';
                submitBtn.disabled = true;

                setTimeout(() => {
                    document.getElementById('successModal').classList.add('active');
                    contactForm.reset();
                    charCount.textContent = '0';
                    submitBtn.innerHTML = '送信する';
                    submitBtn.disabled = false;
                }, 1000);
            }
        });

        function closeModal() {
            document.getElementById('successModal').classList.remove('active');
        }

        // モーダルの背景をクリックして閉じる
        document.getElementById('successModal').addEventListener('click', (e) => {
            if (e.target === document.getElementById('successModal')) {
                closeModal();
            }
        });
    </script>
</body>
</html>
