Сайт в раработке 
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ITCoffee | Архитекторы цифрового будущего</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #0A0A0A;
            --secondary: #00F5FF;
            --accent: #FF2E63;
            --neon-blue: #00F5FF;
            --neon-pink: #FF2E63;
            --neon-purple: #9D4EDD;
            --dark-bg: #0A0A0A;
            --card-bg: rgba(30, 30, 30, 0.7);
            --glass: rgba(255, 255, 255, 0.05);
            --glass-border: rgba(255, 255, 255, 0.1);
            --gradient-primary: linear-gradient(135deg, #00F5FF 0%, #9D4EDD 50%, #FF2E63 100%);
            --gradient-secondary: linear-gradient(135deg, #FF2E63 0%, #00F5FF 100%);
            --neon-glow-blue: 0 0 20px rgba(0, 245, 255, 0.7);
            --neon-glow-pink: 0 0 20px rgba(255, 46, 99, 0.7);
            --section-spacing: 120px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            background: var(--dark-bg);
            color: white;
            line-height: 1.6;
            overflow-x: hidden;
            position: relative;
        }

        .loader {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--dark-bg);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: opacity 0.5s ease, visibility 0.5s ease;
        }

        .loader.hidden {
            opacity: 0;
            visibility: hidden;
        }

        .loader-content {
            text-align: center;
        }

        .loader-logo {
            font-size: 3rem;
            font-weight: 900;
            margin-bottom: 20px;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .loader-bar {
            width: 200px;
            height: 4px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 4px;
            overflow: hidden;
            margin: 0 auto;
        }

        .loader-progress {
            height: 100%;
            width: 0%;
            background: var(--gradient-primary);
            border-radius: 4px;
            transition: width 0.05s linear;
        }

        .animated-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: 
                radial-gradient(circle at 20% 30%, rgba(0, 245, 255, 0.05) 0%, transparent 50%),
                radial-gradient(circle at 80% 70%, rgba(255, 46, 99, 0.05) 0%, transparent 50%),
                radial-gradient(circle at 40% 80%, rgba(157, 78, 221, 0.05) 0%, transparent 50%);
            animation: bgPulse 15s ease-in-out infinite;
        }

        @keyframes bgPulse {
            0%, 100% { opacity: 0.5; }
            50% { opacity: 1; }
        }

        .grid-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(0, 245, 255, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 245, 255, 0.03) 1px, transparent 1px);
            background-size: 50px 50px;
            z-index: -1;
            animation: gridMove 20s linear infinite;
        }

        @keyframes gridMove {
            0% { transform: translate(0, 0); }
            100% { transform: translate(50px, 50px); }
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 40px;
        }

        nav {
            position: fixed;
            top: 0;
            width: 100%;
            background: rgba(10, 10, 10, 0.9);
            backdrop-filter: blur(20px);
            z-index: 1000;
            padding: 20px 0;
            border-bottom: 1px solid var(--glass-border);
            transition: all 0.3s ease;
        }

        .nav-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 28px;
            font-weight: 900;
            color: white;
            text-decoration: none;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .logo-dot {
            width: 8px;
            height: 8px;
            background: var(--gradient-primary);
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        .nav-links {
            display: flex;
            gap: 40px;
            list-style: none;
        }

        .nav-links a {
            color: white;
            text-decoration: none;
            font-weight: 600;
            position: relative;
            padding: 8px 0;
            transition: all 0.3s ease;
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--gradient-primary);
            transition: width 0.3s ease;
        }

        .nav-links a:hover {
            color: var(--neon-blue);
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        .mobile-menu-btn {
            display: none;
            background: none;
            border: none;
            color: white;
            font-size: 1.5rem;
            cursor: pointer;
            z-index: 1001;
        }

        .mobile-menu {
            position: fixed;
            top: 0;
            right: -100%;
            width: 300px;
            height: 100vh;
            background: rgba(10, 10, 10, 0.95);
            backdrop-filter: blur(20px);
            z-index: 1000;
            padding: 100px 40px 40px;
            transition: right 0.4s ease;
            border-left: 1px solid var(--glass-border);
        }

        .mobile-menu.active {
            right: 0;
        }

        .mobile-nav-links {
            list-style: none;
            display: flex;
            flex-direction: column;
            gap: 30px;
        }

        .mobile-nav-links a {
            color: white;
            text-decoration: none;
            font-size: 1.2rem;
            font-weight: 600;
            padding: 10px 0;
            display: block;
            border-bottom: 1px solid var(--glass-border);
            transition: color 0.3s ease;
        }

        .mobile-nav-links a:hover {
            color: var(--neon-blue);
        }

        .menu-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            z-index: 999;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
        }

        .menu-overlay.active {
            opacity: 1;
            visibility: visible;
        }

        .hero {
            min-height: 100vh;
            display: flex;
            align-items: center;
            position: relative;
            overflow: hidden;
            padding-top: 80px;
        }

        .hero-content {
            position: relative;
            z-index: 2;
            max-width: 800px;
        }

        .hero-badge {
            display: inline-flex;
            align-items: center;
            gap: 10px;
            background: rgba(0, 245, 255, 0.1);
            color: var(--neon-blue);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 30px;
            border: 1px solid rgba(0, 245, 255, 0.3);
        }

        .hero-title {
            font-size: 4.5rem;
            font-weight: 900;
            line-height: 1.1;
            margin-bottom: 30px;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .hero-subtitle {
            font-size: 1.3rem;
            color: rgba(255, 255, 255, 0.8);
            margin-bottom: 40px;
            line-height: 1.6;
        }

        .hero-stats {
            display: flex;
            gap: 40px;
            margin-top: 50px;
        }

        .stat {
            text-align: center;
        }

        .stat-value {
            font-size: 2.5rem;
            font-weight: 800;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 5px;
            background-clip: text;
        }

        .stat-label {
            font-size: 0.9rem;
            color: rgba(255, 255, 255, 0.7);
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn {
            display: inline-flex;
            align-items: center;
            gap: 10px;
            padding: 16px 32px;
            background: var(--gradient-primary);
            color: white;
            text-decoration: none;
            border-radius: 8px;
            font-weight: 700;
            transition: all 0.3s ease;
            border: none;
            cursor: pointer;
            box-shadow: var(--neon-glow-blue);
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0, 245, 255, 0.4);
        }

        .btn-outline {
            background: transparent;
            border: 2px solid;
            border-image: var(--gradient-primary) 1;
            color: white;
            box-shadow: none;
        }

        .btn-outline:hover {
            background: var(--gradient-primary);
            color: white;
        }

        section {
            padding: var(--section-spacing) 0;
        }

        .section-header {
            text-align: center;
            margin-bottom: 80px;
        }

        .section-label {
            display: inline-block;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 2px;
            font-size: 0.9rem;
            margin-bottom: 15px;
            background-clip: text;
        }

        .section-title {
            font-size: 3.5rem;
            font-weight: 800;
            margin-bottom: 20px;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .section-subtitle {
            font-size: 1.2rem;
            color: rgba(255, 255, 255, 0.7);
            max-width: 600px;
            margin: 0 auto;
        }

        .projects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
            gap: 30px;
            margin-top: 60px;
        }

        .project-card {
            background: var(--card-bg);
            border-radius: 16px;
            overflow: hidden;
            transition: all 0.4s ease;
            border: 1px solid var(--glass-border);
            backdrop-filter: blur(10px);
            position: relative;
        }

        .project-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: var(--gradient-primary);
            transform: scaleX(0);
            transition: transform 0.4s ease;
        }

        .project-card:hover::before {
            transform: scaleX(1);
        }

        .project-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
        }

        .project-image {
            height: 220px;
            overflow: hidden;
            position: relative;
        }

        .project-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease;
        }

        .project-card:hover .project-image img {
            transform: scale(1.1);
        }

        .project-content {
            padding: 30px;
        }

        .project-category {
            display: inline-block;
            background: rgba(0, 245, 255, 0.1);
            color: var(--neon-blue);
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            margin-bottom: 15px;
        }

        .project-title {
            font-size: 1.4rem;
            font-weight: 700;
            margin-bottom: 15px;
            color: white;
        }

        .project-description {
            color: rgba(255, 255, 255, 0.7);
            margin-bottom: 20px;
            line-height: 1.6;
        }

        .project-tech {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }

        .tech-tag {
            background: rgba(255, 255, 255, 0.1);
            color: rgba(255, 255, 255, 0.8);
            padding: 4px 12px;
            border-radius: 12px;
            font-size: 0.8rem;
        }

        .tech-showcase {
            background: rgba(30, 30, 30, 0.5);
            border-radius: 24px;
            padding: 80px 60px;
            margin-top: 80px;
            border: 1px solid var(--glass-border);
        }

        .tech-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 40px;
            margin-top: 60px;
        }

        .tech-card {
            background: var(--card-bg);
            padding: 40px 30px;
            border-radius: 16px;
            text-align: center;
            transition: all 0.3s ease;
            border: 1px solid var(--glass-border);
        }

        .tech-card:hover {
            transform: translateY(-5px);
            border-color: var(--neon-blue);
            box-shadow: var(--neon-glow-blue);
        }

        .tech-icon {
            font-size: 3rem;
            margin-bottom: 20px;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .tech-name {
            font-size: 1.3rem;
            font-weight: 700;
            margin-bottom: 15px;
            color: white;
        }

        .tech-description {
            color: rgba(255, 255, 255, 0.7);
            line-height: 1.6;
        }

        .contact-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 80px;
            margin-top: 60px;
        }

        .contact-info {
            display: flex;
            flex-direction: column;
            gap: 30px;
        }

        .contact-item {
            display: flex;
            align-items: flex-start;
            gap: 20px;
        }

        .contact-icon {
            font-size: 1.5rem;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .contact-details h4 {
            font-size: 1.2rem;
            margin-bottom: 8px;
            font-weight: 600;
        }

        .contact-details p {
            color: rgba(255, 255, 255, 0.7);
        }

        .social-links {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }

        .social-link {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 50px;
            height: 50px;
            background: var(--card-bg);
            color: white;
            border-radius: 50%;
            transition: all 0.3s ease;
            text-decoration: none;
            border: 1px solid var(--glass-border);
        }

        .social-link:hover {
            background: var(--gradient-primary);
            transform: translateY(-3px);
        }

        .contact-form {
            display: flex;
            flex-direction: column;
            gap: 25px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .form-group label {
            font-weight: 600;
            font-size: 0.95rem;
        }

        .form-control {
            padding: 15px 20px;
            background: var(--card-bg);
            border: 1px solid var(--glass-border);
            border-radius: 8px;
            color: white;
            font-size: 1rem;
            transition: all 0.3s ease;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--neon-blue);
            box-shadow: 0 0 0 2px rgba(0, 245, 255, 0.2);
        }

        textarea.form-control {
            min-height: 150px;
            resize: vertical;
        }

        .form-error {
            color: var(--neon-pink);
            font-size: 0.85rem;
            margin-top: 5px;
            display: none;
        }

        .form-success {
            background: rgba(0, 245, 255, 0.1);
            color: var(--neon-blue);
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            margin-top: 20px;
            display: none;
        }

        footer {
            background: rgba(10, 10, 10, 0.9);
            padding: 80px 0 30px;
            border-top: 1px solid var(--glass-border);
        }

        .footer-content {
            display: grid;
            grid-template-columns: 2fr 1fr 1fr 1fr;
            gap: 50px;
            margin-bottom: 60px;
        }

        .footer-info h3 {
            font-size: 24px;
            font-weight: 800;
            margin-bottom: 20px;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .footer-info p {
            color: rgba(255, 255, 255, 0.7);
            line-height: 1.6;
            margin-bottom: 30px;
        }

        .footer-column h4 {
            font-size: 1.2rem;
            margin-bottom: 25px;
            font-weight: 700;
        }

        .footer-links {
            list-style: none;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .footer-links a {
            color: rgba(255, 255, 255, 0.7);
            text-decoration: none;
            transition: color 0.3s ease;
        }

        .footer-links a:hover {
            color: var(--neon-blue);
        }

        .copyright {
            text-align: center;
            padding-top: 30px;
            border-top: 1px solid var(--glass-border);
            color: rgba(255, 255, 255, 0.7);
            font-size: 0.9rem;
        }

        .scroll-to-top {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 50px;
            height: 50px;
            background: var(--gradient-primary);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            text-decoration: none;
            box-shadow: var(--neon-glow-blue);
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
            z-index: 99;
        }

        .scroll-to-top.active {
            opacity: 1;
            visibility: visible;
        }

        .scroll-to-top:hover {
            transform: translateY(-5px);
        }

        /* Новые стили для дополнительных разделов */
        .services-tabs {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 50px;
            flex-wrap: wrap;
        }

        .service-tab {
            padding: 15px 30px;
            background: var(--card-bg);
            border: 1px solid var(--glass-border);
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
        }

        .service-tab.active {
            background: var(--gradient-primary);
            color: white;
            box-shadow: var(--neon-glow-blue);
        }

        .service-tab:hover:not(.active) {
            border-color: var(--neon-blue);
        }

        .service-content {
            display: none;
        }

        .service-content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .coming-soon {
            text-align: center;
            padding: 60px 0;
            background: var(--card-bg);
            border-radius: 16px;
            border: 1px solid var(--glass-border);
        }

        .coming-soon-icon {
            font-size: 4rem;
            margin-bottom: 20px;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        @media (max-width: 1200px) {
            .container {
                padding: 0 30px;
            }
            .hero-title {
                font-size: 3.5rem;
            }
            .footer-content {
                grid-template-columns: 1fr 1fr;
            }
        }

        @media (max-width: 992px) {
            .contact-grid {
                grid-template-columns: 1fr;
                gap: 50px;
            }
            .tech-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            .projects-grid {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }
            .mobile-menu-btn {
                display: block;
            }
            .hero-title {
                font-size: 2.5rem;
            }
            .section-title {
                font-size: 2.5rem;
            }
            .tech-grid {
                grid-template-columns: 1fr;
            }
            .footer-content {
                grid-template-columns: 1fr;
            }
            .container {
                padding: 0 20px;
            }
            .hero-stats {
                flex-direction: column;
                gap: 20px;
            }
            .tech-showcase {
                padding: 40px 20px;
            }
            .hero {
                padding-top: 100px;
            }
            .services-tabs {
                flex-direction: column;
                align-items: center;
            }
            .service-tab {
                width: 100%;
                text-align: center;
            }
        }
    </style>
</head>
<body>
    <div class="loader" id="pageLoader">
        <div class="loader-content">
            <div class="loader-logo">ITCoffee</div>
            <div class="loader-bar">
                <div class="loader-progress" id="loaderProgress"></div>
            </div>
        </div>
    </div>
    <div class="animated-bg"></div>
    <div class="grid-overlay"></div>
    <nav>
        <div class="container nav-container">
            <a href="#" class="logo">
                ITCoffee
                <div class="logo-dot"></div>
            </a>
            <ul class="nav-links">
                <li><a href="#projects">Проекты</a></li>
                <li><a href="#tech">Технологии</a></li>
                <li><a href="#services">Услуги</a></li>
                <li><a href="#contact">Контакты</a></li>
            </ul>
            <button class="mobile-menu-btn" id="mobileMenuBtn">
                <i class="fas fa-bars"></i>
            </button>
        </div>
    </nav>

    <div class="mobile-menu" id="mobileMenu">
        <ul class="mobile-nav-links">
            <li><a href="#projects">Проекты</a></li>
            <li><a href="#tech">Технологии</a></li>
            <li><a href="#services">Услуги</a></li>
            <li><a href="#contact">Контакты</a></li>
        </ul>
    </div>
    <div class="menu-overlay" id="menuOverlay"></div>

    <section class="hero">
        <div class="container">
            <div class="hero-content">
                <div class="hero-badge">
                    <i class="fas fa-rocket"></i>
                    Инновации с 2010 года
                </div>
                <h1 class="hero-title">Архитекторы цифрового будущего</h1>
                <p class="hero-subtitle">Создаем технологии, которые переопределяют возможности человечества. От квантовых вычислений до нейроинтерфейсов — мы строим будущее, о котором другие только мечтают.</p>
                <div style="display: flex; gap: 20px; flex-wrap: wrap;">
                    <a href="#projects" class="btn">Исследовать проекты <i class="fas fa-arrow-right"></i></a>
                    <a href="#contact" class="btn btn-outline">Присоединиться к нам</a>
                </div>
                <div class="hero-stats">
                    <div class="stat">
                        <div class="stat-value">$30B+</div>
                        <div class="stat-label">Капитализация</div>
                    </div>
                    <div class="stat">
                        <div class="stat-value">150+</div>
                        <div class="stat-label">Проектов</div>
                    </div>
                    <div class="stat">
                        <div class="stat-value">15</div>
                        <div class="stat-label">Лет инноваций</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="projects">
        <div class="container">
            <div class="section-header">
                <div class="section-label">Наши инновации</div>
                <h2 class="section-title">Прорывные проекты</h2>
                <p class="section-subtitle">Технологии, которые меняют правила игры в глобальном масштабе</p>
            </div>
            
            <div class="projects-grid">
                <div class="project-card">
                    <div class="project-image">
                        <img src="https://images.unsplash.com/photo-1635070041078-e363dbe005cb?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="Quantum Nexus">
                    </div>
                    <div class="project-content">
                        <span class="project-category">Квантовые вычисления</span>
                        <h3 class="project-title">Quantum Nexus</h3>
                        <p class="project-description">Первая в мире коммерческая квантовая сеть, обеспечивающая мгновенную передачу данных на любые расстояния.</p>
                        <div class="project-tech">
                            <span class="tech-tag">Квантовая запутанность</span>
                            <span class="tech-tag">QKD</span>
                            <span class="tech-tag">Квантовые процессоры</span>
                        </div>
                    </div>
                </div>
                
                <div class="project-card">
                    <div class="project-image">
                        <img src="https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="NeuraLink AI">
                    </div>
                    <div class="project-content">
                        <span class="project-category">Искусственный интеллект</span>
                        <h3 class="project-title">NeuraLink AI</h3>
                        <p class="project-description">Когнитивная платформа, способная обучаться и адаптироваться в реальном времени без дополнительного программирования.</p>
                        <div class="project-tech">
                            <span class="tech-tag">Глубокое обучение</span>
                            <span class="tech-tag">Нейросети</span>
                            <span class="tech-tag">AGI</span>
                        </div>
                    </div>
                </div>
                
                <div class="project-card">
                    <div class="project-image">
                        <img src="https://images.unsplash.com/photo-1535223289827-42f1e9919769?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="BioSync">
                    </div>
                    <div class="project-content">
                        <span class="project-category">Биотехнологии</span>
                        <h3 class="project-title">BioSync Implants</h3>
                        <p class="project-description">Биосовместимые импланты, усиливающие когнитивные способности и обеспечивающие прямой интерфейс мозг-компьютер.</p>
                        <div class="project-tech">
                            <span class="tech-tag">Нейроинтерфейсы</span>
                            <span class="tech-tag">Биосенсоры</span>
                            <span class="tech-tag">Нанотехнологии</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="services">
        <div class="container">
            <div class="section-header">
                <div class="section-label">Наши направления</div>
                <h2 class="section-title">Профессиональные услуги</h2>
                <p class="section-subtitle">Комплексные решения для бизнеса любого масштаба</p>
            </div>
            
            <div class="services-tabs">
                <div class="service-tab active" data-tab="security">Информационная безопасность</div>
                <div class="service-tab" data-tab="software">Программное обеспечение</div>
                <div class="service-tab" data-tab="services">Услуги</div>
                <div class="service-tab" data-tab="shop">Интернет-магазин</div>
            </div>
            
            <div class="service-content active" id="security-content">
                <div class="projects-grid">
                    <div class="project-card">
                        <div class="project-image">
                            <img src="https://images.unsplash.com/photo-1550751827-4bd374c3f58b?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="Кибербезопасность">
                        </div>
                        <div class="project-content">
                            <span class="project-category">Защита данных</span>
                            <h3 class="project-title">QuantumShield Security</h3>
                            <p class="project-description">Передовая система кибербезопасности на основе квантовой криптографии для защиты критически важных данных.</p>
                            <div class="project-tech">
                                <span class="tech-tag">Квантовая криптография</span>
                                <span class="tech-tag">Блокчейн</span>
                                <span class="tech-tag">AI Мониторинг</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="project-card">
                        <div class="project-image">
                            <img src="https://images.unsplash.com/photo-1563013544-824ae1b704d3?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="Сетевая безопасность">
                        </div>
                        <div class="project-content">
                            <span class="project-category">Сетевая защита</span>
                            <h3 class="project-title">NeuralGuard Network</h3>
                            <p class="project-description">Самообучающаяся система защиты корпоративных сетей с предиктивной аналитикой угроз.</p>
                            <div class="project-tech">
                                <span class="tech-tag">Нейросети</span>
                                <span class="tech-tag">Предиктивная аналитика</span>
                                <span class="tech-tag">Zero Trust</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="project-card">
                        <div class="project-image">
                            <img src="https://images.unsplash.com/photo-1558494949-ef010cbdcc31?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="Криптография">
                        </div>
                        <div class="project-content">
                            <span class="project-category">Криптография</span>
                            <h3 class="project-title">CryptoVault Solutions</h3>
                            <p class="project-description">Инновационные решения для безопасного хранения и передачи конфиденциальной информации.</p>
                            <div class="project-tech">
                                <span class="tech-tag">Постквантовая криптография</span>
                                <span class="tech-tag">Многофакторная аутентификация</span>
                                <span class="tech-tag">Биометрия</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="service-content" id="software-content">
                <div class="projects-grid">
                    <div class="project-card">
                        <div class="project-image">
                            <img src="https://images.unsplash.com/photo-1555066931-4365d14bab8c?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="Корпоративное ПО">
                        </div>
                        <div class="project-content">
                            <span class="project-category">Корпоративные решения</span>
                            <h3 class="project-title">Enterprise AI Suite</h3>
                            <p class="project-description">Комплексная платформа для автоматизации бизнес-процессов с интеграцией искусственного интеллекта.</p>
                            <div class="project-tech">
                                <span class="tech-tag">Машинное обучение</span>
                                <span class="tech-tag">Аналитика данных</span>
                                <span class="tech-tag">Облачные вычисления</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="project-card">
                        <div class="project-image">
                            <img src="https://images.unsplash.com/photo-1551650975-87deedd944c3?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="Мобильные приложения">
                        </div>
                        <div class="project-content">
                            <span class="project-category">Мобильные решения</span>
                            <h3 class="project-title">NeuroMobile Platform</h3>
                            <p class="project-description">Инновационная платформа для создания адаптивных мобильных приложений с нейроинтерфейсами.</p>
                            <div class="project-tech">
                                <span class="tech-tag">iOS/Android</span>
                                <span class="tech-tag">Нейроинтерфейсы</span>
                                <span class="tech-tag">AR/VR</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="project-card">
                        <div class="project-image">
                            <img src="https://images.unsplash.com/photo-1547658719-da2b51169166?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="Аналитические системы">
                        </div>
                        <div class="project-content">
                            <span class="project-category">Аналитические системы</span>
                            <h3 class="project-title">DataSphere Analytics</h3>
                            <p class="project-description">Мощная аналитическая платформа для обработки больших данных и предиктивного моделирования.</p>
                            <div class="project-tech">
                                <span class="tech-tag">Big Data</span>
                                <span class="tech-tag">Предиктивная аналитика</span>
                                <span class="tech-tag">Визуализация данных</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="service-content" id="services-content">
                <div class="projects-grid">
                    <div class="project-card">
                        <div class="project-image">
                            <img src="https://images.unsplash.com/photo-1552664730-d307ca884978?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="ИТ-консалтинг">
                        </div>
                        <div class="project-content">
                            <span class="project-category">ИТ-консалтинг</span>
                            <h3 class="project-title">Digital Transformation</h3>
                            <p class="project-description">Комплексное сопровождение цифровой трансформации бизнеса с внедрением передовых технологий.</p>
                            <div class="project-tech">
                                <span class="tech-tag">Стратегическое планирование</span>
                                <span class="tech-tag">Технологический аудит</span>
                                <span class="tech-tag">Внедрение решений</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="project-card">
                        <div class="project-image">
                            <img src="https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="Облачные решения">
                        </div>
                        <div class="project-content">
                            <span class="project-category">Облачные решения</span>
                            <h3 class="project-title">Quantum Cloud Services</h3>
                            <p class="project-description">Высокопроизводительные облачные решения с интеграцией квантовых вычислений.</p>
                            <div class="project-tech">
                                <span class="tech-tag">Гибридное облако</span>
                                <span class="tech-tag">Квантовые вычисления</span>
                                <span class="tech-tag">Масштабируемость</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="project-card">
                        <div class="project-image">
                            <img src="https://images.unsplash.com/photo-1544197150-b99a580bb7a8?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80" alt="Техническая поддержка">
                        </div>
                        <div class="project-content">
                            <span class="project-category">Техническая поддержка</span>
                            <h3 class="project-title">AI-Powered Support</h3>
                            <p class="project-description">Круглосуточная техническая поддержка на основе искусственного интеллекта для бизнеса любого масштаба.</p>
                            <div class="project-tech">
                                <span class="tech-tag">Искусственный интеллект</span>
                                <span class="tech-tag">Автоматизация</span>
                                <span class="tech-tag">Проактивный мониторинг</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="service-content" id="shop-content">
                <div class="coming-soon">
                    <div class="coming-soon-icon">
                        <i class="fas fa-shopping-cart"></i>
                    </div>
                    <h3 style="font-size: 2.5rem; margin-bottom: 20px;">Интернет-магазин в разработке</h3>
                    <p style="font-size: 1.2rem; color: rgba(255, 255, 255, 0.7); max-width: 600px; margin: 0 auto;">
                        Мы работаем над созданием уникального интернет-магазина с эксклюзивными технологическими решениями. 
                        Скоро вы сможете приобрести наши продукты напрямую!
                    </p>
                    <div style="margin-top: 40px;">
                        <div class="btn">Узнать первым о запуске <i class="fas fa-bell"></i></div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="tech">
        <div class="container">
            <div class="section-header">
                <div class="section-label">Наш арсенал</div>
                <h2 class="section-title">Передовые технологии</h2>
                <p class="section-subtitle">Инструменты и платформы, которые позволяют нам создавать будущее</p>
            </div>
            
            <div class="tech-grid">
                <div class="tech-card">
                    <div class="tech-icon">
                        <i class="fas fa-atom"></i>
                    </div>
                    <h3 class="tech-name">Квантовые вычисления</h3>
                    <p class="tech-description">Используем квантовые процессоры для решения задач, недоступных классическим компьютерам</p>
                </div>
                
                <div class="tech-card">
                    <div class="tech-icon">
                        <i class="fas fa-brain"></i>
                    </div>
                    <h3 class="tech-name">Искусственный интеллект</h3>
                    <p class="tech-description">Самообучающиеся системы, способные к творческому мышлению и решению сложных проблем</p>
                </div>
                
                <div class="tech-card">
                    <div class="tech-icon">
                        <i class="fas fa-dna"></i>
                    </div>
                    <h3 class="tech-name">Биотехнологии</h3>
                    <p class="tech-description">Синтез биологии и технологий для создания революционных медицинских решений</p>
                </div>
                
                <div class="tech-card">
                    <div class="tech-icon">
                        <i class="fas fa-rocket"></i>
                    </div>
                    <h3 class="tech-name">Космические технологии</h3>
                    <p class="tech-description">Разработка систем для освоения космоса и создания инфраструктуры за пределами Земли</p>
                </div>
                
                <div class="tech-card">
                    <div class="tech-icon">
                        <i class="fas fa-shield-alt"></i>
                    </div>
                    <h3 class="tech-name">Кибербезопасность</h3>
                    <p class="tech-description">Квантово-устойчивые системы защиты для цифровой инфраструктуры будущего</p>
                </div>
                
                <div class="tech-card">
                    <div class="tech-icon">
                        <i class="fas fa-network-wired"></i>
                    </div>
                    <h3 class="tech-name">Web3 & Blockchain</h3>
                    <p class="tech-description">Децентрализованные системы для создания прозрачной и безопасной цифровой экономики</p>
                </div>
            </div>
        </div>
    </section>

    <section id="contact">
        <div class="container">
            <div class="section-header">
                <div class="section-label">Свяжитесь с нами</div>
                <h2 class="section-title">Начните сотрудничество</h2>
                <p class="section-subtitle">Готовы изменить будущее вместе с нами? Мы всегда открыты для новых вызовов</p>
            </div>
            
            <div class="contact-grid">
                <div class="contact-info">
                    <div class="contact-item">
                        <div class="contact-icon">
                            <i class="fas fa-map-marker-alt"></i>
                        </div>
                        <div class="contact-details">
                            <h4>Главный офис</h4>
                            <p>Innovation District, Tech City</p>
                            <p>Silicon Valley, CA 94025</p>
                        </div>
                    </div>
                    
                    <div class="contact-item">
                        <div class="contact-icon">
                            <i class="fas fa-phone"></i>
                        </div>
                        <div class="contact-details">
                            <h4>Телефон</h4>
                            <p>+1 (650) 123-4567</p>
                        </div>
                    </div>
                    
                    <div class="contact-item">
                        <div class="contact-icon">
                            <i class="fas fa-envelope"></i>
                        </div>
                        <div class="contact-details">
                            <h4>Email</h4>
                            <p>innovation@itcoffee.com</p>
                        </div>
                    </div>
                    
                    <div class="social-links">
                        <a href="#" class="social-link"><i class="fab fa-twitter"></i></a>
                        <a href="#" class="social-link"><i class="fab fa-linkedin-in"></i></a>
                        <a href="#" class="social-link"><i class="fab fa-github"></i></a>
                        <a href="#" class="social-link"><i class="fab fa-youtube"></i></a>
                    </div>
                </div>
                
                <form class="contact-form" id="contactForm">
                    <div class="form-group">
                        <label for="name">Ваше имя</label>
                        <input type="text" id="name" class="form-control" placeholder="Введите ваше имя" required>
                        <div class="form-error" id="nameError">Пожалуйста, введите ваше имя</div>
                    </div>
                    
                    <div class="form-group">
                        <label for="email">Email</label>
                        <input type="email" id="email" class="form-control" placeholder="Введите ваш email" required>
                        <div class="form-error" id="emailError">Пожалуйста, введите корректный email</div>
                    </div>
                    
                    <div class="form-group">
                        <label for="subject">Тема</label>
                        <input type="text" id="subject" class="form-control" placeholder="Тема сообщения" required>
                        <div class="form-error" id="subjectError">Пожалуйста, введите тему сообщения</div>
                    </div>
                    
                    <div class="form-group">
                        <label for="message">Сообщение</label>
                        <textarea id="message" class="form-control" placeholder="Опишите ваш проект или идею" required></textarea>
                        <div class="form-error" id="messageError">Пожалуйста, введите ваше сообщение</div>
                    </div>
                    
                    <button type="submit" class="btn" style="align-self: flex-start;">Отправить заявку <i class="fas fa-paper-plane"></i></button>
                    
                    <div class="form-success" id="formSuccess">
                        <i class="fas fa-check-circle"></i> Ваше сообщение успешно отправлено! Мы свяжемся с вами в ближайшее время.
                    </div>
                </form>
            </div>
        </div>
    </section>

    <footer>
        <div class="container">
            <div class="footer-content">
                <div class="footer-info">
                    <h3>ITCoffee</h3>
                    <p>Создаем технологии, которые определяют будущее человечества. 15 лет инноваций, 150+ прорывных проектов, бесконечные возможности.</p>
                </div>
                
                <div class="footer-column">
                    <h4>Компания</h4>
                    <ul class="footer-links">
                        <li><a href="#">О нас</a></li>
                        <li><a href="#">Команда</a></li>
                        <li><a href="#">Карьера</a></li>
                        <li><a href="#">Новости</a></li>
                    </ul>
                </div>
                
                <div class="footer-column">
                    <h4>Ресурсы</h4>
                    <ul class="footer-links">
                        <li><a href="#">Исследования</a></li>
                        <li><a href="#">Публикации</a></li>
                        <li><a href="#">Технологии</a></li>
                        <li><a href="#">Форум</a></li>
                    </ul>
                </div>
                
                <div class="footer-column">
                    <h4>Правовая информация</h4>
                    <ul class="footer-links">
                        <li><a href="#">Политика конфиденциальности</a></li>
                        <li><a href="#">Условия использования</a></li>
                        <li><a href="#">Патенты</a></li>
                        <li><a href="#">Лицензии</a></li>
                    </ul>
                </div>
            </div>
            
            <div class="copyright">
                <p>&copy; 2023 ITCoffee Technologies. Все права защищены. Капитализация: $30+ млрд.</p>
            </div>
        </div>
    </footer>

    <a href="#" class="scroll-to-top" id="scrollToTop">
        <i class="fas fa-arrow-up"></i>
    </a>

    <script>
        // Индикатор загрузки - ровно 5 секунд
        document.addEventListener('DOMContentLoaded', function() {
            const loader = document.getElementById('pageLoader');
            const progress = document.getElementById('loaderProgress');
            
            let width = 0;
            const totalTime = 5000; // 5 секунд
            const steps = 100;
            const stepTime = totalTime / steps; // 50 мс на каждый шаг
            
            const interval = setInterval(() => {
                if (width >= 100) {
                    clearInterval(interval);
                    setTimeout(() => {
                        loader.classList.add('hidden');
                    }, 500);
                } else {
                    width += 1;
                    progress.style.width = width + '%';
                }
            }, stepTime);
        });

        // Мобильное меню
        const mobileMenuBtn = document.getElementById('mobileMenuBtn');
        const mobileMenu = document.getElementById('mobileMenu');
        const menuOverlay = document.getElementById('menuOverlay');
        
        mobileMenuBtn.addEventListener('click', function() {
            mobileMenu.classList.toggle('active');
            menuOverlay.classList.toggle('active');
            document.body.style.overflow = mobileMenu.classList.contains('active') ? 'hidden' : '';
        });
        
        menuOverlay.addEventListener('click', function() {
            mobileMenu.classList.remove('active');
            menuOverlay.classList.remove('active');
            document.body.style.overflow = '';
        });

        document.querySelectorAll('.mobile-nav-links a').forEach(link => {
            link.addEventListener('click', function() {
                mobileMenu.classList.remove('active');
                menuOverlay.classList.remove('active');
                document.body.style.overflow = '';
            });
        });

        // Параллакс эффект для фона
        document.addEventListener('mousemove', (e) => {
            const bg = document.querySelector('.animated-bg');
            const x = e.clientX / window.innerWidth;
            const y = e.clientY / window.innerHeight;
            
            bg.style.transform = `translate(-${x * 20}px, -${y * 20}px)`;
        });

        // Анимация появления элементов при скролле
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -50px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.opacity = '1';
                    entry.target.style.transform = 'translateY(0)';
                }
            });
        }, observerOptions);

        document.querySelectorAll('.project-card, .tech-card').forEach(el => {
            el.style.opacity = '0';
            el.style.transform = 'translateY(30px)';
            el.style.transition = 'opacity 0.6s ease, transform 0.6s ease';
            observer.observe(el);
        });

        // Изменение навигации при скролле
        window.addEventListener('scroll', () => {
            const nav = document.querySelector('nav');
            const scrollToTop = document.getElementById('scrollToTop');
            
            if (window.scrollY > 100) {
                nav.style.background = 'rgba(10, 10, 10, 0.95)';
                nav.style.backdropFilter = 'blur(30px)';
                scrollToTop.classList.add('active');
            } else {
                nav.style.background = 'rgba(10, 10, 10, 0.9)';
                nav.style.backdropFilter = 'blur(20px)';
                scrollToTop.classList.remove('active');
            }
        });

        // Плавная прокрутка для навигационных ссылок
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                
                const targetId = this.getAttribute('href');
                if (targetId === '#') return;
                
                const targetElement = document.querySelector(targetId);
                if (targetElement) {
                    window.scrollTo({
                        top: targetElement.offsetTop - 100,
                        behavior: 'smooth'
                    });
                }
            });
        });

        // Валидация формы
        const contactForm = document.getElementById('contactForm');
        
        contactForm.addEventListener('submit', function(e) {
            e.preventDefault();
            
            let isValid = true;
            
            const name = document.getElementById('name');
            const nameError = document.getElementById('nameError');
            if (name.value.trim() === '') {
                nameError.style.display = 'block';
                isValid = false;
            } else {
                nameError.style.display = 'none';
            }
            
            const email = document.getElementById('email');
            const emailError = document.getElementById('emailError');
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (!emailRegex.test(email.value.trim())) {
                emailError.style.display = 'block';
                isValid = false;
            } else {
                emailError.style.display = 'none';
            }
            
            const subject = document.getElementById('subject');
            const subjectError = document.getElementById('subjectError');
            if (subject.value.trim() === '') {
                subjectError.style.display = 'block';
                isValid = false;
            } else {
                subjectError.style.display = 'none';
            }
            
            const message = document.getElementById('message');
            const messageError = document.getElementById('messageError');
            if (message.value.trim() === '') {
                messageError.style.display = 'block';
                isValid = false;
            } else {
                messageError.style.display = 'none';
            }
            
            if (isValid) {
                const formSuccess = document.getElementById('formSuccess');
                formSuccess.style.display = 'block';
                
                contactForm.reset();
                
                setTimeout(() => {
                    formSuccess.style.display = 'none';
                }, 5000);
            }
        });

        // Табы для услуг
        document.querySelectorAll('.service-tab').forEach(tab => {
            tab.addEventListener('click', function() {
                // Убираем активный класс у всех табов
                document.querySelectorAll('.service-tab').forEach(t => {
                    t.classList.remove('active');
                });
                
                // Добавляем активный класс текущему табу
                this.classList.add('active');
                
                // Скрываем все контенты
                document.querySelectorAll('.service-content').forEach(content => {
                    content.classList.remove('active');
                });
                
                // Показываем соответствующий контент
                const tabId = this.getAttribute('data-tab');
                document.getElementById(`${tabId}-content`).classList.add('active');
            });
        });
    </script>
</body>
</html>
