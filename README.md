<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GitHub Profile — AI/ML Engineer</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=Space+Mono:ital,wght@0,400;0,700;1,400&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #030712;
    --surface: #0d1117;
    --surface2: #111827;
    --border: rgba(255,255,255,0.06);
    --accent: #00f5d4;
    --accent2: #7c3aed;
    --accent3: #f59e0b;
    --text: #f1f5f9;
    --muted: #64748b;
    --glow: 0 0 40px rgba(0,245,212,0.15);
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    position: fixed; width: 12px; height: 12px;
    background: var(--accent); border-radius: 50%;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, width 0.3s, height 0.3s, opacity 0.3s;
    mix-blend-mode: difference;
  }
  .cursor-trail {
    position: fixed; width: 36px; height: 36px;
    border: 1px solid rgba(0,245,212,0.4); border-radius: 50%;
    pointer-events: none; z-index: 9998;
    transform: translate(-50%, -50%);
    transition: all 0.18s ease;
  }

  /* Canvas bg */
  #bg-canvas {
    position: fixed; inset: 0; z-index: 0;
    pointer-events: none; opacity: 0.5;
  }

  .wrapper { position: relative; z-index: 1; }

  /* ---- HERO ---- */
  .hero {
    min-height: 100vh;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    padding: 80px 24px 60px;
    position: relative;
    text-align: center;
  }

  .hero::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(ellipse 80% 60% at 50% 0%, rgba(124,58,237,0.18) 0%, transparent 70%),
                radial-gradient(ellipse 60% 50% at 80% 80%, rgba(0,245,212,0.1) 0%, transparent 60%);
    pointer-events: none;
  }

  .badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(0,245,212,0.08);
    border: 1px solid rgba(0,245,212,0.25);
    color: var(--accent); padding: 6px 16px; border-radius: 100px;
    font-family: 'Space Mono', monospace; font-size: 11px; letter-spacing: 0.12em;
    text-transform: uppercase; margin-bottom: 32px;
    animation: fadeUp 0.8s ease both;
  }
  .badge::before { content: '▶'; font-size: 8px; }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(52px, 10vw, 110px);
    font-weight: 800; line-height: 0.9;
    letter-spacing: -0.03em;
    animation: fadeUp 0.8s 0.1s ease both;
  }

  .hero-name .line1 { display: block; color: var(--text); }
  .hero-name .line2 {
    display: block;
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 60%, var(--accent3) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-tagline {
    margin-top: 28px;
    font-size: clamp(14px, 2vw, 18px);
    color: var(--muted); max-width: 540px;
    line-height: 1.7;
    font-weight: 300;
    animation: fadeUp 0.8s 0.2s ease both;
  }

  .hero-tagline strong { color: var(--text); font-weight: 500; }

  .typing-wrap {
    margin-top: 20px;
    font-family: 'Space Mono', monospace;
    font-size: 13px; color: var(--accent);
    animation: fadeUp 0.8s 0.3s ease both;
  }
  .typing::after {
    content: '|'; animation: blink 1s step-end infinite;
  }
  @keyframes blink { 50% { opacity: 0; } }

  .hero-cta {
    margin-top: 44px;
    display: flex; gap: 14px; flex-wrap: wrap; justify-content: center;
    animation: fadeUp 0.8s 0.4s ease both;
  }

  .btn {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 13px 28px; border-radius: 10px;
    font-family: 'Syne', sans-serif; font-weight: 600; font-size: 14px;
    text-decoration: none; cursor: none;
    transition: transform 0.25s, box-shadow 0.25s;
    letter-spacing: 0.02em;
  }
  .btn-primary {
    background: var(--accent); color: #030712;
    box-shadow: 0 0 30px rgba(0,245,212,0.3);
  }
  .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 0 50px rgba(0,245,212,0.5); }
  .btn-ghost {
    background: transparent; color: var(--text);
    border: 1px solid var(--border);
  }
  .btn-ghost:hover { transform: translateY(-3px); border-color: rgba(255,255,255,0.2); }

  /* Scroll indicator */
  .scroll-hint {
    position: absolute; bottom: 32px; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    font-family: 'Space Mono', monospace; font-size: 10px; color: var(--muted);
    letter-spacing: 0.15em; text-transform: uppercase;
    animation: fadeUp 1s 1s ease both;
  }
  .scroll-line {
    width: 1px; height: 50px;
    background: linear-gradient(to bottom, var(--accent), transparent);
    animation: scrollPulse 2s ease-in-out infinite;
  }
  @keyframes scrollPulse { 0%,100%{opacity:0.3;transform:scaleY(1)} 50%{opacity:1;transform:scaleY(1.1)} }

  /* ---- STATS BAR ---- */
  .stats-bar {
    background: var(--surface);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    padding: 28px 24px;
    display: flex; justify-content: center;
    gap: 0;
  }
  .stat {
    flex: 1; max-width: 200px;
    text-align: center; padding: 0 24px;
    border-right: 1px solid var(--border);
  }
  .stat:last-child { border-right: none; }
  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 32px; font-weight: 800;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .stat-label { font-size: 11px; color: var(--muted); letter-spacing: 0.1em; text-transform: uppercase; margin-top: 4px; }

  /* ---- SECTIONS ---- */
  .section {
    padding: 100px 24px;
    max-width: 1100px; margin: 0 auto;
  }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--accent); margin-bottom: 16px;
    display: flex; align-items: center; gap: 12px;
  }
  .section-label::after {
    content: ''; flex: 1; max-width: 60px; height: 1px;
    background: var(--accent); opacity: 0.4;
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(32px, 5vw, 52px); font-weight: 800;
    letter-spacing: -0.02em; line-height: 1.05;
    margin-bottom: 16px;
  }

  .section-sub { color: var(--muted); font-size: 16px; line-height: 1.7; max-width: 520px; }

  /* ---- SKILLS GRID ---- */
  .skills-layout {
    display: grid; grid-template-columns: 1fr 1fr 1fr;
    gap: 20px; margin-top: 60px;
  }

  @media(max-width: 768px) {
    .skills-layout { grid-template-columns: 1fr; }
    .stat { display: none; }
    .stat:first-child, .stat:last-child { display: block; }
  }

  .skill-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px; padding: 32px 28px;
    position: relative; overflow: hidden;
    transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
    cursor: none;
  }
  .skill-card::before {
    content: ''; position: absolute;
    top: 0; left: 0; right: 0; height: 3px;
    background: var(--card-accent, var(--accent));
    transform: scaleX(0); transform-origin: left;
    transition: transform 0.4s ease;
  }
  .skill-card:hover { transform: translateY(-6px); border-color: rgba(255,255,255,0.12); }
  .skill-card:hover::before { transform: scaleX(1); }
  .skill-card:hover { box-shadow: 0 20px 60px rgba(0,0,0,0.4); }

  .skill-card.primary { --card-accent: var(--accent); }
  .skill-card.secondary { --card-accent: var(--accent2); }
  .skill-card.tertiary { --card-accent: var(--accent3); }
  .skill-card.featured {
    grid-column: span 2;
    background: linear-gradient(135deg, rgba(0,245,212,0.05) 0%, rgba(124,58,237,0.05) 100%);
  }

  .skill-icon {
    width: 52px; height: 52px;
    background: rgba(255,255,255,0.05);
    border-radius: 14px; display: flex; align-items: center; justify-content: center;
    font-size: 26px; margin-bottom: 20px;
  }

  .skill-title {
    font-family: 'Syne', sans-serif; font-weight: 700;
    font-size: 20px; margin-bottom: 10px;
  }

  .skill-desc { color: var(--muted); font-size: 14px; line-height: 1.7; }

  .tag-list { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 18px; }
  .tag {
    padding: 4px 12px; border-radius: 100px;
    font-family: 'Space Mono', monospace; font-size: 10px;
    letter-spacing: 0.08em; text-transform: uppercase;
    background: rgba(255,255,255,0.05); border: 1px solid var(--border);
    color: var(--muted);
    transition: color 0.2s, border-color 0.2s;
  }
  .skill-card:hover .tag { color: var(--text); border-color: rgba(255,255,255,0.15); }

  /* Progress bars */
  .skill-bars { margin-top: 18px; display: flex; flex-direction: column; gap: 12px; }
  .bar-item { }
  .bar-top { display: flex; justify-content: space-between; margin-bottom: 6px; font-size: 12px; color: var(--muted); }
  .bar-track { height: 4px; background: rgba(255,255,255,0.06); border-radius: 100px; overflow: hidden; }
  .bar-fill {
    height: 100%; border-radius: 100px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    width: 0%; transition: width 1.2s cubic-bezier(0.4,0,0.2,1);
  }

  /* ---- TECH STACK ---- */
  .tech-section {
    padding: 80px 24px;
    background: var(--surface);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
  }
  .tech-inner { max-width: 1100px; margin: 0 auto; }

  .tech-grid {
    display: flex; flex-wrap: wrap; gap: 12px;
    margin-top: 48px;
  }

  .tech-chip {
    display: inline-flex; align-items: center; gap: 10px;
    padding: 10px 20px; border-radius: 12px;
    background: rgba(255,255,255,0.04);
    border: 1px solid var(--border);
    font-size: 13px; font-weight: 500;
    transition: all 0.25s;
    cursor: none;
  }
  .tech-chip:hover {
    background: rgba(0,245,212,0.08);
    border-color: rgba(0,245,212,0.3);
    color: var(--accent); transform: scale(1.05);
  }
  .tech-chip .dot {
    width: 7px; height: 7px; border-radius: 50%;
  }

  /* ---- TIMELINE ---- */
  .journey-section { padding: 100px 24px; max-width: 1100px; margin: 0 auto; }

  .timeline { margin-top: 60px; position: relative; }
  .timeline::before {
    content: ''; position: absolute;
    left: 0; top: 0; bottom: 0; width: 1px;
    background: linear-gradient(to bottom, var(--accent), var(--accent2), transparent);
  }

  .tl-item {
    padding: 0 0 48px 40px; position: relative;
  }
  .tl-dot {
    position: absolute; left: -5px; top: 4px;
    width: 11px; height: 11px; border-radius: 50%;
    background: var(--accent); border: 2px solid var(--bg);
    box-shadow: 0 0 12px rgba(0,245,212,0.6);
  }
  .tl-year {
    font-family: 'Space Mono', monospace;
    font-size: 11px; color: var(--accent); letter-spacing: 0.12em;
    text-transform: uppercase; margin-bottom: 8px;
  }
  .tl-title {
    font-family: 'Syne', sans-serif; font-weight: 700;
    font-size: 22px; margin-bottom: 8px;
  }
  .tl-desc { color: var(--muted); font-size: 14px; line-height: 1.7; max-width: 500px; }

  /* ---- CONTACT ---- */
  .contact-section {
    padding: 120px 24px;
    text-align: center;
    position: relative;
  }
  .contact-section::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(ellipse 70% 60% at 50% 100%, rgba(124,58,237,0.15) 0%, transparent 70%);
    pointer-events: none;
  }

  .contact-inner { max-width: 640px; margin: 0 auto; position: relative; }

  .contact-links {
    display: flex; justify-content: center;
    flex-wrap: wrap; gap: 16px; margin-top: 48px;
  }

  .contact-card {
    display: flex; align-items: center; gap: 12px;
    padding: 16px 28px; border-radius: 14px;
    background: var(--surface);
    border: 1px solid var(--border);
    font-weight: 500; font-size: 14px;
    text-decoration: none; color: var(--text);
    transition: all 0.25s; cursor: none;
  }
  .contact-card:hover {
    border-color: var(--accent);
    box-shadow: 0 0 30px rgba(0,245,212,0.15);
    transform: translateY(-4px);
  }
  .contact-icon { font-size: 20px; }

  /* ---- FOOTER ---- */
  footer {
    border-top: 1px solid var(--border);
    padding: 32px 24px;
    text-align: center;
    font-family: 'Space Mono', monospace;
    font-size: 11px; color: var(--muted);
    letter-spacing: 0.1em;
  }
  footer span { color: var(--accent); }

  /* ---- ANIMATIONS ---- */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .reveal {
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }

  /* Glitch text effect */
  .glitch {
    position: relative;
  }
  .glitch::before, .glitch::after {
    content: attr(data-text);
    position: absolute; inset: 0;
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 60%, var(--accent3) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .glitch::before {
    animation: glitch1 4s infinite;
    clip-path: polygon(0 20%, 100% 20%, 100% 40%, 0 40%);
  }
  .glitch::after {
    animation: glitch2 4s infinite;
    clip-path: polygon(0 60%, 100% 60%, 100% 80%, 0 80%);
  }
  @keyframes glitch1 {
    0%,90%,100%{transform:translate(0)} 92%{transform:translate(-3px,1px)} 94%{transform:translate(3px,-1px)} 96%{transform:translate(-1px,0)}
  }
  @keyframes glitch2 {
    0%,90%,100%{transform:translate(0)} 91%{transform:translate(3px,-1px)} 93%{transform:translate(-3px,1px)} 95%{transform:translate(2px,0)}
  }

  /* Floating orbs */
  .orbs {
    position: fixed; inset: 0; pointer-events: none; z-index: 0; overflow: hidden;
  }
  .orb {
    position: absolute; border-radius: 50%;
    filter: blur(80px); opacity: 0.07;
    animation: orbFloat linear infinite;
  }
  .orb1 { width: 600px; height: 600px; background: var(--accent2); top: -200px; left: -100px; animation-duration: 20s; }
  .orb2 { width: 400px; height: 400px; background: var(--accent); bottom: -100px; right: -100px; animation-duration: 25s; animation-delay: -8s; }
  .orb3 { width: 300px; height: 300px; background: var(--accent3); top: 50%; left: 50%; animation-duration: 18s; animation-delay: -5s; }
  @keyframes orbFloat {
    0%,100%{transform:translate(0,0) scale(1)}
    33%{transform:translate(40px,-30px) scale(1.05)}
    66%{transform:translate(-20px,40px) scale(0.95)}
  }

  /* Nav */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; justify-content: space-between; align-items: center;
    padding: 20px 40px;
    background: rgba(3,7,18,0.8);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
    animation: fadeDown 0.8s ease both;
  }
  @keyframes fadeDown {
    from { opacity: 0; transform: translateY(-20px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  .nav-logo {
    font-family: 'Syne', sans-serif; font-weight: 800;
    font-size: 20px; letter-spacing: -0.02em;
    color: var(--text);
  }
  .nav-logo span { color: var(--accent); }
  .nav-links { display: flex; gap: 32px; }
  .nav-links a {
    font-family: 'Space Mono', monospace; font-size: 11px;
    letter-spacing: 0.12em; text-transform: uppercase;
    color: var(--muted); text-decoration: none;
    transition: color 0.2s; cursor: none;
  }
  .nav-links a:hover { color: var(--accent); }

  @media(max-width: 600px) {
    nav { padding: 16px 20px; }
    .nav-links { gap: 16px; }
    .nav-links a { font-size: 9px; }
    .skills-layout { grid-template-columns: 1fr; }
    .skill-card.featured { grid-column: span 1; }
    .stats-bar { flex-wrap: wrap; }
    .stat { min-width: 50%; border-right: none; border-bottom: 1px solid var(--border); padding: 16px; }
  }
</style>
</head>
<body>

<!-- Cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-trail" id="cursor-trail"></div>

<!-- Orbs -->
<div class="orbs">
  <div class="orb orb1"></div>
  <div class="orb orb2"></div>
  <div class="orb orb3"></div>
</div>

<!-- Canvas -->
<canvas id="bg-canvas"></canvas>

<!-- Nav -->
<nav>
  <div class="nav-logo">Al Sami<span>.</span></div>
  <div class="nav-links">
    <a href="#skills">Skills</a>
    <a href="#stack">Stack</a>
    <a href="#journey">Journey</a>
    <a href="#contact">Contact</a>
  </div>
</nav>

<div class="wrapper">

  <!-- HERO -->
  <section class="hero">
    <div class="badge">Open to opportunities · 2026</div>
    <h1 class="hero-name">
      <span class="line1">Crafting</span>
      <span class="line2 glitch" data-text="Intelligent Systems">Intelligent Systems</span>
    </h1>
    <p class="hero-tagline">
      <strong>AI/ML Engineer & Full-Stack Developer</strong> — building deep learning models, scalable web apps, and Android experiences. Embedded systems enthusiast.
    </p>
    <div class="typing-wrap">
      &gt; <span class="typing" id="typing-text"></span>
    </div>
    <div class="hero-cta">
      <a href="#skills" class="btn btn-primary">View My Work ↓</a>
      <a href="#contact" class="btn btn-ghost">Get In Touch</a>
    </div>
    <div class="scroll-hint">
      <div class="scroll-line"></div>
      Scroll
    </div>
  </section>

  <!-- STATS -->
  <div class="stats-bar">
    <div class="stat">
      <div class="stat-num" data-target="3">0</div>
      <div class="stat-label">Years Learning</div>
    </div>
    <div class="stat">
      <div class="stat-num" data-target="20">0</div>
      <div class="stat-label">Projects Built</div>
    </div>
    <div class="stat">
      <div class="stat-num" data-target="8">0</div>
      <div class="stat-label">Tech Domains</div>
    </div>
    <div class="stat">
      <div class="stat-num" data-target="100">0</div>
      <div class="stat-label">% Passionate</div>
    </div>
  </div>

  <!-- SKILLS -->
  <section class="section" id="skills">
    <div class="section-label">What I Do</div>
    <h2 class="section-title reveal">Skills &<br>Expertise</h2>
    <p class="section-sub reveal reveal-delay-1">Focused on intelligent systems — from training neural nets to shipping mobile apps.</p>

    <div class="skills-layout">

      <!-- AI/ML — featured -->
      <div class="skill-card featured primary reveal">
        <div class="skill-icon">🧠</div>
        <div class="skill-title">Machine Learning & Deep Learning</div>
        <div class="skill-desc">My primary domain. Building and training models for computer vision, NLP, and predictive analytics. From data wrangling to production deployment.</div>
        <div class="skill-bars">
          <div class="bar-item">
            <div class="bar-top"><span>Neural Networks</span><span>30%</span></div>
            <div class="bar-track"><div class="bar-fill" data-width="90"></div></div>
          </div>
          <div class="bar-item">
            <div class="bar-top"><span>Computer Vision</span><span>50%</span></div>
            <div class="bar-track"><div class="bar-fill" data-width="82"></div></div>
          </div>
          <div class="bar-item">
            <div class="bar-top"><span>NLP / Transformers</span><span>20%</span></div>
            <div class="bar-track"><div class="bar-fill" data-width="75"></div></div>
          </div>
          <div class="bar-item">
            <div class="bar-top"><span>Model Deployment</span><span>50%</span></div>
            <div class="bar-track"><div class="bar-fill" data-width="70"></div></div>
          </div>
        </div>
        <div class="tag-list">
          <span class="tag">PyTorch</span><span class="tag">TensorFlow</span><span class="tag">scikit-learn</span>
          <span class="tag">Keras</span><span class="tag">HuggingFace</span><span class="tag">OpenCV</span>
        </div>
      </div>

      <!-- Web -->
      <div class="skill-card secondary reveal reveal-delay-1">
        <div class="skill-icon">🌐</div>
        <div class="skill-title">Web Development</div>
        <div class="skill-desc">Designing and building fast, responsive web experiences — from landing pages to full-stack applications.</div>
        <div class="skill-bars">
          <div class="bar-item">
            <div class="bar-top"><span>Frontend</span><span>78%</span></div>
            <div class="bar-track"><div class="bar-fill" data-width="78"></div></div>
          </div>
          <div class="bar-item">
            <div class="bar-top"><span>Backend / APIs</span><span>65%</span></div>
            <div class="bar-track"><div class="bar-fill" data-width="65"></div></div>
          </div>
        </div>
        <div class="tag-list">
          <span class="tag">React</span><span class="tag">Node.js</span><span class="tag">Python</span><span class="tag">HTML/CSS</span>
        </div>
      </div>

      <!-- Android -->
      <div class="skill-card secondary reveal reveal-delay-2">
        <div class="skill-icon">📱</div>
        <div class="skill-title">Android Development</div>
        <div class="skill-desc">Crafting native Android applications with clean UI and smooth user experiences using modern development practices.</div>
        <div class="skill-bars">
          <div class="bar-item">
            <div class="bar-top"><span>Kotlin / Java</span><span>70%</span></div>
            <div class="bar-track"><div class="bar-fill" data-width="70"></div></div>
          </div>
          <div class="bar-item">
            <div class="bar-top"><span>Jetpack Compose</span><span>60%</span></div>
            <div class="bar-track"><div class="bar-fill" data-width="60"></div></div>
          </div>
        </div>
        <div class="tag-list">
          <span class="tag">Android Studio</span><span class="tag">Kotlin</span><span class="tag">Firebase</span>
        </div>
      </div>

      <!-- Embedded -->
      <div class="skill-card tertiary reveal reveal-delay-1">
        <div class="skill-icon">⚡</div>
        <div class="skill-title">Embedded Systems</div>
        <div class="skill-desc">Exploring the bridge between software and hardware — microcontrollers, sensors, and IoT experimentation.</div>
        <div class="skill-bars">
          <div class="bar-item">
            <div class="bar-top"><span>Microcontrollers</span><span>50%</span></div>
            <div class="bar-track"><div class="bar-fill" data-width="50"></div></div>
          </div>
        </div>
        <div class="tag-list">
          <span class="tag">Arduino</span><span class="tag">Raspberry Pi</span><span class="tag">C/C++</span>
        </div>
      </div>

    </div>
  </section>

  <!-- TECH STACK -->
  <section class="tech-section" id="stack">
    <div class="tech-inner">
      <div class="section-label reveal">Technologies</div>
      <h2 class="section-title reveal">My Tech Stack</h2>
      <p class="section-sub reveal reveal-delay-1">Tools and languages I reach for daily.</p>

      <div class="tech-grid" id="tech-grid">
        <!-- JS rendered -->
      </div>
    </div>
  </section>

  <!-- JOURNEY -->
  <section class="journey-section" id="journey">
    <div class="section-label reveal">Background</div>
    <h2 class="section-title reveal">My Journey</h2>
    <p class="section-sub reveal reveal-delay-1">From curiosity to craft — how I got here.</p>

    <div class="timeline">
      <div class="tl-item reveal">
        <div class="tl-dot"></div>
        <div class="tl-year">2022 · Starting Out</div>
        <div class="tl-title">First Lines of Code</div>
        <div class="tl-desc">Started with Python, fell in love with logic and problem solving. Built first projects, discovered the power of programming to create real things.</div>
      </div>
      <div class="tl-item reveal reveal-delay-1">
        <div class="tl-dot"></div>
        <div class="tl-year">2023 · Going Deeper</div>
        <div class="tl-title">Diving into AI & ML</div>
        <div class="tl-desc">Discovered machine learning and became fascinated by neural networks. Started training models, exploring datasets, and building intelligent applications.</div>
      </div>
      <div class="tl-item reveal reveal-delay-2">
        <div class="tl-dot"></div>
        <div class="tl-year">2024 · Expanding</div>
        <div class="tl-title">Web & Android Development</div>
        <div class="tl-desc">Expanded into full-stack web development and Android apps to bring AI-powered ideas to life in products people can actually use.</div>
      </div>
      <div class="tl-item reveal reveal-delay-3">
        <div class="tl-dot" style="background:var(--accent3);box-shadow:0 0 12px rgba(245,158,11,0.6)"></div>
        <div class="tl-year">2025 · Now</div>
        <div class="tl-title">Building & Growing</div>
        <div class="tl-desc">Deepening expertise in deep learning and generative AI. Exploring embedded systems. Seeking opportunities to collaborate on meaningful, impactful projects.</div>
      </div>
    </div>
  </section>

  <!-- CONTACT -->
  <section class="contact-section" id="contact">
    <div class="contact-inner">
      <div class="section-label reveal" style="justify-content:center">Let's Connect</div>
      <h2 class="section-title reveal">Open To<br>Collaboration</h2>
      <p class="section-sub reveal reveal-delay-1" style="margin:0 auto; text-align:center">
        Whether it's a research project, open-source contribution, internship, or just a conversation about AI — I'm always interested.
      </p>
      <div class="contact-links reveal reveal-delay-2">
        <a href="https://github.com/al-sami-2005" class="contact-card">
          <span class="contact-icon">🐙</span> GitHub
        </a>
        <a href="www.linkedin.com/in/al-sami-10as70" class="contact-card">
          <span class="contact-icon">💼</span> LinkedIn
        </a>
        <a href="mailto:alsami10@gmail.com" class="contact-card">
          <span class="contact-icon">✉️</span> Email
        </a>
        <a href="https://wa.me/01516502591" class="contact-card">
          <span class="contact-icon">💬</span> WhatsApp
        </a>
      </div>
    </div>
  </section>

  <footer>
    Designed &amp; Built with precision · <span>Al Sami</span> · 2026
  </footer>

</div>

<script>
// ---- Cursor ----
const cursor = document.getElementById('cursor');
const trail = document.getElementById('cursor-trail');
let mx = 0, my = 0, tx = 0, ty = 0;
document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; cursor.style.left = mx+'px'; cursor.style.top = my+'px'; });
function animTrail() { tx += (mx-tx)*0.12; ty += (my-ty)*0.12; trail.style.left = tx+'px'; trail.style.top = ty+'px'; requestAnimationFrame(animTrail); }
animTrail();

// ---- Canvas particle field ----
const canvas = document.getElementById('bg-canvas');
const ctx = canvas.getContext('2d');
let W, H, particles = [];
function resize() { W = canvas.width = window.innerWidth; H = canvas.height = window.innerHeight; }
resize(); window.addEventListener('resize', resize);

class Particle {
  constructor() { this.reset(); }
  reset() {
    this.x = Math.random()*W; this.y = Math.random()*H;
    this.vx = (Math.random()-0.5)*0.3; this.vy = (Math.random()-0.5)*0.3;
    this.r = Math.random()*1.5+0.3;
    this.alpha = Math.random()*0.5+0.1;
  }
  update() {
    this.x += this.vx; this.y += this.vy;
    if(this.x<0||this.x>W||this.y<0||this.y>H) this.reset();
  }
  draw() {
    ctx.beginPath(); ctx.arc(this.x,this.y,this.r,0,Math.PI*2);
    ctx.fillStyle = `rgba(0,245,212,${this.alpha})`; ctx.fill();
  }
}

for(let i=0;i<120;i++) particles.push(new Particle());

function drawLines() {
  for(let i=0;i<particles.length;i++) {
    for(let j=i+1;j<particles.length;j++) {
      const d = Math.hypot(particles[i].x-particles[j].x, particles[i].y-particles[j].y);
      if(d<120) {
        ctx.beginPath();
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.strokeStyle = `rgba(0,245,212,${0.07*(1-d/120)})`; ctx.lineWidth=0.5; ctx.stroke();
      }
    }
  }
}

function loop() {
  ctx.clearRect(0,0,W,H);
  particles.forEach(p=>{ p.update(); p.draw(); });
  drawLines();
  requestAnimationFrame(loop);
}
loop();

// ---- Typing effect ----
const phrases = [
  'training neural networks...',
  'building deep learning models...',
  'shipping Android apps...',
  'crafting web experiences...',
  'exploring embedded systems...',
  'always learning...'
];
let pi=0, ci=0, deleting=false;
const typEl = document.getElementById('typing-text');
function typeLoop() {
  const phrase = phrases[pi];
  if(!deleting) {
    typEl.textContent = phrase.slice(0, ++ci);
    if(ci===phrase.length) { deleting=true; setTimeout(typeLoop, 1800); return; }
  } else {
    typEl.textContent = phrase.slice(0, --ci);
    if(ci===0) { deleting=false; pi=(pi+1)%phrases.length; }
  }
  setTimeout(typeLoop, deleting?40:55);
}
typeLoop();

// ---- Scroll reveal ----
const reveals = document.querySelectorAll('.reveal');
const io = new IntersectionObserver(entries => {
  entries.forEach(e => { if(e.isIntersecting) e.target.classList.add('visible'); });
}, { threshold: 0.12 });
reveals.forEach(el => io.observe(el));

// ---- Animated counters ----
const statNums = document.querySelectorAll('.stat-num');
const statIo = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if(e.isIntersecting) {
      const el = e.target, target = +el.dataset.target;
      let cur=0; const step = target/60;
      const t = setInterval(()=>{
        cur = Math.min(cur+step, target);
        el.textContent = Math.round(cur)+(target===100?'%':'+');
        if(cur>=target) clearInterval(t);
      },16);
      statIo.unobserve(el);
    }
  });
}, {threshold:0.5});
statNums.forEach(el => statIo.observe(el));

// ---- Progress bars ----
const barIo = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if(e.isIntersecting) {
      e.target.querySelectorAll('.bar-fill').forEach(b => {
        setTimeout(()=>{ b.style.width = b.dataset.width+'%'; }, 200);
      });
      barIo.unobserve(e.target);
    }
  });
}, {threshold:0.3});
document.querySelectorAll('.skill-card').forEach(c => barIo.observe(c));

// ---- Tech chips ----
const techs = [
  { name:'Python', color:'#3776ab' },
  { name:'PyTorch', color:'#ee4c2c' },
  { name:'TensorFlow', color:'#ff6f00' },
  { name:'scikit-learn', color:'#f7931e' },
  { name:'OpenCV', color:'#5c3ee8' },
  { name:'HuggingFace', color:'#ffd21e' },
  { name:'NumPy', color:'#4dabcf' },
  { name:'Pandas', color:'#150458' },
  { name:'Matplotlib', color:'#11557c' },
  { name:'React', color:'#61dafb' },
  { name:'Node.js', color:'#3c873a' },
  { name:'FastAPI', color:'#009688' },
  { name:'HTML/CSS', color:'#e34c26' },
  { name:'JavaScript', color:'#f0db4f' },
  { name:'Kotlin', color:'#7f52ff' },
  { name:'Android Studio', color:'#3ddc84' },
  { name:'Firebase', color:'#ffca28' },
  { name:'Git / GitHub', color:'#f14e32' },
  { name:'Linux', color:'#fcc624' },
  { name:'Arduino', color:'#00979d' },
  { name:'C / C++', color:'#659bd3' },
  { name:'Raspberry Pi', color:'#c51a4a' },
  { name:'Docker', color:'#2496ed' },
  { name:'REST APIs', color:'#6cbbda' },
];

const grid = document.getElementById('tech-grid');
techs.forEach((t,i) => {
  const chip = document.createElement('div');
  chip.className='tech-chip reveal';
  chip.style.transitionDelay = (i*0.03)+'s';
  chip.innerHTML = `<span class="dot" style="background:${t.color}"></span>${t.name}`;
  grid.appendChild(chip);
  io.observe(chip);
});
</script>
</body>
</html>
