<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
<title>SeniorShield | WA Guardian AI</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&family=Syne:wght@700;800&family=JetBrains+Mono:wght@300;400;600&display=swap" rel="stylesheet" />
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
/* ══════════════════════════════════════
   ROOT VARIABLES
══════════════════════════════════════ */
:root{
  --cyan:#00f2ff; --indigo:#4f46e5;
  --bg:#0b1120;   --card:#111827;  --surface:#1e293b;
  --text:#e2e8f0; --muted:rgba(226,232,240,0.5);
  --danger:#ff4d4d; --warn:#ffcc00; --ok:#00ff88;
  --radius:15px;
  --pad-x:60px;   /* desktop horizontal padding */
}
*{ margin:0; padding:0; box-sizing:border-box; }
html{ scroll-behavior:smooth; }
body{
  background:var(--bg); color:var(--text);
  overflow-x:hidden; font-family:'Poppins',sans-serif;
  -webkit-tap-highlight-color:transparent;
}
.hidden{ display:none !important; }
img,canvas,textarea,input,button{ max-width:100%; }

/* ══════════════════════════════════════
   SHARED HEADER
══════════════════════════════════════ */
.site-header{
  display:flex; justify-content:space-between; align-items:center;
  padding:16px var(--pad-x); background:#0f172a;
  border-bottom:1px solid rgba(0,242,255,0.12);
  position:sticky; top:0; z-index:200;
}
.logo{
  font-size:clamp(15px,4vw,20px); font-weight:800; color:var(--cyan);
  letter-spacing:2px; font-family:'Syne',sans-serif;
}
.nav-btn{
  background:none; border:1px solid var(--cyan); color:var(--cyan);
  padding:8px 20px; border-radius:20px; cursor:pointer;
  font-family:'Poppins',sans-serif; font-weight:600;
  font-size:14px; transition:.2s; white-space:nowrap;
  min-height:40px;
}
.nav-btn:hover{ background:var(--cyan); color:#0b1120; }

/* ══════════════════════════════════════
   HERO
══════════════════════════════════════ */
.hero{
  min-height:calc(100svh - 61px);
  display:flex; flex-direction:column;
  justify-content:center; align-items:center; text-align:center;
  background:radial-gradient(ellipse at center,#0f172a 0%,#020617 100%);
  animation:fadeIn 1.5s ease; padding:40px 24px;
}
.hero h1{
  font-size:clamp(26px,6vw,54px); margin-bottom:16px; font-weight:800;
  font-family:'Syne',sans-serif; line-height:1.2;
  background:linear-gradient(90deg,var(--cyan),var(--indigo));
  -webkit-background-clip:text; color:transparent;
}
.hero p{
  font-size:clamp(13px,3.5vw,17px); opacity:.6; margin-bottom:32px;
  font-family:'JetBrains Mono',monospace; padding:0 10px;
}
.hero-btn{
  padding:14px 36px; border:none; border-radius:30px;
  background:linear-gradient(90deg,var(--cyan),var(--indigo));
  font-weight:700; cursor:pointer; font-size:15px;
  font-family:'Poppins',sans-serif; transition:.2s;
  box-shadow:0 0 30px rgba(0,242,255,0.3); color:#0b1120;
  min-height:48px;
}
.hero-btn:hover{ transform:scale(1.04); }

/* ══════════════════════════════════════
   LOGIN PAGE
══════════════════════════════════════ */
#loginPage{
  display:flex; align-items:center; justify-content:center;
  min-height:100svh; background:var(--bg); padding:20px;
}
.login-box{
  background:var(--card); padding:clamp(24px,5vw,40px) clamp(20px,5vw,36px);
  border-radius:20px; width:100%; max-width:380px;
  box-shadow:0 0 40px rgba(0,242,255,0.15);
  border:1px solid rgba(0,242,255,0.1);
}
.login-title{
  text-align:center; margin-bottom:24px; font-weight:800; color:var(--cyan);
  font-family:'Syne',sans-serif; font-size:clamp(17px,4vw,20px); letter-spacing:1px;
}

/* TABS */
.tab-bar{ display:flex; gap:8px; margin-bottom:24px; }
.tab-btn{
  flex:1; padding:11px 8px; border:1px solid rgba(0,242,255,0.3);
  background:transparent; color:var(--cyan); border-radius:10px;
  cursor:pointer; font-family:'Poppins',sans-serif;
  font-weight:600; font-size:clamp(12px,3.5vw,14px); transition:.2s;
  min-height:44px;
}
.tab-btn.active{ background:var(--cyan); color:#0b1120; border-color:var(--cyan); }

/* INPUTS */
.field{
  width:100%; padding:13px 14px; margin:8px 0;
  border:1px solid var(--surface); border-radius:10px;
  background:var(--surface); color:var(--text);
  font-family:'Poppins',sans-serif; font-size:15px;
  outline:none; transition:.2s; min-height:48px;
}
.field:focus{ border-color:var(--cyan); }
.btn-login{
  width:100%; background:linear-gradient(90deg,var(--cyan),var(--indigo));
  border:none; padding:14px 20px; border-radius:12px; margin-top:12px;
  cursor:pointer; font-family:'Poppins',sans-serif; font-weight:700;
  font-size:15px; transition:.2s; color:#0b1120; min-height:50px;
}
.btn-login:hover{ opacity:.88; transform:scale(1.02); }
.btn-login:active{ transform:scale(0.98); }

/* ══════════════════════════════════════
   NFC UI
══════════════════════════════════════ */
.nfc-wrapper{ text-align:center; padding:10px 0; }
.nfc-badge{
  display:inline-block; padding:6px 14px; border-radius:20px;
  font-family:'JetBrains Mono',monospace; font-size:12px; font-weight:600;
  margin-bottom:20px; background:var(--surface); color:var(--muted);
  border:1px solid var(--surface); transition:.4s;
}
.nfc-badge.scanning{ background:rgba(0,242,255,0.1); color:var(--cyan); border-color:var(--cyan); }
.nfc-badge.success { background:rgba(0,255,136,0.1); color:var(--ok);   border-color:var(--ok);   }
.nfc-badge.error   { background:rgba(255,77,77,0.1);  color:var(--danger);border-color:var(--danger);}

.nfc-rings{ position:relative; width:120px; height:120px; margin:0 auto 22px; }
.nfc-ring { position:absolute; border-radius:50%; border:2px solid transparent; }
.nfc-ring:nth-child(1){ width:120px;height:120px;top:0;left:0;border-color:rgba(0,242,255,0.15);}
.nfc-ring:nth-child(2){ width:88px;height:88px;top:16px;left:16px;border-color:rgba(0,242,255,0.25);}
.nfc-ring:nth-child(3){ width:56px;height:56px;top:32px;left:32px;border-color:rgba(0,242,255,0.4);}
.nfc-icon{ position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);font-size:26px; }
.nfc-rings.scanning .nfc-ring{ animation:ringPulse 1.6s ease-in-out infinite; }
.nfc-rings.scanning .nfc-ring:nth-child(2){ animation-delay:.2s; }
.nfc-rings.scanning .nfc-ring:nth-child(3){ animation-delay:.4s; }
.nfc-rings.success .nfc-ring{ border-color:var(--ok)!important;    opacity:.5; }
.nfc-rings.error   .nfc-ring{ border-color:var(--danger)!important; opacity:.5; }
@keyframes ringPulse{0%,100%{transform:scale(1);opacity:.3;}50%{transform:scale(1.1);opacity:1;}}

.nfc-uid{
  background:var(--surface); border-radius:10px; padding:10px 14px;
  font-family:'JetBrains Mono',monospace; font-size:12px; color:var(--muted);
  margin:12px 0; min-height:36px; word-break:break-all; text-align:center;
  border:1px solid rgba(255,255,255,0.05); transition:.3s;
}
.nfc-uid.found{ color:var(--cyan); border-color:rgba(0,242,255,0.3); }
.nfc-info{
  font-size:11px; color:var(--muted); font-family:'JetBrains Mono',monospace;
  margin-bottom:14px; line-height:1.7;
}
.nfc-info a{ color:var(--cyan); text-decoration:none; }
.btn-nfc{
  background:var(--surface); border:1px solid var(--cyan); color:var(--cyan);
  padding:11px 24px; border-radius:12px; cursor:pointer;
  font-family:'Poppins',sans-serif; font-weight:600; font-size:14px;
  transition:.2s; min-height:46px; width:100%;
}
.btn-nfc:hover{ background:rgba(0,242,255,0.08); }
.btn-nfc:disabled{ opacity:.4; cursor:not-allowed; }

/* ══════════════════════════════════════
   DASHBOARD HEADER
══════════════════════════════════════ */
#dashboard{ animation:fadeIn .5s ease; }
.dash-header{
  display:flex; justify-content:space-between; align-items:center;
  padding:16px var(--pad-x); background:#111827;
  border-bottom:1px solid rgba(0,242,255,0.1);
  position:sticky; top:0; z-index:200; gap:12px;
}
.dash-logo{
  font-weight:700; color:var(--cyan); font-family:'Syne',sans-serif;
  letter-spacing:1px; font-size:clamp(13px,3.5vw,18px); line-height:1.3;
}
.dash-logout{
  background:none; border:1px solid var(--cyan); color:var(--cyan);
  padding:8px 18px; border-radius:20px; cursor:pointer;
  font-family:'Poppins',sans-serif; font-weight:600;
  font-size:13px; transition:.2s; white-space:nowrap; min-height:40px;
}
.dash-logout:hover{ background:var(--cyan); color:#0b1120; }

/* CONTAINER */
.container{ padding:28px var(--pad-x); }

/* STAT PILLS */
.stats-strip{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:14px; margin-bottom:24px;
}
.stat-pill{
  background:#141b2d; border-radius:14px; padding:18px 12px;
  text-align:center; box-shadow:0 0 16px rgba(0,242,255,0.07);
}
.stat-pill .num{ font-size:clamp(24px,5vw,32px); font-weight:700; font-family:'Syne',sans-serif; }
.stat-pill .lbl{ font-size:clamp(10px,2.5vw,12px); opacity:.55; font-family:'Poppins',sans-serif; margin-top:4px; }
.stat-pill.high .num{ color:var(--danger); }
.stat-pill.med  .num{ color:var(--warn);   }
.stat-pill.low  .num{ color:var(--ok);     }

/* WA CARDS */
.wa-card{
  background:#141b2d; padding:clamp(18px,4vw,30px);
  border-radius:var(--radius); margin-bottom:24px;
  box-shadow:0 0 20px rgba(0,242,255,0.08);
}
.wa-card h2{
  margin-bottom:16px; color:var(--cyan);
  font-family:'Poppins',sans-serif;
  font-size:clamp(14px,4vw,18px); font-weight:600;
}
.wa-card textarea{
  width:100%; height:clamp(100px,20vw,130px);
  padding:14px; border-radius:10px;
  border:1px solid transparent; background:#0f1626;
  color:white; font-family:'Poppins',sans-serif;
  font-size:clamp(13px,3.5vw,15px); resize:vertical;
  outline:none; transition:.2s;
}
.wa-card textarea:focus{ border-color:rgba(0,242,255,0.35); }

.btn-scan{
  margin-top:14px; padding:13px 28px;
  background:var(--cyan); border:none; border-radius:30px;
  font-weight:600; cursor:pointer; font-family:'Poppins',sans-serif;
  font-size:14px; color:#0b1120; transition:.2s;
  min-height:48px; width:100%;
}
.btn-scan:hover{ box-shadow:0 0 18px var(--cyan); }
.btn-scan:active{ transform:scale(0.98); }

.result-box{
  margin-top:16px; font-weight:600;
  font-size:clamp(13px,3.8vw,17px); font-family:'Poppins',sans-serif;
  line-height:1.5;
}
.risk-high{ color:var(--danger); }
.risk-medium{ color:var(--warn); }
.risk-low{ color:var(--ok); }

.scan-bar{
  height:5px; margin-top:12px; border-radius:4px;
  overflow:hidden; background:var(--surface);
}
.scan-bar-inner{
  height:100%; width:0; border-radius:4px;
  background:linear-gradient(90deg,var(--cyan),var(--indigo));
  transition:width .5s ease;
}

.wa-log{
  font-size:clamp(11px,3vw,13px); line-height:1.9;
  max-height:180px; overflow-y:auto;
  background:#0f1626; padding:14px; border-radius:10px;
  font-family:'JetBrains Mono',monospace;
  word-break:break-word;
}
.wa-card canvas{ background:#0f1626; border-radius:10px; padding:10px; width:100%!important; }

/* ══════════════════════════════════════
   ANIMATIONS
══════════════════════════════════════ */
@keyframes fadeIn{ from{opacity:0;transform:translateY(8px);}to{opacity:1;transform:translateY(0);} }

/* ══════════════════════════════════════
   TABLET  ≤ 768px
══════════════════════════════════════ */
@media(max-width:768px){
  :root{ --pad-x:20px; }

  .site-header{ padding:14px var(--pad-x); }
  .dash-header { padding:14px var(--pad-x); }
  .container   { padding:20px var(--pad-x); }

  .hero{ padding:32px 20px; }
  .hero p{ font-size:13px; }

  .login-box{ padding:28px 20px; }

  .stats-strip{ gap:10px; }
  .stat-pill{ padding:14px 8px; border-radius:12px; }

  .wa-card{ padding:20px; border-radius:12px; }

  .dash-logo{ font-size:13px; letter-spacing:.5px; }
}

/* ══════════════════════════════════════
   MOBILE  ≤ 480px
══════════════════════════════════════ */
@media(max-width:480px){
  :root{ --pad-x:16px; }

  /* header: stack logo & button nicely */
  .site-header{ flex-wrap:wrap; gap:8px; }
  .dash-header{ flex-wrap:nowrap; gap:8px; }
  .dash-logo  { font-size:12px; letter-spacing:0; }
  .dash-logout{ padding:7px 12px; font-size:12px; }

  /* hero */
  .hero{ padding:28px 16px; min-height:100svh; }
  .hero-btn{ padding:13px 28px; font-size:14px; }

  /* login */
  #loginPage{ padding:16px; align-items:flex-start; padding-top:60px; }
  .login-box{ border-radius:16px; }
  .login-title{ font-size:18px; }
  .tab-btn{ font-size:12px; padding:10px 4px; }

  /* stats — 3 cols still but tighter */
  .stats-strip{ grid-template-columns:repeat(3,1fr); gap:8px; }
  .stat-pill .num{ font-size:22px; }
  .stat-pill .lbl{ font-size:9px; }

  /* cards */
  .wa-card{ padding:16px; margin-bottom:16px; }
  .wa-card h2{ font-size:14px; margin-bottom:12px; }
  .wa-card textarea{ font-size:13px; height:100px; }

  /* scan button full-width */
  .btn-scan{ font-size:14px; padding:13px 16px; }

  /* log */
  .wa-log{ font-size:11px; max-height:150px; }

  /* nfc */
  .nfc-rings{ width:100px; height:100px; }
  .nfc-ring:nth-child(1){width:100px;height:100px;}
  .nfc-ring:nth-child(2){width:74px;height:74px;top:13px;left:13px;}
  .nfc-ring:nth-child(3){width:48px;height:48px;top:26px;left:26px;}
  .nfc-icon{ font-size:22px; }
}

/* ══════════════════════════════════════
   WIDE DESKTOP  ≥ 1400px
══════════════════════════════════════ */
@media(min-width:1400px){
  :root{ --pad-x:100px; }
  .stats-strip{ grid-template-columns:repeat(3,minmax(0,240px)); justify-content:start; }
}
</style>
</head>
<body>

<!-- ══════ HOME ══════ -->
<section id="homePage">
  <header class="site-header">
    <div class="logo">SENIORSHIELD</div>
    <button class="nav-btn" onclick="showLogin()">Login</button>
  </header>
  <div class="hero">
    <h1>Protecting Elderly from Digital Attacks</h1>
    <p>AI-powered WhatsApp Hack Detection System</p>
    <button class="hero-btn" onclick="showLogin()">Access Dashboard</button>
  </div>
</section>

<!-- ══════ LOGIN ══════ -->
<section id="loginPage" class="hidden">
  <div class="login-box">
    <div class="login-title">SENIORSHIELD</div>

    <div class="tab-bar">
      <button class="tab-btn active" onclick="showTab('tabPassword',this)">🔑 Password</button>
      <button class="tab-btn"        onclick="showTab('tabNFC',this)"     >📡 NFC</button>
    </div>

    <!-- PASSWORD TAB -->
    <div id="tabPassword">
      <input class="field" type="text"     id="user" placeholder="Username"    autocomplete="username"  />
      <input class="field" type="password" id="pass" placeholder="Password"    autocomplete="current-password" />
      <button class="btn-login" onclick="login()">Login</button>
    </div>

    <!-- NFC TAB -->
    <div id="tabNFC" class="hidden">
      <div class="nfc-wrapper">
        <div id="nfcBadge" class="nfc-badge">● SIAP</div>
        <div id="nfcRings" class="nfc-rings">
          <div class="nfc-ring"></div>
          <div class="nfc-ring"></div>
          <div class="nfc-ring"></div>
          <span class="nfc-icon">📡</span>
        </div>
        <div id="nfcUID" class="nfc-uid">UID akan tampil di sini...</div>
        <p class="nfc-info">
          Gunakan Chrome Android &amp; aktifkan NFC.<br/>
          <a href="https://support.google.com/android/answer/9075925" target="_blank">Cara aktifkan NFC ›</a>
        </p>
        <button id="nfcScanBtn" class="btn-nfc" onclick="startNFCScan()">Mulai Scan NFC</button>
        <div id="nfcHint" style="margin-top:10px;font-size:11px;color:var(--muted);font-family:'JetBrains Mono',monospace;"></div>
      </div>
    </div>
  </div>
</section>

<!-- ══════ DASHBOARD ══════ -->
<section id="dashboard" class="hidden">

  <div class="dash-header">
    <div class="dash-logo">🛡 WA GUARDIAN AI — SENIORSHIELD</div>
    <button class="dash-logout" onclick="logout()">Logout</button>
  </div>

  <div class="container">

    <!-- STAT PILLS -->
    <div class="stats-strip">
      <div class="stat-pill high">
        <div class="num" id="statHigh">0</div>
        <div class="lbl">⚠ High Risk</div>
      </div>
      <div class="stat-pill med">
        <div class="num" id="statMed">0</div>
        <div class="lbl">⚡ Medium</div>
      </div>
      <div class="stat-pill low">
        <div class="num" id="statLow">0</div>
        <div class="lbl">✓ Low Risk</div>
      </div>
    </div>

    <!-- SCAN CARD -->
    <div class="wa-card">
      <h2>📩 Scan SMS / WhatsApp Text</h2>
      <textarea id="inputText" placeholder="Tempel pesan mencurigakan di sini..."></textarea>
      <button class="btn-scan" onclick="scanText()">🔍 Scan Sekarang</button>
      <div class="scan-bar"><div id="scanBar" class="scan-bar-inner"></div></div>
      <div id="resultBox" class="result-box"></div>
    </div>

    <!-- CHART CARD -->
    <div class="wa-card">
      <h2>📊 Statistik Deteksi</h2>
      <canvas id="attackChart"></canvas>
    </div>

    <!-- LOG CARD -->
    <div class="wa-card">
      <h2>📋 Log Aktivitas</h2>
      <div class="wa-log" id="logBox">Menunggu scan pertama...<br/></div>
    </div>

  </div>
</section>

<!-- ══════ SCRIPT ══════ -->
<script>
/* ── DATABASE NFC ── */
const NFC_DATABASE = [
  { uid:"04:a3:b2:c1", name:"Admin Utama"    },
  { uid:"04:12:34:56", name:"Staff Senior 1"  },
  { uid:"04:ab:cd:ef", name:"Staff Senior 2"  },
];

/* ── DATABASE USER ── */
const USER_DATABASE = [
  { username:"admin",        password:"1234",             name:"Admin"        },
  { username:"seniorshield", password:"sahabatselamanya", name:"SeniorShield" },
];

/* ── KEYWORD & DOMAIN DATABASE ── */
const phishingKeywords = [
  "hadiah","klik link","verifikasi akun","akun diblokir",
  "transfer sekarang","menang undian","gratis saldo",
  "bank","pin","otp","kode verifikasi","whatsapp support",
  "login dari perangkat baru","reset password","data anda",
  "segera","urgent","konfirmasi","perangkat baru","terkena hack",
  "kode rahasia","jangan beritahu","transfer dana","rekening"
];
const suspiciousDomains = [".xyz",".top",".click",".gq",".ru",".tk",".cf",".ml",".ga"];

/* ── NAVIGASI ── */
function showLogin(){
  document.getElementById("homePage").classList.add("hidden");
  document.getElementById("loginPage").classList.remove("hidden");
}
function showDashboard(){
  document.getElementById("loginPage").classList.add("hidden");
  document.getElementById("dashboard").classList.remove("hidden");
  loadLogs();
}
function showTab(tabId, btn){
  document.querySelectorAll(".tab-btn").forEach(b => b.classList.remove("active"));
  document.getElementById("tabPassword").classList.add("hidden");
  document.getElementById("tabNFC").classList.add("hidden");
  document.getElementById(tabId).classList.remove("hidden");
  btn.classList.add("active");
}
function logout(){ location.reload(); }

/* ── LOGIN ── */
function login(){
  const u = document.getElementById("user").value.trim();
  const p = document.getElementById("pass").value;
  const match = USER_DATABASE.find(x => x.username===u && x.password===p);
  if(match){ showDashboard(); }
  else{ alert("Username atau password salah."); }
}

// Enter key support
document.addEventListener("DOMContentLoaded",()=>{
  ["user","pass"].forEach(id=>{
    document.getElementById(id).addEventListener("keydown", e=>{
      if(e.key==="Enter") login();
    });
  });
});

/* ── NFC LOGIN ── */
let nfcAbortCtrl = null;
async function startNFCScan(){
  const btn   = document.getElementById("nfcScanBtn");
  const badge = document.getElementById("nfcBadge");
  const uid   = document.getElementById("nfcUID");
  const hint  = document.getElementById("nfcHint");

  if(!("NDEFReader" in window)){
    setNFCState("error");
    badge.textContent = "● NFC Tidak Didukung";
    uid.textContent   = "Gunakan Chrome 89+ di Android dengan NFC aktif.";
    return;
  }
  try{
    btn.disabled=true; btn.textContent="Scanning...";
    setNFCState("scanning");
    badge.textContent = "● SCANNING...";
    uid.textContent   = "Menunggu kartu NFC ditempelkan...";
    uid.classList.remove("found");
    hint.textContent  = "Tempelkan kartu NFC ke belakang ponsel Anda";

    nfcAbortCtrl = new AbortController();
    const reader = new NDEFReader();
    await reader.scan({ signal:nfcAbortCtrl.signal });
    reader.addEventListener("reading",({serialNumber})=> handleNFCRead(serialNumber));
    reader.addEventListener("readingerror",()=>{
      setNFCState("error"); badge.textContent="● Error Membaca";
      uid.textContent="Gagal membaca. Coba lagi."; resetNFCBtn();
    });
  }catch(err){
    if(err.name==="NotAllowedError"){ badge.textContent="● Izin Ditolak"; uid.textContent="Aktifkan izin NFC di browser."; }
    else if(err.name==="AbortError"){ badge.textContent="● Dibatalkan";   uid.textContent="Scan dibatalkan."; }
    else{ badge.textContent="● Error"; uid.textContent=err.message; }
    setNFCState("error"); hint.textContent=""; resetNFCBtn();
  }
}
function handleNFCRead(rawUID){
  const badge=document.getElementById("nfcBadge");
  const uid  =document.getElementById("nfcUID");
  const hint =document.getElementById("nfcHint");
  uid.textContent="UID: "+rawUID.toUpperCase();
  uid.classList.add("found");
  const match=NFC_DATABASE.find(e=>e.uid.toLowerCase()===rawUID.toLowerCase());
  if(match){
    setNFCState("success"); badge.textContent="✓ TERVERIFIKASI";
    hint.textContent="Selamat datang, "+match.name+"!";
    if(nfcAbortCtrl) nfcAbortCtrl.abort();
    setTimeout(()=>showDashboard(),1200);
  }else{
    setNFCState("error"); badge.textContent="✗ TIDAK DIKENAL";
    hint.textContent="Kartu tidak terdaftar di sistem.";
    if(nfcAbortCtrl) nfcAbortCtrl.abort();
    resetNFCBtn(2800);
  }
}
function setNFCState(s){
  document.getElementById("nfcRings").className="nfc-rings"+(s?" "+s:"");
  document.getElementById("nfcBadge").className="nfc-badge" +(s?" "+s:"");
}
function resetNFCBtn(d=0){
  setTimeout(()=>{
    const b=document.getElementById("nfcScanBtn");
    if(b){ b.disabled=false; b.textContent="Mulai Scan NFC"; }
  },d);
}

/* ── CHART ── */
let highCount=0, mediumCount=0, lowCount=0;
const attackChart = new Chart(
  document.getElementById("attackChart").getContext("2d"),{
  type:"bar",
  data:{
    labels:["High Risk","Medium Risk","Low Risk"],
    datasets:[{
      label:"Jumlah Deteksi",
      data:[0,0,0],
      backgroundColor:["rgba(255,77,77,.75)","rgba(255,204,0,.75)","rgba(0,255,136,.75)"],
      borderColor:["#ff4d4d","#ffcc00","#00ff88"],
      borderWidth:1, borderRadius:6
    }]
  },
  options:{
    responsive:true,
    maintainAspectRatio:true,
    plugins:{ legend:{ labels:{ color:"white", font:{family:"Poppins",size:12} } } },
    scales:{
      x:{ ticks:{color:"white",font:{size:11}}, grid:{color:"rgba(255,255,255,0.04)"} },
      y:{ ticks:{color:"white",font:{size:11}}, grid:{color:"rgba(255,255,255,0.04)"}, beginAtZero:true }
    }
  }
});

/* ── SCAN TEXT ── */
function scanText(){
  const text=document.getElementById("inputText").value.toLowerCase();
  let score=0;
  phishingKeywords.forEach(kw=>{ if(text.includes(kw)) score+=15; });
  suspiciousDomains.forEach(d =>{ if(text.includes(d))  score+=25; });
  if(text.match(/https?:\/\//))                     score+=20;
  if(text.match(/\d{4,6}/) && text.includes("otp")) score+=30;
  else if(text.match(/\d{4,6}/))                    score+=10;

  const bar=document.getElementById("scanBar");
  bar.style.width="0";
  setTimeout(()=>{ bar.style.width=Math.min(score,100)+"%"; },50);

  let status,cls;
  if(score>=60){
    status="HIGH RISK — Kemungkinan Phishing / Hack WA!"; cls="result-box risk-high";
    highCount++; notifyUser("⚠️ HIGH RISK terdeteksi!");
  }else if(score>=30){
    status="MEDIUM RISK — Perlu waspada."; cls="result-box risk-medium"; mediumCount++;
  }else{
    status="LOW RISK — Pesan aman."; cls="result-box risk-low"; lowCount++;
  }

  const rb=document.getElementById("resultBox");
  rb.className=cls;
  rb.innerHTML="Skor Risiko: <strong>"+score+"</strong> → "+status;
  updateChart(); addLog(status); saveLog(status);
}

/* ── CHART UPDATE ── */
function updateChart(){
  attackChart.data.datasets[0].data=[highCount,mediumCount,lowCount];
  attackChart.update();
  document.getElementById("statHigh").textContent=highCount;
  document.getElementById("statMed" ).textContent=mediumCount;
  document.getElementById("statLow" ).textContent=lowCount;
}

/* ── LOG SYSTEM ── */
function addLog(msg){
  const time  =new Date().toLocaleTimeString();
  const logBox=document.getElementById("logBox");
  const color =msg.includes("HIGH")?"#ff4d4d":msg.includes("MEDIUM")?"#ffcc00":"#00ff88";
  logBox.innerHTML+=`<span style="color:${color}">[${time}] ${msg}</span><br/>`;
  logBox.scrollTop=logBox.scrollHeight;
}
function saveLog(msg){
  try{
    const logs=JSON.parse(localStorage.getItem("ss_logs"))||[];
    logs.push({time:new Date().toLocaleTimeString(),msg});
    if(logs.length>100) logs.shift();
    localStorage.setItem("ss_logs",JSON.stringify(logs));
  }catch(e){}
}
function loadLogs(){
  try{
    const logs=JSON.parse(localStorage.getItem("ss_logs"))||[];
    if(!logs.length) return;
    document.getElementById("logBox").innerHTML="";
    logs.forEach(l=>addLog(l.msg));
  }catch(e){}
}

/* ── NOTIFICATION ── */
function notifyUser(msg){
  if(Notification.permission!=="granted"){ Notification.requestPermission(); }
  else{ new Notification("SeniorShield Alert",{body:msg}); }
}
</script>
</body>
</html>
