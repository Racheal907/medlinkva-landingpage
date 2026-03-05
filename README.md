<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MedLink VA — Virtual Medical Assistant Services</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700;900&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --navy: #0a1628;
    --blue-deep: #0d3b6e;
    --blue-mid: #1565c0;
    --teal: #0097a7;
    --teal-light: #00bcd4;
    --sky: #4fc3f7;
    --white: #ffffff;
    --glass: rgba(255,255,255,0.08);
    --glass-border: rgba(255,255,255,0.15);
    --text-muted: rgba(255,255,255,0.65);
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  html { scroll-behavior: smooth; }
  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--navy);
    color: var(--white);
    overflow-x: hidden;
  }
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 80% 60% at 20% 0%, rgba(21,101,192,0.45) 0%, transparent 60%),
      radial-gradient(ellipse 60% 50% at 80% 30%, rgba(0,151,167,0.3) 0%, transparent 55%),
      radial-gradient(ellipse 50% 70% at 50% 100%, rgba(13,59,110,0.6) 0%, transparent 60%);
    pointer-events: none;
    z-index: 0;
  }

  /* NAV */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 1000;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem 5%;
    background: rgba(10,22,40,0.88);
    backdrop-filter: blur(16px);
    border-bottom: 1px solid var(--glass-border);
  }
  .logo {
    font-family: 'Playfair Display', serif;
    font-size: 1.5rem;
    font-weight: 700;
    background: linear-gradient(135deg, var(--sky), var(--teal-light));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .logo span { font-weight: 400; opacity: 0.75; }
  .nav-links { display: flex; gap: 1.6rem; list-style: none; align-items: center; }
  .nav-links a {
    color: rgba(255,255,255,0.8);
    text-decoration: none;
    font-size: 0.88rem;
    font-weight: 500;
    transition: color 0.2s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -3px; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--teal-light), var(--sky));
    transform: scaleX(0);
    transition: transform 0.25s;
    border-radius: 2px;
  }
  .nav-links a:hover { color: var(--white); }
  .nav-links a:hover::after { transform: scaleX(1); }
  .nav-cta {
    background: linear-gradient(135deg, var(--teal), var(--blue-mid)) !important;
    color: white !important;
    padding: 0.5rem 1.3rem !important;
    border-radius: 50px !important;
    font-weight: 600 !important;
    box-shadow: 0 4px 20px rgba(0,151,167,0.35) !important;
    transition: transform 0.2s, box-shadow 0.2s !important;
  }
  .nav-cta:hover { transform: translateY(-2px) !important; box-shadow: 0 8px 30px rgba(0,151,167,0.5) !important; }
  .nav-cta::after { display: none !important; }
  .hamburger { display: none; flex-direction: column; gap: 5px; cursor: pointer; padding: 4px; }
  .hamburger span { display: block; width: 24px; height: 2px; background: white; border-radius: 2px; }
  @media(max-width:768px){ .nav-links{display:none} .hamburger{display:flex} }
  .mobile-nav {
    display: none;
    position: fixed;
    top: 63px; left: 0; right: 0;
    background: rgba(10,22,40,0.97);
    border-bottom: 1px solid var(--glass-border);
    padding: 1.5rem 5%;
    z-index: 998;
    flex-direction: column;
    gap: 1rem;
  }
  .mobile-nav.open { display: flex; }
  .mobile-nav a { color: rgba(255,255,255,0.85); text-decoration: none; font-size: 1rem; padding: 0.5rem 0; border-bottom: 1px solid var(--glass-border); }

  /* URGENCY BANNER */
  .urgency-banner {
    position: fixed;
    top: 63px; left: 0; right: 0;
    z-index: 999;
    background: linear-gradient(90deg, #b71c1c, #d32f2f, #b71c1c);
    text-align: center;
    padding: 0.55rem;
    font-size: 0.875rem;
    font-weight: 600;
    animation: pulseBar 2s ease-in-out infinite;
  }
  @keyframes pulseBar { 0%,100%{opacity:1} 50%{opacity:0.85} }
  .urgency-banner .timer { font-weight: 700; color: #ffeb3b; margin: 0 0.3rem; }
  .urgency-banner del { opacity: 0.65; margin-right: 0.2rem; }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex;
    align-items: center;
    padding: 11rem 5% 6rem;
    position: relative;
    z-index: 1;
  }
  .hero-content { max-width: 660px; }
  .hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    background: rgba(0,188,212,0.12);
    border: 1px solid rgba(0,188,212,0.3);
    border-radius: 50px;
    padding: 0.4rem 1rem;
    font-size: 0.78rem;
    font-weight: 700;
    color: var(--teal-light);
    letter-spacing: 1.2px;
    text-transform: uppercase;
    margin-bottom: 1.4rem;
    animation: fadeUp 0.8s ease both;
  }
  .hero-badge::before { content:'●'; color:#4caf50; animation: blink 1.5s infinite; margin-right:2px; }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.3} }
  .hero h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.5rem,5.5vw,4rem);
    font-weight: 900;
    line-height: 1.1;
    margin-bottom: 1.3rem;
    animation: fadeUp 0.8s 0.1s ease both;
  }
  .hero h1 em {
    font-style: normal;
    background: linear-gradient(135deg, var(--teal-light), var(--sky));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .hero p {
    font-size: 1.1rem;
    color: var(--text-muted);
    line-height: 1.7;
    margin-bottom: 2rem;
    max-width: 540px;
    animation: fadeUp 0.8s 0.2s ease both;
  }
  .hero-actions {
    display: flex; gap: 1rem; flex-wrap: wrap;
    animation: fadeUp 0.8s 0.3s ease both;
  }
  .btn-primary {
    background: linear-gradient(135deg, var(--teal), var(--blue-mid));
    color: white;
    padding: 0.9rem 2.1rem;
    border: none;
    border-radius: 50px;
    font-family: 'DM Sans', sans-serif;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    box-shadow: 0 6px 28px rgba(0,151,167,0.4);
    transition: transform 0.2s, box-shadow 0.2s;
    text-decoration: none;
    display: inline-block;
  }
  .btn-primary:hover { transform: translateY(-3px); box-shadow: 0 12px 38px rgba(0,151,167,0.55); }
  .btn-outline {
    background: transparent;
    color: white;
    padding: 0.9rem 2.1rem;
    border: 1.5px solid rgba(255,255,255,0.28);
    border-radius: 50px;
    font-family: 'DM Sans', sans-serif;
    font-size: 1rem;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.2s;
    text-decoration: none;
    display: inline-block;
  }
  .btn-outline:hover { border-color: var(--teal-light); color: var(--teal-light); background: rgba(0,188,212,0.07); }

  /* HERO VISUAL */
  .hero-visual {
    position: absolute;
    right: 5%; top: 50%;
    transform: translateY(-50%);
    width: 400px; height: 400px;
    animation: fadeUp 1s 0.4s ease both;
    display: flex; align-items: center; justify-content: center;
  }
  @media(max-width:1024px){ .hero-visual{display:none} }
  .orb {
    width: 360px; height: 360px;
    border-radius: 50%;
    background: radial-gradient(circle at 35% 35%, rgba(0,188,212,0.22), rgba(21,101,192,0.12), transparent 70%);
    border: 1px solid rgba(0,188,212,0.18);
    animation: spin 14s linear infinite;
    position: relative;
    display: flex; align-items: center; justify-content: center;
  }
  @keyframes spin { from{transform:rotate(0)} to{transform:rotate(360deg)} }
  .orb::before {
    content:'';
    position:absolute; inset:22px;
    border-radius:50%;
    border:1px dashed rgba(0,188,212,0.18);
  }
  .orb-inner {
    position:absolute; inset:70px;
    border-radius:50%;
    background: radial-gradient(circle, rgba(0,151,167,0.28), rgba(21,101,192,0.18));
    display:flex; align-items:center; justify-content:center;
    flex-direction:column; text-align:center;
    animation: spin 14s linear infinite reverse;
    padding:1.5rem;
  }
  .orb-icon { font-size:2.8rem; margin-bottom:0.4rem; }
  .orb-text { font-family:'Playfair Display',serif; font-size:0.95rem; font-weight:600; color:var(--teal-light); line-height:1.3; }
  .float-card {
    position:absolute;
    background:rgba(10,22,40,0.88);
    backdrop-filter:blur(10px);
    border:1px solid var(--glass-border);
    border-radius:12px;
    padding:0.8rem 1.1rem;
    font-size:0.8rem;
    white-space:nowrap;
  }
  .float-card:nth-child(2){ top:14%; left:-8%; animation:float 3s ease-in-out infinite; }
  .float-card:nth-child(3){ bottom:18%; right:-4%; animation:float 3s 1.5s ease-in-out infinite; }
  .float-card strong { display:block; color:var(--teal-light); font-weight:600; margin-bottom:0.15rem; }
  @keyframes float { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-10px)} }

  /* STATS */
  .stats {
    position:relative; z-index:1;
    display:grid; grid-template-columns:repeat(4,1fr);
    gap:1.5rem; padding:2.8rem 5%;
    background:rgba(255,255,255,0.03);
    border-top:1px solid var(--glass-border);
    border-bottom:1px solid var(--glass-border);
  }
  @media(max-width:768px){ .stats{grid-template-columns:repeat(2,1fr)} }
  .stat-item { text-align:center; }
  .stat-num {
    font-family:'Playfair Display',serif;
    font-size:2.2rem; font-weight:700;
    background:linear-gradient(135deg,var(--teal-light),var(--sky));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent;
  }
  .stat-lbl { font-size:0.82rem; color:var(--text-muted); margin-top:0.3rem; }

  /* SECTIONS */
  section { position:relative; z-index:1; padding:5rem 5%; }
  .section-tag {
    font-size:0.72rem; font-weight:700; letter-spacing:2px;
    text-transform:uppercase; color:var(--teal-light); margin-bottom:0.7rem;
  }
  .section-title {
    font-family:'Playfair Display',serif;
    font-size:clamp(1.9rem,3.5vw,2.7rem);
    font-weight:700; line-height:1.2; margin-bottom:1rem;
  }
  .section-title em {
    font-style:normal;
    background:linear-gradient(135deg,var(--teal-light),var(--sky));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent;
  }
  .section-sub { color:var(--text-muted); font-size:1rem; line-height:1.7; max-width:540px; margin-bottom:3rem; }

  /* SERVICES */
  #administrative, #ehr-data-entry { scroll-margin-top: 130px; }
  .services-hdr { text-align:center; max-width:600px; margin:0 auto 3.5rem; }
  .services-hdr .section-sub { margin:0 auto; }
  .services-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(280px,1fr)); gap:1.4rem; }
  .service-card {
    background:var(--glass);
    border:1px solid var(--glass-border);
    border-radius:20px;
    padding:1.9rem;
    transition:transform 0.3s, border-color 0.3s, box-shadow 0.3s;
    position:relative; overflow:hidden;
  }
  .service-card::before {
    content:'';
    position:absolute; top:0; left:0; right:0; height:3px;
    background:linear-gradient(90deg,var(--teal),var(--blue-mid),var(--sky));
    opacity:0; transition:opacity 0.3s;
  }
  .service-card:hover { transform:translateY(-6px); border-color:rgba(0,188,212,0.35); box-shadow:0 20px 48px rgba(0,0,0,0.25); }
  .service-card:hover::before { opacity:1; }
  .svc-icon {
    width:50px; height:50px;
    background:linear-gradient(135deg,rgba(0,151,167,0.22),rgba(21,101,192,0.18));
    border:1px solid rgba(0,188,212,0.22);
    border-radius:13px;
    display:flex; align-items:center; justify-content:center;
    font-size:1.4rem; margin-bottom:1.1rem;
  }
  .service-card h3 { font-family:'Playfair Display',serif; font-size:1.15rem; font-weight:700; margin-bottom:0.65rem; }
  .service-card p { color:var(--text-muted); font-size:0.88rem; line-height:1.65; }
  .svc-divider {
    text-align:center; padding:2rem 0 1rem;
    font-size:0.72rem; font-weight:700; letter-spacing:2px;
    text-transform:uppercase; color:rgba(0,188,212,0.55);
    position:relative; z-index:1;
  }

  /* WHY US */
  #why-us { scroll-margin-top: 130px; }
  .why-grid { display:grid; grid-template-columns:1fr 1fr; gap:4rem; align-items:center; }
  @media(max-width:1024px){ .why-grid{grid-template-columns:1fr} }
  .why-list { display:flex; flex-direction:column; gap:1.3rem; }
  .why-item {
    display:flex; gap:1.1rem; align-items:flex-start;
    padding:1.3rem; background:var(--glass);
    border:1px solid var(--glass-border); border-radius:14px;
    transition:all 0.3s;
  }
  .why-item:hover { border-color:rgba(0,188,212,0.3); background:rgba(0,188,212,0.06); }
  .why-check {
    width:38px; height:38px; min-width:38px;
    background:linear-gradient(135deg,var(--teal),var(--blue-mid));
    border-radius:50%;
    display:flex; align-items:center; justify-content:center;
    font-size:1rem; box-shadow:0 4px 14px rgba(0,151,167,0.35);
  }
  .why-text h4 { font-weight:600; font-size:0.97rem; margin-bottom:0.28rem; }
  .why-text p { color:var(--text-muted); font-size:0.85rem; line-height:1.6; }
  .why-visual {
    background:var(--glass); border:1px solid var(--glass-border);
    border-radius:22px; padding:2.3rem; text-align:center;
  }
  .why-visual-emoji { font-size:3.5rem; margin-bottom:0.9rem; }
  .why-visual h3 { font-family:'Playfair Display',serif; font-size:1.5rem; margin-bottom:0.9rem; }
  .why-visual p { color:var(--text-muted); font-size:0.92rem; line-height:1.65; margin-bottom:1.4rem; }
  .trust-badges { display:flex; flex-direction:column; gap:0.7rem; }
  .trust-badge {
    background:rgba(0,151,167,0.12);
    border:1px solid rgba(0,151,167,0.25);
    border-radius:9px; padding:0.55rem 1rem;
    font-size:0.83rem; font-weight:500; color:var(--teal-light);
  }

  /* PRICING */
  #pricing { scroll-margin-top: 130px; }
  .pricing-wrap { max-width:700px; margin:0 auto; }
  .pricing-card {
    background:linear-gradient(135deg,rgba(21,101,192,0.18),rgba(0,151,167,0.13));
    border:1.5px solid rgba(0,188,212,0.38);
    border-radius:26px; padding:2.8rem;
    position:relative; overflow:hidden;
    box-shadow:0 24px 70px rgba(0,0,0,0.28), 0 0 0 1px rgba(0,188,212,0.1);
  }
  .pricing-card::before {
    content:'';
    position:absolute; top:-70px; right:-70px;
    width:230px; height:230px; border-radius:50%;
    background:radial-gradient(circle,rgba(0,188,212,0.13),transparent 60%);
  }
  .pricing-popular {
    position:absolute; top:1.4rem; right:1.4rem;
    background:linear-gradient(135deg,var(--teal),var(--blue-mid));
    padding:0.3rem 0.95rem; border-radius:50px;
    font-size:0.72rem; font-weight:700; letter-spacing:0.5px; text-transform:uppercase;
  }
  .pricing-name { font-family:'Playfair Display',serif; font-size:1.45rem; font-weight:700; margin-bottom:0.4rem; }
  .pricing-tagline { color:var(--text-muted); font-size:0.92rem; margin-bottom:1.4rem; }
  .pricing-amount { display:flex; align-items:flex-end; gap:0.75rem; margin-bottom:0.4rem; }
  .price-old { font-size:1.45rem; text-decoration:line-through; color:rgba(255,255,255,0.38); }
  .price-new {
    font-family:'Playfair Display',serif; font-size:3.3rem; font-weight:900;
    background:linear-gradient(135deg,var(--teal-light),var(--sky));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent;
    line-height:1;
  }
  .price-period { color:var(--text-muted); font-size:0.92rem; padding-bottom:0.35rem; }
  .price-savings {
    display:inline-block;
    background:rgba(76,175,80,0.18); border:1px solid rgba(76,175,80,0.32);
    color:#a5d6a7; padding:0.28rem 0.85rem; border-radius:50px;
    font-size:0.78rem; font-weight:600; margin-bottom:1.8rem;
  }
  .pricing-features {
    list-style:none; display:grid; grid-template-columns:1fr 1fr; gap:0.75rem;
    margin-bottom:2.2rem;
  }
  @media(max-width:600px){ .pricing-features{grid-template-columns:1fr} }
  .pricing-features li {
    display:flex; align-items:center; gap:0.55rem;
    font-size:0.88rem; color:rgba(255,255,255,0.85);
  }
  .pricing-features li::before {
    content:'✓';
    width:19px; height:19px; min-width:19px;
    background:linear-gradient(135deg,var(--teal),var(--blue-mid));
    border-radius:50%; display:flex; align-items:center; justify-content:center;
    font-size:0.6rem; font-weight:700;
  }
  .pricing-urgency {
    background:rgba(183,28,28,0.13);
    border:1px solid rgba(244,67,54,0.28);
    border-radius:11px; padding:0.9rem 1.3rem;
    margin-bottom:1.7rem;
    display:flex; align-items:center; justify-content:space-between;
    gap:1rem; flex-wrap:wrap;
  }
  .urg-text { font-size:0.85rem; color:#ff8a80; font-weight:500; }
  .countdown { display:flex; gap:0.55rem; }
  .count-unit { text-align:center; }
  .count-num {
    background:rgba(244,67,54,0.18); border:1px solid rgba(244,67,54,0.38);
    border-radius:7px; padding:0.28rem 0.55rem;
    font-size:1.05rem; font-weight:700; color:#ff8a80;
    font-family:monospace; min-width:34px; display:block; text-align:center;
  }
  .count-lbl { font-size:0.58rem; color:rgba(255,255,255,0.38); margin-top:0.18rem; text-align:center; }

  /* CONTACT */
  #contact { scroll-margin-top: 130px; }
  .contact-grid { display:grid; grid-template-columns:1fr 1fr; gap:3rem; align-items:start; }
  @media(max-width:1024px){ .contact-grid{grid-template-columns:1fr} }
  .contact-info h3 { font-family:'Playfair Display',serif; font-size:1.9rem; margin-bottom:0.9rem; }
  .contact-info p { color:var(--text-muted); line-height:1.7; margin-bottom:1.8rem; }
  .contact-item {
    display:flex; align-items:center; gap:0.95rem;
    padding:0.95rem 1.2rem; background:var(--glass);
    border:1px solid var(--glass-border); border-radius:12px;
    margin-bottom:0.9rem; text-decoration:none; color:inherit;
    transition:all 0.25s;
  }
  .contact-item:hover { border-color:rgba(0,188,212,0.32); background:rgba(0,188,212,0.06); }
  .c-icon {
    font-size:1.25rem; width:40px; height:40px;
    background:linear-gradient(135deg,rgba(0,151,167,0.22),rgba(21,101,192,0.18));
    border-radius:10px; display:flex; align-items:center; justify-content:center;
    min-width:40px;
  }
  .c-detail strong { display:block; font-size:0.72rem; text-transform:uppercase; letter-spacing:1px; color:var(--teal-light); margin-bottom:0.18rem; }
  .c-detail span { font-size:0.92rem; }

  /* CONTACT FORM */
  .contact-form-wrap { background:var(--glass); border:1px solid var(--glass-border); border-radius:22px; padding:2.3rem; }
  .contact-form-wrap h3 { font-family:'Playfair Display',serif; font-size:1.35rem; margin-bottom:1.4rem; }

  /* FOOTER */
  footer {
    position:relative; z-index:1;
    text-align:center; padding:2.3rem 5%;
    border-top:1px solid var(--glass-border);
    color:var(--text-muted); font-size:0.82rem;
  }
  footer strong { background:linear-gradient(135deg,var(--teal-light),var(--sky)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; }

  /* MODAL */
  .modal-overlay {
    display:none; position:fixed; inset:0;
    background:rgba(0,0,0,0.78); backdrop-filter:blur(7px);
    z-index:2000; align-items:center; justify-content:center; padding:1rem;
  }
  .modal-overlay.active { display:flex; }
  .modal {
    background:linear-gradient(135deg,#0d2040,#0a1628);
    border:1px solid rgba(0,188,212,0.32);
    border-radius:22px; padding:2.4rem;
    max-width:490px; width:100%;
    position:relative;
    animation:modalIn 0.35s cubic-bezier(0.34,1.56,0.64,1) both;
    box-shadow:0 30px 75px rgba(0,0,0,0.5);
    max-height:90vh; overflow-y:auto;
  }
  @keyframes modalIn { from{opacity:0;transform:scale(0.85) translateY(28px)} to{opacity:1;transform:scale(1) translateY(0)} }
  .modal-close {
    position:absolute; top:1.1rem; right:1.1rem;
    background:rgba(255,255,255,0.1); border:none; color:white;
    width:31px; height:31px; border-radius:50%; font-size:0.95rem;
    cursor:pointer; display:flex; align-items:center; justify-content:center;
    transition:background 0.2s;
  }
  .modal-close:hover { background:rgba(255,255,255,0.2); }
  .modal-top { text-align:center; margin-bottom:1.8rem; }
  .modal-icon { font-size:2.3rem; margin-bottom:0.7rem; }
  .modal h2 { font-family:'Playfair Display',serif; font-size:1.55rem; margin-bottom:0.4rem; }
  .modal-sub { color:var(--text-muted); font-size:0.87rem; line-height:1.5; }

  /* FORM */
  .form-group { margin-bottom:1.1rem; }
  .form-group label { display:block; font-size:0.76rem; font-weight:600; letter-spacing:0.5px; color:var(--teal-light); margin-bottom:0.38rem; text-transform:uppercase; }
  .form-group input,
  .form-group select,
  .form-group textarea {
    width:100%; background:rgba(255,255,255,0.06);
    border:1.5px solid rgba(255,255,255,0.11);
    border-radius:9px; color:white;
    padding:0.75rem 0.95rem;
    font-family:'DM Sans',sans-serif; font-size:0.92rem;
    transition:border-color 0.2s; outline:none;
  }
  .form-group input::placeholder, .form-group textarea::placeholder { color:rgba(255,255,255,0.28); }
  .form-group input:focus, .form-group select:focus, .form-group textarea:focus { border-color:var(--teal-light); background:rgba(0,188,212,0.05); }
  .form-group select option { background:#0d2040; color:white; }
  .form-group textarea { resize:vertical; min-height:75px; }
  .form-row { display:grid; grid-template-columns:1fr 1fr; gap:0.9rem; }
  @media(max-width:500px){ .form-row{grid-template-columns:1fr} }
  .submit-btn {
    width:100%; background:linear-gradient(135deg,var(--teal),var(--blue-mid));
    color:white; border:none; padding:0.95rem;
    border-radius:11px; font-family:'DM Sans',sans-serif;
    font-size:0.98rem; font-weight:600; cursor:pointer; margin-top:0.4rem;
    box-shadow:0 6px 22px rgba(0,151,167,0.38);
    transition:transform 0.2s, box-shadow 0.2s;
  }
  .submit-btn:hover { transform:translateY(-2px); box-shadow:0 10px 32px rgba(0,151,167,0.5); }
  .submit-btn:disabled { opacity:0.6; cursor:not-allowed; transform:none; }
  .success-message { display:none; text-align:center; padding:1rem; }
  .success-message.show { display:block; }
  .success-icon { font-size:2.8rem; margin-bottom:0.9rem; }
  .success-message h3 { font-family:'Playfair Display',serif; font-size:1.35rem; margin-bottom:0.45rem; color:var(--teal-light); }
  .success-message p { color:var(--text-muted); font-size:0.87rem; line-height:1.6; }

  /* ANIMATIONS */
  @keyframes fadeUp { from{opacity:0;transform:translateY(28px)} to{opacity:1;transform:none} }
  .reveal { opacity:0; transform:translateY(28px); transition:opacity 0.6s, transform 0.6s; }
  .reveal.visible { opacity:1; transform:none; }
</style>
</head>
<body>

<!-- URGENCY BANNER -->
<div class="urgency-banner">
  🔥 LIMITED OFFER: <del>$600</del> → <strong>$450/mo</strong> &nbsp;|&nbsp; Expires in: <span class="timer" id="bannerTimer">47:59:59</span> &nbsp;|&nbsp; Secure your rate today!
</div>

<!-- NAV -->
<nav>
  <div class="logo">MedLink<span>VA</span></div>
  <ul class="nav-links">
    <li><a href="#services">Services</a></li>
    <li><a href="#administrative">Administrative</a></li>
    <li><a href="#ehr-data-entry">EHR Data Entry</a></li>
    <li><a href="#why-us">Why Us</a></li>
    <li><a href="#pricing">Pricing</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#" class="nav-cta" onclick="openModal(); return false;">Get Started</a></li>
  </ul>
  <div class="hamburger" id="hamburger" onclick="toggleMenu()">
    <span></span><span></span><span></span>
  </div>
</nav>
<div class="mobile-nav" id="mobileNav">
  <a href="#services" onclick="closeMenu()">Services</a>
  <a href="#administrative" onclick="closeMenu()">Administrative</a>
  <a href="#ehr-data-entry" onclick="closeMenu()">EHR Data Entry</a>
  <a href="#why-us" onclick="closeMenu()">Why Us</a>
  <a href="#pricing" onclick="closeMenu()">Pricing</a>
  <a href="#contact" onclick="closeMenu()">Contact</a>
  <a href="#" onclick="openModal();closeMenu();return false;">Get Started</a>
</div>

<!-- HERO -->
<section class="hero">
  <div class="hero-content">
    <div class="hero-badge">🩺 Virtual Medical Assistant Services</div>
    <h1>Your Practice,<br>Managed with <em>Precision.</em></h1>
    <p>Expert virtual medical assistance that keeps your healthcare operations running smoothly — so you can focus entirely on patient care.</p>
    <div class="hero-actions">
      <button class="btn-primary" onclick="openModal()">Book Free Consultation</button>
      <a href="#services" class="btn-outline">Explore Services</a>
    </div>
  </div>
  <div class="hero-visual">
    <div class="orb">
      <div class="orb-inner">
        <div class="orb-icon">🏥</div>
        <div class="orb-text">Virtual<br>Medical VA</div>
      </div>
    </div>
    <div class="float-card">
      <strong>📅 Appointment Set</strong>
      Dr. Nakamura — 2:30 PM
    </div>
    <div class="float-card">
      <strong>📋 EHR Updated</strong>
      12 records synced ✓
    </div>
  </div>
</section>

<!-- STATS -->
<div class="stats">
  <div class="stat-item"><div class="stat-num">100%</div><div class="stat-lbl">HIPAA-Aware Handling</div></div>
  <div class="stat-item"><div class="stat-num">24/7</div><div class="stat-lbl">Remote Availability</div></div>
  <div class="stat-item"><div class="stat-num">7+</div><div class="stat-lbl">Specialised Services</div></div>
  <div class="stat-item"><div class="stat-num">$450</div><div class="stat-lbl">All-Inclusive Monthly</div></div>
</div>

<!-- SERVICES -->
<section id="services">
  <div class="services-hdr reveal">
    <div class="section-tag">What We Do</div>
    <h2 class="section-title">Comprehensive <em>Virtual Medical</em> Services</h2>
    <p class="section-sub">Every service tailored to the unique demands of healthcare professionals — efficient, accurate, and discreet.</p>
  </div>

  <div class="svc-divider" id="administrative">— Administrative Services —</div>
  <div class="services-grid" style="margin-bottom:2.5rem;">
    <div class="service-card reveal">
      <div class="svc-icon">📧</div>
      <h3>Email Management</h3>
      <p>Organised, prioritised inbox management. We handle correspondence, flag urgent messages, and draft professional responses on your behalf.</p>
    </div>
    <div class="service-card reveal">
      <div class="svc-icon">📆</div>
      <h3>Calendar Management</h3>
      <p>Seamless calendar coordination — scheduling, rescheduling, reminders, and conflict resolution so your day flows without interruption.</p>
    </div>
    <div class="service-card reveal">
      <div class="svc-icon">🗓️</div>
      <h3>Appointment Scheduling</h3>
      <p>Patient and staff appointments managed with precision — confirmations, reminders, and no-show follow-ups all handled for you.</p>
    </div>
    <div class="service-card reveal">
      <div class="svc-icon">📞</div>
      <h3>Appointment Setting</h3>
      <p>Proactive outreach and booking to fill your schedule. We confirm details, communicate with patients, and reduce cancellations.</p>
    </div>
    <div class="service-card reveal">
      <div class="svc-icon">🎧</div>
      <h3>Customer Service</h3>
      <p>Professional, empathetic patient-facing support via phone or email. We represent your practice with the care and warmth it deserves.</p>
    </div>
  </div>

  <div class="svc-divider" id="ehr-data-entry">— EHR &amp; Clinical Support —</div>
  <div class="services-grid">
    <div class="service-card reveal">
      <div class="svc-icon">🗂️</div>
      <h3>EHR Data Entry</h3>
      <p>Accurate, timely entry of patient records into your EHR system. We ensure data integrity, reduce errors, and keep charts audit-ready.</p>
    </div>
    <div class="service-card reveal">
      <div class="svc-icon">📡</div>
      <h3>Remote Patient Monitoring Assistant</h3>
      <p>RPM program support — tracking patient data, flagging anomalies, and coordinating with clinical staff for timely interventions.</p>
    </div>
  </div>
</section>

<!-- WHY US -->
<section id="why-us" style="background:rgba(255,255,255,0.02);border-top:1px solid var(--glass-border);border-bottom:1px solid var(--glass-border);">
  <div class="why-grid">
    <div>
      <div class="section-tag reveal">Why Choose Us</div>
      <h2 class="section-title reveal">The <em>MedLink VA</em> Difference</h2>
      <p class="section-sub reveal">We're not a generic VA service. We specialise exclusively in virtual medical support — that distinction matters.</p>
      <div class="why-list">
        <div class="why-item reveal">
          <div class="why-check">🎯</div>
          <div class="why-text">
            <h4>Healthcare-Focused Expertise</h4>
            <p>Our team understands medical workflows, terminology, and clinical operations — no lengthy onboarding needed.</p>
          </div>
        </div>
        <div class="why-item reveal">
          <div class="why-check">🔒</div>
          <div class="why-text">
            <h4>Confidentiality &amp; Discretion</h4>
            <p>Patient information is treated with the utmost care, following HIPAA-aware practices in every interaction.</p>
          </div>
        </div>
        <div class="why-item reveal">
          <div class="why-check">⚡</div>
          <div class="why-text">
            <h4>Fast Turnaround Times</h4>
            <p>We're responsive, reliable, and available. Tasks completed with speed and accuracy every single time.</p>
          </div>
        </div>
        <div class="why-item reveal">
          <div class="why-check">💰</div>
          <div class="why-text">
            <h4>Significant Cost Savings</h4>
            <p>No overhead of a full-time hire. Premium support at a fraction of the cost — now just $450/month.</p>
          </div>
        </div>
      </div>
    </div>
    <div class="why-visual reveal">
      <div class="why-visual-emoji">🩺</div>
      <h3>Built for Healthcare Professionals</h3>
      <p>We partner with solo practitioners, group practices, telehealth companies, and healthcare startups who need reliable virtual support without the full-time cost.</p>
      <div class="trust-badges">
        <div class="trust-badge">✅ Healthcare Workflow Expertise</div>
        <div class="trust-badge">✅ EHR Systems Proficient</div>
        <div class="trust-badge">✅ Telehealth Ready</div>
        <div class="trust-badge">✅ Flexible &amp; Scalable</div>
      </div>
    </div>
  </div>
</section>

<!-- PRICING -->
<section id="pricing">
  <div style="text-align:center;margin-bottom:3rem;" class="reveal">
    <div class="section-tag">Pricing</div>
    <h2 class="section-title">Complete Virtual Medical<br><em>Assistant Package</em></h2>
    <p class="section-sub" style="margin:0 auto;">One transparent price. Every service included. No surprises.</p>
  </div>
  <div class="pricing-wrap">
    <div class="pricing-card reveal">
      <div class="pricing-popular">⭐ Best Value</div>
      <div class="pricing-name">Complete Virtual Medical Assistant Package</div>
      <div class="pricing-tagline">Everything you need to run a lean, efficient medical practice — remotely.</div>
      <div class="pricing-amount">
        <span class="price-old">$600</span>
        <span class="price-new">$450</span>
        <span class="price-period">/ month</span>
      </div>
      <div class="price-savings">🎉 Save $150/month — Limited Time Offer</div>
      <ul class="pricing-features">
        <li>Email Management</li>
        <li>Calendar Management</li>
        <li>Appointment Scheduling</li>
        <li>Appointment Setting</li>
        <li>Customer Service</li>
        <li>EHR Data Entry</li>
        <li>Remote Patient Monitoring</li>
        <li>Priority Support</li>
      </ul>
      <div class="pricing-urgency">
        <div class="urg-text">⏰ Offer expires in:</div>
        <div class="countdown">
          <div class="count-unit"><span class="count-num" id="hours">47</span><div class="count-lbl">HRS</div></div>
          <div class="count-unit"><span class="count-num" id="mins">59</span><div class="count-lbl">MIN</div></div>
          <div class="count-unit"><span class="count-num" id="secs">59</span><div class="count-lbl">SEC</div></div>
        </div>
      </div>
      <button class="btn-primary" style="width:100%;border-radius:12px;font-size:1rem;padding:1rem;" onclick="openModal()">
        Claim This Rate — Book Now
      </button>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact" style="background:rgba(255,255,255,0.02);border-top:1px solid var(--glass-border);">
  <div class="contact-grid">
    <div class="contact-info reveal">
      <div class="section-tag">Get In Touch</div>
      <h3>Ready to Streamline<br>Your Practice?</h3>
      <p>Reach out today and let's discuss how MedLink VA can support your healthcare operations. We respond within 24 hours.</p>
      <a href="mailto:medlinkva@gmail.com" class="contact-item">
        <div class="c-icon">✉️</div>
        <div class="c-detail"><strong>Email Us</strong><span>medlinkva@gmail.com</span></div>
      </a>
      <a href="tel:+256785724420" class="contact-item">
        <div class="c-icon">📱</div>
        <div class="c-detail"><strong>Call / WhatsApp</strong><span>+256 785 724 420</span></div>
      </a>
      <div class="contact-item" style="cursor:default;">
        <div class="c-icon">🌍</div>
        <div class="c-detail"><strong>Serving</strong><span>Worldwide — Fully Remote</span></div>
      </div>
    </div>
    <div class="contact-form-wrap reveal">
      <h3>Send Us a Message</h3>
      <form id="contactForm" onsubmit="submitContactForm(event)">
        <div class="form-row">
          <div class="form-group">
            <label>First Name</label>
            <input type="text" id="cf_first" placeholder="Jane" required>
          </div>
          <div class="form-group">
            <label>Last Name</label>
            <input type="text" id="cf_last" placeholder="Smith" required>
          </div>
        </div>
        <div class="form-group">
          <label>Email Address</label>
          <input type="email" id="cf_email" placeholder="jane@yourpractice.com" required>
        </div>
        <div class="form-group">
          <label>Phone / WhatsApp</label>
          <input type="tel" id="cf_phone" placeholder="+1 000 000 0000">
        </div>
        <div class="form-group">
          <label>Message</label>
          <textarea id="cf_msg" placeholder="Tell us about your practice and what support you need..." rows="4"></textarea>
        </div>
        <button type="submit" class="submit-btn" id="cfBtn">Send Message →</button>
        <p id="cfFeedback" style="display:none;margin-top:0.9rem;text-align:center;color:#a5d6a7;font-size:0.87rem;"></p>
      </form>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <p><strong>MedLink VA</strong> — Virtual Medical Assistant Services</p>
  <p style="margin-top:0.45rem;">✉️ medlinkva@gmail.com &nbsp;|&nbsp; 📱 +256 785 724 420</p>
  <p style="margin-top:0.45rem;opacity:0.45;">© 2025 MedLink VA. All rights reserved.</p>
</footer>

<!-- POPUP MODAL -->
<div class="modal-overlay" id="modalOverlay" onclick="handleOverlay(event)">
  <div class="modal">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <div id="formContent">
      <div class="modal-top">
        <div class="modal-icon">🩺</div>
        <h2>Book Your Free Consultation</h2>
        <p class="modal-sub">Lock in your <strong style="color:var(--teal-light)">$450/month</strong> rate before the offer expires. We'll reach out within 24 hours.</p>
      </div>
      <div class="form-row">
        <div class="form-group"><label>First Name *</label><input type="text" id="m_first" placeholder="Jane"></div>
        <div class="form-group"><label>Last Name *</label><input type="text" id="m_last" placeholder="Smith"></div>
      </div>
      <div class="form-group"><label>Email Address *</label><input type="email" id="m_email" placeholder="jane@yourpractice.com"></div>
      <div class="form-group"><label>Phone / WhatsApp *</label><input type="tel" id="m_phone" placeholder="+1 000 000 0000"></div>
      <div class="form-group"><label>Practice / Organisation</label><input type="text" id="m_practice" placeholder="Your Clinic Name"></div>
      <div class="form-group">
        <label>Primary Service Needed</label>
        <select id="m_service">
          <option value="">Select a service...</option>
          <option>Email &amp; Calendar Management</option>
          <option>Appointment Scheduling / Setting</option>
          <option>Customer Service</option>
          <option>EHR Data Entry</option>
          <option>Remote Patient Monitoring</option>
          <option>All Services (Complete Package)</option>
        </select>
      </div>
      <div class="form-group"><label>Additional Notes</label><textarea id="m_notes" placeholder="Tell us more about your needs..." rows="3"></textarea></div>
      <button class="submit-btn" id="m_submitBtn" onclick="submitModal()">Submit &amp; Claim My Rate 🎉</button>
    </div>
    <div class="success-message" id="successMessage">
      <div class="success-icon">🎉</div>
      <h3>You're All Set!</h3>
      <p>Thank you! Your consultation request has been prepared. Your email client will open so you can send your details directly to MedLink VA at <strong style="color:var(--teal-light)">medlinkva@gmail.com</strong>. We'll confirm your $450/month rate within 24 hours.</p>
    </div>
  </div>
</div>

<script>
// COUNTDOWN
(function(){
  let deadline = parseInt(localStorage.getItem('mlv_dl') || '0');
  if(!deadline || deadline < Date.now()){
    deadline = Date.now() + 48*3600*1000;
    localStorage.setItem('mlv_dl', deadline);
  }
  function tick(){
    const left = deadline - Date.now();
    if(left <= 0){
      ['hours','mins','secs'].forEach(id=> document.getElementById(id).textContent='00');
      document.getElementById('bannerTimer').textContent='00:00:00';
      return;
    }
    const h=Math.floor(left/3600000), m=Math.floor((left%3600000)/60000), s=Math.floor((left%60000)/1000);
    const p=n=>String(n).padStart(2,'0');
    document.getElementById('hours').textContent=p(h);
    document.getElementById('mins').textContent=p(m);
    document.getElementById('secs').textContent=p(s);
    document.getElementById('bannerTimer').textContent=`${p(h)}:${p(m)}:${p(s)}`;
  }
  tick(); setInterval(tick,1000);
})();

// MODAL
function openModal(){ document.getElementById('modalOverlay').classList.add('active'); document.body.style.overflow='hidden'; }
function closeModal(){ document.getElementById('modalOverlay').classList.remove('active'); document.body.style.overflow=''; }
function handleOverlay(e){ if(e.target===document.getElementById('modalOverlay')) closeModal(); }

// MODAL SUBMIT → mailto to medlinkva@gmail.com
function submitModal(){
  const first=document.getElementById('m_first').value.trim();
  const last=document.getElementById('m_last').value.trim();
  const email=document.getElementById('m_email').value.trim();
  const phone=document.getElementById('m_phone').value.trim();
  const practice=document.getElementById('m_practice').value.trim();
  const service=document.getElementById('m_service').value;
  const notes=document.getElementById('m_notes').value.trim();
  if(!first||!last||!email||!phone){ alert('Please fill in all required fields (*)'); return; }
  const btn=document.getElementById('m_submitBtn');
  btn.disabled=true; btn.textContent='Processing...';
  const subj=encodeURIComponent(`New Consultation Request – ${first} ${last}`);
  const body=encodeURIComponent(`NEW CONSULTATION REQUEST – MedLink VA\n\nName: ${first} ${last}\nEmail: ${email}\nPhone: ${phone}\nPractice: ${practice||'N/A'}\nService: ${service||'Not specified'}\nNotes: ${notes||'N/A'}\n\n---\nSubmitted via MedLink VA Website`);
  setTimeout(()=>{
    window.location.href=`mailto:medlinkva@gmail.com?subject=${subj}&body=${body}`;
    document.getElementById('formContent').style.display='none';
    document.getElementById('successMessage').classList.add('show');
    btn.disabled=false; btn.textContent='Submit & Claim My Rate 🎉';
  },600);
}

// CONTACT FORM SUBMIT → mailto to medlinkva@gmail.com
function submitContactForm(e){
  e.preventDefault();
  const first=document.getElementById('cf_first').value.trim();
  const last=document.getElementById('cf_last').value.trim();
  const email=document.getElementById('cf_email').value.trim();
  const phone=document.getElementById('cf_phone').value.trim();
  const msg=document.getElementById('cf_msg').value.trim();
  const btn=document.getElementById('cfBtn');
  const fb=document.getElementById('cfFeedback');
  btn.disabled=true; btn.textContent='Sending...';
  const subj=encodeURIComponent(`Website Message – ${first} ${last}`);
  const body=encodeURIComponent(`NEW MESSAGE – MedLink VA Website\n\nName: ${first} ${last}\nEmail: ${email}\nPhone: ${phone||'N/A'}\nMessage: ${msg||'N/A'}\n\n---\nSent via MedLink VA Contact Form`);
  setTimeout(()=>{
    window.location.href=`mailto:medlinkva@gmail.com?subject=${subj}&body=${body}`;
    btn.textContent='✓ Message Prepared!';
    fb.style.display='block';
    fb.textContent="Your message will open in your email client. We'll respond within 24 hours!";
  },600);
}

// MOBILE MENU
function toggleMenu(){ document.getElementById('mobileNav').classList.toggle('open'); }
function closeMenu(){ document.getElementById('mobileNav').classList.remove('open'); }

// SCROLL REVEAL
const obs=new IntersectionObserver((entries)=>{
  entries.forEach((entry,i)=>{ if(entry.isIntersecting) setTimeout(()=>entry.target.classList.add('visible'),i*70); });
},{threshold:0.1});
document.querySelectorAll('.reveal').forEach(el=>obs.observe(el));

// AUTO POPUP after 7s
setTimeout(()=>{ if(!document.getElementById('modalOverlay').classList.contains('active')) openModal(); },7000);
</script>
</body>
</html>
