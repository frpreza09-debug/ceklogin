<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0"/>
<title>SeniorShield | WA Guardian AI</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&family=Syne:wght@700;800&family=JetBrains+Mono:wght@300;400;600&display=swap" rel="stylesheet"/>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
/* ══════════════════════════════════════ ROOT ══════════════════════════════════════ */
:root{
  --cyan:#00f2ff; --indigo:#4f46e5;
  --bg:#0b1120; --card:#111827; --surface:#1e293b;
  --text:#e2e8f0; --muted:rgba(226,232,240,0.5);
  --danger:#ff4d4d; --warn:#ffcc00; --ok:#00ff88;
  --radius:15px; --pad-x:60px;
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{background:var(--bg);color:var(--text);overflow-x:hidden;font-family:'Poppins',sans-serif;-webkit-tap-highlight-color:transparent;}
.hidden{display:none!important;}
img,canvas,textarea,input,button{max-width:100%;}

/* ══════════════════════════════════════ HEADER ══════════════════════════════════════ */
.site-header{
  display:flex;justify-content:space-between;align-items:center;
  padding:16px var(--pad-x);background:#0f172a;
  border-bottom:1px solid rgba(0,242,255,0.12);
  position:sticky;top:0;z-index:200;
}
.logo{font-size:clamp(15px,4vw,20px);font-weight:800;color:var(--cyan);letter-spacing:2px;font-family:'Syne',sans-serif;}
.nav-btn{background:none;border:1px solid var(--cyan);color:var(--cyan);padding:8px 20px;border-radius:20px;cursor:pointer;font-family:'Poppins',sans-serif;font-weight:600;font-size:14px;transition:.2s;white-space:nowrap;min-height:40px;}
.nav-btn:hover{background:var(--cyan);color:#0b1120;}

/* ══════════════════════════════════════ HERO ══════════════════════════════════════ */
.hero{min-height:calc(100svh - 61px);display:flex;flex-direction:column;justify-content:center;align-items:center;text-align:center;background:radial-gradient(ellipse at center,#0f172a 0%,#020617 100%);animation:fadeIn 1.5s ease;padding:40px 24px;}
.hero h1{font-size:clamp(26px,6vw,54px);margin-bottom:16px;font-weight:800;font-family:'Syne',sans-serif;line-height:1.2;background:linear-gradient(90deg,var(--cyan),var(--indigo));-webkit-background-clip:text;color:transparent;}
.hero p{font-size:clamp(13px,3.5vw,17px);opacity:.6;margin-bottom:32px;font-family:'JetBrains Mono',monospace;padding:0 10px;}
.hero-btn{padding:14px 36px;border:none;border-radius:30px;background:linear-gradient(90deg,var(--cyan),var(--indigo));font-weight:700;cursor:pointer;font-size:15px;font-family:'Poppins',sans-serif;transition:.2s;box-shadow:0 0 30px rgba(0,242,255,0.3);color:#0b1120;min-height:48px;}
.hero-btn:hover{transform:scale(1.04);}

/* ══════════════════════════════════════ LOGIN ══════════════════════════════════════ */
#loginPage{display:flex;align-items:center;justify-content:center;min-height:100svh;background:var(--bg);padding:20px;}
.login-box{background:var(--card);padding:clamp(24px,5vw,40px) clamp(20px,5vw,36px);border-radius:20px;width:100%;max-width:380px;box-shadow:0 0 40px rgba(0,242,255,0.15);border:1px solid rgba(0,242,255,0.1);}
.login-title{text-align:center;margin-bottom:24px;font-weight:800;color:var(--cyan);font-family:'Syne',sans-serif;font-size:clamp(17px,4vw,20px);letter-spacing:1px;}
.tab-bar{display:flex;gap:8px;margin-bottom:24px;}
.tab-btn{flex:1;padding:11px 8px;border:1px solid rgba(0,242,255,0.3);background:transparent;color:var(--cyan);border-radius:10px;cursor:pointer;font-family:'Poppins',sans-serif;font-weight:600;font-size:clamp(12px,3.5vw,14px);transition:.2s;min-height:44px;}
.tab-btn.active{background:var(--cyan);color:#0b1120;border-color:var(--cyan);}
.field{width:100%;padding:13px 14px;margin:8px 0;border:1px solid var(--surface);border-radius:10px;background:var(--surface);color:var(--text);font-family:'Poppins',sans-serif;font-size:15px;outline:none;transition:.2s;min-height:48px;}
.field:focus{border-color:var(--cyan);}
.btn-login{width:100%;background:linear-gradient(90deg,var(--cyan),var(--indigo));border:none;padding:14px 20px;border-radius:12px;margin-top:12px;cursor:pointer;font-family:'Poppins',sans-serif;font-weight:700;font-size:15px;transition:.2s;color:#0b1120;min-height:50px;}
.btn-login:hover{opacity:.88;transform:scale(1.02);}

/* ══════════════════════════════════════ NFC ══════════════════════════════════════ */
.nfc-wrapper{text-align:center;padding:10px 0;}
.nfc-badge{display:inline-block;padding:6px 14px;border-radius:20px;font-family:'JetBrains Mono',monospace;font-size:12px;font-weight:600;margin-bottom:20px;background:var(--surface);color:var(--muted);border:1px solid var(--surface);transition:.4s;}
.nfc-badge.scanning{background:rgba(0,242,255,0.1);color:var(--cyan);border-color:var(--cyan);}
.nfc-badge.success{background:rgba(0,255,136,0.1);color:var(--ok);border-color:var(--ok);}
.nfc-badge.error{background:rgba(255,77,77,0.1);color:var(--danger);border-color:var(--danger);}
.nfc-rings{position:relative;width:120px;height:120px;margin:0 auto 22px;}
.nfc-ring{position:absolute;border-radius:50%;border:2px solid transparent;}
.nfc-ring:nth-child(1){width:120px;height:120px;top:0;left:0;border-color:rgba(0,242,255,0.15);}
.nfc-ring:nth-child(2){width:88px;height:88px;top:16px;left:16px;border-color:rgba(0,242,255,0.25);}
.nfc-ring:nth-child(3){width:56px;height:56px;top:32px;left:32px;border-color:rgba(0,242,255,0.4);}
.nfc-icon{position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);font-size:26px;}
.nfc-rings.scanning .nfc-ring{animation:ringPulse 1.6s ease-in-out infinite;}
.nfc-rings.scanning .nfc-ring:nth-child(2){animation-delay:.2s;}
.nfc-rings.scanning .nfc-ring:nth-child(3){animation-delay:.4s;}
.nfc-rings.success .nfc-ring{border-color:var(--ok)!important;opacity:.5;}
.nfc-rings.error .nfc-ring{border-color:var(--danger)!important;opacity:.5;}
@keyframes ringPulse{0%,100%{transform:scale(1);opacity:.3;}50%{transform:scale(1.1);opacity:1;}}
.nfc-uid{background:var(--surface);border-radius:10px;padding:10px 14px;font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--muted);margin:12px 0;min-height:36px;word-break:break-all;text-align:center;border:1px solid rgba(255,255,255,0.05);transition:.3s;}
.nfc-uid.found{color:var(--cyan);border-color:rgba(0,242,255,0.3);}
.nfc-info{font-size:11px;color:var(--muted);font-family:'JetBrains Mono',monospace;margin-bottom:14px;line-height:1.7;}
.nfc-info a{color:var(--cyan);text-decoration:none;}
.btn-nfc{background:var(--surface);border:1px solid var(--cyan);color:var(--cyan);padding:11px 24px;border-radius:12px;cursor:pointer;font-family:'Poppins',sans-serif;font-weight:600;font-size:14px;transition:.2s;min-height:46px;width:100%;}
.btn-nfc:hover{background:rgba(0,242,255,0.08);}
.btn-nfc:disabled{opacity:.4;cursor:not-allowed;}

/* ══════════════════════════════════════ DASHBOARD ══════════════════════════════════════ */
#dashboard{animation:fadeIn .5s ease;}
.dash-header{display:flex;justify-content:space-between;align-items:center;padding:14px var(--pad-x);background:#111827;border-bottom:1px solid rgba(0,242,255,0.1);position:sticky;top:0;z-index:200;gap:12px;flex-wrap:wrap;}
.dash-logo{font-weight:700;color:var(--cyan);font-family:'Syne',sans-serif;letter-spacing:1px;font-size:clamp(13px,3.5vw,18px);line-height:1.3;}
.dash-header-right{display:flex;align-items:center;gap:10px;flex-wrap:wrap;}
.dash-logout{background:none;border:1px solid var(--cyan);color:var(--cyan);padding:8px 18px;border-radius:20px;cursor:pointer;font-family:'Poppins',sans-serif;font-weight:600;font-size:13px;transition:.2s;white-space:nowrap;min-height:40px;}
.dash-logout:hover{background:var(--cyan);color:#0b1120;}
.container{padding:24px var(--pad-x);}

/* STAT PILLS */
.stats-strip{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;margin-bottom:24px;}
.stat-pill{background:#141b2d;border-radius:14px;padding:18px 12px;text-align:center;box-shadow:0 0 16px rgba(0,242,255,0.07);}
.stat-pill .num{font-size:clamp(24px,5vw,32px);font-weight:700;font-family:'Syne',sans-serif;}
.stat-pill .lbl{font-size:clamp(10px,2.5vw,12px);opacity:.55;font-family:'Poppins',sans-serif;margin-top:4px;}
.stat-pill.high .num{color:var(--danger);}
.stat-pill.med  .num{color:var(--warn);}
.stat-pill.low  .num{color:var(--ok);}

/* WA CARDS */
.wa-card{background:#141b2d;padding:clamp(18px,4vw,28px);border-radius:var(--radius);margin-bottom:22px;box-shadow:0 0 20px rgba(0,242,255,0.08);}
.wa-card h2{margin-bottom:14px;color:var(--cyan);font-family:'Poppins',sans-serif;font-size:clamp(14px,4vw,17px);font-weight:600;}
.wa-card textarea{width:100%;height:clamp(90px,18vw,120px);padding:14px;border-radius:10px;border:1px solid transparent;background:#0f1626;color:white;font-family:'Poppins',sans-serif;font-size:clamp(13px,3.5vw,14px);resize:vertical;outline:none;transition:.2s;}
.wa-card textarea:focus{border-color:rgba(0,242,255,0.35);}
.btn-scan{margin-top:12px;padding:13px 28px;background:var(--cyan);border:none;border-radius:30px;font-weight:600;cursor:pointer;font-family:'Poppins',sans-serif;font-size:14px;color:#0b1120;transition:.2s;min-height:48px;width:100%;}
.btn-scan:hover{box-shadow:0 0 18px var(--cyan);}
.btn-scan:active{transform:scale(0.98);}
.result-box{margin-top:14px;font-weight:600;font-size:clamp(13px,3.8vw,16px);font-family:'Poppins',sans-serif;line-height:1.5;}
.risk-high{color:var(--danger);}
.risk-medium{color:var(--warn);}
.risk-low{color:var(--ok);}
.scan-bar{height:5px;margin-top:10px;border-radius:4px;overflow:hidden;background:var(--surface);}
.scan-bar-inner{height:100%;width:0;border-radius:4px;background:linear-gradient(90deg,var(--cyan),var(--indigo));transition:width .5s ease;}
.wa-log{font-size:clamp(11px,3vw,13px);line-height:1.9;max-height:180px;overflow-y:auto;background:#0f1626;padding:14px;border-radius:10px;font-family:'JetBrains Mono',monospace;word-break:break-word;}
.wa-card canvas{background:#0f1626;border-radius:10px;padding:10px;width:100%!important;}

/* ══════════════════════════════════════
   AUTO-MONITOR STATUS BAR
══════════════════════════════════════ */
.monitor-bar{
  display:flex;align-items:center;justify-content:space-between;
  background:#0d1a2d;border:1px solid rgba(0,242,255,0.15);
  border-radius:12px;padding:12px 18px;margin-bottom:22px;
  flex-wrap:wrap;gap:10px;
}
.monitor-left{display:flex;align-items:center;gap:12px;flex-wrap:wrap;}
.monitor-dot{
  width:10px;height:10px;border-radius:50%;
  background:#555;flex-shrink:0;transition:.3s;
}
.monitor-dot.active{background:var(--ok);box-shadow:0 0 8px var(--ok);animation:blink 1.4s ease-in-out infinite;}
.monitor-dot.error{background:var(--danger);box-shadow:0 0 8px var(--danger);}
@keyframes blink{0%,100%{opacity:1;}50%{opacity:.3;}}
.monitor-label{font-size:13px;font-family:'JetBrains Mono',monospace;color:var(--muted);}
.monitor-label span{color:var(--cyan);font-weight:600;}
.monitor-right{display:flex;gap:8px;align-items:center;flex-wrap:wrap;}
.btn-monitor{padding:7px 16px;border-radius:20px;border:1px solid;cursor:pointer;font-family:'Poppins',sans-serif;font-size:12px;font-weight:600;transition:.2s;min-height:34px;}
.btn-start{border-color:var(--ok);color:var(--ok);background:rgba(0,255,136,0.06);}
.btn-start:hover{background:rgba(0,255,136,0.15);}
.btn-stop{border-color:var(--danger);color:var(--danger);background:rgba(255,77,77,0.06);}
.btn-stop:hover{background:rgba(255,77,77,0.15);}
.btn-settings{border-color:var(--cyan);color:var(--cyan);background:rgba(0,242,255,0.06);}
.btn-settings:hover{background:rgba(0,242,255,0.14);}
.counter-badge{background:var(--surface);border-radius:8px;padding:4px 10px;font-size:11px;font-family:'JetBrains Mono',monospace;color:var(--muted);}

/* ══════════════════════════════════════
   API SETTINGS PANEL
══════════════════════════════════════ */
.settings-panel{
  background:#0d1a2d;border:1px solid rgba(0,242,255,0.2);
  border-radius:14px;padding:20px;margin-bottom:22px;
  animation:slideDown .3s ease;
}
@keyframes slideDown{from{opacity:0;transform:translateY(-10px);}to{opacity:1;transform:translateY(0);}}
.settings-panel h3{color:var(--cyan);font-size:14px;margin-bottom:16px;font-family:'Poppins',sans-serif;font-weight:600;}
.settings-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;}
.settings-group{display:flex;flex-direction:column;gap:5px;}
.settings-group.full{grid-column:1/-1;}
.settings-label{font-size:11px;color:var(--muted);font-family:'JetBrains Mono',monospace;text-transform:uppercase;letter-spacing:.5px;}
.settings-input{width:100%;padding:10px 12px;background:var(--surface);border:1px solid rgba(0,242,255,0.15);border-radius:8px;color:var(--text);font-family:'JetBrains Mono',monospace;font-size:12px;outline:none;transition:.2s;}
.settings-input:focus{border-color:var(--cyan);}
.settings-select{width:100%;padding:10px 12px;background:var(--surface);border:1px solid rgba(0,242,255,0.15);border-radius:8px;color:var(--text);font-family:'JetBrains Mono',monospace;font-size:12px;outline:none;transition:.2s;}
.settings-actions{display:flex;gap:8px;margin-top:14px;flex-wrap:wrap;}
.btn-save-settings{padding:9px 20px;background:var(--cyan);border:none;border-radius:10px;color:#0b1120;font-family:'Poppins',sans-serif;font-weight:700;font-size:13px;cursor:pointer;transition:.2s;}
.btn-save-settings:hover{opacity:.85;}
.btn-test-api{padding:9px 20px;background:transparent;border:1px solid var(--indigo);border-radius:10px;color:#a5b4fc;font-family:'Poppins',sans-serif;font-weight:600;font-size:13px;cursor:pointer;transition:.2s;}
.btn-test-api:hover{background:rgba(79,70,229,0.2);}
.btn-sim{padding:9px 20px;background:transparent;border:1px solid var(--warn);border-radius:10px;color:var(--warn);font-family:'Poppins',sans-serif;font-weight:600;font-size:13px;cursor:pointer;transition:.2s;}
.btn-sim:hover{background:rgba(255,204,0,0.1);}
.api-status-line{margin-top:12px;font-size:11px;font-family:'JetBrains Mono',monospace;padding:8px 12px;border-radius:8px;background:var(--surface);border:1px solid rgba(255,255,255,0.04);}

/* ══════════════════════════════════════
   DANGER POPUP ALERT
══════════════════════════════════════ */
.popup-overlay{
  position:fixed;inset:0;background:rgba(0,0,0,0.7);
  display:flex;align-items:center;justify-content:center;
  z-index:9999;padding:20px;
  animation:overlayIn .2s ease;
  backdrop-filter:blur(4px);
}
@keyframes overlayIn{from{opacity:0;}to{opacity:1;}}
.popup-box{
  background:#0f172a;border-radius:20px;width:100%;max-width:460px;
  border:1px solid rgba(255,77,77,0.4);
  box-shadow:0 0 60px rgba(255,77,77,0.25),0 20px 60px rgba(0,0,0,0.5);
  animation:popIn .3s cubic-bezier(.34,1.56,.64,1);
  overflow:hidden;
}
@keyframes popIn{from{opacity:0;transform:scale(0.85);}to{opacity:1;transform:scale(1);}}
.popup-header{
  background:linear-gradient(135deg,rgba(255,77,77,0.2),rgba(79,70,229,0.2));
  padding:20px 24px 16px;border-bottom:1px solid rgba(255,77,77,0.2);
  position:relative;
}
.popup-header-row{display:flex;align-items:center;gap:12px;}
.popup-icon{font-size:32px;animation:shake .4s ease;}
@keyframes shake{0%,100%{transform:rotate(0);}25%{transform:rotate(-8deg);}75%{transform:rotate(8deg);}}
.popup-title{font-family:'Syne',sans-serif;font-size:18px;font-weight:800;color:var(--danger);}
.popup-subtitle{font-size:12px;color:var(--muted);font-family:'JetBrains Mono',monospace;margin-top:2px;}
.popup-close{position:absolute;top:16px;right:16px;background:rgba(255,255,255,0.08);border:none;color:var(--muted);width:28px;height:28px;border-radius:50%;cursor:pointer;font-size:14px;display:flex;align-items:center;justify-content:center;transition:.2s;}
.popup-close:hover{background:rgba(255,77,77,0.2);color:var(--danger);}
.popup-body{padding:20px 24px;}
.popup-sender{display:flex;align-items:center;gap:10px;margin-bottom:14px;}
.popup-sender-icon{width:38px;height:38px;border-radius:50%;background:rgba(255,77,77,0.12);border:1px solid rgba(255,77,77,0.3);display:flex;align-items:center;justify-content:center;font-size:18px;flex-shrink:0;}
.popup-sender-info{flex:1;min-width:0;}
.popup-sender-name{font-weight:600;font-size:14px;color:var(--text);}
.popup-sender-time{font-size:11px;color:var(--muted);font-family:'JetBrains Mono',monospace;}
.popup-message-box{
  background:#070d1a;border-radius:12px;padding:14px 16px;
  font-size:13px;line-height:1.7;color:var(--text);
  border:1px solid rgba(255,255,255,0.06);max-height:120px;overflow-y:auto;
  font-family:'Poppins',sans-serif;margin-bottom:14px;word-break:break-word;
}
.popup-risk-badge{
  display:inline-flex;align-items:center;gap:6px;
  padding:6px 14px;border-radius:20px;font-size:12px;font-weight:700;
  margin-bottom:16px;font-family:'JetBrains Mono',monospace;
}
.popup-risk-badge.high{background:rgba(255,77,77,0.15);color:var(--danger);border:1px solid rgba(255,77,77,0.3);}
.popup-risk-badge.medium{background:rgba(255,204,0,0.15);color:var(--warn);border:1px solid rgba(255,204,0,0.3);}
.popup-score{font-size:11px;color:var(--muted);font-family:'JetBrains Mono',monospace;margin-bottom:16px;}
.popup-keywords{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:18px;}
.popup-keyword{background:rgba(255,77,77,0.1);border:1px solid rgba(255,77,77,0.25);color:#fca5a5;padding:3px 10px;border-radius:20px;font-size:11px;font-family:'JetBrains Mono',monospace;}
.popup-actions{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.popup-btn-dismiss{padding:12px;background:var(--surface);border:1px solid rgba(255,255,255,0.1);border-radius:12px;color:var(--muted);font-family:'Poppins',sans-serif;font-weight:600;font-size:13px;cursor:pointer;transition:.2s;min-height:46px;}
.popup-btn-dismiss:hover{background:#1e293b;color:var(--text);}
.popup-btn-block{padding:12px;background:rgba(255,77,77,0.15);border:1px solid rgba(255,77,77,0.3);border-radius:12px;color:var(--danger);font-family:'Poppins',sans-serif;font-weight:700;font-size:13px;cursor:pointer;transition:.2s;min-height:46px;}
.popup-btn-block:hover{background:rgba(255,77,77,0.25);}

/* MEDIUM RISK popup — orange variant */
.popup-box.medium{border-color:rgba(255,204,0,0.4);box-shadow:0 0 60px rgba(255,204,0,0.15),0 20px 60px rgba(0,0,0,0.5);}
.popup-box.medium .popup-header{background:linear-gradient(135deg,rgba(255,204,0,0.15),rgba(79,70,229,0.1));}
.popup-box.medium .popup-header{border-color:rgba(255,204,0,0.2);}
.popup-box.medium .popup-title{color:var(--warn);}

/* TOAST QUEUE (small notifications) */
.toast-container{position:fixed;bottom:24px;right:24px;z-index:8000;display:flex;flex-direction:column;gap:10px;max-width:340px;}
.toast{
  background:#111827;border-radius:12px;padding:14px 16px;
  box-shadow:0 8px 32px rgba(0,0,0,0.4);
  border:1px solid;animation:toastIn .3s ease;
  display:flex;align-items:flex-start;gap:10px;cursor:pointer;
}
.toast:hover{opacity:.85;}
@keyframes toastIn{from{opacity:0;transform:translateX(60px);}to{opacity:1;transform:translateX(0);}}
@keyframes toastOut{from{opacity:1;transform:translateX(0);}to{opacity:0;transform:translateX(60px);}}
.toast.high{border-color:rgba(255,77,77,0.4);}
.toast.medium{border-color:rgba(255,204,0,0.4);}
.toast.low{border-color:rgba(0,255,136,0.3);}
.toast-icon{font-size:20px;flex-shrink:0;margin-top:1px;}
.toast-body{flex:1;min-width:0;}
.toast-title{font-size:13px;font-weight:700;margin-bottom:3px;}
.toast.high .toast-title{color:var(--danger);}
.toast.medium .toast-title{color:var(--warn);}
.toast.low .toast-title{color:var(--ok);}
.toast-msg{font-size:11px;color:var(--muted);font-family:'JetBrains Mono',monospace;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.toast-time{font-size:10px;color:var(--muted);font-family:'JetBrains Mono',monospace;margin-top:4px;}
.toast-close{background:none;border:none;color:var(--muted);cursor:pointer;font-size:14px;flex-shrink:0;padding:0 2px;line-height:1;}

/* ══════════════════════════════════════ ANIMATIONS ══════════════════════════════════════ */
@keyframes fadeIn{from{opacity:0;transform:translateY(8px);}to{opacity:1;transform:translateY(0);}}

/* ══════════════════════════════════════ RESPONSIVE ══════════════════════════════════════ */
@media(max-width:768px){
  :root{--pad-x:20px;}
  .site-header,.dash-header{padding:14px var(--pad-x);}
  .container{padding:18px var(--pad-x);}
  .settings-grid{grid-template-columns:1fr;}
  .toast-container{bottom:16px;right:12px;left:12px;max-width:100%;}
}
@media(max-width:480px){
  :root{--pad-x:14px;}
  .dash-header{flex-wrap:nowrap;}
  .dash-logo{font-size:11px;letter-spacing:0;}
  .dash-logout{padding:7px 10px;font-size:11px;}
  #loginPage{padding:16px;align-items:flex-start;padding-top:50px;}
  .stats-strip{gap:8px;}
  .stat-pill .num{font-size:22px;}
  .stat-pill .lbl{font-size:9px;}
  .popup-box{border-radius:16px;}
  .popup-body{padding:16px;}
  .popup-actions{grid-template-columns:1fr;}
  .nfc-rings{width:100px;height:100px;}
  .nfc-ring:nth-child(1){width:100px;height:100px;}
  .nfc-ring:nth-child(2){width:74px;height:74px;top:13px;left:13px;}
  .nfc-ring:nth-child(3){width:48px;height:48px;top:26px;left:26px;}
  .monitor-bar{flex-direction:column;align-items:flex-start;}
}
@media(min-width:1400px){
  :root{--pad-x:100px;}
}
</style>
</head>
<body>

<!-- ══════════════════════════════════ HOME ══════════════════════════════════ -->
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

<!-- ══════════════════════════════════ LOGIN ══════════════════════════════════ -->
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
        <div id="nfcHint" style="margin-top:10px;font-size:11px;color:var(--muted);font-family:'JetBrains Mono',monospace;"></div>
      </div>
    </div>
  </div>
</section>

<!-- ══════════════════════════════════ DASHBOARD ══════════════════════════════════ -->
<section id="dashboard" class="hidden">
  <div class="dash-header">
    <div class="dash-logo">🛡 WA GUARDIAN AI — SENIORSHIELD</div>
    <div class="dash-header-right">
      <button class="btn-monitor btn-settings" onclick="toggleSettings()">⚙ API Setup</button>
      <button class="dash-logout" onclick="logout()">Logout</button>
    </div>
  </div>

  <div class="container">

    <!-- AUTO-MONITOR STATUS BAR -->
    <div class="monitor-bar">
      <div class="monitor-left">
        <div id="monitorDot" class="monitor-dot"></div>
        <div class="monitor-label" id="monitorLabel">Monitor: <span>Tidak Aktif</span></div>
        <div class="counter-badge" id="msgCounter">0 pesan diperiksa</div>
      </div>
      <div class="monitor-right">
        <button class="btn-monitor btn-start" onclick="startMonitor()">▶ Mulai Monitor</button>
        <button class="btn-monitor btn-stop"  onclick="stopMonitor()" >■ Stop</button>
      </div>
    </div>

    <!-- API SETTINGS PANEL (hidden by default) -->
    <div id="settingsPanel" class="settings-panel hidden">
      <h3>⚙ Konfigurasi API &amp; Auto-Monitor</h3>
      <div class="settings-grid">
        <div class="settings-group">
          <div class="settings-label">Mode Koneksi</div>
          <select class="settings-select" id="connMode" onchange="onConnModeChange()">
            <option value="simulate">🧪 Simulasi (Demo)</option>
            <option value="poll">🔄 HTTP Polling API</option>
            <option value="ws">⚡ WebSocket Real-time</option>
          </select>
        </div>
        <div class="settings-group">
          <div class="settings-label">Interval Polling (detik)</div>
          <input class="settings-input" id="pollInterval" type="number" value="10" min="3" max="300"/>
        </div>
        <div class="settings-group full" id="apiUrlGroup">
          <div class="settings-label">URL API / WebSocket</div>
          <input class="settings-input" id="apiUrl" type="text" placeholder="https://your-server.com/api/sms/latest  atau  ws://your-server.com/ws"/>
        </div>
        <div class="settings-group" id="apiKeyGroup">
          <div class="settings-label">API Key (opsional)</div>
          <input class="settings-input" id="apiKey" type="text" placeholder="Bearer token / API key"/>
        </div>
        <div class="settings-group">
          <div class="settings-label">Risiko Minimum Notifikasi</div>
          <select class="settings-select" id="minRisk">
            <option value="30">Medium & High Risk</option>
            <option value="60">High Risk saja</option>
            <option value="0">Semua pesan</option>
          </select>
        </div>
      </div>

      <!-- INFO BOX: cara integrasi -->
      <div style="margin-top:14px;background:#070d1a;border-radius:10px;padding:14px;font-size:11px;font-family:'JetBrains Mono',monospace;color:var(--muted);line-height:2;border:1px solid rgba(0,242,255,0.08);">
        <div style="color:var(--cyan);font-weight:600;margin-bottom:6px;">📡 Format JSON yang diharapkan dari API:</div>
        <div style="color:#a5f3fc;">[{</div>
        <div style="padding-left:16px;color:var(--text);">
          "id": "msg_001",<br/>
          "sender": "+6281234567890",<br/>
          "body": "isi pesan SMS",<br/>
          "timestamp": "2025-01-01T10:00:00Z"<br/>
        </div>
        <div style="color:#a5f3fc;">}]</div>
        <div style="margin-top:8px;color:var(--muted);">Server harus mengembalikan array pesan baru sejak <code style="color:var(--cyan);">?since=TIMESTAMP</code></div>
      </div>

      <div class="settings-actions">
        <button class="btn-save-settings" onclick="saveSettings()">💾 Simpan & Terapkan</button>
        <button class="btn-test-api"      onclick="testConnection()">🔌 Test Koneksi</button>
        <button class="btn-sim"           onclick="triggerSimulation()">🧪 Kirim Pesan Uji</button>
      </div>
      <div class="api-status-line" id="apiStatusLine">Status: Belum dikonfigurasi</div>
    </div>

    <!-- STAT PILLS -->
    <div class="stats-strip">
      <div class="stat-pill high"><div class="num" id="statHigh">0</div><div class="lbl">⚠ High Risk</div></div>
      <div class="stat-pill med" ><div class="num" id="statMed" >0</div><div class="lbl">⚡ Medium</div></div>
      <div class="stat-pill low" ><div class="num" id="statLow" >0</div><div class="lbl">✓ Low Risk</div></div>
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

  </div>
</section>

<!-- ══════════════════════════════════ POPUP CONTAINER ══════════════════════════════════ -->
<div id="popupContainer"></div>
<!-- TOAST CONTAINER -->
<div class="toast-container" id="toastContainer"></div>

<!-- ══════════════════════════════════════════════════════════════════════════════════
     SCRIPT
══════════════════════════════════════════════════════════════════════════════════ -->
<script>
/* ════════════════════════════════════
   DATABASES
════════════════════════════════════ */
const NFC_DATABASE = [
  {uid:"04:a3:b2:c1",name:"Admin Utama"},
  {uid:"04:12:34:56",name:"Staff Senior 1"},
  {uid:"04:ab:cd:ef",name:"Staff Senior 2"},
];
const USER_DATABASE = [
  {username:"admin",       password:"1234",            name:"Admin"},
  {username:"seniorshield",password:"sahabatselamanya",name:"SeniorShield"},
];
const PHISHING_KEYWORDS = [
  "hadiah","klik link","verifikasi akun","akun diblokir",
  "transfer sekarang","menang undian","gratis saldo",
  "bank","pin","otp","kode verifikasi","whatsapp support",
  "login dari perangkat baru","reset password","data anda",
  "segera","urgent","konfirmasi","perangkat baru","terkena hack",
  "kode rahasia","jangan beritahu","transfer dana","rekening"
];
const SUSPICIOUS_DOMAINS = [".xyz",".top",".click",".gq",".ru",".tk",".cf",".ml",".ga"];

/* SIMULATION MESSAGES — test messages to demo the system */
const SIM_MESSAGES = [
  {sender:"+6281234567890",body:"Selamat! Akun WhatsApp Anda akan diblokir. Klik link ini untuk verifikasi: http://wa-verify.xyz/login123"},
  {sender:"+6289876543210",body:"Halo, kode OTP Anda adalah 482931. Jangan beritahu siapapun. Transfer dana sekarang."},
  {sender:"+6282111222333",body:"Hadiah undian Anda senilai 50 juta sudah siap. Hubungi CS kami segera: http://hadiah-wa.top/klaim"},
  {sender:"+6283444555666",body:"Pesan dari teman: Apa kabar? Kita jadi ketemuan besok kan?"},
  {sender:"Bank Central",   body:"Informasi: Tagihan kartu kredit Anda sudah jatuh tempo. Silakan bayar melalui aplikasi resmi."},
  {sender:"+6285999888777",body:"PIN ATM Anda akan direset karena login dari perangkat baru. Hubungi 1234 untuk konfirmasi."},
  {sender:"WA Support",     body:"Akun WhatsApp Anda akan dihapus dalam 24 jam. Klik link berikut untuk mempertahankan akun: http://whatsapp-support.gq/save"},
  {sender:"+6287666555444",body:"Mama, ini aku. Nomor baru. Tolong transfer dulu ke rekening ini ya, nanti aku ganti."},
];
let simIndex = 0;

/* ════════════════════════════════════
   STATE
════════════════════════════════════ */
let highCount=0, mediumCount=0, lowCount=0, totalScanned=0;
let monitorInterval=null, wsConn=null;
let seenMessageIds=new Set();
let cfg = {
  mode:"simulate",
  url:"",
  key:"",
  interval:10,
  minRisk:30,
};

/* ════════════════════════════════════
   NAVIGATION
════════════════════════════════════ */
function showLogin(){ document.getElementById("homePage").classList.add("hidden"); document.getElementById("loginPage").classList.remove("hidden"); }
function showDashboard(){ document.getElementById("loginPage").classList.add("hidden"); document.getElementById("dashboard").classList.remove("hidden"); loadLogs(); }
function showTab(tabId,btn){ document.querySelectorAll(".tab-btn").forEach(b=>b.classList.remove("active")); document.getElementById("tabPassword").classList.add("hidden"); document.getElementById("tabNFC").classList.add("hidden"); document.getElementById(tabId).classList.remove("hidden"); btn.classList.add("active"); }
function logout(){ stopMonitor(); if(wsConn) wsConn.close(); location.reload(); }

/* ════════════════════════════════════
   LOGIN
════════════════════════════════════ */
function login(){
  const u=document.getElementById("user").value.trim();
  const p=document.getElementById("pass").value;
  if(USER_DATABASE.find(x=>x.username===u&&x.password===p)){ showDashboard(); }
  else{ alert("Username atau password salah."); }
}
document.addEventListener("DOMContentLoaded",()=>{
  ["user","pass"].forEach(id=>{ document.getElementById(id).addEventListener("keydown",e=>{if(e.key==="Enter")login();}); });
});

/* ════════════════════════════════════
   NFC
════════════════════════════════════ */
let nfcAbortCtrl=null;
async function startNFCScan(){
  const btn=document.getElementById("nfcScanBtn"),badge=document.getElementById("nfcBadge"),uid=document.getElementById("nfcUID"),hint=document.getElementById("nfcHint");
  if(!("NDEFReader" in window)){ setNFCState("error"); badge.textContent="● NFC Tidak Didukung"; uid.textContent="Gunakan Chrome 89+ di Android."; return; }
  try{
    btn.disabled=true; btn.textContent="Scanning..."; setNFCState("scanning"); badge.textContent="● SCANNING..."; uid.textContent="Menunggu kartu NFC..."; uid.classList.remove("found"); hint.textContent="Tempelkan kartu NFC ke ponsel";
    nfcAbortCtrl=new AbortController();
    const reader=new NDEFReader();
    await reader.scan({signal:nfcAbortCtrl.signal});
    reader.addEventListener("reading",({serialNumber})=>handleNFCRead(serialNumber));
    reader.addEventListener("readingerror",()=>{ setNFCState("error"); badge.textContent="● Error Membaca"; uid.textContent="Gagal membaca."; resetNFCBtn(); });
  }catch(err){
    if(err.name==="NotAllowedError"){badge.textContent="● Izin Ditolak"; uid.textContent="Aktifkan izin NFC.";}
    else if(err.name==="AbortError"){badge.textContent="● Dibatalkan"; uid.textContent="Scan dibatalkan.";}
    else{badge.textContent="● Error"; uid.textContent=err.message;}
    setNFCState("error"); hint.textContent=""; resetNFCBtn();
  }
}
function handleNFCRead(rawUID){
  const badge=document.getElementById("nfcBadge"),uid=document.getElementById("nfcUID"),hint=document.getElementById("nfcHint");
  uid.textContent="UID: "+rawUID.toUpperCase(); uid.classList.add("found");
  const match=NFC_DATABASE.find(e=>e.uid.toLowerCase()===rawUID.toLowerCase());
  if(match){ setNFCState("success"); badge.textContent="✓ TERVERIFIKASI"; hint.textContent="Selamat datang, "+match.name+"!"; if(nfcAbortCtrl)nfcAbortCtrl.abort(); setTimeout(()=>showDashboard(),1200); }
  else{ setNFCState("error"); badge.textContent="✗ TIDAK DIKENAL"; hint.textContent="Kartu tidak terdaftar."; if(nfcAbortCtrl)nfcAbortCtrl.abort(); resetNFCBtn(2800); }
}
function setNFCState(s){ document.getElementById("nfcRings").className="nfc-rings"+(s?" "+s:""); document.getElementById("nfcBadge").className="nfc-badge"+(s?" "+s:""); }
function resetNFCBtn(d=0){ setTimeout(()=>{ const b=document.getElementById("nfcScanBtn"); if(b){b.disabled=false;b.textContent="Mulai Scan NFC";} },d); }

/* ════════════════════════════════════
   SETTINGS PANEL
════════════════════════════════════ */
function toggleSettings(){
  const p=document.getElementById("settingsPanel");
  p.classList.toggle("hidden");
}
function onConnModeChange(){
  const mode=document.getElementById("connMode").value;
  const show=(mode!=="simulate");
  document.getElementById("apiUrlGroup").style.opacity=show?"1":"0.4";
  document.getElementById("apiKeyGroup").style.opacity=show?"1":"0.4";
}
function saveSettings(){
  cfg.mode     = document.getElementById("connMode").value;
  cfg.url      = document.getElementById("apiUrl").value.trim();
  cfg.key      = document.getElementById("apiKey").value.trim();
  cfg.interval = parseInt(document.getElementById("pollInterval").value)||10;
  cfg.minRisk  = parseInt(document.getElementById("minRisk").value)||30;
  setApiStatus("✅ Pengaturan disimpan. Mode: "+cfg.mode);
  document.getElementById("settingsPanel").classList.add("hidden");
}
function setApiStatus(msg){ document.getElementById("apiStatusLine").textContent="Status: "+msg; }

async function testConnection(){
  if(cfg.mode==="simulate"){ setApiStatus("🧪 Mode simulasi aktif - tidak perlu koneksi real"); return; }
  if(!cfg.url){ setApiStatus("❌ URL API belum diisi"); return; }
  setApiStatus("🔄 Menghubungkan ke "+cfg.url+" ...");
  try{
    const headers={"Content-Type":"application/json"};
    if(cfg.key) headers["Authorization"]="Bearer "+cfg.key;
    const res=await fetch(cfg.url+"?test=1",{method:"GET",headers,signal:AbortSignal.timeout(5000)});
    if(res.ok){ setApiStatus("✅ Koneksi berhasil! Status: "+res.status); }
    else{ setApiStatus("⚠ Server merespons dengan status: "+res.status); }
  }catch(err){ setApiStatus("❌ Koneksi gagal: "+err.message); }
}

/* ════════════════════════════════════
   AUTO MONITOR — START / STOP
════════════════════════════════════ */
function startMonitor(){
  if(monitorInterval||wsConn){ showToast("Monitor sudah berjalan","",null,"low"); return; }
  saveSettings(); // apply current settings
  const dot=document.getElementById("monitorDot");
  const lbl=document.getElementById("monitorLabel");

  if(cfg.mode==="simulate"){
    dot.classList.add("active");
    lbl.innerHTML='Monitor: <span style="color:var(--ok)">AKTIF — Simulasi</span>';
    monitorInterval=setInterval(()=>fetchAndScan_Simulate(),cfg.interval*1000);
    showToast("Monitor Aktif","Mode simulasi berjalan setiap "+cfg.interval+"s","simulate","low");

  }else if(cfg.mode==="poll"){
    if(!cfg.url){ setApiStatus("❌ URL API harus diisi untuk mode polling"); return; }
    dot.classList.add("active");
    lbl.innerHTML='Monitor: <span style="color:var(--ok)">AKTIF — HTTP Polling</span>';
    monitorInterval=setInterval(()=>fetchAndScan_HTTP(),cfg.interval*1000);
    showToast("Monitor Aktif","Polling API setiap "+cfg.interval+"s","api","low");

  }else if(cfg.mode==="ws"){
    if(!cfg.url){ setApiStatus("❌ URL WebSocket harus diisi"); return; }
    connectWebSocket();
  }
}

function stopMonitor(){
  if(monitorInterval){ clearInterval(monitorInterval); monitorInterval=null; }
  if(wsConn){ wsConn.close(); wsConn=null; }
  const dot=document.getElementById("monitorDot");
  dot.classList.remove("active","error");
  document.getElementById("monitorLabel").innerHTML='Monitor: <span>Tidak Aktif</span>';
  showToast("Monitor Dihentikan","Auto-deteksi dimatikan","","low");
}

/* ════════════════════════════════════
   FETCH SIMULATE — demo mode
════════════════════════════════════ */
function fetchAndScan_Simulate(){
  const msg=SIM_MESSAGES[simIndex % SIM_MESSAGES.length];
  simIndex++;
  const smsObj={id:"sim_"+simIndex, sender:msg.sender, body:msg.body, timestamp:new Date().toISOString()};
  processIncomingMessage(smsObj);
}

/* ════════════════════════════════════
   FETCH HTTP POLLING
════════════════════════════════════ */
let lastFetchTime=new Date().toISOString();
async function fetchAndScan_HTTP(){
  try{
    const headers={"Content-Type":"application/json"};
    if(cfg.key) headers["Authorization"]="Bearer "+cfg.key;
    const url=cfg.url+(cfg.url.includes("?")?"&":"?")+"since="+encodeURIComponent(lastFetchTime);
    const res=await fetch(url,{headers,signal:AbortSignal.timeout(8000)});
    if(!res.ok) throw new Error("HTTP "+res.status);
    const data=await res.json();
    lastFetchTime=new Date().toISOString();
    if(Array.isArray(data)){
      data.forEach(msg=>{ if(!seenMessageIds.has(msg.id)){ seenMessageIds.add(msg.id); processIncomingMessage(msg); } });
    }
    setApiStatus("✅ Last poll: "+new Date().toLocaleTimeString()+" | "+( Array.isArray(data)?data.length:0)+" pesan");
  }catch(err){
    setApiStatus("❌ Poll gagal: "+err.message);
    document.getElementById("monitorDot").className="monitor-dot error";
  }
}

/* ════════════════════════════════════
   WEBSOCKET
════════════════════════════════════ */
function connectWebSocket(){
  const dot=document.getElementById("monitorDot");
  const lbl=document.getElementById("monitorLabel");
  try{
    wsConn=new WebSocket(cfg.url+(cfg.key?"?token="+cfg.key:""));
    wsConn.onopen=()=>{
      dot.classList.add("active");
      lbl.innerHTML='Monitor: <span style="color:var(--ok)">AKTIF — WebSocket</span>';
      setApiStatus("✅ WebSocket terhubung: "+cfg.url);
      showToast("WebSocket Terhubung","Real-time monitoring aktif","ws","low");
    };
    wsConn.onmessage=(event)=>{
      try{
        const data=JSON.parse(event.data);
        const msgs=Array.isArray(data)?data:[data];
        msgs.forEach(msg=>{ if(!seenMessageIds.has(msg.id)){ seenMessageIds.add(msg.id); processIncomingMessage(msg); } });
      }catch(e){}
    };
    wsConn.onerror=()=>{ dot.className="monitor-dot error"; setApiStatus("❌ WebSocket error"); };
    wsConn.onclose=()=>{ dot.classList.remove("active","error"); lbl.innerHTML='Monitor: <span>WebSocket Terputus</span>'; wsConn=null; };
  }catch(err){ setApiStatus("❌ WebSocket gagal: "+err.message); }
}

/* ════════════════════════════════════
   PROCESS INCOMING MESSAGE
════════════════════════════════════ */
function processIncomingMessage(smsObj){
  const {id, sender, body, timestamp} = smsObj;
  const result = analyzeText(body);
  totalScanned++;
  document.getElementById("msgCounter").textContent=totalScanned+" pesan diperiksa";

  // Only alert/popup above configured threshold
  if(result.score >= cfg.minRisk){
    const riskLevel = result.score>=60?"high":"medium";
    showDangerPopup({sender, body, score:result.score, status:result.status, keywords:result.foundKeywords, riskLevel, timestamp});
    showToast(result.status, body, riskLevel, riskLevel);
    notifyBrowser(sender, result.status);
    if(result.score>=60){ highCount++; } else{ mediumCount++; }
  }else{
    lowCount++;
    if(result.score>=0) showToast("Pesan Aman","Dari: "+sender,"low","low");
  }

  addLog("[AUTO] "+sender+" → "+result.status, result.score>=60?"#ff4d4d":result.score>=30?"#ffcc00":"#00ff88");
  updateChart();
}

/* ════════════════════════════════════
   MANUAL SCAN
════════════════════════════════════ */
function scanText(bodyOverride=null, senderOverride=null, manual=false){
  const text=bodyOverride||document.getElementById("inputText").value;
  if(!text.trim()) return;
  const result=analyzeText(text);

  if(manual){
    const bar=document.getElementById("scanBar");
    bar.style.width="0";
    setTimeout(()=>{ bar.style.width=Math.min(result.score,100)+"%"; },50);
    const rb=document.getElementById("resultBox");
    const cls=result.score>=60?"result-box risk-high":result.score>=30?"result-box risk-medium":"result-box risk-low";
    rb.className=cls;
    rb.innerHTML="Skor Risiko: <strong>"+result.score+"</strong> → "+result.status;
    if(result.score>=60){ highCount++; notifyBrowser("Manual Scan",result.status); showDangerPopup({sender:"Manual Scan",body:text,score:result.score,status:result.status,keywords:result.foundKeywords,riskLevel:"high",timestamp:new Date().toISOString()}); }
    else if(result.score>=30){ mediumCount++; }
    else{ lowCount++; }
    addLog("[MANUAL] "+result.status, result.score>=60?"#ff4d4d":result.score>=30?"#ffcc00":"#00ff88");
    updateChart();
    saveLog(result.status);
  }
  return result;
}

/* ════════════════════════════════════
   ANALYZE TEXT — core engine
════════════════════════════════════ */
function analyzeText(text){
  const t=text.toLowerCase();
  let score=0;
  const foundKeywords=[];

  PHISHING_KEYWORDS.forEach(kw=>{ if(t.includes(kw)){ score+=15; foundKeywords.push(kw); } });
  SUSPICIOUS_DOMAINS.forEach(d=>{ if(t.includes(d)){ score+=25; foundKeywords.push(d); } });
  if(t.match(/https?:\/\//))                    score+=20;
  if(t.match(/\d{4,6}/)&&t.includes("otp"))     score+=30;
  else if(t.match(/\d{4,6}/))                   score+=10;

  let status;
  if(score>=60) status="HIGH RISK — Kemungkinan Phishing / Hack WA!";
  else if(score>=30) status="MEDIUM RISK — Perlu waspada.";
  else status="LOW RISK — Pesan aman.";

  return {score, status, foundKeywords:[...new Set(foundKeywords)]};
}

/* ════════════════════════════════════
   TRIGGER SIMULATION (manual test)
════════════════════════════════════ */
function triggerSimulation(){
  fetchAndScan_Simulate();
  setApiStatus("🧪 Pesan uji dikirim: "+new Date().toLocaleTimeString());
}

/* ════════════════════════════════════
   DANGER POPUP
════════════════════════════════════ */
function showDangerPopup({sender,body,score,status,keywords,riskLevel,timestamp}){
  const id="popup_"+Date.now();
  const time=timestamp?new Date(timestamp).toLocaleTimeString():new Date().toLocaleTimeString();

  const kw=keywords.map(k=>`<span class="popup-keyword">${k}</span>`).join("");

  const html=`
  <div class="popup-overlay" id="${id}" onclick="closePopupOutside(event,'${id}')">
    <div class="popup-box ${riskLevel}">
      <div class="popup-header">
        <div class="popup-header-row">
          <span class="popup-icon">${riskLevel==="high"?"🚨":"⚠️"}</span>
          <div>
            <div class="popup-title">${riskLevel==="high"?"ANCAMAN TERDETEKSI":"PESAN MENCURIGAKAN"}</div>
            <div class="popup-subtitle">SeniorShield AI Alert</div>
          </div>
        </div>
        <button class="popup-close" onclick="closePopup('${id}')">✕</button>
      </div>
      <div class="popup-body">
        <div class="popup-sender">
          <div class="popup-sender-icon">📱</div>
          <div class="popup-sender-info">
            <div class="popup-sender-name">${escHtml(sender)}</div>
            <div class="popup-sender-time">${time}</div>
          </div>
        </div>
        <div class="popup-message-box">${escHtml(body)}</div>
        <div class="popup-risk-badge ${riskLevel}">
          ${riskLevel==="high"?"🔴 HIGH RISK":"🟡 MEDIUM RISK"}
        </div>
        <div class="popup-score">Skor Ancaman: ${score} / 100+</div>
        ${kw?`<div class="popup-keywords">${kw}</div>`:""}
        <div class="popup-actions">
          <button class="popup-btn-dismiss" onclick="closePopup('${id}')">✓ Mengerti</button>
          <button class="popup-btn-block"   onclick="blockAndClose('${id}','${escHtml(sender)}')">🚫 Blokir Pengirim</button>
        </div>
      </div>
    </div>
  </div>`;

  document.getElementById("popupContainer").insertAdjacentHTML("beforeend",html);
}

function closePopup(id){
  const el=document.getElementById(id);
  if(el){ el.style.animation="overlayIn .2s ease reverse"; setTimeout(()=>el.remove(),200); }
}
function closePopupOutside(e,id){ if(e.target.id===id) closePopup(id); }
function blockAndClose(id,sender){
  closePopup(id);
  addLog("[BLOKIR] Pengirim "+sender+" ditandai sebagai berbahaya","#ff4d4d");
  showToast("Pengirim Diblokir",sender+" ditandai berbahaya","block","high");
}

/* ════════════════════════════════════
   TOAST
════════════════════════════════════ */
function showToast(title,msg,type,level){
  const icon=level==="high"?"🚨":level==="medium"?"⚠️":"✅";
  const id="toast_"+Date.now();
  const time=new Date().toLocaleTimeString();
  const html=`
  <div class="toast ${level}" id="${id}" onclick="removeToast('${id}')">
    <span class="toast-icon">${icon}</span>
    <div class="toast-body">
      <div class="toast-title">${escHtml(title)}</div>
      <div class="toast-msg">${escHtml(msg.substring(0,60)+(msg.length>60?"...":""))}</div>
      <div class="toast-time">${time}</div>
    </div>
    <button class="toast-close" onclick="removeToast('${id}')">✕</button>
  </div>`;
  document.getElementById("toastContainer").insertAdjacentHTML("beforeend",html);
  setTimeout(()=>removeToast(id),6000);
}
function removeToast(id){
  const el=document.getElementById(id);
  if(el){ el.style.animation="toastOut .3s ease forwards"; setTimeout(()=>el.remove(),300); }
}

/* ════════════════════════════════════
   CHART
════════════════════════════════════ */
const attackChart=new Chart(document.getElementById("attackChart").getContext("2d"),{
  type:"bar",
  data:{
    labels:["High Risk","Medium Risk","Low Risk"],
    datasets:[{label:"Jumlah Deteksi",data:[0,0,0],backgroundColor:["rgba(255,77,77,.75)","rgba(255,204,0,.75)","rgba(0,255,136,.75)"],borderColor:["#ff4d4d","#ffcc00","#00ff88"],borderWidth:1,borderRadius:6}]
  },
  options:{responsive:true,maintainAspectRatio:true,plugins:{legend:{labels:{color:"white",font:{family:"Poppins",size:12}}}},scales:{x:{ticks:{color:"white",font:{size:11}},grid:{color:"rgba(255,255,255,0.04)"}},y:{ticks:{color:"white",font:{size:11}},grid:{color:"rgba(255,255,255,0.04)"},beginAtZero:true}}}
});
function updateChart(){
  attackChart.data.datasets[0].data=[highCount,mediumCount,lowCount];
  attackChart.update();
  document.getElementById("statHigh").textContent=highCount;
  document.getElementById("statMed").textContent=mediumCount;
  document.getElementById("statLow").textContent=lowCount;
}

/* ════════════════════════════════════
   LOG SYSTEM
════════════════════════════════════ */
function addLog(msg,color){
  const time=new Date().toLocaleTimeString();
  const logBox=document.getElementById("logBox");
  const c=color||(msg.includes("HIGH")?"#ff4d4d":msg.includes("MEDIUM")?"#ffcc00":"#00ff88");
  logBox.innerHTML+=`<span style="color:${c}">[${time}] ${msg}</span><br/>`;
  logBox.scrollTop=logBox.scrollHeight;
}
function saveLog(msg){ try{ const logs=JSON.parse(localStorage.getItem("ss_logs"))||[]; logs.push({time:new Date().toLocaleTimeString(),msg}); if(logs.length>200)logs.shift(); localStorage.setItem("ss_logs",JSON.stringify(logs)); }catch(e){} }
function loadLogs(){ try{ const logs=JSON.parse(localStorage.getItem("ss_logs"))||[]; if(!logs.length)return; document.getElementById("logBox").innerHTML=""; logs.forEach(l=>addLog(l.msg)); }catch(e){} }

/* ════════════════════════════════════
   BROWSER NOTIFICATION
════════════════════════════════════ */
function notifyBrowser(sender,status){
  if(Notification.permission==="granted"){ new Notification("⚠ SeniorShield Alert",{body:sender+"\n"+status,icon:"data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🛡</text></svg>"}); }
  else if(Notification.permission!=="denied"){ Notification.requestPermission(); }
}

/* ════════════════════════════════════
   UTILS
════════════════════════════════════ */
function escHtml(s){ return String(s).replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;").replace(/"/g,"&quot;"); }
</script>
</body>
</html>
