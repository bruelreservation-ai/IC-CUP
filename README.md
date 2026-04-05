<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>IBERIA CUP</title>
<style>
* { margin:0; padding:0; box-sizing:border-box; }

body {
  background: #ffffff;
  color: #111111;
  font-family: system-ui, -apple-system, sans-serif;
  min-height: 100vh;
}

.wrap { max-width:520px; margin:0 auto; padding:14px 14px 40px; }

/* HEADER */
.header { text-align:center; padding:26px 0 16px; border-radius:12px; overflow:hidden; position:relative; border-bottom:2px solid #ddd; margin-bottom:18px; background:#111; }
.header-bg { position:absolute; inset:0; background-size:cover; background-position:center 40%; filter:brightness(0.32) saturate(0.7); z-index:0; }
.header > *:not(.header-bg) { position:relative; z-index:1; }
.header-logo { font-size:2.4rem; font-weight:900; letter-spacing:4px; color:#fff; text-shadow:0 2px 12px rgba(0,0,0,0.95); line-height:1; }
.header-logo span { color:#f0c040; }
.header-sub { font-size:0.72rem; letter-spacing:5px; color:rgba(255,255,255,0.88); margin-top:4px; text-shadow:0 1px 8px rgba(0,0,0,1); font-weight:600; text-transform:uppercase; }
.header-flags { font-size:1.4rem; margin-top:6px; letter-spacing:8px; }
.header-date { display:inline-block; margin-top:10px; background:rgba(0,0,0,0.55); border:1px solid rgba(240,192,64,0.5); border-radius:4px; padding:3px 16px; font-size:0.72rem; letter-spacing:3px; color:#f0c040; font-weight:700; }
.upload-hint { display:block; margin-top:8px; cursor:pointer; font-size:0.6rem; letter-spacing:3px; color:rgba(255,255,255,0.35); }

/* SECTION LABEL */
.section-label { font-size:0.75rem; font-weight:800; letter-spacing:5px; color:#888; margin-bottom:10px; display:flex; align-items:center; gap:10px; text-transform:uppercase; }
.section-label::before,.section-label::after { content:''; flex:1; height:1px; background:#ddd; }
.live-dot { width:7px; height:7px; border-radius:50%; background:#c0431a; animation:blink 1.1s infinite; display:inline-block; margin-right:5px; }
@keyframes blink { 0%,100%{opacity:1}50%{opacity:.2} }

/* GLOBAL BANNER */
.global-banner { display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-bottom:18px; }
.global-card { background:#f8f8f8; border:1px solid #ddd; border-radius:10px; padding:12px 14px; text-align:center; }
.global-name { font-size:1.1rem; font-weight:800; letter-spacing:2px; text-transform:uppercase; }
.global-pts { font-size:2.4rem; font-weight:900; line-height:1; }
.global-sub { font-size:0.6rem; color:#999; letter-spacing:2px; margin-top:2px; text-transform:uppercase; }

/* CATCH TABLE */
.catch-wrap { background:#fff; border:1px solid #ddd; border-radius:10px; overflow:hidden; margin-bottom:18px; }
.catch-tbl { width:100%; border-collapse:collapse; }
.catch-tbl th { font-size:0.62rem; letter-spacing:2px; font-weight:700; padding:7px 10px; background:#f5f5f5; border-bottom:1px solid #ddd; text-align:center; color:#888; text-transform:uppercase; }
.catch-tbl th:first-child { text-align:left; }
.catch-tbl td { padding:9px 10px; border-bottom:1px solid #f0f0f0; font-size:1.1rem; font-weight:700; text-align:center; color:#111; }
.catch-tbl td:first-child { font-size:0.82rem; font-weight:700; letter-spacing:1px; text-align:left; color:#333; text-transform:uppercase; }
.catch-tbl tr:last-child td { border-bottom:none; background:#f8f8f8; font-size:0.9rem; color:#888; }
.catch-tbl tr:last-child td:first-child { font-size:0.7rem; letter-spacing:2px; text-transform:uppercase; }

/* DAY NAV */
.day-nav { margin-bottom:16px; }
.day-nav-top { display:flex; align-items:center; justify-content:space-between; margin-bottom:8px; }
.day-label { font-size:1.4rem; font-weight:900; letter-spacing:3px; color:#111; text-transform:uppercase; }
.day-country { font-size:0.65rem; letter-spacing:4px; padding:3px 10px; border-radius:4px; font-weight:700; display:inline-block; margin-top:3px; text-transform:uppercase; }
.day-country.es { background:rgba(198,12,48,0.1); border:1px solid rgba(198,12,48,0.3); color:#c0102a; }
.day-country.pt { background:rgba(0,102,0,0.1); border:1px solid rgba(0,150,0,0.3); color:#207830; }
.day-dots { display:flex; gap:5px; flex-wrap:wrap; }
.day-dot { width:32px; height:32px; border-radius:6px; border:1px solid #ddd; background:#f8f8f8; cursor:pointer; font-size:0.85rem; font-weight:700; color:#aaa; display:flex; align-items:center; justify-content:center; transition:all .15s; }
.day-dot.es-dot { border-top:3px solid rgba(198,12,48,0.4); }
.day-dot.pt-dot { border-top:3px solid rgba(0,150,0,0.4); }
.day-dot.active.es-dot { border-color:#c0102a; color:#c0102a; background:rgba(198,12,48,0.08); }
.day-dot.active.pt-dot { border-color:#207830; color:#207830; background:rgba(0,150,0,0.08); }
.day-dot.has-data { color:#666; border-color:#bbb; }
.nav-arrows { display:flex; gap:6px; }
.nav-btn { width:36px; height:36px; border-radius:8px; border:1px solid #ddd; background:#f8f8f8; color:#666; cursor:pointer; font-size:1.1rem; display:flex; align-items:center; justify-content:center; }
.nav-btn:active { background:#eee; }

/* STANDINGS */
.standings { background:#fff; border:1px solid #ddd; border-radius:10px; overflow:hidden; margin-bottom:18px; }
.standings-head { display:grid; grid-template-columns:36px 1fr 70px 44px; padding:6px 12px; background:#f5f5f5; border-bottom:1px solid #ddd; font-size:0.6rem; letter-spacing:2px; color:#aaa; font-weight:700; text-transform:uppercase; }
.standings-row { display:grid; grid-template-columns:36px 1fr 70px 44px; align-items:center; padding:9px 12px; border-bottom:1px solid #f0f0f0; }
.standings-row:last-child { border-bottom:none; }
.standings-row.top { background:#fffdf0; }
.st-rank { font-size:1.3rem; font-weight:900; color:#ccc; }
.st-rank.r1 { color:#c8960a; }
.st-rank.r2 { color:#888; }
.st-name { font-size:1.1rem; font-weight:800; line-height:1; display:flex; align-items:center; gap:6px; text-transform:uppercase; }
.st-thumb { width:24px; height:24px; border-radius:5px; object-fit:cover; }
.st-breakdown { font-size:0.6rem; color:#aaa; letter-spacing:1px; margin-top:1px; }
.st-bar-wrap { height:5px; background:#eee; border-radius:3px; overflow:hidden; }
.st-bar { height:100%; border-radius:3px; }
.st-pts { font-size:1.7rem; font-weight:900; text-align:right; line-height:1; }

/* CARDS */
.cards { display:flex; flex-direction:column; gap:12px; margin-bottom:18px; }
.card { background:#fff; border:1px solid #ddd; border-radius:12px; overflow:hidden; position:relative; }
.card.leader { border-color:#c8960a; border-width:2px; }
.card-accent { height:4px; }
.card-head { display:flex; align-items:flex-start; gap:12px; padding:13px 13px 0; }
.avatar-upload { position:relative; cursor:pointer; flex-shrink:0; }
.avatar-upload input { display:none; }
.avatar-img { width:50px; height:50px; border-radius:9px; object-fit:cover; border:2px solid #ddd; display:block; }
.avatar-placeholder { width:50px; height:50px; border-radius:9px; display:flex; align-items:center; justify-content:center; font-size:1.5rem; border:2px dashed #ddd; background:#f8f8f8; }
.avatar-edit-hint { position:absolute; bottom:0; right:0; background:rgba(0,0,0,0.5); border-radius:3px; font-size:0.5rem; padding:1px 3px; color:#fff; }
.card-meta { flex:1; }
.card-name { font-size:1.5rem; font-weight:900; letter-spacing:2px; line-height:1; text-transform:uppercase; }
.card-number { font-size:0.6rem; letter-spacing:3px; color:#aaa; margin-top:1px; text-transform:uppercase; }
.card-score { text-align:right; flex-shrink:0; }
.card-pts { font-size:2.6rem; font-weight:900; line-height:1; }
.card-pts-label { font-size:0.56rem; letter-spacing:3px; color:#aaa; text-transform:uppercase; }
.leader-crown { position:absolute; top:9px; right:11px; font-size:1.1rem; animation:levitate 2s ease-in-out infinite; }
@keyframes levitate { 0%,100%{transform:translateY(0) rotate(-5deg)}50%{transform:translateY(-5px) rotate(5deg)} }

/* SPECIES TABLE */
.species-table { width:100%; border-collapse:collapse; margin-top:12px; }
.species-table th { font-size:0.6rem; letter-spacing:2px; color:#aaa; font-weight:700; padding:5px 6px; background:#f8f8f8; border-top:1px solid #eee; border-bottom:1px solid #eee; text-align:left; text-transform:uppercase; }
.species-table th:last-child,.species-table th:nth-child(3) { text-align:center; }
.species-table td { padding:9px 6px; border-bottom:1px solid #f0f0f0; vertical-align:middle; }
.species-table tr:last-child td { border-bottom:none; }
.sp-name { font-size:0.85rem; font-weight:700; letter-spacing:1px; color:#222; display:flex; align-items:center; gap:7px; text-transform:uppercase; }
.milestone-pill { background:rgba(200,150,10,.12); border:1px solid rgba(200,150,10,.35); color:#a07800; border-radius:20px; padding:1px 7px; font-size:0.58rem; font-weight:700; letter-spacing:1px; }
.size-wrap { display:flex; align-items:center; gap:4px; }
.size-inp { width:46px; background:#f5f5f5; border:1px solid #ddd; border-radius:6px; color:#111; font-size:1rem; font-weight:700; text-align:center; padding:4px 2px; outline:none; transition:border-color .2s; -moz-appearance:textfield; font-family:system-ui,-apple-system,sans-serif; }
.size-inp::-webkit-outer-spin-button,.size-inp::-webkit-inner-spin-button { -webkit-appearance:none; }
.size-inp::placeholder { color:#ccc; font-size:.7rem; font-weight:400; }
.size-inp:focus { border-color:#999; }
.size-unit { font-size:.6rem; color:#aaa; }
.crown-icon { font-size:.9rem; }
.ctr { display:flex; align-items:center; gap:4px; justify-content:center; }
.ctr-btn { width:26px; height:26px; border-radius:6px; border:1px solid #ddd; cursor:pointer; font-size:1rem; font-weight:700; display:flex; align-items:center; justify-content:center; transition:all .12s; background:#f5f5f5; color:#555; }
.ctr-btn:active { background:#e0e0e0; transform:scale(.88); }
.ctr-val { font-size:1.4rem; font-weight:900; min-width:22px; text-align:center; }
.pts-cell { text-align:center; }
.pts-pill { display:inline-block; font-size:0.9rem; font-weight:800; padding:2px 7px; border-radius:4px; min-width:32px; letter-spacing:1px; }
.pts-pill.on  { background:rgba(30,140,60,.1); color:#1a7a30; border:1px solid rgba(30,140,60,.3); }
.pts-pill.off { background:transparent; color:#ddd; border:1px solid #eee; }
@keyframes popIn { 0%{transform:scale(1)}40%{transform:scale(1.18)}70%{transform:scale(.95)}100%{transform:scale(1)} }
.pop { animation:popIn .35s ease; }

/* BONUS */
.bonus-panel { background:#fffdf0; border:1px solid #e8d880; border-radius:10px; padding:13px; margin-bottom:18px; }
.bonus-title { font-size:0.85rem; font-weight:800; letter-spacing:4px; color:#a07800; margin-bottom:10px; text-transform:uppercase; }
.bonus-row { display:flex; align-items:center; gap:8px; margin-bottom:8px; }
.bonus-row:last-child { margin-bottom:0; }
.bonus-name { font-size:0.95rem; font-weight:800; letter-spacing:1px; min-width:84px; text-transform:uppercase; }
.bonus-inp { flex:1; background:#fff; border:1px solid #e0d070; border-radius:6px; color:#333; font-family:system-ui,-apple-system,sans-serif; font-size:0.8rem; padding:6px 9px; outline:none; }
.bonus-inp::placeholder { color:#ccc; }
.bonus-btn { width:34px; height:34px; border-radius:6px; border:1px solid #e0d070; background:#fff; color:#bbb; cursor:pointer; font-size:1rem; display:flex; align-items:center; justify-content:center; transition:all .2s; flex-shrink:0; }
.bonus-btn.on { background:#fff8d0; border-color:#c8960a; color:#c8960a; }

/* RULES */
.rules-panel { background:#fff; border:1px solid #ddd; border-radius:10px; overflow:hidden; margin-bottom:18px; }
.rules-head { background:#f5f5f5; border-bottom:1px solid #ddd; padding:9px 13px; font-size:0.85rem; font-weight:800; letter-spacing:4px; color:#888; text-transform:uppercase; }
.rules-table { width:100%; border-collapse:collapse; }
.rules-table th { background:#f8f8f8; font-size:0.6rem; letter-spacing:3px; color:#aaa; font-weight:700; padding:6px 13px; text-align:left; border-bottom:1px solid #eee; text-transform:uppercase; }
.rules-table td { padding:9px 13px; font-size:0.8rem; color:#333; border-bottom:1px solid #f5f5f5; vertical-align:top; line-height:1.4; font-weight:500; }
.rules-table tr:last-child td { border-bottom:none; }
.rules-table td:first-child { font-size:1rem; width:34px; text-align:center; padding-right:4px; }
.rules-table td:last-child { font-size:1rem; font-weight:800; color:#1a7a30; white-space:nowrap; text-align:right; width:68px; }
.rule-note { display:block; font-size:0.66rem; color:#aaa; margin-top:2px; font-weight:400; }
.maille-badges { display:flex; gap:7px; padding:9px 13px; background:#f8f8f8; border-top:1px solid #eee; flex-wrap:wrap; }
.maille-badge { display:inline-flex; align-items:center; gap:4px; background:#fff; border:1px solid #ddd; border-radius:4px; padding:3px 9px; font-size:0.7rem; font-weight:700; letter-spacing:1px; color:#888; text-transform:uppercase; }
.maille-val { color:#a07800; font-size:0.95rem; font-weight:800; }

footer { text-align:center; font-size:0.56rem; letter-spacing:4px; color:#ccc; padding-bottom:10px; text-transform:uppercase; }
</style>
</head>
<body>
<div class="wrap">

<div class="header">
  <div class="header-bg" id="heroBg"></div>
  <div class="header-logo">IBERIA <span>CUP</span></div>
  <div class="header-sub">12 Jours · Espagne & Portugal</div>
  <div class="header-flags">🇪🇸 🇵🇹</div>
  <div class="header-date" id="dateBadge">📅 ...</div>
  <label class="upload-hint">📷 CHARGER PHOTO DE FOND<input type="file" id="heroUpload" accept="image/*" style="display:none"/></label>
</div>

<div class="section-label">🌍 Classement global — 12 jours</div>
<div class="global-banner" id="globalBanner"></div>

<div class="section-label">🐟 Tableau des captures</div>
<div id="catchTable"></div>

<div class="day-nav">
  <div class="day-nav-top">
    <div>
      <div class="day-label" id="dayLabel">Jour 1</div>
      <div class="day-country es" id="dayCountry">🇪🇸 Espagne</div>
    </div>
    <div class="nav-arrows">
      <button class="nav-btn" id="btnPrev">‹</button>
      <button class="nav-btn" id="btnNext">›</button>
    </div>
  </div>
  <div class="day-dots" id="dayDots"></div>
</div>

<div class="section-label"><span class="live-dot"></span>Standings du jour</div>
<div class="standings">
  <div class="standings-head"><div>RNK</div><div>ANGLER</div><div>PROGRESS</div><div style="text-align:right">PTS</div></div>
  <div id="standings"></div>
</div>

<div class="section-label">Scorecards</div>
<div class="cards" id="cards"></div>

<div class="bonus-panel">
  <div class="bonus-title">⭐ Wild Card & 📡 Live Scope</div>
  <div id="bonusGrid"></div>
</div>

<div class="section-label">Règlement officiel</div>
<div class="rules-panel">
  <div class="rules-head">📋 Tournament Rules</div>
  <table class="rules-table">
    <thead><tr><th></th><th>Règle</th><th style="text-align:right">Points</th></tr></thead>
    <tbody>
      <tr><td>🎸</td><td><b>Plus gros BASS maillé</b> (≥30cm)<span class="rule-note">Par jour · En cas d'égalité, le premier pris l'emporte</span></td><td>+1 PT</td></tr>
      <tr><td>🐟</td><td><b>Plus gros BROCHET maillé</b> (≥60cm)<span class="rule-note">Par jour · En cas d'égalité, le premier pris l'emporte</span></td><td>+1 PT</td></tr>
      <tr><td>📦</td><td><b>Atteindre 3 captures</b> d'une même espèce<span class="rule-note">Par jour · Une seule fois par espèce</span></td><td>+1 PT</td></tr>
      <tr><td>📊</td><td><b>Plus grand total</b> toutes espèces<span class="rule-note">Par jour · Bass ≥30cm · Brochet ≥60cm · Sandre ≥50cm</span></td><td>+1 PT</td></tr>
      <tr><td>⚡</td><td><b>SANDRE capturé</b> (au moins 1 maillé ≥50cm)<span class="rule-note">1 seul point par jour quelle que soit la quantité</span></td><td>+1 PT</td></tr>
      <tr><td>📡</td><td><b>Poisson pris au Live Scope</b><span class="rule-note">Validé par l'autre angler · 1 seul bonus par jour</span></td><td>+1 PT</td></tr>
      <tr><td>⭐</td><td><b>Action Insolite</b> validée par l'autre angler</td><td>+1 PT</td></tr>
    </tbody>
  </table>
  <div class="maille-badges">
    <div class="maille-badge">🎸 Bass <span class="maille-val">≥ 30 cm</span></div>
    <div class="maille-badge">🐟 Brochet <span class="maille-val">≥ 60 cm</span></div>
    <div class="maille-badge">⚡ Sandre <span class="maille-val">≥ 50 cm</span></div>
  </div>
</div>

<footer>Iberia Cup · Cast & Conquer · v4.0</footer>
</div>

<script>
const ANGLERS = [
  { id:0, name:'GUILLAUME', number:'#01', emoji:'🎣', hex:'#1a6a9a' },
  { id:1, name:'ANTOINE',   number:'#02', emoji:'🏆', hex:'#9a7000' },
];

const SPECIES = [
  { id:'bass',   label:'BASS',    emoji:'🎸', hasSize:true,  minSize:30 },
  { id:'pike',   label:'BROCHET', emoji:'🐟', hasSize:true,  minSize:60 },
  { id:'zander', label:'SANDRE',  emoji:'⚡', hasSize:true,  minSize:50 },
];

const TOTAL_DAYS = 12, ES_DAYS = 6;

function freshAngler(id) {
  return { id, counts:{bass:0,pike:0,zander:0}, sizes:{bass:'',pike:'',zander:''}, milestone3:{bass:false,pike:false,zander:false}, sizets:{bass:0,pike:0,zander:0}, bonus:false, bonusNote:'', livescope:false };
}
function freshDay() { return { anglers: ANGLERS.map(a=>freshAngler(a.id)) }; }
function fresh() { return { currentDay:0, days:Array.from({length:TOTAL_DAYS},()=>freshDay()), photos:[null,null] }; }

let S = fresh();
const save = () => { try { localStorage.setItem('iberiacup4', JSON.stringify(S)); } catch(e){} };
const load = () => { try { const d=localStorage.getItem('iberiacup4'); if(d) S=JSON.parse(d); } catch(e){} };
const getDay = () => S.days[S.currentDay];

function biggestSize(day, spId) {
  const min=SPECIES.find(s=>s.id===spId).minSize;
  let best={size:0,ts:Infinity,id:-1};
  day.anglers.forEach(a=>{
    const v=parseFloat(a.sizes[spId])||0;
    if(v<min||v===0) return;
    if(v>best.size||(v===best.size&&a.sizets[spId]<best.ts)) best={size:v,ts:a.sizets[spId],id:a.id};
  });
  return best.id;
}

function totalFish(a) { return Object.values(a.counts).reduce((s,v)=>s+v,0); }

function volumeLeader(day) {
  let max=0, winner=-1;
  day.anglers.forEach(a=>{ const t=totalFish(a); if(t>max){max=t;winner=a.id;} });
  return max>0?winner:-1;
}

function computeDayScores(day) {
  const bassBest=biggestSize(day,'bass'), pikeBest=biggestSize(day,'pike'), volWin=volumeLeader(day);
  return day.anglers.map(a=>{
    let pts=0; const bd=[];
    SPECIES.forEach(sp=>{ if(a.milestone3[sp.id]){pts+=1;bd.push('x3'+sp.emoji);} });
    if(a.id===bassBest){ pts+=1; bd.push('👑🎸'); }
    if(a.id===pikeBest){ pts+=1; bd.push('👑🐟'); }
    if(a.id===volWin)  { pts+=1; bd.push('📊'); }
    const zv=parseFloat(a.sizes.zander)||0;
    if(a.counts.zander>0&&zv>=50){ pts+=1; bd.push('⚡'); }
    if(a.livescope){ pts+=1; bd.push('📡'); }
    if(a.bonus)    { pts+=1; bd.push('⭐'); }
    return {id:a.id, pts, bd};
  });
}

function computeGlobalScores() {
  const totals=ANGLERS.map(a=>({id:a.id,pts:0}));
  S.days.forEach(day=>{ computeDayScores(day).forEach(s=>{ totals[s.id].pts+=s.pts; }); });
  return totals;
}

function computeGlobalCatches() {
  const totals=ANGLERS.map(a=>({id:a.id,counts:{bass:0,pike:0,zander:0}}));
  S.days.forEach(day=>{ day.anglers.forEach(a=>{ SPECIES.forEach(sp=>{ totals[a.id].counts[sp.id]+=a.counts[sp.id]; }); }); });
  return totals;
}

function dayHasData(di) {
  return S.days[di].anglers.some(a=>Object.values(a.counts).some(v=>v>0)||a.bonus||a.livescope);
}

function upCount(aid, spId, d) {
  const a=getDay().anglers[aid];
  a.counts[spId]=Math.max(0,a.counts[spId]+d);
  a.milestone3[spId]=a.counts[spId]>=3;
  save(); render();
  const el=document.getElementById('v'+aid+spId);
  if(el){el.classList.remove('pop');void el.offsetWidth;el.classList.add('pop');}
}

function upSize(aid, spId, val) {
  const a=getDay().anglers[aid];
  const prev=parseFloat(a.sizes[spId])||0, next=parseFloat(val)||0;
  a.sizes[spId]=val;
  if(next>prev) a.sizets[spId]=Date.now();
  save();
  const sp=SPECIES.find(s=>s.id===spId);
  const mailed=next>=sp.minSize&&next>0;
  const bc=val?(mailed?'#5a9a5a':'#c05050'):'#ddd';
  const inp=document.getElementById('sz'+aid+spId);
  if(inp) inp.style.borderColor=bc;
  const bB=biggestSize(getDay(),'bass'), pB=biggestSize(getDay(),'pike'), zB=biggestSize(getDay(),'zander');
  const winMap={bass:bB,pike:pB,zander:zB};
  const isWin=aid===winMap[spId]&&mailed;
  const cr=document.getElementById('cr'+aid+spId);
  if(cr) cr.textContent=isWin?'👑':'cm';
  renderStandings(); renderGlobal(); renderCatchTable();
}

function toggleBonus(aid)     { getDay().anglers[aid].bonus=!getDay().anglers[aid].bonus; save(); render(); }
function toggleLivescope(aid) { getDay().anglers[aid].livescope=!getDay().anglers[aid].livescope; save(); render(); }
function upBonusNote(aid,val) { getDay().anglers[aid].bonusNote=val; save(); }

function uploadPhoto(aid) {
  const inp=document.getElementById('photoInp'+aid), file=inp.files[0]; if(!file) return;
  const reader=new FileReader();
  reader.onload=function(ev){
    const canvas=document.createElement('canvas'), img=new Image();
    img.onload=function(){
      const size=120, scale=Math.min(size/img.width,size/img.height);
      canvas.width=img.width*scale; canvas.height=img.height*scale;
      canvas.getContext('2d').drawImage(img,0,0,canvas.width,canvas.height);
      S.photos[aid]=canvas.toDataURL('image/jpeg',0.8); save(); render();
    };
    img.src=ev.target.result;
  };
  reader.readAsDataURL(file);
}

function renderGlobal() {
  const global=computeGlobalScores(), sorted=[...global].sort((a,b)=>b.pts-a.pts);
  document.getElementById('globalBanner').innerHTML=sorted.map((s,i)=>{
    const cfg=ANGLERS[s.id], photo=S.photos[s.id];
    const thumb=photo?'<img src="'+photo+'" style="width:32px;height:32px;border-radius:7px;object-fit:cover;border:2px solid '+cfg.hex+'55;margin:0 auto 4px;display:block;"/>'
      :'<div style="font-size:1.4rem;margin-bottom:2px;">'+cfg.emoji+'</div>';
    return '<div class="global-card" style="border-color:'+(i===0&&s.pts>0?cfg.hex:'#ddd')+'">'
      +thumb
      +'<div class="global-name" style="color:'+cfg.hex+'">'+cfg.name+'</div>'
      +'<div class="global-pts" style="color:'+cfg.hex+'">'+s.pts+'</div>'
      +'<div class="global-sub">PTS CUMULÉS '+(i===0&&s.pts>0?'👑':'')+'</div>'
      +'</div>';
  }).join('');
}

function renderCatchTable() {
  const catches=computeGlobalCatches();
  const rows=SPECIES.map(sp=>{
    const vals=catches.map(c=>c.counts[sp.id]);
    const total=vals.reduce((s,v)=>s+v,0);
    return '<tr><td>'+sp.emoji+' '+sp.label+'</td>'
      +catches.map((c,i)=>'<td style="color:'+ANGLERS[i].hex+'">'+(c.counts[sp.id]||'—')+'</td>').join('')
      +'<td style="color:#999">'+(total||'—')+'</td></tr>';
  }).join('');
  const pTotals=catches.map(c=>Object.values(c.counts).reduce((s,v)=>s+v,0));
  const grand=pTotals.reduce((s,v)=>s+v,0);
  document.getElementById('catchTable').innerHTML=
    '<div class="catch-wrap"><table class="catch-tbl"><thead><tr>'
    +'<th>Espèce</th>'
    +ANGLERS.map(a=>'<th style="color:'+a.hex+'">'+a.name+'</th>').join('')
    +'<th>Total</th></tr></thead><tbody>'
    +rows
    +'<tr><td>Total</td>'
    +pTotals.map((t,i)=>'<td style="color:'+ANGLERS[i].hex+'">'+(t||'—')+'</td>').join('')
    +'<td>'+(grand||'—')+'</td></tr>'
    +'</tbody></table></div>';
}

function renderStandings() {
  const day=getDay(), scores=computeDayScores(day);
  const maxPts=Math.max(...scores.map(s=>s.pts),1);
  const sorted=[...scores].sort((a,b)=>b.pts-a.pts);
  document.getElementById('standings').innerHTML=sorted.map((s,i)=>{
    const cfg=ANGLERS[s.id], photo=S.photos[s.id];
    const thumb=photo?'<img class="st-thumb" src="'+photo+'" style="border:1.5px solid '+cfg.hex+'55;"/>'
      :'<span style="font-size:1rem;">'+cfg.emoji+'</span>';
    return '<div class="standings-row'+(i===0&&s.pts>0?' top':'')+'"><div class="st-rank '+(i===0?'r1':'r2')+'">'+(i===0?'🥇':'🥈')+'</div>'
      +'<div class="st-info"><div class="st-name" style="color:'+cfg.hex+'">'+thumb+cfg.name+'</div>'
      +'<div class="st-breakdown">'+(s.bd.join(' · ')||'—')+'</div></div>'
      +'<div class="st-bar-wrap"><div class="st-bar" style="width:'+Math.round(s.pts/maxPts*100)+'%;background:'+cfg.hex+'"></div></div>'
      +'<div class="st-pts" style="color:'+cfg.hex+'">'+s.pts+'</div></div>';
  }).join('');
}

function render() {
  const day=getDay(), scores=computeDayScores(day);
  const topPts=Math.max(...scores.map(s=>s.pts));
  const leadId=topPts>0?scores.find(s=>s.pts===topPts).id:-1;
  const isES=S.currentDay<ES_DAYS;

  document.getElementById('dateBadge').textContent='📅 '+new Date().toLocaleDateString('fr-FR',{weekday:'long',day:'numeric',month:'long',year:'numeric'}).toUpperCase();
  document.getElementById('dayLabel').textContent='Jour '+(S.currentDay+1);
  const dc=document.getElementById('dayCountry');
  dc.textContent=isES?'🇪🇸 Espagne':'🇵🇹 Portugal';
  dc.className='day-country '+(isES?'es':'pt');

  document.getElementById('dayDots').innerHTML=Array.from({length:TOTAL_DAYS},function(_,i){
    const es=i<ES_DAYS, active=i===S.currentDay, hd=dayHasData(i);
    return '<div class="day-dot '+(es?'es-dot':'pt-dot')+(active?' active':'')+(hd&&!active?' has-data':'')+'" onclick="goDay('+i+')">'+(i+1)+'</div>';
  }).join('');

  renderStandings(); renderGlobal(); renderCatchTable();

  const bassBest=biggestSize(day,'bass'), pikeBest=biggestSize(day,'pike'), zanderBest=biggestSize(day,'zander');
  const winMap={bass:bassBest,pike:pikeBest,zander:zanderBest};

  document.getElementById('cards').innerHTML=day.anglers.map(function(angler){
    const cfg=ANGLERS[angler.id], sc=scores[angler.id], photo=S.photos[angler.id];
    const isLead=angler.id===leadId&&sc.pts>0;
    const avatarHtml=photo
      ?'<label class="avatar-upload"><img class="avatar-img" src="'+photo+'" style="border-color:'+cfg.hex+'66"/><span class="avatar-edit-hint">✎</span><input type="file" id="photoInp'+angler.id+'" accept="image/*" onchange="uploadPhoto('+angler.id+')"/></label>'
      :'<label class="avatar-upload"><div class="avatar-placeholder" style="border-color:'+cfg.hex+'44">'+cfg.emoji+'</div><span class="avatar-edit-hint">📷</span><input type="file" id="photoInp'+angler.id+'" accept="image/*" onchange="uploadPhoto('+angler.id+')"/></label>';

    const spRows=SPECIES.map(function(sp){
      const count=angler.counts[sp.id], ms=angler.milestone3[sp.id];
      const sv=angler.sizes[sp.id], nv=parseFloat(sv)||0;
      const mailed=nv>=sp.minSize&&nv>0;
      const isWin=angler.id===winMap[sp.id]&&mailed;
      const bc=sv?(mailed?'#5a9a5a':'#c05050'):'#ddd';
      const sizeCell='<div class="size-wrap"><input type="number" inputmode="decimal" class="size-inp" id="sz'+angler.id+sp.id+'" placeholder="'+sp.minSize+'cm" value="'+sv+'" style="border-color:'+bc+'" oninput="upSize('+angler.id+',\''+sp.id+'\',this.value)"/><span id="cr'+angler.id+sp.id+'" class="'+(isWin?'crown-icon':'size-unit')+'">'+(isWin?'👑':'cm')+'</span></div>';
      let dpts=0;
      if(sp.id==='zander'){ const zv=parseFloat(angler.sizes.zander)||0; if(count>0&&zv>=50) dpts=1; }
      else if(ms) dpts=1;
      return '<tr><td><div class="sp-name"><span>'+sp.emoji+'</span>'+sp.label+(ms?'<span class="milestone-pill">x3 ✓</span>':'')+'</div></td>'
        +'<td>'+sizeCell+'</td>'
        +'<td><div class="ctr"><button class="ctr-btn minus" onclick="upCount('+angler.id+',\''+sp.id+'\',-1)">−</button><span class="ctr-val" id="v'+angler.id+sp.id+'" style="color:'+cfg.hex+'">'+count+'</span><button class="ctr-btn plus" onclick="upCount('+angler.id+',\''+sp.id+'\',1)">+</button></div></td>'
        +'<td class="pts-cell"><span class="pts-pill '+(dpts>0?'on':'off')+'">'+(dpts>0?'+'+dpts:'·')+'</span></td></tr>';
    }).join('');

    return '<div class="card'+(isLead?' leader':'')+'"><div class="card-accent" style="background:'+cfg.hex+'"></div>'
      +(isLead?'<div class="leader-crown">👑</div>':'')
      +'<div class="card-head">'+avatarHtml
      +'<div class="card-meta"><div class="card-name" style="color:'+cfg.hex+'">'+cfg.name+'</div>'
      +'<div class="card-number">Competitor '+cfg.number+'</div></div>'
      +'<div class="card-score"><div class="card-pts" style="color:'+cfg.hex+'">'+sc.pts+'</div>'
      +'<div class="card-pts-label">Points</div></div></div>'
      +'<table class="species-table"><thead><tr><th>Espèce</th><th>Taille</th><th style="text-align:center">Captures</th><th style="text-align:center">Pts</th></tr></thead>'
      +'<tbody>'+spRows+'</tbody></table></div>';
  }).join('');

  document.getElementById('bonusGrid').innerHTML=day.anglers.map(function(angler){
    const cfg=ANGLERS[angler.id];
    return '<div class="bonus-row"><div class="bonus-name" style="color:'+cfg.hex+'">'+cfg.name+'</div>'
      +'<input class="bonus-inp" type="text" placeholder="Action insolite…" value="'+angler.bonusNote+'" oninput="upBonusNote('+angler.id+',this.value)"/>'
      +'<button class="bonus-btn'+(angler.bonus?' on':'')+'" onclick="toggleBonus('+angler.id+')">⭐</button>'
      +'<button class="bonus-btn'+(angler.livescope?' on':'')+'" onclick="toggleLivescope('+angler.id+')">📡</button></div>';
  }).join('');
}

function goDay(i){ S.currentDay=i; save(); render(); }

load(); render();

document.getElementById('btnPrev').onclick=function(){ if(S.currentDay>0){S.currentDay--;save();render();} };
document.getElementById('btnNext').onclick=function(){ if(S.currentDay<TOTAL_DAYS-1){S.currentDay++;save();render();} };

document.getElementById('heroUpload').addEventListener('change',function(e){
  var file=e.target.files[0]; if(!file) return;
  var reader=new FileReader();
  reader.onload=function(ev){
    var canvas=document.createElement('canvas'), img=new Image();
    img.onload=function(){
      var maxW=900, scale=Math.min(1,maxW/img.width);
      canvas.width=img.width*scale; canvas.height=img.height*scale;
      canvas.getContext('2d').drawImage(img,0,0,canvas.width,canvas.height);
      var dataUrl=canvas.toDataURL('image/jpeg',0.72);
      document.getElementById('heroBg').style.backgroundImage='url('+dataUrl+')';
      try{ localStorage.setItem('iberiacup4_hero',dataUrl); } catch(e){}
    };
    img.src=ev.target.result;
  };
  reader.readAsDataURL(file);
});
var savedHero=localStorage.getItem('iberiacup4_hero');
if(savedHero) document.getElementById('heroBg').style.backgroundImage='url('+savedHero+')';
</script>
</body>
</html>
