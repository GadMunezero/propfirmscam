<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PropFirmScam — Prop firm intelligence platform</title>
<meta name="description" content="Independent prop firm research: rules, payouts, leadership, and health scores — sourced and dated, not paid placement.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=IBM+Plex+Sans:wght@400;500;600&family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#0B0D10;
    --bg-2:#0E1013;
    --panel:#14171C;
    --panel-2:#1B1F26;
    --panel-3:#20242C;
    --line:#262B33;
    --line-soft:#1D2129;
    --amber:#E8A33D;
    --amber-dim:#8a6224;
    --amber-soft:rgba(232,163,61,0.08);
    --text:#E7E5DF;
    --text-dim:#8A8F98;
    --text-faint:#5B6069;
    --danger:#E2574C;
    --success:#4FBF7B;
    --warn:#E8C33D;
    --blue:#6FB8E0;
  }
  *{box-sizing:border-box; margin:0; padding:0;}
  html{scroll-behavior:smooth;}
  body{
    background:
      radial-gradient(1100px 520px at 12% -8%, rgba(232,163,61,0.05), transparent 60%),
      radial-gradient(900px 500px at 100% 0%, rgba(111,184,224,0.035), transparent 55%),
      var(--bg);
    color:var(--text);
    font-family:'IBM Plex Sans', sans-serif;
    line-height:1.5;
    -webkit-font-smoothing:antialiased;
    min-height:100vh;
  }
  h1,h2,h3,h4{font-family:'Space Grotesk', sans-serif; font-weight:600; letter-spacing:-0.01em;}
  .mono{font-family:'IBM Plex Mono', monospace;}
  a{color:inherit; cursor:pointer;}
  button{font-family:inherit; cursor:pointer;}
  .wrap{max-width:1180px; margin:0 auto; padding:0 24px;}
  ::selection{background:var(--amber); color:#0B0D10;}
  :focus-visible{outline:2px solid var(--amber); outline-offset:2px; border-radius:3px;}
  .sr-only{position:absolute; width:1px; height:1px; overflow:hidden; clip:rect(0,0,0,0);}

  /* ---------- Ticker ---------- */
  .ticker-bar{
    position:sticky; top:0; z-index:60;
    background:#0E1013; border-bottom:1px solid var(--line);
    overflow:hidden; white-space:nowrap;
    height:36px; display:flex; align-items:center;
  }
  .ticker-track{
    display:inline-flex; gap:48px; padding-left:100%;
    animation:scrollTicker 46s linear infinite;
  }
  .ticker-bar:hover .ticker-track{animation-play-state:paused;}
  @keyframes scrollTicker{ from{transform:translateX(0);} to{transform:translateX(-100%);} }
  .ticker-item{font-family:'IBM Plex Mono', monospace; font-size:12.5px; color:var(--text-dim); display:inline-flex; gap:8px; align-items:center; text-decoration:none;}
  .ticker-item:hover{color:var(--amber);}
  .ticker-item b{color:var(--text); font-weight:500;}
  .tick-up{color:var(--success);}
  .tick-down{color:var(--danger);}
  .tick-flat{color:var(--warn);}

  /* ---------- Nav ---------- */
  header.nav{
    position:sticky; top:36px; z-index:59;
    background:rgba(11,13,16,0.88); backdrop-filter:blur(10px) saturate(1.1);
    border-bottom:1px solid var(--line);
  }
  nav{display:flex; align-items:center; justify-content:space-between; gap:16px; padding:14px 24px; max-width:1180px; margin:0 auto;}
  .logo{display:flex; align-items:center; gap:8px; font-family:'Space Grotesk'; font-weight:700; font-size:18px; text-decoration:none; flex-shrink:0;}
  .logo .dot{width:8px; height:8px; background:var(--amber); border-radius:1px; display:inline-block;}
  .navlinks{display:flex; gap:22px; font-size:13.5px; color:var(--text-dim); align-items:center;}
  .navlinks a{text-decoration:none; transition:color .15s; padding:4px 2px; border-bottom:1px solid transparent;}
  .navlinks a:hover{color:var(--amber);}
  .navlinks a.active{color:var(--amber); border-bottom-color:var(--amber-dim);}
  .nav-right{display:flex; align-items:center; gap:10px;}
  .nav-search-btn{display:flex; align-items:center; gap:8px; background:var(--panel); border:1px solid var(--line); color:var(--text-dim); padding:8px 12px; border-radius:6px; font-size:12.5px; font-family:'IBM Plex Mono';}
  .nav-search-btn:hover{border-color:var(--amber-dim); color:var(--text);}
  .hamburger{display:none; background:none; border:1px solid var(--line); border-radius:6px; padding:8px 10px; color:var(--text);}
  @media (max-width:900px){
    .navlinks{display:none;}
    .hamburger{display:flex;}
  }
  .mobile-menu{display:none; flex-direction:column; border-top:1px solid var(--line); background:var(--bg-2);}
  .mobile-menu.open{display:flex;}
  .mobile-menu a{padding:14px 24px; border-bottom:1px solid var(--line-soft); text-decoration:none; color:var(--text-dim); font-size:14px;}
  .mobile-menu a.active{color:var(--amber);}

  /* ---------- Search overlay ---------- */
  .search-overlay{position:fixed; inset:0; background:rgba(8,9,11,0.72); backdrop-filter:blur(4px); z-index:100; display:none; align-items:flex-start; justify-content:center; padding:12vh 20px 20px;}
  .search-overlay.open{display:flex;}
  .search-modal{width:100%; max-width:620px; background:var(--panel); border:1px solid var(--line); border-radius:10px; box-shadow:0 24px 60px rgba(0,0,0,0.5); overflow:hidden;}
  .search-modal-input{width:100%; background:var(--panel-2); border:none; border-bottom:1px solid var(--line); color:var(--text); padding:18px 20px; font-size:16px; font-family:'IBM Plex Sans';}
  .search-modal-input:focus{outline:none;}
  .search-modal-body{max-height:60vh; overflow-y:auto; padding:8px;}
  .search-cat-label{font-family:'IBM Plex Mono'; font-size:11px; text-transform:uppercase; letter-spacing:.06em; color:var(--amber-dim); padding:10px 12px 4px;}
  .search-result-row{display:flex; justify-content:space-between; align-items:center; padding:10px 12px; border-radius:6px; text-decoration:none; color:var(--text);}
  .search-result-row:hover{background:var(--panel-2);}
  .search-result-row .r-sub{color:var(--text-dim); font-size:12px; font-family:'IBM Plex Mono';}
  .search-empty{padding:24px; text-align:center; color:var(--text-dim); font-size:13.5px;}
  .search-hint{padding:10px 20px; font-size:11.5px; color:var(--text-faint); font-family:'IBM Plex Mono'; border-top:1px solid var(--line);}

  /* ---------- Breadcrumb ---------- */
  .crumbs{display:flex; gap:6px; align-items:center; font-family:'IBM Plex Mono'; font-size:12px; color:var(--text-faint); padding:18px 0 0;}
  .crumbs a{text-decoration:none; color:var(--text-dim);}
  .crumbs a:hover{color:var(--amber);}

  /* ---------- Hero ---------- */
  .hero{padding:64px 0 48px; border-bottom:1px solid var(--line); position:relative;}
  .eyebrow{font-family:'IBM Plex Mono'; font-size:12px; letter-spacing:0.12em; text-transform:uppercase; color:var(--amber); margin-bottom:18px; display:flex; align-items:center; gap:10px;}
  .eyebrow::before{content:''; width:20px; height:1px; background:var(--amber);}
  .hero h1{font-size:clamp(32px,5vw,54px); line-height:1.05; max-width:760px; margin-bottom:20px;}
  .hero h1 em{font-style:normal; color:var(--amber);}
  .hero p.sub{color:var(--text-dim); max-width:560px; font-size:16.5px; margin-bottom:32px;}
  .search-row{display:flex; gap:10px; max-width:640px; flex-wrap:wrap; position:relative;}
  .search-input{
    flex:1; min-width:240px; background:var(--panel); border:1px solid var(--line); color:var(--text);
    padding:15px 16px; border-radius:6px; font-size:15px; font-family:'IBM Plex Sans';
  }
  .search-input::placeholder{color:var(--text-dim);}
  .btn{
    font-family:'IBM Plex Mono'; font-size:13.5px; font-weight:500; letter-spacing:0.01em;
    padding:14px 20px; border-radius:6px; border:1px solid transparent; cursor:pointer;
    transition:all .15s; text-decoration:none; display:inline-flex; align-items:center; gap:8px;
  }
  .btn-primary{background:var(--amber); color:#0B0D10;}
  .btn-primary:hover{background:#f0b256; transform:translateY(-1px);}
  .btn-ghost{background:transparent; border:1px solid var(--line); color:var(--text);}
  .btn-ghost:hover{border-color:var(--amber); color:var(--amber);}
  .btn-sm{padding:8px 14px; font-size:12px;}
  .hero-stats{display:flex; gap:40px; margin-top:48px; flex-wrap:wrap;}
  .stat b{display:block; font-family:'Space Grotesk'; font-size:26px;}
  .stat span{color:var(--text-dim); font-size:12.5px; font-family:'IBM Plex Mono'; text-transform:uppercase; letter-spacing:.06em;}

  .scam-banner{
    margin-top:32px; max-width:680px; background:rgba(226,87,76,0.07); border:1px solid rgba(226,87,76,0.3);
    border-radius:8px; padding:14px 16px; font-size:13.5px; display:flex; gap:10px; align-items:flex-start;
  }
  .scam-banner b{color:var(--danger);}
  .scam-banner a{color:var(--danger); text-decoration:underline;}
  .data-note{margin-top:14px; max-width:680px; font-size:11.5px; color:var(--text-faint); font-family:'IBM Plex Mono'; line-height:1.6;}

  /* ---------- Section shell ---------- */
  section{padding:64px 0; border-bottom:1px solid var(--line);}
  .section-head{display:flex; justify-content:space-between; align-items:flex-end; margin-bottom:32px; gap:20px; flex-wrap:wrap;}
  .section-head .num{font-family:'IBM Plex Mono'; color:var(--amber-dim); font-size:13px; margin-bottom:8px;}
  .section-head h2{font-size:28px;}
  .section-head p{color:var(--text-dim); font-size:14.5px; max-width:480px;}
  .cat-tabs{display:flex; gap:6px; flex-wrap:wrap;}
  .cat-tab{font-family:'IBM Plex Mono'; font-size:12.5px; padding:8px 14px; border-radius:6px; border:1px solid var(--line); background:var(--panel); color:var(--text-dim); cursor:pointer; transition:all .12s;}
  .cat-tab:hover{border-color:var(--amber-dim);}
  .cat-tab.active{border-color:var(--amber); color:var(--amber); background:var(--amber-soft);}
  .cat-badge{font-family:'IBM Plex Mono'; font-size:10.5px; text-transform:uppercase; padding:2px 7px; border-radius:4px; letter-spacing:.04em;}
  .cat-futures{background:rgba(79,191,123,0.1); color:var(--success);}
  .cat-cfd{background:rgba(111,184,224,0.12); color:var(--blue);}

  /* ---------- Verification pills ---------- */
  .vpill{font-family:'IBM Plex Mono'; font-size:10px; text-transform:uppercase; letter-spacing:.04em; padding:3px 8px; border-radius:4px; display:inline-flex; align-items:center; gap:4px; white-space:nowrap;}
  .v-verified{background:rgba(79,191,123,0.12); color:var(--success);}
  .v-unverified{background:rgba(232,195,61,0.12); color:var(--warn);}
  .v-editorial{background:rgba(232,163,61,0.1); color:var(--amber);}
  .v-user{background:rgba(111,184,224,0.12); color:var(--blue);}

  .link-firm{color:var(--amber); text-decoration:none; border-bottom:1px solid transparent;}
  .link-firm:hover{border-bottom-color:var(--amber-dim);}

  /* ---------- Firm cards (directory + homepage) ---------- */
  .firm-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(280px,1fr)); gap:16px;}
  .firm-card{
    background:linear-gradient(180deg, var(--panel), var(--panel) 60%, var(--panel-2));
    border:1px solid var(--line); border-radius:12px; padding:22px; text-decoration:none; color:var(--text);
    display:flex; flex-direction:column; gap:12px; transition:transform .15s, border-color .15s, box-shadow .15s;
    position:relative; overflow:hidden;
  }
  .firm-card:hover{transform:translateY(-3px); border-color:var(--amber-dim); box-shadow:0 14px 34px rgba(0,0,0,0.35);}
  .firm-card-top{display:flex; justify-content:space-between; align-items:flex-start; gap:10px;}
  .firm-card-name{font-family:'Space Grotesk'; font-weight:700; font-size:18px;}
  .firm-card-score{font-family:'IBM Plex Mono'; font-size:20px; color:var(--amber); flex-shrink:0;}
  .firm-card-score span{font-size:11px; color:var(--text-dim); display:block; font-weight:400; text-align:right;}
  .firm-card-stats{display:grid; grid-template-columns:1fr 1fr; gap:8px; font-size:12.5px; color:var(--text-dim); font-family:'IBM Plex Mono';}
  .firm-card-stats b{color:var(--text); font-weight:500;}
  .firm-card-flags{display:flex; gap:6px; flex-wrap:wrap;}
  .flag-chip{font-size:11px; font-family:'IBM Plex Mono'; padding:3px 8px; border:1px solid var(--line); border-radius:20px; color:var(--text-dim);}
  .flag-chip.yes{color:var(--success); border-color:rgba(79,191,123,0.3);}
  .firm-card-cta{margin-top:auto; font-family:'IBM Plex Mono'; font-size:12.5px; color:var(--amber); display:flex; align-items:center; gap:6px;}

  /* ---------- Directory filters ---------- */
  .filter-bar{background:var(--panel); border:1px solid var(--line); border-radius:10px; padding:18px 20px; margin-bottom:24px; display:flex; flex-wrap:wrap; gap:14px; align-items:flex-end;}
  .filter-field{display:flex; flex-direction:column; gap:5px;}
  .filter-field label{font-size:11px; font-family:'IBM Plex Mono'; text-transform:uppercase; color:var(--text-dim); letter-spacing:.04em;}
  .filter-field select, .filter-field input{background:var(--panel-2); border:1px solid var(--line); color:var(--text); padding:8px 10px; border-radius:5px; font-size:13px; font-family:'IBM Plex Mono';}
  .filter-toggle{display:flex; align-items:center; gap:6px; font-size:12.5px; color:var(--text-dim); cursor:pointer; user-select:none;}
  .filter-toggle input{accent-color:var(--amber);}
  .filter-count{font-family:'IBM Plex Mono'; font-size:12.5px; color:var(--text-dim); margin-left:auto;}

  /* ---------- Quiz ---------- */
  .quiz-shell{background:var(--panel); border:1px solid var(--line); border-radius:12px; padding:32px; display:grid; grid-template-columns:1.1fr 1fr; gap:32px; box-shadow:0 20px 50px rgba(0,0,0,0.25);}
  @media (max-width:860px){.quiz-shell{grid-template-columns:1fr;}}
  .q-group{margin-bottom:20px;}
  .q-label{font-size:13px; color:var(--text-dim); margin-bottom:10px; font-family:'IBM Plex Mono'; text-transform:uppercase; letter-spacing:.05em;}
  .q-options{display:flex; gap:8px; flex-wrap:wrap;}
  .q-opt{
    padding:9px 14px; border:1px solid var(--line); border-radius:5px; font-size:13.5px; cursor:pointer;
    background:var(--panel-2); transition:all .12s; color:var(--text-dim); user-select:none;
  }
  .q-opt:hover{border-color:var(--amber-dim);}
  .q-opt.active{border-color:var(--amber); color:var(--amber); background:var(--amber-soft);}
  .result-panel{background:var(--panel-2); border:1px solid var(--line); border-radius:10px; padding:22px; display:flex; flex-direction:column; gap:14px;}
  .match-card{border:1px solid var(--line); border-radius:9px; padding:16px; background:var(--panel);}
  .match-card.best{border-color:var(--amber); box-shadow:0 0 0 1px rgba(232,163,61,0.15) inset;}
  .match-top{display:flex; justify-content:space-between; align-items:center; margin-bottom:4px; gap:10px;}
  .match-name{font-family:'Space Grotesk'; font-weight:600; font-size:16px; text-decoration:none; color:var(--text);}
  .match-name:hover{color:var(--amber);}
  .match-score{font-family:'IBM Plex Mono'; color:var(--amber); font-size:15px; flex-shrink:0;}
  .match-reasons{list-style:none; font-size:12.5px; color:var(--text-dim); margin-top:8px; display:flex; flex-direction:column; gap:4px;}
  .match-reasons li::before{content:'✓ '; color:var(--success);}
  .match-concerns{list-style:none; font-size:12.5px; color:var(--text-dim); margin-top:6px; display:flex; flex-direction:column; gap:4px;}
  .match-concerns li::before{content:'⚠ '; color:var(--warn);}
  .match-cta{margin-top:10px; font-size:12.5px; font-family:'IBM Plex Mono'; color:var(--amber); text-decoration:none; display:inline-flex; align-items:center; gap:4px;}
  .avoid-list{margin-top:6px;}
  .avoid-item{font-size:12.5px; color:var(--text-dim); margin-bottom:8px; padding-left:14px; border-left:2px solid var(--danger);}
  .avoid-item b{color:var(--text);}

  /* ---------- Comparison table ---------- */
  .table-scroll{overflow-x:auto; border:1px solid var(--line); border-radius:10px;}
  table{border-collapse:collapse; width:100%; min-width:900px; font-size:13.5px;}
  th,td{padding:12px 16px; text-align:left; border-bottom:1px solid var(--line); white-space:nowrap;}
  thead th{background:var(--panel); font-family:'IBM Plex Mono'; font-size:11.5px; text-transform:uppercase; letter-spacing:.04em; color:var(--text-dim); position:sticky; top:0;}
  tbody tr:hover{background:var(--panel);}
  td.firm-cell{font-family:'Space Grotesk'; font-weight:600; color:var(--text); position:sticky; left:0; background:var(--bg);}
  td.firm-cell a{color:var(--text); text-decoration:none;}
  td.firm-cell a:hover{color:var(--amber);}
  tbody tr:hover td.firm-cell{background:var(--panel);}
  .yes{color:var(--success);}
  .no{color:var(--danger);}
  .trust-pill{font-family:'IBM Plex Mono'; padding:3px 8px; border-radius:4px; font-size:12px;}
  .trust-hi{background:rgba(79,191,123,0.12); color:var(--success);}
  .trust-mid{background:rgba(232,195,61,0.12); color:var(--warn);}
  .trust-lo{background:rgba(226,87,76,0.12); color:var(--danger);}

  /* ---------- Compare picker ---------- */
  .compare-picker{display:flex; flex-wrap:wrap; gap:8px; margin-bottom:22px;}
  .compare-chip{font-family:'IBM Plex Mono'; font-size:12.5px; padding:9px 14px; border-radius:20px; border:1px solid var(--line); background:var(--panel); color:var(--text-dim); cursor:pointer;}
  .compare-chip.active{border-color:var(--amber); color:var(--amber); background:var(--amber-soft);}
  .compare-chip:disabled{opacity:.35; cursor:not-allowed;}
  .winner-cell{color:var(--success); font-weight:600;}
  .winner-cell::after{content:' ✓';}

  /* ---------- Health dashboard ---------- */
  .health-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(280px,1fr)); gap:16px;}
  .health-card{background:var(--panel); border:1px solid var(--line); border-radius:10px; padding:20px; text-decoration:none; color:var(--text); display:block; transition:border-color .15s, transform .15s;}
  .health-card:hover{border-color:var(--amber-dim); transform:translateY(-2px);}
  .health-head{display:flex; justify-content:space-between; align-items:center; margin-bottom:14px;}
  .health-head h4{font-size:16px;}
  .health-rows{display:flex; flex-direction:column; gap:8px;}
  .health-row{display:flex; justify-content:space-between; font-size:13px; color:var(--text-dim); gap:10px;}
  .risk-badge{font-family:'IBM Plex Mono'; font-size:10.5px; text-transform:uppercase; padding:3px 8px; border-radius:4px; letter-spacing:.03em;}
  .risk-low{background:rgba(79,191,123,0.12); color:var(--success);}
  .risk-med{background:rgba(232,195,61,0.12); color:var(--warn);}
  .risk-unverified{background:rgba(138,143,152,0.15); color:var(--text-dim);}

  /* ---------- Score bars ---------- */
  .score-bar-row{display:flex; align-items:center; gap:12px; margin-bottom:10px;}
  .score-bar-label{width:150px; flex-shrink:0; font-size:12.5px; color:var(--text-dim); font-family:'IBM Plex Mono';}
  .score-bar-track{flex:1; height:8px; background:var(--panel-2); border-radius:4px; overflow:hidden; border:1px solid var(--line);}
  .score-bar-fill{height:100%; background:linear-gradient(90deg, var(--amber-dim), var(--amber)); width:0; transition:width .8s cubic-bezier(.2,.8,.2,1);}
  .score-bar-val{width:52px; text-align:right; font-family:'IBM Plex Mono'; font-size:12.5px; color:var(--text);}

  /* ---------- Coupons / offers ---------- */
  .coupon-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(260px,1fr)); gap:16px;}
  .coupon-card{background:var(--panel); border:1px solid var(--line); border-radius:10px; padding:20px; display:flex; flex-direction:column; gap:10px;}
  .coupon-card h4{font-size:16px;}
  .coupon-note{font-size:12.5px; color:var(--text-dim); line-height:1.55;}

  /* ---------- Tools ---------- */
  .tools-grid{display:grid; grid-template-columns:repeat(2,1fr); gap:20px;}
  @media (max-width:800px){.tools-grid{grid-template-columns:1fr;}}
  .tool-card{background:var(--panel); border:1px solid var(--line); border-radius:10px; padding:24px;}
  .tool-card h4{margin-bottom:14px; font-size:16px;}
  .field-row{display:flex; gap:10px; margin-bottom:10px; flex-wrap:wrap;}
  .field{flex:1; min-width:120px;}
  .field label{display:block; font-size:11.5px; color:var(--text-dim); margin-bottom:5px; font-family:'IBM Plex Mono'; text-transform:uppercase;}
  .field input, .field select{
    width:100%; background:var(--panel-2); border:1px solid var(--line); color:var(--text);
    padding:9px 10px; border-radius:5px; font-size:13.5px; font-family:'IBM Plex Mono';
  }
  .tool-output{margin-top:12px; padding:12px 14px; background:var(--panel-2); border-radius:6px; font-family:'IBM Plex Mono'; font-size:14px; border-left:3px solid var(--amber);}

  /* ---------- Reviews ---------- */
  .review-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(290px,1fr)); gap:16px;}
  .review-card{background:var(--panel); border:1px solid var(--line); border-radius:10px; padding:20px;}
  .review-tags{display:flex; gap:6px; flex-wrap:wrap; margin:10px 0;}
  .tag{font-size:11px; font-family:'IBM Plex Mono'; padding:3px 8px; border:1px solid var(--line); border-radius:4px; color:var(--text-dim);}
  .review-body{font-size:13.5px; color:var(--text-dim); margin-bottom:10px;}
  .review-foot{display:flex; justify-content:space-between; font-size:12px; color:var(--text-dim); font-family:'IBM Plex Mono';}
  .review-firm-link{text-decoration:none; color:var(--text); font-family:'Space Grotesk'; font-weight:600; font-size:15px;}
  .review-firm-link:hover{color:var(--amber);}

  /* ---------- Firm profile page ---------- */
  .profile-hero{padding:40px 0 0;}
  .profile-top{display:flex; justify-content:space-between; gap:24px; flex-wrap:wrap; align-items:flex-start;}
  .profile-badge-row{display:flex; gap:8px; flex-wrap:wrap; margin-bottom:14px;}
  .profile-title{font-size:clamp(30px,5vw,44px); margin-bottom:6px;}
  .profile-sub{color:var(--text-dim); font-family:'IBM Plex Mono'; font-size:13px;}
  .profile-score-box{background:var(--panel); border:1px solid var(--line); border-radius:12px; padding:20px 26px; text-align:center; min-width:150px;}
  .profile-score-num{font-family:'Space Grotesk'; font-size:40px; color:var(--amber); line-height:1;}
  .profile-score-label{font-size:11px; color:var(--text-dim); font-family:'IBM Plex Mono'; text-transform:uppercase; margin-top:6px;}
  .profile-actions{display:flex; gap:10px; margin-top:20px; flex-wrap:wrap;}

  .profile-subnav{position:sticky; top:calc(36px + 65px); z-index:40; background:rgba(11,13,16,0.94); backdrop-filter:blur(8px); border-bottom:1px solid var(--line); border-top:1px solid var(--line); margin-top:28px;}
  .profile-subnav-inner{display:flex; gap:4px; overflow-x:auto; padding:0 24px; max-width:1180px; margin:0 auto;}
  .profile-subnav a{flex-shrink:0; padding:13px 14px; font-family:'IBM Plex Mono'; font-size:12.5px; color:var(--text-dim); text-decoration:none; border-bottom:2px solid transparent;}
  .profile-subnav a:hover{color:var(--text);}
  .profile-subnav a.active{color:var(--amber); border-bottom-color:var(--amber);}

  .profile-section{padding:44px 0; border-bottom:1px solid var(--line); scroll-margin-top:130px;}
  .profile-section h3{font-size:22px; margin-bottom:20px; display:flex; align-items:center; gap:10px;}
  .fact-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(220px,1fr)); gap:14px;}
  .fact-card{background:var(--panel); border:1px solid var(--line); border-radius:9px; padding:16px;}
  .fact-label{font-size:11px; font-family:'IBM Plex Mono'; text-transform:uppercase; color:var(--text-dim); letter-spacing:.04em; margin-bottom:8px; display:flex; justify-content:space-between; align-items:center; gap:6px;}
  .fact-value{font-family:'Space Grotesk'; font-size:19px; margin-bottom:8px;}
  .fact-meta{font-size:11px; color:var(--text-faint); font-family:'IBM Plex Mono'; line-height:1.5;}
  .fact-meta a{color:var(--amber-dim); text-decoration:none;}
  .fact-meta a:hover{text-decoration:underline;}

  .flags-cols{display:grid; grid-template-columns:1fr 1fr; gap:20px;}
  @media (max-width:700px){.flags-cols{grid-template-columns:1fr;}}
  .flags-col h5{font-size:12.5px; font-family:'IBM Plex Mono'; text-transform:uppercase; letter-spacing:.04em; margin-bottom:12px;}
  .flags-col.pos h5{color:var(--success);}
  .flags-col.neg h5{color:var(--warn);}
  .flag-line{font-size:13.5px; color:var(--text-dim); padding:9px 0; border-bottom:1px solid var(--line-soft); display:flex; gap:8px;}
  .flag-line:last-child{border-bottom:none;}

  .timeline{display:flex; flex-direction:column;}
  .timeline-item{display:flex; gap:20px; padding:16px 0; border-left:2px solid var(--line); position:relative; padding-left:24px; margin-left:6px;}
  .timeline-item::before{content:''; position:absolute; left:-7px; top:20px; width:12px; height:12px; border-radius:50%; background:var(--amber); border:2px solid var(--bg);}
  .timeline-date{font-family:'IBM Plex Mono'; font-size:12px; color:var(--amber); min-width:90px; flex-shrink:0;}
  .timeline-body{font-size:13.5px; color:var(--text-dim);}
  .timeline-src{font-size:11px; color:var(--text-faint); margin-top:4px; font-family:'IBM Plex Mono';}

  .why-score{background:var(--panel-2); border:1px solid var(--line); border-radius:9px; padding:16px 18px; font-size:13px; color:var(--text-dim); margin-top:18px; line-height:1.6;}

  .tooltip-term{border-bottom:1px dashed var(--text-faint); cursor:help;}

  footer{padding:44px 0; text-align:center; color:var(--text-dim); font-size:12.5px; font-family:'IBM Plex Mono';}
  footer b{color:var(--amber);}
  .footer-links{display:flex; gap:18px; justify-content:center; margin-bottom:16px; flex-wrap:wrap;}
  .footer-links a{color:var(--text-dim); text-decoration:none;}
  .footer-links a:hover{color:var(--amber);}

  ::-webkit-scrollbar{height:8px; width:8px;}
  ::-webkit-scrollbar-thumb{background:var(--line); border-radius:4px;}
  @media (prefers-reduced-motion:reduce){ .ticker-track{animation:none;} .firm-card, .score-bar-fill{transition:none;} }

  /* ---------- Article / research pages ---------- */
  .article-body{max-width:720px; font-size:15.5px; color:var(--text-dim); line-height:1.75;}
  .article-body h3{color:var(--text); margin:28px 0 10px; font-size:19px;}
  .article-body p{margin-bottom:14px;}
  .article-card{background:var(--panel); border:1px solid var(--line); border-radius:10px; padding:22px; text-decoration:none; color:var(--text); display:block; transition:border-color .15s, transform .15s;}
  .article-card:hover{border-color:var(--amber-dim); transform:translateY(-2px);}
  .article-card .a-eyebrow{font-family:'IBM Plex Mono'; font-size:11px; color:var(--amber-dim); text-transform:uppercase; letter-spacing:.05em; margin-bottom:8px;}
  .article-card h4{font-size:16.5px; margin-bottom:8px;}
  .article-card p{font-size:13px; color:var(--text-dim);}
  .research-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(280px,1fr)); gap:16px;}

  /* ---------- Recently changed / trending on home ---------- */
  .change-list{display:flex; flex-direction:column; border:1px solid var(--line); border-radius:10px; overflow:hidden;}
  .change-row{display:flex; justify-content:space-between; align-items:center; padding:14px 18px; border-bottom:1px solid var(--line); background:var(--panel); text-decoration:none; color:var(--text); gap:14px;}
  .change-row:last-child{border-bottom:none;}
  .change-row:hover{background:var(--panel-2);}
  .change-left{display:flex; gap:12px; align-items:center; min-width:0;}
  .change-firm{font-family:'Space Grotesk'; font-weight:600; font-size:14px; flex-shrink:0;}
  .change-desc{font-size:13px; color:var(--text-dim); overflow:hidden; text-overflow:ellipsis; white-space:nowrap;}
  .change-date{font-family:'IBM Plex Mono'; font-size:11.5px; color:var(--text-faint); flex-shrink:0;}

  .trend-row{display:flex; gap:10px; flex-wrap:wrap;}
  .trend-chip{display:flex; align-items:center; gap:8px; background:var(--panel); border:1px solid var(--line); border-radius:20px; padding:8px 14px 8px 10px; text-decoration:none; color:var(--text); font-size:13px;}
  .trend-chip:hover{border-color:var(--amber-dim);}
  .trend-num{font-family:'IBM Plex Mono'; color:var(--amber-dim); font-size:12px;}

  /* ---------- Arena / Games (secondary, moved down) ---------- */
  .secondary-band{background:linear-gradient(180deg, var(--bg-2), var(--bg)); }
  .arena-head{background:linear-gradient(180deg, rgba(232,163,61,0.05), transparent); border:1px solid var(--line); border-radius:10px; padding:22px 26px; margin-bottom:26px; display:flex; justify-content:space-between; align-items:center; gap:20px; flex-wrap:wrap;}
  .arena-head p{color:var(--text-dim); font-size:13.5px; max-width:520px;}
  .game-grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(300px,1fr)); gap:18px;}
  .game-card{background:var(--panel); border:1px solid var(--line); border-radius:10px; padding:20px; display:flex; flex-direction:column; gap:12px;}
  .game-card h4{font-size:16px; display:flex; align-items:center; gap:8px;}
  .game-card .desc{color:var(--text-dim); font-size:12.5px;}
  .game-badge{font-family:'IBM Plex Mono'; font-size:10.5px; text-transform:uppercase; letter-spacing:.05em; padding:3px 8px; border-radius:4px; background:var(--amber-soft); color:var(--amber); align-self:flex-start;}
  .game-stage{background:var(--panel-2); border:1px solid var(--line); border-radius:8px; padding:16px; min-height:140px; display:flex; flex-direction:column; align-items:center; justify-content:center; gap:9px; text-align:center;}
  .big-price{font-family:'IBM Plex Mono'; font-size:30px; font-weight:600;}
  .game-msg{font-size:12.5px; color:var(--text-dim); min-height:18px;}
  .game-row{display:flex; gap:8px; width:100%;}
  .game-row .btn{flex:1; justify-content:center; padding:10px; font-size:12.5px;}
  .btn-up{background:rgba(79,191,123,0.12); color:var(--success); border:1px solid rgba(79,191,123,0.3);}
  .btn-up:hover{background:rgba(79,191,123,0.22);}
  .btn-down{background:rgba(226,87,76,0.12); color:var(--danger); border:1px solid rgba(226,87,76,0.3);}
  .btn-down:hover{background:rgba(226,87,76,0.22);}
  .streak-row{display:flex; justify-content:space-between; width:100%; font-family:'IBM Plex Mono'; font-size:12px; color:var(--text-dim);}
  .candle-icons{display:flex; gap:8px; flex-wrap:wrap; justify-content:center;}
  .candle-btn{width:42px; height:42px; border-radius:6px; border:1px solid var(--line); cursor:pointer; font-size:17px; display:flex; align-items:center; justify-content:center; background:var(--panel);}
  .candle-btn.flash{outline:2px solid var(--amber);}
  .candle-btn:active{transform:scale(0.94);}
  #sim_canvas{width:100%; height:110px; display:block; background:var(--panel); border-radius:6px;}
  .sim-hud{display:flex; justify-content:space-between; width:100%; font-family:'IBM Plex Mono'; font-size:12px; flex-wrap:wrap; gap:6px;}
  .sim-hud b{color:var(--text);}
  .leaderboard{margin-top:8px; font-family:'IBM Plex Mono'; font-size:12px; color:var(--text-dim); width:100%;}
  .leaderboard div{display:flex; justify-content:space-between; padding:4px 0; border-bottom:1px solid var(--line);}
  .leaderboard div:last-child{border-bottom:none;}
  .leaderboard .you{color:var(--amber);}

  .growth-grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(300px,1fr)); gap:18px;}
  .growth-card{background:var(--panel); border:1px solid var(--line); border-radius:10px; padding:20px; display:flex; flex-direction:column; gap:12px;}
  .growth-card h4{font-size:16px; display:flex; align-items:center; gap:8px;}
  .growth-card .desc{color:var(--text-dim); font-size:12.5px;}
  .code-box{display:flex; gap:8px; align-items:center;}
  .code-box input{flex:1; background:var(--panel-2); border:1px solid var(--line); color:var(--amber); font-family:'IBM Plex Mono'; padding:10px 12px; border-radius:6px; font-size:13px;}
  .progress-track{height:8px; background:var(--panel-2); border-radius:4px; overflow:hidden; border:1px solid var(--line);}
  .progress-fill{height:100%; background:var(--amber); width:0%; transition:width .4s;}
  .progress-label{font-family:'IBM Plex Mono'; font-size:11.5px; color:var(--text-dim); display:flex; justify-content:space-between;}
  .confession-form{display:flex; gap:8px;}
  .confession-form textarea{flex:1; background:var(--panel-2); border:1px solid var(--line); color:var(--text); font-family:'IBM Plex Sans'; padding:10px 12px; border-radius:6px; font-size:13px; resize:none; min-height:44px;}
  .confession-wall{display:flex; flex-direction:column; gap:10px; max-height:260px; overflow-y:auto; padding-right:4px;}
  .confession{background:var(--panel-2); border:1px solid var(--line); border-radius:8px; padding:12px 14px; font-size:12.5px;}
  .confession .meta{font-family:'IBM Plex Mono'; font-size:11px; color:var(--text-dim); margin-bottom:6px; display:flex; justify-content:space-between;}
  .confession .heart{cursor:pointer; color:var(--text-dim); background:none; border:none;}
  .confession .heart.liked{color:var(--danger);}
  .toast{position:fixed; bottom:24px; left:50%; transform:translateX(-50%) translateY(20px); background:var(--amber); color:#0B0D10; padding:11px 20px; border-radius:6px; font-family:'IBM Plex Mono'; font-size:13px; font-weight:600; opacity:0; pointer-events:none; transition:all .25s; z-index:200;}
  .toast.show{opacity:1; transform:translateX(-50%) translateY(0);}

  .about-grid{display:grid; grid-template-columns:1fr 1fr; gap:28px;}
  @media (max-width:800px){.about-grid{grid-template-columns:1fr;}}
  .about-card{background:var(--panel); border:1px solid var(--line); border-radius:10px; padding:22px;}
  .about-card h4{margin-bottom:10px; font-size:16px;}
  .about-card p{font-size:13.5px; color:var(--text-dim); line-height:1.65;}
</style>
</head>
<body>

<div class="ticker-bar" aria-hidden="true">
  <div class="ticker-track" id="tickerTrack"></div>
</div>

<header class="nav">
  <nav>
    <a href="#/" class="logo"><span class="dot"></span>PropFirmScam</a>
    <div class="navlinks" id="navlinks"></div>
    <div class="nav-right">
      <button class="nav-search-btn" id="navSearchBtn" aria-label="Search">🔍 <span>Search</span></button>
      <button class="hamburger" id="hamburgerBtn" aria-label="Menu" aria-expanded="false">☰</button>
    </div>
  </nav>
  <div class="mobile-menu" id="mobileMenu"></div>
</header>

<div class="search-overlay" id="searchOverlay">
  <div class="search-modal">
    <input class="search-modal-input" id="searchModalInput" type="text" placeholder="Search firms, reviews, news... (Esc to close)">
    <div class="search-modal-body" id="searchModalBody"></div>
    <div class="search-hint">Enter to jump to top result · Esc to close</div>
  </div>
</div>

<main id="app"></main>

<footer>
  <div class="wrap">
    <div class="footer-links">
      <a href="#/firms">Firms</a><a href="#/compare">Compare</a><a href="#/match">Match Me</a>
      <a href="#/health">Health</a><a href="#/reviews">Reviews</a><a href="#/tools">Tools</a>
      <a href="#/arena">Arena</a><a href="#/about">About &amp; Methodology</a>
    </div>
    <b>PropFirmScam</b> — independent prop firm research. Rankings are algorithmic and editorial, not paid placement, not financial advice. Demo build — sample dataset, see /about for sourcing.
  </div>
</footer>

<div class="toast" id="toast"></div>

<script>
/* ============================================================
   DATA — single source of truth. Every card/table/page reads
   from this array. Nothing here should be presented as fact
   beyond what's explicitly source-tagged.
   ============================================================ */
const NOW_YEAR = 2026;

const firms = [
  {slug:"topstep", name:"TopStep", category:"futures", score:72, trustpilot:3.6, tpDate:"Dec 2025", founded:2012, hq:"Chicago, IL", dailyDD:1000, overallDD:2000, split:90, news:true, weekend:false, platforms:["NT8","TV"], steps:"one", payoutDays:2, priceFrom:165, style:["day","swing"], budgetMax:200,
    officialUrl:"https://www.topstep.com/",
    leadership:{name:"Michael Patak", title:"Founder & CEO", verified:true, sourceLabel:"Finance Magnates, Dec 23 2025", sourceUrl:"https://www.financemagnates.com/forex/topstep-faces-prop-traders-wrath-due-to-repeated-outages-ceo-sets-january-deadline-for-a-fix/"},
    newsItem:{change:"Platform outages dropped Trustpilot score to 3.6; CEO pledged a January fix", dir:"down", date:"Dec 2025", source:"Finance Magnates"}},
  {slug:"tradeify", name:"Tradeify", category:"futures", score:94, trustpilot:4.7, tpDate:"2026", founded:2024, hq:"Miami / Boca Raton, FL", dailyDD:2500, overallDD:3000, split:90, news:true, weekend:true, platforms:["NT8","TV","MT5"], steps:"one", payoutDays:1, priceFrom:145, style:["scalp","day","swing"], budgetMax:200,
    officialUrl:"https://tradeify.co/",
    leadership:{name:"Brett Simberkoff", co:"Vinan Mistry — Co-Founder & COO", title:"Co-Founder & CEO", verified:true, sourceLabel:"Finance Magnates, 2026", sourceUrl:"https://www.financemagnates.com/executives/tradeify-co-founders-difficult-to-enter-futures-prop-subscription-ditch-barely-moved-revenue/"},
    newsItem:{change:"Killed its monthly evaluation subscription — founders say it barely moved revenue", dir:"flat", date:"Jul 2026", source:"Finance Magnates"}},
  {slug:"tradeday", name:"TradeDay", category:"futures", score:70, trustpilot:null, tpDate:null, founded:2020, hq:"UK-based", dailyDD:1500, overallDD:2500, split:85, news:false, weekend:false, platforms:["NT8"], steps:"two", payoutDays:5, priceFrom:150, style:["day"], budgetMax:250,
    officialUrl:"https://www.tradeday.com/",
    leadership:{name:null, title:"Leadership not independently verified", verified:false},
    newsItem:null},
  {slug:"earn2trade", name:"Earn2Trade", category:"futures", score:74, trustpilot:null, tpDate:null, founded:2018, hq:"Chicago, IL (HQ unverified)", dailyDD:1100, overallDD:2000, split:80, news:false, weekend:false, platforms:["NT8","TV"], steps:"two", payoutDays:7, priceFrom:150, style:["day","swing"], budgetMax:250,
    officialUrl:"https://www.earn2trade.com/",
    leadership:{name:null, title:"Leadership not independently verified", verified:false},
    newsItem:null},
  {slug:"lucid-trading", name:"Lucid Trading", category:"futures", score:68, trustpilot:null, tpDate:null, founded:null, hq:"Unverified", dailyDD:2000, overallDD:3000, split:90, news:true, weekend:true, platforms:["NT8","TV"], steps:"one", payoutDays:1, priceFrom:130, style:["scalp","day","swing"], budgetMax:150,
    officialUrl:null,
    leadership:{name:null, title:"Leadership not independently verified", verified:false},
    newsItem:null},
  {slug:"alpha-futures", name:"Alpha Futures", category:"futures", score:70, trustpilot:null, tpDate:null, founded:null, hq:"Unverified", dailyDD:2000, overallDD:2500, split:90, news:true, weekend:true, platforms:["NT8","TV"], steps:"one", payoutDays:2, priceFrom:140, style:["scalp","day"], budgetMax:200,
    officialUrl:null,
    leadership:{name:null, title:"Leadership not independently verified", verified:false},
    newsItem:null},
  {slug:"apex-trader-funding", name:"Apex Trader Funding", category:"futures", score:80, trustpilot:null, tpDate:null, founded:2021, hq:"Austin, TX", dailyDD:2500, overallDD:2500, split:90, news:true, weekend:true, platforms:["NT8","TV"], steps:"one", payoutDays:1, priceFrom:147, style:["scalp","day","swing"], budgetMax:200,
    officialUrl:"https://apextraderfunding.com/",
    leadership:{name:"Darrell Martin", title:"Founder & CEO", verified:true, sourceLabel:"Company About page", sourceUrl:"https://apextraderfunding.com/about/"},
    newsItem:{change:"Grew out of the 30,000+ member Apex Investing trading community into one of the largest futures evaluators by trader count", dir:"up", date:"2026", source:"Company About page"}},
  {slug:"myfundedfutures", name:"MyFundedFutures", category:"futures", score:94, trustpilot:4.7, tpDate:"2026", founded:2022, hq:"Dallas / Southlake, TX", dailyDD:2000, overallDD:2500, split:90, news:true, weekend:true, platforms:["NT8","TV"], steps:"one", payoutDays:2, priceFrom:145, style:["scalp","day","swing"], budgetMax:200,
    officialUrl:"https://myfundedfutures.com/",
    leadership:{name:"Matthew Leech", title:"Founder & CEO", verified:true, sourceLabel:"PropTradingVibes, Mar 2026", sourceUrl:"https://proptradingvibes.com/blog/myfundedfutures-ceo-matthew-leech-fdcf8"},
    newsItem:{change:"Completed a major product restructuring; Leech also currently runs Talero Brokerage and Fintevo alongside MFFU", dir:"flat", date:"Jul 2025", source:"PropTradingVibes"}},
  {slug:"ftmo", name:"FTMO", category:"cfd", score:96, trustpilot:null, tpDate:null, founded:2015, hq:"Prague, Czech Republic", dailyDD:5, overallDD:10, split:90, news:false, weekend:true, platforms:["MT5"], steps:"two", payoutDays:14, priceFrom:155, style:["swing","day"], budgetMax:9999,
    officialUrl:"https://ftmo.com/",
    leadership:{name:"Otakar Šuffner", co:"Marek Vašíček — Co-Founder & CTO", title:"CEO & Co-Founder", verified:true, sourceLabel:"FTMO / Forbes CZ, Mar 2026", sourceUrl:"https://ftmo.com/en/blog/forbes-the-ftmo-cover-story/"},
    newsItem:{change:"FTMO Group's acquisition of global forex broker OANDA profiled in a Forbes CZ cover story", dir:"up", date:"2026", source:"Forbes CZ / FTMO"}},
  {slug:"fundingpips", name:"FundingPips", category:"cfd", score:90, trustpilot:4.5, tpDate:"2026", founded:2022, hq:"Dubai, UAE", dailyDD:5, overallDD:10, split:90, news:true, weekend:true, platforms:["MT5"], steps:"one", payoutDays:1, priceFrom:39, style:["scalp","swing","day"], budgetMax:150,
    officialUrl:"https://fundingpips.com/",
    leadership:{name:"Khaled Ayesh", title:"CEO & Owner", verified:true, sourceLabel:"Finance Magnates, Nov 2025", sourceUrl:"https://www.financemagnates.com/thought-leadership/from-fundingpips-to-trading-ceo-powers-next-chapter-in-trading-innovation/"},
    newsItem:{change:"CEO Khaled Ayesh launched a new trader-first brokerage, Tradin, extending FundingPips beyond evaluations", dir:"up", date:"Nov 2025", source:"Finance Magnates"}},
  {slug:"the5ers", name:"The5ers", category:"cfd", score:85, trustpilot:null, tpDate:null, founded:2015, hq:"Ra'anana, Israel", dailyDD:5, overallDD:12, split:80, news:true, weekend:true, platforms:["MT5"], steps:"any", payoutDays:5, priceFrom:97, style:["swing","day"], budgetMax:9999,
    officialUrl:"https://the5ers.com/",
    leadership:{name:"Gil Ben-Hur", co:"Saul Lokier — CEO", title:"Founder", verified:true, sourceLabel:"Finance Magnates, Aug 2025", sourceUrl:"https://www.financemagnates.com/executives/we-dont-sell-dreams-we-dont-drive-lamborghinis-the5ers-founder/"},
    newsItem:{change:"Founder argued the popular two-step model is structurally incompatible with true A-book execution; expanded into US futures in Feb 2026", dir:"up", date:"Feb 2026", source:"Finance Magnates"}},
  {slug:"fundednext", name:"FundedNext", category:"cfd", score:80, trustpilot:null, tpDate:null, founded:2015, hq:"Multi-region (est. as NEXT Ventures)", dailyDD:5, overallDD:10, split:90, news:true, weekend:true, platforms:["MT5"], steps:"any", payoutDays:5, priceFrom:49, style:["scalp","swing","day"], budgetMax:9999,
    officialUrl:"https://fundednext.com/",
    leadership:{name:"Abdullah Jayed", co:"Abdullah Galib — Co-Founder", title:"Co-Founder", verified:true, sourceLabel:"FundedNext company page", sourceUrl:"https://fundednext.com/company"},
    newsItem:{change:"Grew from a 5-person team (as NEXT Ventures) into FundedNext, FundedNext Futures and FNmarkets, ~600 staff across four regions", dir:"up", date:"2026", source:"FundedNext company page"}},
];

// Industry-level (not firm-specific) ticker items
const industryNews = [
  {change:"~80–100 prop firms shut down industry-wide amid a platform/licensing crisis", dir:"down", date:"Feb 2024–2025", source:"MyForexFirms investigation"},
  {change:"FundingPips reintroduced MetaTrader 5 after a year-long break", dir:"up", date:"Mar 2025", source:"Finance Magnates", firmSlug:"fundingpips"},
];

const reviews = [
  {firmSlug:"tradeify", style:"Scalper", platform:"NinjaTrader", funded:true, paid:true, body:"Payout hit in under 24h after the request. Daily DD is generous enough for scalping NQ around the open.", days:"2d ago"},
  {firmSlug:"topstep", style:"Day Trader", platform:"TradingView", funded:true, paid:true, body:"Platform hiccups were real late last year, but support communicated well and things have been stable since.", days:"5d ago"},
  {firmSlug:"ftmo", style:"Swing", platform:"MT5", funded:true, paid:true, body:"Slower payout cycle but the rules are the most transparent of any firm I've used across three funded accounts.", days:"1w ago"},
  {firmSlug:"the5ers", style:"Swing", platform:"MT5", funded:true, paid:true, body:"No re-billing once funded, which matches what the founder says publicly. Fills feel like real A-book execution.", days:"6d ago"},
  {firmSlug:"apex-trader-funding", style:"Day Trader", platform:"NinjaTrader", funded:true, paid:true, body:"Straightforward one-step eval, and the reset discount during their sale made a second attempt cheap.", days:"3d ago"},
  {firmSlug:"fundingpips", style:"Scalper", platform:"MT5", funded:true, paid:true, body:"Fastest payout I've seen — under 20 hours. Spreads widen during high-impact news though, plan around it.", days:"4d ago"},
];

const research = [
  {slug:"payout-verification", eyebrow:"Explainer", title:"Why prop-firm payout claims are difficult to verify", teaser:"Most 'total paid out' figures are self-reported by the firm, with no independent audit trail.",
    body:["Prop firms routinely advertise a headline number — \"$X million paid to traders\" — on their homepage. In almost every case, that figure is self-reported: it comes from the firm's own internal ledger, not from a bank, auditor, or regulator.",
    "That doesn't automatically make the number false. But it means the claim carries the same evidentiary weight as any other marketing statement, and traders researching a firm should treat it that way rather than as a fact.",
    "A few things are worth checking before trusting a payout claim: does the firm publish transaction-level evidence (not just a total)? Is there a third-party verification service involved? Are user-submitted payout reports from independent trackers roughly consistent with the firm's own figures? None of these fully substitute for an audit, but they narrow the gap between marketing copy and reality.",
    "On this site, payout speed figures (like '~1 day') are compiled from company statements and are labeled editorial/compiled rather than independently verified — because in most cases, they aren't."]},
  {slug:"trailing-drawdown", eyebrow:"Explainer", title:"How trailing drawdown actually works", teaser:"The rule that quietly fails more traders than any profit target.",
    body:["Trailing drawdown is the single rule most likely to blindside a new prop trader, because it doesn't behave the way a simple 'don't lose more than $X' rule would.",
    "In a trailing model, the drawdown floor rises as your account's peak equity rises — often intraday, tick by tick, not just at the end of the day. That means unrealized open profit can pull your floor up before you've locked in a gain, and a normal pullback in a winning trade can breach the floor even though your realized P&L is still positive.",
    "End-of-day (EOD) drawdown is the friendlier cousin: the floor only recalculates once, at the daily close, based on the day's ending balance — not floating equity. That gives a trader more room to ride out intraday noise.",
    "Before paying for any evaluation, confirm in writing (not just from a sales page) whether the firm uses trailing or EOD drawdown, and whether the trailing calculation uses realized balance or floating equity — the difference materially changes how much room you actually have."]},
  {slug:"prop-firm-shutdowns", eyebrow:"Explainer", title:"Prop firm shutdowns: what traders should look for", teaser:"Roughly 80–100 firms closed industry-wide in a recent 18-month stretch. The warning signs were similar.",
    body:["Industry coverage has tracked somewhere in the range of 80–100 prop firm closures across a recent stretch spanning early 2024 into late 2025, driven in large part by a wave of licensing and platform-access disruptions that hit smaller operators hardest.",
    "Firms that later collapsed tended to share a few traits before the fact: anonymous or unverifiable ownership, payout claims with no supporting detail, aggressive discounting that didn't match their apparent scale, and a pattern of rule changes announced with little notice.",
    "None of these signs guarantee failure on their own — plenty of legitimate firms run frequent promotions or make rule changes. But stacked together, they're worth weighing before committing evaluation fees, and they're a large part of why this site tries to separately label what's independently sourced versus what's simply stated by the firm."]},
];

/* ============================================================
   HELPERS
   ============================================================ */
function esc(s){ return String(s==null?'':s).replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }
function firmBySlug(slug){ return firms.find(f=>f.slug===slug); }
function catLabel(c){ return c==='cfd' ? 'CFD / Forex' : 'Futures'; }
function stepsLabel(s){ return s==='one' ? '1-step' : s==='two' ? '2-step' : 'Flexible'; }
function scoreClass(s){ return s>=85 ? 'trust-hi' : s>=75 ? 'trust-mid' : 'trust-lo'; }
function riskLevel(f){ if(!f.trustpilot && !f.leadership.verified) return {label:'UNVERIFIED', cls:'risk-unverified'}; if(f.score>=85) return {label:'LOW RISK*', cls:'risk-low'}; return {label:'MEDIUM RISK*', cls:'risk-med'}; }
function vpill(status){
  const map = {
    verified:['v-verified','✓ Verified'], unverified:['v-unverified','⚠ Unverified'],
    editorial:['v-editorial','◆ Editorial'], user:['v-user','◇ User reported']
  };
  const [cls,label] = map[status] || map.editorial;
  return `<span class="vpill ${cls}">${label}</span>`;
}
function firmLink(slug, text, cls){ return `<a href="#/firms/${slug}" class="${cls||'link-firm'}">${esc(text)}</a>`; }
function toast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg; t.classList.add('show');
  clearTimeout(window._toastTimer);
  window._toastTimer = setTimeout(()=>t.classList.remove('show'), 1600);
}
function reviewsFor(slug){ return reviews.filter(r=>r.firmSlug===slug); }

function healthBreakdown(f){
  const factors = {
    "Transparency": f.leadership.verified ? 1 : 0.45,
    "Payout track record": f.trustpilot ? (f.trustpilot/5) : 0.4,
    "Rules clarity": 0.72 + (f.news?0.09:0) + (f.weekend?0.06:0),
    "Company history": f.founded ? Math.min(1, Math.max(0.35,(NOW_YEAR-f.founded)/12)) : 0.32,
    "Platform coverage": Math.min(1, 0.45 + f.platforms.length*0.16),
  };
  const keys = Object.keys(factors);
  const sumFactors = keys.reduce((s,k)=>s+factors[k],0);
  let running = 0; const out = [];
  keys.forEach((k,i)=>{
    let v;
    if(i === keys.length-1){ v = f.score - running; }
    else { v = Math.round(f.score * (factors[k]/sumFactors)); running += v; }
    v = Math.max(0, Math.min(20, v));
    out.push({label:k, value:v, max:20});
  });
  return out;
}

function riskFlags(f){
  const pos=[], neg=[];
  if(f.leadership.verified) pos.push('Named, publicly sourced leadership on record'); else neg.push('Leadership identity not independently verified');
  if(f.trustpilot) pos.push(`Public Trustpilot rating of ${f.trustpilot}/5 as of ${f.tpDate}`); else neg.push('No public Trustpilot rating found at time of writing');
  if(f.founded && (NOW_YEAR-f.founded)>=3) pos.push(`${NOW_YEAR-f.founded}+ years of public operating history`);
  if(!f.founded) neg.push('Founding date not independently verified');
  if(f.newsItem) pos.push('Recent activity independently reported by industry press');
  if(f.news) pos.push('Publicly states news trading is permitted');
  neg.push('Payout volume is firm-reported and not independently audited');
  if(f.score < 78) neg.push('Below-average composite score relative to the tracked peer set');
  return {pos, neg};
}

function changelogFor(f){
  const items = [];
  if(f.newsItem) items.push(f.newsItem);
  industryNews.forEach(n=>{ if(n.firmSlug===f.slug) items.push(n); });
  return items;
}

/* ============================================================
   ROUTER
   ============================================================ */
const NAV_ITEMS = [
  ['/firms','Firms'],['/compare','Compare'],['/match','Match Me'],['/health','Health'],
  ['/reviews','Reviews'],['/coupons','Offers'],['/tools','Tools'],['/arena','🎮 Arena'],['/about','About']
];

function buildNav(){
  const route = getRouteName();
  document.getElementById('navlinks').innerHTML = NAV_ITEMS.map(([path,label])=>
    `<a href="#${path}" class="${route===path?'active':''}">${label}</a>`).join('');
  document.getElementById('mobileMenu').innerHTML = NAV_ITEMS.map(([path,label])=>
    `<a href="#${path}" class="${route===path?'active':''}">${label}</a>`).join('');
}
function getRouteName(){
  const h = (location.hash.slice(1)||'/').split('#')[0];
  const parts = h.split('/').filter(Boolean);
  if(parts[0]==='firms' && parts.length===1) return '/firms';
  if(parts.length && !['firms','compare','match','health','reviews','coupons','tools','arena','about','research'].includes(parts[0])) return '';
  return parts.length ? '/'+parts[0] : '/';
}
function parseRoute(){
  let h = location.hash.slice(1) || '/';
  let sectionAnchor = null;
  if(h.includes('#')){ [h, sectionAnchor] = h.split('#'); }
  const parts = h.split('/').filter(Boolean);
  if(parts.length===0) return {name:'home', sectionAnchor};
  if(parts[0]==='firms' && parts.length===1) return {name:'firms', sectionAnchor};
  if(parts[0]==='firms' && parts.length===2) return {name:'firm', slug:parts[1], sectionAnchor};
  if(parts[0]==='compare') return {name:'compare', sectionAnchor};
  if(parts[0]==='match') return {name:'match', sectionAnchor};
  if(parts[0]==='health') return {name:'health', sectionAnchor};
  if(parts[0]==='reviews') return {name:'reviews', sectionAnchor};
  if(parts[0]==='coupons') return {name:'offers', sectionAnchor};
  if(parts[0]==='tools') return {name:'tools', sectionAnchor};
  if(parts[0]==='arena') return {name:'arena', sectionAnchor};
  if(parts[0]==='about') return {name:'about', sectionAnchor};
  if(parts[0]==='research' && parts[1]) return {name:'article', slug:parts[1], sectionAnchor};
  return {name:'notfound', sectionAnchor};
}

let compareSelection = [];

function render(){
  const route = parseRoute();
  buildNav();
  const app = document.getElementById('app');
  let html = '';
  switch(route.name){
    case 'home': document.title = 'PropFirmScam — Find your funded match'; html = pageHome(); break;
    case 'firms': document.title = 'Firm Directory | PropFirmScam'; html = pageFirms(); break;
    case 'firm': {
      const f = firmBySlug(route.slug);
      if(!f){ html = pageNotFound(); break; }
      document.title = `${f.name} Review, Rules & Payouts | PropFirmScam`;
      html = pageFirm(f);
      break;
    }
    case 'compare': document.title = 'Compare Prop Firms | PropFirmScam'; html = pageCompare(); break;
    case 'match': document.title = 'Match Me | PropFirmScam'; html = pageMatch(); break;
    case 'health': document.title = 'Firm Health & Risk | PropFirmScam'; html = pageHealth(); break;
    case 'reviews': document.title = 'Trader Reviews | PropFirmScam'; html = pageReviews(); break;
    case 'offers': document.title = 'Offers | PropFirmScam'; html = pageOffers(); break;
    case 'tools': document.title = 'Trader Tools | PropFirmScam'; html = pageTools(); break;
    case 'arena': document.title = 'The Arena | PropFirmScam'; html = pageArena(); break;
    case 'about': document.title = 'About & Methodology | PropFirmScam'; html = pageAbout(); break;
    case 'article': {
      const a = research.find(r=>r.slug===route.slug);
      if(!a){ html = pageNotFound(); break; }
      document.title = a.title + ' | PropFirmScam';
      html = pageArticle(a);
      break;
    }
    default: html = pageNotFound();
  }
  app.innerHTML = html;
  afterRender(route);
}

function afterRender(route){
  renderTicker();
  if(route.sectionAnchor){
    setTimeout(()=>{ const el = document.getElementById(route.sectionAnchor); if(el) el.scrollIntoView({behavior:'smooth', block:'start'}); }, 30);
  } else {
    window.scrollTo({top:0, behavior:'instant' in window ? 'instant' : 'auto'});
  }
  if(route.name==='firms') initFirmsPage();
  if(route.name==='firm') initFirmPage(route.slug);
  if(route.name==='compare') initComparePage();
  if(route.name==='match') initMatchPage();
  if(route.name==='health') initHealthPage();
  if(route.name==='reviews') initReviewsPage();
  if(route.name==='tools') initToolsPage();
  if(route.name==='arena') initArenaPage();
  if(route.name==='home') initHomePage();
  initMobileMenu();
  initSearch();
}

window.addEventListener('hashchange', render);
window.addEventListener('DOMContentLoaded', render);

/* ============================================================
   TICKER
   ============================================================ */
function renderTicker(){
  const track = document.getElementById('tickerTrack');
  const dirIcon = {up:'▲', down:'▼', flat:'●'};
  const items = [];
  firms.forEach(f=>{ if(f.newsItem) items.push({...f.newsItem, firmName:f.name, firmSlug:f.slug}); });
  industryNews.forEach(n=>{ items.push({...n, firmName:n.firmSlug?firmBySlug(n.firmSlug).name:'Industry', firmSlug:n.firmSlug||null}); });
  const doubled = items.concat(items);
  track.innerHTML = doubled.map(r => {
    const inner = `<span class="tick-${r.dir}">${dirIcon[r.dir]}</span> <b>${esc(r.firmName)}</b> ${esc(r.change)} <span style="color:var(--text-dim)">· ${r.date} · ${r.source}</span>`;
    return r.firmSlug ? `<a href="#/firms/${r.firmSlug}" class="ticker-item">${inner}</a>` : `<span class="ticker-item">${inner}</span>`;
  }).join('<span style="color:var(--line)">/</span>');
}

/* ============================================================
   MOBILE MENU + SEARCH
   ============================================================ */
function initMobileMenu(){
  const btn = document.getElementById('hamburgerBtn');
  const menu = document.getElementById('mobileMenu');
  btn.onclick = () => {
    const open = menu.classList.toggle('open');
    btn.setAttribute('aria-expanded', open ? 'true':'false');
  };
  menu.querySelectorAll('a').forEach(a => a.addEventListener('click', ()=>{ menu.classList.remove('open'); btn.setAttribute('aria-expanded','false'); }));
}

function searchIndex(q){
  q = q.trim().toLowerCase();
  if(!q) return null;
  const firmHits = firms.filter(f => f.name.toLowerCase().includes(q) || f.hq.toLowerCase().includes(q));
  const reviewHits = reviews.filter(r => { const f = firmBySlug(r.firmSlug); return f && (f.name.toLowerCase().includes(q)) && false; }); // reserved
  const newsHits = [];
  firms.forEach(f=>{ if(f.newsItem && (f.name.toLowerCase().includes(q) || f.newsItem.change.toLowerCase().includes(q))) newsHits.push({firm:f, item:f.newsItem}); });
  const revHits = reviews.filter(r => { const f = firmBySlug(r.firmSlug); return f.name.toLowerCase().includes(q) || r.body.toLowerCase().includes(q) || r.style.toLowerCase().includes(q); });
  return {firmHits, newsHits, revHits};
}

function renderSearchResultsHTML(q){
  const res = searchIndex(q);
  if(!res) return '<div class="search-empty">Start typing to search firms, reviews, and news.</div>';
  const {firmHits, newsHits, revHits} = res;
  if(!firmHits.length && !newsHits.length && !revHits.length) return `<div class="search-empty">No matches for "${esc(q)}" in our tracked dataset.</div>`;
  let html = '';
  if(firmHits.length){
    html += '<div class="search-cat-label">Firms</div>';
    html += firmHits.map(f=>`<a href="#/firms/${f.slug}" class="search-result-row" onclick="closeSearch()"><span>${esc(f.name)}</span><span class="r-sub">${catLabel(f.category)} · ${f.score}/100</span></a>`).join('');
  }
  if(revHits.length){
    html += '<div class="search-cat-label">Reviews</div>';
    html += revHits.slice(0,4).map(r=>{ const f = firmBySlug(r.firmSlug); return `<a href="#/firms/${f.slug}#reviews" class="search-result-row" onclick="closeSearch()"><span>${esc(f.name)} — ${esc(r.style)} review</span><span class="r-sub">${r.days}</span></a>`; }).join('');
  }
  if(newsHits.length){
    html += '<div class="search-cat-label">News</div>';
    html += newsHits.slice(0,4).map(({firm,item})=>`<a href="#/firms/${firm.slug}#history" class="search-result-row" onclick="closeSearch()"><span>${esc(firm.name)} ${esc(item.change)}</span><span class="r-sub">${item.date}</span></a>`).join('');
  }
  return html;
}

function closeSearch(){ document.getElementById('searchOverlay').classList.remove('open'); }
function openSearch(){ document.getElementById('searchOverlay').classList.add('open'); const input = document.getElementById('searchModalInput'); input.value=''; document.getElementById('searchModalBody').innerHTML = renderSearchResultsHTML(''); setTimeout(()=>input.focus(), 30); }

function initSearch(){
  document.getElementById('navSearchBtn').onclick = openSearch;
  const overlay = document.getElementById('searchOverlay');
  overlay.onclick = (e)=>{ if(e.target===overlay) closeSearch(); };
  const input = document.getElementById('searchModalInput');
  input.oninput = ()=>{ document.getElementById('searchModalBody').innerHTML = renderSearchResultsHTML(input.value); };
  document.onkeydown = (e)=>{
    if(e.key==='/' && document.activeElement.tagName!=='INPUT' && document.activeElement.tagName!=='TEXTAREA'){ e.preventDefault(); openSearch(); }
    if(e.key==='Escape') closeSearch();
  };
}

/* ============================================================
   PAGE: HOME
   ============================================================ */
function pageHome(){
  const top = [...firms].sort((a,b)=>b.score-a.score).slice(0,6);
  const changed = firms.filter(f=>f.newsItem).sort((a,b)=> (b.score-a.score)).slice(0,6);
  const trending = [...firms].sort((a,b)=>b.score-a.score).slice(0,6);
  const latestReviews = reviews.slice(0,3);

  return `
  <section class="hero wrap" style="border-bottom:none; padding-top:56px;">
    <div class="eyebrow">Prop firm intelligence</div>
    <h1>Find your <em>funded</em> match — not just the cheapest challenge.</h1>
    <p class="sub">${firms.length} prop firms tracked across futures and CFD/forex — scored on public rules, disclosed payout speed, and who's actually running the company. Search, compare, or answer 7 questions to get a ranked match.</p>
    <div class="search-row">
      <input class="search-input" id="firmSearch" type="text" placeholder="Search a firm — e.g. Tradeify, TopStep, FTMO...">
      <a href="#/match" class="btn btn-primary">Find My Match →</a>
      <a href="#/firms" class="btn btn-ghost">Explore Firms</a>
    </div>
    <div id="searchResults" style="max-width:640px; margin-top:10px; font-size:13px; color:var(--text-dim);"></div>

    <div class="scam-banner">
      <span>⚠</span>
      <span><b>Documented case:</b> industry investigations have identified prop firms that fabricated payout figures and pre-launch reviews before collapsing — one widely-reported case involved a firm claiming $85M in payouts that were never verified independently, and roughly 80–100 prop firms shut down industry-wide between Feb 2024 and late 2025. Always demand independently verifiable payout proof before paying for a challenge. <a href="#/research/prop-firm-shutdowns">Read the full breakdown →</a></span>
    </div>
    <div class="data-note">Firm data compiled from company statements, Trustpilot, and financial-industry press (Finance Magnates, company newsrooms) as of July 2026. Composite scores are an editorial estimate, not a certification — see <a href="#/about" style="color:var(--amber-dim)">methodology</a>.</div>

    <div class="hero-stats">
      <div class="stat"><b class="mono">${firms.length}</b><span>Firms tracked</span></div>
      <div class="stat"><b class="mono">2</b><span>Categories — futures &amp; CFD</span></div>
      <div class="stat"><b class="mono">${firms.filter(f=>f.leadership.verified).length}</b><span>Leaderships sourced</span></div>
      <div class="stat"><b class="mono">Jul '26</b><span>Data last refreshed</span></div>
    </div>
  </section>

  <section class="wrap">
    <div class="section-head">
      <div><div class="num">Top rated</div><h2>Top rated firms</h2><p>Highest composite score across the tracked set — editorial, not a certification.</p></div>
      <a href="#/firms" class="btn btn-ghost btn-sm">View full directory →</a>
    </div>
    <div class="firm-grid">${top.map(firmCard).join('')}</div>
  </section>

  <section class="wrap">
    <div class="section-head">
      <div><div class="num">Live tracking</div><h2>Recently changed</h2><p>Independently reported rule, product, or leadership changes.</p></div>
    </div>
    <div class="change-list">
      ${changed.map(f=>`<a href="#/firms/${f.slug}#history" class="change-row">
        <div class="change-left"><span class="change-firm">${esc(f.name)}</span><span class="change-desc">${esc(f.newsItem.change)}</span></div>
        <span class="change-date">${f.newsItem.date}</span>
      </a>`).join('')}
    </div>
  </section>

  <section class="wrap">
    <div class="section-head">
      <div><div class="num">Trending</div><h2>Firms traders are researching</h2><p>Ranked by composite score within our tracked set (illustrative, not live traffic data).</p></div>
    </div>
    <div class="trend-row">${trending.map((f,i)=>`<a href="#/firms/${f.slug}" class="trend-chip"><span class="trend-num">#${i+1}</span>${esc(f.name)}</a>`).join('')}</div>
  </section>

  <section class="wrap">
    <div class="section-head">
      <div><div class="num">Field reports</div><h2>Latest reviews</h2><p>Tagged by trading style, platform, and funded/payout status.</p></div>
      <a href="#/reviews" class="btn btn-ghost btn-sm">Read all reviews →</a>
    </div>
    <div class="review-grid">${latestReviews.map(reviewCard).join('')}</div>
  </section>

  <section class="wrap" style="border-bottom:none;">
    <div class="section-head">
      <div><div class="num">Research</div><h2>Research &amp; intelligence</h2><p>Explainers on how prop-firm mechanics actually work.</p></div>
    </div>
    <div class="research-grid">${research.map(articleCard).join('')}</div>
  </section>
  `;
}

function firmCard(f){
  return `<a href="#/firms/${f.slug}" class="firm-card">
    <div class="firm-card-top">
      <div><div class="firm-card-name">${esc(f.name)}</div><span class="cat-badge cat-${f.category}">${catLabel(f.category)}</span></div>
      <div class="firm-card-score">${f.score}<span>/100</span></div>
    </div>
    <div class="firm-card-stats">
      <div>Starting <b>$${f.priceFrom}</b></div>
      <div>Split <b>${f.split}%</b></div>
      <div>Payout <b>~${f.payoutDays}d</b></div>
      <div>Steps <b>${stepsLabel(f.steps)}</b></div>
    </div>
    <div class="firm-card-flags">
      <span class="flag-chip ${f.news?'yes':''}">${f.news?'✓':'✕'} News trading</span>
      <span class="flag-chip ${f.weekend?'yes':''}">${f.weekend?'✓':'✕'} Weekend hold</span>
    </div>
    <div class="firm-card-cta">Investigate →</div>
  </a>`;
}

function reviewCard(r){
  const f = firmBySlug(r.firmSlug);
  return `<div class="review-card">
    <div class="match-top"><a href="#/firms/${f.slug}" class="review-firm-link">${esc(f.name)}</a><span class="mono" style="font-size:12px; color:var(--text-dim);">${r.days}</span></div>
    <div class="review-tags">
      <span class="tag">${esc(r.style)}</span><span class="tag">${esc(r.platform)}</span>
      <span class="tag" style="color:${r.funded?'var(--success)':'var(--danger)'}">${r.funded?'Funded':'Not funded'}</span>
      <span class="tag" style="color:${r.paid?'var(--success)':'var(--danger)'}">${r.paid?'Paid':'Not paid'}</span>
    </div>
    <div class="review-body">${esc(r.body)}</div>
    <div style="margin-top:4px;">${vpill('user')}</div>
  </div>`;
}

function articleCard(a){
  return `<a href="#/research/${a.slug}" class="article-card">
    <div class="a-eyebrow">${esc(a.eyebrow)}</div>
    <h4>${esc(a.title)}</h4>
    <p>${esc(a.teaser)}</p>
  </a>`;
}

function initHomePage(){
  const input = document.getElementById('firmSearch');
  if(!input) return;
  input.addEventListener('input', e=>{
    const q = e.target.value.trim();
    document.getElementById('searchResults').innerHTML = q ? homeSearchPreview(q) : '';
  });
}
function homeSearchPreview(q){
  const hits = firms.filter(f=>f.name.toLowerCase().includes(q.toLowerCase()));
  return hits.length
    ? hits.map(f=>`<div style="padding:6px 0;">→ ${firmLink(f.slug, f.name)} — ${catLabel(f.category)} · score ${f.score}/100</div>`).join('')
    : `<div>No firm matches "${esc(q)}" — try <a href="#/firms" class="link-firm">the full directory</a>.</div>`;
}

/* ============================================================
   PAGE: FIRM DIRECTORY (/firms)
   ============================================================ */
function pageFirms(){
  return `
  <div class="wrap"><div class="crumbs"><a href="#/">Home</a> / <span>Firms</span></div></div>
  <section class="wrap" style="border-bottom:none; padding-top:24px;">
    <div class="section-head">
      <div><div class="num">Directory</div><h2>All tracked firms</h2><p>Filter by category, platform, price, payout speed, and rules — every card links to a full profile.</p></div>
    </div>
    <div class="filter-bar">
      <div class="filter-field"><label>Search</label><input type="text" id="dirSearch" placeholder="Firm name..."></div>
      <div class="filter-field"><label>Category</label><select id="dirCat"><option value="all">All</option><option value="futures">Futures</option><option value="cfd">CFD / Forex</option></select></div>
      <div class="filter-field"><label>Min score</label><select id="dirScore"><option value="0">Any</option><option value="70">70+</option><option value="80">80+</option><option value="90">90+</option></select></div>
      <div class="filter-field"><label>Platform</label><select id="dirPlatform"><option value="any">Any</option><option value="NT8">NinjaTrader</option><option value="TV">TradingView</option><option value="MT5">MT5</option></select></div>
      <div class="filter-field"><label>Max price</label><select id="dirPrice"><option value="9999">Any</option><option value="100">$100</option><option value="150">$150</option><option value="250">$250</option></select></div>
      <label class="filter-toggle"><input type="checkbox" id="dirNews"> News trading only</label>
      <label class="filter-toggle"><input type="checkbox" id="dirWeekend"> Weekend holding only</label>
      <span class="filter-count" id="dirCount"></span>
    </div>
    <div class="firm-grid" id="dirGrid"></div>
  </section>
  `;
}
function initFirmsPage(){
  const els = {
    search: document.getElementById('dirSearch'), cat: document.getElementById('dirCat'),
    score: document.getElementById('dirScore'), platform: document.getElementById('dirPlatform'),
    price: document.getElementById('dirPrice'), news: document.getElementById('dirNews'), weekend: document.getElementById('dirWeekend')
  };
  function apply(){
    let list = firms.filter(f=>{
      if(els.search.value.trim() && !f.name.toLowerCase().includes(els.search.value.trim().toLowerCase())) return false;
      if(els.cat.value!=='all' && f.category!==els.cat.value) return false;
      if(f.score < Number(els.score.value)) return false;
      if(els.platform.value!=='any' && !f.platforms.includes(els.platform.value)) return false;
      if(f.priceFrom > Number(els.price.value)) return false;
      if(els.news.checked && !f.news) return false;
      if(els.weekend.checked && !f.weekend) return false;
      return true;
    }).sort((a,b)=>b.score-a.score);
    document.getElementById('dirGrid').innerHTML = list.length ? list.map(firmCard).join('') : '<div class="search-empty">No firms match these filters.</div>';
    document.getElementById('dirCount').textContent = `${list.length} / ${firms.length} firms`;
  }
  Object.values(els).forEach(el => el.addEventListener('input', apply));
  apply();
}

/* ============================================================
   PAGE: FIRM PROFILE (/firms/:slug)
   ============================================================ */
const PROFILE_SECTIONS = [
  ['overview','Overview'],['rules','Rules'],['payouts','Payouts'],['health','Health'],
  ['leadership','Leadership'],['reviews','Reviews'],['history','History']
];
function pageFirm(f){
  const risk = riskLevel(f);
  const breakdown = healthBreakdown(f);
  const flags = riskFlags(f);
  const changelog = changelogFor(f);
  const frReviews = reviewsFor(f.slug);

  return `
  <div class="wrap"><div class="crumbs"><a href="#/">Home</a> / <a href="#/firms">Firms</a> / <span>${esc(f.name)}</span></div></div>
  <div class="wrap profile-hero">
    <div class="profile-top">
      <div>
        <div class="profile-badge-row">
          <span class="cat-badge cat-${f.category}">${catLabel(f.category)}</span>
          <span class="risk-badge ${risk.cls}">${risk.label}</span>
        </div>
        <h1 class="profile-title">${esc(f.name)}</h1>
        <div class="profile-sub">${esc(catLabel(f.category))} prop firm · HQ ${esc(f.hq)} · Founded ${f.founded||'unverified'}</div>
        <div class="profile-actions">
          ${f.officialUrl ? `<a class="btn btn-primary" href="${f.officialUrl}" target="_blank" rel="noopener">Visit official site ↗</a>` : `<span class="btn btn-ghost" style="opacity:.6; cursor:default;">Official site unverified</span>`}
          <a class="btn btn-ghost" href="#/compare">Add to compare</a>
          <a class="btn btn-ghost" href="#/firms/${f.slug}#reviews">Read reviews (${frReviews.length})</a>
        </div>
      </div>
      <div class="profile-score-box">
        <div class="profile-score-num">${f.score}</div>
        <div class="profile-score-label">Health score /100</div>
      </div>
    </div>
  </div>

  <div class="profile-subnav">
    <div class="profile-subnav-inner" id="profileSubnav">
      ${PROFILE_SECTIONS.map(([id,label])=>`<a href="#/firms/${f.slug}#${id}" data-sec="${id}">${label}</a>`).join('')}
    </div>
  </div>

  <div class="wrap">
    <section class="profile-section" id="overview">
      <h3>Quick facts</h3>
      <div class="fact-grid">
        <div class="fact-card"><div class="fact-label">Starting price ${vpill('editorial')}</div><div class="fact-value">$${f.priceFrom}</div><div class="fact-meta">Compiled from company pricing pages, Jul 2026</div></div>
        <div class="fact-card"><div class="fact-label">Profit split ${vpill('editorial')}</div><div class="fact-value">${f.split}%</div><div class="fact-meta">As disclosed by the firm</div></div>
        <div class="fact-card"><div class="fact-label">Evaluation type ${vpill('editorial')}</div><div class="fact-value">${stepsLabel(f.steps)}</div><div class="fact-meta">Program structure may vary by plan</div></div>
        <div class="fact-card"><div class="fact-label">Payout speed ${vpill('editorial')}</div><div class="fact-value">~${f.payoutDays} day${f.payoutDays===1?'':'s'}</div><div class="fact-meta">Firm-stated average, not independently audited</div></div>
        <div class="fact-card"><div class="fact-label">Platforms ${vpill('editorial')}</div><div class="fact-value" style="font-size:15px;">${f.platforms.join(', ')}</div><div class="fact-meta">Supported at time of writing</div></div>
        <div class="fact-card"><div class="fact-label">Founded ${vpill(f.founded?'editorial':'unverified')}</div><div class="fact-value">${f.founded||'—'}</div><div class="fact-meta">${f.founded?'Compiled from public company records':'Not independently verified'}</div></div>
        <div class="fact-card"><div class="fact-label">Headquarters ${vpill(f.hq.toLowerCase().includes('unverified')?'unverified':'editorial')}</div><div class="fact-value" style="font-size:15px;">${esc(f.hq)}</div><div class="fact-meta">Self-reported location</div></div>
      </div>
    </section>

    <section class="profile-section" id="rules">
      <h3>Trading rules</h3>
      <div class="fact-grid">
        <div class="fact-card"><div class="fact-label">Daily drawdown ${vpill('editorial')}</div><div class="fact-value">${f.category==='cfd' ? f.dailyDD+'%' : '$'+f.dailyDD.toLocaleString()}</div><div class="fact-meta">Source: official rules page · verify before funding</div></div>
        <div class="fact-card"><div class="fact-label">Maximum drawdown ${vpill('editorial')}</div><div class="fact-value">${f.category==='cfd' ? f.overallDD+'%' : '$'+f.overallDD.toLocaleString()}</div><div class="fact-meta">Source: official rules page</div></div>
        <div class="fact-card"><div class="fact-label">Drawdown type <span class="tooltip-term" title="Trailing floors rise with peak equity, often intraday. EOD floors only reset once per day. Confirm directly with the firm.">ⓘ</span> ${vpill('unverified')}</div><div class="fact-value" style="font-size:14px;">Not independently verified</div><div class="fact-meta">Confirm trailing vs. EOD directly with the firm — see our <a href="#/research/trailing-drawdown">drawdown explainer</a></div></div>
        <div class="fact-card"><div class="fact-label">News trading ${vpill('editorial')}</div><div class="fact-value ${f.news?'yes':'no'}">${f.news?'Allowed':'Not allowed'}</div><div class="fact-meta">As stated in public rules</div></div>
        <div class="fact-card"><div class="fact-label">Weekend / overnight holding ${vpill('editorial')}</div><div class="fact-value ${f.weekend?'yes':'no'}">${f.weekend?'Allowed':'Not allowed'}</div><div class="fact-meta">As stated in public rules</div></div>
        <div class="fact-card"><div class="fact-label">Consistency rule ${vpill('unverified')}</div><div class="fact-value" style="font-size:14px;">Not independently verified</div><div class="fact-meta">Varies by plan — check official rules</div></div>
        <div class="fact-card"><div class="fact-label">Min. trading days / scaling ${vpill('unverified')}</div><div class="fact-value" style="font-size:14px;">Not independently verified</div><div class="fact-meta">Check official rules before funding</div></div>
      </div>
    </section>

    <section class="profile-section" id="payouts">
      <h3>Payout intelligence</h3>
      <div class="fact-grid">
        <div class="fact-card"><div class="fact-label">Average payout time ${vpill('editorial')}</div><div class="fact-value">~${f.payoutDays}d</div><div class="fact-meta">Firm-stated average</div></div>
        <div class="fact-card"><div class="fact-label">Payout methods ${vpill('unverified')}</div><div class="fact-value" style="font-size:14px;">Not independently verified</div><div class="fact-meta">Check official site</div></div>
        <div class="fact-card"><div class="fact-label">Minimum payout ${vpill('unverified')}</div><div class="fact-value" style="font-size:14px;">Not independently verified</div><div class="fact-meta">Varies by plan</div></div>
        <div class="fact-card"><div class="fact-label">Public payout evidence ${vpill('unverified')}</div><div class="fact-value" style="font-size:14px;">Limited / self-reported</div><div class="fact-meta">No independent audit trail located at time of writing</div></div>
      </div>
      <div class="why-score">This site does not treat a firm's own "total paid out" figure as verified fact. See <a href="#/research/payout-verification" class="link-firm">why payout claims are hard to verify</a>.</div>
    </section>

    <section class="profile-section" id="health">
      <h3>Health score breakdown</h3>
      ${breakdown.map(b=>`
        <div class="score-bar-row">
          <div class="score-bar-label">${esc(b.label)}</div>
          <div class="score-bar-track"><div class="score-bar-fill" data-w="${(b.value/b.max*100)}"></div></div>
          <div class="score-bar-val">${b.value}/${b.max}</div>
        </div>`).join('')}
      <div class="why-score"><b style="color:var(--text)">Why this score?</b> Weighted from verified leadership status, public Trustpilot signal (when present), years of operating history, disclosed rule flexibility, and platform coverage. This is an editorial model, not a credit rating or regulatory score — see <a href="#/about" class="link-firm">methodology</a>.</div>

      <h3 style="margin-top:36px;">Risk flags</h3>
      <div class="flags-cols">
        <div class="flags-col pos"><h5>Positive signals</h5>${flags.pos.map(p=>`<div class="flag-line"><span style="color:var(--success)">✓</span>${esc(p)}</div>`).join('')}</div>
        <div class="flags-col neg"><h5>Watch items</h5>${flags.neg.map(n=>`<div class="flag-line"><span style="color:var(--warn)">⚠</span>${esc(n)}</div>`).join('')}</div>
      </div>
    </section>

    <section class="profile-section" id="leadership">
      <h3>Company &amp; leadership</h3>
      <div class="fact-grid">
        <div class="fact-card" style="grid-column:span 2;">
          <div class="fact-label">Leadership ${vpill(f.leadership.verified?'verified':'unverified')}</div>
          <div class="fact-value" style="font-size:17px;">${f.leadership.name || 'Not publicly confirmed'}</div>
          <div class="fact-meta">${esc(f.leadership.title)}${f.leadership.co ? ' · '+esc(f.leadership.co) : ''}${f.leadership.sourceUrl ? `<br>Source: <a href="${f.leadership.sourceUrl}" target="_blank" rel="noopener">${esc(f.leadership.sourceLabel)}</a>` : ''}</div>
        </div>
        <div class="fact-card"><div class="fact-label">Headquarters</div><div class="fact-value" style="font-size:15px;">${esc(f.hq)}</div></div>
        <div class="fact-card"><div class="fact-label">Founded</div><div class="fact-value">${f.founded||'Unverified'}</div></div>
      </div>
    </section>

    <section class="profile-section" id="reviews">
      <h3>Trader reviews (${frReviews.length})</h3>
      ${frReviews.length ? `<div class="review-grid">${frReviews.map(reviewCard).join('')}</div>` : `<div class="search-empty" style="text-align:left; padding:0;">No reviews tracked for ${esc(f.name)} yet. <a href="#/reviews" class="link-firm">Browse all reviews →</a></div>`}
    </section>

    <section class="profile-section" id="history" style="border-bottom:none;">
      <h3>Change log</h3>
      ${changelog.length ? `<div class="timeline">${changelog.map(c=>`
        <div class="timeline-item">
          <div class="timeline-date">${c.date}</div>
          <div class="timeline-body">${esc(c.change)}<div class="timeline-src">Source: ${esc(c.source)}</div></div>
        </div>`).join('')}</div>` : `<div class="search-empty" style="text-align:left; padding:0;">No independently reported changes tracked for ${esc(f.name)} yet.</div>`}
    </section>
  </div>
  `;
}
function initFirmPage(slug){
  document.querySelectorAll('.score-bar-fill').forEach(el=>{ const w = el.dataset.w; requestAnimationFrame(()=>{ el.style.width = w+'%'; }); });
  const links = document.querySelectorAll('#profileSubnav a');
  function setActiveByScroll(){
    let current = PROFILE_SECTIONS[0][0];
    PROFILE_SECTIONS.forEach(([id])=>{ const el = document.getElementById(id); if(el && el.getBoundingClientRect().top < 160) current = id; });
    links.forEach(l=> l.classList.toggle('active', l.dataset.sec===current));
  }
  window.addEventListener('scroll', setActiveByScroll, {passive:true});
  setActiveByScroll();
}

/* ============================================================
   PAGE: COMPARE
   ============================================================ */
function pageCompare(){
  if(compareSelection.length===0) compareSelection = firms.slice(0,3).map(f=>f.slug);
  return `
  <div class="wrap"><div class="crumbs"><a href="#/">Home</a> / <span>Compare</span></div></div>
  <section class="wrap" style="border-bottom:none; padding-top:24px;">
    <div class="section-head">
      <div><div class="num">Side by side</div><h2>Compare 2–4 firms</h2><p>Pick firms below — winner indicators highlight the best value on speed-sensitive fields.</p></div>
    </div>
    <div class="compare-picker" id="comparePicker"></div>
    <div class="table-scroll">
      <table id="compareTable">
        <thead><tr>
          <th>Firm</th><th>Score*</th><th>Category</th><th>Daily DD</th><th>Overall DD</th>
          <th>Profit split</th><th>News trading</th><th>Weekend hold</th><th>Platforms</th>
          <th>Steps</th><th>Payout speed</th><th>Price from</th>
        </tr></thead>
        <tbody id="compareBody"></tbody>
      </table>
    </div>
    <div class="data-note" style="margin-top:12px;">*Composite score is an editorial estimate blending public Trustpilot ratings, years operating, and press coverage — not a regulatory rating. ✓ marks the best value in that row among the firms selected.</div>
  </section>
  `;
}
function initComparePage(){
  function renderPicker(){
    document.getElementById('comparePicker').innerHTML = firms.map(f=>{
      const active = compareSelection.includes(f.slug);
      const disabled = !active && compareSelection.length>=4;
      return `<button class="compare-chip ${active?'active':''}" data-slug="${f.slug}" ${disabled?'disabled':''}>${active?'✓ ':''}${esc(f.name)}</button>`;
    }).join('');
    document.querySelectorAll('.compare-chip').forEach(btn=>{
      btn.onclick = ()=>{
        const slug = btn.dataset.slug;
        if(compareSelection.includes(slug)) compareSelection = compareSelection.filter(s=>s!==slug);
        else if(compareSelection.length<4) compareSelection.push(slug);
        renderPicker(); renderTable();
      };
    });
  }
  function bestFor(rows, key, higherBetter){
    const vals = rows.map(r=>r[key]);
    return higherBetter ? Math.max(...vals) : Math.min(...vals);
  }
  function renderTable(){
    const rows = compareSelection.map(firmBySlug).filter(Boolean);
    if(!rows.length){ document.getElementById('compareBody').innerHTML = `<tr><td colspan="12" class="search-empty">Select at least 2 firms above.</td></tr>`; return; }
    const bestScore = bestFor(rows,'score',true);
    const bestSplit = bestFor(rows,'split',true);
    const bestPayout = bestFor(rows,'payoutDays',false);
    const bestPrice = bestFor(rows,'priceFrom',false);
    document.getElementById('compareBody').innerHTML = rows.map(f=>`
      <tr>
        <td class="firm-cell"><a href="#/firms/${f.slug}">${esc(f.name)}</a></td>
        <td class="${f.score===bestScore?'winner-cell':''}"><span class="trust-pill ${scoreClass(f.score)}">${f.score}</span></td>
        <td><span class="cat-badge cat-${f.category}">${catLabel(f.category)}</span></td>
        <td class="mono">${f.category==='cfd' ? f.dailyDD+'%' : '$'+f.dailyDD.toLocaleString()}</td>
        <td class="mono">${f.category==='cfd' ? f.overallDD+'%' : '$'+f.overallDD.toLocaleString()}</td>
        <td class="mono ${f.split===bestSplit?'winner-cell':''}">${f.split}%</td>
        <td class="${f.news?'yes':'no'}">${f.news?'Yes':'No'}</td>
        <td class="${f.weekend?'yes':'no'}">${f.weekend?'Yes':'No'}</td>
        <td>${f.platforms.join(', ')}</td>
        <td class="mono">${stepsLabel(f.steps)}</td>
        <td class="mono ${f.payoutDays===bestPayout?'winner-cell':''}">${f.payoutDays}d</td>
        <td class="mono ${f.priceFrom===bestPrice?'winner-cell':''}">$${f.priceFrom}</td>
      </tr>
    `).join('');
  }
  renderPicker(); renderTable();
}

/* ============================================================
   PAGE: MATCH ENGINE
   ============================================================ */
const matchAnswers = {};
function pageMatch(){
  return `
  <div class="wrap"><div class="crumbs"><a href="#/">Home</a> / <span>Match Me</span></div></div>
  <section class="wrap" style="border-bottom:none; padding-top:24px;">
    <div class="section-head">
      <div><div class="num">Match engine</div><h2>Answer 7 questions. Get a ranked match.</h2><p>We score every firm against your trading style, budget, and platform — then explain exactly why the runner-ups fall short.</p></div>
    </div>
    <div class="quiz-shell">
      <div>
        <div class="q-group"><div class="q-label">Market</div><div class="q-options" data-key="market">
          <div class="q-opt" data-val="futures">Futures</div><div class="q-opt" data-val="forex">Forex</div>
        </div></div>
        <div class="q-group"><div class="q-label">Style</div><div class="q-options" data-key="style">
          <div class="q-opt" data-val="scalp">Scalping</div><div class="q-opt" data-val="swing">Swing / hold overnight</div><div class="q-opt" data-val="day">Day trading, flat by close</div>
        </div></div>
        <div class="q-group"><div class="q-label">News trading</div><div class="q-options" data-key="news">
          <div class="q-opt" data-val="yes">I trade the news</div><div class="q-opt" data-val="no">Doesn't matter</div>
        </div></div>
        <div class="q-group"><div class="q-label">Max budget for evaluation</div><div class="q-options" data-key="budget">
          <div class="q-opt" data-val="150">Under $150</div><div class="q-opt" data-val="300">Under $300</div><div class="q-opt" data-val="9999">No limit</div>
        </div></div>
        <div class="q-group"><div class="q-label">Challenge type</div><div class="q-options" data-key="steps">
          <div class="q-opt" data-val="one">One-step</div><div class="q-opt" data-val="two">Two-step</div><div class="q-opt" data-val="any">Either</div>
        </div></div>
        <div class="q-group"><div class="q-label">Platform</div><div class="q-options" data-key="platform">
          <div class="q-opt" data-val="NT8">NinjaTrader</div><div class="q-opt" data-val="TV">TradingView</div><div class="q-opt" data-val="MT5">MT5</div><div class="q-opt" data-val="any">No preference</div>
        </div></div>
        <div class="q-group"><div class="q-label">Payout speed priority</div><div class="q-options" data-key="payout">
          <div class="q-opt" data-val="fast">Fastest possible</div><div class="q-opt" data-val="standard">Standard is fine</div>
        </div></div>
      </div>
      <div class="result-panel" id="resultPanel"><div style="color:var(--text-dim); font-size:13.5px;">Answer the questions on the left — your match updates live.</div></div>
    </div>
  </section>
  `;
}
function initMatchPage(){
  document.querySelectorAll('.q-options').forEach(group=>{
    // restore previous selection visuals
    const key = group.dataset.key;
    if(matchAnswers[key]){
      [...group.children].forEach(c=>c.classList.toggle('active', c.dataset.val===matchAnswers[key]));
    }
    group.addEventListener('click', e=>{
      const opt = e.target.closest('.q-opt');
      if(!opt) return;
      [...group.children].forEach(c=>c.classList.remove('active'));
      opt.classList.add('active');
      matchAnswers[key] = opt.dataset.val;
      runMatch();
    });
  });
  runMatch();
}
function runMatch(){
  const panel = document.getElementById('resultPanel');
  if(!panel) return;
  const answers = matchAnswers;
  const answered = Object.keys(answers).length;
  if(answered < 3){
    panel.innerHTML = `<div style="color:var(--text-dim); font-size:13.5px;">Answer at least 3 questions to see a preliminary match (${answered}/7 so far).</div>`;
    return;
  }
  const scored = firms.map(f=>{
    let score = 40; const reasons = []; const concerns = []; const avoid = [];
    if(answers.market){
      const wantCat = answers.market === 'forex' ? 'cfd' : 'futures';
      if(f.category === wantCat){ score += 18; reasons.push(`Supports ${answers.market} trading`); }
      else { score -= 30; avoid.push(`Doesn't offer ${answers.market} accounts`); concerns.push(`Doesn't offer ${answers.market} accounts`); }
    }
    if(answers.style){
      if(f.style.includes(answers.style)){ score += 14; reasons.push(`Rules fit a ${answers.style==='scalp'?'scalping':answers.style} approach`); }
      else { score -= 10; concerns.push('Not clearly suited to your trading style'); }
    }
    if(answers.news){
      if(answers.news==='yes'){ if(f.news){ score+=12; reasons.push('Allows news trading'); } else { score-=20; avoid.push(`Doesn't allow news trading`); concerns.push(`Doesn't allow news trading`); } }
    }
    if(answers.budget){
      const b = Number(answers.budget);
      if(f.priceFrom <= b){ score += 8; reasons.push(`Evaluation starts at $${f.priceFrom}, within budget`); }
      else { score -= 15; avoid.push(`Starting price ($${f.priceFrom}) exceeds your budget`); concerns.push(`Starting price ($${f.priceFrom}) exceeds your budget`); }
    }
    if(answers.steps && answers.steps!=='any'){
      if(f.steps===answers.steps || f.steps==='any'){ score += 8; reasons.push(`${answers.steps==='one'?'One-step':'Two-step'} evaluation available`); }
      else { score -= 8; concerns.push(`Only offers a ${f.steps}-step evaluation`); }
    }
    if(answers.platform && answers.platform!=='any'){
      if(f.platforms.includes(answers.platform)){ score += 10; reasons.push(`Supports ${answers.platform}`); }
      else { score -= 14; avoid.push(`Doesn't support ${answers.platform}`); concerns.push(`Doesn't support ${answers.platform}`); }
    }
    if(answers.payout==='fast'){
      if(f.payoutDays<=2){ score += 10; reasons.push(`Fast payouts — avg ${f.payoutDays} day(s)`); }
      else { score -= 6; concerns.push(`Slower payout cycle (~${f.payoutDays} days)`); }
    }
    if(answers.style==='swing'){
      if(f.weekend){ score += 6; reasons.push('Allows weekend/overnight holding'); }
      else { score -= 18; avoid.push(`Doesn't allow overnight holding`); concerns.push(`Doesn't allow overnight holding`); }
    }
    if(!f.leadership.verified) concerns.push('Leadership not independently verified');
    if(!f.trustpilot) concerns.push('No public Trustpilot rating on file');
    score = Math.max(2, Math.min(98, score));
    return {...f, matchScore:score, reasons, concerns, avoid};
  }).sort((a,b)=>b.matchScore-a.matchScore);

  const [best, second, third] = scored;
  const avoided = scored.filter(f=>f.avoid.length>=2).slice(0,2);

  function matchCardHTML(m, isBest){
    return `<div class="match-card ${isBest?'best':''}">
      <div class="match-top">${firmLink(m.slug, (isBest?'🏆 ':'')+m.name, 'match-name')}<span class="match-score">${m.matchScore}%</span></div>
      <ul class="match-reasons">${m.reasons.slice(0,4).map(r=>`<li>${esc(r)}</li>`).join('')}</ul>
      ${m.concerns.length? `<ul class="match-concerns">${m.concerns.slice(0,3).map(c=>`<li>${esc(c)}</li>`).join('')}</ul>` : ''}
      <a href="#/firms/${m.slug}" class="match-cta">View full ${esc(m.name)} investigation →</a>
    </div>`;
  }
  panel.innerHTML = `
    <div style="font-size:12px; font-family:'IBM Plex Mono'; color:var(--text-dim); text-transform:uppercase; letter-spacing:.05em;">Your best match (${answered}/7 answered)</div>
    ${matchCardHTML(best, true)}
    <div style="font-size:11px; font-family:'IBM Plex Mono'; color:var(--text-faint); text-transform:uppercase; letter-spacing:.05em; margin-top:6px;">2nd best match</div>
    ${second ? matchCardHTML(second,false) : ''}
    <div style="font-size:11px; font-family:'IBM Plex Mono'; color:var(--text-faint); text-transform:uppercase; letter-spacing:.05em; margin-top:6px;">3rd best match</div>
    ${third ? matchCardHTML(third,false) : ''}
    ${avoided.length ? `<div class="avoid-list">
      <div style="font-size:12px; font-family:'IBM Plex Mono'; color:var(--danger); text-transform:uppercase; letter-spacing:.05em; margin-bottom:8px;">Probably avoid</div>
      ${avoided.map(f=>`<div class="avoid-item"><b>${esc(f.name)}</b> — ${esc(f.avoid[0])}</div>`).join('')}
    </div>` : ''}
  `;
}

/* ============================================================
   PAGE: HEALTH
   ============================================================ */
function pageHealth(){
  return `
  <div class="wrap"><div class="crumbs"><a href="#/">Home</a> / <span>Health</span></div></div>
  <section class="wrap" style="border-bottom:none; padding-top:24px;">
    <div class="section-head">
      <div><div class="num">Firm health</div><h2>Public track record, at a glance</h2><p>Trustpilot ratings and years operating where publicly disclosed — flagged clearly when we couldn't verify a number. Editorial scoring, not a regulatory or financial guarantee.</p></div>
      <div class="cat-tabs" id="healthTabs">
        <button class="cat-tab active" data-cat="all">All</button>
        <button class="cat-tab" data-cat="futures">Futures</button>
        <button class="cat-tab" data-cat="cfd">CFD / Forex</button>
      </div>
    </div>
    <div class="health-grid" id="healthGrid"></div>
    <div class="data-note" style="margin-top:16px;">Risk labels (LOW RISK / MEDIUM RISK / UNVERIFIED) are an editorial estimate derived from public signal availability, not a credit rating, audit, or financial advice. See <a href="#/about" style="color:var(--amber-dim)">methodology</a>.</div>
  </section>
  `;
}
function initHealthPage(){
  function renderGrid(cat){
    const rows = cat==='all' ? firms : firms.filter(f=>f.category===cat);
    document.getElementById('healthGrid').innerHTML = rows.map(f=>{
      const risk = riskLevel(f);
      return `<a href="#/firms/${f.slug}" class="health-card">
        <div class="health-head"><h4>${esc(f.name)}</h4><span class="risk-badge ${risk.cls}">${risk.label}</span></div>
        <div class="health-rows">
          <div class="health-row"><span>Composite score</span><span><span class="trust-pill ${scoreClass(f.score)}">${f.score}/100</span></span></div>
          <div class="health-row"><span>Trustpilot</span><span>${f.trustpilot ? `${f.trustpilot}/5 <span style="color:var(--text-dim)">(${f.tpDate})</span>` : `<span style="color:var(--text-dim)">Not verified</span>`}</span></div>
          <div class="health-row"><span>Years operating</span><span>${f.founded ? (NOW_YEAR-f.founded)+'y' : 'Unverified'}</span></div>
          <div class="health-row"><span>Leadership</span><span>${f.leadership.verified ? '✓ Verified' : '⚠ Unverified'}</span></div>
          <div class="health-row"><span>Category</span><span><span class="cat-badge cat-${f.category}">${catLabel(f.category)}</span></span></div>
        </div>
      </a>`;
    }).join('');
  }
  document.querySelectorAll('#healthTabs .cat-tab').forEach(tab=>{
    tab.onclick = ()=>{ document.querySelectorAll('#healthTabs .cat-tab').forEach(t=>t.classList.remove('active')); tab.classList.add('active'); renderGrid(tab.dataset.cat); };
  });
  renderGrid('all');
}

/* ============================================================
   PAGE: REVIEWS
   ============================================================ */
function pageReviews(){
  return `
  <div class="wrap"><div class="crumbs"><a href="#/">Home</a> / <span>Reviews</span></div></div>
  <section class="wrap" style="border-bottom:none; padding-top:24px;">
    <div class="section-head">
      <div><div class="num">Field reports</div><h2>Trader reviews</h2><p>Filtered by how the reviewer actually trades — not anonymous star ratings. ${vpill('user')} marks user-submitted content.</p></div>
    </div>
    <div class="filter-bar">
      <div class="filter-field"><label>Firm</label><select id="revFirm"><option value="all">All firms</option>${firms.map(f=>`<option value="${f.slug}">${esc(f.name)}</option>`).join('')}</select></div>
      <div class="filter-field"><label>Style</label><select id="revStyle"><option value="all">Any</option><option value="Scalper">Scalper</option><option value="Day Trader">Day Trader</option><option value="Swing">Swing</option></select></div>
      <div class="filter-field"><label>Platform</label><select id="revPlatform"><option value="all">Any</option><option value="NinjaTrader">NinjaTrader</option><option value="TradingView">TradingView</option><option value="MT5">MT5</option></select></div>
      <label class="filter-toggle"><input type="checkbox" id="revFunded"> Funded only</label>
      <label class="filter-toggle"><input type="checkbox" id="revPaid"> Paid out only</label>
      <span class="filter-count" id="revCount"></span>
    </div>
    <div class="review-grid" id="revGrid"></div>
  </section>
  `;
}
function initReviewsPage(){
  const els = {firm:document.getElementById('revFirm'), style:document.getElementById('revStyle'), platform:document.getElementById('revPlatform'), funded:document.getElementById('revFunded'), paid:document.getElementById('revPaid')};
  function apply(){
    const list = reviews.filter(r=>{
      if(els.firm.value!=='all' && r.firmSlug!==els.firm.value) return false;
      if(els.style.value!=='all' && r.style!==els.style.value) return false;
      if(els.platform.value!=='all' && r.platform!==els.platform.value) return false;
      if(els.funded.checked && !r.funded) return false;
      if(els.paid.checked && !r.paid) return false;
      return true;
    });
    document.getElementById('revGrid').innerHTML = list.length ? list.map(reviewCard).join('') : '<div class="search-empty">No reviews match these filters.</div>';
    document.getElementById('revCount').textContent = `${list.length} / ${reviews.length} reviews`;
  }
  Object.values(els).forEach(el=>el.addEventListener('input', apply));
  apply();
}

/* ============================================================
   PAGE: OFFERS (formerly coupons — no fabricated codes)
   ============================================================ */
function pageOffers(){
  const withUrl = firms.filter(f=>f.officialUrl);
  const withoutUrl = firms.filter(f=>!f.officialUrl);
  return `
  <div class="wrap"><div class="crumbs"><a href="#/">Home</a> / <span>Offers</span></div></div>
  <section class="wrap" style="border-bottom:none; padding-top:24px;">
    <div class="section-head">
      <div><div class="num">Offers</div><h2>Official links, not fabricated codes</h2><p>We used to list "auto-tracked" discount codes here. We removed them: we can't independently confirm any specific code is live, unexpired, or actually issued by the firm — and posting invented codes is exactly the kind of unverifiable claim this site exists to call out.</p></div>
    </div>
    <div class="scam-banner" style="max-width:none;">
      <span>⚠</span>
      <span>PropFirmScam does not issue, generate, or verify discount codes. Any current promotion is controlled entirely by the firm and can change without notice. Check the firm's own pricing page before paying for an evaluation.</span>
    </div>
    <div class="coupon-grid" style="margin-top:28px;">
      ${withUrl.map(f=>`<div class="coupon-card">
        <h4>${esc(f.name)}</h4>
        <div class="coupon-note">Starting price we've tracked: <b class="mono" style="color:var(--text)">$${f.priceFrom}</b>. Current promotions, if any, live on the firm's own site.</div>
        ${vpill('editorial')}
        <a class="btn btn-ghost btn-sm" style="justify-content:center;" href="${f.officialUrl}" target="_blank" rel="noopener">Check official offers ↗</a>
        <a href="#/firms/${f.slug}" class="link-firm" style="font-size:12.5px;">View full profile →</a>
      </div>`).join('')}
    </div>
    ${withoutUrl.length ? `<div class="data-note" style="margin-top:24px;">No independently confirmed official domain on file for: ${withoutUrl.map(f=>esc(f.name)).join(', ')}. We won't link to a guessed URL — search cautiously and verify the domain yourself before entering payment details.</div>` : ''}
  </section>
  `;
}

/* ============================================================
   PAGE: TOOLS
   ============================================================ */
function pageTools(){
  return `
  <div class="wrap"><div class="crumbs"><a href="#/">Home</a> / <span>Tools</span></div></div>
  <section class="wrap" style="border-bottom:none; padding-top:24px;">
    <div class="section-head"><div><div class="num">Trader tools</div><h2>Free calculators</h2><p>Fixed-risk position sizing, drawdown buffer, and challenge probability — no signup, nothing is stored.</p></div></div>
    <div class="tools-grid">
      <div class="tool-card">
        <h4>Position size calculator</h4>
        <div class="field-row"><div class="field"><label>Account size ($)</label><input type="number" id="ps_account" value="50000"></div><div class="field"><label>Risk per trade ($)</label><input type="number" id="ps_risk" value="500"></div></div>
        <div class="field-row"><div class="field"><label>Stop distance (ticks)</label><input type="number" id="ps_ticks" value="12"></div><div class="field"><label>Tick value ($)</label><input type="number" id="ps_tickval" value="12.50"></div></div>
        <button class="btn btn-ghost" style="width:100%; justify-content:center;" onclick="calcPositionSize()">Calculate</button>
        <div class="tool-output" id="ps_out">Contracts: —</div>
      </div>
      <div class="tool-card">
        <h4>Drawdown buffer calculator</h4>
        <div class="field-row"><div class="field"><label>Starting balance ($)</label><input type="number" id="dd_start" value="150000"></div><div class="field"><label>Max drawdown ($)</label><input type="number" id="dd_max" value="4500"></div></div>
        <div class="field-row"><div class="field"><label>Current equity ($)</label><input type="number" id="dd_current" value="151200"></div><div class="field"><label>DD type</label><select id="dd_type"><option value="eod">End-of-day</option><option value="trailing">Trailing (live)</option></select></div></div>
        <button class="btn btn-ghost" style="width:100%; justify-content:center;" onclick="calcDrawdown()">Calculate</button>
        <div class="tool-output" id="dd_out">Buffer remaining: —</div>
      </div>
      <div class="tool-card">
        <h4>Challenge probability estimator</h4>
        <div class="field-row"><div class="field"><label>Win rate (%)</label><input type="number" id="cp_wr" value="52"></div><div class="field"><label>Avg R:R</label><input type="number" id="cp_rr" value="1.5" step="0.1"></div></div>
        <div class="field-row"><div class="field"><label>Trades to target</label><input type="number" id="cp_trades" value="40"></div></div>
        <button class="btn btn-ghost" style="width:100%; justify-content:center;" onclick="calcProbability()">Estimate</button>
        <div class="tool-output" id="cp_out">Estimated edge: —</div>
      </div>
      <div class="tool-card">
        <h4>Consistency rule checker</h4>
        <div class="field-row"><div class="field"><label>Total profit so far ($)</label><input type="number" id="cr_total" value="9000"></div><div class="field"><label>Best single day ($)</label><input type="number" id="cr_best" value="3200"></div></div>
        <div class="field-row"><div class="field"><label>Consistency rule (%)</label><input type="number" id="cr_rule" value="30"></div></div>
        <button class="btn btn-ghost" style="width:100%; justify-content:center;" onclick="calcConsistency()">Check</button>
        <div class="tool-output" id="cr_out">Status: —</div>
      </div>
    </div>
  </section>
  `;
}
function initToolsPage(){ calcPositionSize(); calcDrawdown(); calcProbability(); calcConsistency(); }
function calcPositionSize(){
  const acc = +document.getElementById('ps_account').value, risk = +document.getElementById('ps_risk').value;
  const ticks = +document.getElementById('ps_ticks').value, tickVal = +document.getElementById('ps_tickval').value;
  const perContractRisk = ticks * tickVal;
  const contracts = perContractRisk > 0 ? Math.floor(risk / perContractRisk) : 0;
  document.getElementById('ps_out').innerHTML = `Contracts: <b>${contracts}</b> &nbsp;|&nbsp; Risk per contract: $${perContractRisk.toFixed(2)} &nbsp;|&nbsp; Total risk: $${(contracts*perContractRisk).toFixed(2)} (${((contracts*perContractRisk)/acc*100).toFixed(2)}% of account)`;
}
function calcDrawdown(){
  const start = +document.getElementById('dd_start').value, max = +document.getElementById('dd_max').value;
  const current = +document.getElementById('dd_current').value, type = document.getElementById('dd_type').value;
  const floor = type==='eod' ? start-max : Math.max(start,current)-max;
  const buffer = current-floor;
  document.getElementById('dd_out').innerHTML = `Drawdown floor: <b>$${floor.toLocaleString()}</b> &nbsp;|&nbsp; Buffer remaining: <b style="color:${buffer>0?'var(--success)':'var(--danger)'}">$${buffer.toLocaleString()}</b>`;
}
function calcProbability(){
  const wr = +document.getElementById('cp_wr').value/100, rr = +document.getElementById('cp_rr').value, trades = +document.getElementById('cp_trades').value;
  const expectancyR = (wr*rr)-(1-wr);
  const edge = expectancyR>0?'Positive':expectancyR===0?'Breakeven':'Negative';
  document.getElementById('cp_out').innerHTML = `Expectancy: <b>${expectancyR.toFixed(3)}R</b> per trade &nbsp;|&nbsp; Over ${trades} trades: <b>${(expectancyR*trades).toFixed(1)}R</b> &nbsp;|&nbsp; Edge: <b style="color:${expectancyR>0?'var(--success)':'var(--danger)'}">${edge}</b>`;
}
function calcConsistency(){
  const total = +document.getElementById('cr_total').value, best = +document.getElementById('cr_best').value, rule = +document.getElementById('cr_rule').value/100;
  const pct = total>0 ? (best/total*100) : 0; const pass = pct <= rule*100;
  document.getElementById('cr_out').innerHTML = `Best day is <b>${pct.toFixed(1)}%</b> of total profit (limit ${(rule*100).toFixed(0)}%) — <b style="color:${pass?'var(--success)':'var(--danger)'}">${pass?'Within rule':'Rule breached'}</b>`;
}

/* ============================================================
   PAGE: ARENA (games — secondary) + GROWTH
   ============================================================ */
function pageArena(){
  return `
  <div class="wrap"><div class="crumbs"><a href="#/">Home</a> / <span>Arena</span></div></div>
  <section class="wrap secondary-band" style="border-bottom:none; padding-top:24px;">
    <div class="arena-head">
      <div><div class="num">Extras</div><h2 style="margin-top:4px;">Prove you're better than your P&amp;L suggests</h2><p>Three dumb little games for traders who are "just checking one chart" at 2am. No signup, no stakes, mild public shame only.</p></div>
      <div class="game-badge">Scores reset on refresh — this is a demo arena, not your prop firm</div>
    </div>
    <div class="game-grid">
      <div class="game-card">
        <div><div class="game-badge">Reflexes</div><h4 style="margin-top:8px;">🪜 Price Ladder</h4><div class="desc">Guess if the next tick goes up or down. Streak resets on the first wrong call — just like your account.</div></div>
        <div class="game-stage">
          <div class="big-price mono" id="ladder_price">100.00</div>
          <div class="game-msg" id="ladder_msg">Make the call.</div>
          <div class="game-row"><button class="btn btn-up" onclick="ladderGuess('up')">▲ Up</button><button class="btn btn-down" onclick="ladderGuess('down')">▼ Down</button></div>
          <div class="streak-row"><span>Streak: <b id="ladder_streak" class="mono" style="color:var(--text)">0</b></span><span>Best: <b id="ladder_best" class="mono" style="color:var(--text)">0</b></span></div>
        </div>
      </div>
      <div class="game-card">
        <div><div class="game-badge">Pattern memory</div><h4 style="margin-top:8px;">🧠 Signal Recall</h4><div class="desc">Watch the candle sequence, then repeat it back. Every round adds one more candle.</div></div>
        <div class="game-stage">
          <div class="game-msg" id="signal_msg">Level 0 — tap start to watch the sequence.</div>
          <div class="candle-icons" id="signal_icons">
            <button class="candle-btn" data-c="green" onclick="signalInput('green')">🟩</button>
            <button class="candle-btn" data-c="red" onclick="signalInput('red')">🟥</button>
            <button class="candle-btn" data-c="doji" onclick="signalInput('doji')">⬜</button>
            <button class="candle-btn" data-c="spike" onclick="signalInput('spike')">⚡</button>
          </div>
          <div class="streak-row"><span>Level: <b id="signal_level" class="mono" style="color:var(--text)">0</b></span><span>Best: <b id="signal_best" class="mono" style="color:var(--text)">0</b></span></div>
          <button class="btn btn-primary" style="width:100%; justify-content:center;" onclick="startSignalGame()">Start / Restart</button>
        </div>
      </div>
      <div class="game-card">
        <div><div class="game-badge">Competition</div><h4 style="margin-top:8px;">⏱️ The 5-Minute Gauntlet</h4><div class="desc">A fake market ticks for 5 real minutes. Go long, short, or flat. End P&amp;L gets ranked on the leaderboard.</div></div>
        <div class="game-stage" style="align-items:stretch;">
          <canvas id="sim_canvas" height="110"></canvas>
          <div class="sim-hud"><span>Time: <b id="sim_time">5:00</b></span><span>Price: <b id="sim_price">100.00</b></span><span>Pos: <b id="sim_pos">FLAT</b></span><span>P&amp;L: <b id="sim_pnl">$0</b></span></div>
          <div class="game-row"><button class="btn btn-up" onclick="simSetPosition('long')">Long</button><button class="btn btn-ghost" style="justify-content:center;" onclick="simSetPosition('flat')">Flat</button><button class="btn btn-down" onclick="simSetPosition('short')">Short</button></div>
          <button class="btn btn-primary" style="width:100%; justify-content:center;" id="sim_startbtn" onclick="startSim()">Start Today's Gauntlet</button>
          <div class="game-msg" id="sim_msg"></div>
          <div class="leaderboard" id="sim_leaderboard"></div>
        </div>
      </div>
    </div>
  </section>

  <section class="wrap secondary-band" style="border-bottom:none;">
    <div class="section-head"><div><div class="num">Community</div><h2>Grow the desk</h2><p>Invite codes, embeddable badges, and the confession wall nobody asked for.</p></div></div>
    <div class="growth-grid">
      <div class="growth-card">
        <h4>🤝 Squad Codes</h4><div class="desc">Invite 3 traders from your Discord or cohort. At 3, unlock an exclusive badge (demo).</div>
        <div class="code-box"><input type="text" id="squad_code" readonly><button class="btn btn-ghost" onclick="copySquadCode()">Copy</button></div>
        <div class="progress-label"><span>Invites tracked</span><span id="squad_progress_label">0 / 3</span></div>
        <div class="progress-track"><div class="progress-fill" id="squad_progress_fill"></div></div>
        <button class="btn btn-ghost" style="justify-content:center;" onclick="simulateInvite()">Simulate an invite joining (demo)</button>
      </div>
      <div class="growth-card">
        <h4>🫣 The Confession Wall</h4><div class="desc">Anonymous. Cathartic. Post your worst trading moment.</div>
        <div class="confession-form"><textarea id="confession_input" placeholder="e.g. Moved my stop 'just this once' on an NQ short..." maxlength="180"></textarea><button class="btn btn-primary" onclick="postConfession()">Post</button></div>
        <div class="confession-wall" id="confessionWall"></div>
      </div>
    </div>
  </section>
  `;
}
function initArenaPage(){
  ladderPrice=100; ladderStreak=0; ladderBest=0;
  signalSeq=[]; signalLevel=0; signalBest=0; signalInputIdx=0; signalLocked=true;
  simRunning=false; simPrice=100; simHistory=[100]; simPos='flat'; simPnl=0; simTimeLeft=300;
  document.getElementById('signal_msg').textContent = 'Level 0 — tap start to watch the sequence.';
  renderSimLeaderboard(); drawSimChart();
  document.getElementById('squad_code').value = 'DESK-' + Math.random().toString(36).slice(2,8).toUpperCase();
  squadInvites = 0; updateSquadProgress();
  confessions = confessions.length ? confessions : defaultConfessions.slice();
  renderConfessions();
}
let ladderPrice=100, ladderStreak=0, ladderBest=0;
const ladderWinMsgs = ["Clean read.", "You're either good or lucky.", "Streak's building — don't get cocky.", "Diamond hands, diamond eyes.", "The tape respects you."];
const ladderLoseMsgs = ["Streak's gone. Just like your Friday PnL.", "Rekt. Streak reset to zero.", "That's a stop-out. Try again.", "The market disagreed, loudly."];
function ladderGuess(dir){
  const change = (Math.random()*1.2 - 0.6);
  const newPrice = Math.max(1, ladderPrice + change);
  const actualDir = newPrice >= ladderPrice ? 'up' : 'down';
  const correct = dir === actualDir;
  ladderPrice = newPrice;
  document.getElementById('ladder_price').textContent = ladderPrice.toFixed(2);
  if(correct){
    ladderStreak++; if(ladderStreak>ladderBest) ladderBest=ladderStreak;
    document.getElementById('ladder_msg').textContent = ladderWinMsgs[Math.min(ladderStreak,ladderWinMsgs.length)-1] || ladderWinMsgs[ladderWinMsgs.length-1];
  } else {
    document.getElementById('ladder_msg').textContent = ladderLoseMsgs[Math.floor(Math.random()*ladderLoseMsgs.length)];
    ladderStreak = 0;
  }
  document.getElementById('ladder_streak').textContent = ladderStreak;
  document.getElementById('ladder_best').textContent = ladderBest;
}
const signalColors = ['green','red','doji','spike'];
let signalSeq=[], signalLevel=0, signalBest=0, signalInputIdx=0, signalLocked=true;
function startSignalGame(){ signalSeq=[]; signalLevel=0; signalInputIdx=0; document.getElementById('signal_level').textContent=0; nextSignalRound(); }
function nextSignalRound(){
  signalLevel++; signalInputIdx=0; signalSeq.push(signalColors[Math.floor(Math.random()*4)]);
  document.getElementById('signal_level').textContent = signalLevel;
  document.getElementById('signal_msg').textContent = `Level ${signalLevel} — watch closely...`;
  signalLocked = true; playSignalSequence();
}
function playSignalSequence(){
  let i=0; const btns = document.querySelectorAll('.candle-btn');
  function flashNext(){
    btns.forEach(b=>b.classList.remove('flash'));
    if(i>=signalSeq.length){ signalLocked=false; document.getElementById('signal_msg').textContent='Your turn — repeat the sequence.'; return; }
    const c = signalSeq[i]; const btn = [...btns].find(b=>b.dataset.c===c); btn.classList.add('flash'); i++;
    setTimeout(flashNext, 550);
  }
  setTimeout(flashNext, 500);
}
function signalInput(c){
  if(signalLocked) return;
  if(signalSeq[signalInputIdx]===c){
    signalInputIdx++;
    if(signalInputIdx===signalSeq.length){
      if(signalLevel>signalBest){ signalBest=signalLevel; document.getElementById('signal_best').textContent=signalBest; }
      document.getElementById('signal_msg').textContent = 'Correct — next level loading...';
      signalLocked=true; setTimeout(nextSignalRound, 700);
    }
  } else {
    document.getElementById('signal_msg').textContent = `Busted at level ${signalLevel}. Hit Start to run it back.`;
    signalLocked=true;
  }
}
let simRunning=false, simPrice=100, simHistory=[100], simPos='flat', simPnl=0, simTimeLeft=300, simInterval=null;
let simLeaderboard = [{name:'quietscalper', pnl:612},{name:'nq_or_nothing', pnl:340},{name:'vwap_believer', pnl:95},{name:'ripped_stops', pnl:-180}];
function startSim(){
  if(simRunning) return;
  simRunning=true; simPrice=100; simHistory=[100]; simPos='flat'; simPnl=0; simTimeLeft=300;
  document.getElementById('sim_pos').textContent='FLAT'; document.getElementById('sim_startbtn').textContent='Running...'; document.getElementById('sim_startbtn').disabled=true;
  document.getElementById('sim_msg').textContent=''; updateSimHud(); drawSimChart();
  simInterval = setInterval(simTick, 1000);
}
function simSetPosition(p){ if(!simRunning) return; simPos=p; document.getElementById('sim_pos').textContent=p.toUpperCase(); }
function simTick(){
  simTimeLeft--; const change=(Math.random()*1-0.5); const newPrice=Math.max(1,simPrice+change); const delta=newPrice-simPrice;
  if(simPos==='long') simPnl += delta*100; else if(simPos==='short') simPnl -= delta*100;
  simPrice=newPrice; simHistory.push(simPrice); if(simHistory.length>150) simHistory.shift();
  updateSimHud(); drawSimChart(); if(simTimeLeft<=0) endSim();
}
function updateSimHud(){
  const m=Math.floor(Math.max(0,simTimeLeft)/60), s=Math.max(0,simTimeLeft)%60;
  document.getElementById('sim_time').textContent = `${m}:${s.toString().padStart(2,'0')}`;
  document.getElementById('sim_price').textContent = simPrice.toFixed(2);
  const pnlEl = document.getElementById('sim_pnl');
  pnlEl.textContent = (simPnl>=0?'$':'-$')+Math.abs(simPnl).toFixed(0);
  pnlEl.style.color = simPnl>=0 ? 'var(--success)' : 'var(--danger)';
}
function drawSimChart(){
  const canvas = document.getElementById('sim_canvas'); if(!canvas) return;
  const ctx = canvas.getContext('2d'); canvas.width = canvas.clientWidth; canvas.height = 110;
  const w=canvas.width, h=canvas.height; ctx.clearRect(0,0,w,h);
  const min=Math.min(...simHistory), max=Math.max(...simHistory); const range=(max-min)||1;
  ctx.beginPath();
  simHistory.forEach((p,i)=>{ const x=(i/((simHistory.length-1)||1))*w; const y=h-((p-min)/range)*h*0.8-h*0.1; if(i===0) ctx.moveTo(x,y); else ctx.lineTo(x,y); });
  ctx.strokeStyle='#E8A33D'; ctx.lineWidth=2; ctx.stroke();
}
function gradeSim(pnl){
  if(pnl>800) return "Certified market wizard. Screenshot this before it mean-reverts.";
  if(pnl>200) return "Solid. You'd survive an eval — barely.";
  if(pnl>=0) return "Breakeven-ish. Very 'consistency rule compliant' of you.";
  if(pnl>-200) return "Small loss. Completely normal, definitely not a pattern.";
  return "Blown. At least it wasn't a real funded account. ...Right?";
}
function addToLeaderboard(pnl){ simLeaderboard.push({name:'You', pnl:Math.round(pnl), you:true}); simLeaderboard.sort((a,b)=>b.pnl-a.pnl); renderSimLeaderboard(); }
function renderSimLeaderboard(){
  const el = document.getElementById('sim_leaderboard'); if(!el) return;
  el.innerHTML = simLeaderboard.slice(0,6).map((e,i)=>`<div class="${e.you?'you':''}"><span>#${i+1} ${e.you?'You':esc(e.name)}</span><span>${e.pnl>=0?'$':'-$'}${Math.abs(e.pnl)}</span></div>`).join('');
}
function endSim(){
  clearInterval(simInterval); simRunning=false;
  document.getElementById('sim_startbtn').textContent='Run it back'; document.getElementById('sim_startbtn').disabled=false;
  document.getElementById('sim_msg').textContent = gradeSim(simPnl); addToLeaderboard(simPnl);
}
let squadInvites = 0;
function copySquadCode(){ const el = document.getElementById('squad_code'); navigator.clipboard?.writeText(el.value).catch(()=>{}); toast('Code copied'); }
function simulateInvite(){ if(squadInvites>=3) return; squadInvites++; updateSquadProgress(); if(squadInvites===3) toast('Squad tier unlocked (demo)'); }
function updateSquadProgress(){
  const fill = document.getElementById('squad_progress_fill'); if(!fill) return;
  fill.style.width = (squadInvites/3*100)+'%';
  document.getElementById('squad_progress_label').textContent = `${squadInvites} / 3`;
}
let confessions = [];
const defaultConfessions = [
  {text:"Moved my stop 'just this once' on an NQ short. You already know.", likes:14},
  {text:"Revenge-traded ES after a red day and turned -$200 into -$1,100.", likes:22},
  {text:"Closed a winning swing trade early because I got nervous about the weekend gap.", likes:9},
];
function renderConfessions(){
  const wall = document.getElementById('confessionWall'); if(!wall) return;
  wall.innerHTML = confessions.map((c,i)=>`<div class="confession">
    <div class="meta"><span>anon_trader_${(i*137+7)%9000}</span><button class="heart ${c.liked?'liked':''}" onclick="likeConfession(${i})">${c.liked?'♥':'♡'} ${c.likes}</button></div>
    ${esc(c.text)}
  </div>`).join('');
}
function likeConfession(i){ confessions[i].liked = !confessions[i].liked; confessions[i].likes += confessions[i].liked ? 1 : -1; renderConfessions(); }
function postConfession(){
  const input = document.getElementById('confession_input');
  const text = input.value.trim();
  if(!text) return;
  confessions.unshift({text, likes:0}); input.value=''; renderConfessions(); toast('Posted (demo, not saved)');
}

/* ============================================================
   PAGE: ABOUT
   ============================================================ */
function pageAbout(){
  return `
  <div class="wrap"><div class="crumbs"><a href="#/">Home</a> / <span>About</span></div></div>
  <section class="wrap" style="border-bottom:none; padding-top:24px;">
    <div class="section-head"><div><div class="num">About</div><h2>What PropFirmScam is, and isn't</h2><p>Read this before trusting any score on this site.</p></div></div>
    <div class="about-grid">
      <div class="about-card"><h4>What we do</h4><p>We compile publicly available information about prop trading firms — pricing, rules, disclosed leadership, Trustpilot ratings where present, and press coverage of major changes — into one place, and we link every claim to where it came from.</p></div>
      <div class="about-card"><h4>What we don't do</h4><p>We don't audit payout ledgers, verify bank statements, or have any regulatory authority. Composite scores are an editorial estimate, not a certification, credit rating, or financial advice. We don't fabricate coupon codes, reviews, or leadership names — where we couldn't independently confirm something, the page says so.</p></div>
      <div class="about-card"><h4>How the health score works</h4><p>Each firm's 0–100 score is distributed across five weighted signals: leadership transparency, public payout/Trustpilot signal, disclosed rule flexibility, years of operating history, and platform coverage. See the "Why this score?" note on any firm profile for the specific breakdown.</p></div>
      <div class="about-card"><h4>Verification labels</h4><p>${vpill('verified')} means we found an independent, citable source. ${vpill('unverified')} means we looked and couldn't confirm it. ${vpill('editorial')} means it's our compiled estimate from firm-stated information. ${vpill('user')} means it's a review or claim from a site visitor, not fact-checked by us.</p></div>
    </div>
    <div class="data-note" style="margin-top:24px;">This is a demo research build with a sample dataset current as of July 2026. Always confirm rules, pricing, and payout terms directly with the firm before paying for an evaluation.</div>
  </section>
  `;
}

/* ============================================================
   PAGE: RESEARCH ARTICLE
   ============================================================ */
function pageArticle(a){
  return `
  <div class="wrap"><div class="crumbs"><a href="#/">Home</a> / <span>Research</span> / <span>${esc(a.title)}</span></div></div>
  <section class="wrap" style="border-bottom:none; padding-top:24px;">
    <div class="eyebrow">${esc(a.eyebrow)}</div>
    <h1 style="font-size:clamp(28px,4.5vw,42px); max-width:760px; margin-bottom:24px;">${esc(a.title)}</h1>
    <div class="article-body">${a.body.map(p=>`<p>${esc(p)}</p>`).join('')}</div>
    <div style="margin-top:36px;"><a href="#/" class="btn btn-ghost">← Back to home</a></div>
  </section>
  `;
}

function pageNotFound(){
  return `<div class="wrap" style="padding:100px 24px; text-align:center;">
    <div class="eyebrow" style="justify-content:center;">404</div>
    <h1 style="margin-bottom:16px;">Page not found</h1>
    <p style="color:var(--text-dim); margin-bottom:24px;">That page doesn't exist in this build.</p>
    <a href="#/" class="btn btn-primary">Back to home</a>
  </div>`;
}
</script>
</body>
</html>
