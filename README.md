<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>VlokProduction — Web & SaaS Solutions</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --ink: #0a0a0f;
      --paper: #f5f2eb;
      --accent: #ff3c2f;
      --accent2: #1a1aff;
      --mid: #c8c4b8;
      --soft: #e8e4dc;
    }
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      background: var(--ink);
      color: var(--paper);
      font-family: 'DM Sans', sans-serif;
      font-size: 16px;
      line-height: 1.6;
      overflow-x: hidden;
      cursor: none;
    }

    /* Custom cursor */
    #cursor {
      position: fixed; top: 0; left: 0;
      width: 14px; height: 14px;
      background: var(--accent);
      border-radius: 50%;
      pointer-events: none;
      z-index: 9999;
      transform: translate(-50%, -50%);
      transition: transform 0.1s, width 0.2s, height 0.2s, background 0.2s;
      mix-blend-mode: difference;
    }
    #cursor.expand {
      width: 48px; height: 48px;
      background: var(--paper);
    }

    /* Noise overlay */
    body::before {
      content: '';
      position: fixed; inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 9000;
      opacity: 0.5;
    }

    /* NAV */
    nav {
      position: fixed; top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex; align-items: center; justify-content: space-between;
      padding: 1.4rem 3rem;
      mix-blend-mode: difference;
    }
    .nav-logo {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.6rem;
      letter-spacing: 0.08em;
      color: var(--paper);
      text-decoration: none;
    }
    .nav-links { display: flex; gap: 2.5rem; list-style: none; }
    .nav-links a {
      font-family: 'Space Mono', monospace;
      font-size: 0.72rem;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      color: var(--paper);
      text-decoration: none;
      opacity: 0.7;
      transition: opacity 0.2s;
    }
    .nav-links a:hover { opacity: 1; }

    /* HERO */
    #hero {
      min-height: 100vh;
      display: grid;
      grid-template-columns: 1fr 1fr;
      align-items: end;
      padding: 8rem 3rem 5rem;
      position: relative;
      border-bottom: 1px solid rgba(245,242,235,0.12);
    }
    .hero-left { align-self: end; }
    .hero-tag {
      font-family: 'Space Mono', monospace;
      font-size: 0.7rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 1.4rem;
      opacity: 0;
      animation: fadeUp 0.8s 0.2s forwards;
    }
    .hero-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(5rem, 10vw, 10rem);
      line-height: 0.92;
      letter-spacing: -0.01em;
      opacity: 0;
      animation: fadeUp 0.9s 0.4s forwards;
    }
    .hero-title span { color: var(--accent); }
    .hero-sub {
      margin-top: 2rem;
      font-size: 1.05rem;
      font-weight: 300;
      color: var(--mid);
      max-width: 480px;
      opacity: 0;
      animation: fadeUp 0.9s 0.6s forwards;
    }
    .hero-cta {
      margin-top: 3rem;
      display: flex; gap: 1rem; flex-wrap: wrap;
      opacity: 0;
      animation: fadeUp 0.9s 0.8s forwards;
    }
    .btn {
      display: inline-block;
      padding: 0.9rem 2.2rem;
      font-family: 'Space Mono', monospace;
      font-size: 0.78rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      text-decoration: none;
      transition: all 0.25s;
      cursor: none;
    }
    .btn-primary {
      background: var(--accent);
      color: var(--paper);
      border: 2px solid var(--accent);
    }
    .btn-primary:hover { background: transparent; color: var(--accent); }
    .btn-ghost {
      background: transparent;
      color: var(--paper);
      border: 2px solid rgba(245,242,235,0.3);
    }
    .btn-ghost:hover { border-color: var(--paper); }

    .hero-right {
      align-self: stretch;
      display: flex; flex-direction: column; justify-content: flex-end;
      padding-bottom: 0.5rem;
      opacity: 0;
      animation: fadeIn 1.2s 0.6s forwards;
    }
    .hero-stats {
      display: grid; grid-template-columns: 1fr 1fr;
      gap: 1.5rem 2rem;
      margin-bottom: 2rem;
    }
    .stat-num {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 3.5rem;
      line-height: 1;
      color: var(--paper);
    }
    .stat-num sup { font-size: 1.4rem; color: var(--accent); }
    .stat-label {
      font-family: 'Space Mono', monospace;
      font-size: 0.68rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--mid);
      margin-top: 0.2rem;
    }
    .hero-marquee-wrap {
      overflow: hidden;
      border-top: 1px solid rgba(245,242,235,0.12);
      padding-top: 1.2rem;
    }
    .hero-marquee {
      display: flex; gap: 3rem;
      animation: marquee 18s linear infinite;
      white-space: nowrap;
    }
    .marquee-item {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.1rem;
      letter-spacing: 0.15em;
      color: var(--mid);
      flex-shrink: 0;
    }
    .marquee-dot { color: var(--accent); margin-right: 3rem; }

    /* SERVICES */
    #services {
      padding: 7rem 3rem;
      border-bottom: 1px solid rgba(245,242,235,0.12);
    }
    .section-header {
      display: flex; align-items: baseline; gap: 1.5rem;
      margin-bottom: 4rem;
    }
    .section-num {
      font-family: 'Space Mono', monospace;
      font-size: 0.7rem;
      color: var(--accent);
      letter-spacing: 0.15em;
    }
    .section-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(2.5rem, 5vw, 4rem);
      line-height: 1;
      letter-spacing: 0.02em;
    }
    .services-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 0;
      border: 1px solid rgba(245,242,235,0.12);
    }
    .service-card {
      padding: 2.5rem;
      border-right: 1px solid rgba(245,242,235,0.12);
      position: relative;
      overflow: hidden;
      transition: background 0.3s;
    }
    .service-card:last-child { border-right: none; }
    .service-card::after {
      content: '';
      position: absolute; bottom: 0; left: 0;
      width: 100%; height: 3px;
      background: var(--accent);
      transform: scaleX(0);
      transform-origin: left;
      transition: transform 0.35s cubic-bezier(0.77,0,0.175,1);
    }
    .service-card:hover { background: rgba(245,242,235,0.04); }
    .service-card:hover::after { transform: scaleX(1); }
    .service-icon {
      width: 48px; height: 48px;
      margin-bottom: 1.8rem;
      opacity: 0.9;
    }
    .service-name {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.7rem;
      letter-spacing: 0.04em;
      margin-bottom: 0.8rem;
    }
    .service-desc {
      font-size: 0.9rem;
      color: var(--mid);
      line-height: 1.7;
      font-weight: 300;
    }
    .service-tags {
      margin-top: 1.5rem;
      display: flex; flex-wrap: wrap; gap: 0.5rem;
    }
    .tag {
      font-family: 'Space Mono', monospace;
      font-size: 0.62rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      padding: 0.3rem 0.7rem;
      border: 1px solid rgba(245,242,235,0.2);
      color: var(--mid);
    }

    /* WORK */
    #work {
      padding: 7rem 3rem;
      border-bottom: 1px solid rgba(245,242,235,0.12);
    }
    .work-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 2px;
      background: rgba(245,242,235,0.08);
    }
    .work-item {
      background: var(--ink);
      padding: 3rem;
      position: relative;
      overflow: hidden;
      min-height: 280px;
      display: flex; flex-direction: column; justify-content: flex-end;
    }
    .work-item:first-child { grid-column: span 2; min-height: 380px; }
    .work-item-bg {
      position: absolute; inset: 0;
      background: linear-gradient(135deg, var(--c1), var(--c2));
      opacity: 0.15;
      transition: opacity 0.4s;
    }
    .work-item:hover .work-item-bg { opacity: 0.28; }
    .work-item-num {
      font-family: 'Space Mono', monospace;
      font-size: 0.65rem;
      letter-spacing: 0.2em;
      color: var(--accent);
      margin-bottom: 1rem;
      position: relative;
    }
    .work-item-name {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(2rem, 4vw, 3.2rem);
      line-height: 1;
      letter-spacing: 0.02em;
      position: relative;
    }
    .work-item-type {
      margin-top: 0.6rem;
      font-size: 0.85rem;
      font-weight: 300;
      color: var(--mid);
      position: relative;
    }
    .work-link {
      margin-top: 1.5rem;
      font-family: 'Space Mono', monospace;
      font-size: 0.7rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--paper);
      text-decoration: none;
      display: inline-flex; align-items: center; gap: 0.6rem;
      position: relative;
      opacity: 0;
      transition: opacity 0.3s;
    }
    .work-item:hover .work-link { opacity: 1; }
    .work-link::after {
      content: '→';
      transition: transform 0.2s;
    }
    .work-link:hover::after { transform: translateX(4px); }

    /* PRICING */
    #pricing {
      padding: 7rem 3rem;
      border-bottom: 1px solid rgba(245,242,235,0.12);
    }
    .pricing-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 2px;
      background: rgba(245,242,235,0.08);
      margin-top: 4rem;
    }
    .pricing-card {
      background: var(--ink);
      padding: 3rem 2.5rem;
      position: relative;
      transition: background 0.3s;
    }
    .pricing-card.featured {
      background: var(--accent);
    }
    .pricing-card.featured .price-currency,
    .pricing-card.featured .price-amount,
    .pricing-card.featured .price-period,
    .pricing-card.featured .pricing-name,
    .pricing-card.featured .pricing-desc,
    .pricing-card.featured .pricing-feature {
      color: var(--paper) !important;
    }
    .pricing-card.featured .pricing-feature { border-color: rgba(245,242,235,0.25) !important; }
    .pricing-badge {
      font-family: 'Space Mono', monospace;
      font-size: 0.6rem;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      background: var(--ink);
      color: var(--accent);
      padding: 0.25rem 0.8rem;
      display: inline-block;
      margin-bottom: 1.5rem;
    }
    .pricing-name {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.8rem;
      letter-spacing: 0.05em;
      margin-bottom: 0.5rem;
    }
    .pricing-desc {
      font-size: 0.85rem;
      color: var(--mid);
      font-weight: 300;
      margin-bottom: 2rem;
    }
    .price-row {
      display: flex; align-items: baseline; gap: 0.3rem;
      margin-bottom: 2rem;
      border-top: 1px solid rgba(245,242,235,0.12);
      padding-top: 1.5rem;
    }
    .pricing-card.featured .price-row { border-color: rgba(245,242,235,0.3); }
    .price-currency {
      font-family: 'Space Mono', monospace;
      font-size: 1rem;
      color: var(--mid);
      align-self: flex-start;
      margin-top: 0.4rem;
    }
    .price-amount {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 4rem;
      line-height: 1;
      color: var(--paper);
    }
    .price-period {
      font-family: 'Space Mono', monospace;
      font-size: 0.7rem;
      color: var(--mid);
      letter-spacing: 0.1em;
    }
    .pricing-features { list-style: none; }
    .pricing-feature {
      font-size: 0.88rem;
      color: var(--mid);
      padding: 0.65rem 0;
      border-bottom: 1px solid rgba(245,242,235,0.08);
      display: flex; align-items: center; gap: 0.7rem;
      font-weight: 300;
    }
    .pricing-feature::before {
      content: '—';
      color: var(--accent);
      font-family: 'Space Mono', monospace;
      font-size: 0.7rem;
      flex-shrink: 0;
    }
    .pricing-card.featured .pricing-feature::before { color: var(--paper); }
    .pricing-cta {
      margin-top: 2.5rem;
      display: block;
      text-align: center;
      padding: 0.9rem;
      font-family: 'Space Mono', monospace;
      font-size: 0.72rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      text-decoration: none;
      border: 2px solid rgba(245,242,235,0.25);
      color: var(--paper);
      transition: all 0.25s;
      cursor: none;
    }
    .pricing-cta:hover { border-color: var(--paper); background: rgba(245,242,235,0.06); }
    .pricing-card.featured .pricing-cta {
      background: var(--ink);
      color: var(--paper);
      border-color: var(--ink);
    }
    .pricing-card.featured .pricing-cta:hover { background: rgba(0,0,0,0.8); }

    /* ABOUT */
    #about {
      padding: 7rem 3rem;
      border-bottom: 1px solid rgba(245,242,235,0.12);
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 6rem;
      align-items: center;
    }
    .about-eyebrow {
      font-family: 'Space Mono', monospace;
      font-size: 0.7rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 1.2rem;
    }
    .about-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(2.8rem, 5vw, 4.5rem);
      line-height: 1;
      letter-spacing: 0.02em;
      margin-bottom: 2rem;
    }
    .about-body {
      font-size: 1rem;
      color: var(--mid);
      line-height: 1.8;
      font-weight: 300;
      margin-bottom: 1.2rem;
    }
    .about-profile-link {
      display: inline-flex; align-items: center; gap: 0.7rem;
      font-family: 'Space Mono', monospace;
      font-size: 0.72rem;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      color: var(--paper);
      text-decoration: none;
      margin-top: 1rem;
      border-bottom: 1px solid rgba(245,242,235,0.3);
      padding-bottom: 0.2rem;
      transition: border-color 0.2s, color 0.2s;
    }
    .about-profile-link:hover { color: var(--accent); border-color: var(--accent); }
    .about-profile-link::after { content: '↗'; }
    .about-right { position: relative; }
    .about-card {
      border: 1px solid rgba(245,242,235,0.12);
      padding: 2.5rem;
      margin-bottom: 1.5rem;
    }
    .about-card-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.2rem;
      letter-spacing: 0.08em;
      margin-bottom: 1rem;
      color: var(--accent);
    }
    .skill-list {
      display: flex; flex-wrap: wrap; gap: 0.6rem;
    }
    .skill-pill {
      font-family: 'Space Mono', monospace;
      font-size: 0.65rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      padding: 0.35rem 0.8rem;
      border: 1px solid rgba(245,242,235,0.15);
      color: var(--mid);
      transition: border-color 0.2s, color 0.2s;
    }
    .skill-pill:hover { border-color: var(--accent); color: var(--paper); }

    /* CONTACT */
    #contact {
      padding: 7rem 3rem;
    }
    .contact-inner {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 6rem;
      align-items: start;
    }
    .contact-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(3rem, 7vw, 7rem);
      line-height: 0.95;
      letter-spacing: -0.01em;
    }
    .contact-title span { color: var(--accent); display: block; }
    .contact-sub {
      margin-top: 2rem;
      font-size: 1rem;
      color: var(--mid);
      font-weight: 300;
      line-height: 1.7;
    }
    .contact-links { margin-top: 3rem; }
    .contact-link-row {
      display: flex; align-items: center; justify-content: space-between;
      padding: 1.4rem 0;
      border-top: 1px solid rgba(245,242,235,0.12);
      text-decoration: none;
      color: var(--paper);
      transition: padding-left 0.2s;
      cursor: none;
    }
    .contact-link-row:last-child { border-bottom: 1px solid rgba(245,242,235,0.12); }
    .contact-link-row:hover { padding-left: 0.8rem; }
    .contact-link-row:hover .cl-arrow { transform: rotate(-45deg); }
    .cl-label {
      font-family: 'Space Mono', monospace;
      font-size: 0.7rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--mid);
    }
    .cl-value {
      font-size: 1rem;
      font-weight: 300;
    }
    .cl-arrow {
      font-size: 1.2rem;
      transition: transform 0.2s;
    }
    .contact-right { padding-top: 1rem; }
    .contact-form-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.6rem;
      letter-spacing: 0.05em;
      margin-bottom: 2rem;
      color: var(--mid);
    }
    .form-group { margin-bottom: 1.5rem; }
    .form-group label {
      display: block;
      font-family: 'Space Mono', monospace;
      font-size: 0.65rem;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--mid);
      margin-bottom: 0.5rem;
    }
    .form-group input,
    .form-group textarea,
    .form-group select {
      width: 100%;
      background: rgba(245,242,235,0.05);
      border: 1px solid rgba(245,242,235,0.15);
      color: var(--paper);
      font-family: 'DM Sans', sans-serif;
      font-size: 0.95rem;
      font-weight: 300;
      padding: 0.85rem 1.1rem;
      outline: none;
      transition: border-color 0.2s;
      appearance: none;
      -webkit-appearance: none;
      cursor: none;
    }
    .form-group select { cursor: none; }
    .form-group input:focus,
    .form-group textarea:focus,
    .form-group select:focus {
      border-color: var(--accent);
    }
    .form-group textarea { resize: vertical; min-height: 100px; }
    .form-submit {
      width: 100%;
      padding: 1rem;
      font-family: 'Space Mono', monospace;
      font-size: 0.78rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      background: var(--accent);
      color: var(--paper);
      border: 2px solid var(--accent);
      cursor: none;
      transition: all 0.25s;
    }
    .form-submit:hover { background: transparent; color: var(--accent); }

    /* FOOTER */
    footer {
      border-top: 1px solid rgba(245,242,235,0.12);
      padding: 2.5rem 3rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .footer-logo {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.3rem;
      letter-spacing: 0.08em;
      color: var(--paper);
    }
    .footer-copy {
      font-family: 'Space Mono', monospace;
      font-size: 0.65rem;
      letter-spacing: 0.1em;
      color: var(--mid);
    }
    .footer-copy span { color: var(--accent); }

    /* ANIMATIONS */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(28px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
    @keyframes marquee {
      from { transform: translateX(0); }
      to { transform: translateX(-50%); }
    }

    /* SCROLL REVEAL */
    .reveal {
      opacity: 0;
      transform: translateY(30px);
      transition: opacity 0.7s cubic-bezier(0.22,1,0.36,1), transform 0.7s cubic-bezier(0.22,1,0.36,1);
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* RESPONSIVE */
    @media (max-width: 900px) {
      nav { padding: 1.2rem 1.5rem; }
      .nav-links { display: none; }
      #hero { grid-template-columns: 1fr; padding: 7rem 1.5rem 4rem; gap: 4rem; }
      .hero-right { display: none; }
      .services-grid { grid-template-columns: 1fr; }
      .service-card { border-right: none; border-bottom: 1px solid rgba(245,242,235,0.12); }
      .work-grid { grid-template-columns: 1fr; }
      .work-item:first-child { grid-column: span 1; }
      .pricing-grid { grid-template-columns: 1fr; }
      #about { grid-template-columns: 1fr; gap: 3rem; padding: 5rem 1.5rem; }
      #services, #work, #pricing, #contact { padding: 5rem 1.5rem; }
      .contact-inner { grid-template-columns: 1fr; gap: 3rem; }
      footer { flex-direction: column; gap: 1rem; text-align: center; padding: 2rem 1.5rem; }
    }
  </style>
</head>
<body>

<div id="cursor"></div>

<!-- NAV -->
<nav>
  <a href="#" class="nav-logo">VLOK/</a>
  <ul class="nav-links">
    <li><a href="#services">Services</a></li>
    <li><a href="#work">Work</a></li>
    <li><a href="#pricing">Pricing</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-left">
    <p class="hero-tag">// Web & SaaS Development</p>
    <h1 class="hero-title">
      Build<br/>
      <span>Better</span><br/>
      Digital
    </h1>
    <p class="hero-sub">
      Freelance web solutions, SaaS platforms, and B2B digital products — crafted with precision and built to scale.
    </p>
    <div class="hero-cta">
      <a href="#contact" class="btn btn-primary">Start a project</a>
      <a href="#work" class="btn btn-ghost">View work</a>
    </div>
  </div>
  <div class="hero-right">
    <div class="hero-stats">
      <div>
        <div class="stat-num">30<sup>+</sup></div>
        <div class="stat-label">Projects shipped</div>
      </div>
      <div>
        <div class="stat-num">4<sup>+</sup></div>
        <div class="stat-label">Years building</div>
      </div>
      <div>
        <div class="stat-num">100<sup>%</sup></div>
        <div class="stat-label">Client satisfaction</div>
      </div>
      <div>
        <div class="stat-num">B2B</div>
        <div class="stat-label">SaaS specialist</div>
      </div>
    </div>
    <div class="hero-marquee-wrap">
      <div class="hero-marquee">
        <span class="marquee-item">React</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">Next.js</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">Node.js</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">SaaS</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">B2B</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">Tailwind</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">PostgreSQL</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">API Design</span><span class="marquee-dot">✦</span>
        <!-- repeated for seamless loop -->
        <span class="marquee-item">React</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">Next.js</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">Node.js</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">SaaS</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">B2B</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">Tailwind</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">PostgreSQL</span><span class="marquee-dot">✦</span>
        <span class="marquee-item">API Design</span><span class="marquee-dot">✦</span>
      </div>
    </div>
  </div>
</section>

<!-- SERVICES -->
<section id="services">
  <div class="section-header reveal">
    <span class="section-num">01</span>
    <h2 class="section-title">What I Build</h2>
  </div>
  <div class="services-grid">
    <div class="service-card reveal">
      <svg class="service-icon" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect x="4" y="8" width="40" height="28" rx="2" stroke="#ff3c2f" stroke-width="2"/>
        <path d="M4 14h40M16 36v4M32 36v4M12 40h24" stroke="#ff3c2f" stroke-width="2" stroke-linecap="round"/>
        <path d="M18 22l-4 3 4 3M30 22l4 3-4 3M23 19l2 10" stroke="rgba(245,242,235,0.6)" stroke-width="1.5" stroke-linecap="round"/>
      </svg>
      <h3 class="service-name">Web Development</h3>
      <p class="service-desc">Fast, accessible, and beautifully crafted websites. From landing pages to complex web applications — pixel-perfect across all devices.</p>
      <div class="service-tags">
        <span class="tag">React</span>
        <span class="tag">Next.js</span>
        <span class="tag">HTML/CSS</span>
        <span class="tag">WordPress</span>
      </div>
    </div>
    <div class="service-card reveal" style="transition-delay:0.12s">
      <svg class="service-icon" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M8 12h32M8 24h32M8 36h32" stroke="rgba(245,242,235,0.4)" stroke-width="1.5" stroke-linecap="round"/>
        <rect x="10" y="8" width="28" height="32" rx="3" stroke="#ff3c2f" stroke-width="2"/>
        <path d="M18 20h12M18 28h8" stroke="rgba(245,242,235,0.7)" stroke-width="1.5" stroke-linecap="round"/>
        <circle cx="34" cy="34" r="8" fill="var(--ink)" stroke="#1a1aff" stroke-width="2"/>
        <path d="M31 34h6M34 31v6" stroke="#1a1aff" stroke-width="1.5" stroke-linecap="round"/>
      </svg>
      <h3 class="service-name">SaaS Platforms</h3>
      <p class="service-desc">Full-stack SaaS products with authentication, billing, dashboards, and multi-tenant architecture — ready to onboard your first paying customer.</p>
      <div class="service-tags">
        <span class="tag">Node.js</span>
        <span class="tag">PostgreSQL</span>
        <span class="tag">Stripe</span>
        <span class="tag">Auth</span>
      </div>
    </div>
    <div class="service-card reveal" style="transition-delay:0.24s">
      <svg class="service-icon" viewBox="0 0 48 48" fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="14" cy="24" r="8" stroke="#ff3c2f" stroke-width="2"/>
        <circle cx="34" cy="24" r="8" stroke="rgba(245,242,235,0.4)" stroke-width="2"/>
        <path d="M22 24h4" stroke="rgba(245,242,235,0.7)" stroke-width="2" stroke-linecap="round"/>
        <path d="M8 14v-4h4M8 34v4h4M40 14v-4h-4M40 34v4h-4" stroke="rgba(245,242,235,0.3)" stroke-width="1.5" stroke-linecap="round"/>
      </svg>
      <h3 class="service-name">B2B Solutions</h3>
      <p class="service-desc">Custom internal tools, client portals, CRM integrations, and automation workflows that streamline your business operations and impress your clients.</p>
      <div class="service-tags">
        <span class="tag">REST APIs</span>
        <span class="tag">Integrations</span>
        <span class="tag">Dashboards</span>
        <span class="tag">Automation</span>
      </div>
    </div>
  </div>
</section>

<!-- WORK -->
<section id="work">
  <div class="section-header reveal">
    <span class="section-num">02</span>
    <h2 class="section-title">Selected Work</h2>
  </div>
  <div class="work-grid">
    <div class="work-item reveal" style="--c1:#ff3c2f;--c2:#ff8a00">
      <div class="work-item-bg"></div>
      <span class="work-item-num">01 — SAAS PLATFORM</span>
      <h3 class="work-item-name">Analytics Dashboard</h3>
      <p class="work-item-type">B2B SaaS · React · Node.js · PostgreSQL</p>
      <a href="#contact" class="work-link">View details</a>
    </div>
    <div class="work-item reveal" style="--c1:#1a1aff;--c2:#8a00ff">
      <div class="work-item-bg"></div>
      <span class="work-item-num">02 — WEB APP</span>
      <h3 class="work-item-name">Client Portal</h3>
      <p class="work-item-type">B2B · Next.js · Auth · Stripe</p>
      <a href="#contact" class="work-link">View details</a>
    </div>
    <div class="work-item reveal" style="--c1:#00c896;--c2:#1a1aff">
      <div class="work-item-bg"></div>
      <span class="work-item-num">03 — WEBSITE</span>
      <h3 class="work-item-name">Marketing Site</h3>
      <p class="work-item-type">Corporate · Next.js · CMS · SEO</p>
      <a href="#contact" class="work-link">View details</a>
    </div>
  </div>
  <p style="margin-top:2rem;font-size:0.85rem;color:var(--mid);font-family:'Space Mono',monospace;letter-spacing:0.08em;">
    More work available on request — <a href="mailto:vlokprodction@gmail.com" style="color:var(--accent);text-decoration:none;">get in touch</a>
  </p>
</section>

<!-- PRICING -->
<section id="pricing">
  <div class="section-header reveal">
    <span class="section-num">03</span>
    <h2 class="section-title">Transparent Pricing</h2>
  </div>
  <div class="pricing-grid">
    <div class="pricing-card reveal">
      <p class="pricing-name">Starter</p>
      <p class="pricing-desc">Perfect for landing pages, portfolios, and small business sites.</p>
      <div class="price-row">
        <span class="price-currency">$</span>
        <span class="price-amount">299</span>
        <span class="price-period">/ project</span>
      </div>
      <ul class="pricing-features">
        <li class="pricing-feature">Up to 5 pages</li>
        <li class="pricing-feature">Responsive design</li>
        <li class="pricing-feature">Contact form</li>
        <li class="pricing-feature">SEO basics</li>
        <li class="pricing-feature">2 revision rounds</li>
        <li class="pricing-feature">7-day delivery</li>
      </ul>
      <a href="#contact" class="pricing-cta">Get started</a>
    </div>
    <div class="pricing-card featured reveal" style="transition-delay:0.12s">
      <span class="pricing-badge">Most Popular</span>
      <p class="pricing-name">Pro</p>
      <p class="pricing-desc">Custom web apps, SaaS MVPs, and full-featured business solutions.</p>
      <div class="price-row">
        <span class="price-currency">$</span>
        <span class="price-amount">999</span>
        <span class="price-period">/ project</span>
      </div>
      <ul class="pricing-features">
        <li class="pricing-feature">Full custom web app</li>
        <li class="pricing-feature">Backend + database</li>
        <li class="pricing-feature">User auth system</li>
        <li class="pricing-feature">Payment integration</li>
        <li class="pricing-feature">Unlimited revisions</li>
        <li class="pricing-feature">30-day support</li>
      </ul>
      <a href="#contact" class="pricing-cta">Get started</a>
    </div>
    <div class="pricing-card reveal" style="transition-delay:0.24s">
      <p class="pricing-name">Enterprise</p>
      <p class="pricing-desc">B2B platforms, large-scale SaaS, and ongoing development partnerships.</p>
      <div class="price-row">
        <span class="price-currency">$</span>
        <span class="price-amount">Custom</span>
      </div>
      <ul class="pricing-features">
        <li class="pricing-feature">Multi-tenant SaaS</li>
        <li class="pricing-feature">Custom integrations</li>
        <li class="pricing-feature">Team dashboards</li>
        <li class="pricing-feature">Priority support</li>
        <li class="pricing-feature">Retainer options</li>
        <li class="pricing-feature">NDA available</li>
      </ul>
      <a href="#contact" class="pricing-cta">Let's talk</a>
    </div>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="about-left reveal">
    <p class="about-eyebrow">// About me</p>
    <h2 class="about-title">Developer.<br/>Problem<br/>Solver.</h2>
    <p class="about-body">
      I'm Vishwa Aloka — a freelance web developer specialising in clean, functional digital products. I bridge the gap between design and engineering to deliver web solutions that work beautifully and scale reliably.
    </p>
    <p class="about-body">
      From lean MVPs to production-grade SaaS platforms, I work closely with founders, product teams, and businesses to bring their digital vision to life — on time, within budget, and with zero compromises on quality.
    </p>
    <a href="https://vishwa-aloka-16.github.io" target="_blank" rel="noopener noreferrer" class="about-profile-link">
      Visit full profile
    </a>
  </div>
  <div class="about-right reveal" style="transition-delay:0.15s">
    <div class="about-card">
      <h4 class="about-card-title">Frontend</h4>
      <div class="skill-list">
        <span class="skill-pill">HTML5</span>
        <span class="skill-pill">CSS3</span>
        <span class="skill-pill">JavaScript</span>
        <span class="skill-pill">TypeScript</span>
        <span class="skill-pill">React</span>
        <span class="skill-pill">Next.js</span>
        <span class="skill-pill">Tailwind</span>
        <span class="skill-pill">Figma</span>
      </div>
    </div>
    <div class="about-card">
      <h4 class="about-card-title">Backend & Data</h4>
      <div class="skill-list">
        <span class="skill-pill">Node.js</span>
        <span class="skill-pill">Express</span>
        <span class="skill-pill">PostgreSQL</span>
        <span class="skill-pill">MongoDB</span>
        <span class="skill-pill">REST API</span>
        <span class="skill-pill">GraphQL</span>
        <span class="skill-pill">Firebase</span>
      </div>
    </div>
    <div class="about-card">
      <h4 class="about-card-title">Tools & DevOps</h4>
      <div class="skill-list">
        <span class="skill-pill">Git</span>
        <span class="skill-pill">Vercel</span>
        <span class="skill-pill">AWS</span>
        <span class="skill-pill">Docker</span>
        <span class="skill-pill">Stripe</span>
        <span class="skill-pill">Supabase</span>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="contact-inner">
    <div class="reveal">
      <h2 class="contact-title">
        Let's<br/>
        <span>Work.</span>
      </h2>
      <p class="contact-sub">
        Have a project in mind? Whether it's a quick site or a complex SaaS platform, I'd love to hear about it. Reach out and let's build something great together.
      </p>
      <div class="contact-links">
        <a href="mailto:vlokprodction@gmail.com" class="contact-link-row">
          <div>
            <div class="cl-label">Email</div>
            <div class="cl-value">vlokprodction@gmail.com</div>
          </div>
          <span class="cl-arrow">↗</span>
        </a>
        <a href="https://vishwa-aloka-16.github.io" target="_blank" rel="noopener" class="contact-link-row">
          <div>
            <div class="cl-label">Portfolio</div>
            <div class="cl-value">vishwa-aloka-16.github.io</div>
          </div>
          <span class="cl-arrow">↗</span>
        </a>
        <a href="https://github.com/vlokprodction" target="_blank" rel="noopener" class="contact-link-row">
          <div>
            <div class="cl-label">GitHub</div>
            <div class="cl-value">vlokprodction</div>
          </div>
          <span class="cl-arrow">↗</span>
        </a>
      </div>
    </div>
    <div class="contact-right reveal" style="transition-delay:0.15s">
      <p class="contact-form-title">Send a message</p>
      <div class="form-group">
        <label>Your name</label>
        <input type="text" placeholder="Jane Smith" />
      </div>
      <div class="form-group">
        <label>Email address</label>
        <input type="email" placeholder="jane@company.com" />
      </div>
      <div class="form-group">
        <label>Project type</label>
        <select>
          <option value="">Select a service...</option>
          <option>Website / Landing Page</option>
          <option>SaaS Platform</option>
          <option>B2B Web App</option>
          <option>API / Backend</option>
          <option>Other</option>
        </select>
      </div>
      <div class="form-group">
        <label>Tell me about your project</label>
        <textarea placeholder="Describe what you're building and your timeline..."></textarea>
      </div>
      <button class="form-submit" onclick="handleSubmit(this)">Send message →</button>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <span class="footer-logo">VLOK/PRODUCTION</span>
  <span class="footer-copy">© 2025 VlokProduction — <span>Available for new projects</span></span>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  document.addEventListener('mousemove', e => {
    cursor.style.left = e.clientX + 'px';
    cursor.style.top = e.clientY + 'px';
  });
  document.querySelectorAll('a, button, .work-item, .service-card, .pricing-card').forEach(el => {
    el.addEventListener('mouseenter', () => cursor.classList.add('expand'));
    el.addEventListener('mouseleave', () => cursor.classList.remove('expand'));
  });

  // Scroll reveal
  const revealEls = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, { threshold: 0.12 });
  revealEls.forEach(el => observer.observe(el));

  // Simple form handler
  function handleSubmit(btn) {
    const name = btn.closest('.contact-right').querySelector('input[type="text"]').value;
    const email = btn.closest('.contact-right').querySelector('input[type="email"]').value;
    const message = btn.closest('.contact-right').querySelector('textarea').value;

    if (!name || !email || !message) {
      btn.textContent = 'Please fill all fields';
      btn.style.background = 'rgba(255,60,47,0.2)';
      btn.style.color = 'var(--accent)';
      setTimeout(() => {
        btn.textContent = 'Send message →';
        btn.style.background = 'var(--accent)';
        btn.style.color = 'var(--paper)';
      }, 2000);
      return;
    }

    // Compose mailto
    const subject = encodeURIComponent('Project Inquiry from ' + name);
    const body = encodeURIComponent(`Name: ${name}\nEmail: ${email}\n\n${message}`);
    window.location.href = `mailto:vlokprodction@gmail.com?subject=${subject}&body=${body}`;

    btn.textContent = 'Opening email client...';
    btn.style.background = 'rgba(245,242,235,0.1)';
  }
</script>
</body>
</html>
