<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>SeniorShield NFC Login</title>
<style>
* {margin:0;padding:0;box-sizing:border-box;font-family:'Inter',sans-serif;}
body {background:#0b1120;color:white;}
.hidden {display:none;}
</style>
</head>
<body>

<!-- Halaman NFC Login -->
<div id="nfc-login">
<header style="display:flex;justify-content:space-between;align-items:center;padding:20px;background:#0f172a;">
<div style="color:#00f2ff;font-weight:700;">NFC Login</div>
</header>
<div style="padding:20px;text-align:center;">
<p>Silakan tap kartu NFC Anda untuk login otomatis.</p>
<button id="startNFC" style="padding:10px 20px;border:none;border-radius:8px;background:#00f2ff;font-weight:600;cursor:pointer;">Aktifkan NFC</button>
</div>
</div>

<!-- Halaman utama setelah login NFC -->
<div id="main-content" style="display:none;">
<!-- Isi halaman utama akan diganti dengan kode berikut -->
</div>

<script>
// Fungsi untuk mengganti halaman utama setelah NFC cocok
function loadNFCPage() {
  document.getElementById('nfc-login').style.display = 'none';
  document.getElementById('main-content').style.display = 'block';
  // Ganti isi main-content dengan halaman baru
  document.getElementById('main-content').innerHTML = `
  <header style="display:flex;justify-content:space-between;align-items:center;padding:20px;background:#111827;">
    <div style="font-weight:700;font-size:22px;color:#00f2ff;">WA GUARDIAN AI</div>
  </header>
  <div style="padding:40px 60px;">
    <div class="card" style="background:#141b2d;padding:30px;border-radius:15px;margin-bottom:30px;">
      <h2 style="margin-bottom:20px;color:#00f2ff;">Scan SMS / WhatsApp Text</h2>
      <textarea id="inputText" placeholder="Tempel pesan mencurigakan di sini..." style="width:100%;height:120px;padding:15px;border-radius:10px;border:none;background:#0f1626;color:white;"></textarea>
      <button onclick="scanText()" style="margin-top:15px;padding:12px 25px;background:#00f2ff;border:none;border-radius:30px;font-weight:600;cursor:pointer;">Scan Sekarang</button>
      <div id="result" class="result" style="margin-top:20px;font-weight:600;font-size:18px;"></div>
    </div>
    <div class="card" style="background:#141b2d;padding:30px;border-radius:15px;margin-bottom:30px;">
      <h2 style="margin-bottom:20px;color:#00f2ff;">Statistik Deteksi</h2>
      <canvas id="attackChart"></canvas>
    </div>
    <div class="card" style="background:#141b2d;padding:30px;border-radius:15px;margin-bottom:30px;">
      <h2 style="margin-bottom:20px;color:#00f2ff;">Log Aktivitas</h2>
      <div class="log" id="logBox" style="font-size:13px;line-height:1.6;color:#00ff99;max-height:150px;overflow:auto;background:#0f1626;padding:10px;border-radius:10px;"></div>
    </div>
  </div>
  `;

  // Inisialisasi chart dan fungsi lainnya
  initPage();
}

// Fungsi inisialisasi halaman utama
function initPage() {
  // Buat chart
  const ctx = document.getElementById('attackChart').getContext('2d');
  window.attackChart = new Chart(ctx,{
    type:'bar',
    data:{
      labels:['High Risk','Medium Risk','Low Risk'],
      datasets:[{
        label:'Detections',
        data:[0,0,0],
        backgroundColor:['#ff4d4d','#ffcc00','#00ff88']
      }]
    },
    options:{
      plugins:{legend:{labels:{color:'white'}}},
      scales:{
        x:{ticks:{color:'white'}},
        y:{ticks:{color:'white'}}
      }
    }
  });
  // Reset counts
  window.highCount=0; window.mediumCount=0; window.lowCount=0;
  // Load logs dari local storage
  loadLogs();
}

// Fungsi NFC
const databaseSerials = {
  "07:C9:44:2A": true
  // Tambah serial lain jika perlu
};

document.getElementById('startNFC').onclick = () => {
  startNFC();
};

async function startNFC() {
  if ('NDEFReader' in window) {
    try {
      const ndef = new NDEFReader();
      await ndef.scan();
      alert('Silakan tap kartu NFC...');
      ndef.onreading = event => {
        const serialNumber = event.serialNumber;
        alert('NFC Detected: ' + serialNumber);
        checkNFC(serialNumber);
      };
    } catch (error) {
      console.log('Error saat scan NFC:', error);
      alert('Gagal mengaktifkan NFC: ' + error);
    }
  } else {
    alert('Web NFC tidak didukung browser ini.');
  }
}

function checkNFC(serialNumber) {
  const matched = !!databaseSerials[serialNumber];
  if (matched) {
    alert('Serial cocok, otomatis login!');
    loadNFCPage();
  } else {
    alert('Serial tidak cocok!');
  }
}

// Fungsi untuk memindahkan ke halaman baru
function loadNFCPage() {
  document.getElementById('nfc-login').style.display = 'none';
  document.getElementById('main-content').style.display = 'block';
  document.getElementById('main-content').innerHTML = `
  <header style="display:flex;justify-content:space-between;align-items:center;padding:20px;background:#111827;">
    <div style="font-weight:700;font-size:22px;color:#00f2ff;">WA GUARDIAN AI</div>
  </header>
  <div style="padding:40px 60px;">
    <div class="card" style="background:#141b2d;padding:30px;border-radius:15px;margin-bottom:30px;">
      <h2 style="margin-bottom:20px;color:#00f2ff;">Scan SMS / WhatsApp Text</h2>
      <textarea id="inputText" placeholder="Tempel pesan mencurigakan di sini..." style="width:100%;height:120px;padding:15px;border-radius:10px;border:none;background:#0f1626;color:white;"></textarea>
      <button onclick="scanText()" style="margin-top:15px;padding:12px 25px;background:#00f2ff;border:none;border-radius:30px;font-weight:600;cursor:pointer;">Scan Sekarang</button>
      <div id="result" class="result" style="margin-top:20px;font-weight:600;font-size:18px;"></div>
    </div>
    <div class="card" style="background:#141b2d;padding:30px;border-radius:15px;margin-bottom:30px;">
      <h2 style="margin-bottom:20px;color:#00f2ff;">Statistik Deteksi</h2>
      <canvas id="attackChart"></canvas>
    </div>
    <div class="card" style="background:#141b2d;padding:30px;border-radius:15px;margin-bottom:30px;">
      <h2 style="margin-bottom:20px;color:#00f2ff;">Log Aktivitas</h2>
      <div class="log" id="logBox" style="font-size:13px;line-height:1.6;color:#00ff99;max-height:150px;overflow:auto;background:#0f1626;padding:10px;border-radius:10px;"></div>
    </div>
  </div>
  `;
  initPage();
}

// Fungsi scan text
function scanText() {
  let text = document.getElementById("inputText").value.toLowerCase();
  let score = 0;
  const keywords=["hadiah","klik link","verifikasi akun","akun diblokir",
  "transfer sekarang","menang undian","gratis saldo",
  "bank","pin","otp","kode verifikasi","whatsapp support",
  "login dari perangkat baru","reset password","data anda"];

  const domains=[".xyz",".top",".click",".gq",".ru",".tk"];

  keywords.forEach(k => { if (text.includes(k)) score+=15; });
  domains.forEach(d => { if (text.includes(d)) score+=25; });
  if (text.match(/http[s]?:\/\//)) score+=20;
  if (text.match(/\d{4,6}/) && text.includes("otp")) score+=30;

  let status="", className="";
  if (score>=60) {
    status="HIGH RISK - Kemungkinan Phishing / Hack WA!";
    className="risk-high";
    window.highCount++; notifyUser("⚠️ HIGH RISK terdeteksi!");
  } else if (score>=30) {
    status="MEDIUM RISK - Perlu waspada.";
    className="risk-medium";
    window.mediumCount++;
  } else {
    status="LOW RISK - Aman.";
    className="risk-low";
    window.lowCount++;
  }

  document.getElementById("result").innerHTML="Skor Risiko: "+score+" → "+status;
  document.getElementById("result").className="result "+className;
  updateChart();
  addLog(status);
  saveLog(status);
}

function updateChart() {
  attackChart.data.datasets[0].data = [window.highCount, window.mediumCount, window.lowCount];
  attackChart.update();
}

function addLog(msg) {
  let time = new Date().toLocaleTimeString();
  let box=document.getElementById("logBox");
  box.innerHTML += "["+time+"] "+msg+"<br>";
  box.scrollTop=box.scrollHeight;
}

function saveLog(msg) {
  let logs = JSON.parse(localStorage.getItem("logs")) || [];
  logs.push({time:new Date().toLocaleTimeString(), msg:msg});
  localStorage.setItem("logs",JSON.stringify(logs));
}

function loadLogs() {
  let logs = JSON.parse(localStorage.getItem("logs")) || [];
  logs.forEach(log => {
    addLog(log.msg);
  });
}

// Notification
function notifyUser(msg) {
  if(Notification.permission !== "granted") {
    Notification.requestPermission();
  } else {
    new Notification("WA Guardian Alert",{body:msg});
  }
}
</script>
</body>
</html>
