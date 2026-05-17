<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FarmLink — Farm to Table, No Middlemen</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Sans:wght@300;400;500;600&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --soil: #2D1B0E;
    --bark: #4A2C1A;
    --harvest: #E8A020;
    --wheat: #F5D98B;
    --sage: #6B8F5E;
    --moss: #4A6741;
    --sprout: #A8C494;
    --cream: #FAF6EE;
    --offwhite: #F2EDE3;
    --terracotta: #C0522A;
    --sky: #8BB8C8;
    --text: #1A0F00;
    --muted: #6B5B47;
    --card-bg: #FFFCF5;
    --border: #E8DEC9;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--cream);
    color: var(--text);
    overflow-x: hidden;
  }

  /* ─── NOISE TEXTURE OVERLAY ─── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 9999;
    opacity: 0.4;
  }

  /* ─── NAV ─── */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 1000;
    background: rgba(250,246,238,0.92);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
    padding: 0 2rem;
    height: 64px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .nav-logo {
    font-family: 'Playfair Display', serif;
    font-weight: 900;
    font-size: 1.5rem;
    color: var(--moss);
    display: flex;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
  }

  .nav-logo span { color: var(--harvest); }

  .nav-links {
    display: flex;
    gap: 2rem;
    list-style: none;
    align-items: center;
  }

  .nav-links a {
    text-decoration: none;
    color: var(--muted);
    font-size: 0.9rem;
    font-weight: 500;
    letter-spacing: 0.02em;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--moss); }

  .nav-actions {
    display: flex;
    gap: 0.75rem;
    align-items: center;
  }

  .btn {
    padding: 0.55rem 1.25rem;
    border-radius: 100px;
    font-family: 'DM Sans', sans-serif;
    font-weight: 600;
    font-size: 0.85rem;
    cursor: pointer;
    border: none;
    transition: all 0.2s;
    letter-spacing: 0.01em;
  }

  .btn-ghost {
    background: transparent;
    color: var(--moss);
    border: 1.5px solid var(--moss);
  }
  .btn-ghost:hover { background: var(--moss); color: white; }

  .btn-primary {
    background: var(--moss);
    color: white;
  }
  .btn-primary:hover { background: var(--soil); transform: translateY(-1px); }

  .btn-harvest {
    background: var(--harvest);
    color: var(--soil);
  }
  .btn-harvest:hover { background: #d4901a; transform: translateY(-1px); }

  .cart-btn {
    position: relative;
    background: var(--soil);
    color: white;
    border: none;
    width: 42px; height: 42px;
    border-radius: 50%;
    cursor: pointer;
    font-size: 1.1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: transform 0.2s;
  }
  .cart-btn:hover { transform: scale(1.08); }

  .cart-badge {
    position: absolute;
    top: -4px; right: -4px;
    background: var(--terracotta);
    color: white;
    font-size: 0.6rem;
    font-weight: 700;
    width: 18px; height: 18px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 2px solid var(--cream);
  }

  /* ─── HERO ─── */
  .hero {
    min-height: 100vh;
    padding-top: 64px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    position: relative;
    overflow: hidden;
  }

  .hero-left {
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 5rem 3rem 5rem 5rem;
  }

  .hero-eyebrow {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    background: var(--sprout);
    color: var(--moss);
    padding: 0.35rem 0.9rem;
    border-radius: 100px;
    font-size: 0.78rem;
    font-weight: 600;
    letter-spacing: 0.05em;
    text-transform: uppercase;
    margin-bottom: 1.5rem;
    width: fit-content;
    animation: fadeUp 0.8s ease both;
  }

  .hero-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(3rem, 5vw, 5rem);
    font-weight: 900;
    line-height: 1.05;
    margin-bottom: 1.5rem;
    animation: fadeUp 0.8s 0.1s ease both;
  }

  .hero-title em {
    font-style: normal;
    color: var(--harvest);
    position: relative;
    display: inline-block;
  }

  .hero-title em::after {
    content: '';
    position: absolute;
    bottom: 4px; left: 0; right: 0;
    height: 6px;
    background: var(--sprout);
    z-index: -1;
    border-radius: 3px;
  }

  .hero-desc {
    font-size: 1.1rem;
    color: var(--muted);
    line-height: 1.7;
    max-width: 480px;
    margin-bottom: 2.5rem;
    animation: fadeUp 0.8s 0.2s ease both;
  }

  .hero-cta {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    animation: fadeUp 0.8s 0.3s ease both;
  }

  .hero-cta .btn {
    padding: 0.85rem 2rem;
    font-size: 1rem;
  }

  .hero-stats {
    display: flex;
    gap: 2.5rem;
    margin-top: 3.5rem;
    animation: fadeUp 0.8s 0.4s ease both;
  }

  .stat-item { text-align: left; }
  .stat-num {
    font-family: 'Playfair Display', serif;
    font-size: 2rem;
    font-weight: 700;
    color: var(--moss);
  }
  .stat-label {
    font-size: 0.78rem;
    color: var(--muted);
    letter-spacing: 0.04em;
    text-transform: uppercase;
    font-weight: 500;
  }

  .hero-right {
    position: relative;
    overflow: hidden;
    background: var(--moss);
    clip-path: polygon(8% 0, 100% 0, 100% 100%, 0% 100%);
  }

  .hero-right-inner {
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 3rem;
    gap: 1.5rem;
  }

  .hero-image-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto auto;
    gap: 1rem;
    width: 100%;
    max-width: 420px;
    animation: fadeIn 1s 0.5s ease both;
  }

  .hero-img-card {
    border-radius: 16px;
    overflow: hidden;
    background: var(--bark);
    position: relative;
    height: 180px;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: 1rem;
  }

  .hero-img-card.tall { grid-row: span 2; height: 100%; }

  .hero-img-emoji {
    font-size: 3.5rem;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -60%);
    filter: drop-shadow(0 4px 8px rgba(0,0,0,0.3));
    transition: transform 0.3s;
  }
  .hero-img-card:hover .hero-img-emoji { transform: translate(-50%, -65%) scale(1.1); }

  .hero-img-label {
    color: white;
    font-size: 0.75rem;
    font-weight: 600;
    letter-spacing: 0.03em;
    text-transform: uppercase;
    background: rgba(0,0,0,0.4);
    backdrop-filter: blur(4px);
    padding: 0.3rem 0.7rem;
    border-radius: 8px;
    width: fit-content;
    position: relative;
    z-index: 1;
  }

  .hero-img-price {
    color: var(--harvest);
    font-size: 0.85rem;
    font-weight: 700;
    position: relative;
    z-index: 1;
  }

  /* gradient overlays for img cards */
  .hero-img-card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(to bottom, transparent 40%, rgba(0,0,0,0.6));
    z-index: 0;
  }

  /* card colors */
  .card-green { background: linear-gradient(135deg, #3a6b2e, #5a9e4a); }
  .card-orange { background: linear-gradient(135deg, #a84820, #d4702a); }
  .card-yellow { background: linear-gradient(135deg, #8a7020, #c4a830); }
  .card-blue { background: linear-gradient(135deg, #2a5870, #4a90a8); }

  /* ─── MARQUEE STRIP ─── */
  .marquee-strip {
    background: var(--soil);
    padding: 0.75rem 0;
    overflow: hidden;
    white-space: nowrap;
  }

  .marquee-inner {
    display: inline-flex;
    gap: 3rem;
    animation: marquee 20s linear infinite;
  }

  .marquee-item {
    color: var(--wheat);
    font-size: 0.85rem;
    font-weight: 500;
    letter-spacing: 0.03em;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .marquee-dot {
    width: 5px; height: 5px;
    background: var(--harvest);
    border-radius: 50%;
    display: inline-block;
  }

  @keyframes marquee {
    from { transform: translateX(0); }
    to { transform: translateX(-50%); }
  }

  /* ─── SECTION COMMON ─── */
  section { padding: 6rem 5rem; }

  .section-tag {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    font-size: 0.75rem;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--moss);
    margin-bottom: 1rem;
  }

  .section-tag::before {
    content: '';
    width: 20px; height: 2px;
    background: var(--harvest);
    display: inline-block;
  }

  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 3.5vw, 3rem);
    font-weight: 800;
    line-height: 1.15;
    margin-bottom: 1rem;
  }

  .section-sub {
    font-size: 1.05rem;
    color: var(--muted);
    max-width: 520px;
    line-height: 1.7;
  }

  /* ─── HOW IT WORKS ─── */
  .how-section { background: var(--offwhite); }

  .how-header {
    text-align: center;
    margin-bottom: 4rem;
  }
  .how-header .section-tag { justify-content: center; }
  .how-header .section-sub { margin: 0 auto; }

  .how-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 2rem;
    position: relative;
  }

  .how-grid::before {
    content: '';
    position: absolute;
    top: 2.5rem;
    left: 15%;
    right: 15%;
    height: 2px;
    background: repeating-linear-gradient(90deg, var(--sprout) 0, var(--sprout) 8px, transparent 8px, transparent 16px);
    z-index: 0;
  }

  .how-card {
    background: white;
    border-radius: 20px;
    padding: 2rem 1.5rem;
    text-align: center;
    border: 1px solid var(--border);
    position: relative;
    z-index: 1;
    transition: transform 0.3s, box-shadow 0.3s;
  }
  .how-card:hover { transform: translateY(-6px); box-shadow: 0 20px 40px rgba(45,27,14,0.1); }

  .how-icon {
    width: 64px; height: 64px;
    background: var(--sprout);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 1.25rem;
    font-size: 1.75rem;
    position: relative;
  }

  .how-step {
    position: absolute;
    top: -6px; right: -6px;
    background: var(--moss);
    color: white;
    width: 22px; height: 22px;
    border-radius: 50%;
    font-size: 0.65rem;
    font-weight: 700;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'DM Mono', monospace;
  }

  .how-card h3 {
    font-family: 'Playfair Display', serif;
    font-size: 1.15rem;
    font-weight: 700;
    margin-bottom: 0.6rem;
  }

  .how-card p { font-size: 0.88rem; color: var(--muted); line-height: 1.6; }

  /* ─── PRODUCTS ─── */
  .products-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    margin-bottom: 2.5rem;
    flex-wrap: wrap;
    gap: 1rem;
  }

  .category-tabs {
    display: flex;
    gap: 0.5rem;
    flex-wrap: wrap;
    margin-bottom: 2.5rem;
  }

  .tab-btn {
    padding: 0.45rem 1.1rem;
    border-radius: 100px;
    font-size: 0.83rem;
    font-weight: 600;
    border: 1.5px solid var(--border);
    background: white;
    color: var(--muted);
    cursor: pointer;
    transition: all 0.2s;
  }
  .tab-btn:hover, .tab-btn.active {
    background: var(--moss);
    color: white;
    border-color: var(--moss);
  }

  .products-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 1.5rem;
  }

  .product-card {
    background: var(--card-bg);
    border-radius: 20px;
    border: 1px solid var(--border);
    overflow: hidden;
    transition: transform 0.3s, box-shadow 0.3s;
    cursor: pointer;
    animation: fadeUp 0.5s ease both;
  }
  .product-card:hover { transform: translateY(-6px); box-shadow: 0 24px 48px rgba(45,27,14,0.12); }

  .product-img {
    height: 180px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 4.5rem;
    position: relative;
    overflow: hidden;
  }

  .product-badge {
    position: absolute;
    top: 0.75rem; left: 0.75rem;
    background: var(--harvest);
    color: var(--soil);
    font-size: 0.65rem;
    font-weight: 700;
    padding: 0.25rem 0.6rem;
    border-radius: 6px;
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }

  .product-badge.organic { background: var(--sprout); color: var(--moss); }
  .product-badge.sale { background: var(--terracotta); color: white; }

  .product-fav {
    position: absolute;
    top: 0.75rem; right: 0.75rem;
    background: white;
    border: none;
    width: 32px; height: 32px;
    border-radius: 50%;
    cursor: pointer;
    font-size: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    transition: transform 0.2s;
  }
  .product-fav:hover { transform: scale(1.2); }
  .product-fav.liked { color: #e53;  }

  .product-body { padding: 1.25rem; }

  .product-farmer {
    display: flex;
    align-items: center;
    gap: 0.4rem;
    margin-bottom: 0.5rem;
  }

  .farmer-avatar {
    width: 22px; height: 22px;
    border-radius: 50%;
    background: var(--moss);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.6rem;
    color: white;
    font-weight: 700;
    flex-shrink: 0;
  }

  .farmer-name {
    font-size: 0.75rem;
    color: var(--muted);
    font-weight: 500;
  }

  .farmer-verified { color: var(--moss); font-size: 0.7rem; }

  .product-name {
    font-family: 'Playfair Display', serif;
    font-size: 1.05rem;
    font-weight: 700;
    margin-bottom: 0.3rem;
    line-height: 1.3;
  }

  .product-meta {
    font-size: 0.78rem;
    color: var(--muted);
    margin-bottom: 0.75rem;
  }

  .product-price-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 0.5rem;
  }

  .product-price {
    display: flex;
    align-items: baseline;
    gap: 0.4rem;
  }

  .price-current {
    font-family: 'DM Mono', monospace;
    font-size: 1.2rem;
    font-weight: 700;
    color: var(--moss);
  }

  .price-old {
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    color: var(--muted);
    text-decoration: line-through;
  }

  .price-save {
    font-size: 0.7rem;
    color: var(--terracotta);
    font-weight: 600;
  }

  .add-cart-btn {
    background: var(--moss);
    color: white;
    border: none;
    width: 36px; height: 36px;
    border-radius: 50%;
    font-size: 1.1rem;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s;
    flex-shrink: 0;
  }
  .add-cart-btn:hover { background: var(--soil); transform: scale(1.1); }

  .product-rating {
    display: flex;
    align-items: center;
    gap: 0.3rem;
    font-size: 0.75rem;
    color: var(--harvest);
    margin-bottom: 0.75rem;
  }
  .rating-count { color: var(--muted); }

  /* ─── FARMER SECTION ─── */
  .farmers-section {
    background: var(--soil);
    color: white;
  }

  .farmers-section .section-tag { color: var(--wheat); }
  .farmers-section .section-title { color: white; }
  .farmers-section .section-sub { color: rgba(255,255,255,0.65); }

  .farmers-layout {
    display: grid;
    grid-template-columns: 1fr 1.6fr;
    gap: 4rem;
    align-items: center;
  }

  .farmer-cards-scroll {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .farmer-profile-card {
    background: rgba(255,255,255,0.07);
    border: 1px solid rgba(255,255,255,0.12);
    border-radius: 16px;
    padding: 1.25rem 1.5rem;
    display: flex;
    align-items: center;
    gap: 1.25rem;
    transition: background 0.2s;
    cursor: pointer;
  }
  .farmer-profile-card:hover { background: rgba(255,255,255,0.12); }

  .farmer-big-avatar {
    width: 52px; height: 52px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.5rem;
    flex-shrink: 0;
  }

  .farmer-info { flex: 1; }

  .farmer-card-name {
    font-weight: 600;
    font-size: 0.95rem;
    color: white;
    margin-bottom: 0.2rem;
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }

  .verified-badge {
    background: var(--sprout);
    color: var(--moss);
    font-size: 0.6rem;
    font-weight: 700;
    padding: 0.15rem 0.45rem;
    border-radius: 4px;
    letter-spacing: 0.03em;
    text-transform: uppercase;
  }

  .farmer-card-loc {
    font-size: 0.78rem;
    color: rgba(255,255,255,0.5);
    margin-bottom: 0.5rem;
  }

  .farmer-card-tags {
    display: flex;
    gap: 0.4rem;
    flex-wrap: wrap;
  }

  .farmer-tag {
    background: rgba(255,255,255,0.1);
    color: var(--wheat);
    font-size: 0.65rem;
    padding: 0.2rem 0.55rem;
    border-radius: 6px;
    font-weight: 500;
  }

  .farmer-earnings {
    text-align: right;
  }

  .farmer-sales {
    font-family: 'DM Mono', monospace;
    font-size: 1rem;
    font-weight: 700;
    color: var(--harvest);
    margin-bottom: 0.15rem;
  }

  .farmer-sales-label {
    font-size: 0.68rem;
    color: rgba(255,255,255,0.45);
    letter-spacing: 0.03em;
  }

  .farmers-cta-box {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 20px;
    padding: 2.5rem;
    margin-top: 1.5rem;
  }

  .benefit-list {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    margin: 1.5rem 0 2rem;
  }

  .benefit-item {
    display: flex;
    align-items: flex-start;
    gap: 0.75rem;
    font-size: 0.9rem;
    color: rgba(255,255,255,0.8);
    line-height: 1.5;
  }

  .benefit-check {
    width: 22px; height: 22px;
    background: var(--moss);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.7rem;
    flex-shrink: 0;
    margin-top: 0.1rem;
  }

  /* ─── SAVINGS BANNER ─── */
  .savings-section {
    background: var(--harvest);
    padding: 4rem 5rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 2rem;
    flex-wrap: wrap;
  }

  .savings-left h2 {
    font-family: 'Playfair Display', serif;
    font-size: 2.5rem;
    font-weight: 900;
    color: var(--soil);
    margin-bottom: 0.5rem;
  }

  .savings-left p { color: var(--bark); font-size: 1.05rem; }

  .savings-pills {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
  }

  .saving-pill {
    background: white;
    border-radius: 16px;
    padding: 1.25rem 1.75rem;
    text-align: center;
    min-width: 130px;
  }

  .saving-pill-num {
    font-family: 'Playfair Display', serif;
    font-size: 2rem;
    font-weight: 900;
    color: var(--moss);
    display: block;
  }

  .saving-pill-label {
    font-size: 0.78rem;
    color: var(--muted);
    font-weight: 500;
    text-align: center;
  }

  /* ─── TESTIMONIALS ─── */
  .testimonials-section { background: var(--offwhite); }

  .testimonials-header { text-align: center; margin-bottom: 3rem; }
  .testimonials-header .section-tag { justify-content: center; }

  .testimonials-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.5rem;
  }

  .testimonial-card {
    background: white;
    border-radius: 20px;
    padding: 1.75rem;
    border: 1px solid var(--border);
    transition: transform 0.3s;
  }
  .testimonial-card:hover { transform: translateY(-4px); }

  .testimonial-stars { font-size: 0.9rem; color: var(--harvest); margin-bottom: 1rem; }

  .testimonial-text {
    font-size: 0.95rem;
    color: var(--text);
    line-height: 1.7;
    margin-bottom: 1.5rem;
    font-style: italic;
  }

  .testimonial-author {
    display: flex;
    align-items: center;
    gap: 0.75rem;
  }

  .author-avatar {
    width: 40px; height: 40px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.2rem;
  }

  .author-name {
    font-weight: 700;
    font-size: 0.9rem;
    margin-bottom: 0.1rem;
  }

  .author-role { font-size: 0.75rem; color: var(--muted); }

  /* ─── NEWSLETTER ─── */
  .newsletter-section {
    background: var(--moss);
    color: white;
    text-align: center;
    padding: 5rem;
  }

  .newsletter-section .section-title { color: white; font-size: 2.5rem; }
  .newsletter-section .section-sub { color: rgba(255,255,255,0.7); margin: 0 auto 2rem; }

  .newsletter-form {
    display: flex;
    gap: 0.75rem;
    max-width: 480px;
    margin: 0 auto;
    flex-wrap: wrap;
    justify-content: center;
  }

  .newsletter-input {
    flex: 1;
    min-width: 240px;
    padding: 0.85rem 1.25rem;
    border-radius: 100px;
    border: none;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.9rem;
    outline: none;
    background: rgba(255,255,255,0.15);
    color: white;
    border: 1.5px solid rgba(255,255,255,0.2);
    transition: border-color 0.2s;
  }
  .newsletter-input::placeholder { color: rgba(255,255,255,0.5); }
  .newsletter-input:focus { border-color: var(--wheat); }

  /* ─── FOOTER ─── */
  footer {
    background: var(--soil);
    color: rgba(255,255,255,0.7);
    padding: 4rem 5rem 2rem;
  }

  .footer-grid {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr;
    gap: 3rem;
    margin-bottom: 3rem;
  }

  .footer-logo {
    font-family: 'Playfair Display', serif;
    font-weight: 900;
    font-size: 1.6rem;
    color: white;
    margin-bottom: 0.75rem;
  }

  .footer-logo span { color: var(--harvest); }

  .footer-desc {
    font-size: 0.88rem;
    line-height: 1.7;
    max-width: 280px;
  }

  .footer-col h4 {
    font-size: 0.85rem;
    font-weight: 700;
    color: white;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 1.25rem;
  }

  .footer-col ul { list-style: none; display: flex; flex-direction: column; gap: 0.75rem; }

  .footer-col a {
    color: rgba(255,255,255,0.6);
    text-decoration: none;
    font-size: 0.88rem;
    transition: color 0.2s;
  }
  .footer-col a:hover { color: var(--wheat); }

  .footer-bottom {
    border-top: 1px solid rgba(255,255,255,0.1);
    padding-top: 1.5rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
    font-size: 0.8rem;
    color: rgba(255,255,255,0.4);
  }

  .footer-socials { display: flex; gap: 0.75rem; }

  .social-btn {
    width: 34px; height: 34px;
    border-radius: 50%;
    background: rgba(255,255,255,0.08);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.85rem;
    cursor: pointer;
    transition: background 0.2s;
    text-decoration: none;
    color: rgba(255,255,255,0.7);
  }
  .social-btn:hover { background: var(--moss); }

  /* ─── CART SIDEBAR ─── */
  .cart-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.5);
    z-index: 1100;
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s;
  }
  .cart-overlay.open { opacity: 1; visibility: visible; }

  .cart-sidebar {
    position: fixed;
    top: 0; right: 0;
    height: 100vh;
    width: 420px;
    max-width: 95vw;
    background: var(--cream);
    z-index: 1200;
    transform: translateX(100%);
    transition: transform 0.35s cubic-bezier(0.4,0,0.2,1);
    display: flex;
    flex-direction: column;
  }
  .cart-sidebar.open { transform: translateX(0); }

  .cart-header {
    padding: 1.5rem;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .cart-header h2 {
    font-family: 'Playfair Display', serif;
    font-size: 1.3rem;
    font-weight: 700;
  }

  .close-btn {
    background: none;
    border: none;
    font-size: 1.4rem;
    cursor: pointer;
    color: var(--muted);
    transition: color 0.2s;
  }
  .close-btn:hover { color: var(--text); }

  .cart-items {
    flex: 1;
    overflow-y: auto;
    padding: 1.25rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .cart-empty {
    text-align: center;
    padding: 3rem 1.5rem;
    color: var(--muted);
  }

  .cart-empty-icon { font-size: 3.5rem; margin-bottom: 1rem; display: block; }

  .cart-item {
    background: white;
    border-radius: 14px;
    padding: 1rem;
    border: 1px solid var(--border);
    display: flex;
    gap: 0.875rem;
    align-items: center;
  }

  .cart-item-emoji {
    width: 56px; height: 56px;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    background: var(--offwhite);
    flex-shrink: 0;
  }

  .cart-item-info { flex: 1; min-width: 0; }

  .cart-item-name {
    font-weight: 600;
    font-size: 0.9rem;
    margin-bottom: 0.2rem;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .cart-item-price {
    font-family: 'DM Mono', monospace;
    font-size: 0.85rem;
    color: var(--moss);
    font-weight: 700;
  }

  .qty-controls {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .qty-btn {
    width: 28px; height: 28px;
    border-radius: 50%;
    border: 1.5px solid var(--border);
    background: white;
    cursor: pointer;
    font-size: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.2s;
    line-height: 1;
    color: var(--text);
  }
  .qty-btn:hover { background: var(--moss); border-color: var(--moss); color: white; }

  .qty-num {
    font-family: 'DM Mono', monospace;
    font-weight: 700;
    font-size: 0.9rem;
    min-width: 20px;
    text-align: center;
  }

  .remove-btn {
    background: none;
    border: none;
    font-size: 0.9rem;
    cursor: pointer;
    color: var(--muted);
    padding: 0.25rem;
    transition: color 0.2s;
  }
  .remove-btn:hover { color: var(--terracotta); }

  .cart-footer {
    border-top: 1px solid var(--border);
    padding: 1.5rem;
  }

  .cart-total-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 0.5rem;
  }

  .cart-total-label { font-size: 0.85rem; color: var(--muted); }
  .cart-total-val { font-family: 'DM Mono', monospace; font-size: 0.9rem; font-weight: 600; }
  .cart-total-val.grand { font-size: 1.3rem; color: var(--moss); }

  .cart-total-row.grand .cart-total-label {
    font-weight: 700;
    font-size: 1rem;
    color: var(--text);
  }

  .checkout-btn {
    width: 100%;
    padding: 1rem;
    background: var(--moss);
    color: white;
    border: none;
    border-radius: 100px;
    font-family: 'DM Sans', sans-serif;
    font-size: 1rem;
    font-weight: 700;
    cursor: pointer;
    margin-top: 1.25rem;
    transition: all 0.2s;
    letter-spacing: 0.02em;
  }
  .checkout-btn:hover { background: var(--soil); transform: translateY(-1px); }

  .cart-savings {
    background: var(--sprout);
    border-radius: 10px;
    padding: 0.6rem 0.9rem;
    font-size: 0.82rem;
    color: var(--moss);
    font-weight: 600;
    text-align: center;
    margin-top: 0.75rem;
  }

  /* ─── TOAST ─── */
  .toast {
    position: fixed;
    bottom: 2rem;
    left: 50%;
    transform: translateX(-50%) translateY(100px);
    background: var(--soil);
    color: white;
    padding: 0.85rem 1.5rem;
    border-radius: 100px;
    font-size: 0.9rem;
    font-weight: 500;
    z-index: 2000;
    transition: transform 0.35s cubic-bezier(0.4,0,0.2,1);
    pointer-events: none;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    box-shadow: 0 8px 24px rgba(0,0,0,0.3);
  }
  .toast.show { transform: translateX(-50%) translateY(0); }

  /* ─── MODAL ─── */
  .modal-overlay {
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.6);
    z-index: 1500;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 1rem;
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s;
  }
  .modal-overlay.open { opacity: 1; visibility: visible; }

  .modal-box {
    background: var(--cream);
    border-radius: 24px;
    width: 100%;
    max-width: 520px;
    max-height: 90vh;
    overflow-y: auto;
    padding: 2.5rem;
    transform: scale(0.9);
    transition: transform 0.3s;
    position: relative;
  }
  .modal-overlay.open .modal-box { transform: scale(1); }

  .modal-close {
    position: absolute;
    top: 1.25rem; right: 1.25rem;
    background: var(--offwhite);
    border: none;
    width: 36px; height: 36px;
    border-radius: 50%;
    cursor: pointer;
    font-size: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: background 0.2s;
  }
  .modal-close:hover { background: var(--border); }

  .modal-emoji {
    font-size: 4rem;
    margin-bottom: 1rem;
    display: block;
    text-align: center;
  }

  .modal-product-name {
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem;
    font-weight: 800;
    text-align: center;
    margin-bottom: 0.5rem;
  }

  .modal-farmer-info {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    margin-bottom: 1.5rem;
    font-size: 0.85rem;
    color: var(--muted);
  }

  .modal-desc {
    font-size: 0.95rem;
    color: var(--muted);
    line-height: 1.7;
    margin-bottom: 1.5rem;
    text-align: center;
  }

  .modal-price-row {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    margin-bottom: 1.5rem;
  }

  .modal-price-current {
    font-family: 'Playfair Display', serif;
    font-size: 2rem;
    font-weight: 900;
    color: var(--moss);
  }

  .modal-price-mrp {
    font-size: 1.1rem;
    color: var(--muted);
    text-decoration: line-through;
  }

  .modal-price-save {
    background: var(--sprout);
    color: var(--moss);
    font-size: 0.8rem;
    font-weight: 700;
    padding: 0.3rem 0.7rem;
    border-radius: 8px;
  }

  .modal-add-btn {
    width: 100%;
    padding: 1rem;
    background: var(--moss);
    color: white;
    border: none;
    border-radius: 100px;
    font-family: 'DM Sans', sans-serif;
    font-size: 1rem;
    font-weight: 700;
    cursor: pointer;
    transition: all 0.2s;
  }
  .modal-add-btn:hover { background: var(--soil); }

  /* ─── SELLER MODAL ─── */
  .sell-form {
    display: flex;
    flex-direction: column;
    gap: 1.1rem;
  }

  .form-group { display: flex; flex-direction: column; gap: 0.4rem; }

  .form-label {
    font-size: 0.82rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--muted);
  }

  .form-input, .form-select, .form-textarea {
    padding: 0.75rem 1rem;
    border: 1.5px solid var(--border);
    border-radius: 12px;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.9rem;
    background: white;
    color: var(--text);
    outline: none;
    transition: border-color 0.2s;
  }
  .form-input:focus, .form-select:focus, .form-textarea:focus { border-color: var(--moss); }

  .form-textarea { resize: vertical; min-height: 90px; }

  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; }

  /* ─── ANIMATIONS ─── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  /* ─── SCROLLBAR ─── */
  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: var(--offwhite); }
  ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }
  ::-webkit-scrollbar-thumb:hover { background: var(--muted); }

  /* ─── RESPONSIVE ─── */
  @media (max-width: 1024px) {
    .hero { grid-template-columns: 1fr; }
    .hero-right { display: none; }
    section { padding: 4rem 2.5rem; }
    .savings-section { padding: 3rem 2.5rem; }
    footer { padding: 3rem 2.5rem 2rem; }
    .footer-grid { grid-template-columns: 1fr 1fr; }
    .how-grid { grid-template-columns: repeat(2, 1fr); }
    .how-grid::before { display: none; }
    .farmers-layout { grid-template-columns: 1fr; }
    .testimonials-grid { grid-template-columns: 1fr 1fr; }
  }

  @media (max-width: 640px) {
    .nav-links { display: none; }
    .hero-left { padding: 3rem 1.5rem; }
    section { padding: 3rem 1.5rem; }
    .savings-section { padding: 2.5rem 1.5rem; }
    footer { padding: 2.5rem 1.5rem 1.5rem; }
    .footer-grid { grid-template-columns: 1fr; }
    .how-grid { grid-template-columns: 1fr; }
    .testimonials-grid { grid-template-columns: 1fr; }
    .products-grid { grid-template-columns: 1fr 1fr; }
    .savings-pills { justify-content: center; }
    .newsletter-section { padding: 3.5rem 1.5rem; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-logo" onclick="scrollToTop()">🌾 Farm<span>Link</span></div>
  <ul class="nav-links">
    <li><a href="#products">Shop</a></li>
    <li><a href="#how">How It Works</a></li>
    <li><a href="#farmers">Our Farmers</a></li>
    <li><a href="#testimonials">Reviews</a></li>
  </ul>
  <div class="nav-actions">
    <button class="btn btn-ghost" onclick="openSellModal()">Sell Your Produce</button>
    <button class="cart-btn" onclick="toggleCart()">
      🛒
      <span class="cart-badge" id="cartBadge">0</span>
    </button>
  </div>
</nav>

<!-- HERO -->
<section class="hero" id="top">
  <div class="hero-left">
    <div class="hero-eyebrow">🌱 Zero Middlemen, 100% Fresh</div>
    <h1 class="hero-title">
      Farm Fresh,<br>
      <em>Direct to</em><br>
      Your Door
    </h1>
    <p class="hero-desc">
      FarmLink connects farmers directly with consumers. Farmers earn <strong>40% more</strong>. You pay <strong>30% less</strong>. No warehouses, no brokers — just pure, traceable goodness from field to fork.
    </p>
    <div class="hero-cta">
      <button class="btn btn-primary" onclick="document.getElementById('products').scrollIntoView({behavior:'smooth'})">Shop the Harvest</button>
      <button class="btn btn-ghost" onclick="openSellModal()">Become a Seller</button>
    </div>
    <div class="hero-stats">
      <div class="stat-item">
        <div class="stat-num">2,400+</div>
        <div class="stat-label">Active Farmers</div>
      </div>
      <div class="stat-item">
        <div class="stat-num">₹0</div>
        <div class="stat-label">Commission Charged</div>
      </div>
      <div class="stat-item">
        <div class="stat-num">48hr</div>
        <div class="stat-label">Farm to Doorstep</div>
      </div>
    </div>
  </div>
  <div class="hero-right">
    <div class="hero-right-inner">
      <div class="hero-image-grid">
        <div class="hero-img-card tall card-green">
          <div class="hero-img-emoji">🥬</div>
          <span class="hero-img-label">Spinach</span>
          <span class="hero-img-price">₹28/bunch</span>
        </div>
        <div class="hero-img-card card-orange">
          <div class="hero-img-emoji">🍅</div>
          <span class="hero-img-label">Tomatoes</span>
          <span class="hero-img-price">₹24/kg</span>
        </div>
        <div class="hero-img-card card-yellow">
          <div class="hero-img-emoji">🥕</div>
          <span class="hero-img-label">Carrots</span>
          <span class="hero-img-price">₹35/kg</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-strip">
  <div class="marquee-inner" id="marqueeInner">
    <span class="marquee-item"><span class="marquee-dot"></span> 100% Organic Options</span>
    <span class="marquee-item"><span class="marquee-dot"></span> Direct from 2,400+ Farms</span>
    <span class="marquee-item"><span class="marquee-dot"></span> No Hidden Charges</span>
    <span class="marquee-item"><span class="marquee-dot"></span> Farmer gets 90% Revenue</span>
    <span class="marquee-item"><span class="marquee-dot"></span> 48hr Fresh Delivery</span>
    <span class="marquee-item"><span class="marquee-dot"></span> Traceable Farm-to-Fork</span>
    <span class="marquee-item"><span class="marquee-dot"></span> Seasonal & Local Produce</span>
    <span class="marquee-item"><span class="marquee-dot"></span> Supporting Rural India</span>
    <span class="marquee-item"><span class="marquee-dot"></span> 100% Organic Options</span>
    <span class="marquee-item"><span class="marquee-dot"></span> Direct from 2,400+ Farms</span>
    <span class="marquee-item"><span class="marquee-dot"></span> No Hidden Charges</span>
    <span class="marquee-item"><span class="marquee-dot"></span> Farmer gets 90% Revenue</span>
    <span class="marquee-item"><span class="marquee-dot"></span> 48hr Fresh Delivery</span>
    <span class="marquee-item"><span class="marquee-dot"></span> Traceable Farm-to-Fork</span>
    <span class="marquee-item"><span class="marquee-dot"></span> Seasonal & Local Produce</span>
    <span class="marquee-item"><span class="marquee-dot"></span> Supporting Rural India</span>
  </div>
</div>

<!-- HOW IT WORKS -->
<section class="how-section" id="how">
  <div class="how-header">
    <div class="section-tag">How It Works</div>
    <h2 class="section-title">Simple, Fair & Transparent</h2>
    <p class="section-sub">A two-sided marketplace built on trust — every rupee is accounted for, every crop is traceable.</p>
  </div>
  <div class="how-grid">
    <div class="how-card">
      <div class="how-icon">🧑‍🌾<span class="how-step">1</span></div>
      <h3>Farmer Lists Produce</h3>
      <p>Farmers register, get verified, and list fresh produce with pricing, quantity, and harvest date.</p>
    </div>
    <div class="how-card">
      <div class="how-icon">🛒<span class="how-step">2</span></div>
      <h3>Customer Orders</h3>
      <p>Buyers browse verified listings, compare prices, and order directly — no broker involved at any step.</p>
    </div>
    <div class="how-card">
      <div class="how-icon">🚜<span class="how-step">3</span></div>
      <h3>Farm-Fresh Dispatch</h3>
      <p>Produce is packed same-day on the farm and dispatched via our cold-chain partner network.</p>
    </div>
    <div class="how-card">
      <div class="how-icon">💸<span class="how-step">4</span></div>
      <h3>Farmer Gets Paid</h3>
      <p>90% of the order value goes directly to the farmer within 24 hours of delivery confirmation.</p>
    </div>
  </div>
</section>

<!-- PRODUCTS -->
<section id="products">
  <div class="products-header">
    <div>
      <div class="section-tag">Today's Market</div>
      <h2 class="section-title">Fresh from the Field</h2>
    </div>
    <button class="btn btn-ghost" onclick="showAllProducts()">View All →</button>
  </div>
  <div class="category-tabs" id="categoryTabs"></div>
  <div class="products-grid" id="productsGrid"></div>
</section>

<!-- SAVINGS BANNER -->
<section class="savings-section">
  <div class="savings-left">
    <h2>You Save. They Earn.</h2>
    <p>The numbers that make FarmLink different from every other grocery app.</p>
  </div>
  <div class="savings-pills">
    <div class="saving-pill">
      <span class="saving-pill-num">40%</span>
      <span class="saving-pill-label">More Farmer Income</span>
    </div>
    <div class="saving-pill">
      <span class="saving-pill-num">30%</span>
      <span class="saving-pill-label">Customer Savings</span>
    </div>
    <div class="saving-pill">
      <span class="saving-pill-num">90%</span>
      <span class="saving-pill-label">Revenue to Farmer</span>
    </div>
    <div class="saving-pill">
      <span class="saving-pill-num">₹0</span>
      <span class="saving-pill-label">Middlemen Cut</span>
    </div>
  </div>
</section>

<!-- FARMERS -->
<section class="farmers-section" id="farmers">
  <div class="farmers-layout">
    <div>
      <div class="section-tag">Our Community</div>
      <h2 class="section-title">Meet the Farmers Behind Every Bite</h2>
      <p class="section-sub">Real people. Real farms. Every product you buy supports a family, a village, and a sustainable future.</p>
      <div class="farmers-cta-box">
        <h3 style="color:white;font-family:'Playfair Display',serif;font-size:1.25rem;margin-bottom:1rem;">Why Sell on FarmLink?</h3>
        <ul class="benefit-list">
          <li class="benefit-item"><span class="benefit-check">✓</span> Keep 90% of every sale — no broker, no commission</li>
          <li class="benefit-item"><span class="benefit-check">✓</span> Get paid within 24 hours of delivery confirmation</li>
          <li class="benefit-item"><span class="benefit-check">✓</span> Reach thousands of buyers across your state</li>
          <li class="benefit-item"><span class="benefit-check">✓</span> Free listing, free farmer account, always</li>
          <li class="benefit-item"><span class="benefit-check">✓</span> Logistics support with our cold-chain partners</li>
        </ul>
        <button class="btn btn-harvest" style="width:100%;padding:0.85rem;font-size:1rem;" onclick="openSellModal()">Register as a Farmer →</button>
      </div>
    </div>
    <div class="farmer-cards-scroll" id="farmerCards"></div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials-section" id="testimonials">
  <div class="testimonials-header">
    <div class="section-tag">Real Stories</div>
    <h2 class="section-title">What People Are Saying</h2>
  </div>
  <div class="testimonials-grid" id="testimonialsGrid"></div>
</section>

<!-- NEWSLETTER -->
<section class="newsletter-section">
  <div class="section-tag" style="color:var(--wheat);justify-content:center;display:flex">Stay Connected</div>
  <h2 class="section-title">Get Seasonal Deals &<br>Fresh Arrivals</h2>
  <p class="section-sub">Weekly updates on what's freshly harvested, exclusive farmer stories, and early-access deals.</p>
  <div class="newsletter-form">
    <input class="newsletter-input" type="email" placeholder="your@email.com" id="newsletterEmail">
    <button class="btn btn-harvest" style="padding:0.85rem 1.75rem;font-size:0.95rem;" onclick="subscribeNewsletter()">Subscribe</button>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-grid">
    <div>
      <div class="footer-logo">🌾 Farm<span>Link</span></div>
      <p class="footer-desc">India's first zero-commission farm-to-consumer marketplace. Built to empower farmers and feed families better.</p>
    </div>
    <div class="footer-col">
      <h4>Marketplace</h4>
      <ul>
        <li><a href="#">Fresh Vegetables</a></li>
        <li><a href="#">Seasonal Fruits</a></li>
        <li><a href="#">Grains & Pulses</a></li>
        <li><a href="#">Dairy & Eggs</a></li>
        <li><a href="#">Organic Range</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h4>Farmers</h4>
      <ul>
        <li><a href="#" onclick="openSellModal();return false;">Sell on FarmLink</a></li>
        <li><a href="#">Farmer Dashboard</a></li>
        <li><a href="#">Pricing Policy</a></li>
        <li><a href="#">Logistics Partner</a></li>
        <li><a href="#">Farmer Stories</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h4>Company</h4>
      <ul>
        <li><a href="#">About Us</a></li>
        <li><a href="#">Our Mission</a></li>
        <li><a href="#">Press</a></li>
        <li><a href="#">Careers</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <span>© 2025 FarmLink. Built with ❤️ for India's Farmers.</span>
    <div class="footer-socials">
      <a class="social-btn" href="#">𝕏</a>
      <a class="social-btn" href="#">in</a>
      <a class="social-btn" href="#">📘</a>
      <a class="social-btn" href="#">📷</a>
    </div>
  </div>
</footer>

<!-- CART SIDEBAR -->
<div class="cart-overlay" id="cartOverlay" onclick="toggleCart()"></div>
<div class="cart-sidebar" id="cartSidebar">
  <div class="cart-header">
    <h2>🛒 Your Cart</h2>
    <button class="close-btn" onclick="toggleCart()">✕</button>
  </div>
  <div class="cart-items" id="cartItems">
    <div class="cart-empty">
      <span class="cart-empty-icon">🧺</span>
      <p style="font-weight:600;margin-bottom:0.5rem;">Your basket is empty</p>
      <p style="font-size:0.85rem;">Add some fresh produce to get started!</p>
    </div>
  </div>
  <div class="cart-footer" id="cartFooter" style="display:none">
    <div class="cart-total-row">
      <span class="cart-total-label">Subtotal</span>
      <span class="cart-total-val" id="cartSubtotal">₹0</span>
    </div>
    <div class="cart-total-row">
      <span class="cart-total-label">Delivery</span>
      <span class="cart-total-val" style="color:var(--moss);font-weight:700;">FREE</span>
    </div>
    <div class="cart-total-row grand">
      <span class="cart-total-label">Total</span>
      <span class="cart-total-val grand" id="cartTotal">₹0</span>
    </div>
    <div class="cart-savings" id="cartSavingsMsg">You saved ₹0 vs retail prices 🎉</div>
    <button class="checkout-btn" onclick="checkout()">Proceed to Checkout →</button>
  </div>
</div>

<!-- PRODUCT MODAL -->
<div class="modal-overlay" id="productModal" onclick="closeModal(event)">
  <div class="modal-box" id="modalBox">
    <button class="modal-close" onclick="closeProductModal()">✕</button>
    <span class="modal-emoji" id="modalEmoji"></span>
    <h2 class="modal-product-name" id="modalName"></h2>
    <div class="modal-farmer-info" id="modalFarmer"></div>
    <p class="modal-desc" id="modalDesc"></p>
    <div class="modal-price-row" id="modalPriceRow"></div>
    <button class="modal-add-btn" id="modalAddBtn">Add to Cart</button>
  </div>
</div>

<!-- SELL MODAL -->
<div class="modal-overlay" id="sellModal" onclick="closeSellModal(event)">
  <div class="modal-box">
    <button class="modal-close" onclick="document.getElementById('sellModal').classList.remove('open')">✕</button>
    <h2 style="font-family:'Playfair Display',serif;font-size:1.8rem;font-weight:800;margin-bottom:0.3rem;">Become a Seller 🌾</h2>
    <p style="color:var(--muted);font-size:0.9rem;margin-bottom:1.5rem;">Join 2,400+ farmers earning directly. Free to list, always.</p>
    <div class="sell-form" id="sellForm">
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Full Name</label>
          <input class="form-input" type="text" placeholder="Ramesh Kumar" id="sellerName">
        </div>
        <div class="form-group">
          <label class="form-label">Phone Number</label>
          <input class="form-input" type="tel" placeholder="+91 98765 43210" id="sellerPhone">
        </div>
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Village / Town</label>
          <input class="form-input" type="text" placeholder="Sikar, Rajasthan" id="sellerVillage">
        </div>
        <div class="form-group">
          <label class="form-label">State</label>
          <select class="form-select" id="sellerState">
            <option value="">Select State</option>
            <option>Rajasthan</option><option>Uttar Pradesh</option><option>Punjab</option>
            <option>Haryana</option><option>Maharashtra</option><option>Gujarat</option>
            <option>Karnataka</option><option>Andhra Pradesh</option><option>Tamil Nadu</option>
            <option>Madhya Pradesh</option><option>Bihar</option><option>Odisha</option>
          </select>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">What do you grow?</label>
        <input class="form-input" type="text" placeholder="Tomatoes, Wheat, Onions..." id="sellerCrops">
      </div>
      <div class="form-row">
        <div class="form-group">
          <label class="form-label">Farm Size (acres)</label>
          <input class="form-input" type="number" placeholder="5" id="sellerAcres">
        </div>
        <div class="form-group">
          <label class="form-label">Category</label>
          <select class="form-select" id="sellerCategory">
            <option value="">Select</option>
            <option>Vegetables</option><option>Fruits</option><option>Grains & Pulses</option>
            <option>Dairy & Eggs</option><option>Spices & Herbs</option><option>Organic</option>
          </select>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Brief Description</label>
        <textarea class="form-textarea" placeholder="Tell buyers about your farm, farming practices, and what makes your produce special..." id="sellerDesc"></textarea>
      </div>
      <button class="btn btn-primary" style="padding:0.9rem;font-size:0.95rem;border-radius:12px;" onclick="submitSeller()">Submit Application →</button>
    </div>
    <div id="sellerSuccess" style="display:none;text-align:center;padding:2rem 0;">
      <div style="font-size:3.5rem;margin-bottom:1rem;">🎉</div>
      <h3 style="font-family:'Playfair Display',serif;font-size:1.5rem;margin-bottom:0.5rem;">Application Received!</h3>
      <p style="color:var(--muted);font-size:0.9rem;line-height:1.6;">We'll verify your details and contact you within 48 hours. Welcome to the FarmLink family!</p>
    </div>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast">
  <span id="toastIcon">✓</span>
  <span id="toastMsg">Added to cart!</span>
</div>

<script>
// ─── DATA ───
const products = [
  { id:1, name:"Organic Tomatoes", emoji:"🍅", farmer:"Suresh Patel", location:"Nashik, MH", price:24, mrp:38, unit:"kg", category:"Vegetables", badge:"Organic", bgColor:"card-orange", desc:"Sun-ripened, pesticide-free tomatoes from the volcanic soil of Nashik. Naturally sweet and rich in lycopene. Harvested this morning.", rating:4.8, reviews:142 },
  { id:2, name:"Fresh Spinach", emoji:"🥬", farmer:"Kamla Devi", location:"Sikar, RJ", price:28, mrp:45, unit:"bunch", category:"Vegetables", badge:"Fresh", bgColor:"card-green", desc:"Tender, crispy spinach grown with natural compost. Rich in iron and folate. Picked at peak freshness within the last 12 hours.", rating:4.9, reviews:89 },
  { id:3, name:"Purple Brinjal", emoji:"🍆", farmer:"Arjun Singh", location:"Lucknow, UP", price:32, mrp:55, unit:"kg", category:"Vegetables", badge:"Fresh", bgColor:"", desc:"Premium-grade brinjal with a firm texture and deep flavor. Perfect for curries, bharta, and grilling. Grown using traditional methods.", rating:4.6, reviews:67 },
  { id:4, name:"Alphonso Mangoes", emoji:"🥭", farmer:"Rajiv Sawant", location:"Ratnagiri, MH", price:320, mrp:520, unit:"dozen", category:"Fruits", badge:"Seasonal", bgColor:"card-yellow", desc:"Genuine GI-tagged Hapus Alphonso. No carbide ripening, no artificial color. Sweet, saffron-colored flesh that melts on the tongue.", rating:5.0, reviews:234 },
  { id:5, name:"Baby Carrots", emoji:"🥕", farmer:"Gurpreet Kaur", location:"Amritsar, PB", price:35, mrp:58, unit:"kg", category:"Vegetables", badge:"Organic", bgColor:"card-orange", desc:"Tender baby carrots harvested early for maximum sweetness. Great for salads, juicing, and healthy snacking. Organically certified.", rating:4.7, reviews:103 },
  { id:6, name:"Green Peas", emoji:"🫛", farmer:"Mohan Lal", location:"Meerut, UP", price:55, mrp:85, unit:"kg", category:"Vegetables", badge:"Fresh", bgColor:"card-green", desc:"Sweet, plump green peas freshly shelled. Bursting with natural sweetness. Best consumed within 2 days for peak flavor.", rating:4.8, reviews:78 },
  { id:7, name:"Basmati Rice", emoji:"🌾", farmer:"Hardev Singh", location:"Karnal, HR", price:85, mrp:135, unit:"kg", category:"Grains", badge:"Premium", bgColor:"card-yellow", desc:"Aged Pusa Basmati from the IGP-protected Karnal belt. Long, aromatic grains that double in length on cooking. 18-month aged stock.", rating:4.9, reviews:312 },
  { id:8, name:"Farm Eggs", emoji:"🥚", farmer:"Lakshmi Bai", location:"Coimbatore, TN", price:72, mrp:110, unit:"dozen", category:"Dairy & Eggs", badge:"Free Range", bgColor:"card-orange", desc:"Free-range country hen eggs. Deep orange yolks, firm whites. Hens are fed naturally with no hormones or antibiotics ever.", rating:4.9, reviews:189 },
  { id:9, name:"Pink Guava", emoji:"🍈", farmer:"Santosh Yadav", location:"Allahabad, UP", price:45, mrp:72, unit:"kg", category:"Fruits", badge:"Seasonal", bgColor:"", desc:"Sweet, pink-fleshed Allahabad Safeda guava. High in Vitamin C. Naturally ripened on the tree, no ethylene treatment.", rating:4.7, reviews:56 },
  { id:10, name:"Masoor Dal", emoji:"🫘", farmer:"Prem Kumar", location:"Indore, MP", price:95, mrp:148, unit:"kg", category:"Grains", badge:"Organic", bgColor:"card-green", desc:"Red split lentils grown without synthetic fertilizers in Malwa's fertile black soil. High protein, quick cooking, rich earthy flavor.", rating:4.8, reviews:94 },
  { id:11, name:"Banana Cluster", emoji:"🍌", farmer:"Velu Murugan", location:"Trichy, TN", price:38, mrp:62, unit:"dozen", category:"Fruits", badge:"Fresh", bgColor:"card-yellow", desc:"Robusta bananas harvested at the right ripeness. Naturally sweet, no chemicals. Great for daily nutrition and kids' snacks.", rating:4.6, reviews:71 },
  { id:12, name:"Turmeric Root", emoji:"🟡", farmer:"Anita Patil", location:"Sangli, MH", price:120, mrp:200, unit:"kg", category:"Spices", badge:"Organic", bgColor:"card-orange", desc:"Organic raw turmeric with 4.5%+ curcumin content. Naturally dried and polished. Far superior to powdered alternatives in potency.", rating:4.9, reviews:167 },
];

const farmers = [
  { name:"Suresh Patel", emoji:"👨‍🌾", location:"Nashik, Maharashtra", tags:["Tomatoes","Onions","Grapes"], sales:"₹1,24,000", bg:"card-green" },
  { name:"Kamla Devi", emoji:"👩‍🌾", location:"Sikar, Rajasthan", tags:["Spinach","Fenugreek","Coriander"], sales:"₹68,500", bg:"card-yellow" },
  { name:"Gurpreet Kaur", emoji:"👩‍🌾", location:"Amritsar, Punjab", tags:["Carrots","Potatoes","Wheat"], sales:"₹2,10,000", bg:"card-blue" },
  { name:"Hardev Singh", emoji:"👨‍🌾", location:"Karnal, Haryana", tags:["Basmati","Wheat","Maize"], sales:"₹3,85,000", bg:"card-orange" },
  { name:"Velu Murugan", emoji:"👨‍🌾", location:"Trichy, Tamil Nadu", tags:["Bananas","Coconuts","Jackfruit"], sales:"₹92,300", bg:"card-green" },
];

const testimonials = [
  { text:"I used to sell my tomatoes to a mandi agent for ₹12/kg. On FarmLink I get ₹22-24. My income doubled in one season. My children can now go to a better school.", author:"Suresh Patel", role:"Tomato Farmer, Nashik", emoji:"👨‍🌾", stars:5 },
  { text:"The quality is unbelievable. I got spinach that was clearly picked the same morning — still had dew on it. And the price was ₹28 vs ₹50 in my local store. Never going back.", author:"Priya Nair", role:"Customer, Pune", emoji:"👩", stars:5 },
  { text:"As a mother of two, I care deeply about what my family eats. Knowing exactly which farm my vegetables come from, and that no brokers touched them, gives me real peace of mind.", author:"Anita Sharma", role:"Customer, Delhi", emoji:"👩‍👧", stars:5 },
  { text:"The platform is so simple even I could list my produce without any tech help. The payment came to my account the very next morning. I told every farmer in my village about FarmLink.", author:"Mohan Lal", role:"Pea Farmer, Meerut", emoji:"🧑‍🌾", stars:5 },
  { text:"I run a small restaurant. My food costs are down 28% since I switched to buying from FarmLink. And my customers keep commenting on how fresh the ingredients taste.", author:"Rahul Verma", role:"Restaurant Owner, Jaipur", emoji:"👨‍🍳", stars:5 },
  { text:"It's not just a shopping app. It's a movement. Supporting farmers directly feels genuinely meaningful. Plus the Alphonso mangoes I ordered were the best I've had in years.", author:"Deepa Krishnan", role:"Customer, Bengaluru", emoji:"👩‍💼", stars:5 },
];

// ─── STATE ───
let cart = [];
let activeCategory = "All";

// ─── INIT ───
document.addEventListener('DOMContentLoaded', () => {
  renderCategoryTabs();
  renderProducts();
  renderFarmerCards();
  renderTestimonials();
});

// ─── CATEGORIES ───
function renderCategoryTabs() {
  const cats = ["All", "Vegetables", "Fruits", "Grains", "Dairy & Eggs", "Spices"];
  const container = document.getElementById('categoryTabs');
  container.innerHTML = cats.map(c => `
    <button class="tab-btn ${c === activeCategory ? 'active' : ''}" onclick="setCategory('${c}')">${c}</button>
  `).join('');
}

function setCategory(cat) {
  activeCategory = cat;
  renderCategoryTabs();
  renderProducts();
}

// ─── PRODUCTS ───
function renderProducts() {
  const filtered = activeCategory === "All" ? products : products.filter(p => p.category === activeCategory);
  const container = document.getElementById('productsGrid');
  container.innerHTML = filtered.map((p, i) => {
    const save = Math.round(((p.mrp - p.price) / p.mrp) * 100);
    const initials = p.farmer.split(' ').map(x => x[0]).join('');
    const badgeClass = p.badge === 'Organic' ? 'organic' : p.badge === 'Sale' ? 'sale' : '';
    return `
    <div class="product-card" style="animation-delay:${i * 0.06}s" onclick="openProduct(${p.id})">
      <div class="product-img ${p.bgColor || 'card-blue'}">
        <span style="font-size:4.5rem;position:relative;z-index:1;filter:drop-shadow(0 4px 12px rgba(0,0,0,0.2))">${p.emoji}</span>
        <div class="product-badge ${badgeClass}">${p.badge}</div>
        <button class="product-fav" id="fav-${p.id}" onclick="toggleFav(event, ${p.id})">🤍</button>
      </div>
      <div class="product-body">
        <div class="product-farmer">
          <div class="farmer-avatar">${initials}</div>
          <span class="farmer-name">${p.farmer}</span>
          <span class="farmer-verified">✓</span>
        </div>
        <div class="product-name">${p.name}</div>
        <div class="product-rating">
          ${'★'.repeat(Math.floor(p.rating))}${'☆'.repeat(5-Math.floor(p.rating))}
          <span class="rating-count" style="color:var(--muted)">(${p.reviews})</span>
        </div>
        <div class="product-meta">per ${p.unit} · ${p.location}</div>
        <div class="product-price-row">
          <div class="product-price">
            <span class="price-current">₹${p.price}</span>
            <span class="price-old">₹${p.mrp}</span>
            <span class="price-save">-${save}%</span>
          </div>
          <button class="add-cart-btn" onclick="addToCart(event, ${p.id})">+</button>
        </div>
      </div>
    </div>`;
  }).join('');
}

function showAllProducts() {
  activeCategory = "All";
  renderCategoryTabs();
  renderProducts();
  document.getElementById('products').scrollIntoView({ behavior:'smooth' });
}

// ─── PRODUCT MODAL ───
function openProduct(id) {
  const p = products.find(x => x.id === id);
  if (!p) return;
  const save = Math.round(((p.mrp - p.price) / p.mrp) * 100);
  document.getElementById('modalEmoji').textContent = p.emoji;
  document.getElementById('modalName').textContent = p.name;
  document.getElementById('modalFarmer').innerHTML = `
    <span style="font-size:1rem">🧑‍🌾</span>
    <strong>${p.farmer}</strong>
    <span>·</span>
    <span>${p.location}</span>
    <span style="color:var(--moss);font-weight:700">✓ Verified</span>`;
  document.getElementById('modalDesc').textContent = p.desc;
  document.getElementById('modalPriceRow').innerHTML = `
    <span class="modal-price-current">₹${p.price}</span>
    <span class="modal-price-mrp">₹${p.mrp}</span>
    <span class="modal-price-save">Save ${save}%</span>`;
  document.getElementById('modalAddBtn').onclick = () => { addToCartById(id); closeProductModal(); };
  document.getElementById('productModal').classList.add('open');
}

function closeProductModal() {
  document.getElementById('productModal').classList.remove('open');
}

function closeModal(e) {
  if (e.target.id === 'productModal') closeProductModal();
}

// ─── CART ───
function addToCart(e, id) {
  e.stopPropagation();
  addToCartById(id);
}

function addToCartById(id) {
  const p = products.find(x => x.id === id);
  const existing = cart.find(x => x.id === id);
  if (existing) existing.qty++;
  else cart.push({ ...p, qty: 1 });
  updateCartUI();
  showToast('✓', `${p.name} added to cart!`);
}

function removeFromCart(id) {
  cart = cart.filter(x => x.id !== id);
  updateCartUI();
}

function changeQty(id, delta) {
  const item = cart.find(x => x.id === id);
  if (!item) return;
  item.qty += delta;
  if (item.qty <= 0) removeFromCart(id);
  else updateCartUI();
}

function updateCartUI() {
  const totalItems = cart.reduce((s, x) => s + x.qty, 0);
  document.getElementById('cartBadge').textContent = totalItems;

  const itemsEl = document.getElementById('cartItems');
  const footerEl = document.getElementById('cartFooter');

  if (cart.length === 0) {
    itemsEl.innerHTML = `
      <div class="cart-empty">
        <span class="cart-empty-icon">🧺</span>
        <p style="font-weight:600;margin-bottom:0.5rem;">Your basket is empty</p>
        <p style="font-size:0.85rem;">Add some fresh produce to get started!</p>
      </div>`;
    footerEl.style.display = 'none';
    return;
  }

  footerEl.style.display = 'block';

  itemsEl.innerHTML = cart.map(item => `
    <div class="cart-item">
      <div class="cart-item-emoji">${item.emoji}</div>
      <div class="cart-item-info">
        <div class="cart-item-name">${item.name}</div>
        <div class="cart-item-price">₹${item.price} / ${item.unit}</div>
      </div>
      <div class="qty-controls">
        <button class="qty-btn" onclick="changeQty(${item.id}, -1)">−</button>
        <span class="qty-num">${item.qty}</span>
        <button class="qty-btn" onclick="changeQty(${item.id}, 1)">+</button>
      </div>
      <button class="remove-btn" onclick="removeFromCart(${item.id})">🗑️</button>
    </div>
  `).join('');

  const subtotal = cart.reduce((s, x) => s + x.price * x.qty, 0);
  const mrpTotal = cart.reduce((s, x) => s + x.mrp * x.qty, 0);
  const saved = mrpTotal - subtotal;

  document.getElementById('cartSubtotal').textContent = `₹${subtotal}`;
  document.getElementById('cartTotal').textContent = `₹${subtotal}`;
  document.getElementById('cartSavingsMsg').textContent = `You saved ₹${saved} vs retail prices 🎉`;
}

function toggleCart() {
  document.getElementById('cartSidebar').classList.toggle('open');
  document.getElementById('cartOverlay').classList.toggle('open');
}

function checkout() {
  if (cart.length === 0) return;
  const total = cart.reduce((s, x) => s + x.price * x.qty, 0);
  showToast('🎉', `Order of ₹${total} placed! Thank you!`);
  cart = [];
  updateCartUI();
  toggleCart();
}

// ─── FARMERS ───
function renderFarmerCards() {
  const el = document.getElementById('farmerCards');
  el.innerHTML = farmers.map(f => `
    <div class="farmer-profile-card">
      <div class="farmer-big-avatar ${f.bg}">${f.emoji}</div>
      <div class="farmer-info">
        <div class="farmer-card-name">
          ${f.name}
          <span class="verified-badge">✓ Verified</span>
        </div>
        <div class="farmer-card-loc">📍 ${f.location}</div>
        <div class="farmer-card-tags">
          ${f.tags.map(t => `<span class="farmer-tag">${t}</span>`).join('')}
        </div>
      </div>
      <div class="farmer-earnings">
        <div class="farmer-sales">${f.sales}</div>
        <div class="farmer-sales-label">Total Earned</div>
      </div>
    </div>
  `).join('');
}

// ─── TESTIMONIALS ───
function renderTestimonials() {
  const el = document.getElementById('testimonialsGrid');
  const colors = ['#FFF8F0','#F0FFF4','#F0F4FF','#FFF0F5','#F5FFF0','#FFF5F0'];
  el.innerHTML = testimonials.map((t, i) => `
    <div class="testimonial-card" style="background:${colors[i % colors.length]}">
      <div class="testimonial-stars">${'★'.repeat(t.stars)}</div>
      <p class="testimonial-text">"${t.text}"</p>
      <div class="testimonial-author">
        <div class="author-avatar" style="background:var(--sprout)">${t.emoji}</div>
        <div>
          <div class="author-name">${t.author}</div>
          <div class="author-role">${t.role}</div>
        </div>
      </div>
    </div>
  `).join('');
}

// ─── SELL MODAL ───
function openSellModal() {
  document.getElementById('sellModal').classList.add('open');
  document.getElementById('sellForm').style.display = 'flex';
  document.getElementById('sellerSuccess').style.display = 'none';
}

function closeSellModal(e) {
  if (e.target.id === 'sellModal') document.getElementById('sellModal').classList.remove('open');
}

function submitSeller() {
  const name = document.getElementById('sellerName').value.trim();
  const phone = document.getElementById('sellerPhone').value.trim();
  const state = document.getElementById('sellerState').value;
  if (!name || !phone || !state) { showToast('⚠️', 'Please fill in Name, Phone & State'); return; }
  document.getElementById('sellForm').style.display = 'none';
  document.getElementById('sellerSuccess').style.display = 'block';
  showToast('🌾', `Welcome ${name}! Application submitted!`);
}

// ─── FAV ───
function toggleFav(e, id) {
  e.stopPropagation();
  const btn = document.getElementById(`fav-${id}`);
  const isLiked = btn.classList.toggle('liked');
  btn.textContent = isLiked ? '❤️' : '🤍';
  showToast(isLiked ? '❤️' : '💔', isLiked ? 'Added to wishlist' : 'Removed from wishlist');
}

// ─── NEWSLETTER ───
function subscribeNewsletter() {
  const email = document.getElementById('newsletterEmail').value.trim();
  if (!email || !email.includes('@')) { showToast('⚠️', 'Please enter a valid email'); return; }
  document.getElementById('newsletterEmail').value = '';
  showToast('✉️', 'Subscribed! Fresh deals coming your way 🌱');
}

// ─── TOAST ───
function showToast(icon, msg) {
  const toast = document.getElementById('toast');
  document.getElementById('toastIcon').textContent = icon;
  document.getElementById('toastMsg').textContent = msg;
  toast.classList.add('show');
  setTimeout(() => toast.classList.remove('show'), 2800);
}

function scrollToTop() {
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

// ─── SCROLL ANIMATIONS ───
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.style.opacity = '1';
      entry.target.style.transform = 'translateY(0)';
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.how-card, .testimonial-card, .farmer-profile-card').forEach(el => {
  el.style.opacity = '0';
  el.style.transform = 'translateY(20px)';
  el.style.transition = 'opacity 0.5s ease, transform 0.5s ease';
  observer.observe(el);
});
</script>
</body>
</html>
