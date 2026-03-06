<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>SeniorShield | WA Guardian AI</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&family=Syne:wght@700;800&family=JetBrains+Mono:wght@300;400;600&display=swap" rel="stylesheet"/>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
/* ══════════════════════════════════════════════════
   TOKENS
══════════════════════════════════════════════════ */
:root{
  --cyan:#00f2ff; --indigo:#4f46e5;
  --bg:#0b1120;   --card:#111827;  --deep:#0d1525; --surface:#1e293b;
  --text:#e2e8f0; --muted:rgba(226,232,240,0.45);
  --danger:#ff4d4d; --warn:#ffcc00; --ok:#00ff88;
  --r:14px;

  /* spacing tokens — override at breakpoints */
  --px:16px;   /* horizontal page padding  */
  --gap:12px;  /* card gap                  */
}
@media(min-width:600px){ :root{ --px:28px; --gap:16px; } }
@media(min-width:900px){ :root{ --px:52px; --gap:20px; } }
@media(min-width:1280px){ :root{ --px:88px; } }

/* ══════════════════════════════════════════════════
   BASE
══════════════════════════════════════════════════ */
*{ margin:0; padding:0; box-sizing:border-box; }
html{ scroll-behavior:smooth; }
body{
  background:var(--bg); color:var(--text); font-family:'Poppins',sans-serif;
  overflow-x:hidden; -webkit-tap-highlight-color:transparent;
  /* allow native scroll feel on iOS */
  -webkit-overflow-scrolling:touch;
}
.hidden{ display:none !important; }
*, *::before, *::after{ max-width:100%; }

/* ══════════════════════════════════════════════════
   HOME — HEADER & HERO
══════════════════════════════════════════════════ */
.site-header{
  display:flex; justify-content:space-between; align-items:center;
  padding:14px var(--px); background:#0f172a;
  border-bottom:1px solid rgba(0,242,255,0.12);
  position:sticky; top:0; z-index:300;
}
.logo{
  font-size:clamp(14px,4.5vw,20px); font-weight:800; color:var(--cyan);
  letter-spacing:2px; font-family:'Syne',sans-serif;
}
.nav-btn{
  background:none; border:1.5px solid var(--cyan); color:var(--cyan);
  padding:8px 18px; border-radius:20px; cursor:pointer;
  font-family:'Poppins',sans-serif; font-weight:600; font-size:13px;
  transition:.2s; white-space:nowrap; min-height:40px; min-width:72px;
}
.nav-btn:hover{ background:var(--cyan); color:#0b1120; }

.hero{
  min-height:calc(100svh - 58px);
  display:flex; flex-direction:column;
  justify-content:center; align-items:center; text-align:center;
  background:radial-gradient(ellipse at center,#0f172a 0%,#020617 100%);
  animation:fadeUp 1.4s ease; padding:40px var(--px);
}
.hero h1{
  font-size:clamp(24px,7vw,56px); margin-bottom:14px; font-weight:800;
  font-family:'Syne',sans-serif; line-height:1.15;
  background:linear-gradient(90deg,var(--cyan),var(--indigo));
  -webkit-background-clip:text; color:transparent;
}
.hero p{
  font-size:clamp(12px,3.5vw,16px); opacity:.6; margin-bottom:28px;
  font-family:'JetBrains Mono',monospace;
}
.hero-btn{
  padding:13px 34px; border:none; border-radius:30px;
  background:linear-gradient(90deg,var(--cyan),var(--indigo));
  font-weight:700; cursor:pointer; font-size:14px;
  font-family:'Poppins',sans-serif; transition:.2s;
  box-shadow:0 0 28px rgba(0,242,255,0.28); color:#0b1120;
  min-height:48px;
}
.hero-btn:hover{ transform:scale(1.04); }
.hero-btn:active{ transform:scale(.97); }

/* ══════════════════════════════════════════════════
   LOGIN PAGE
══════════════════════════════════════════════════ */
#loginPage{
  display:flex; align-items:center; justify-content:center;
  min-height:100svh; background:var(--bg); padding:20px var(--px);
}
.login-box{
  background:var(--card); padding:clamp(22px,5vw,38px) clamp(18px,5vw,34px);
  border-radius:20px; width:100%; max-width:400px;
  box-shadow:0 0 48px rgba(0,242,255,0.13); border:1px solid rgba(0,242,255,0.1);
}
.login-title{
  text-align:center; margin-bottom:22px; font-weight:800; color:var(--cyan);
  font-family:'Syne',sans-serif; font-size:clamp(16px,4vw,20px); letter-spacing:1px;
}
.tab-bar{ display:flex; gap:8px; margin-bottom:22px; }
.tab-btn{
  flex:1; padding:11px 6px; border:1.5px solid rgba(0,242,255,0.3);
  background:transparent; color:var(--cyan); border-radius:10px;
  cursor:pointer; font-family:'Poppins',sans-serif; font-weight:600;
  font-size:clamp(12px,3.5vw,13px); transition:.2s; min-height:44px;
}
.tab-btn.active{ background:var(--cyan); color:#0b1120; border-color:var(--cyan); }
.field{
  width:100%; padding:13px 14px; margin:7px 0;
  border:1.5px solid var(--surface); border-radius:10px;
  background:var(--surface); color:var(--text);
  font-family:'Poppins',sans-serif; font-size:15px;
  outline:none; transition:.2s; min-height:50px;
}
.field:focus{ border-color:var(--cyan); }
.btn-login{
  width:100%; background:linear-gradient(90deg,var(--cyan),var(--indigo));
  border:none; padding:14px; border-radius:12px; margin-top:12px;
  cursor:pointer; font-family:'Poppins',sans-serif; font-weight:700;
  font-size:15px; color:#0b1120; min-height:50px; transition:.2s;
}
.btn-login:hover{ opacity:.88; }
.btn-login:active{ transform:scale(.98); }

/* ══════════════════════════════════════════════════
   NFC
══════════════════════════════════════════════════ */
.nfc-wrapper{ text-align:center; padding:8px 0; }
.nfc-badge{
  display:inline-block; padding:5px 14px; border-radius:20px;
  font-family:'JetBrains Mono',monospace; font-size:11px; font-weight:600;
  margin-bottom:16px; background:var(--surface); color:var(--muted);
  border:1px solid var(--surface); transition:.4s;
}
.nfc-badge.scanning{ background:rgba(0,242,255,0.1); color:var(--cyan); border-color:var(--cyan); }
.nfc-badge.success { background:rgba(0,255,136,0.1); color:var(--ok);   border-color:var(--ok);   }
.nfc-badge.error   { background:rgba(255,77,77,0.1);  color:var(--danger);border-color:var(--danger);}
.nfc-rings{ position:relative; width:110px; height:110px; margin:0 auto 18px; }
.nfc-ring { position:absolute; border-radius:50%; border:2px solid transparent; }
.nfc-ring:nth-child(1){ width:110px;height:110px;top:0;left:0;  border-color:rgba(0,242,255,0.15);}
.nfc-ring:nth-child(2){ width:80px; height:80px; top:15px;left:15px;border-color:rgba(0,242,255,0.25);}
.nfc-ring:nth-child(3){ width:50px; height:50px; top:30px;left:30px;border-color:rgba(0,242,255,0.4); }
.nfc-icon{ position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);font-size:24px; }
.nfc-rings.scanning .nfc-ring{ animation:ringPulse 1.6s ease-in-out infinite; }
.nfc-rings.scanning .nfc-ring:nth-child(2){ animation-delay:.2s; }
.nfc-rings.scanning .nfc-ring:nth-child(3){ animation-delay:.4s; }
.nfc-rings.success .nfc-ring{ border-color:var(--ok)!important;    opacity:.5; }
.nfc-rings.error   .nfc-ring{ border-color:var(--danger)!important; opacity:.5; }
@keyframes ringPulse{0%,100%{transform:scale(1);opacity:.3;}50%{transform:scale(1.1);opacity:1;}}
.nfc-uid{
  background:var(--surface); border-radius:10px; padding:9px 13px;
  font-family:'JetBrains Mono',monospace; font-size:11px; color:var(--muted);
  margin:10px 0; min-height:34px; word-break:break-all; text-align:center;
  border:1px solid rgba(255,255,255,0.05); transition:.3s;
}
.nfc-uid.found{ color:var(--cyan); border-color:rgba(0,242,255,0.3); }
.nfc-info{ font-size:11px; color:var(--muted); font-family:'JetBrains Mono',monospace; margin-bottom:12px; line-height:1.7; }
.nfc-info a{ color:var(--cyan); text-decoration:none; }
.btn-nfc{
  background:var(--surface); border:1.5px solid var(--cyan); color:var(--cyan);
  padding:11px 20px; border-radius:12px; cursor:pointer;
  font-family:'Poppins',sans-serif; font-weight:600; font-size:14px;
  transition:.2s; min-height:46px; width:100%;
}
.btn-nfc:hover{ background:rgba(0,242,255,0.08); }
.btn-nfc:disabled{ opacity:.4; cursor:not-allowed; }

/* ══════════════════════════════════════════════════
   DASHBOARD SHELL
══════════════════════════════════════════════════ */
#dashboard{ animation:fadeUp .4s ease; display:flex; flex-direction:column; min-height:100svh; }

/* ── top bar ── */
.dash-header{
  display:flex; justify-content:space-between; align-items:center;
  padding:0 var(--px); background:#111827; height:56px;
  border-bottom:1px solid rgba(0,242,255,0.1);
  position:sticky; top:0; z-index:300; gap:10px; flex-shrink:0;
}
.dash-logo{
  font-weight:800; color:var(--cyan); font-family:'Syne',sans-serif;
  letter-spacing:.5px; font-size:clamp(11px,3.2vw,16px); line-height:1.3;
  white-space:nowrap; overflow:hidden; text-overflow:ellipsis; max-width:60vw;
}
.dash-header-right{ display:flex; align-items:center; gap:8px; flex-shrink:0; }
.dash-btn{
  background:none; border:1.5px solid var(--cyan); color:var(--cyan);
  padding:6px 14px; border-radius:20px; cursor:pointer;
  font-family:'Poppins',sans-serif; font-weight:600;
  font-size:12px; transition:.2s; white-space:nowrap; min-height:36px;
}
.dash-btn:hover{ background:var(--cyan); color:#0b1120; }

/* ── scrollable body ── */
.dash-body{
  flex:1; overflow-y:auto; padding:var(--gap) var(--px) calc(var(--gap) + env(safe-area-inset-bottom));
}

/* ══════════════════════════════════════════════════
   STAT PILLS  — always 3-col
══════════════════════════════════════════════════ */
.stats-strip{
  display:grid; grid-template-columns:repeat(3,1fr);
  gap:var(--gap); margin-bottom:var(--gap);
}
.stat-pill{
  background:var(--deep); border:1px solid rgba(0,242,255,0.07);
  border-radius:var(--r); padding:14px 8px; text-align:center;
}
.stat-pill .num{
  font-size:clamp(20px,6vw,34px); font-weight:800; font-family:'Syne',sans-serif;
  line-height:1;
}
.stat-pill .lbl{ font-size:clamp(9px,2.4vw,11px); opacity:.5; margin-top:4px; white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
.stat-pill.high .num{ color:var(--danger); }
.stat-pill.med  .num{ color:var(--warn);   }
.stat-pill.low  .num{ color:var(--ok);     }

/* ══════════════════════════════════════════════════
   MONITOR BAR
══════════════════════════════════════════════════ */
.monitor-bar{
  display:flex; align-items:center; justify-content:space-between;
  background:var(--deep); border:1px solid rgba(0,242,255,0.14);
  border-radius:var(--r); padding:12px 16px; margin-bottom:var(--gap);
  gap:10px; flex-wrap:wrap;
}
.monitor-left{ display:flex; align-items:center; gap:10px; min-width:0; flex:1; }
.monitor-dot{ width:9px; height:9px; border-radius:50%; background:#444; flex-shrink:0; transition:.3s; }
.monitor-dot.active{ background:var(--ok); box-shadow:0 0 8px var(--ok); animation:blink 1.4s ease-in-out infinite; }
.monitor-dot.error { background:var(--danger); box-shadow:0 0 8px var(--danger); }
@keyframes blink{0%,100%{opacity:1;}50%{opacity:.25;}}
.monitor-label{ font-size:12px; font-family:'JetBrains Mono',monospace; color:var(--muted); white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
.monitor-label b{ color:var(--cyan); }
.counter-badge{
  background:var(--surface); border-radius:8px; padding:3px 9px;
  font-size:10px; font-family:'JetBrains Mono',monospace; color:var(--muted); white-space:nowrap;
}
.monitor-right{ display:flex; gap:7px; flex-shrink:0; }
.mbtn{
  padding:6px 13px; border-radius:16px; border:1.5px solid; cursor:pointer;
  font-family:'Poppins',sans-serif; font-size:11px; font-weight:700;
  transition:.2s; min-height:32px; white-space:nowrap;
}
.mbtn-start{ border-color:var(--ok);    color:var(--ok);    background:rgba(0,255,136,0.06); }
.mbtn-stop { border-color:var(--danger);color:var(--danger);background:rgba(255,77,77,0.06);  }
.mbtn:hover{ opacity:.75; }
.mbtn:active{ transform:scale(.95); }

/* ══════════════════════════════════════════════════
   SETTINGS PANEL
══════════════════════════════════════════════════ */
.settings-panel{
  background:var(--deep); border:1px solid rgba(0,242,255,0.18);
  border-radius:var(--r); padding:18px; margin-bottom:var(--gap);
  animation:slideDown .25s ease;
}
@keyframes slideDown{from{opacity:0;transform:translateY(-8px);}to{opacity:1;transform:translateY(0);}}
.settings-panel h3{ color:var(--cyan); font-size:13px; margin-bottom:14px; font-weight:600; }
.settings-grid{ display:grid; grid-template-columns:1fr; gap:10px; }
@media(min-width:600px){ .settings-grid{ grid-template-columns:1fr 1fr; } }
.sg-full{ grid-column:1/-1; }
.settings-group{ display:flex; flex-direction:column; gap:4px; }
.slabel{ font-size:10px; color:var(--muted); font-family:'JetBrains Mono',monospace; text-transform:uppercase; letter-spacing:.5px; }
.sinput,.sselect{
  width:100%; padding:9px 11px;
  background:var(--surface); border:1px solid rgba(0,242,255,0.14);
  border-radius:8px; color:var(--text);
  font-family:'JetBrains Mono',monospace; font-size:12px;
  outline:none; transition:.2s; min-height:38px;
}
.sinput:focus,.sselect:focus{ border-color:var(--cyan); }
.api-code{
  margin-top:12px; background:#070d1a; border-radius:10px; padding:12px;
  font-size:10px; font-family:'JetBrains Mono',monospace; color:var(--muted);
  line-height:1.9; border:1px solid rgba(0,242,255,0.07);
}
.api-code-title{ color:var(--cyan); font-weight:700; margin-bottom:5px; font-size:11px; }
.settings-actions{ display:flex; gap:8px; margin-top:12px; flex-wrap:wrap; }
.sbtn{
  padding:9px 16px; border-radius:9px; cursor:pointer;
  font-family:'Poppins',sans-serif; font-weight:700; font-size:12px; transition:.2s;
  min-height:38px; border:1.5px solid;
}
.sbtn-save{ background:var(--cyan); border-color:var(--cyan); color:#0b1120; }
.sbtn-test{ background:transparent; border-color:var(--indigo); color:#a5b4fc; }
.sbtn-sim { background:transparent; border-color:var(--warn);   color:var(--warn); }
.sbtn:hover{ opacity:.8; }
.api-status-line{
  margin-top:10px; font-size:10px; font-family:'JetBrains Mono',monospace;
  padding:7px 11px; border-radius:8px; background:var(--surface);
  border:1px solid rgba(255,255,255,0.04); color:var(--muted);
}

/* ══════════════════════════════════════════════════
   WA CARDS
══════════════════════════════════════════════════ */
.wa-card{
  background:var(--deep); border:1px solid rgba(0,242,255,0.07);
  border-radius:var(--r); padding:clamp(16px,4vw,24px);
  margin-bottom:var(--gap);
}
.wa-card h2{
  margin-bottom:12px; color:var(--cyan);
  font-size:clamp(13px,3.8vw,16px); font-weight:600;
}
.wa-card textarea{
  width:100%; height:clamp(88px,22vw,120px); padding:12px;
  border-radius:10px; border:1px solid rgba(255,255,255,0.06);
  background:#0a1020; color:white; font-family:'Poppins',sans-serif;
  font-size:clamp(12px,3.5vw,14px); resize:vertical; outline:none; transition:.2s;
}
.wa-card textarea:focus{ border-color:rgba(0,242,255,0.3); }
.btn-scan{
  width:100%; margin-top:11px; padding:13px;
  background:var(--cyan); border:none; border-radius:12px;
  font-weight:700; cursor:pointer; font-family:'Poppins',sans-serif;
  font-size:14px; color:#0b1120; transition:.2s; min-height:48px;
}
.btn-scan:hover{ box-shadow:0 0 20px rgba(0,242,255,0.4); }
.btn-scan:active{ transform:scale(.98); }
.scan-bar{ height:4px; margin-top:10px; border-radius:4px; overflow:hidden; background:var(--surface); }
.scan-bar-inner{ height:100%; width:0; border-radius:4px; background:linear-gradient(90deg,var(--cyan),var(--indigo)); transition:width .5s ease; }
.result-box{ margin-top:12px; font-weight:700; font-size:clamp(12px,3.8vw,15px); line-height:1.5; }
.risk-high  { color:var(--danger); }
.risk-medium{ color:var(--warn);   }
.risk-low   { color:var(--ok);     }
.wa-log{
  font-size:clamp(10px,2.8vw,12px); line-height:1.9; max-height:170px; overflow-y:auto;
  background:#0a1020; padding:12px; border-radius:10px;
  font-family:'JetBrains Mono',monospace; word-break:break-word;
}
.wa-card canvas{ background:#0a1020; border-radius:10px; padding:8px; width:100%!important; }

/* ══════════════════════════════════════════════════
   DANGER POPUP  — bottom sheet on mobile, modal on desktop
══════════════════════════════════════════════════ */
.popup-overlay{
  position:fixed; inset:0; background:rgba(0,0,0,0.72);
  display:flex; align-items:flex-end; justify-content:center;  /* bottom-sheet default */
  z-index:9000; padding:0;
  animation:overlayIn .2s ease; backdrop-filter:blur(4px);
}
@keyframes overlayIn{from{opacity:0;}to{opacity:1;}}
@media(min-width:600px){
  .popup-overlay{ align-items:center; padding:20px; }
}
.popup-box{
  background:#0f172a; width:100%; max-width:460px;
  border:1px solid rgba(255,77,77,0.35);
  box-shadow:0 0 60px rgba(255,77,77,0.2),0 20px 50px rgba(0,0,0,0.5);
  overflow:hidden;
  /* mobile: slide up as bottom sheet */
  border-radius:20px 20px 0 0;
  animation:sheetUp .35s cubic-bezier(.32,1,.32,1);
}
@keyframes sheetUp{from{transform:translateY(100%);}to{transform:translateY(0);}}
@media(min-width:600px){
  .popup-box{ border-radius:20px; animation:popIn .3s cubic-bezier(.34,1.56,.64,1); }
  @keyframes popIn{from{opacity:0;transform:scale(0.86);}to{opacity:1;transform:scale(1);}}
}
/* drag handle for bottom sheet */
.popup-drag{
  width:36px; height:4px; background:rgba(255,255,255,0.15);
  border-radius:2px; margin:10px auto 0; display:block;
}
@media(min-width:600px){ .popup-drag{ display:none; } }
.popup-box.medium{ border-color:rgba(255,204,0,0.35); box-shadow:0 0 60px rgba(255,204,0,0.12),0 20px 50px rgba(0,0,0,0.5); }
.popup-header{
  background:linear-gradient(135deg,rgba(255,77,77,0.18),rgba(79,70,229,0.18));
  padding:16px 20px 14px; border-bottom:1px solid rgba(255,77,77,0.15);
  position:relative;
}
.popup-box.medium .popup-header{ background:linear-gradient(135deg,rgba(255,204,0,0.12),rgba(79,70,229,0.1)); border-color:rgba(255,204,0,0.15); }
.popup-header-row{ display:flex; align-items:center; gap:11px; }
.popup-icon{ font-size:28px; animation:shake .4s ease; }
@keyframes shake{0%,100%{transform:rotate(0);}25%{transform:rotate(-8deg);}75%{transform:rotate(8deg);}}
.popup-title{ font-family:'Syne',sans-serif; font-size:clamp(15px,4vw,18px); font-weight:800; color:var(--danger); }
.popup-box.medium .popup-title{ color:var(--warn); }
.popup-subtitle{ font-size:11px; color:var(--muted); font-family:'JetBrains Mono',monospace; margin-top:1px; }
.popup-close{
  position:absolute; top:14px; right:14px;
  background:rgba(255,255,255,0.08); border:none; color:var(--muted);
  width:28px; height:28px; border-radius:50%; cursor:pointer; font-size:13px;
  display:flex; align-items:center; justify-content:center; transition:.2s;
}
.popup-close:hover{ background:rgba(255,77,77,0.2); color:var(--danger); }
.popup-body{ padding:16px 20px 20px; }
.popup-sender{ display:flex; align-items:center; gap:10px; margin-bottom:12px; }
.popup-sender-icon{
  width:36px; height:36px; border-radius:50%;
  background:rgba(255,77,77,0.1); border:1px solid rgba(255,77,77,0.25);
  display:flex; align-items:center; justify-content:center; font-size:17px; flex-shrink:0;
}
.popup-sender-name{ font-weight:600; font-size:13px; }
.popup-sender-time{ font-size:10px; color:var(--muted); font-family:'JetBrains Mono',monospace; }
.popup-message-box{
  background:#070d1a; border-radius:10px; padding:12px 14px;
  font-size:12px; line-height:1.7; color:var(--text);
  border:1px solid rgba(255,255,255,0.05); max-height:100px; overflow-y:auto;
  margin-bottom:12px; word-break:break-word;
}
.popup-risk-badge{
  display:inline-flex; align-items:center; gap:5px;
  padding:5px 13px; border-radius:20px; font-size:11px; font-weight:700;
  margin-bottom:10px; font-family:'JetBrains Mono',monospace;
}
.popup-risk-badge.high  { background:rgba(255,77,77,0.12);  color:var(--danger); border:1px solid rgba(255,77,77,0.25); }
.popup-risk-badge.medium{ background:rgba(255,204,0,0.12);  color:var(--warn);   border:1px solid rgba(255,204,0,0.25); }
.popup-score{ font-size:10px; color:var(--muted); font-family:'JetBrains Mono',monospace; margin-bottom:12px; }
.popup-keywords{ display:flex; flex-wrap:wrap; gap:5px; margin-bottom:14px; }
.popup-kw{ background:rgba(255,77,77,0.08); border:1px solid rgba(255,77,77,0.2); color:#fca5a5; padding:2px 9px; border-radius:20px; font-size:10px; font-family:'JetBrains Mono',monospace; }
.popup-actions{ display:grid; grid-template-columns:1fr 1fr; gap:9px; }
.popup-btn-ok{
  padding:12px; background:var(--surface); border:1px solid rgba(255,255,255,0.1);
  border-radius:11px; color:var(--muted); font-family:'Poppins',sans-serif;
  font-weight:600; font-size:13px; cursor:pointer; transition:.2s; min-height:46px;
}
.popup-btn-ok:hover{ background:#1e293b; color:var(--text); }
.popup-btn-block{
  padding:12px; background:rgba(255,77,77,0.12);
  border:1px solid rgba(255,77,77,0.28); border-radius:11px; color:var(--danger);
  font-family:'Poppins',sans-serif; font-weight:700; font-size:13px;
  cursor:pointer; transition:.2s; min-height:46px;
}
.popup-btn-block:hover{ background:rgba(255,77,77,0.22); }

/* ══════════════════════════════════════════════════
   TOAST  — bottom-left on desktop, bottom on mobile
══════════════════════════════════════════════════ */
.toast-wrap{
  position:fixed; bottom:0; left:0; right:0; z-index:8000;
  padding:0 12px calc(12px + env(safe-area-inset-bottom));
  display:flex; flex-direction:column-reverse; gap:8px;
  pointer-events:none;
}
@media(min-width:600px){
  .toast-wrap{ left:auto; right:20px; bottom:20px; width:320px; }
}
.toast{
  background:#141f35; border-radius:12px; padding:12px 14px;
  box-shadow:0 8px 28px rgba(0,0,0,0.45);
  border-left:3px solid;
  display:flex; align-items:flex-start; gap:10px;
  animation:toastIn .3s ease; pointer-events:all; cursor:pointer;
}
.toast:hover{ opacity:.85; }
@keyframes toastIn{ from{opacity:0;transform:translateY(16px);}to{opacity:1;transform:translateY(0);} }
@keyframes toastOut{ from{opacity:1;transform:translateY(0);}to{opacity:0;transform:translateY(16px);} }
.toast.high  { border-color:var(--danger); }
.toast.medium{ border-color:var(--warn);   }
.toast.low   { border-color:var(--ok);     }
.toast-icon{ font-size:18px; flex-shrink:0; }
.toast-body{ flex:1; min-width:0; }
.toast-title{ font-size:12px; font-weight:700; }
.toast.high  .toast-title{ color:var(--danger); }
.toast.medium .toast-title{ color:var(--warn); }
.toast.low   .toast-title{ color:var(--ok); }
.toast-msg { font-size:11px; color:var(--muted); font-family:'JetBrains Mono',monospace; overflow:hidden; text-overflow:ellipsis; white-space:nowrap; }
.toast-time{ font-size:10px; color:var(--muted); font-family:'JetBrains Mono',monospace; margin-top:2px; }
.toast-x{ background:none; border:none; color:var(--muted); font-size:14px; cursor:pointer; padding:0 2px; flex-shrink:0; }

/* ══════════════════════════════════════════════════
   ANIMATIONS
══════════════════════════════════════════════════ */
@keyframes fadeUp{ from{opacity:0;transform:translateY(10px);}to{opacity:1;transform:translateY(0);} }
</style>
</head>
<body>

<!-- ═══════════════════════ HOME ═══════════════════════ -->
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

<!-- ═══════════════════════ LOGIN ═══════════════════════ -->
<section id="loginPage" class="hidden">
  <div class="login-box">
    <div class="login-title">SENIORSHIELD</div>
    <div class="tab-bar">
      <button class="tab-btn active" onclick="showTab('tabPassword',this)">🔑 Password</button>
      <button class="tab-btn"        onclick="showTab('tabNFC',this)"     >📡 NFC</button>
    </div>
    <div id="tabPassword">
      <input class="field" type="text"     id="user" placeholder="Username"  autocomplete="username"/>
      <input class="field" type="password" id="pass" placeholder="Password"  autocomplete="current-password"/>
      <button class="btn-login" onclick="login()">Login</button>
    </div>
    <div id="tabNFC" class="hidden">
      <div class="nfc-wrapper">
        <div id="nfcBadge" class="nfc-badge">● SIAP</div>
        <div id="nfcRings" class="nfc-rings">
          <div class="nfc-ring"></div><div class="nfc-ring"></div><div class="nfc-ring"></div>
          <span class="nfc-icon">📡</span>
        </div>
        <div id="nfcUID" class="nfc-uid">UID akan tampil di sini...</div>
        <p class="nfc-info">Gunakan Chrome Android &amp; aktifkan NFC.<br/><a href="https://support.google.com/android/answer/9075925" target="_blank">Cara aktifkan NFC ›</a></p>
        <button id="nfcScanBtn" class="btn-nfc" onclick="startNFCScan()">Mulai Scan NFC</button>
        <div id="nfcHint" style="margin-top:10px;font-size:11px;color:var(--muted);font-family:'JetBrains Mono',monospace;text-align:center;"></div>
      </div>
    </div>
  </div>
</section>

<!-- ═══════════════════════ DASHBOARD ═══════════════════════ -->
<section id="dashboard" class="hidden">

  <!-- sticky top bar -->
  <div class="dash-header">
    <div class="dash-logo">🛡 WA GUARDIAN — SENIORSHIELD</div>
    <div class="dash-header-right">
      <button class="dash-btn" onclick="toggleSettings()">⚙ API</button>
      <button class="dash-btn" onclick="logout()">Logout</button>
    </div>
  </div>

  <!-- scrollable content -->
  <div class="dash-body">

    <!-- MONITOR BAR -->
    <div class="monitor-bar">
      <div class="monitor-left">
        <div id="monDot" class="monitor-dot"></div>
        <div id="monLabel" class="monitor-label">Monitor: <b>Tidak Aktif</b></div>
        <div id="msgCounter" class="counter-badge">0 pesan</div>
      </div>
      <div class="monitor-right">
        <button class="mbtn mbtn-start" onclick="startMonitor()">▶ Mulai</button>
        <button class="mbtn mbtn-stop"  onclick="stopMonitor()">■ Stop</button>
      </div>
    </div>

    <!-- SETTINGS PANEL -->
    <div id="settingsPanel" class="settings-panel hidden">
      <h3>⚙ Konfigurasi API &amp; Monitor</h3>
      <div class="settings-grid">
        <div class="settings-group">
          <div class="slabel">Mode Koneksi</div>
          <select class="sselect" id="connMode" onchange="onConnModeChange()">
            <option value="simulate">🧪 Simulasi (Demo)</option>
            <option value="poll">🔄 HTTP Polling API</option>
            <option value="ws">⚡ WebSocket Real-time</option>
          </select>
        </div>
        <div class="settings-group">
          <div class="slabel">Interval Polling (detik)</div>
          <input class="sinput" id="pollInterval" type="number" value="10" min="3" max="300"/>
        </div>
        <div class="settings-group sg-full" id="apiUrlGroup">
          <div class="slabel">URL API / WebSocket</div>
          <input class="sinput" id="apiUrl" type="text" placeholder="https://server.com/api/sms/latest"/>
        </div>
        <div class="settings-group">
          <div class="slabel">API Key (opsional)</div>
          <input class="sinput" id="apiKey" type="text" placeholder="Bearer token"/>
        </div>
        <div class="settings-group">
          <div class="slabel">Notifikasi minimum</div>
          <select class="sselect" id="minRisk">
            <option value="30">Medium &amp; High Risk</option>
            <option value="60">High Risk saja</option>
            <option value="0">Semua pesan</option>
          </select>
        </div>
      </div>
      <div class="api-code">
        <div class="api-code-title">📡 Format JSON API yang diharapkan:</div>
        [{ "id":"msg_001", "sender":"+628xxx", "body":"isi pesan", "timestamp":"ISO8601" }]<br/>
        <span style="color:#94a3b8;">Server harus mendukung param: ?since=TIMESTAMP</span>
      </div>
      <div class="settings-actions">
        <button class="sbtn sbtn-save" onclick="saveSettings()">💾 Simpan</button>
        <button class="sbtn sbtn-test" onclick="testConnection()">🔌 Test Koneksi</button>
        <button class="sbtn sbtn-sim"  onclick="triggerSimulation()">🧪 Kirim Uji</button>
      </div>
      <div class="api-status-line" id="apiStatusLine">Status: Belum dikonfigurasi</div>
    </div>

    <!-- STATS -->
    <div class="stats-strip">
      <div class="stat-pill high"><div class="num" id="statHigh">0</div><div class="lbl">⚠ High</div></div>
      <div class="stat-pill med" ><div class="num" id="statMed" >0</div><div class="lbl">⚡ Medium</div></div>
      <div class="stat-pill low" ><div class="num" id="statLow" >0</div><div class="lbl">✓ Low</div></div>
    </div>

    <!-- SCAN MANUAL -->
    <div class="wa-card">
      <h2>📩 Scan Manual SMS / WhatsApp</h2>
      <textarea id="inputText" placeholder="Tempel pesan mencurigakan di sini..."></textarea>
      <button class="btn-scan" onclick="scanText(null,null,true)">🔍 Scan Sekarang</button>
      <div class="scan-bar"><div id="scanBar" class="scan-bar-inner"></div></div>
      <div id="resultBox" class="result-box"></div>
    </div>

    <!-- CHART -->
    <div class="wa-card">
      <h2>📊 Statistik Deteksi</h2>
      <canvas id="attackChart"></canvas>
    </div>

    <!-- LOG -->
    <div class="wa-card">
      <h2>📋 Log Aktivitas</h2>
      <div class="wa-log" id="logBox">Menunggu pesan...<br/></div>
    </div>

  </div><!-- /.dash-body -->
</section>

<!-- POPUP & TOAST containers -->
<div id="popupContainer"></div>
<div class="toast-wrap" id="toastWrap"></div>

<!-- ═══════════════════════════════════════════════════════════
     JAVASCRIPT
═══════════════════════════════════════════════════════════ -->
<script>
/* ── DATABASES ── */
const NFC_DB=[
  {uid:"04:a3:b2:c1",name:"Admin Utama"},
  {uid:"04:12:34:56",name:"Staff Senior 1"},
  {uid:"04:ab:cd:ef",name:"Staff Senior 2"},
];
const USER_DB=[
  {username:"admin",       password:"1234",            name:"Admin"},
  {username:"seniorshield",password:"sahabatselamanya",name:"SeniorShield"},
];
const KEYWORDS=[
  "hadiah","klik link","verifikasi akun","akun diblokir","transfer sekarang",
  "menang undian","gratis saldo","bank","pin","otp","kode verifikasi",
  "whatsapp support","login dari perangkat baru","reset password","data anda",
  "segera","urgent","konfirmasi","perangkat baru","terkena hack",
  "kode rahasia","jangan beritahu","transfer dana","rekening"
];
const BAD_DOMAINS=[".xyz",".top",".click",".gq",".ru",".tk",".cf",".ml",".ga"];
const SIM_MSGS=[
  {sender:"+6281234567890",body:"Selamat! Akun WhatsApp Anda akan diblokir. Klik link ini: http://wa-verify.xyz/login123"},
  {sender:"+6289876543210",body:"Kode OTP Anda: 482931. Jangan beritahu siapapun. Transfer dana sekarang."},
  {sender:"+6282111222333",body:"Hadiah undian Anda 50 juta siap. Hubungi CS: http://hadiah-wa.top/klaim"},
  {sender:"+6283444555666",body:"Halo! Apa kabar? Jadi ketemuan besok kan?"},
  {sender:"Bank Central",   body:"Tagihan kartu kredit jatuh tempo. Bayar melalui aplikasi resmi."},
  {sender:"+6285999888777",body:"PIN ATM akan direset karena login dari perangkat baru. Hubungi 1234."},
  {sender:"WA Support",     body:"Akun akan dihapus 24 jam. Klik: http://whatsapp-support.gq/save"},
  {sender:"+6287666555444",body:"Mama, ini aku. Nomor baru. Tolong transfer ke rekening ini ya."},
];
let simIdx=0;

/* ── STATE ── */
let highC=0,medC=0,lowC=0,totalC=0;
let monInterval=null,wsConn=null;
let seenIds=new Set();
let cfg={mode:"simulate",url:"",key:"",interval:10,minRisk:30};

/* ── NAVIGATION ── */
function showLogin(){
  g("homePage").classList.add("hidden");
  g("loginPage").classList.remove("hidden");
}
function showDashboard(){
  g("loginPage").classList.add("hidden");
  g("dashboard").classList.remove("hidden");
  loadLogs();
  // request notification permission immediately after login
  if(Notification.permission==="default") Notification.requestPermission();
}
function showTab(id,btn){
  qsa(".tab-btn").forEach(b=>b.classList.remove("active"));
  g("tabPassword").classList.add("hidden");
  g("tabNFC").classList.add("hidden");
  g(id).classList.remove("hidden");
  btn.classList.add("active");
}
function logout(){ stopMonitor(); if(wsConn)wsConn.close(); location.reload(); }

/* ── LOGIN ── */
function login(){
  const u=g("user").value.trim(), p=g("pass").value;
  if(USER_DB.find(x=>x.username===u&&x.password===p)) showDashboard();
  else alert("Username atau password salah.");
}
document.addEventListener("DOMContentLoaded",()=>{
  ["user","pass"].forEach(id=>g(id).addEventListener("keydown",e=>{if(e.key==="Enter")login();}));
});

/* ── NFC ── */
let nfcAC=null;
async function startNFCScan(){
  const btn=g("nfcScanBtn"),badge=g("nfcBadge"),uid=g("nfcUID"),hint=g("nfcHint");
  if(!("NDEFReader" in window)){setNS("error");badge.textContent="● NFC Tidak Didukung";uid.textContent="Gunakan Chrome 89+ di Android.";return;}
  try{
    btn.disabled=true;btn.textContent="Scanning...";setNS("scanning");
    badge.textContent="● SCANNING...";uid.textContent="Menunggu kartu NFC...";
    uid.classList.remove("found");hint.textContent="Tempelkan kartu ke ponsel";
    nfcAC=new AbortController();
    const r=new NDEFReader();
    await r.scan({signal:nfcAC.signal});
    r.addEventListener("reading",({serialNumber})=>handleNFC(serialNumber));
    r.addEventListener("readingerror",()=>{setNS("error");badge.textContent="● Error";uid.textContent="Gagal membaca.";resetNFCBtn();});
  }catch(e){
    if(e.name==="NotAllowedError"){badge.textContent="● Izin Ditolak";uid.textContent="Aktifkan izin NFC.";}
    else if(e.name==="AbortError"){badge.textContent="● Dibatalkan";uid.textContent="Scan dibatalkan.";}
    else{badge.textContent="● Error";uid.textContent=e.message;}
    setNS("error");hint.textContent="";resetNFCBtn();
  }
}
function handleNFC(raw){
  const badge=g("nfcBadge"),uid=g("nfcUID"),hint=g("nfcHint");
  uid.textContent="UID: "+raw.toUpperCase();uid.classList.add("found");
  const m=NFC_DB.find(e=>e.uid.toLowerCase()===raw.toLowerCase());
  if(m){setNS("success");badge.textContent="✓ TERVERIFIKASI";hint.textContent="Selamat datang, "+m.name+"!";if(nfcAC)nfcAC.abort();setTimeout(()=>showDashboard(),1200);}
  else{setNS("error");badge.textContent="✗ TIDAK DIKENAL";hint.textContent="Kartu tidak terdaftar.";if(nfcAC)nfcAC.abort();resetNFCBtn(2800);}
}
function setNS(s){g("nfcRings").className="nfc-rings"+(s?" "+s:"");g("nfcBadge").className="nfc-badge"+(s?" "+s:"");}
function resetNFCBtn(d=0){setTimeout(()=>{const b=g("nfcScanBtn");if(b){b.disabled=false;b.textContent="Mulai Scan NFC";}},d);}

/* ── SETTINGS ── */
function toggleSettings(){g("settingsPanel").classList.toggle("hidden");}
function onConnModeChange(){
  const m=g("connMode").value,s=(m!=="simulate");
  g("apiUrlGroup").style.opacity=s?"1":"0.4";
}
function saveSettings(){
  cfg.mode=g("connMode").value;cfg.url=g("apiUrl").value.trim();
  cfg.key=g("apiKey").value.trim();cfg.interval=parseInt(g("pollInterval").value)||10;
  cfg.minRisk=parseInt(g("minRisk").value)||30;
  setAS("✅ Disimpan. Mode: "+cfg.mode);
  g("settingsPanel").classList.add("hidden");
}
function setAS(t){g("apiStatusLine").textContent="Status: "+t;}
async function testConnection(){
  if(cfg.mode==="simulate"){setAS("🧪 Mode simulasi — tidak perlu koneksi");return;}
  if(!cfg.url){setAS("❌ URL belum diisi");return;}
  setAS("🔄 Menghubungkan...");
  try{
    const h={"Content-Type":"application/json"};
    if(cfg.key)h["Authorization"]="Bearer "+cfg.key;
    const r=await fetch(cfg.url+"?test=1",{method:"GET",headers:h,signal:AbortSignal.timeout(6000)});
    setAS(r.ok?"✅ Berhasil! Status: "+r.status:"⚠ Status: "+r.status);
  }catch(e){setAS("❌ Gagal: "+e.message);}
}

/* ── MONITOR ── */
function startMonitor(){
  if(monInterval||wsConn){toast("Monitor sudah berjalan","","low");return;}
  saveSettings();
  const dot=g("monDot"),lbl=g("monLabel");
  if(cfg.mode==="simulate"){
    dot.classList.add("active");
    lbl.innerHTML='Monitor: <b style="color:var(--ok)">AKTIF — Simulasi</b>';
    monInterval=setInterval(simTick,cfg.interval*1000);
    toast("Monitor Aktif","Simulasi setiap "+cfg.interval+"s","low");
  }else if(cfg.mode==="poll"){
    if(!cfg.url){setAS("❌ URL harus diisi");return;}
    dot.classList.add("active");
    lbl.innerHTML='Monitor: <b style="color:var(--ok)">AKTIF — HTTP Poll</b>';
    monInterval=setInterval(pollHTTP,cfg.interval*1000);
    toast("Monitor Aktif","Polling API setiap "+cfg.interval+"s","low");
  }else if(cfg.mode==="ws"){
    if(!cfg.url){setAS("❌ URL WebSocket harus diisi");return;}
    connectWS();
  }
}
function stopMonitor(){
  if(monInterval){clearInterval(monInterval);monInterval=null;}
  if(wsConn){wsConn.close();wsConn=null;}
  g("monDot").className="monitor-dot";
  g("monLabel").innerHTML='Monitor: <b>Tidak Aktif</b>';
  toast("Monitor Dihentikan","Auto-deteksi dimatikan","low");
}

/* ── SIM TICK ── */
function simTick(){
  const m=SIM_MSGS[simIdx%SIM_MSGS.length];simIdx++;
  processMsg({id:"sim_"+simIdx,sender:m.sender,body:m.body,timestamp:new Date().toISOString()});
}
function triggerSimulation(){simTick();setAS("🧪 Pesan uji dikirim: "+new Date().toLocaleTimeString());}

/* ── HTTP POLL ── */
let lastPoll=new Date().toISOString();
async function pollHTTP(){
  try{
    const h={"Content-Type":"application/json"};
    if(cfg.key)h["Authorization"]="Bearer "+cfg.key;
    const url=cfg.url+(cfg.url.includes("?")?"&":"?")+"since="+encodeURIComponent(lastPoll);
    const r=await fetch(url,{headers:h,signal:AbortSignal.timeout(8000)});
    if(!r.ok)throw new Error("HTTP "+r.status);
    const data=await r.json();
    lastPoll=new Date().toISOString();
    if(Array.isArray(data)) data.forEach(m=>{if(!seenIds.has(m.id)){seenIds.add(m.id);processMsg(m);}});
    setAS("✅ Poll "+new Date().toLocaleTimeString());
  }catch(e){setAS("❌ Poll gagal: "+e.message);g("monDot").className="monitor-dot error";}
}

/* ── WEBSOCKET ── */
function connectWS(){
  const dot=g("monDot"),lbl=g("monLabel");
  try{
    wsConn=new WebSocket(cfg.url+(cfg.key?"?token="+cfg.key:""));
    wsConn.onopen=()=>{dot.classList.add("active");lbl.innerHTML='Monitor: <b style="color:var(--ok)">AKTIF — WebSocket</b>';setAS("✅ WS terhubung");toast("WebSocket Terhubung","Real-time aktif","low");};
    wsConn.onmessage=(ev)=>{try{const d=JSON.parse(ev.data);(Array.isArray(d)?d:[d]).forEach(m=>{if(!seenIds.has(m.id)){seenIds.add(m.id);processMsg(m);}});}catch(e){}};
    wsConn.onerror=()=>{dot.className="monitor-dot error";setAS("❌ WS error");};
    wsConn.onclose=()=>{dot.classList.remove("active","error");lbl.innerHTML='Monitor: <b>WS Terputus</b>';wsConn=null;};
  }catch(e){setAS("❌ WS gagal: "+e.message);}
}

/* ── PROCESS INCOMING ── */
function processMsg({id,sender,body,timestamp}){
  const res=analyze(body);
  totalC++;g("msgCounter").textContent=totalC+" pesan";
  if(res.score>=cfg.minRisk){
    const lv=res.score>=60?"high":"medium";
    showPopup({sender,body,score:res.score,status:res.status,keywords:res.found,lv,timestamp});
    toast(res.status,"Dari: "+sender,lv);
    notifyOS(sender,res.status);
    if(lv==="high")highC++;else medC++;
  }else{
    lowC++;
    if(cfg.minRisk===0) toast("Pesan Aman","Dari: "+sender,"low");
  }
  addLog("[AUTO] "+sender+" → "+res.status,res.score>=60?"#ff4d4d":res.score>=30?"#ffcc00":"#00ff88");
  updateChart();
}

/* ── MANUAL SCAN ── */
function scanText(bodyOvr=null,senderOvr=null,manual=false){
  const text=bodyOvr||g("inputText").value;
  if(!text.trim())return;
  const res=analyze(text);
  if(manual){
    const bar=g("scanBar");bar.style.width="0";
    setTimeout(()=>{bar.style.width=Math.min(res.score,100)+"%";},50);
    const rb=g("resultBox");
    rb.className=res.score>=60?"result-box risk-high":res.score>=30?"result-box risk-medium":"result-box risk-low";
    rb.innerHTML="Skor: <strong>"+res.score+"</strong> → "+res.status;
    if(res.score>=60){highC++;notifyOS("Manual Scan",res.status);showPopup({sender:"Manual Scan",body:text,score:res.score,status:res.status,keywords:res.found,lv:"high",timestamp:new Date().toISOString()});}
    else if(res.score>=30)medC++;else lowC++;
    addLog("[MANUAL] "+res.status,res.score>=60?"#ff4d4d":res.score>=30?"#ffcc00":"#00ff88");
    updateChart();saveLog(res.status);
  }
  return res;
}

/* ── ANALYZE ── */
function analyze(text){
  const t=text.toLowerCase();let score=0;const found=[];
  KEYWORDS.forEach(k=>{if(t.includes(k)){score+=15;found.push(k);}});
  BAD_DOMAINS.forEach(d=>{if(t.includes(d)){score+=25;found.push(d);}});
  if(t.match(/https?:\/\//))score+=20;
  if(t.match(/\d{4,6}/)&&t.includes("otp"))score+=30;
  else if(t.match(/\d{4,6}/))score+=10;
  let status=score>=60?"HIGH RISK — Kemungkinan Phishing / Hack WA!":score>=30?"MEDIUM RISK — Perlu waspada.":"LOW RISK — Pesan aman.";
  return{score,status,found:[...new Set(found)]};
}

/* ── CHART ── */
let highCount=0,mediumCount=0,lowCount=0;
const chart=new Chart(g("attackChart").getContext("2d"),{
  type:"bar",
  data:{labels:["High Risk","Medium Risk","Low Risk"],datasets:[{label:"Deteksi",data:[0,0,0],backgroundColor:["rgba(255,77,77,.75)","rgba(255,204,0,.75)","rgba(0,255,136,.75)"],borderColor:["#ff4d4d","#ffcc00","#00ff88"],borderWidth:1,borderRadius:6}]},
  options:{responsive:true,maintainAspectRatio:true,plugins:{legend:{labels:{color:"white",font:{family:"Poppins",size:11}}}},scales:{x:{ticks:{color:"white",font:{size:10}},grid:{color:"rgba(255,255,255,0.04)"}},y:{ticks:{color:"white",font:{size:10}},grid:{color:"rgba(255,255,255,0.04)"},beginAtZero:true}}}
});
function updateChart(){
  chart.data.datasets[0].data=[highC,medC,lowC];chart.update();
  g("statHigh").textContent=highC;g("statMed").textContent=medC;g("statLow").textContent=lowC;
}

/* ── LOG ── */
function addLog(msg,color){
  const t=new Date().toLocaleTimeString(),lb=g("logBox");
  const c=color||(msg.includes("HIGH")?"#ff4d4d":msg.includes("MEDIUM")?"#ffcc00":"#00ff88");
  lb.innerHTML+=`<span style="color:${c}">[${t}] ${msg}</span><br/>`;
  lb.scrollTop=lb.scrollHeight;
}
function saveLog(msg){try{const l=JSON.parse(localStorage.getItem("ss_logs"))||[];l.push({time:new Date().toLocaleTimeString(),msg});if(l.length>200)l.shift();localStorage.setItem("ss_logs",JSON.stringify(l));}catch(e){}}
function loadLogs(){try{const l=JSON.parse(localStorage.getItem("ss_logs"))||[];if(!l.length)return;g("logBox").innerHTML="";l.forEach(x=>addLog(x.msg));}catch(e){}}

/* ── OS NOTIFICATION ── */
function notifyOS(sender,status){
  if(Notification.permission==="granted")new Notification("⚠ SeniorShield",{body:sender+"\n"+status});
  else if(Notification.permission!=="denied")Notification.requestPermission();
}

/* ── POPUP ── */
function showPopup({sender,body,score,status,keywords,lv,timestamp}){
  const id="p"+Date.now();
  const t=timestamp?new Date(timestamp).toLocaleTimeString():new Date().toLocaleTimeString();
  const kw=keywords.map(k=>`<span class="popup-kw">${esc(k)}</span>`).join("");
  g("popupContainer").insertAdjacentHTML("beforeend",`
  <div class="popup-overlay" id="${id}" onclick="closePopupOut(event,'${id}')">
    <div class="popup-box ${lv}">
      <span class="popup-drag"></span>
      <div class="popup-header">
        <div class="popup-header-row">
          <span class="popup-icon">${lv==="high"?"🚨":"⚠️"}</span>
          <div>
            <div class="popup-title">${lv==="high"?"ANCAMAN TERDETEKSI":"PESAN MENCURIGAKAN"}</div>
            <div class="popup-subtitle">SeniorShield AI Alert</div>
          </div>
        </div>
        <button class="popup-close" onclick="closePopup('${id}')">✕</button>
      </div>
      <div class="popup-body">
        <div class="popup-sender">
          <div class="popup-sender-icon">📱</div>
          <div><div class="popup-sender-name">${esc(sender)}</div><div class="popup-sender-time">${t}</div></div>
        </div>
        <div class="popup-message-box">${esc(body)}</div>
        <div class="popup-risk-badge ${lv}">${lv==="high"?"🔴 HIGH RISK":"🟡 MEDIUM RISK"}</div>
        <div class="popup-score">Skor Ancaman: ${score}</div>
        ${kw?`<div class="popup-keywords">${kw}</div>`:""}
        <div class="popup-actions">
          <button class="popup-btn-ok"    onclick="closePopup('${id}')">✓ Mengerti</button>
          <button class="popup-btn-block" onclick="blockClose('${id}','${esc(sender)}')">🚫 Blokir</button>
        </div>
      </div>
    </div>
  </div>`);
}
function closePopup(id){const el=g(id);if(el){el.style.opacity="0";el.style.transition="opacity .2s";setTimeout(()=>el.remove(),200);}}
function closePopupOut(e,id){if(e.target.id===id)closePopup(id);}
function blockClose(id,sender){closePopup(id);addLog("[BLOKIR] "+sender+" ditandai berbahaya","#ff4d4d");toast("Diblokir",sender+" ditandai berbahaya","high");}

/* ── TOAST ── */
function toast(title,msg,level){
  const icon=level==="high"?"🚨":level==="medium"?"⚠️":"✅";
  const id="t"+Date.now();
  g("toastWrap").insertAdjacentHTML("beforeend",`
  <div class="toast ${level}" id="${id}" onclick="rmToast('${id}')">
    <span class="toast-icon">${icon}</span>
    <div class="toast-body">
      <div class="toast-title">${esc(title)}</div>
      <div class="toast-msg">${esc((msg||"").substring(0,55)+((msg||"").length>55?"...":""))}</div>
      <div class="toast-time">${new Date().toLocaleTimeString()}</div>
    </div>
    <button class="toast-x" onclick="rmToast('${id}')">✕</button>
  </div>`);
  setTimeout(()=>rmToast(id),6000);
}
function rmToast(id){const el=g(id);if(el){el.style.animation="toastOut .3s ease forwards";setTimeout(()=>el.remove(),300);}}

/* ── UTILS ── */
function g(id){return document.getElementById(id);}
function qsa(s){return document.querySelectorAll(s);}
function esc(s){return String(s).replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;").replace(/"/g,"&quot;");}
</script>
</body>
</html>
