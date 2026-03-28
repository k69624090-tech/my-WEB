<!DOCTYPE html>
<html lang="ja">
<head><meta name="google-site-verification" content="H8KB4WG-ImEgHXB_7marNjMajn8xP_RULeC6kNUR1Kc" /> <meta name="description" content="Kakeru Shinoharaのポートフォリオ。画像生成AIや動画生成AIを活用したSNSプロジェクト『まわループ』や『tukikage.art』などの活動をまとめています。">
<meta name="keywords" content="Kakeru Shinohara, 篠原翔, AIクリエイター, まわループ, 画像生成AI, SNS収益化">
<link rel="canonical" href="https://あなたのユーザー名.github.io/リポジトリ名/">
    
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kakeru Shinohara | AI Creator & Digital Project Builder</title>

    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&family=Noto+Sans+JP:wght@300;400;500;700&display=swap" rel="stylesheet">

    <style>
        /* =========================================
           CSS Custom Properties
        ========================================= */
        @property --angle {
            syntax: '<angle>';
            initial-value: 0deg;
            inherits: false;
        }

        :root {
            --bg-base: #0B0F19;
            --bg-card: #111827;
            --text-main: #F3F4F6;
            --text-sub: #9CA3AF;
            --accent: #7C3AED;
            --accent-sub: #22D3EE;
            --border-color: rgba(255, 255, 255, 0.08);
            --glow-purple: 0 0 20px rgba(124, 58, 237, 0.4);
            --glow-cyan: 0 0 20px rgba(34, 211, 238, 0.3);
            --glass-bg: rgba(17, 24, 39, 0.5);
            --glass-border: rgba(255, 255, 255, 0.1);
            --gradient-primary: linear-gradient(135deg, #7C3AED, #22D3EE);
            --gradient-text: linear-gradient(90deg, #7C3AED, #22D3EE, #7C3AED);
            --nav-height: 60px;
        }

        /* =========================================
           Base & Global
        ========================================= */
        * { box-sizing: border-box; }
        html { scroll-behavior: smooth; }

        body {
            margin: 0;
            padding: 0;
            font-family: 'Inter', 'Noto Sans JP', sans-serif;
            background-color: var(--bg-base);
            color: var(--text-main);
            line-height: 1.8;
            overflow-x: hidden;
            letter-spacing: 0.03em;
        }

        /* Noise texture overlay */
        body::before {
            content: '';
            position: fixed;
            inset: 0;
            z-index: 9999;
            pointer-events: none;
            opacity: 0.035;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='1'/%3E%3C/svg%3E");
            background-repeat: repeat;
            background-size: 256px 256px;
        }

        /* Custom scrollbar */
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb {
            background: linear-gradient(180deg, #7C3AED, #22D3EE);
            border-radius: 3px;
        }

        /* Selection */
        ::selection {
            background: rgba(124, 58, 237, 0.4);
            color: #fff;
        }

        h1, h2, h3, h4 {
            font-family: 'Inter', 'Noto Sans JP', sans-serif;
            margin: 0;
            font-weight: 700;
        }

        a {
            text-decoration: none;
            color: inherit;
        }

        section {
            padding: 100px 20px;
            max-width: 960px;
            margin: 0 auto;
            position: relative;
        }

        /* Section title */
        .section-title {
            font-size: 2.8rem;
            margin-bottom: 50px;
            letter-spacing: 3px;
            text-align: center;
            background: linear-gradient(135deg, var(--text-main), var(--accent-sub), var(--accent));
            background-size: 200% auto;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            position: relative;
            display: inline-block;
            width: 100%;
        }
        .section-title::after {
            content: '';
            display: block;
            width: 60px;
            height: 3px;
            background: var(--gradient-primary);
            margin: 16px auto 0;
            border-radius: 2px;
        }

        /* Animations */
        .fade-in-up {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.8s ease, transform 0.8s ease;
        }
        .fade-in-up.show {
            opacity: 1;
            transform: translateY(0);
        }

        /* Stagger children */
        .stagger-item {
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.6s ease, transform 0.6s ease;
        }
        .stagger-item.show {
            opacity: 1;
            transform: translateY(0);
        }

        /* =========================================
           Loader
        ========================================= */
        #loader {
            position: fixed;
            inset: 0;
            z-index: 10000;
            background: var(--bg-base);
            display: flex;
            align-items: center;
            justify-content: center;
            transition: opacity 0.5s ease;
        }
        #loader .spinner {
            width: 40px;
            height: 40px;
            border: 3px solid rgba(124, 58, 237, 0.2);
            border-top-color: var(--accent);
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
        }
        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* =========================================
           Navigation
        ========================================= */
        .main-nav {
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 1000;
            background: rgba(11, 15, 25, 0.6);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
            transition: all 0.3s ease;
        }
        .main-nav.nav-scrolled {
            background: rgba(11, 15, 25, 0.85);
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.3);
        }
        .nav-inner {
            max-width: 960px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 14px 24px;
        }
        .nav-logo {
            font-weight: 700;
            font-size: 1.3rem;
            background: var(--gradient-primary);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: 2px;
        }
        .nav-links {
            display: flex;
            gap: 28px;
        }
        .nav-links a {
            font-size: 0.85rem;
            color: var(--text-sub);
            font-weight: 500;
            letter-spacing: 1px;
            position: relative;
            transition: color 0.3s ease;
            cursor: pointer;
        }
        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -4px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--gradient-primary);
            transition: width 0.3s ease;
            border-radius: 1px;
        }
        .nav-links a:hover {
            color: var(--text-main);
        }
        .nav-links a:hover::after {
            width: 100%;
        }
        /* Active nav link */
        .nav-links a.nav-active {
            color: var(--text-main);
        }
        .nav-links a.nav-active::after {
            width: 100%;
        }

        /* Hamburger menu */
        .hamburger {
            display: none;
            background: none;
            border: none;
            cursor: pointer;
            padding: 8px;
            z-index: 1001;
        }
        .hamburger span {
            display: block;
            width: 24px;
            height: 2px;
            background: var(--text-main);
            margin: 5px 0;
            transition: all 0.3s ease;
            border-radius: 1px;
        }

        /* =========================================
           SPA Pages
        ========================================= */
        .page {
            display: none;
            min-height: calc(100vh - var(--nav-height));
        }
        .page.active {
            display: block;
        }
        .page-enter {
            animation: pageIn 0.45s ease-out forwards;
        }
        @keyframes pageIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .page-exit {
            animation: pageOut 0.3s ease-in forwards;
        }
        @keyframes pageOut {
            from { opacity: 1; transform: translateY(0); }
            to { opacity: 0; transform: translateY(-15px); }
        }

        /* Breadcrumb */
        .breadcrumb {
            padding: 80px 20px 0;
            max-width: 960px;
            margin: 0 auto;
            font-size: 0.85rem;
            color: var(--text-sub);
        }
        .breadcrumb a {
            color: var(--accent-sub);
            transition: opacity 0.3s;
        }
        .breadcrumb a:hover { opacity: 0.7; }
        .breadcrumb .sep { margin: 0 8px; color: var(--text-sub); }
        .breadcrumb .current { color: var(--text-main); font-weight: 500; }

        /* =========================================
           Hero
        ========================================= */
        .hero {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 0 20px;
            position: relative;
            overflow: hidden;
        }
        /* Animated gradient bg */
        .hero::before {
            content: '';
            position: absolute;
            inset: 0;
            background:
                radial-gradient(ellipse at 20% 50%, rgba(124, 58, 237, 0.15) 0%, transparent 50%),
                radial-gradient(ellipse at 80% 20%, rgba(34, 211, 238, 0.1) 0%, transparent 50%),
                radial-gradient(ellipse at 50% 80%, rgba(124, 58, 237, 0.08) 0%, transparent 40%);
            animation: hero-bg-drift 12s ease-in-out infinite alternate;
            z-index: 0;
        }
        @keyframes hero-bg-drift {
            0% { transform: scale(1) translate(0, 0); }
            100% { transform: scale(1.1) translate(-20px, 10px); }
        }
        /* Grid pattern */
        .hero::after {
            content: '';
            position: absolute;
            inset: 0;
            background-image:
                linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
            background-size: 60px 60px;
            animation: grid-move 20s linear infinite;
            z-index: 0;
        }
        @keyframes grid-move {
            0% { transform: translate(0, 0); }
            100% { transform: translate(60px, 60px); }
        }

        .hero-glass {
            position: relative;
            z-index: 1;
            background: rgba(17, 24, 39, 0.4);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 28px;
            padding: 50px 48px;
            max-width: 780px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
        }

        .hero-avatar {
            width: 110px;
            height: 110px;
            border-radius: 50%;
            object-fit: cover;
            border: 3px solid rgba(124, 58, 237, 0.4);
            box-shadow: 0 0 30px rgba(124, 58, 237, 0.3);
            margin-bottom: 20px;
            transition: transform 0.5s ease, box-shadow 0.5s ease;
        }
        .hero-avatar:hover {
            transform: scale(1.05);
            box-shadow: 0 0 40px rgba(124, 58, 237, 0.5);
        }

        .hero h1 {
            font-size: 3.8rem;
            margin-bottom: 10px;
            letter-spacing: 3px;
            background: linear-gradient(90deg, #ffffff 0%, #22D3EE 50%, #7C3AED 100%);
            background-size: 200% auto;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: gradient-shift 5s ease-in-out infinite;
        }
        @keyframes gradient-shift {
            0%, 100% { background-position: 0% center; }
            50% { background-position: 100% center; }
        }

        .hero .job-title {
            font-size: 0.9rem;
            color: var(--accent-sub);
            margin-bottom: 28px;
            font-weight: 600;
            letter-spacing: 4px;
            text-transform: uppercase;
        }
        .hero p {
            color: var(--text-sub);
            max-width: 700px;
            font-size: 1rem;
            margin-bottom: 32px;
            margin-left: auto;
            margin-right: auto;
        }

        /* Buttons */
        .btn-main {
            display: inline-block;
            padding: 16px 44px;
            background: linear-gradient(135deg, #7C3AED, #6d28d9, #4f46e5);
            background-size: 200% auto;
            color: #fff;
            border-radius: 999px;
            font-weight: 600;
            transition: all 0.4s ease;
            box-shadow: 0 4px 20px rgba(124, 58, 237, 0.3);
            letter-spacing: 0.5px;
            cursor: pointer;
            border: none;
            font-size: 1rem;
            font-family: inherit;
        }
        .btn-main:hover {
            background-position: right center;
            transform: translateY(-3px);
            box-shadow: 0 8px 30px rgba(124, 58, 237, 0.5);
        }

        /* See more link */
        .see-more-link {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            color: var(--accent-sub);
            font-weight: 600;
            font-size: 0.9rem;
            margin-top: 24px;
            transition: gap 0.3s ease, color 0.3s ease;
            cursor: pointer;
        }
        .see-more-link:hover {
            gap: 12px;
            color: #fff;
        }
        .see-more-link::after {
            content: '\2192';
        }

        /* =========================================
           Home Overview Sections
        ========================================= */
        .home-section {
            padding: 80px 20px;
            max-width: 960px;
            margin: 0 auto;
            text-align: center;
        }
        .home-section-header {
            font-size: 1.8rem;
            margin-bottom: 12px;
            letter-spacing: 2px;
            background: linear-gradient(135deg, var(--text-main), var(--accent-sub));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .home-section-sub {
            color: var(--text-sub);
            margin-bottom: 40px;
            font-size: 0.95rem;
        }

        /* Home featured projects (compact grid) */
        .home-projects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            gap: 20px;
            margin-bottom: 16px;
        }

        /* Home skills overview */
        .home-skills-wrap {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            margin-bottom: 16px;
        }
        .home-skills-wrap span {
            background: var(--glass-bg);
            backdrop-filter: blur(8px);
            -webkit-backdrop-filter: blur(8px);
            border: 1px solid rgba(124, 58, 237, 0.15);
            padding: 8px 16px;
            border-radius: 10px;
            font-size: 0.85rem;
            transition: all 0.3s ease;
        }
        .home-skills-wrap span:hover {
            border-color: var(--accent);
            box-shadow: var(--glow-purple);
            transform: translateY(-2px);
        }

        /* =========================================
           Mission & About
        ========================================= */
        .text-center-block {
            text-align: center;
            max-width: 750px;
            margin: 0 auto;
        }
        .text-center-block p {
            color: var(--text-sub);
            margin-bottom: 24px;
        }
        .highlight {
            color: var(--accent-sub);
            font-weight: 700;
        }
        .list-style-none {
            list-style: none;
            padding: 0;
            color: var(--text-main);
            display: inline-block;
            text-align: left;
            background: var(--glass-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            padding: 24px 40px;
            border-radius: 16px;
            border: 1px solid var(--glass-border);
        }
        .list-style-none li {
            margin-bottom: 10px;
        }

        /* Section separators */
        .section-sep {
            border-top: 1px solid rgba(124, 58, 237, 0.1);
        }
        .section-sep-line::before {
            content: '';
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 80%;
            max-width: 600px;
            height: 1px;
            background: linear-gradient(90deg, transparent, rgba(34, 211, 238, 0.2), transparent);
        }

        /* =========================================
           Projects (Cards)
        ========================================= */
        .projects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 24px;
        }

        .project-card {
            background: var(--glass-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid var(--glass-border);
            border-radius: 20px;
            padding: 30px;
            transition: all 0.4s ease;
            display: flex;
            flex-direction: column;
            position: relative;
            overflow: hidden;
        }
        /* Animated gradient border */
        .project-card::before {
            content: '';
            position: absolute;
            inset: 0;
            padding: 1px;
            border-radius: 20px;
            background: conic-gradient(from var(--angle, 0deg), #7C3AED, #22D3EE, #7C3AED);
            -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
            animation: rotate-border 4s linear infinite;
            opacity: 0;
            transition: opacity 0.4s ease;
            pointer-events: none;
        }
        @keyframes rotate-border {
            to { --angle: 360deg; }
        }
        .project-card:hover::before {
            opacity: 1;
        }
        .project-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4), 0 0 30px rgba(124, 58, 237, 0.15);
        }
        .project-card h3 {
            font-size: 1.35rem;
            margin-bottom: 10px;
            color: var(--text-main);
        }
        .project-card p {
            color: var(--text-sub);
            font-size: 0.95rem;
            margin-bottom: 20px;
            flex-grow: 1;
        }

        /* Tags */
        .tags {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 20px;
        }
        .tag {
            background: rgba(34, 211, 238, 0.08);
            color: var(--accent-sub);
            padding: 4px 12px;
            border-radius: 6px;
            font-size: 0.78rem;
            font-weight: 600;
            border: 1px solid rgba(34, 211, 238, 0.2);
            transition: all 0.3s ease;
        }
        .tag:hover {
            box-shadow: 0 0 12px rgba(34, 211, 238, 0.3);
            background: rgba(34, 211, 238, 0.15);
        }

        /* Card buttons */
        .card-links {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }
        .btn-sub {
            padding: 8px 18px;
            background: transparent;
            color: var(--text-main);
            border: 1px solid var(--border-color);
            border-radius: 999px;
            font-size: 0.85rem;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
        }
        .btn-sub:hover {
            border-color: var(--accent-sub);
            color: var(--accent-sub);
            box-shadow: var(--glow-cyan);
            background: rgba(34, 211, 238, 0.05);
        }
        .btn-coming-soon {
            padding: 8px 18px;
            background: rgba(255,255,255,0.02);
            color: var(--text-sub);
            border: 1px dashed rgba(255, 255, 255, 0.1);
            border-radius: 999px;
            font-size: 0.85rem;
            cursor: not-allowed;
        }

        /* =========================================
           Strengths
        ========================================= */
        .strengths-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            text-align: center;
        }
        .strength-item {
            background: var(--glass-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid var(--glass-border);
            padding: 28px 20px;
            border-radius: 16px;
            font-weight: 600;
            transition: all 0.4s ease;
            position: relative;
        }
        .strength-item:hover {
            transform: translateY(-5px) perspective(600px) rotateX(2deg);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3), var(--glow-purple);
            border-color: rgba(124, 58, 237, 0.3);
        }

        /* =========================================
           Skills
        ========================================= */
        .skills-container {
            display: flex;
            flex-direction: column;
            gap: 36px;
        }
        .skill-category h3 {
            font-size: 1.2rem;
            margin-bottom: 16px;
            color: var(--accent-sub);
            padding-bottom: 12px;
            position: relative;
        }
        .skill-category h3::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, var(--accent), var(--accent-sub), transparent);
            border-radius: 1px;
        }
        .skill-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }
        .skill-tags span {
            background: var(--glass-bg);
            backdrop-filter: blur(8px);
            -webkit-backdrop-filter: blur(8px);
            border: 1px solid rgba(124, 58, 237, 0.15);
            padding: 10px 18px;
            border-radius: 10px;
            font-size: 0.9rem;
            transition: all 0.3s ease;
        }
        .skill-tags span:hover {
            border-color: var(--accent);
            box-shadow: var(--glow-purple);
            transform: translateY(-2px);
            background: rgba(124, 58, 237, 0.08);
        }

        /* =========================================
           Gallery
        ========================================= */
        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
        }
        .gallery-item {
            height: 260px;
            border-radius: 18px;
            overflow: hidden;
            background-color: var(--bg-card);
            border: 1px solid var(--glass-border);
            position: relative;
            transition: all 0.4s ease;
        }
        .gallery-item:hover {
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4), var(--glow-purple);
        }
        .gallery-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.6s ease, filter 0.6s ease;
        }
        .gallery-item:hover img {
            transform: scale(1.15);
            filter: brightness(1.1);
        }
        /* Image overlay on hover */
        .gallery-item-overlay {
            position: absolute;
            inset: 0;
            background: linear-gradient(to top, rgba(11, 15, 25, 0.7) 0%, transparent 60%);
            opacity: 0;
            transition: opacity 0.4s ease;
            z-index: 1;
        }
        .gallery-item:hover .gallery-item-overlay {
            opacity: 1;
        }
        /* Placeholder */
        .gallery-placeholder-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: var(--text-sub);
            font-weight: 600;
            letter-spacing: 1px;
            z-index: 2;
        }
        .gallery-item-placeholder {
            position: absolute;
            inset: 0;
            background: linear-gradient(135deg, rgba(124, 58, 237, 0.06), rgba(34, 211, 238, 0.04), rgba(124, 58, 237, 0.06));
            background-size: 400% 400%;
            animation: pulse-bg 4s ease-in-out infinite;
        }
        @keyframes pulse-bg {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        /* =========================================
           Vision
        ========================================= */
        .vision-section {
            position: relative;
        }
        .vision-section::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 400px;
            height: 400px;
            background: radial-gradient(circle, rgba(124, 58, 237, 0.08) 0%, transparent 70%);
            pointer-events: none;
        }

        /* =========================================
           Contact
        ========================================= */
        .contact-section {
            text-align: center;
            background: linear-gradient(135deg, var(--bg-card) 0%, #1e1b4b 50%, var(--bg-card) 100%);
            background-size: 400% 400%;
            animation: contact-gradient 10s ease infinite;
            padding: 80px 30px;
            border-radius: 28px;
            border: 1px solid rgba(124, 58, 237, 0.2);
            margin-bottom: 50px;
            position: relative;
            overflow: hidden;
        }
        @keyframes contact-gradient {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }
        .contact-section::before {
            content: '';
            position: absolute;
            inset: 0;
            border-radius: 28px;
            padding: 1px;
            background: conic-gradient(from var(--angle, 0deg), transparent, rgba(124, 58, 237, 0.3), transparent, rgba(34, 211, 238, 0.3), transparent);
            -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
            animation: rotate-border 6s linear infinite;
            opacity: 0.6;
            pointer-events: none;
        }
        .contact-section h2 {
            font-size: 2.5rem;
            margin-bottom: 20px;
            background: linear-gradient(135deg, var(--text-main), var(--accent-sub));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .contact-section p {
            color: var(--text-sub);
            margin-bottom: 30px;
            position: relative;
            z-index: 1;
        }
        .contact-links {
            display: flex;
            justify-content: center;
            gap: 16px;
            flex-wrap: wrap;
            position: relative;
            z-index: 1;
        }
        .contact-links a {
            padding: 12px 30px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 999px;
            transition: all 0.4s ease;
            font-weight: 500;
        }
        .contact-links a:hover {
            border-color: var(--accent-sub);
            color: var(--accent-sub);
            box-shadow: var(--glow-cyan);
            background: rgba(34, 211, 238, 0.08);
            transform: translateY(-3px);
        }

        /* =========================================
           Footer
        ========================================= */
        .footer {
            text-align: center;
            padding: 30px 20px;
            color: var(--text-sub);
            font-size: 0.8rem;
            border-top: 1px solid var(--border-color);
        }

        /* =========================================
           Back to Top
        ========================================= */
        #back-to-top {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 44px;
            height: 44px;
            border-radius: 50%;
            background: var(--glass-bg);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 1px solid var(--glass-border);
            color: var(--text-main);
            font-size: 1.2rem;
            cursor: pointer;
            opacity: 0;
            transform: translateY(10px);
            transition: all 0.3s ease;
            z-index: 999;
            pointer-events: none;
        }
        #back-to-top.visible {
            opacity: 1;
            transform: translateY(0);
            pointer-events: auto;
        }
        #back-to-top:hover {
            border-color: var(--accent);
            box-shadow: var(--glow-purple);
            transform: translateY(-3px);
        }

        /* =========================================
           Responsive
        ========================================= */
        @media (max-width: 1024px) {
            .projects-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        @media (max-width: 768px) {
            .hero h1 { font-size: 2.4rem; }
            .hero-glass { padding: 36px 22px; margin: 0 10px; }
            .hero-avatar { width: 85px; height: 85px; }
            .hero .job-title { font-size: 0.75rem; letter-spacing: 3px; }
            section { padding: 70px 20px; }
            .section-title { font-size: 2rem; }
            .hero p { font-size: 0.9rem; }
            .projects-grid { grid-template-columns: 1fr; }
            .home-projects-grid { grid-template-columns: 1fr; }
            .strengths-grid { grid-template-columns: 1fr 1fr; }
            .gallery-grid { grid-template-columns: 1fr 1fr; }
            .contact-section { padding: 50px 20px; }

            /* Hamburger visible */
            .hamburger { display: block; }
            .nav-links {
                display: flex;
                flex-direction: column;
                position: fixed;
                top: 0;
                right: -280px;
                width: 260px;
                height: 100vh;
                background: rgba(11, 15, 25, 0.95);
                backdrop-filter: blur(20px);
                -webkit-backdrop-filter: blur(20px);
                padding: 90px 30px 30px;
                gap: 24px;
                transition: right 0.4s cubic-bezier(0.4, 0, 0.2, 1);
                border-left: 1px solid var(--glass-border);
                z-index: 999;
            }
            .nav-links.open { right: 0; }
            .nav-links a { font-size: 1rem; }

            /* Hamburger X transform */
            .hamburger.active span:nth-child(1) {
                transform: rotate(45deg) translate(5px, 5px);
            }
            .hamburger.active span:nth-child(2) { opacity: 0; }
            .hamburger.active span:nth-child(3) {
                transform: rotate(-45deg) translate(5px, -5px);
            }

            /* Mobile overlay */
            .nav-overlay {
                display: none;
                position: fixed;
                inset: 0;
                background: rgba(0, 0, 0, 0.5);
                z-index: 998;
            }
            .nav-overlay.show { display: block; }
        }
        @media (max-width: 480px) {
            .hero h1 { font-size: 1.9rem; }
            .strengths-grid { grid-template-columns: 1fr; }
            .gallery-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <!-- Loader -->
    <div id="loader">
        <div class="spinner"></div>
    </div>

    <!-- Mobile overlay -->
    <div class="nav-overlay" id="navOverlay"></div>

    <!-- Navigation -->
    <nav class="main-nav">
        <div class="nav-inner">
            <a href="#/home" class="nav-logo">KS</a>
            <div class="nav-links" id="navLinks">
                <a href="#/home" data-nav="home">Home</a>
                <a href="#/about" data-nav="about">About</a>
                <a href="#/projects" data-nav="projects">Projects</a>
                <a href="#/skills" data-nav="skills">Skills</a>
                <a href="#/gallery" data-nav="gallery">Gallery</a>
                <a href="#/contact" data-nav="contact">Contact</a>
            </div>
            <button class="hamburger" id="hamburger" aria-label="Menu" aria-expanded="false">
                <span></span><span></span><span></span>
            </button>
        </div>
    </nav>

    <!-- Back to Top -->
    <button id="back-to-top" aria-label="Back to top">&#8593;</button>

    <!-- ============================================
         PAGE: Home
    ============================================= -->
    <div class="page" data-page="home">

        <!-- Hero -->
        <div class="hero">
            <div class="hero-glass fade-in-up">
                <img src="profile.jpg" alt="Kakeru Shinohara" class="hero-avatar" loading="lazy">
                <h1>Kakeru Shinohara</h1>
                <div class="job-title">AI Creator / Digital Project Builder</div>
                <p>AI技術とインターネットを活用し、<br>個人の創作・発信・収益化の可能性を探求しています。<br>画像生成AI・動画生成AI・文章生成AIなどのツールを活用し、<br>複数のプロジェクトを通して<br>AI時代における新しい個人活動の形を実践・研究しています。</p>
                <p style="margin-top: -16px;">AIを使ったコンテンツ制作、SNS運用、ビジネスの実験などを通じて、<br>個人でも価値を生み出せる仕組みを研究しています。</p>
                <a href="#/projects" class="btn-main">Projects を見る</a>
            </div>
        </div>

        <!-- Home: Mission teaser -->
        <div class="home-section fade-in-up">
            <h2 class="home-section-header">Mission</h2>
            <p class="home-section-sub">AIを使って、個人が価値を生み出せる時代をつくる。<br>ただ語るのではなく、実際のプロジェクトとして実践し続けること。</p>
            <a href="#/about" class="see-more-link">詳しく見る</a>
        </div>

        <!-- Home: Featured Projects -->
        <div class="home-section fade-in-up">
            <h2 class="home-section-header">Featured Projects</h2>
            <p class="home-section-sub">現在進行中の注目プロジェクト</p>
            <div class="home-projects-grid">

                <div class="project-card stagger-item">
                    <h3>まわループ。</h3>
                    <div class="tags">
                        <span class="tag">AI Art</span><span class="tag">Visual</span><span class="tag">TikTok</span>
                    </div>
                    <p>AI生成アートを活用したクリエイティブプロジェクト。</p>
                    <div class="card-links">
                        <a href="https://www.tiktok.com/@mawaloop.jp" target="_blank" class="btn-sub">&#9654; TikTokを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>tukikage.art</h3>
                    <div class="tags">
                        <span class="tag">Digital Art</span><span class="tag">TikTok</span>
                    </div>
                    <p>幻想的な世界観をテーマにしたデジタルアートプロジェクト。</p>
                    <div class="card-links">
                        <a href="https://www.tiktok.com/@tsukikage.art" target="_blank" class="btn-sub">&#9654; TikTokを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>note × X 収益化実践</h3>
                    <div class="tags">
                        <span class="tag">note</span><span class="tag">X</span><span class="tag">Monetization</span>
                    </div>
                    <p>SNSとコンテンツ発信を組み合わせた長期型収益モデルの研究。</p>
                    <div class="card-links">
                        <a href="https://note.com/fit_hosta1330" target="_blank" class="btn-sub">&#9654; noteを見る</a>
                        <a href="https://x.com/kakechan_note" target="_blank" class="btn-sub">&#9654; Xを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>メルカリ販売実践プロジェクト</h3>
                    <div class="tags">
                        <span class="tag">Business</span><span class="tag">Mercari</span>
                    </div>
                    <p>実データをもとに出品方法・価格設定・売れる条件を分析。</p>
                    <div class="card-links">
                        <a href="https://jp.mercari.com/user/profile/809675688" target="_blank" class="btn-sub">&#9654; メルカリを見る</a>
                    </div>
                </div>

            </div>
            <a href="#/projects" class="see-more-link">全14プロジェクトを見る</a>
        </div>

        <!-- Home: Skills overview -->
        <div class="home-section fade-in-up">
            <h2 class="home-section-header">Skills</h2>
            <p class="home-section-sub">AI / Creative / Content / Project</p>
            <div class="home-skills-wrap">
                <span class="stagger-item">画像生成AI</span>
                <span class="stagger-item">動画生成AI</span>
                <span class="stagger-item">文章生成AI</span>
                <span class="stagger-item">SNS運用</span>
                <span class="stagger-item">note記事制作</span>
                <span class="stagger-item">実験プロジェクト設計</span>
                <span class="stagger-item">デジタル導線構築</span>
            </div>
            <a href="#/skills" class="see-more-link">スキル詳細を見る</a>
        </div>

    </div>

    <!-- ============================================
         PAGE: About
    ============================================= -->
    <div class="page" data-page="about">
        <div class="breadcrumb">
            <a href="#/home">Home</a><span class="sep">/</span><span class="current">About</span>
        </div>

        <!-- Mission -->
        <section class="fade-in-up section-sep">
            <h2 class="section-title">Mission</h2>
            <div class="text-center-block">
                <h3 style="font-size: 1.5rem; margin-bottom: 20px;">AIを使って、個人が価値を生み出せる時代をつくる</h3>
                <p>AI技術の進化により、<br>個人でも創作・発信・ビジネス構築ができる時代が広がっています。</p>
                <p>私はその可能性を、<br>ただ語るのではなく <span class="highlight">実際のプロジェクトとして実践し続けること</span> を大切にしています。</p>
                <p>AIを使うこと自体が目的ではなく、<br><span class="highlight">AIを活用して「自分の表現」と「自分の活動」を作れる状態</span><br>を目指しています。</p>
            </div>
        </section>

        <!-- About -->
        <section class="fade-in-up section-sep-line">
            <h2 class="section-title">About</h2>
            <div class="text-center-block">
                <p>AI技術とインターネットを活用した<br>デジタルコンテンツ制作・個人ビジネス・情報発信の研究と実践を行っています。</p>
                <p>画像生成AI、動画生成AI、文章生成AIなどを活用しながら、<br><span class="highlight">「個人がゼロから価値を生み出す仕組み」</span>をテーマに<br>複数のプロジェクトを運営しています。</p>

                <p style="margin-top: 40px; margin-bottom: 10px;">私の活動の特徴は、</p>
                <ul class="list-style-none">
                    <li>・実際にプロジェクトを立ち上げる</li>
                    <li>・データを取りながら分析する</li>
                    <li>・成功と失敗のプロセスを研究する</li>
                </ul>
                <p style="margin-top: 10px;">という <span class="highlight">実験型のアプローチ</span> です。</p>

                <p style="margin-top: 30px;">AI時代における個人の可能性を、<br>創作・発信・収益化の3つの視点から探りながら<br>プロジェクトとして積み上げています。</p>
            </div>
        </section>

        <!-- Strengths -->
        <section class="fade-in-up">
            <h2 class="section-title">Strengths</h2>
            <div class="strengths-grid">
                <div class="strength-item stagger-item">実験型で動けること</div>
                <div class="strength-item stagger-item">複数領域を横断して<br>活動できること</div>
                <div class="strength-item stagger-item">初心者視点で<br>情報整理できること</div>
                <div class="strength-item stagger-item">継続してプロジェクトを<br>積み上げられること</div>
            </div>
        </section>

        <!-- Vision -->
        <section class="fade-in-up vision-section">
            <h2 class="section-title">Vision</h2>
            <div class="text-center-block">
                <p>AIは、特別な人だけのものではなく、<br>個人が自分の可能性を広げるための強力な道具だと考えています。</p>
                <p>今後はAIを活用した創作・発信・収益化の実践を深めながら、<br>個人でも挑戦できる形に整理し、<br>より多くの人に届く形で発信していきたいと考えています。</p>
                <p><span class="highlight">創作と実用の両方を大切にしながら、<br>AI時代の新しい個人活動の形を<br>自分自身のプロジェクトとして積み上げていきます。</span></p>
            </div>
        </section>
    </div>

    <!-- ============================================
         PAGE: Projects
    ============================================= -->
    <div class="page" data-page="projects">
        <div class="breadcrumb">
            <a href="#/home">Home</a><span class="sep">/</span><span class="current">Projects</span>
        </div>

        <section class="fade-in-up">
            <h2 class="section-title">Projects</h2>
            <div class="projects-grid">

                <div class="project-card stagger-item">
                    <h3>まわループ。</h3>
                    <div class="tags">
                        <span class="tag">AI Art</span><span class="tag">Visual</span><span class="tag">TikTok</span>
                    </div>
                    <p>AI生成アートを活用したクリエイティブプロジェクト。<br>ビジュアル制作や映像コンテンツを通して、AI時代の新しい表現を探っています。</p>
                    <div class="card-links">
                        <a href="https://www.tiktok.com/@mawaloop.jp" target="_blank" class="btn-sub">&#9654; TikTokを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>tukikage.art</h3>
                    <div class="tags">
                        <span class="tag">Digital Art</span><span class="tag">TikTok</span>
                    </div>
                    <p>AI画像生成を活用したデジタルアートプロジェクト。<br>幻想的な世界観をテーマに作品制作を行っています。</p>
                    <div class="card-links">
                        <a href="https://www.tiktok.com/@tsukikage.art" target="_blank" class="btn-sub">&#9654; TikTokを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>AI副業研究所</h3>
                    <div class="tags">
                        <span class="tag">Research</span><span class="tag">Business</span>
                    </div>
                    <p>AIを活用した副業や個人ビジネスの可能性を研究するプロジェクト。</p>
                    <div class="card-links">
                        <span class="btn-coming-soon">&#9654; Coming Soon</span>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>note × X 収益化実践</h3>
                    <div class="tags">
                        <span class="tag">note</span><span class="tag">X</span><span class="tag">Monetization</span>
                    </div>
                    <p>SNSとコンテンツ発信を組み合わせた長期型収益モデルを研究・実践するプロジェクト。</p>
                    <div class="card-links">
                        <a href="https://note.com/fit_hosta1330" target="_blank" class="btn-sub">&#9654; noteを見る</a>
                        <a href="https://x.com/kakechan_note" target="_blank" class="btn-sub">&#9654; Xを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>メルカリ販売実践プロジェクト</h3>
                    <div class="tags">
                        <span class="tag">Business</span><span class="tag">Mercari</span>
                    </div>
                    <p>不用品販売をテーマに、出品方法・価格設定・売れる条件などを実データをもとに分析しているプロジェクト。</p>
                    <div class="card-links">
                        <a href="https://jp.mercari.com/user/profile/809675688" target="_blank" class="btn-sub">&#9654; メルカリを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>デイリーチョイス</h3>
                    <div class="tags">
                        <span class="tag">Instagram</span><span class="tag">Affiliate</span>
                    </div>
                    <p>Instagramを活用した商品紹介・情報発信プロジェクト。</p>
                    <div class="card-links">
                        <a href="https://www.instagram.com/choisudeiri/" target="_blank" class="btn-sub">&#9654; Instagramを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>ポイカツ収益化計画</h3>
                    <div class="tags">
                        <span class="tag">X</span><span class="tag">Research</span>
                    </div>
                    <p>ポイ活を収益導線として捉え、継続・効率化・情報整理の観点から研究しているプロジェクト。</p>
                    <div class="card-links">
                        <a href="https://x.com/reo_poipoti" target="_blank" class="btn-sub">&#9654; Xを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>AIマスター</h3>
                    <div class="tags">
                        <span class="tag">X</span><span class="tag">AI Tool</span>
                    </div>
                    <p>AI活用の情報発信と収益化の可能性を研究するプロジェクト。</p>
                    <div class="card-links">
                        <a href="https://x.com/aimasuta631" target="_blank" class="btn-sub">&#9654; Xを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>レンAI × ポイカツ最適化ナビ</h3>
                    <div class="tags">
                        <span class="tag">X</span><span class="tag">AI Tool</span>
                    </div>
                    <p>AIを使ってポイ活情報を整理し、初心者でも分かりやすく活用できる形を目指すプロジェクト。</p>
                    <div class="card-links">
                        <a href="https://x.com/ai_poikatsu_opt" target="_blank" class="btn-sub">&#9654; Xを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>AI初心者「60代主婦が始めました」</h3>
                    <div class="tags">
                        <span class="tag">note</span><span class="tag">Beginner</span>
                    </div>
                    <p>AI初心者向けに、AIの使い方や可能性をわかりやすく伝えるプロジェクト。</p>
                    <div class="card-links">
                        <a href="https://note.com/loyal_cosmos5598" target="_blank" class="btn-sub">&#9654; noteを見る</a>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>TikTok AI初心者向け発信</h3>
                    <div class="tags">
                        <span class="tag">TikTok</span><span class="tag">Short Video</span>
                    </div>
                    <p>AI初心者向けにショート動画でAI活用を伝えるプロジェクト。</p>
                    <div class="card-links">
                        <span class="btn-coming-soon">&#9654; Coming Soon</span>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>note運用 / 情報発信</h3>
                    <div class="tags">
                        <span class="tag">note</span><span class="tag">Writing</span>
                    </div>
                    <p>実践や実体験をもとに、情報を記事として蓄積・発信するプロジェクト。</p>
                    <div class="card-links">
                        <span class="btn-coming-soon">&#9654; Coming Soon</span>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>AI活用の仕組み化</h3>
                    <div class="tags">
                        <span class="tag">System</span><span class="tag">AI Tool</span>
                    </div>
                    <p>AIを使った情報整理・文章制作・学習効率化など、日々の活動を支える仕組みづくりの研究。</p>
                    <div class="card-links">
                        <span class="btn-coming-soon">&#9654; Coming Soon</span>
                    </div>
                </div>

                <div class="project-card stagger-item">
                    <h3>エルマート関連発信</h3>
                    <div class="tags">
                        <span class="tag">Video</span><span class="tag">SNS</span>
                    </div>
                    <p>商品紹介や情報発信におけるAI動画・SNS活用の実験プロジェクト。</p>
                    <div class="card-links">
                        <span class="btn-coming-soon">&#9654; Coming Soon</span>
                    </div>
                </div>

            </div>
        </section>
    </div>

    <!-- ============================================
         PAGE: Skills
    ============================================= -->
    <div class="page" data-page="skills">
        <div class="breadcrumb">
            <a href="#/home">Home</a><span class="sep">/</span><span class="current">Skills</span>
        </div>

        <section class="fade-in-up">
            <h2 class="section-title">Skills</h2>
            <div class="skills-container">
                <div class="skill-category">
                    <h3>AI / Creative</h3>
                    <div class="skill-tags">
                        <span class="stagger-item">画像生成AI</span><span class="stagger-item">動画生成AI</span><span class="stagger-item">文章生成AI</span><span class="stagger-item">AIプロンプト設計</span><span class="stagger-item">AIコンテンツ企画</span>
                    </div>
                </div>
                <div class="skill-category">
                    <h3>Content / Media</h3>
                    <div class="skill-tags">
                        <span class="stagger-item">SNS運用</span><span class="stagger-item">note記事制作</span><span class="stagger-item">ショート動画企画</span><span class="stagger-item">情報発信設計</span>
                    </div>
                </div>
                <div class="skill-category">
                    <h3>Project / Research</h3>
                    <div class="skill-tags">
                        <span class="stagger-item">実験プロジェクト設計</span><span class="stagger-item">デジタル導線構築</span><span class="stagger-item">個人収益モデル研究</span><span class="stagger-item">情報整理 / コンテンツ構造化</span>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <!-- ============================================
         PAGE: Gallery
    ============================================= -->
    <div class="page" data-page="gallery">
        <div class="breadcrumb">
            <a href="#/home">Home</a><span class="sep">/</span><span class="current">Gallery</span>
        </div>

        <section class="fade-in-up">
            <h2 class="section-title">Gallery</h2>
            <div class="gallery-grid">
                <div class="gallery-item stagger-item">
                    <img src="AI Concept Art.png" alt="AI Concept Art" loading="lazy">
                    <div class="gallery-item-overlay"></div>
                </div>
                <div class="gallery-item stagger-item">
                    <div class="gallery-item-placeholder"></div>
                    <span class="gallery-placeholder-text">Digital Visuals</span>
                </div>
                <div class="gallery-item stagger-item">
                    <div class="gallery-item-placeholder"></div>
                    <span class="gallery-placeholder-text">Short Video</span>
                </div>
                <div class="gallery-item stagger-item">
                    <div class="gallery-item-placeholder"></div>
                    <span class="gallery-placeholder-text">Social Contents</span>
                </div>
            </div>
        </section>
    </div>

    <!-- ============================================
         PAGE: Contact
    ============================================= -->
    <div class="page" data-page="contact">
        <div class="breadcrumb">
            <a href="#/home">Home</a><span class="sep">/</span><span class="current">Contact</span>
        </div>

        <section class="fade-in-up">
            <div class="contact-section">
                <h2>Contact</h2>
                <p>活動やプロジェクトに関するお問い合わせは<br>以下のSNSよりお願いいたします。</p>
                <div class="contact-links">
                    <a href="https://x.com/kakechan_note" target="_blank">X (Twitter)</a>
                    <a href="https://note.com/fit_hosta1330" target="_blank">note</a>
                    <a href="https://www.tiktok.com/@mawaloop.jp" target="_blank">TikTok</a>
                    <a href="https://www.instagram.com/choisudeiri/" target="_blank">Instagram</a>
                </div>
            </div>
        </section>
    </div>

    <!-- Footer -->
    <div class="footer">
        &copy; 2025 Kakeru Shinohara. All rights reserved.
    </div>

    <script>
        // =========================================
        // SPA Router
        // =========================================
        const Router = {
            routes: ['home', 'about', 'projects', 'skills', 'gallery', 'contact'],
            currentPage: null,

            init() {
                window.addEventListener('hashchange', () => this.navigate());
                this.navigate();
            },

            getPageFromHash() {
                const hash = location.hash.replace('#/', '').replace('#', '');
                return this.routes.includes(hash) ? hash : 'home';
            },

            navigate() {
                const page = this.getPageFromHash();
                if (page === this.currentPage) return;
                this.transition(page);
            },

            transition(newPage) {
                const oldEl = document.querySelector('.page.active');
                const newEl = document.querySelector(`[data-page="${newPage}"]`);
                if (!newEl) return;

                if (oldEl && oldEl !== newEl) {
                    oldEl.classList.add('page-exit');
                    oldEl.addEventListener('animationend', function handler() {
                        oldEl.classList.remove('active', 'page-exit');
                        oldEl.style.display = 'none';
                        oldEl.removeEventListener('animationend', handler);
                    });
                }

                // Small delay for exit animation to start
                const delay = oldEl && oldEl !== newEl ? 150 : 0;
                setTimeout(() => {
                    newEl.style.display = 'block';
                    newEl.classList.add('active', 'page-enter');
                    newEl.addEventListener('animationend', function handler() {
                        newEl.classList.remove('page-enter');
                        newEl.removeEventListener('animationend', handler);
                    });

                    window.scrollTo({ top: 0, behavior: 'instant' });
                    this.triggerAnimations(newEl);
                }, delay);

                this.currentPage = newPage;
                this.updateNav(newPage);
            },

            updateNav(page) {
                document.querySelectorAll('.nav-links a[data-nav]').forEach(a => {
                    if (a.getAttribute('data-nav') === page) {
                        a.classList.add('nav-active');
                    } else {
                        a.classList.remove('nav-active');
                    }
                });
            },

            triggerAnimations(pageEl) {
                // Reset and re-observe fade-in-up elements
                pageEl.querySelectorAll('.fade-in-up').forEach(el => {
                    el.classList.remove('show');
                    void el.offsetWidth; // force reflow
                    fadeObserver.observe(el);
                });

                // Reset and re-observe stagger items
                const containers = pageEl.querySelectorAll('.projects-grid, .home-projects-grid, .strengths-grid, .gallery-grid, .skill-tags, .home-skills-wrap');
                containers.forEach(container => {
                    container.querySelectorAll('.stagger-item').forEach(item => {
                        item.classList.remove('show');
                        item.style.transitionDelay = '';
                    });
                    staggerObserver.observe(container);
                });
            }
        };

        // =========================================
        // Intersection Observers
        // =========================================
        const fadeObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('show');
                }
            });
        }, { threshold: 0.1 });

        const staggerObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    const items = entry.target.querySelectorAll('.stagger-item');
                    items.forEach((item, i) => {
                        item.style.transitionDelay = `${i * 0.08}s`;
                        item.classList.add('show');
                    });
                    staggerObserver.unobserve(entry.target);
                }
            });
        }, { threshold: 0.1 });

        // =========================================
        // Loader & Init
        // =========================================
        window.addEventListener('load', () => {
            const loader = document.getElementById('loader');
            loader.style.opacity = '0';
            setTimeout(() => {
                loader.style.display = 'none';
                Router.init();
            }, 500);
        });

        // =========================================
        // Nav scroll effect
        // =========================================
        window.addEventListener('scroll', () => {
            document.querySelector('.main-nav').classList.toggle('nav-scrolled', window.scrollY > 50);

            // Back to top visibility
            const btn = document.getElementById('back-to-top');
            btn.classList.toggle('visible', window.scrollY > 400);
        });

        // =========================================
        // Back to top
        // =========================================
        document.getElementById('back-to-top').addEventListener('click', () => {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        });

        // =========================================
        // Hamburger menu
        // =========================================
        const hamburger = document.getElementById('hamburger');
        const navLinks = document.getElementById('navLinks');
        const navOverlay = document.getElementById('navOverlay');

        function closeMenu() {
            hamburger.classList.remove('active');
            navLinks.classList.remove('open');
            navOverlay.classList.remove('show');
            hamburger.setAttribute('aria-expanded', 'false');
        }

        hamburger.addEventListener('click', () => {
            const isOpen = navLinks.classList.contains('open');
            if (isOpen) {
                closeMenu();
            } else {
                hamburger.classList.add('active');
                navLinks.classList.add('open');
                navOverlay.classList.add('show');
                hamburger.setAttribute('aria-expanded', 'true');
            }
        });

        navOverlay.addEventListener('click', closeMenu);

        navLinks.querySelectorAll('a').forEach(a => {
            a.addEventListener('click', closeMenu);
        });

        // =========================================
        // Internal navigation links (see-more, btn-main with hash)
        // =========================================
        document.addEventListener('click', (e) => {
            const link = e.target.closest('a[href^="#/"]');
            if (link) {
                e.preventDefault();
                const hash = link.getAttribute('href');
                location.hash = hash;
            }
        });
    </script>
</body>
</html>
