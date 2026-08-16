<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="OpenGuide - Turning Rescue Dogs into Guide Dogs. An accessible, community-driven training platform.">
    <title>OpenGuide — Rescue to Guide</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-primary: #0a0a0f;
            --bg-secondary: #12121a;
            --bg-tertiary: #1a1a25;
            --bg-card: #161622;
            --accent: #6366f1;
            --accent-hover: #818cf8;
            --accent-glow: rgba(99, 102, 241, 0.3);
            --text-primary: #f1f1f4;
            --text-secondary: #a1a1aa;
            --text-muted: #71717a;
            --success: #22c55e;
            --warning: #f59e0b;
            --danger: #ef4444;
            --border: rgba(255,255,255,0.08);
            --radius: 12px;
            --radius-sm: 8px;
            --transition: all 0.2s ease;
        }
        * { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; font-size: 16px; }
        body {
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            line-height: 1.6;
            min-height: 100vh;
            overflow-x: hidden;
        }
        .skip-link {
            position: absolute;
            top: -40px;
            left: 0;
            background: var(--accent);
            color: white;
            padding: 8px 16px;
            z-index: 10000;
            border-radius: 0 0 var(--radius-sm) 0;
            font-weight: 600;
            text-decoration: none;
            transition: top 0.3s;
        }
        .skip-link:focus { top: 0; }
        .sr-only {
            position: absolute;
            width: 1px; height: 1px;
            padding: 0; margin: -1px;
            overflow: hidden;
            clip: rect(0,0,0,0);
            white-space: nowrap;
            border: 0;
        }
        nav {
            position: fixed;
            top: 0; left: 0; right: 0;
            background: rgba(10,10,15,0.85);
            backdrop-filter: blur(20px);
            border-bottom: 1px solid var(--border);
            z-index: 1000;
            padding: 0 24px;
        }
        .nav-container {
            max-width: 1200px;
            margin: 0 auto;
            display: flex;
            align-items: center;
            justify-content: space-between;
            height: 64px;
        }
        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: 800;
            font-size: 1.25rem;
            color: var(--text-primary);
            text-decoration: none;
        }
        .logo-icon {
            width: 36px; height: 36px;
            background: linear-gradient(135deg, var(--accent), #8b5cf6);
            border-radius: var(--radius-sm);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.1rem;
        }
        .nav-links {
            display: flex;
            gap: 8px;
            list-style: none;
        }
        .nav-links a {
            color: var(--text-secondary);
            text-decoration: none;
            padding: 8px 16px;
            border-radius: var(--radius-sm);
            font-weight: 500;
            font-size: 0.9rem;
            transition: var(--transition);
            border: 1px solid transparent;
            cursor: pointer;
            background: none;
            font-family: inherit;
        }
        .nav-links a:hover, .nav-links a:focus {
            color: var(--text-primary);
            background: var(--bg-tertiary);
            border-color: var(--border);
            outline: 2px solid var(--accent);
            outline-offset: 2px;
        }
        .nav-links a.active {
            color: var(--accent-hover);
            background: rgba(99,102,241,0.1);
        }
        .menu-toggle {
            display: none;
            background: none;
            border: 1px solid var(--border);
            color: var(--text-primary);
            padding: 8px 12px;
            border-radius: var(--radius-sm);
            cursor: pointer;
        }
        main { padding-top: 64px; }
        .section {
            max-width: 1200px;
            margin: 0 auto;
            padding: 80px 24px;
            display: none;
        }
        .section.active {
            display: block;
            animation: fadeIn 0.4s ease;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .hero {
            text-align: center;
            padding: 100px 24px 60px;
            max-width: 900px;
            margin: 0 auto;
        }
        .hero-badge {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            background: rgba(99,102,241,0.1);
            border: 1px solid rgba(99,102,241,0.3);
            color: var(--accent-hover);
            padding: 6px 16px;
            border-radius: 100px;
            font-size: 0.85rem;
            font-weight: 600;
            margin-bottom: 24px;
        }
        .hero h1 {
            font-size: clamp(2.5rem, 6vw, 4.5rem);
            font-weight: 800;
            line-height: 1.05;
            margin-bottom: 24px;
            letter-spacing: -0.03em;
        }
        .hero h1 span {
            background: linear-gradient(135deg, var(--accent), #c084fc);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        .hero p {
            font-size: 1.25rem;
            color: var(--text-secondary);
            max-width: 640px;
            margin: 0 auto 40px;
            line-height: 1.7;
        }
        .hero-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 16px;
            max-width: 800px;
            margin: 48px auto 0;
        }
        .stat-card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            padding: 24px;
            text-align: center;
        }
        .stat-number {
            font-size: 2rem;
            font-weight: 800;
            color: var(--accent-hover);
            display: block;
        }
        .stat-label {
            font-size: 0.85rem;
            color: var(--text-muted);
            margin-top: 4px;
        }
        .btn {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 12px 28px;
            border-radius: var(--radius-sm);
            font-weight: 600;
            font-size: 0.95rem;
            cursor: pointer;
            transition: var(--transition);
            border: none;
            text-decoration: none;
        }
        .btn-primary {
            background: linear-gradient(135deg, var(--accent), #8b5cf6);
            color: white;
            box-shadow: 0 4px 20px var(--accent-glow);
        }
        .btn-primary:hover, .btn-primary:focus {
            transform: translateY(-2px);
            box-shadow: 0 8px 30px var(--accent-glow);
            outline: 2px solid var(--accent-hover);
            outline-offset: 2px;
        }
        .btn-secondary {
            background: var(--bg-tertiary);
            color: var(--text-primary);
            border: 1px solid var(--border);
        }
        .btn-secondary:hover, .btn-secondary:focus {
            background: var(--bg-card);
            border-color: var(--accent);
            outline: 2px solid var(--accent);
            outline-offset: 2px;
        }
        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 20px;
            margin-top: 32px;
        }
        .card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            padding: 28px;
            transition: var(--transition);
        }
        .card:hover {
            border-color: rgba(99,102,241,0.3);
            transform: translateY(-2px);
        }
        .card h3 {
            font-size: 1.1rem;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .card p {
            color: var(--text-secondary);
            font-size: 0.95rem;
        }
        .section-header {
            margin-bottom: 40px;
        }
        .section-header h2 {
            font-size: 2rem;
            font-weight: 700;
            margin-bottom: 8px;
        }
        .section-header p {
            color: var(--text-secondary);
            max-width: 600px;
        }
        .milestone-container {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            padding: 32px;
            margin-top: 24px;
        }
        .milestone-track {
            display: flex;
            justify-content: space-between;
            position: relative;
            margin-bottom: 40px;
        }
        .milestone-track::before {
            content: '';
            position: absolute;
            top: 20px;
            left: 0; right: 0;
            height: 4px;
            background: var(--bg-tertiary);
            border-radius: 2px;
            z-index: 0;
        }
        .milestone-step {
            position: relative;
            z-index: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 12px;
            cursor: pointer;
            background: none;
            border: none;
            color: inherit;
            font-family: inherit;
            flex: 1;
        }
        .milestone-dot {
            width: 44px; height: 44px;
            border-radius: 50%;
            background: var(--bg-secondary);
            border: 3px solid var(--bg-tertiary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            font-size: 0.9rem;
            transition: var(--transition);
        }
        .milestone-step.completed .milestone-dot {
            background: var(--accent);
            border-color: var(--accent);
            color: white;
        }
        .milestone-step.active .milestone-dot {
            background: var(--bg-secondary);
            border-color: var(--accent);
            color: var(--accent);
            box-shadow: 0 0 20px var(--accent-glow);
        }
        .milestone-label {
            font-size: 0.75rem;
            font-weight: 600;
            color: var(--text-muted);
            text-align: center;
            max-width: 90px;
        }
        .milestone-step.completed .milestone-label,
        .milestone-step.active .milestone-label {
            color: var(--text-primary);
        }
        .milestone-detail {
            background: var(--bg-secondary);
            border-radius: var(--radius-sm);
            padding: 24px;
            border-left: 4px solid var(--accent);
            display: none;
        }
        .milestone-detail.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }
        .milestone-detail h4 {
            margin-bottom: 8px;
            font-size: 1.1rem;
        }
        .milestone-detail ul {
            margin: 12px 0 0 20px;
            color: var(--text-secondary);
        }
        .milestone-detail li {
            margin-bottom: 6px;
        }
        .progress-wrapper {
            margin-top: 24px;
        }
        .progress-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 8px;
            font-size: 0.9rem;
        }
        .progress-bar {
            height: 10px;
            background: var(--bg-tertiary);
            border-radius: 5px;
            overflow: hidden;
        }
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--accent), #8b5cf6);
            border-radius: 5px;
            transition: width 0.6s ease;
            width: 0%;
        }
        .module-list {
            display: flex;
            flex-direction: column;
            gap: 16px;
            margin-top: 24px;
        }
        .module-item {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            overflow: hidden;
            transition: var(--transition);
        }
        .module-header {
            padding: 20px 24px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            cursor: pointer;
            background: none;
            border: none;
            width: 100%;
            color: inherit;
            font-family: inherit;
            text-align: left;
        }
        .module-header:hover {
            background: rgba(255,255,255,0.02);
        }
        .module-title {
            display: flex;
            align-items: center;
            gap: 14px;
        }
        .module-icon {
            width: 40px; height: 40px;
            background: rgba(99,102,241,0.1);
            border-radius: var(--radius-sm);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
        }
        .module-meta h4 {
            font-size: 1rem;
            margin-bottom: 2px;
        }
        .module-meta span {
            font-size: 0.8rem;
            color: var(--text-muted);
        }
        .module-toggle {
            font-size: 1.2rem;
            color: var(--text-muted);
            transition: transform 0.2s;
        }
        .module-item.expanded .module-toggle {
            transform: rotate(180deg);
        }
        .module-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.4s ease;
        }
        .module-item.expanded .module-content {
            max-height: 3000px;
        }
        .module-body {
            padding: 0 24px 24px;
        }
        .audio-controls {
            display: flex;
            gap: 12px;
            margin: 16px 0;
            flex-wrap: wrap;
        }
        .audio-btn {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            padding: 8px 16px;
            background: var(--bg-tertiary);
            border: 1px solid var(--border);
            color: var(--text-primary);
            border-radius: var(--radius-sm);
            cursor: pointer;
            font-size: 0.85rem;
            font-weight: 500;
            transition: var(--transition);
            font-family: inherit;
        }
        .audio-btn:hover, .audio-btn:focus {
            border-color: var(--accent);
            outline: 2px solid var(--accent);
            outline-offset: 2px;
        }
        .audio-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        .transcript-box {
            background: var(--bg-secondary);
            border-radius: var(--radius-sm);
            padding: 16px;
            margin-top: 12px;
            border-left: 3px solid var(--accent);
        }
        .transcript-box h5 {
            font-size: 0.8rem;
            text-transform: uppercase;
            letter-spacing: 0.05em;
            color: var(--text-muted);
            margin-bottom: 8px;
        }
        .transcript-box p, .transcript-box ul {
            font-size: 0.95rem;
            color: var(--text-secondary);
            line-height: 1.7;
        }
        .transcript-box ul {
            margin-left: 20px;
        }
        .transcript-box li {
            margin-bottom: 6px;
        }
        .video-wrapper {
            position: relative;
            padding-bottom: 56.25%;
            height: 0;
            overflow: hidden;
            border-radius: var(--radius-sm);
            margin: 16px 0;
            background: var(--bg-secondary);
        }
        .video-wrapper iframe {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            border: none;
        }
        .video-caption {
            font-size: 0.85rem;
            color: var(--text-muted);
            margin-top: 8px;
            font-style: italic;
        }
        .waiver-form {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            padding: 32px;
            margin-top: 24px;
        }
        .form-group {
            margin-bottom: 20px;
        }
        .form-group label {
            display: block;
            margin-bottom: 6px;
            font-weight: 500;
            font-size: 0.9rem;
        }
        .form-group input,
        .form-group textarea,
        .form-group select {
            width: 100%;
            padding: 12px 16px;
            background: var(--bg-secondary);
            border: 1px solid var(--border);
            border-radius: var(--radius-sm);
            color: var(--text-primary);
            font-family: inherit;
            font-size: 0.95rem;
            transition: var(--transition);
        }
        .form-group input:focus,
        .form-group textarea:focus,
        .form-group select:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px var(--accent-glow);
        }
        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 16px;
        }
        .waiver-preview {
            background: var(--bg-secondary);
            border: 1px solid var(--border);
            border-radius: var(--radius-sm);
            padding: 24px;
            margin-top: 24px;
            max-height: 400px;
            overflow-y: auto;
            font-family: Georgia, serif;
            line-height: 1.8;
            color: var(--text-primary);
            display: none;
        }
        .waiver-preview.active {
            display: block;
        }
        .waiver-preview h3 {
            font-family: Inter, sans-serif;
            margin-bottom: 16px;
            text-align: center;
        }
        .hub-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
            margin-top: 24px;
        }
        .hub-card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            padding: 24px;
            text-align: center;
        }
        .hub-avatar {
            width: 64px; height: 64px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--accent), #8b5cf6);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            margin: 0 auto 16px;
        }
        .hub-card h4 {
            margin-bottom: 4px;
        }
        .hub-card .role {
            color: var(--accent-hover);
            font-size: 0.85rem;
            font-weight: 600;
            margin-bottom: 12px;
        }
        .hub-card p {
            color: var(--text-secondary);
            font-size: 0.9rem;
        }
        .checklist-container {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: var(-Openguide
-radius);
            padding: 32px;
            margin-top: 24px;
        }
        .checklist-item {
            display: flex;
            align-items: flex-start;
            gap: 16px;
            padding: 16px;
            border-radius: var(--radius-sm);
            transition: var(--transition);
            cursor: pointer;
            border-bottom: 1px solid var(--border);
        }
        .checklist-item:last-child { border-bottom: none; }
        .checklist-item:hover { background: rgba(255,255,255,0.02); }
        .checklist-item.completed { opacity: 0.65; }
        .checklist-item.completed .checklist-text h4 {
            text-decoration: line-through;
            color: var(--text-muted);
        }
        .checklist-box {
            width: 24px; height: 24px;
            border: 2px solid var(--border);
            border-radius: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
            margin-top: 2px;
            transition: var(--transition);
            font-size: 0.85rem;
            font-weight: 700;
        }
        .checklist-item.completed .checklist-box {
            background: var(--success);
            border-color: var(--success);
            color: white;
        }
        .checklist-text h4 {
            font-size: 1rem;
            margin-bottom: 4px;
        }
        .checklist-text p {
            font-size: 0.85rem;
            color: var(--text-secondary);
        }
        /* Voice section */
        .voice-demo {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            padding: 32px;
            margin-top: 24px;
            text-align: center;
        }
        .voice-input {
            width: 100%;
            padding: 16px;
            background: var(--bg-secondary);
            border: 1px solid var(--border);
            border-radius: var(--radius-sm);
            color: var(--text-primary);
            font-family: inherit;
            font-size: 1rem;
            margin-bottom: 16px;
            resize: vertical;
            min-height: 120px;
        }
        .voice-input:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px var(--accent-glow);
        }
        .api-key-input {
            width: 100%;
            padding: 12px 16px;
            background: var(--bg-secondary);
            border: 1px solid var(--border);
            border-radius: var(--radius-sm);
            color: var(--text-primary);
            font-family: inherit;
            font-size: 0.9rem;
            margin-bottom: 16px;
        }
        .api-key-input:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px var(--accent-glow);
        }
        /* Footer */
        footer {
            border-top: 1px solid var(--border);
            padding: 48px 24px;
            text-align: center;
            color: var(--text-muted);
            font-size: 0.9rem;
        }
        .footer-links {
            display: flex;
            justify-content: center;
            gap: 24px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        .footer-links a {
            color: var(--text-secondary);
            text-decoration: none;
            transition: var(--transition);
            font-weight: 500;
        }
        .footer-links a:hover {
            color: var(--accent-hover);
        }
        /* Toast */
        .toast {
            position: fixed;
            bottom: 24px;
            right: 24px;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-left: 4px solid var(--accent);
            padding: 16px 24px;
            border-radius: var(--radius-sm);
            box-shadow: 0 8px 32px rgba(0,0,0,0.4);
            transform: translateY(100px);
            opacity: 0;
            transition: all 0.3s ease;
            z-index: 9999;
            max-width: 360px;
            font-weight: 500;
        }
        .toast.show {
            transform: translateY(0);
            opacity: 1;
        }
        /* Mobile menu */
        .mobile-menu {
            display: none;
            position: absolute;
            top: 64px;
            left: 0; right: 0;
            background: var(--bg-secondary);
            border-bottom: 1px solid var(--border);
            padding: 16px;
        }
        .mobile-menu.open { display: block; }
        .mobile-menu a {
            display: block;
            padding: 12px 16px;
            color: var(--text-secondary);
            text-decoration: none;
            border-radius: var(--radius-sm);
            font-weight: 500;
        }
        .mobile-menu a:hover {
            background: var(--bg-tertiary);
            color: var(--text-primary);
        }
        /* Responsive */
        @media (max-width: 768px) {
            .nav-links { display: none; }
            .menu-toggle { display: block; }
            .hero { padding: 80px 16px 40px; }
            .section { padding: 60px 16px; }
            .form-row { grid-template-columns: 1fr; }
            .milestone-track {
                flex-wrap: wrap;
                gap: 16px;
            }
            .milestone-track::before { display: none; }
            .milestone-step { flex: 1 1 30%; min-width: 80px; }
            .card-grid { grid-template-columns: 1fr; }
            .hub-grid { grid-template-columns: 1fr; }
            .hero-stats { grid-template-columns: 1fr 1fr; }
            .toast {
                left: 16px; right: 16px;
                max-width: none;
            }
        }
        @media print {
            nav, .btn, .audio-controls, .menu-toggle, footer { display: none !important; }
            .section { display: block !important; padding: 20px; }
            .waiver-preview { display: block !important; border: 2px solid #000; }
            body { background: white; color: black; }
        }
    </style>
</head>
<body>
    <a href="#main" class="skip-link">Skip to content</a>
    <nav role="navigation" aria-label="Main">
        <div class="nav-container">
            <a href="#" class="logo" onclick="showSection('home'); return false;">
                <div class="logo-icon">🐕‍🦺</div>
                OpenGuide
            </a>
            <ul class="nav-links" role="menubar">
                <li><a href="#home" onclick="showSection('home')" class="active" role="menuitem">Home</a></li>
                <li><a href="#training" onclick="showSection('training')" role="menuitem">Training</a></li>
                <li><a href="#voice" onclick="showSection('voice')" role="menuitem">Voice</a></li>
                <li><a href="#ada" onclick="showSection('ada')" role="menuitem">ADA</a></li>
                <li><a href="#community" onclick="showSection('community')" role="menuitem">Community</a></li>
                <li><a href="#waiver" onclick="showSection('waiver')" role="menuitem">Waiver</a></li>
            </ul>
            <button class="menu-toggle" onclick="toggleMenu()" aria-label="Toggle menu">☰</button>
        </div>
        <div class="mobile-menu" id="mobileMenu">
            <a href="#home" onclick="showSection('home'); toggleMenu()">Home</a>
            <a href="#training" onclick="showSection('training'); toggleMenu()">Training</a>
            <a href="#voice" onclick="showSection('voice'); toggleMenu()">Voice</a>
            <a href="#ada" onclick="showSection('ada'); toggleMenu()">ADA</a>
            <a href="#community" onclick="showSection('community'); toggleMenu()">Community</a>
            <a href="#waiver" onclick="showSection('waiver'); toggleMenu()">Waiver</a>
        </div>
    </nav>

    <main id="main">
        <!-- HOME SECTION -->
        <section id="home" class="section active">
            <div class="hero">
                <div class="hero-badge">🐾 DEV Dog Days 2026</div>
                <h1>Turning Rescue Dogs<br>into <span>Guide Dogs</span></h1>
                <p>OpenGuide is a free, accessible platform that helps rescues and volunteers train service dogs using structured curricula, voice-guided lessons, and community support.</p>
                <div style="display:flex; gap:12px; justify-content:center; flex-wrap:wrap;">
                    <button class="btn btn-primary" onclick="showSection('training')">Start Training →</button>
                    <button class="btn btn-secondary" onclick="showSection('ada')">ADA Checklist</button>
                </div>
                <div class="hero-stats">
                    <div class="stat-card">
                        <span class="stat-number" id="statDogs">0</span>
                        <span class="stat-label">Dogs in Training</span>
                    </div>
                    <div class="stat-card">
                        <span class="stat-number">12</span>
                        <span class="stat-label">Training Modules</span>
                    </div>
                    <div class="stat-card">
                        <span class="stat-number">100%</span>
                        <span class="stat-label">Free & Open</span>
                    </div>
                    <div class="stat-card">
                        <span class="stat-number" id="statGrad">0</span>
                        <span class="stat-label">Graduated Teams</span>
                    </div>
                </div>
            </div>

            <div class="section-header" style="text-align:center; margin-top:60px;">
                <h2>Why OpenGuide?</h2>
                <p>Professional guide dog programs cost $25K–$50K per dog. We're changing that.</p>
            </div>
            <div class="card-grid">
                <div class="card">
                    <h3>📚 Structured Curriculum</h3>
                    <p>Step-by-step training modules based on ADI standards, from basic obedience to advanced guiding tasks.</p>
                </div>
                <div class="card">
                    <h3>🔊 Voice-Guided Lessons</h3>
                    <p>Hands-free audio instructions powered by ElevenLabs — train while you handle the leash.</p>
                </div>
                <div class="card">
                    <h3>✅ ADA Compliance Tools</h3>
                    <p>Built-in checklists and documentation to ensure your dog meets public access requirements.</p>
                </div>
                <div class="card">
                    <h3>🤝 Community Hub</h3>
                    <p>Connect with trainers, fosters, and recipients. Share progress, ask questions, find mentors.</p>
                </div>
                <div class="card">
                    <h3>🎥 Video Library</h3>
                    <p>Curated YouTube training videos embedded directly into each module for visual reference.</p>
                </div>
                <div class="card">
                    <h3>📋 Digital Waivers</h3>
                    <p>Built-in liability waivers and volunteer agreements, signable right from your phone.</p>
                </div>
            </div>
        </section>

        <!-- TRAINING SECTION -->
        <section id="training" class="section">
            <div class="section-header">
                <h2>Training Curriculum</h2>
                <p>Follow the milestone path from rescue intake to certified guide dog. Click any milestone to see details.</p>
            </div>

            <div class="milestone-container">
                <div class="milestone-track" role="tablist" aria-label="Training milestones">
                    <button class="milestone-step active" onclick="setMilestone(0)" role="tab" aria-selected="true">
                        <div class="milestone-dot">1</div>
                        <span class="milestone-label">Intake & Assessment</span>
                    </button>
                    <button class="milestone-step" onclick="setMilestone(1)" role="tab" aria-selected="false">
                        <div class="milestone-dot">2</div>
                        <span class="milestone-label">Basic Obedience</span>
                    </button>
                    <button class="milestone-step" onclick="setMilestone(2)" role="tab" aria-selected="false">
                        <div class="milestone-dot">3</div>
                        <span class="milestone-label">Public Access</span>
                    </button>
                    <button class="milestone-step" onclick="setMilestone(3)" role="tab" aria-selected="false">
                        <div class="milestone-dot">4</div>
                        <span class="milestone-label">Task Training</span>
                    </button>
                    <button class="milestone-step" onclick="setMilestone(4)" role="tab" aria-selected="false">
                        <div class="milestone-dot">5</div>
                        <span class="milestone-label">Team Matching</span>
                    </button>
                    <button class="milestone-step" onclick="setMilestone(5)" role="tab" aria-selected="false">
                        <div class="milestone-dot">6</div>
                        <span class="milestone-label">Certification</span>
                    </button>
                </div>

                <div id="milestoneDetails"></div>

                <div class="progress-wrapper">
                    <div class="progress-header">
                        <span>Overall Progress</span>
                        <span id="progressPercent">0%</span>
                    </div>
                    <div class="progress-bar" role="progressbar" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100">
                        <div class="progress-fill" id="progressFill"></div>
                    </div>
                </div>
            </div>

            <div class="section-header" style="margin-top:60px;">
                <h2>Training Modules</h2>
                <p>Expand each module to access videos, audio lessons, and step-by-step guides.</p>
            </div>
            <div class="module-list" id="moduleList"></div>
        </section>

        <!-- VOICE SECTION -->
        <section id="voice" class="section">
            <div class="section-header">
                <h2>Voice-Guided Training</h2>
                <p>Hands-free audio instruction so you can focus on your dog, not your screen. Use browser TTS now, or connect your ElevenLabs API key for premium voices.</p>
            </div>

            <div class="voice-demo">
                <h3 style="margin-bottom:16px;">🎙️ Try a Voice Lesson</h3>
                <p style="color:var(--text-secondary); margin-bottom:20px;">Select a preset command or type your own training cue. The voice will guide you through the exercise.</p>
                
                <select id="voicePreset" class="api-key-input" style="margin-bottom:12px;">
                    <option value="">-- Choose a preset lesson --</option>
                    <option value="heel">Heel Position & Loose Leash Walking</option>
                    <option value="sit">Sit-Stay with Distractions</option>
                    <option value="down">Down-Stay Duration Build</option>
                    <option value="come">Recall from 20ft with Distractions</option>
                    <option value="ignore">Ignore Food on Ground</option>
                </select>

                <textarea id="voiceText" class="voice-input" placeholder="Or type your own training instructions here...">Welcome to OpenGuide. Today we'll practice heel position. Start with your dog on your left side. Hold a treat at your hip. Take one step forward. If your dog moves with you, say 'Yes!' and reward. Repeat for five steps, then ten.</textarea>
                
                <div class="audio-controls">
                    <button class="audio-btn" onclick="speakText()" id="speakBtn">▶️ Speak Lesson</button>
                    <button class="audio-btn" onclick="pauseSpeech()" id="pauseBtn" disabled>⏸️ Pause</button>
                    <button class="audio-btn" onclick="stopSpeech()" id="stopBtn" disabled>⏹️ Stop</button>
                </div>

                <div style="margin-top:24px; padding-top:24px; border-top:1px solid var(--border);">
                    <h4 style="margin-bottom:12px; font-size:0.95rem;">🔑 ElevenLabs Integration (Optional)</h4>
                    <p style="color:var(--text-secondary); font-size:0.85rem; margin-bottom:12px;">Paste your API key to use premium AI voices. Key is stored locally in your browser only.</p>
                    <input type="password" id="elevenKey" class="api-key-input" placeholder="ElevenLabs API Key (sk_...)">
                    <button class="audio-btn" onclick="saveElevenKey()">💾 Save Key</button>
                    <button class="audio-btn" onclick="clearElevenKey()">🗑️ Clear</button>
                    <p id="keyStatus" style="font-size:0.8rem; margin-top:8px; color:var(--text-muted);"></p>
                </div>
            </div>
        </section>

        <!-- ADA SECTION -->
        <section id="ada" class="section">
            <div class="section-header">
                <h2>ADA Compliance Checklist</h2>
                <p>Ensure your service dog team meets the requirements for public access under the Americans with Disabilities Act. Check items off as you complete them — progress saves automatically.</p>
            </div>

            <div class="checklist-container">
                <div id="adaChecklist"></div>
            </div>

            <div style="margin-top:32px; text-align:center;">
                <button class="btn btn-primary" onclick="exportChecklist()">📥 Export Progress</button>
                <button class="btn btn-secondary" onclick="resetChecklist()">🔄 Reset All</button>
            </div>
        </section>

        <!-- COMMUNITY SECTION -->
        <section id="community" class="section">
            <div class="section-header">
                <h2>Community Hub</h2>
                <p>Meet the trainers, fosters, and volunteers making OpenGuide possible.</p>
            </div>

            <div class="hub-grid">
                <div class="hub-card">
                    <div class="hub-avatar">👩‍🏫</div>
                    <h4>Sarah Chen</h4>
                    <div class="role">Lead Trainer</div>
                    <p>15 years experience with guide dogs. Specializes in mobility task training and handler education.</p>
                </div>
                <div class="hub-card">
                    <div class="hub-avatar">👨‍⚕️</div>
                    <h4>Dr. Marcus Webb</h4>
                    <div class="role">Veterinary Advisor</div>
                    <p>Board-certified veterinary behaviorist. Reviews all health and temperament protocols.</p>
                </div>
                <div class="hub-card">
                    <div class="hub-avatar">🧑‍🤝‍🧑</div>
                    <h4>Jesse & River</h4>
                    <div class="role">Graduated Team</div>
                    <p>First OpenGuide graduate team. River, a Lab mix from a county shelter, now guides Jesse daily.</p>
                </div>
                <div class="hub-card">
                    <div class="hub-avatar">🏠</div>
                    <h4>Paws & Hearts Rescue</h4>
                    <div class="role">Partner Rescue</div>
                    <p>Provides temperament-tested dogs for the program. 8 dogs currently in foster-to-train pipeline.</p>
                </div>
            </div>

            <div class="section-header" style="margin-top:60px;">
                <h2>Join the Conversation</h2>
                <p>Share updates, ask questions, and celebrate milestones.</p>
            </div>
            <div class="card" style="max-width:600px; margin:0 auto;">
                <h3>💬 Discu
