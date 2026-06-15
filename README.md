<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>0xOverClock — Steam Catalog</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Rajdhani:wght@400;600;700&family=Share+Tech+Mono&family=Inter:wght@400;500;600&display=swap');

  *{margin:0;padding:0;box-sizing:border-box}
  :root{
    --red:#e8000e;--red-dark:#9c0009;--red-glow:rgba(232,0,14,0.3);
    --bg:#0a0a0a;--surface:#111;--surface2:#1a1a1a;--surface3:#222;
    --border:#2a2a2a;--border-red:rgba(232,0,14,0.4);
    --text:#f0f0f0;--muted:#777;--mono:'Share Tech Mono',monospace;
    --display:'Rajdhani',sans-serif;--body:'Inter',sans-serif;
  }

  body{background:var(--bg);color:var(--text);font-family:var(--body);min-height:100vh;overflow-x:hidden}

  /* SCANLINE OVERLAY */
  body::before{
    content:'';position:fixed;top:0;left:0;width:100%;height:100%;
    background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,0.05) 2px,rgba(0,0,0,0.05) 4px);
    pointer-events:none;z-index:0;
  }

  /* HERO */
  .hero{
    position:relative;text-align:center;padding:60px 24px 40px;
    border-bottom:1px solid var(--border-red);overflow:hidden;
  }
  .hero::before{
    content:'';position:absolute;bottom:0;left:50%;transform:translateX(-50%);
    width:80%;height:1px;background:linear-gradient(90deg,transparent,var(--red),transparent);
  }
  .hero-bg{
    position:absolute;inset:0;
    background:radial-gradient(ellipse 60% 60% at 50% 100%,rgba(232,0,14,0.08),transparent);
    pointer-events:none;
  }

  .logo-wrap{display:flex;align-items:center;justify-content:center;gap:16px;margin-bottom:8px}
  .logo-box{
    width:54px;height:54px;background:var(--red);border-radius:8px;
    display:flex;align-items:center;justify-content:center;
    font-family:var(--display);font-weight:700;font-size:22px;color:#fff;
    letter-spacing:-1px;flex-shrink:0;
    box-shadow:0 0 20px var(--red-glow);
  }
  .brand-name{font-family:var(--display);font-size:42px;font-weight:700;letter-spacing:2px;line-height:1}
  .brand-0x{color:var(--red)}
  .brand-rest{color:#fff}

  .tagline{font-family:var(--mono);font-size:11px;color:var(--red);letter-spacing:3px;text-transform:uppercase;margin-bottom:4px}
  .sub{font-size:13px;color:var(--muted);margin-bottom:28px}

  /* BADGES */
  .badge-row{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin-bottom:28px}
  .badge{
    display:inline-flex;align-items:center;gap:6px;
    padding:6px 14px;border-radius:4px;font-size:12px;font-weight:500;
    border:1px solid;font-family:var(--mono);letter-spacing:0.5px;
    text-decoration:none;transition:all 0.2s;cursor:pointer;
  }
  .badge-red{background:rgba(232,0,14,0.1);border-color:var(--red);color:var(--red)}
  .badge-red:hover{background:var(--red);color:#fff;box-shadow:0 0 16px var(--red-glow)}
  .badge-blue{background:rgba(29,155,240,0.08);border-color:#1d9bf0;color:#1d9bf0}
  .badge-blue:hover{background:#1d9bf0;color:#fff}
  .badge-purple{background:rgba(88,101,242,0.1);border-color:#5865F2;color:#5865F2}
  .badge-purple:hover{background:#5865F2;color:#fff}
  .badge-white{background:rgba(255,255,255,0.05);border-color:#444;color:#ccc}
  .badge-white:hover{background:rgba(255,255,255,0.1);color:#fff}
  .badge svg{width:14px;height:14px;flex-shrink:0}

  /* HOW TO ORDER */
  .how-section{padding:40px 24px;border-bottom:1px solid var(--border);max-width:900px;margin:0 auto}
  .section-label{font-family:var(--mono);font-size:10px;color:var(--red);letter-spacing:3px;text-transform:uppercase;margin-bottom:20px}
  .steps{display:grid;grid-template-columns:repeat(4,1fr);gap:12px}
  .step{
    background:var(--surface);border:1px solid var(--border);border-radius:8px;
    padding:20px 16px;text-align:center;position:relative;
  }
  .step::after{
    content:'→';position:absolute;right:-14px;top:50%;transform:translateY(-50%);
    color:var(--red);font-size:18px;z-index:1;
  }
  .step:last-child::after{display:none}
  .step-num{font-family:var(--mono);font-size:10px;color:var(--red);letter-spacing:2px;margin-bottom:10px}
  .step-icon{font-size:28px;margin-bottom:10px}
  .step-title{font-weight:600;font-size:14px;margin-bottom:4px}
  .step-desc{font-size:12px;color:var(--muted)}

  /* MAIN CATALOG */
  .catalog{padding:0 24px 60px;max-width:1100px;margin:0 auto}
  .catalog-header{display:flex;align-items:center;justify-content:space-between;padding:32px 0 20px;flex-wrap:wrap;gap:12px}
  .catalog-title{font-family:var(--display);font-size:28px;font-weight:700;letter-spacing:1px}
  .count-badge{background:var(--red);color:#fff;font-family:var(--mono);font-size:11px;padding:4px 10px;border-radius:4px}

  /* FILTER TABS */
  .filters{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:28px}
  .filter-btn{
    padding:6px 14px;border-radius:4px;font-size:12px;font-family:var(--mono);
    border:1px solid var(--border);background:var(--surface);color:var(--muted);
    cursor:pointer;transition:all 0.2s;letter-spacing:0.5px;
  }
  .filter-btn:hover,.filter-btn.active{border-color:var(--red);color:var(--red);background:rgba(232,0,14,0.08)}
  .filter-btn.active{background:rgba(232,0,14,0.15)}

  /* SEARCH */
  .search-wrap{position:relative;margin-bottom:24px}
  .search-wrap svg{position:absolute;left:12px;top:50%;transform:translateY(-50%);color:var(--muted)}
  #search{
    width:100%;padding:10px 12px 10px 38px;background:var(--surface);
    border:1px solid var(--border);border-radius:6px;color:var(--text);
    font-family:var(--body);font-size:14px;outline:none;transition:border 0.2s;
  }
  #search:focus{border-color:var(--red)}
  #search::placeholder{color:var(--muted)}

  /* GRID */
  .games-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:10px}
  .game-card{
    background:var(--surface);border:1px solid var(--border);border-radius:8px;
    padding:14px 16px;display:flex;align-items:flex-start;gap:10px;
    transition:all 0.2s;cursor:default;
    animation:fadeUp 0.3s ease both;
  }
  .game-card:hover{border-color:var(--border-red);background:var(--surface2);transform:translateY(-1px)}
  .game-dot{width:8px;height:8px;border-radius:50%;background:var(--red);flex-shrink:0;margin-top:5px;box-shadow:0 0 6px var(--red-glow)}
  .game-name{font-size:13px;font-weight:500;line-height:1.4;color:var(--text)}
  .game-card.hidden{display:none}

  /* CATEGORY HEADING */
  .cat-heading{
    grid-column:1/-1;display:flex;align-items:center;gap:12px;
    padding:8px 0;margin-top:16px;
  }
  .cat-heading:first-child{margin-top:0}
  .cat-line{flex:1;height:1px;background:var(--border)}
  .cat-name{font-family:var(--mono);font-size:11px;color:var(--red);letter-spacing:2px;text-transform:uppercase;white-space:nowrap}

  /* FOOTER */
  .footer{
    background:var(--surface);border-top:1px solid var(--border-red);
    padding:40px 24px;text-align:center;position:relative;overflow:hidden;
  }
  .footer::before{
    content:'';position:absolute;top:0;left:50%;transform:translateX(-50%);
    width:60%;height:1px;background:linear-gradient(90deg,transparent,var(--red),transparent);
  }
  .footer-brand{font-family:var(--display);font-size:32px;font-weight:700;letter-spacing:3px;margin-bottom:4px}
  .footer-sub{font-family:var(--mono);font-size:10px;color:var(--muted);letter-spacing:2px;margin-bottom:24px}
  .footer-btns{display:flex;flex-wrap:wrap;gap:10px;justify-content:center}

  /* NO RESULTS */
  .no-results{
    grid-column:1/-1;padding:60px;text-align:center;
    color:var(--muted);font-family:var(--mono);font-size:13px;letter-spacing:1px;
    display:none;
  }
  .no-results.show{display:block}

  @keyframes fadeUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}

  /* TICKER */
  .ticker{background:var(--red);overflow:hidden;white-space:nowrap;padding:7px 0}
  .ticker-inner{display:inline-block;animation:ticker 30s linear infinite;font-family:var(--mono);font-size:11px;color:#fff;letter-spacing:1px}
  @keyframes ticker{0%{transform:translateX(0)}100%{transform:translateX(-50%)}}

  @media(max-width:600px){
    .steps{grid-template-columns:1fr 1fr}
    .step::after{display:none}
    .brand-name{font-size:28px}
  }
</style>
</head>
<body>

<div class="ticker">
  <span class="ticker-inner">
    🎮 0xOVERCLOCK &nbsp;•&nbsp; PLAY MORE. PAY LESS. &nbsp;•&nbsp; 500+ GAMES &nbsp;•&nbsp; INSTANT DELIVERY &nbsp;•&nbsp; TRUSTED BY GAMERS &nbsp;•&nbsp; DM ON FACEBOOK OR DISCORD &nbsp;•&nbsp; 0xOVERCLOCK &nbsp;•&nbsp; PLAY MORE. PAY LESS. &nbsp;•&nbsp; 500+ GAMES &nbsp;•&nbsp; INSTANT DELIVERY &nbsp;•&nbsp; TRUSTED BY GAMERS &nbsp;•&nbsp; DM ON FACEBOOK OR DISCORD &nbsp;•&nbsp;
  </span>
</div>

<div class="hero">
  <div class="hero-bg"></div>
  <div style="position:relative;z-index:1">
    <div class="logo-wrap">
      <div class="logo-box">0x</div>
      <div class="brand-name"><span class="brand-0x">0x</span><span class="brand-rest">OVERCLOCK</span></div>
    </div>
    <div class="tagline">Steam Game Catalog</div>
    <div class="sub">500+ Games &nbsp;·&nbsp; Multiple Accounts &nbsp;·&nbsp; Instant Delivery &nbsp;·&nbsp; Trusted Since Day One</div>
    <div class="badge-row">
      <a href="https://www.facebook.com/0xoverclockofficial" target="_blank" class="badge badge-blue">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/></svg>
        Facebook
      </a>
      <a href="https://discord.gg/KNmw8Ayj" target="_blank" class="badge badge-purple">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0 12.64 12.64 0 0 0-.617-1.25.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057.1 18.08.114 18.102.132 18.116a19.9 19.9 0 0 0 5.993 3.03.078.078 0 0 0 .084-.028c.462-.63.874-1.295 1.226-1.994a.076.076 0 0 0-.041-.106 13.107 13.107 0 0 1-1.872-.892.077.077 0 0 1-.008-.128 10.2 10.2 0 0 0 .372-.292.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127 12.299 12.299 0 0 1-1.873.892.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028 19.839 19.839 0 0 0 6.002-3.03.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03zM8.02 15.33c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.956-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.956 2.418-2.157 2.418zm7.975 0c-1.183 0-2.157-1.085-2.157-2.419 0-1.333.955-2.419 2.157-2.419 1.21 0 2.176 1.096 2.157 2.42 0 1.333-.946 2.418-2.157 2.418z"/></svg>
        Discord — 0xsniffa
      </a>
      <a href="https://www.instagram.com/0xOverClock" target="_blank" class="badge badge-red">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"/></svg>
        Instagram
      </a>
      <span class="badge badge-white">
        🎮 500+ Games Available
      </span>
    </div>
  </div>
</div>

<div class="how-section">
  <div class="section-label">// How to Order</div>
  <div class="steps">
    <div class="step">
      <div class="step-num">01 /</div>
      <div class="step-icon">🔍</div>
      <div class="step-title">Find Your Game</div>
      <div class="step-desc">Browse the catalog below and pick your title</div>
    </div>
    <div class="step">
      <div class="step-num">02 /</div>
      <div class="step-icon">💬</div>
      <div class="step-title">DM Admin</div>
      <div class="step-desc">Message on Facebook, Discord, or Instagram</div>
    </div>
    <div class="step">
      <div class="step-num">03 /</div>
      <div class="step-icon">💳</div>
      <div class="step-title">Send Payment</div>
      <div class="step-desc">Pay via method shared by admin after confirmation</div>
    </div>
    <div class="step">
      <div class="step-num">04 /</div>
      <div class="step-icon">🎮</div>
      <div class="step-title">Get Access</div>
      <div class="step-desc">Credentials delivered instantly after payment</div>
    </div>
  </div>
</div>

<div class="catalog">
  <div class="catalog-header">
    <div>
      <div class="section-label">// Game Catalog</div>
      <div class="catalog-title">Available Titles <span class="count-badge" id="count-display">500+ Games</span></div>
    </div>
  </div>

  <div class="search-wrap">
    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
    <input type="text" id="search" placeholder="Search games..." oninput="filterGames()">
  </div>

  <div class="filters" id="filters"></div>

  <div class="games-grid" id="grid">
    <div class="no-results" id="no-results">// No games found matching your search</div>
  </div>
</div>

<div class="footer">
  <div class="footer-brand"><span style="color:var(--red)">0x</span>OVERCLOCK</div>
  <div class="footer-sub">PLAY MORE &nbsp;·&nbsp; PAY LESS &nbsp;·&nbsp; TRUSTED BY GAMERS</div>
  <div class="footer-btns">
    <a href="https://www.facebook.com/0xoverclockofficial" target="_blank" class="badge badge-blue">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/></svg>
      Order on Facebook
    </a>
    <a href="https://discord.gg/KNmw8Ayj" target="_blank" class="badge badge-purple">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M20.317 4.37a19.791 19.791 0 0 0-4.885-1.515.074.074 0 0 0-.079.037c-.21.375-.444.864-.608 1.25a18.27 18.27 0 0 0-5.487 0 12.64 12.64 0 0 0-.617-1.25.077.077 0 0 0-.079-.037A19.736 19.736 0 0 0 3.677 4.37a.07.07 0 0 0-.032.027C.533 9.046-.32 13.58.099 18.057.1 18.08.114 18.102.132 18.116a19.9 19.9 0 0 0 5.993 3.03.078.078 0 0 0 .084-.028c.462-.63.874-1.295 1.226-1.994a.076.076 0 0 0-.041-.106 13.107 13.107 0 0 1-1.872-.892.077.077 0 0 1-.008-.128 10.2 10.2 0 0 0 .372-.292.074.074 0 0 1 .077-.01c3.928 1.793 8.18 1.793 12.062 0a.074.074 0 0 1 .078.01c.12.098.246.198.373.292a.077.077 0 0 1-.006.127 12.299 12.299 0 0 1-1.873.892.077.077 0 0 0-.041.107c.36.698.772 1.362 1.225 1.993a.076.076 0 0 0 .084.028 19.839 19.839 0 0 0 6.002-3.03.077.077 0 0 0 .032-.054c.5-5.177-.838-9.674-3.549-13.66a.061.061 0 0 0-.031-.03z"/></svg>
      Discord — 0xsniffa
    </a>
    <a href="https://www.instagram.com/0xOverClock" target="_blank" class="badge badge-red">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 0 0 0-12.324zM12 16a4 4 0 1 1 0-8 4 4 0 0 1 0 8zm6.406-11.845a1.44 1.44 0 1 0 0 2.881 1.44 1.44 0 0 0 0-2.881z"/></svg>
      Instagram
    </a>
  </div>
</div>

<script>
const CATALOG = {
  "GTA & Open World": ["Grand Theft Auto V","GTA V Legacy + Enhanced","GTA: San Andreas","GTA IV","Red Dead Redemption 2","Red Dead Redemption 2 Ultimate Edition","Cyberpunk 2077","Cyberpunk 2077: Phantom Liberty","Watch Dogs","Battlefield 2042"],
  "Racing & Driving": ["Forza Horizon 4","Forza Horizon 5","Euro Truck Simulator 2","American Truck Simulator","Assetto Corsa","BeamNG.drive","City Car Driving","Need for Speed: Most Wanted","Need for Speed: Heat","Need for Speed: Rivals","Need for Speed: Unbound","DiRT Rally","FlatOut 2","GRID 2"],
  "Action & Adventure": ["Elden Ring","Elden Ring + Nightreign","Black Myth: Wukong","God of War (2018)","God of War Ragnarök","Dark Souls III","Dark Souls Remastered","Dying Light","Dying Light 2","Dying Light: The Beast","Ghost of Tsushima","Kingdom Come: Deliverance","Kingdom Come: Deliverance II","Lies of P","Mad Max","Rise of the Ronin","Ghostrunner 1","Ghostrunner 2","Batman: Arkham Origins","Batman series","Injustice 2","Mortal Kombat 1","Mortal Kombat 11","Mortal Kombat X","TEKKEN 7","Stellar Blade","Wo Long: Fallen Dynasty","SYSTEM SHOCK 2 REMASTER","Borderlands 4","Ready or Not","The Witcher 3: Wild Hunt","Portal 2","Sekiro: Shadows Die Twice"],
  "Horror & Survival": ["Resident Evil Village","Resident Evil 4 Remake","Resident Evil 2 Remake","Resident Evil 3 Remake","Resident Evil 7 Biohazard","Resident Evil Requiem","Resident Evil 0 & 1","Resident Evil Re:Verse","Silent Hill 2 Remake","Silent Hill F","S.T.A.L.K.E.R. 2: Heart of Chornobyl","S.T.A.L.K.E.R. Trilogy","Outlast","Outlast 2","Dead by Daylight","Phasmophobia","Project Zomboid","DayZ"],
  "Shooters & War": ["Call of Duty: Modern Warfare (2019)","Call of Duty: Modern Warfare 2 (2022)","Call of Duty: Modern Warfare 3","Call of Duty: Black Ops","Call of Duty: Black Ops 2","Call of Duty: Cold War","Call of Duty: World at War","Call of Duty: WWII","Call of Duty: Ghosts","Call of Duty: Infinite Warfare","Call of Duty 4: Modern Warfare","Battlefield 4","Battlefield V","DOOM Eternal","DOOM: The Dark Ages","DOOM 64","Rainbow Six Siege","HELLDIVER 1 & 2","Deep Rock Galactic","Sea of Thieves","Ghost Recon: Breakpoint","Ghost Recon: Wildlands","Arma 3","SUPERHOT + Mind Control Delete","Delta Force","Killing Floor","SCUM"],
  "Survival & Sandbox": ["The Forest","Sons of the Forest","7 Days to Die","Subnautica","Subnautica: Below Zero","Rust","Valheim","Raft","Green Hell","ARK: Survival Evolved","ARK: Survival Ascended","Terraria","Only Up","It Takes Two","Content Warning","Lethal Company","R.E.P.O.","A Plague Tale: Innocence","A Plague Tale: Requiem","Stardew Valley","Don't Starve","Don't Starve Together","Manor Lords","Minecraft Dungeons"],
  "Strategy & RPG": ["Baldur's Gate 3","Hogwarts Legacy","Hogwarts Legacy Deluxe","Fallout 4","Fallout: New Vegas","Fallout 76","Skyrim Special Edition","Hearts of Iron IV","Civilization V","Civilization VI","Victoria 3","Age of Wonders 4","Company of Heroes","Company of Heroes 2","Warhammer 40,000: Space Marine 2","Warhammer: Vermintide 2","Metro 2033 Redux","Metro: Last Light","Metro Exodus","Half-Life 2","Half-Life: Alyx","Mafia: Definitive Edition","Mafia II: Definitive Edition","Mafia III: Definitive Edition","Mafia: The Old Country","Cities: Skylines II","Factorio","Northgard"],
  "Story & Narrative": ["The Last of Us Part I","The Last of Us Part II Remastered","Detroit: Become Human","Heavy Rain","Beyond: Two Souls","Marvel's Spider-Man 2","Marvel's Spider-Man Remastered","Marvel's Spider-Man: Miles Morales","Assassin's Creed Shadows","Assassin's Creed Valhalla","Assassin's Creed Origins","Assassin's Creed Mirage","Uncharted: Legacy of Thieves Collection","MiSide","Stray","Life is Strange","Life is Strange 2","Days Gone","Tomb Raider Trilogy","Rise of the Tomb Raider","Shadow of the Tomb Raider","Alan Wake","The Walking Dead: Definitive Series","Atomic Heart","Atomic Heart Gold + All DLC","Split Fiction","Dune: Awakening","Sleeping Dogs","Saints Row IV","Just Cause 3","Just Cause 4","Death Stranding"],
  "Co-op & Multiplayer": ["Left 4 Dead 2","Left 4 Dead 1 + 2","Garry's Mod","Among Us","PAYDAY 2","PAYDAY 3","Borderlands 2","Borderlands: The Pre-Sequel","Borderlands 3","Devil May Cry 5","Slime Rancher 1 / 2","TABS","Deep Rock Galactic"],
  "Indie & Casual": ["Geometry Dash","Hollow Knight","Hollow Knight: Silksong","Cuphead","Binding of Isaac Rebirth","Poppy Playtime 1-5","Five Nights at Freddy's: Security Breach","Five Nights at Freddy's: Secret of the Mimic","My Summer Car","House Flipper","Goat Simulator","Schedule I","Supermarket Simulator","Teardown","Inscryption","Oxygen Not Included","RimWorld","Cult of the Lamb","For the King","Hades II","The Henry Stickmin Collection","The Long Dark","Tiny Bunny","Undertale","Deltarune","Little Nightmares 1 / 2 / 3","People Playground","Buckshot Roulette","Fishing Planet"],
  "New Releases 2025": ["Marvel Rivals","Borderlands 4","Resident Evil Requiem","Silent Hill F","Dying Light: The Beast Deluxe","DOOM: The Dark Ages","S.T.A.L.K.E.R. 2","Mafia: The Old Country","Clair Obscur: Expedition 33","Microsoft Flight Simulator 2024","HITMAN World of Assassination","EA SPORTS FC 25","Farming Simulator 25","Elden Ring Nightreign","inZOI","PEAK","R.E.P.O.","Split Fiction"],
};

let activeFilter = 'All';
const grid = document.getElementById('grid');
const filtersEl = document.getElementById('filters');
const noResults = document.getElementById('no-results');
const countDisplay = document.getElementById('count-display');

const allGames = Object.values(CATALOG).flat();
const uniqueGames = [...new Set(allGames)];

function buildFilters() {
  const cats = ['All', ...Object.keys(CATALOG)];
  cats.forEach(cat => {
    const btn = document.createElement('button');
    btn.className = 'filter-btn' + (cat === 'All' ? ' active' : '');
    btn.textContent = cat === 'All' ? 'All Games' : cat;
    btn.onclick = () => {
      activeFilter = cat;
      document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      filterGames();
    };
    filtersEl.appendChild(btn);
  });
}

function filterGames() {
  const q = document.getElementById('search').value.toLowerCase().trim();
  grid.innerHTML = '';
  grid.appendChild(noResults);
  noResults.classList.remove('show');

  let total = 0;
  const seen = new Set();

  const cats = activeFilter === 'All' ? Object.keys(CATALOG) : [activeFilter];
  cats.forEach((cat, ci) => {
    const games = CATALOG[cat];
    const matching = games.filter(g => {
      if (seen.has(g.toLowerCase())) return false;
      if (q && !g.toLowerCase().includes(q)) return false;
      seen.add(g.toLowerCase());
      return true;
    });
    if (!matching.length) return;

    if (activeFilter === 'All') {
      const heading = document.createElement('div');
      heading.className = 'cat-heading';
      heading.innerHTML = `<div class="cat-line"></div><div class="cat-name">${cat}</div><div class="cat-line"></div>`;
      grid.appendChild(heading);
    }

    matching.forEach((g, i) => {
      const card = document.createElement('div');
      card.className = 'game-card';
      card.style.animationDelay = (i * 0.02) + 's';
      card.innerHTML = `<div class="game-dot"></div><div class="game-name">${g}</div>`;
      grid.appendChild(card);
      total++;
    });
  });

  countDisplay.textContent = total + ' Games';
  if (total === 0) noResults.classList.add('show');
}

buildFilters();
filterGames();
</script>
</body>
</html>
