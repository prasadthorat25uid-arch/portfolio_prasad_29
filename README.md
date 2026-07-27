 
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Prasad Sudhir Thorat — Cybersecurity & AI Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700;800&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">

<style>
  :root {
    --bg-void: #03060a;
    --bg-panel: rgba(16, 22, 31, 0.6);
    --bg-panel-2: rgba(20, 28, 39, 0.8);
    --border: rgba(69, 224, 196, 0.2);
    --border-soft: rgba(255, 255, 255, 0.05);
    --teal: #45E0C4;
    --teal-glow: rgba(69, 224, 196, 0.6);
    --amber: #F5A623;
    --amber-glow: rgba(245, 166, 35, 0.6);
    --text-1: #E7EEF5;
    --text-2: #8FA1B3;
    --text-3: #546477;
    --mono: 'JetBrains Mono', monospace;
    --sans: 'Inter', sans-serif;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; cursor: none; } /* Hide default cursor for custom one */
  html { scroll-behavior: smooth; }
  
  body {
    background: var(--bg-void);
    color: var(--text-1);
    font-family: var(--sans);
    line-height: 1.6;
    overflow-x: hidden;
  }

  /* CRT Scanline Overlay */
  body::after {
    content: " ";
    display: block;
    position: fixed;
    top: 0; left: 0; bottom: 0; right: 0;
    background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
    z-index: 100;
    background-size: 100% 2px, 3px 100%;
    pointer-events: none;
    opacity: 0.4;
  }

  /* Background Canvas */
  #network-canvas {
    position: fixed;
    top: 0; left: 0;
    width: 100vw; height: 100vh;
    z-index: 0;
    pointer-events: none;
  }

  .wrap { position: relative; z-index: 10; }
  a { color: inherit; text-decoration: none; cursor: none; }
  ::selection { background: var(--teal); color: #000; }

  /* Custom Cursor */
  #cursor {
    position: fixed;
    top: 0; left: 0;
    width: 20px; height: 20px;
    border: 2px solid var(--teal);
    border-radius: 50%;
    transform: translate(-50%, -50%);
    pointer-events: none;
    z-index: 9999;
    transition: width 0.2s, height 0.2s, background-color 0.2s;
    mix-blend-mode: difference;
  }
  #cursor::after {
    content: '';
    position: absolute;
    top: 50%; left: 50%;
    width: 4px; height: 4px;
    background: var(--amber);
    border-radius: 50%;
    transform: translate(-50%, -50%);
  }
  #cursor.hovering {
    width: 40px; height: 40px;
    background-color: rgba(69, 224, 196, 0.1);
    border-color: var(--amber);
  }

  /* ---------- NAV ---------- */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 50;
    display: flex; align-items: center; justify-content: space-between;
    padding: 20px 5vw;
    background: rgba(3, 6, 10, 0.7);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border-soft);
  }
  .nav-id {
    font-family: var(--mono); font-size: 14px; color: var(--teal);
    display: flex; align-items: center; gap: 10px;
    text-shadow: 0 0 10px var(--teal-glow);
  }
  .nav-id .dot { width: 8px; height: 8px; border-radius: 50%; background: var(--teal); box-shadow: 0 0 10px var(--teal); animation: pulse 2s infinite; }
  @keyframes pulse { 0%, 100% { opacity: 1; box-shadow: 0 0 12px var(--teal); } 50% { opacity: 0.3; box-shadow: 0 0 2px var(--teal); } }
  
  .nav-links { display: flex; gap: 32px; font-family: var(--mono); font-size: 13px; letter-spacing: 0.05em; text-transform: uppercase; }
  .nav-links a { color: var(--text-2); position: relative; padding: 4px 0; transition: color .3s; }
  .nav-links a:hover { color: var(--teal); text-shadow: 0 0 8px var(--teal-glow); }
  .nav-links a::after {
    content: ''; position: absolute; bottom: 0; left: 0; width: 0%; height: 1px; background: var(--teal); transition: width 0.3s ease;
  }
  .nav-links a:hover::after { width: 100%; }
  @media(max-width:820px) { .nav-links { display: none; } }

  /* ---------- HERO / BOOT SEQUENCE ---------- */
  .hero {
    min-height: 100vh;
    display: flex; flex-direction: column; justify-content: center;
    padding: 120px 5vw 80px;
    position: relative;
  }
  .terminal {
    max-width: 640px;
    font-family: var(--mono);
    font-size: 15px;
    color: var(--teal);
    min-height: 220px;
    background: rgba(0, 20, 15, 0.3);
    padding: 20px;
    border-radius: 8px;
    border: 1px solid var(--border);
    box-shadow: inset 0 0 20px rgba(69, 224, 196, 0.05);
  }
  .terminal .line { opacity: 0; white-space: pre; overflow: hidden; margin-bottom: 5px; }
  .terminal .prompt { color: var(--text-3); }
  .terminal .ok { color: var(--teal); text-shadow: 0 0 5px var(--teal-glow); }
  .terminal .granted { color: var(--amber); font-weight: 800; text-shadow: 0 0 8px var(--amber-glow); }
  .cursor { display: inline-block; width: 10px; height: 18px; background: var(--teal); vertical-align: middle; animation: blink 1s step-end infinite; margin-left: 4px; box-shadow: 0 0 8px var(--teal); }
  @keyframes blink { 50% { opacity: 0; } }

  /* ---------- PROFILE REVEAL ---------- */
  .profile-reveal {
    opacity: 0; transform: translateY(30px);
    transition: opacity 1s cubic-bezier(0.16, 1, 0.3, 1), transform 1s cubic-bezier(0.16, 1, 0.3, 1);
    margin-top: 50px;
    display: flex; align-items: center; gap: 50px;
    flex-wrap: wrap;
  }
  .profile-reveal.show { opacity: 1; transform: translateY(0); }
  
  .photo-frame {
    position: relative; width: 200px; height: 200px; flex-shrink: 0;
    perspective: 1000px;
  }
  .photo-inner {
    width: 100%; height: 100%; position: relative;
    border-radius: 12px;
    border: 1px solid var(--teal);
    box-shadow: 0 0 20px rgba(69, 224, 196, 0.15);
    overflow: hidden;
    background: var(--bg-panel-2);
  }
  .photo-inner img {
    width: 100%; height: 100%; object-fit: cover;
    filter: grayscale(40%) contrast(1.1) brightness(0.9);
    transition: filter 0.5s ease, transform 0.5s ease;
  }
  .photo-frame:hover .photo-inner img {
    filter: grayscale(0%) contrast(1.1) brightness(1.1);
    transform: scale(1.05);
  }
  .photo-frame::after {
    content: '[ Sai~Prasad';
    position: absolute; bottom: -15px; left: 50%; transform: translateX(-50%);
    font-family: var(--mono); font-size: 10px; letter-spacing: .2em;
    color: var(--teal); background: var(--bg-void);
    padding: 4px 12px; border: 1px solid var(--teal); border-radius: 20px;
    box-shadow: 0 0 10px var(--teal-glow);
  }

  /* Glitch Effect */
  .glitch {
    position: relative;
    font-family: var(--mono);
    font-size: clamp(32px, 5vw, 56px);
    font-weight: 800;
    letter-spacing: -0.02em;
    color: #fff;
    text-shadow: 0 0 10px rgba(255,255,255,0.2);
  }
  .glitch::before, .glitch::after {
    content: attr(data-text);
    position: absolute; top: 0; left: 0; width: 100%; height: 100%;
    background: var(--bg-void);
  }
  .glitch::before {
    left: 2px; text-shadow: -2px 0 var(--teal);
    clip: rect(24px, 550px, 90px, 0);
    animation: glitch-anim-2 3s infinite linear alternate-reverse;
  }
  .glitch::after {
    left: -2px; text-shadow: -2px 0 var(--amber);
    clip: rect(85px, 550px, 140px, 0);
    animation: glitch-anim 2.5s infinite linear alternate-reverse;
  }
  @keyframes glitch-anim {
    0% { clip: rect(10px, 9999px, 91px, 0); }
    20% { clip: rect(61px, 9999px, 19px, 0); }
    40% { clip: rect(23px, 9999px, 48px, 0); }
    60% { clip: rect(89px, 9999px, 13px, 0); }
    80% { clip: rect(31px, 9999px, 81px, 0); }
    100% { clip: rect(54px, 9999px, 12px, 0); }
  }
  @keyframes glitch-anim-2 {
    0% { clip: rect(29px, 9999px, 83px, 0); }
    20% { clip: rect(14px, 9999px, 71px, 0); }
    40% { clip: rect(98px, 9999px, 24px, 0); }
    60% { clip: rect(41px, 9999px, 59px, 0); }
    80% { clip: rect(72px, 9999px, 12px, 0); }
    100% { clip: rect(11px, 9999px, 93px, 0); }
  }

  .id-block .role { color: var(--teal); font-family: var(--mono); font-size: 15px; margin-top: 10px; letter-spacing: .05em; }
  .id-block .meta { color: var(--text-2); font-size: 14px; margin-top: 6px; }
  .id-block .tagline { margin-top: 20px; max-width: 520px; color: var(--text-2); font-size: 16px; line-height: 1.7; }
  
  .cta-row { margin-top: 30px; display: flex; gap: 16px; flex-wrap: wrap; align-items: center; }
  .btn {
    font-family: var(--mono); font-size: 13px; letter-spacing: .05em; text-transform: uppercase;
    padding: 12px 24px; border-radius: 4px;
    display: inline-flex; align-items: center; gap: 8px;
    transition: all .3s cubic-bezier(0.25, 0.8, 0.25, 1);
    position: relative; overflow: hidden;
  }
  .btn-primary {
    background: transparent; color: var(--teal); font-weight: 700;
    border: 1px solid var(--teal); box-shadow: 0 0 10px rgba(69, 224, 196, 0.1);
  }
  .btn-primary::before {
    content: ''; position: absolute; top: 0; left: -100%; width: 100%; height: 100%;
    background: var(--teal); transition: left 0.3s ease; z-index: -1;
  }
  .btn-primary:hover { color: var(--bg-void); box-shadow: 0 0 20px var(--teal-glow); }
  .btn-primary:hover::before { left: 0; }
  
  .icon-row { display: flex; gap: 12px; }
  .icon-btn {
    width: 42px; height: 42px; border-radius: 4px; border: 1px solid var(--border-soft);
    display: flex; align-items: center; justify-content: center;
    color: var(--text-2); transition: all .3s ease;
    background: var(--bg-panel);
  }
  .icon-btn:hover {
    border-color: var(--teal); color: var(--teal);
    transform: translateY(-3px); box-shadow: 0 5px 15px rgba(69, 224, 196, 0.2);
  }
  .icon-btn svg { width: 18px; height: 18px; }

  /* ---------- SECTION SHELL ---------- */
  section { padding: 120px 5vw; position: relative; border-top: 1px solid var(--border-soft); }
  .eyebrow {
    font-family: var(--mono); font-size: 13px; color: var(--amber);
    letter-spacing: .15em; text-transform: uppercase; margin-bottom: 16px;
    display: flex; align-items: center; gap: 10px;
    text-shadow: 0 0 5px var(--amber-glow);
  }
  .eyebrow::before { content: '~/'; color: var(--teal); }
  h2.sec-title {
    font-family: var(--mono); font-size: clamp(28px, 4vw, 40px); font-weight: 800;
    margin-bottom: 50px; color: #fff; letter-spacing: -0.02em;
  }
  .section-inner { max-width: 1200px; margin: 0 auto; }

  /* 3D Tilt Class */
  .tilt-card {
    transform-style: preserve-3d;
    transition: transform 0.1s ease, box-shadow 0.3s ease;
  }
  .tilt-card:hover {
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.5), 0 0 20px rgba(69, 224, 196, 0.1);
    border-color: var(--teal);
  }

  /* ---------- ABOUT ---------- */
  .about-grid { display: grid; grid-template-columns: 1.3fr 1fr; gap: 60px; align-items: start; }
  .about-grid p { color: var(--text-2); font-size: 17px; margin-bottom: 20px; max-width: 65ch; }
  .about-grid p strong { color: var(--teal); font-weight: 600; text-shadow: 0 0 3px rgba(69, 224, 196, 0.3); }
  
  .fact-panel {
    background: var(--bg-panel); border: 1px solid var(--border); border-radius: 12px;
    padding: 30px; backdrop-filter: blur(10px);
  }
  .fact-row { display: flex; justify-content: space-between; padding: 14px 0; border-bottom: 1px dashed var(--border-soft); font-size: 14.5px; }
  .fact-row:last-child { border-bottom: none; }
  .fact-row span:first-child { color: var(--teal); font-family: var(--mono); font-size: 13px; }
  .fact-row span:last-child { color: var(--text-1); text-align: right; font-weight: 500; }

  /* ---------- SKILLS ---------- */
  .skills-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 24px; }
  .skill-card {
    background: var(--bg-panel); border: 1px solid var(--border-soft); border-radius: 12px; padding: 28px;
    backdrop-filter: blur(5px);
  }
  .skill-card .cat { font-family: var(--mono); font-size: 13px; color: var(--amber); letter-spacing: .1em; text-transform: uppercase; margin-bottom: 18px; display: flex; align-items: center; gap: 8px;}
  .skill-card .cat::before { content: '>'; color: var(--teal); }
  .skill-tags { display: flex; flex-wrap: wrap; gap: 10px; transform: translateZ(20px); }
  .skill-tag {
    font-family: var(--mono); font-size: 12.5px; color: var(--text-2);
    border: 1px solid var(--border-soft); padding: 8px 14px; border-radius: 4px;
    transition: all .3s ease; background: rgba(0,0,0,0.2);
  }
  .skill-tag:hover {
    border-color: var(--teal); color: var(--bg-void); background: var(--teal);
    box-shadow: 0 0 15px var(--teal-glow); transform: translateY(-2px);
  }

  /* ---------- EXPERIENCE ---------- */
  .exp-card {
    background: var(--bg-panel); border: 1px solid var(--border-soft); border-radius: 12px;
    padding: 35px; position: relative; overflow: hidden; backdrop-filter: blur(5px);
  }
  .exp-card::before { content: ''; position: absolute; left: 0; top: 0; bottom: 0; width: 4px; background: linear-gradient(to bottom, var(--teal), var(--amber)); }
  .exp-head { display: flex; justify-content: space-between; flex-wrap: wrap; gap: 12px; margin-bottom: 20px; }
  .exp-head h3 { font-size: 22px; color: #fff; letter-spacing: -0.01em; transform: translateZ(30px); }
  .exp-head .company { color: var(--teal); font-size: 15px; margin-top: 6px; font-family: var(--mono); }
  .exp-head .date { font-family: var(--mono); font-size: 12.5px; color: var(--amber); border: 1px solid rgba(245, 166, 35, 0.3); background: rgba(245, 166, 35, 0.05); padding: 6px 14px; border-radius: 20px; height: fit-content; }
  .exp-card ul { list-style: none; color: var(--text-2); font-size: 15.5px; transform: translateZ(20px); }
  .exp-card li { padding-left: 24px; position: relative; margin-bottom: 12px; line-height: 1.6; }
  .exp-card li::before { content: '▹'; position: absolute; left: 0; color: var(--teal); font-family: var(--mono); font-size: 18px; top: -2px; }

  /* ---------- CERTIFICATIONS ---------- */
  .cert-groups { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 24px; }
  .cert-group {
    background: var(--bg-panel); border: 1px solid var(--border-soft); border-radius: 12px;
    padding: 28px; backdrop-filter: blur(5px);
  }
  .cert-group-head { display: flex; align-items: center; gap: 14px; margin-bottom: 20px; padding-bottom: 16px; border-bottom: 1px solid var(--border-soft); transform: translateZ(20px); }
  .cert-group-head .icon {
    width: 38px; height: 38px; border-radius: 8px; background: rgba(69, 224, 196, 0.1);
    display: flex; align-items: center; justify-content: center; color: var(--teal);
    border: 1px solid rgba(69, 224, 196, 0.2); box-shadow: 0 0 10px rgba(69, 224, 196, 0.1);
  }
  .cert-group-head h3 { font-size: 15px; color: #fff; font-family: var(--mono); letter-spacing: .05em; }
  .cert-list { list-style: none; transform: translateZ(10px); }
  .cert-item {
    display: flex; justify-content: space-between; align-items: center; gap: 12px;
    padding: 12px 0; font-size: 14px; color: var(--text-2); border-bottom: 1px dashed rgba(255,255,255,0.05);
    transition: color 0.2s;
  }
  .cert-item:hover { color: #fff; }
  .cert-item:hover .name { color: var(--teal); }
  .cert-item:last-child { border-bottom: none; }
  .cert-item .name { font-weight: 500; transition: color 0.2s; }
  .cert-item .issuer { color: var(--text-3); font-family: var(--mono); font-size: 12px; white-space: nowrap; text-align: right; background: rgba(255,255,255,0.03); padding: 4px 8px; border-radius: 4px; }

  /* ---------- TIMELINE (Achievements) ---------- */
  .timeline { position: relative; padding-left: 35px; }
  .timeline::before { content: ''; position: absolute; left: 7px; top: 8px; bottom: 8px; width: 2px; background: linear-gradient(to bottom, var(--border-soft), var(--teal), var(--border-soft)); }
  .t-item { position: relative; padding-bottom: 45px; transition: transform 0.3s ease; }
  .t-item:hover { transform: translateX(10px); }
  .t-item:last-child { padding-bottom: 0; }
  .t-item::before {
    content: ''; position: absolute; left: -34px; top: 6px; width: 14px; height: 14px; border-radius: 50%;
    background: var(--bg-void); border: 2px solid var(--teal); box-shadow: 0 0 8px var(--teal-glow);
    transition: background 0.3s;
  }
  .t-item:hover::before { background: var(--teal); }
  .t-item .t-date { font-family: var(--mono); font-size: 12.5px; color: var(--amber); letter-spacing: .08em; display: inline-block; margin-bottom: 6px; background: rgba(245, 166, 35, 0.05); padding: 4px 10px; border-radius: 4px;}
  .t-item h4 { font-size: 18px; color: #fff; margin: 4px 0 8px; }
  .t-item p { color: var(--text-2); font-size: 15px; line-height: 1.6; }

  /* ---------- CONTACT / FOOTER ---------- */
  .contact-panel {
    background: linear-gradient(135deg, var(--bg-panel), rgba(16, 22, 31, 0.2)); 
    border: 1px solid var(--teal); border-radius: 16px;
    padding: 80px 5vw; text-align: center;
    position: relative; overflow: hidden;
    box-shadow: 0 0 30px rgba(69, 224, 196, 0.05);
  }
  .contact-panel::before {
    content: ''; position: absolute; top: -50%; left: -50%; width: 200%; height: 200%;
    background: radial-gradient(circle at center, rgba(69, 224, 196, 0.1) 0%, transparent 60%);
    pointer-events: none; animation: rotate 20s linear infinite;
  }
  @keyframes rotate { 100% { transform: rotate(360deg); } }
  .contact-panel h2 { font-family: var(--mono); font-size: clamp(26px, 4vw, 36px); margin-bottom: 20px; color: #fff; }
  .contact-panel p { color: var(--text-2); font-size: 17px; max-width: 520px; margin: 0 auto 40px; }
  
  footer { padding: 40px 5vw; text-align: center; font-family: var(--mono); font-size: 12.5px; color: var(--text-3); border-top: 1px solid var(--border-soft); background: rgba(0,0,0,0.5); }
  footer span { color: var(--teal); }

  @media(max-width:768px) {
    .about-grid { grid-template-columns: 1fr; gap: 40px; }
    section { padding: 80px 6vw; }
    .profile-reveal { flex-direction: column; text-align: center; gap: 30px; }
    .cta-row { justify-content: center; }
    .photo-frame { width: 160px; height: 160px; }
    #cursor { display: none; } /* Disable custom cursor on mobile */
    * { cursor: auto; }
  }
</style>
</head>
<body>

<!-- Interactive Background -->
<canvas id="network-canvas"></canvas>

<!-- Custom Cursor -->
<div id="cursor"></div>

<div class="wrap">
  <nav>
    <div class="nav-id"><span class="dot"></span> Sai~Prasad</div>
    <div class="nav-links">
      <a href="#about" class="hover-target">about</a>
      <a href="#skills" class="hover-target">skills</a>
      <a href="#experience" class="hover-target">experience</a>
      <a href="#certifications" class="hover-target">certs</a>
      <a href="#achievements" class="hover-target">events</a>
      <a href="#contact" class="hover-target">contact</a>
    </div>
  </nav>

  <header class="hero">
    <div class="terminal" id="terminal"></div>
    <div class="profile-reveal" id="profileReveal">
      <div class="photo-frame hover-target tilt-card">
        <div class="photo-inner">
          <img src="profile.jpg" alt="Prasad Sudhir Thorat">
        </div>
      </div>
      <div class="id-block">
        <h1 class="glitch" data-text="Prasad Sudhir Thorat">Prasad Sudhir Thorat</h1>
        <div class="role">> B.Tech (Integrated) CSE | Cybersecurity | AI/Cloud</div>
        <div class="meta">Sanjivani University, Kopargaon — 2nd Year</div>
        <p class="tagline">Building a foundation across cybersecurity, cloud infrastructure, and applied AI — one certification, workshop, and hands-on project at a time. Breaking systems to understand how to secure them.</p>
        <div class="cta-row">
          <a href="Prasad_Thorat_Resume.pdf" download class="btn btn-primary hover-target">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4M7 10l5 5 5-5M12 15V3"/></svg>
            Decrypt Resume
          </a>
          <div class="icon-row">
            <a class="icon-btn hover-target" href="https://www.linkedin.com/in/prasad-thorat-a38578372" target="_blank" rel="noopener" title="LinkedIn">
              <svg viewBox="0 0 24 24" fill="currentColor"><path d="M20.45 20.45h-3.55v-5.57c0-1.33-.02-3.03-1.85-3.03-1.85 0-2.14 1.45-2.14 2.94v5.66H9.36V9h3.41v1.56h.05c.47-.9 1.63-1.85 3.36-1.85 3.6 0 4.27 2.37 4.27 5.45v6.29zM5.34 7.43a2.06 2.06 0 1 1 0-4.12 2.06 2.06 0 0 1 0 4.12zM7.12 20.45H3.56V9h3.56v11.45z"/></svg>
            </a>
            <a class="icon-btn hover-target" href="https://github.com/prasadthorat25uid-arch" target="_blank" rel="noopener" title="GitHub">
              <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C6.48 2 2 6.58 2 12.21c0 4.51 2.87 8.33 6.84 9.68.5.1.68-.22.68-.49 0-.24-.01-.87-.01-1.71-2.78.62-3.37-1.37-3.37-1.37-.45-1.18-1.11-1.49-1.11-1.49-.9-.63.07-.62.07-.62 1 .07 1.53 1.05 1.53 1.05.89 1.56 2.34 1.11 2.91.85.09-.66.35-1.11.63-1.37-2.22-.26-4.56-1.14-4.56-5.06 0-1.12.39-2.03 1.03-2.75-.1-.26-.45-1.31.1-2.73 0 0 .84-.28 2.75 1.05a9.34 9.34 0 0 1 5 0c1.91-1.33 2.75-1.05 2.75-1.05.55 1.42.2 2.47.1 2.73.64.72 1.03 1.63 1.03 2.75 0 3.93-2.34 4.79-4.57 5.05.36.32.68.94.68 1.9 0 1.37-.01 2.48-.01 2.82 0 .27.18.6.69.49A10.02 10.02 0 0 0 22 12.21C22 6.58 17.52 2 12 2z"/></svg>
            </a>
            <a class="icon-btn hover-target" href="https://wa.me/918010989708" target="_blank" rel="noopener" title="WhatsApp">
              <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12.04 2C6.58 2 2.13 6.45 2.13 11.91c0 1.87.5 3.62 1.44 5.13L2 22l5.13-1.53a9.85 9.85 0 0 0 4.91 1.31h.01c5.46 0 9.91-4.45 9.91-9.91 0-2.65-1.03-5.14-2.9-7.01A9.83 9.83 0 0 0 12.04 2zm5.8 14.1c-.24.68-1.4 1.33-1.93 1.4-.5.07-1.09.1-1.76-.11a10.9 10.9 0 0 1-1.7-.63c-3-1.29-4.95-4.3-5.1-4.5-.15-.2-1.22-1.62-1.22-3.1s.78-2.19 1.06-2.49c.28-.3.6-.37.8-.37h.58c.19 0 .43-.07.68.51.24.58.83 2.01.9 2.16.07.15.12.32.02.52-.09.2-.14.32-.28.5-.14.18-.29.4-.42.53-.14.14-.28.29-.12.57.16.28.72 1.19 1.55 1.93 1.06.95 1.96 1.24 2.24 1.38.28.14.44.12.6-.07.16-.19.68-.79.87-1.06.18-.27.36-.22.6-.13.24.09 1.5.71 1.76.84.26.13.43.2.5.31.06.11.06.65-.17 1.32z"/></svg>
            </a>
          </div>
        </div>
      </div>
    </div>
  </header>

  <section id="about" class="scroll-fade">
    <div class="section-inner about-grid">
      <div>
        <div class="eyebrow"> --About Me</div>
        <h2 class="sec-title"> System Overview </h2>
        <p>I'm <strong>Prasad Sudhir Thorat</strong>, a second-year Integrated B.Tech Computer Science & Engineering student at <strong>Sanjivani University, Kopargaon</strong>. My focus sits at the intersection of <strong>cybersecurity, cloud infrastructure, and applied AI</strong> — I believe in understanding systems thoroughly to know precisely where they break.</p>
        <p>Over the past year, I completed a hands-on <strong>cybersecurity internship</strong>, worked through cloud architecture labs on AWS ECS, and stacked up certifications across programming, digital forensics, and generative AI tooling. I actively share my technical learnings — recently covering computer networking, IP addressing, and subnetting on LinkedIn.</p>
        <p>Beyond the technical track, I stay curious about how AI tools redefine productivity and problem-solving, and I actively participate in campus life — from pitching hackathon ideas to competing in national quizzes.</p>
      </div>
      <div class="fact-panel tilt-card hover-target">
        <div class="fact-row"><span>institution</span><span>Sanjivani University</span></div>
        <div class="fact-row"><span>program</span><span>B.Tech (Integrated) CSE</span></div>
        <div class="fact-row"><span>status</span><span>2nd Year, In Progress</span></div>
        <div class="fact-row"><span>location</span><span>Kopargaon, Maharashtra</span></div>
        <div class="fact-row"><span>focus</span><span>Cybersecurity · Cloud · AI</span></div>
        <div class="fact-row"><span>internship</span><span>InternsPort Innovation</span></div>
      </div>
    </div>
  </section>

  <section id="skills" class="scroll-fade">
    <div class="section-inner">
      <div class="eyebrow">cat stack.json</div>
      <h2 class="sec-title">Technical Arsenal</h2>
      <div class="skills-grid">
        <div class="skill-card tilt-card hover-target">
          <div class="cat">Languages</div>
          <div class="skill-tags">
            <span class="skill-tag">C</span><span class="skill-tag">Python</span><span class="skill-tag">HTML</span>
          </div>
        </div>
        <div class="skill-card tilt-card hover-target">
          <div class="cat">Cybersecurity</div>
          <div class="skill-tags">
            <span class="skill-tag">Digital Forensics</span><span class="skill-tag">IP Addressing</span><span class="skill-tag">Subnetting</span><span class="skill-tag">Security Fundamentals</span>
          </div>
        </div>
        <div class="skill-card tilt-card hover-target">
          <div class="cat">Cloud & DevOps</div>
          <div class="skill-tags">
            <span class="skill-tag">AWS ECS</span><span class="skill-tag">KodeKloud Labs</span>
          </div>
        </div>
        <div class="skill-card tilt-card hover-target">
          <div class="cat">AI & GenAI</div>
          <div class="skill-tags">
            <span class="skill-tag">Claude AI</span><span class="skill-tag">Google Workspace AI</span><span class="skill-tag">GenAI Studio</span><span class="skill-tag">ChatGPT</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section id="experience" class="scroll-fade">
    <div class="section-inner">
      <div class="eyebrow">tail -f runtime.log</div>
      <h2 class="sec-title">Experience</h2>
      <div class="exp-card tilt-card hover-target">
        <div class="exp-head">
          <div>
            <h3>Cybersecurity Intern</h3>
            <div class="company">InternsPort Innovation Pvt. Ltd.</div>
          </div>
          <div class="date">FEB 2026 — APR 2026</div>
        </div>
        <ul>
          <li>Completed a rigorous 2-month internship immersed in the domain of cybersecurity.</li>
          <li>Demonstrated strong analytical thinking, problem-solving ability, and effective communication while tackling security scenarios.</li>
          <li>Earned a Letter of Recommendation from the Head of Operations for outstanding performance.</li>
        </ul>
      </div>
    </div>
  </section>

  <section id="certifications" class="scroll-fade">
    <div class="section-inner">
      <div class="eyebrow">ls -la credentials.vault</div>
      <h2 class="sec-title">Certifications</h2>
      <div class="cert-groups">

        <div class="cert-group tilt-card hover-target">
          <div class="cert-group-head">
            <div class="icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 10h-1.26A8 8 0 1 0 9 20h9a5 5 0 0 0 0-10z"/></svg>
            </div>
            <h3>CLOUD & INFRASTRUCTURE</h3>
          </div>
          <ul class="cert-list">
            <li class="cert-item"><span class="name">AWS Elastic Container Service (ECS)</span><span class="issuer">KodeKloud</span></li>
            <li class="cert-item"><span class="name">KodeKloud Challenges Completion</span><span class="issuer">KodeKloud</span></li>
          </ul>
        </div>

        <div class="cert-group tilt-card hover-target">
          <div class="cert-group-head">
            <div class="icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M16 18l6-6-6-6M8 6l-6 6 6 6"/></svg>
            </div>
            <h3>PROGRAMMING</h3>
          </div>
          <ul class="cert-list">
            <li class="cert-item"><span class="name">Introduction to Python</span><span class="issuer">Infosys</span></li>
            <li class="cert-item"><span class="name">Python Fundamentals</span><span class="issuer">Infosys</span></li>
            <li class="cert-item"><span class="name">Master the C Language</span><span class="issuer">Learn Academy</span></li>
            <li class="cert-item"><span class="name">Introduction to C</span><span class="issuer">Sololearn</span></li>
          </ul>
        </div>

        <div class="cert-group tilt-card hover-target">
          <div class="cert-group-head">
            <div class="icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M12 1v6M12 17v6M4.2 4.2l4.2 4.2M15.6 15.6l4.2 4.2M1 12h6M17 12h6M4.2 19.8l4.2-4.2M15.6 8.4l4.2-4.2"/></svg>
            </div>
            <h3>AI & GENERATIVE AI</h3>
          </div>
          <ul class="cert-list">
            <li class="cert-item"><span class="name">AI Fluency & Claude 101</span><span class="issuer">Anthropic</span></li>
            <li class="cert-item"><span class="name">Bring AI to Work Workshop</span><span class="issuer">Google</span></li>
            <li class="cert-item"><span class="name">Generative AI Studio</span><span class="issuer">Simplilearn</span></li>
            <li class="cert-item"><span class="name">Generative AI Mastery</span><span class="issuer">OpenAI Acad.</span></li>
            <li class="cert-item"><span class="name">Microsoft Excel Using AI</span><span class="issuer">OfficeMaster</span></li>
          </ul>
        </div>

        <div class="cert-group tilt-card hover-target">
          <div class="cert-group-head">
            <div class="icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
            </div>
            <h3>CYBERSECURITY & MORE</h3>
          </div>
          <ul class="cert-list">
            <li class="cert-item"><span class="name">Cybersecurity Mastery</span><span class="issuer">Unstop</span></li>
            <li class="cert-item"><span class="name">Digital Forensics Workshop</span><span class="issuer">Indian Cyber</span></li>
            <li class="cert-item"><span class="name">SEBI Investor Awareness Test</span><span class="issuer">NISM</span></li>
            <li class="cert-item"><span class="name">Communication Skills</span><span class="issuer">MindLuster</span></li>
          </ul>
        </div>

      </div>
    </div>
  </section>

  <section id="achievements" class="scroll-fade">
    <div class="section-inner">
      <div class="eyebrow">history -10</div>
      <h2 class="sec-title">Events & Competitions</h2>
      <div class="timeline">
        <div class="t-item">
          <div class="t-date">DEC 2025</div>
          <h4>Artificial Intelligence Workshop</h4>
          <p>Participated at Techfest, IIT Bombay, gaining hands-on exposure to advanced AI concepts.</p>
        </div>
        <div class="t-item">
          <div class="t-date">NOV 2025</div>
          <h4>GenAI Buildathon & Constitution Quiz</h4>
          <p>Competed in the NxtWave / OpenAI Academy Buildathon. Scored 90% in the Sanjivani University Constitution Day Quiz.</p>
        </div>
        <div class="t-item">
          <div class="t-date">SEP 2025</div>
          <h4>Smart India Hackathon (Internal)</h4>
          <p>Represented Team "Code Warriors" during the idea presentation round at Sanjivani University.</p>
        </div>
        <div class="t-item">
          <div class="t-date">2025 — 2026</div>
          <h4>National Level Quizzes</h4>
          <p>Participated in MYBharat Online Quizzes (Viksit Rajasthan @2047, VBYLD 2026) and the Dr. B.R. Ambedkar Quiz 2025 (Ministry of Social Justice).</p>
        </div>
      </div>
    </div>
  </section>

  <section id="contact" class="scroll-fade">
    <div class="section-inner contact-panel tilt-card hover-target">
      <div class="eyebrow" style="justify-content:center;">ping -c 4 prasad</div>
      <h2>Let's build something secure.</h2>
      <p>Always open to discussing internships, collaborations, or deep dives into cybersecurity, cloud architecture, and AI.</p>
      <div class="cta-row" style="justify-content:center;">
        <a href="Prasad_Thorat_Resume.pdf" download class="btn btn-primary hover-target">↓ Download Resume</a>
        <div class="icon-row">
          <a class="icon-btn hover-target" href="https://www.linkedin.com/in/prasad-thorat-a38578372" target="_blank" rel="noopener" title="LinkedIn">
            <svg viewBox="0 0 24 24" fill="currentColor"><path d="M20.45 20.45h-3.55v-5.57c0-1.33-.02-3.03-1.85-3.03-1.85 0-2.14 1.45-2.14 2.94v5.66H9.36V9h3.41v1.56h.05c.47-.9 1.63-1.85 3.36-1.85 3.6 0 4.27 2.37 4.27 5.45v6.29zM5.34 7.43a2.06 2.06 0 1 1 0-4.12 2.06 2.06 0 0 1 0 4.12zM7.12 20.45H3.56V9h3.56v11.45z"/></svg>
          </a>
          <a class="icon-btn hover-target" href="https://github.com/prasadthorat25uid-arch" target="_blank" rel="noopener" title="GitHub">
            <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2C6.48 2 2 6.58 2 12.21c0 4.51 2.87 8.33 6.84 9.68.5.1.68-.22.68-.49 0-.24-.01-.87-.01-1.71-2.78.62-3.37-1.37-3.37-1.37-.45-1.18-1.11-1.49-1.11-1.49-.9-.63.07-.62.07-.62 1 .07 1.53 1.05 1.53 1.05.89 1.56 2.34 1.11 2.91.85.09-.66.35-1.11.63-1.37-2.22-.26-4.56-1.14-4.56-5.06 0-1.12.39-2.03 1.03-2.75-.1-.26-.45-1.31.1-2.73 0 0 .84-.28 2.75 1.05a9.34 9.34 0 0 1 5 0c1.91-1.33 2.75-1.05 2.75-1.05.55 1.42.2 2.47.1 2.73.64.72 1.03 1.63 1.03 2.75 0 3.93-2.34 4.79-4.57 5.05.36.32.68.94.68 1.9 0 1.37-.01 2.48-.01 2.82 0 .27.18.6.69.49A10.02 10.02 0 0 0 22 12.21C22 6.58 17.52 2 12 2z"/></svg>
          </a>
          <a class="icon-btn hover-target" href="https://wa.me/918010989708" target="_blank" rel="noopener" title="WhatsApp">
            <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12.04 2C6.58 2 2.13 6.45 2.13 11.91c0 1.87.5 3.62 1.44 5.13L2 22l5.13-1.53a9.85 9.85 0 0 0 4.91 1.31h.01c5.46 0 9.91-4.45 9.91-9.91 0-2.65-1.03-5.14-2.9-7.01A9.83 9.83 0 0 0 12.04 2zm5.8 14.1c-.24.68-1.4 1.33-1.93 1.4-.5.07-1.09.1-1.76-.11a10.9 10.9 0 0 1-1.7-.63c-3-1.29-4.95-4.3-5.1-4.5-.15-.2-1.22-1.62-1.22-3.1s.78-2.19 1.06-2.49c.28-.3.6-.37.8-.37h.58c.19 0 .43-.07.68.51.24.58.83 2.01.9 2.16.07.15.12.32.02.52-.09.2-.14.32-.28.5-.14.18-.29.4-.42.53-.14.14-.28.29-.12.57.16.28.72 1.19 1.55 1.93 1.06.95 1.96 1.24 2.24 1.38.28.14.44.12.6-.07.16-.19.68-.79.87-1.06.18-.27.36-.22.6-.13.24.09 1.5.71 1.76.84.26.13.43.2.5.31.06.11.06.65-.17 1.32z"/></svg>
          </a>
        </div>
      </div>
    </div>
  </section>

  <footer>
    © 2026 PRASAD_THORAT <span style="margin:0 10px;">|</span> SESSION_TERMINATED_SAFELY <span style="margin:0 10px;">|</span> SECURE_CONNECTION
  </footer>

</div>

<script>
  /* --- Custom Cursor --- */
  const cursor = document.getElementById('cursor');
  const hoverTargets = document.querySelectorAll('.hover-target, a, button');

  document.addEventListener('mousemove', e => {
    cursor.style.left = e.clientX + 'px';
    cursor.style.top = e.clientY + 'px';
  });

  hoverTargets.forEach(target => {
    target.addEventListener('mouseenter', () => cursor.classList.add('hovering'));
    target.addEventListener('mouseleave', () => cursor.classList.remove('hovering'));
  });

  /* --- Terminal Boot Sequence --- */
  const generateHash = () => Math.random().toString(36).substring(2, 8).toUpperCase();
  const lines = [
    {text:`> initializing secure_profile.sys [0x${generateHash()}]`, cls:'prompt'},
    {text:'> scanning credentials ... bypassing firewall ... [OK]', cls:'ok'},
    {text:'> decrypting identity module: PRASAD_SUDHIR_THORAT', cls:'ok'},
    {text:'> institution node: SANJIVANI_UNIVERSITY, KOPARGAON', cls:'prompt'},
    {text:'> loading core_skills: [CYBERSECURITY, CLOUD, AI]', cls:'prompt'},
    {text:'> clearance level: STUDENT_DEVELOPER', cls:'ok'},
    {text:'> ACCESS GRANTED. Welcome, Prasad.', cls:'granted'}
  ];
  const term = document.getElementById('terminal');
  const reveal = document.getElementById('profileReveal');

  function scrambleText(originalText, callback) {
    const chars = '!<>-_\\/[]{}—=+*^?#_';
    let iterations = 0;
    const maxIterations = 10;
    
    const interval = setInterval(() => {
      let scrambled = originalText.split('').map((char, index) => {
        if (index < iterations) return originalText[index];
        return chars[Math.floor(Math.random() * chars.length)];
      }).join('');
      
      callback(scrambled);
      
      if (iterations >= originalText.length) {
        clearInterval(interval);
      }
      iterations += 1/2; // Speed of unscrambling
    }, 20);
  }

  function typeLine(idx){
    if(idx >= lines.length){
      setTimeout(()=> reveal.classList.add('show'), 400);
      return;
    }
    const {text, cls} = lines[idx];
    const div = document.createElement('div');
    div.className = 'line ' + cls;
    term.appendChild(div);
    div.style.opacity = 1;

    // Use scramble effect for the granted line
    if(cls === 'granted') {
      scrambleText(text, (scrambled) => {
        div.innerHTML = scrambled + '<span class="cursor"></span>';
      });
      setTimeout(() => typeLine(idx+1), text.length * 30 + 500);
      return;
    }

    let i = 0;
    const speed = 15;
    function type(){
      if(i <= text.length){
        div.textContent = text.slice(0,i);
        if(i < text.length){
          div.innerHTML = text.slice(0,i) + '<span class="cursor"></span>';
        }
        i++;
        setTimeout(type, speed);
      } else {
        div.textContent = text;
        setTimeout(()=> typeLine(idx+1), 150);
      }
    }
    type();
  }
  
  // Start terminal animation slightly after load
  setTimeout(() => typeLine(0), 300);

  /* --- Scroll Reveal --- */
  const observer = new IntersectionObserver((entries)=>{
    entries.forEach(e=>{
      if(e.isIntersecting){
        e.target.style.opacity = 1;
        e.target.style.transform = 'translateY(0)';
      }
    });
  },{threshold:0.15});
  document.querySelectorAll('.scroll-fade').forEach(s=>{
    s.style.opacity = 0;
    s.style.transform = 'translateY(40px)';
    s.style.transition = 'opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1)';
    observer.observe(s);
  });

  /* --- 3D Tilt Effect --- */
  const tiltCards = document.querySelectorAll('.tilt-card');
  tiltCards.forEach(card => {
    card.addEventListener('mousemove', e => {
      const rect = card.getBoundingClientRect();
      const x = e.clientX - rect.left;
      const y = e.clientY - rect.top;
      
      const centerX = rect.width / 2;
      const centerY = rect.height / 2;
      
      const tiltX = ((y - centerY) / centerY) * -10; // Max tilt 10deg
      const tiltY = ((x - centerX) / centerX) * 10;
      
      card.style.transform = `perspective(1000px) rotateX(${tiltX}deg) rotateY(${tiltY}deg) scale3d(1.02, 1.02, 1.02)`;
    });
    
    card.addEventListener('mouseleave', () => {
      card.style.transform = `perspective(1000px) rotateX(0deg) rotateY(0deg) scale3d(1, 1, 1)`;
    });
  });

  /* --- Canvas Network Background --- */
  const canvas = document.getElementById('network-canvas');
  const ctx = canvas.getContext('2d');
  let width, height;
  let particles = [];
  let mouse = { x: null, y: null, radius: 150 };

  function resize() {
    width = canvas.width = window.innerWidth;
    height = canvas.height = window.innerHeight;
  }
  window.addEventListener('resize', resize);
  resize();

  window.addEventListener('mousemove', (e) => {
    mouse.x = e.x;
    mouse.y = e.y;
  });
  window.addEventListener('mouseout', () => {
    mouse.x = null;
    mouse.y = null;
  });

  class Particle {
    constructor() {
      this.x = Math.random() * width;
      this.y = Math.random() * height;
      this.size = Math.random() * 2 + 1;
      this.speedX = Math.random() * 1 - 0.5;
      this.speedY = Math.random() * 1 - 0.5;
      this.color = Math.random() > 0.5 ? '#45E0C4' : '#182230';
    }
    update() {
      this.x += this.speedX;
      this.y += this.speedY;

      if (this.x > width || this.x < 0) this.speedX = -this.speedX;
      if (this.y > height || this.y < 0) this.speedY = -this.speedY;

      // Mouse interaction
      if(mouse.x != null) {
        let dx = mouse.x - this.x;
        let dy = mouse.y - this.y;
        let distance = Math.sqrt(dx * dx + dy * dy);
        if (distance < mouse.radius) {
          const forceDirectionX = dx / distance;
          const forceDirectionY = dy / distance;
          const force = (mouse.radius - distance) / mouse.radius;
          this.x -= forceDirectionX * force * 2;
          this.y -= forceDirectionY * force * 2;
        }
      }
    }
    draw() {
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
      ctx.fillStyle = this.color;
      ctx.fill();
    }
  }

  function initParticles() {
    particles = [];
    let numberOfParticles = (width * height) / 9000;
    for (let i = 0; i < numberOfParticles; i++) {
      particles.push(new Particle());
    }
  }

  function animateParticles() {
    ctx.clearRect(0, 0, width, height);
    for (let i = 0; i < particles.length; i++) {
      particles[i].update();
      particles[i].draw();
      
      for (let j = i; j < particles.length; j++) {
        let dx = particles[i].x - particles[j].x;
        let dy = particles[i].y - particles[j].y;
        let distance = dx * dx + dy * dy;
        if (distance < 10000) {
          ctx.beginPath();
          ctx.strokeStyle = `rgba(69, 224, 196, ${1 - distance/10000})`;
          ctx.lineWidth = 0.5;
          ctx.moveTo(particles[i].x, particles[i].y);
          ctx.lineTo(particles[j].x, particles[j].y);
          ctx.stroke();
        }
      }
    }
    requestAnimationFrame(animateParticles);
  }

  initParticles();
  animateParticles();

</script>

</body>
</html>
