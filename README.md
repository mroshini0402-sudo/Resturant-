<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Swan Oyster Depot — San Francisco Since 1912</title>
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --ink:      #1a1714;
    --shell:    #f5f0e8;
    --brine:    #2b4a5e;
    --pearl:    #e8ddd0;
    --copper:   #8a6340;
    --mist:     #7a9aaa;
    --white:    #fdfbf8;

    --display: 'Cormorant Garamond', Georgia, serif;
    --body:    'DM Sans', system-ui, sans-serif;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: var(--body);
    background: var(--white);
    color: var(--ink);
    overflow-x: hidden;
  }

  /* ── NAV ── */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px 48px;
    background: transparent;
    transition: background 0.4s, backdrop-filter 0.4s;
  }
  nav.scrolled {
    background: rgba(253,251,248,0.92);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid rgba(26,23,20,0.08);
  }
  .nav-logo {
    font-family: var(--display);
    font-size: 1.1rem;
    font-weight: 600;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--white);
    text-decoration: none;
    transition: color 0.3s;
  }
  nav.scrolled .nav-logo { color: var(--ink); }
  .nav-links { display: flex; gap: 36px; list-style: none; }
  .nav-links a {
    font-size: 0.78rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: rgba(253,251,248,0.85);
    text-decoration: none;
    transition: color 0.3s;
  }
  nav.scrolled .nav-links a { color: var(--ink); }
  .nav-links a:hover { color: var(--copper); }
  .nav-cta {
    font-size: 0.78rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--white);
    border: 1px solid rgba(253,251,248,0.4);
    padding: 10px 22px;
    border-radius: 2px;
    text-decoration: none;
    transition: all 0.3s;
  }
  nav.scrolled .nav-cta { color: var(--brine); border-color: var(--brine); }
  .nav-cta:hover { background: var(--copper); border-color: var(--copper); color: var(--white) !important; }

  .hamburger { display: none; flex-direction: column; gap: 5px; cursor: pointer; }
  .hamburger span { width: 24px; height: 1.5px; background: var(--white); transition: background 0.3s; }
  nav.scrolled .hamburger span { background: var(--ink); }

  /* ── HERO ── */
  .hero {
    position: relative;
    height: 100vh;
    min-height: 640px;
    display: flex;
    align-items: flex-end;
    overflow: hidden;
  }
  .hero-bg {
    position: absolute; inset: 0;
    background:
      linear-gradient(to top, rgba(26,23,20,0.88) 0%, rgba(26,23,20,0.3) 55%, rgba(26,23,20,0.15) 100%),
      url('https://images.unsplash.com/photo-1559737558-2f5a35f4523b?w=1600&q=80') center/cover no-repeat;
  }
  .hero-content {
    position: relative;
    z-index: 1;
    padding: 0 48px 80px;
    max-width: 780px;
  }
  .hero-eyebrow {
    font-family: var(--body);
    font-size: 0.72rem;
    font-weight: 500;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--mist);
    margin-bottom: 20px;
  }
  .hero h1 {
    font-family: var(--display);
    font-size: clamp(3.2rem, 8vw, 6.5rem);
    font-weight: 300;
    line-height: 0.95;
    color: var(--white);
    margin-bottom: 28px;
  }
  .hero h1 em { font-style: italic; color: var(--pearl); }
  .hero-sub {
    font-size: 1rem;
    font-weight: 300;
    line-height: 1.7;
    color: rgba(253,251,248,0.75);
    max-width: 480px;
    margin-bottom: 40px;
  }
  .hero-actions { display: flex; gap: 16px; flex-wrap: wrap; }
  .btn-primary {
    display: inline-block;
    background: var(--copper);
    color: var(--white);
    font-size: 0.78rem;
    font-weight: 500;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 16px 36px;
    border-radius: 2px;
    text-decoration: none;
    transition: all 0.3s;
  }
  .btn-primary:hover { background: #7a5530; transform: translateY(-1px); }
  .btn-ghost {
    display: inline-block;
    color: var(--white);
    font-size: 0.78rem;
    font-weight: 500;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 15px 36px;
    border: 1px solid rgba(253,251,248,0.4);
    border-radius: 2px;
    text-decoration: none;
    transition: all 0.3s;
  }
  .btn-ghost:hover { border-color: var(--white); background: rgba(253,251,248,0.08); }

  .hero-badges {
    position: absolute;
    right: 48px;
    bottom: 80px;
    display: flex;
    flex-direction: column;
    gap: 12px;
    text-align: right;
  }
  .badge {
    font-family: var(--display);
    font-size: 0.85rem;
    font-style: italic;
    color: rgba(253,251,248,0.6);
    letter-spacing: 0.04em;
  }

  /* ── TICKER ── */
  .ticker {
    background: var(--brine);
    padding: 14px 0;
    overflow: hidden;
    white-space: nowrap;
  }
  .ticker-track {
    display: inline-flex;
    gap: 64px;
    animation: ticker 30s linear infinite;
  }
  .ticker-item {
    font-size: 0.7rem;
    font-weight: 500;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: rgba(253,251,248,0.7);
  }
  .ticker-dot {
    display: inline-block;
    width: 4px; height: 4px;
    border-radius: 50%;
    background: var(--mist);
    vertical-align: middle;
    margin: 0 32px;
  }
  @keyframes ticker { from { transform: translateX(0); } to { transform: translateX(-50%); } }

  /* ── SECTIONS SHARED ── */
  section { padding: 100px 48px; }
  .section-eyebrow {
    font-size: 0.7rem;
    font-weight: 500;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--copper);
    margin-bottom: 16px;
  }
  .section-title {
    font-family: var(--display);
    font-size: clamp(2.2rem, 5vw, 3.8rem);
    font-weight: 300;
    line-height: 1.1;
    color: var(--ink);
    margin-bottom: 24px;
  }
  .section-title em { font-style: italic; }

  /* ── ABOUT ── */
  #about { background: var(--shell); }
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto;
  }
  .about-text p {
    font-size: 1.05rem;
    font-weight: 300;
    line-height: 1.8;
    color: #3d3830;
    margin-bottom: 20px;
  }
  .about-text p:last-child { margin-bottom: 0; }
  .about-stats {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 32px;
    margin-top: 40px;
  }
  .stat-item {}
  .stat-number {
    font-family: var(--display);
    font-size: 3rem;
    font-weight: 300;
    color: var(--brine);
    line-height: 1;
  }
  .stat-label {
    font-size: 0.75rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--copper);
    margin-top: 6px;
  }
  .about-image {
    position: relative;
  }
  .about-image img {
    width: 100%;
    aspect-ratio: 3/4;
    object-fit: cover;
    border-radius: 2px;
  }
  .about-image-caption {
    position: absolute;
    bottom: -20px;
    right: -20px;
    background: var(--brine);
    color: var(--white);
    padding: 20px 24px;
    font-family: var(--display);
    font-size: 1rem;
    font-style: italic;
    max-width: 220px;
    line-height: 1.5;
  }

  /* ── MENU / SIGNATURE ── */
  #menu { background: var(--white); }
  .menu-inner { max-width: 1200px; margin: 0 auto; }
  .menu-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    margin-bottom: 64px;
    flex-wrap: wrap;
    gap: 24px;
  }
  .menu-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
  }
  .menu-card {
    position: relative;
    overflow: hidden;
    aspect-ratio: 4/5;
    cursor: pointer;
  }
  .menu-card img {
    width: 100%; height: 100%;
    object-fit: cover;
    transition: transform 0.6s cubic-bezier(0.25,0.46,0.45,0.94);
  }
  .menu-card:hover img { transform: scale(1.06); }
  .menu-card-overlay {
    position: absolute;
    inset: 0;
    background: linear-gradient(to top, rgba(26,23,20,0.85) 0%, transparent 55%);
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: 28px;
  }
  .menu-card-tag {
    font-size: 0.65rem;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--mist);
    margin-bottom: 8px;
  }
  .menu-card-name {
    font-family: var(--display);
    font-size: 1.5rem;
    font-weight: 300;
    color: var(--white);
    line-height: 1.2;
  }
  .menu-card.featured { grid-row: span 2; }
  .menu-card.featured .menu-card-name { font-size: 2.2rem; }

  /* ── EXPERIENCE ── */
  #experience { background: var(--ink); padding: 100px 48px; }
  .exp-inner { max-width: 1200px; margin: 0 auto; }
  .exp-inner .section-eyebrow { color: var(--mist); }
  .exp-inner .section-title { color: var(--white); }
  .exp-list {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 1px;
    margin-top: 64px;
    border: 1px solid rgba(255,255,255,0.08);
  }
  .exp-item {
    padding: 40px 32px;
    border-right: 1px solid rgba(255,255,255,0.08);
  }
  .exp-item:last-child { border-right: none; }
  .exp-icon {
    font-size: 1.8rem;
    margin-bottom: 20px;
    display: block;
  }
  .exp-item-title {
    font-family: var(--display);
    font-size: 1.3rem;
    font-weight: 400;
    color: var(--white);
    margin-bottom: 12px;
  }
  .exp-item-desc {
    font-size: 0.88rem;
    font-weight: 300;
    line-height: 1.7;
    color: rgba(253,251,248,0.5);
  }

  /* ── TESTIMONIALS ── */
  #testimonials { background: var(--shell); }
  .testi-inner { max-width: 1200px; margin: 0 auto; }
  .testi-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    margin-bottom: 64px;
    flex-wrap: wrap;
    gap: 24px;
  }
  .testi-grid {
    display: grid;
    grid-template-columns: 1.4fr 1fr 1fr;
    gap: 24px;
  }
  .testi-card {
    background: var(--white);
    padding: 40px;
    border-radius: 2px;
    display: flex;
    flex-direction: column;
    gap: 20px;
  }
  .testi-card.featured { background: var(--brine); }
  .stars { color: var(--copper); font-size: 0.85rem; letter-spacing: 3px; }
  .testi-card.featured .stars { color: var(--mist); }
  .testi-quote {
    font-family: var(--display);
    font-size: 1.2rem;
    font-style: italic;
    font-weight: 300;
    line-height: 1.6;
    color: var(--ink);
    flex: 1;
  }
  .testi-card.featured .testi-quote { color: var(--white); }
  .testi-author { display: flex; align-items: center; gap: 14px; }
  .testi-avatar {
    width: 40px; height: 40px;
    border-radius: 50%;
    background: var(--pearl);
    display: flex; align-items: center; justify-content: center;
    font-family: var(--display);
    font-size: 1.1rem;
    color: var(--brine);
    font-weight: 600;
    flex-shrink: 0;
  }
  .testi-card.featured .testi-avatar { background: rgba(255,255,255,0.15); color: var(--white); }
  .testi-name {
    font-size: 0.85rem;
    font-weight: 500;
    color: var(--ink);
  }
  .testi-card.featured .testi-name { color: var(--white); }
  .testi-meta {
    font-size: 0.75rem;
    color: var(--copper);
    margin-top: 2px;
  }
  .testi-card.featured .testi-meta { color: var(--mist); }

  /* ── VISIT / CTA ── */
  #visit {
    background: var(--white);
    padding: 100px 48px;
  }
  .visit-inner {
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: start;
  }
  .visit-info .section-title { margin-bottom: 32px; }
  .info-row {
    display: flex;
    align-items: flex-start;
    gap: 16px;
    padding: 20px 0;
    border-bottom: 1px solid var(--pearl);
  }
  .info-icon { font-size: 1.1rem; flex-shrink: 0; margin-top: 2px; }
  .info-label {
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--copper);
    margin-bottom: 4px;
  }
  .info-value {
    font-size: 0.95rem;
    font-weight: 300;
    line-height: 1.6;
    color: var(--ink);
  }
  .info-note {
    font-size: 0.78rem;
    color: var(--mist);
    margin-top: 4px;
  }
  .visit-cta-box {
    background: var(--brine);
    padding: 56px 48px;
    display: flex;
    flex-direction: column;
    gap: 28px;
  }
  .visit-cta-box .section-eyebrow { color: var(--mist); }
  .visit-cta-box .section-title { color: var(--white); }
  .visit-cta-box p {
    font-size: 0.95rem;
    font-weight: 300;
    line-height: 1.8;
    color: rgba(253,251,248,0.7);
  }
  .btn-light {
    display: inline-block;
    background: var(--white);
    color: var(--brine);
    font-size: 0.78rem;
    font-weight: 500;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 16px 36px;
    border-radius: 2px;
    text-decoration: none;
    transition: all 0.3s;
    align-self: flex-start;
  }
  .btn-light:hover { background: var(--pearl); transform: translateY(-1px); }

  /* ── FOOTER ── */
  footer {
    background: var(--ink);
    padding: 64px 48px 40px;
    color: rgba(253,251,248,0.5);
  }
  .footer-top {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 48px;
    margin-bottom: 56px;
    flex-wrap: wrap;
  }
  .footer-brand {
    font-family: var(--display);
    font-size: 1.5rem;
    font-weight: 300;
    color: var(--white);
    margin-bottom: 12px;
  }
  .footer-tagline {
    font-size: 0.82rem;
    line-height: 1.7;
    max-width: 260px;
  }
  .footer-links h4 {
    font-size: 0.7rem;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: rgba(253,251,248,0.3);
    margin-bottom: 16px;
  }
  .footer-links ul { list-style: none; display: flex; flex-direction: column; gap: 10px; }
  .footer-links a {
    font-size: 0.88rem;
    color: rgba(253,251,248,0.6);
    text-decoration: none;
    transition: color 0.2s;
  }
  .footer-links a:hover { color: var(--white); }
  .footer-bottom {
    border-top: 1px solid rgba(255,255,255,0.08);
    padding-top: 28px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 12px;
  }
  .footer-bottom p { font-size: 0.78rem; }
  .footer-bottom span { color: var(--mist); }

  /* ── SCROLL ANIMATIONS ── */
  .reveal {
    opacity: 0;
    transform: translateY(32px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: none; }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }

  /* ── MOBILE ── */
  @media (max-width: 900px) {
    nav { padding: 18px 24px; }
    .nav-links, .nav-cta { display: none; }
    .hamburger { display: flex; }

    section { padding: 72px 24px; }
    .hero-content { padding: 0 24px 64px; }
    .hero-badges { display: none; }

    .about-grid { grid-template-columns: 1fr; gap: 48px; }
    .about-image-caption { right: 0; bottom: -16px; }
    .menu-grid {
      grid-template-columns: 1fr 1fr;
    }
    .menu-card.featured { grid-row: auto; }
    .exp-list { grid-template-columns: 1fr 1fr; }
    .exp-item { border-right: none; border-bottom: 1px solid rgba(255,255,255,0.08); }
    .testi-grid { grid-template-columns: 1fr; }
    .visit-inner { grid-template-columns: 1fr; gap: 48px; }
    footer { padding: 48px 24px 32px; }
    .footer-top { flex-direction: column; gap: 36px; }
    #experience { padding: 72px 24px; }
  }

  @media (max-width: 580px) {
    .menu-grid { grid-template-columns: 1fr; }
    .exp-list { grid-template-columns: 1fr; }
    .about-stats { grid-template-columns: 1fr 1fr; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav id="nav">
  <a href="#" class="nav-logo">Swan Oyster Depot</a>
  <ul class="nav-links">
    <li><a href="#about">Our Story</a></li>
    <li><a href="#menu">Menu</a></li>
    <li><a href="#testimonials">Reviews</a></li>
    <li><a href="#visit">Visit</a></li>
  </ul>
  <a href="tel:+14156731101" class="nav-cta">Call Us</a>
  <div class="hamburger" aria-label="Menu">
    <span></span><span></span><span></span>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-bg"></div>
  <div class="hero-content">
    <p class="hero-eyebrow">San Francisco · Since 1912 · 1517 Polk Street</p>
    <h1>The <em>finest</em><br>seafood<br>in the city.</h1>
    <p class="hero-sub">
      A Polk Street legend. Counter seating, cash only, no reservations — and the freshest oysters, crab, and salmon you'll find in San Francisco.
    </p>
    <div class="hero-actions">
      <a href="tel:+14156731101" class="btn-primary">Call to Order</a>
      <a href="#menu" class="btn-ghost">View Menu</a>
    </div>
  </div>
  <div class="hero-badges">
    <p class="badge">"Anthony Bourdain's<br>favorite spot in SF"</p>
    <p class="badge">★ 4.6 · 2,200+ Reviews</p>
  </div>
</section>

<!-- TICKER -->
<div class="ticker">
  <div class="ticker-track" aria-hidden="true">
    <span class="ticker-item">Fresh Daily</span><span class="ticker-dot"></span>
    <span class="ticker-item">Dungeness Crab</span><span class="ticker-dot"></span>
    <span class="ticker-item">Half Dozen Oysters</span><span class="ticker-dot"></span>
    <span class="ticker-item">Smoked Salmon</span><span class="ticker-dot"></span>
    <span class="ticker-item">Cash Only</span><span class="ticker-dot"></span>
    <span class="ticker-item">Open Since 1912</span><span class="ticker-dot"></span>
    <span class="ticker-item">Counter Seating</span><span class="ticker-dot"></span>
    <span class="ticker-item">Crab Salad</span><span class="ticker-dot"></span>
    <span class="ticker-item">Seafood Cocktails</span><span class="ticker-dot"></span>
    <span class="ticker-item">A San Francisco Icon</span><span class="ticker-dot"></span>
    <!-- repeat for seamless loop -->
    <span class="ticker-item">Fresh Daily</span><span class="ticker-dot"></span>
    <span class="ticker-item">Dungeness Crab</span><span class="ticker-dot"></span>
    <span class="ticker-item">Half Dozen Oysters</span><span class="ticker-dot"></span>
    <span class="ticker-item">Smoked Salmon</span><span class="ticker-dot"></span>
    <span class="ticker-item">Cash Only</span><span class="ticker-dot"></span>
    <span class="ticker-item">Open Since 1912</span><span class="ticker-dot"></span>
    <span class="ticker-item">Counter Seating</span><span class="ticker-dot"></span>
    <span class="ticker-item">Crab Salad</span><span class="ticker-dot"></span>
    <span class="ticker-item">Seafood Cocktails</span><span class="ticker-dot"></span>
    <span class="ticker-item">A San Francisco Icon</span><span class="ticker-dot"></span>
  </div>
</div>

<!-- ABOUT -->
<section id="about">
  <div class="about-grid">
    <div class="about-text reveal">
      <p class="section-eyebrow">Our Story</p>
      <h2 class="section-title">A century of<br><em>pure seafood.</em></h2>
      <p>Swan Oyster Depot has been a fixture on Polk Street since 1912. No frills, no distractions — just a marble counter, a handful of stools, and the best raw bar in the city. The Sancimino family has kept the tradition alive for generations.</p>
      <p>There's no website menu to scroll, no online reservation system. You line up, you sit down, and you eat seafood the way it was meant to be eaten: fresh out of the water and served with a squeeze of lemon.</p>
      <div class="about-stats">
        <div class="stat-item reveal reveal-delay-1">
          <div class="stat-number">1912</div>
          <div class="stat-label">Est. in SF</div>
        </div>
        <div class="stat-item reveal reveal-delay-2">
          <div class="stat-number">4.6★</div>
          <div class="stat-label </html>
