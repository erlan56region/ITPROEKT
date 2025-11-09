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
                                <
