<html lang="bn" data-theme="light">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>নির্মাণ হিসাব v4.0 — Bangladesh Construction Estimator</title>
<link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
/* ===== THEME ===== */
[data-theme="light"] {
  --bg: #f0f4f1; --bg-card: #ffffff; --bg-sidebar: #0f3d22;
  --bg-input: #f5f7f5; --text: #1a2e20; --text-muted: #5a7060;
  --border: #d0dcd4; --border-light: #e8f0ea;
  --sidebar-text: #b8d4be; --sidebar-active: rgba(255,255,255,0.12);
}
[data-theme="dark"] {
  --bg: #0d1f13; --bg-card: #162a1c; --bg-sidebar: #071209;
  --bg-input: #1e3325; --text: #d4f0dc; --text-muted: #7aab85;
  --border: #2a4a32; --border-light: #1e3325;
  --sidebar-text: #7aab85; --sidebar-active: rgba(255,255,255,0.08);
}
:root {
  --primary: #1a6b3a; --primary-light: #2d9653; --primary-dark: #0f4526;
  --accent: #e8a020; --accent-dark: #c47d0a;
  --success: #22c55e; --warning: #f59e0b; --danger: #ef4444; --info: #3b82f6;
  --shadow: 0 2px 12px rgba(0,0,0,0.08); --shadow-lg: 0 8px 32px rgba(0,0,0,0.14);
  --radius: 12px; --radius-sm: 8px;
}
* { box-sizing: border-box; margin: 0; padding: 0; transition: background-color 0.2s, color 0.2s; }
body { font-family: 'Hind Siliguri', sans-serif; background: var(--bg); color: var(--text); min-height: 100vh; }

/* Layout */
.app { display: flex; min-height: 100vh; }
.sidebar { width: 260px; background: var(--bg-sidebar); color: var(--sidebar-text); flex-shrink: 0; display: flex; flex-direction: column; position: sticky; top: 0; height: 100vh; overflow-y: auto; }
.main { flex: 1; overflow-x: hidden; }

/* Sidebar */
.logo { padding: 20px 20px 14px; border-bottom: 1px solid rgba(255,255,255,0.1); }
.logo-title { font-size: 17px; font-weight: 700; color: #fff; }
.logo-sub { font-size: 10px; color: #6b9e77; margin-top: 2px; }
.nav { padding: 10px 0; flex: 1; }
.nav-item { display: flex; align-items: center; gap: 10px; padding: 10px 18px; cursor: pointer; border-left: 3px solid transparent; font-size: 13px; color: var(--sidebar-text); transition: all 0.15s; }
.nav-item:hover { background: rgba(255,255,255,0.06); color: #fff; }
.nav-item.active { background: var(--sidebar-active); border-left-color: var(--accent); color: #fff; font-weight: 600; }
.nav-section { padding: 10px 18px 4px; font-size: 10px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.08em; color: #4a7a55; }
.nav-badge { margin-left: auto; background: var(--accent); color: #fff; font-size: 9px; padding: 1px 6px; border-radius: 10px; font-weight: 700; }
.sidebar-footer { padding: 12px 18px; border-top: 1px solid rgba(255,255,255,0.08); font-size: 11px; color: #4a7a55; }

/* Header */
.header { background: var(--bg-card); border-bottom: 1px solid var(--border); padding: 14px 24px; display: flex; align-items: center; justify-content: space-between; position: sticky; top: 0; z-index: 100; }
.header-left h1 { font-size: 18px; font-weight: 700; color: var(--primary-dark); }
.header-left p { font-size: 12px; color: var(--text-muted); }
.header-right { display: flex; gap: 8px; align-items: center; flex-wrap: wrap; }
.btn { padding: 7px 14px; border-radius: var(--radius-sm); border: none; cursor: pointer; font-family: inherit; font-size: 12px; font-weight: 600; transition: all 0.2s; display: inline-flex; align-items: center; gap: 5px; }
.btn-primary { background: var(--primary); color: #fff; }
.btn-primary:hover { background: var(--primary-light); }
.btn-accent { background: var(--accent); color: #fff; }
.btn-outline { background: transparent; color: var(--primary); border: 1.5px solid var(--primary); }
.btn-outline:hover { background: var(--primary); color: #fff; }
.btn-sm { padding: 5px 10px; font-size: 11px; }
.btn-danger { background: var(--danger); color: #fff; }
.btn-info { background: var(--info); color: #fff; }

/* Summary bar */
.summary-bar { display: grid; grid-template-columns: repeat(5, 1fr); gap: 12px; padding: 16px 24px 0; }
.stat-card { background: var(--bg-card); border: 1px solid var(--border); border-radius: var(--radius); padding: 14px 16px; position: relative; overflow: hidden; }
.stat-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px; }
.stat-card.green::before { background: var(--primary); }
.stat-card.amber::before { background: var(--accent); }
.stat-card.blue::before { background: var(--info); }
.stat-card.red::before { background: var(--danger); }
.stat-card.purple::before { background: #8b5cf6; }
.stat-label { font-size: 11px; color: var(--text-muted); font-weight: 500; margin-bottom: 4px; }
.stat-value { font-size: 18px; font-weight: 700; color: var(--primary-dark); line-height: 1.1; }
.stat-sub { font-size: 10px; color: var(--text-muted); margin-top: 3px; }

/* Content */
.content { padding: 20px 24px; }
.section { display: none; }
.section.active { display: block; }

/* Cards */
.card { background: var(--bg-card); border: 1px solid var(--border); border-radius: var(--radius); padding: 18px 22px; margin-bottom: 18px; }
.card-title { font-size: 15px; font-weight: 700; color: var(--primary-dark); margin-bottom: 14px; display: flex; align-items: center; gap: 8px; padding-bottom: 10px; border-bottom: 1px solid var(--border-light); }
.card-title .badge { font-size: 10px; background: var(--primary); color: #fff; padding: 2px 7px; border-radius: 20px; }
.card-title .badge-warn { font-size: 10px; background: var(--warning); color: #fff; padding: 2px 7px; border-radius: 20px; }

/* Grid */
.grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
.grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 14px; }
.grid-4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; }
.grid-5 { display: grid; grid-template-columns: repeat(5, 1fr); gap: 10px; }

/* Form */
.form-group { display: flex; flex-direction: column; gap: 5px; }
.form-group label { font-size: 12px; font-weight: 600; color: var(--text-muted); }
.form-group select, .form-group input[type=text], .form-group input[type=number] {
  padding: 8px 10px; border: 1.5px solid var(--border); border-radius: var(--radius-sm);
  font-family: inherit; font-size: 13px; color: var(--text); background: var(--bg-input);
  outline: none; transition: border-color 0.2s; width: 100%;
}
.form-group select:focus, .form-group input:focus { border-color: var(--primary); background: var(--bg-card); }
.form-group textarea { padding: 8px 10px; border: 1.5px solid var(--border); border-radius: var(--radius-sm); font-family: inherit; font-size: 13px; color: var(--text); background: var(--bg-input); outline: none; resize: vertical; }
.hint { font-size: 10px; color: var(--text-muted); }

/* Material table */
.mat-table { width: 100%; border-collapse: collapse; font-size: 12px; }
.mat-table th { background: var(--bg); padding: 8px 12px; text-align: left; font-weight: 700; color: var(--text-muted); font-size: 11px; border-bottom: 1px solid var(--border); }
.mat-table td { padding: 9px 12px; border-bottom: 1px solid var(--border-light); color: var(--text); }
.mat-table tr:hover td { background: var(--bg); }
.mat-table .amt { font-weight: 700; color: var(--primary-dark); text-align: right; }

/* Labor */
.labor-row { display: grid; grid-template-columns: 2fr 80px 100px 80px 110px 40px; gap: 8px; align-items: center; padding: 7px 0; border-bottom: 1px solid var(--border-light); font-size: 12px; }
.labor-row input { padding: 5px 7px; border: 1px solid var(--border); border-radius: 5px; font-family: inherit; font-size: 12px; color: var(--text); background: var(--bg-input); width: 100%; }
.labor-total-cell { font-weight: 700; color: var(--primary-dark); font-size: 12px; }

/* Feature grid */
.feature-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; }
.feature-item { display: flex; flex-direction: column; gap: 4px; padding: 10px; border: 1.5px solid var(--border); border-radius: var(--radius-sm); cursor: pointer; transition: all 0.15s; font-size: 12px; background: var(--bg-card); }
.feature-item:hover { border-color: var(--primary); }
.feature-item.selected { border-color: var(--primary); background: #e8f5eb; }
[data-theme="dark"] .feature-item.selected { background: #0d2e16; }
.feature-item-top { display: flex; align-items: center; gap: 6px; }
.feature-cost { font-size: 10px; color: var(--text-muted); padding-left: 20px; }

/* Alert */
.alert { padding: 10px 14px; border-radius: var(--radius-sm); font-size: 12px; margin-bottom: 14px; display: flex; align-items: flex-start; gap: 8px; }
.alert-info { background: #eff6ff; border: 1px solid #bfdbfe; color: #1e40af; }
.alert-warning { background: #fffbeb; border: 1px solid #fde68a; color: #92400e; }
.alert-success { background: #f0fdf4; border: 1px solid #bbf7d0; color: #14532d; }
.alert-danger { background: #fef2f2; border: 1px solid #fecaca; color: #991b1b; }
[data-theme="dark"] .alert-info { background: #1e3a5f; border-color: #2563eb; color: #93c5fd; }
[data-theme="dark"] .alert-success { background: #0d2e16; border-color: #16a34a; color: #86efac; }

/* Checklist */
.checklist-item { display: flex; align-items: flex-start; gap: 10px; padding: 10px 12px; border: 1px solid var(--border-light); border-radius: var(--radius-sm); margin-bottom: 6px; background: var(--bg-card); transition: all 0.2s; }
.checklist-item.done { background: #f0fdf4; border-color: #bbf7d0; opacity: 0.8; }
[data-theme="dark"] .checklist-item.done { background: #0d2e16; border-color: #16a34a; }
.checklist-item input[type=checkbox] { margin-top: 2px; accent-color: var(--primary); transform: scale(1.2); flex-shrink: 0; }
.checklist-label { font-size: 13px; flex: 1; }
.checklist-label.done-text { text-decoration: line-through; color: var(--text-muted); }
.checklist-phase { font-size: 10px; color: var(--text-muted); margin-top: 2px; }

/* Project comparison table */
.compare-table { width: 100%; border-collapse: collapse; font-size: 12px; }
.compare-table th { background: var(--primary); color: #fff; padding: 10px 14px; text-align: left; }
.compare-table td { padding: 9px 14px; border-bottom: 1px solid var(--border-light); color: var(--text); }
.compare-table tr:hover td { background: var(--bg); }
.compare-table .best { color: var(--success); font-weight: 700; }
.compare-table .worst { color: var(--danger); font-weight: 700; }

/* Price trend */
.price-trend-chart { position: relative; width: 100%; height: 220px; }

/* Contract */
.milestone-row { display: grid; grid-template-columns: 2fr 1fr 1fr 120px; gap: 10px; align-items: center; padding: 8px 0; border-bottom: 1px solid var(--border-light); font-size: 12px; }
.milestone-row input, .milestone-row select { padding: 5px 7px; border: 1px solid var(--border); border-radius: 5px; font-family: inherit; font-size: 12px; color: var(--text); background: var(--bg-input); width: 100%; }
.status-badge { padding: 3px 8px; border-radius: 10px; font-size: 10px; font-weight: 700; }
.status-pending { background: #fef3c7; color: #92400e; }
.status-ongoing { background: #dbeafe; color: #1e40af; }
.status-done { background: #dcfce7; color: #14532d; }

/* Floor finishing */
.floor-finish-row { display: grid; grid-template-columns: 80px 1fr 1fr 1fr 120px; gap: 10px; align-items: center; padding: 8px 0; border-bottom: 1px solid var(--border-light); font-size: 12px; }
.floor-finish-row select { padding: 5px 7px; border: 1px solid var(--border); border-radius: 5px; font-family: inherit; font-size: 12px; background: var(--bg-input); color: var(--text); width: 100%; }

/* AI chat */
.ai-chat-box { border: 1px solid var(--border); border-radius: var(--radius); overflow: hidden; }
.ai-messages { min-height: 250px; max-height: 400px; overflow-y: auto; padding: 16px; background: var(--bg); display: flex; flex-direction: column; gap: 10px; }
.ai-msg { padding: 10px 14px; border-radius: 10px; font-size: 13px; line-height: 1.6; max-width: 85%; }
.ai-msg.user { background: var(--primary); color: #fff; align-self: flex-end; border-bottom-right-radius: 4px; }
.ai-msg.bot { background: var(--bg-card); border: 1px solid var(--border); align-self: flex-start; border-bottom-left-radius: 4px; color: var(--text); }
.ai-msg.typing { color: var(--text-muted); font-style: italic; }
.ai-input-row { display: flex; gap: 8px; padding: 12px; border-top: 1px solid var(--border); background: var(--bg-card); }
.ai-input-row input { flex: 1; padding: 8px 12px; border: 1.5px solid var(--border); border-radius: 20px; font-family: inherit; font-size: 13px; background: var(--bg-input); color: var(--text); outline: none; }
.ai-input-row input:focus { border-color: var(--primary); }

/* Badge system */
.badge-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; }
.badge-item { text-align: center; padding: 16px 12px; border: 1.5px solid var(--border); border-radius: var(--radius); }
.badge-item.earned { border-color: var(--accent); background: #fffbeb; }
[data-theme="dark"] .badge-item.earned { background: #2a1f00; }
.badge-icon { font-size: 32px; margin-bottom: 6px; }
.badge-name { font-size: 12px; font-weight: 700; color: var(--text); }
.badge-desc { font-size: 10px; color: var(--text-muted); margin-top: 3px; }
.badge-item.locked .badge-icon { filter: grayscale(1); opacity: 0.4; }
.badge-item.locked .badge-name { color: var(--text-muted); }

/* Theme toggle */
.theme-toggle { width: 44px; height: 22px; border-radius: 11px; background: var(--border); position: relative; cursor: pointer; transition: background 0.3s; border: none; flex-shrink: 0; }
.theme-toggle.dark { background: var(--primary); }
.theme-toggle::after { content: ''; position: absolute; top: 2px; left: 2px; width: 18px; height: 18px; border-radius: 50%; background: #fff; transition: transform 0.3s; }
.theme-toggle.dark::after { transform: translateX(22px); }

/* BOQ */
.boq-table { width: 100%; border-collapse: collapse; font-size: 12px; }
.boq-table th { background: var(--primary-dark); color: #fff; padding: 9px 12px; text-align: left; font-size: 11px; }
.boq-table td { padding: 8px 12px; border-bottom: 1px solid var(--border-light); color: var(--text); }
.boq-table .section-row td { background: var(--bg); font-weight: 700; font-size: 12px; color: var(--primary-dark); }
.boq-table .total-row td { background: var(--primary-dark); color: #fff; font-weight: 700; }

/* Weather card */
.weather-card { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; }
.w-item { text-align: center; padding: 14px 10px; background: var(--bg); border-radius: var(--radius-sm); border: 1px solid var(--border-light); }
.w-icon { font-size: 28px; margin-bottom: 4px; }
.w-label { font-size: 11px; color: var(--text-muted); }
.w-val { font-size: 15px; font-weight: 700; color: var(--text); }

/* Scrollbar */
::-webkit-scrollbar { width: 5px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: #b0cbb8; border-radius: 3px; }

/* Range */
input[type=range] { -webkit-appearance: none; width: 100%; height: 4px; border-radius: 2px; background: var(--border); }
input[type=range]::-webkit-slider-thumb { -webkit-appearance: none; width: 16px; height: 16px; border-radius: 50%; background: var(--primary); cursor: pointer; }

.currency-toggle { display: flex; gap: 4px; }
.cur-btn { padding: 5px 10px; border-radius: 16px; border: 1.5px solid var(--border); background: transparent; cursor: pointer; font-family: inherit; font-size: 11px; font-weight: 600; color: var(--text-muted); }
.cur-btn.active { background: var(--primary); color: #fff; border-color: var(--primary); }

.breakdown-row { display: flex; justify-content: space-between; align-items: center; padding: 8px 0; border-bottom: 1px solid var(--border-light); font-size: 13px; }
.breakdown-row.total { font-weight: 700; font-size: 15px; color: var(--primary-dark); border-top: 2px solid var(--primary); border-bottom: none; padding-top: 10px; margin-top: 4px; }

.loan-result { background: #f0fdf4; border: 1px solid #bbf7d0; border-radius: var(--radius-sm); padding: 14px; margin-top: 10px; }
[data-theme="dark"] .loan-result { background: #0d2e16; border-color: #16a34a; }
.loan-result .monthly { font-size: 26px; font-weight: 700; color: var(--primary); }

.fee-row { display: flex; justify-content: space-between; align-items: center; padding: 7px 0; border-bottom: 1px solid var(--border-light); font-size: 13px; }
.fee-row:last-child { font-weight: 700; border-bottom: none; }

.report-header { text-align: center; padding: 20px; background: linear-gradient(135deg, var(--primary-dark), var(--primary)); color: #fff; border-radius: var(--radius); margin-bottom: 16px; }

.chart-wrap { position: relative; width: 100%; }

/* Progress bar */
.progress-bar-wrap { height: 8px; background: var(--border); border-radius: 4px; overflow: hidden; margin: 6px 0; }
.progress-bar-fill { height: 100%; border-radius: 4px; transition: width 0.5s; }

/* Tabs within section */
.inner-tabs { display: flex; gap: 4px; margin-bottom: 14px; flex-wrap: wrap; }
.inner-tab { padding: 6px 14px; border-radius: 20px; border: 1.5px solid var(--border); background: transparent; cursor: pointer; font-family: inherit; font-size: 12px; font-weight: 500; color: var(--text-muted); }
.inner-tab.active { background: var(--primary); color: #fff; border-color: var(--primary); }

@media print {
  .sidebar, .header-right, .btn, .summary-bar { display: none !important; }
  body { font-size: 12px; }
}
</style>
</head>
<body>
<div class="app">

<!-- ===== SIDEBAR ===== -->
<div class="sidebar">
  <div class="logo">
    <div style="font-size:24px; margin-bottom:4px;">🏗️</div>
    <div class="logo-title">নির্মাণ হিসাব</div>
    <div class="logo-sub">Bangladesh Construction Estimator v4.0</div>
  </div>
  <div class="nav">
    <div class="nav-section">মূল ইনপুট</div>
    <div class="nav-item active" onclick="showSection('location')">📍 লোকেশন ও পরিবেশ</div>
    <div class="nav-item" onclick="showSection('building')">🏢 বিল্ডিং কনফিগারেশন</div>
    <div class="nav-item" onclick="showSection('materials')">🧱 ম্যাটেরিয়াল টেকঅফ</div>
    <div class="nav-item" onclick="showSection('labor')">👷 শ্রমিক ও যন্ত্রপাতি</div>
    <div class="nav-item" onclick="showSection('extras')">⚡ অতিরিক্ত সুবিধা</div>
    <div class="nav-item" onclick="showSection('floorfinish')">🏠 তলা অনুযায়ী ফিনিশিং <span class="nav-badge">নতুন</span></div>
    <div class="nav-section">স্পেশাল</div>
    <div class="nav-item" onclick="showSection('special')">⭐ স্পেশাল ফিচারস</div>
    <div class="nav-item" onclick="showSection('financial')">💰 আর্থিক ও সরকারি ফি</div>
    <div class="nav-item" onclick="showSection('boq')">📋 BOQ জেনারেটর <span class="nav-badge">নতুন</span></div>
    <div class="nav-item" onclick="showSection('contract')">📑 কন্ট্রাক্ট ম্যানেজমেন্ট <span class="nav-badge">নতুন</span></div>
    <div class="nav-section">বিশ্লেষণ</div>
    <div class="nav-item" onclick="showSection('ai')">🤖 AI সাজেশন <span class="nav-badge">নতুন</span></div>
    <div class="nav-item" onclick="showSection('prices')">📈 মূল্য ট্রেন্ড <span class="nav-badge">নতুন</span></div>
    <div class="nav-item" onclick="showSection('weather')">🌤️ আবহাওয়া ও বিলম্ব <span class="nav-badge">নতুন</span></div>
    <div class="nav-item" onclick="showSection('checklist')">✅ কোয়ালিটি চেকলিস্ট <span class="nav-badge">নতুন</span></div>
    <div class="nav-item" onclick="showSection('compare')">📊 মাল্টি-প্রজেক্ট তুলনা <span class="nav-badge">নতুন</span></div>
    <div class="nav-item" onclick="showSection('badges')">🏅 গেমিফিকেশন ব্যাজ <span class="nav-badge">নতুন</span></div>
    <div class="nav-item" onclick="showSection('report')">📄 রিপোর্ট ও QR কোড</div>
  </div>
  <div class="sidebar-footer">
    BNBC ২০২০ | রাজউক অনুমোদিত<br>
    <span id="save-indicator" style="color:#6b9e77;">● অটো-সেভ চালু</span>
  </div>
</div>

<!-- ===== MAIN ===== -->
<div class="main">
  <!-- Header -->
  <div class="header">
    <div class="header-left">
      <h1 id="page-title">লোকেশন ও পরিবেশ</h1>
      <p id="page-sub">এলাকা নির্বাচন করুন</p>
    </div>
    <div class="header-right">
      <div class="currency-toggle">
        <button class="cur-btn active" onclick="setCurrency('BDT',this)">৳ BDT</button>
        <button class="cur-btn" onclick="setCurrency('USD',this)">$ USD</button>
        <button class="cur-btn" onclick="setCurrency('INR',this)">₹ INR</button>
      </div>
      <button class="theme-toggle" id="themeBtn" onclick="toggleTheme()"></button>
      <button class="btn btn-outline btn-sm" onclick="saveProject()">💾 সেভ</button>
      <button class="btn btn-outline btn-sm" onclick="loadProject()">📂 লোড</button>
      <button class="btn btn-accent btn-sm" onclick="showSection('report')">📊 রিপোর্ট</button>
    </div>
  </div>

  <!-- Summary Bar -->
  <div class="summary-bar">
    <div class="stat-card green">
      <div class="stat-label">মোট নির্মাণ খরচ</div>
      <div class="stat-value" id="total-cost">৳ ০</div>
      <div class="stat-sub" id="cost-per-sqft">প্রতি sqft: ৳ ০</div>
    </div>
    <div class="stat-card amber">
      <div class="stat-label">নির্মাণ সময়</div>
      <div class="stat-value" id="construction-time">০ মাস</div>
      <div class="stat-sub" id="manday-info">ম্যান-ডে: ০</div>
    </div>
    <div class="stat-card blue">
      <div class="stat-label">পরিবেশ ফ্যাক্টর</div>
      <div class="stat-value" id="area-factor">১.০০</div>
      <div class="stat-sub" id="zone-info">জোন: —</div>
    </div>
    <div class="stat-card red">
      <div class="stat-label">সরকারি ফি+ভ্যাট</div>
      <div class="stat-value" id="govt-cost">৳ ০</div>
      <div class="stat-sub">রাজউক+ওয়াসা</div>
    </div>
    <div class="stat-card purple">
      <div class="stat-label">প্রজেক্ট স্কোর</div>
      <div class="stat-value" id="project-score">০/১০০</div>
      <div class="stat-sub" id="score-label">হিসাব শুরু করুন</div>
    </div>
  </div>

  <div class="content">

    <!-- ====== LOCATION ====== -->
    <div class="section active" id="section-location">
      <div class="card">
        <div class="card-title">🗺️ লোকেশন নির্বাচন <span class="badge">৬৪ জেলা | ৪৯৫+ উপজেলা</span></div>
        <div class="grid-3">
          <div class="form-group"><label>বিভাগ</label>
            <select id="division" onchange="updateDistricts()">
              <option value="">-- বিভাগ --</option>
              <option value="dhaka">ঢাকা</option><option value="chittagong">চট্টগ্রাম</option>
              <option value="rajshahi">রাজশাহী</option><option value="khulna">খুলনা</option>
              <option value="barisal">বরিশাল</option><option value="sylhet">সিলেট</option>
              <option value="rangpur">রংপুর</option><option value="mymensingh">ময়মনসিংহ</option>
            </select>
          </div>
          <div class="form-group"><label>জেলা</label>
            <select id="district" onchange="updateUpazilas()"><option value="">-- জেলা --</option></select>
          </div>
          <div class="form-group"><label>উপজেলা/থানা</label>
            <select id="upazila" onchange="recalculate()"><option value="">-- উপজেলা --</option></select>
          </div>
        </div>
        <div class="grid-3" style="margin-top:12px;">
          <div class="form-group"><label>এলাকার ধরণ</label>
            <select id="area-type" onchange="recalculate()">
              <option value="1.35">মেট্রো কোর (ঢাকা/চট্টগ্রাম)</option>
              <option value="1.15">সাব-আরবান</option>
              <option value="1.0" selected>শহর (স্ট্যান্ডার্ড)</option>
              <option value="0.85">উপজেলা সদর</option>
              <option value="0.68">গ্রামীণ</option>
            </select>
          </div>
          <div class="form-group"><label>ভূমিকম্প জোন (BNBC ২০২০)</label>
            <select id="seismic-zone" onchange="recalculate()">
              <option value="1.0">জোন-১ (কম) — খুলনা, বরিশাল</option>
              <option value="1.05" selected>জোন-২ (মাঝারি) — ঢাকা, চট্টগ্রাম</option>
              <option value="1.10">জোন-৩ (বেশি) — রাজশাহী, রংপুর</option>
              <option value="1.15">জোন-৪ (অতি বেশি) — সিলেট</option>
            </select>
          </div>
          <div class="form-group"><label>বিশেষ পরিবেশ</label>
            <select id="special-env" onchange="recalculate()">
              <option value="1.0">সাধারণ</option>
              <option value="1.07">সমুদ্র উপকূল (+৭%)</option>
              <option value="1.20">পার্বত্য এলাকা (+২০%)</option>
              <option value="1.12">হাওর/বিল এলাকা (+১২%)</option>
              <option value="1.08">বন্যা প্রবণ (+৮%)</option>
            </select>
          </div>
        </div>
        <div class="grid-3" style="margin-top:12px;">
          <div class="form-group"><label>বন্যা ঝুঁকি</label>
            <select id="flood-risk" onchange="recalculate()">
              <option value="1.0">নেই</option>
              <option value="1.05">কম</option>
              <option value="1.10" selected>মাঝারি</option>
              <option value="1.15">বেশি</option>
              <option value="1.20">অতি বেশি</option>
            </select>
          </div>
          <div class="form-group"><label>গ্যাস সংযোগ দূরত্ব (মিটার)</label>
            <input type="number" id="gas-dist" value="50" min="0" onchange="recalculate()">
            <span class="hint">প্রতি মিটার ৳ ৮০০</span>
          </div>
          <div class="form-group"><label>সিটি কর্পোরেশন / পৌরসভা</label>
            <select id="city-corp" onchange="recalculate()">
              <option value="0">প্রযোজ্য নয়</option>
              <option value="1">ঢাকা উত্তর/দক্ষিণ সিটি কর্প.</option>
              <option value="1">চট্টগ্রাম সিটি কর্প.</option>
              <option value="1">অন্যান্য সিটি কর্পোরেশন (৮টি)</option>
              <option value="0.5">পৌরসভা (১ম শ্রেণী)</option>
              <option value="0.3">পৌরসভা (২য়/৩য় শ্রেণী)</option>
            </select>
          </div>
        </div>
        <div style="margin-top:14px; padding:12px; background:var(--bg); border-radius:var(--radius-sm); font-size:12px;">
          <strong>সম্মিলিত পরিবেশ ফ্যাক্টর:</strong>
          <span id="env-combined" style="font-size:16px; font-weight:700; color:var(--primary); margin-left:8px;">১.১৬</span>
          <span style="margin-left:16px; color:var(--text-muted);">
            এলাকা <span id="ef1">১.০০</span> × ভূমিকম্প <span id="ef2">১.০৫</span> × বন্যা <span id="ef3">১.১০</span> × পরিবেশ <span id="ef4">১.০০</span>
          </span>
        </div>
      </div>
    </div>

    <!-- ====== BUILDING ====== -->
    <div class="section" id="section-building">
      <div class="card">
        <div class="card-title">🏢 বিল্ডিং টাইপ ও কনফিগারেশন <span class="badge">৩০+ ধরণ</span></div>
        <div class="grid-3">
          <div class="form-group"><label>বিল্ডিং টাইপ</label>
            <select id="bldg-type" onchange="onBuildingTypeChange()">
              <option value="1.0">আবাসিক বাড়ি/ফ্ল্যাট</option>
              <option value="1.15">অ্যাপার্টমেন্ট (বহুতল)</option>
              <option value="1.25">বাণিজ্যিক অফিস</option>
              <option value="1.30">শোরুম</option>
              <option value="1.35">ব্যাংক</option>
              <option value="1.68">হাসপাতাল</option>
              <option value="1.45">ক্লিনিক</option>
              <option value="1.20">স্কুল</option>
              <option value="1.30">কলেজ/বিশ্ববিদ্যালয়</option>
              <option value="1.40">হোটেল (★★★)</option>
              <option value="1.60">হোটেল (★★★★★)</option>
              <option value="1.55">রিসোর্ট</option>
              <option value="1.10">মসজিদ</option>
              <option value="0.85">ঈদগাহ মাঠ</option>
              <option value="0.94">গোডাউন/ওয়্যারহাউস</option>
              <option value="0.90">কোল্ড স্টোরেজ</option>
              <option value="1.05">শিল্প কারখানা</option>
              <option value="1.15">গার্মেন্টস</option>
              <option value="1.35">ফুড প্রসেসিং</option>
              <option value="1.50">ফার্মাসিউটিক্যালস</option>
              <option value="1.10">কমিউনিটি সেন্টার</option>
              <option value="1.20">কনভেনশন হল</option>
              <option value="0.95">পেট্রোল পাম্প</option>
              <option value="1.15">ভিলা</option>
              <option value="1.45">ল্যাবরেটরি</option>
              <option value="1.30">স্টেডিয়াম</option>
              <option value="1.25">অডিটোরিয়াম</option>
              <option value="1.10">মাল্টিলেভেল পার্কিং</option>
            </select>
          </div>
          <div class="form-group"><label>নির্মাণ মান</label>
            <select id="quality" onchange="recalculate()">
              <option value="0.70">ইকোনমি (×০.৭)</option>
              <option value="1.00" selected>স্ট্যান্ডার্ড (×১.০)</option>
              <option value="1.35">প্রিমিয়াম (×১.৩৫)</option>
              <option value="1.85">লাক্সারি (×১.৮৫)</option>
            </select>
          </div>
          <div class="form-group"><label>স্ট্রাকচার</label>
            <select id="structure" onchange="recalculate()">
              <option value="1.0" selected>RCC ফ্রেম</option>
              <option value="0.85">লোড বেয়ারিং</option>
              <option value="1.20">স্টিল ফ্রেম</option>
            </select>
          </div>
        </div>
        <div class="grid-4" style="margin-top:12px;">
          <div class="form-group"><label>মোট আয়তন (sqft)</label>
            <input type="number" id="total-area" value="2000" min="100" onchange="recalculate(); renderFloorFinish();">
          </div>
          <div class="form-group"><label>তলা সংখ্যা</label>
            <input type="number" id="floors" value="3" min="1" max="50" onchange="recalculate(); renderFloorFinish();">
          </div>
          <div class="form-group"><label>ফাউন্ডেশন টাইপ</label>
            <select id="foundation" onchange="recalculate()">
              <option value="0.08">শ্যালো</option>
              <option value="0.12" selected>পাইল</option>
              <option value="0.10">র্যাফট</option>
            </select>
          </div>
          <div class="form-group"><label>লিফট সংখ্যা</label>
            <input type="number" id="lifts" value="0" min="0" onchange="recalculate()">
            <span class="hint">প্রতি লিফট ৳ ২৫ লক্ষ</span>
          </div>
        </div>
        <div class="grid-3" style="margin-top:12px;">
          <div class="form-group"><label>কংক্রিট গ্রেড</label>
            <select id="concrete-grade" onchange="recalculate()">
              <option value="1.0">M15</option>
              <option value="1.08" selected>M20 (স্ট্যান্ডার্ড)</option>
              <option value="1.15">M25</option>
              <option value="1.22">M30</option>
            </select>
          </div>
          <div class="form-group"><label>বেস রেট (৳/sqft)</label>
            <input type="number" id="base-rate" value="2200" onchange="recalculate()">
            <span class="hint">ঢাকা স্ট্যান্ডার্ড: ৳ ২২০০–২৮০০</span>
          </div>
          <div class="form-group"><label>মোট কনফিগ ফ্যাক্টর</label>
            <input type="text" id="config-factor" readonly style="font-weight:700; color:var(--primary); background:var(--bg);">
          </div>
        </div>
      </div>
    </div>

    <!-- ====== MATERIALS ====== -->
    <div class="section" id="section-materials">
      <div class="card">
        <div class="card-title">🧱 ম্যাটেরিয়াল টেকঅফ <span class="badge">স্বয়ংক্রিয় হিসাব</span></div>
        <div class="grid-3" style="margin-bottom:14px;">
          <div class="form-group"><label>রডের ডায়া (মিমি)</label>
            <select id="rod-dia" onchange="recalculate()">
              <option value="0.87">৮ মিমি</option>
              <option value="0.92">১০ মিমি</option>
              <option value="1.0" selected>১২ মিমি (সাধারণ)</option>
              <option value="1.12">১৬ মিমি</option>
              <option value="1.25">২০ মিমি</option>
              <option value="1.40">২৫ মিমি</option>
            </select>
          </div>
          <div class="form-group"><label>ইটের ব্র্যান্ড</label>
            <select id="brick-brand" onchange="recalculate()">
              <option value="12">সাধারণ মাটির ইট (৳ ১২)</option>
              <option value="14" selected>১ম শ্রেণী (৳ ১৪)</option>
              <option value="18">হলো ব্লক (৳ ১৮)</option>
              <option value="22">অটো ব্রিক (৳ ২২)</option>
            </select>
          </div>
          <div class="form-group"><label>সিমেন্ট ব্র্যান্ড</label>
            <select id="cement-brand" onchange="recalculate()">
              <option value="480">সাধারণ OPC (৳ ৪৮০)</option>
              <option value="520" selected>Shah Cement (৳ ৫২০)</option>
              <option value="550">Holcim (৳ ৫৫০)</option>
              <option value="580">LaFarge (৳ ৫৮০)</option>
            </select>
          </div>
        </div>
        <table class="mat-table" id="materials-table">
          <thead>
            <tr>
              <th>#</th><th>উপকরণ</th><th>পরিমাণ</th><th>একক</th><th>একক মূল্য (৳)</th><th class="amt">মোট (৳)</th>
            </tr>
          </thead>
          <tbody id="mat-tbody"></tbody>
        </table>
      </div>
      <div class="card">
        <div class="card-title">📊 উপকরণ খরচ বিতরণ</div>
        <div class="chart-wrap" style="height:260px;"><canvas id="matChart" role="img" aria-label="উপকরণ বার চার্ট"></canvas></div>
      </div>
    </div>

    <!-- ====== LABOR ====== -->
    <div class="section" id="section-labor">
      <div class="card">
        <div class="card-title">👷 শ্রমিক তালিকা <span class="badge">৩০+ ক্যাটাগরি</span></div>
        <div style="display:grid; grid-template-columns:2fr 80px 100px 80px 110px 40px; gap:8px; padding:6px 0; border-bottom:2px solid var(--border); font-size:11px; font-weight:700; color:var(--text-muted);">
          <span>পদবী</span><span>সংখ্যা</span><span>দৈনিক মজুরি (৳)</span><span>কর্মদিন</span><span>মোট (৳)</span><span></span>
        </div>
        <div id="labor-list"></div>
        <div style="margin-top:10px; display:flex; gap:8px; flex-wrap:wrap;">
          <button class="btn btn-outline btn-sm" onclick="addLaborRow()">+ শ্রমিক যোগ</button>
          <button class="btn btn-sm" style="background:var(--bg); border:1px solid var(--border);" onclick="resetLabor()">↩ রিসেট</button>
        </div>
      </div>
      <div class="card">
        <div class="card-title">🔧 যন্ত্রপাতি ভাড়া</div>
        <div class="grid-4">
          <div class="form-group"><label>ক্রেন (ঘন্টা)</label>
            <input type="number" id="crane-hrs" value="0" min="0" onchange="recalculate()">
            <span class="hint">৳ ৩,৫০০/ঘন্টা</span></div>
          <div class="form-group"><label>মিক্সার (দিন)</label>
            <input type="number" id="mixer-days" value="30" min="0" onchange="recalculate()">
            <span class="hint">৳ ১,৮০০/দিন</span></div>
          <div class="form-group"><label>পাম্প (দিন)</label>
            <input type="number" id="pump-days" value="0" min="0" onchange="recalculate()">
            <span class="hint">৳ ৮,০০০/দিন</span></div>
          <div class="form-group"><label>ভাইব্রেটর (দিন)</label>
            <input type="number" id="vib-days" value="20" min="0" onchange="recalculate()">
            <span class="hint">৳ ৫০০/দিন</span></div>
        </div>
        <div style="margin-top:10px; padding:10px; background:var(--bg); border-radius:6px; font-size:13px;">
          মোট যন্ত্রপাতি খরচ: <strong id="equip-total">৳ ০</strong> &nbsp;|&nbsp; মোট ম্যান-ডে: <strong id="total-manday">০</strong> &nbsp;|&nbsp; আনু. সময়: <strong id="est-months" style="color:var(--accent);">০ মাস</strong>
        </div>
      </div>
    </div>

    <!-- ====== EXTRAS ====== -->
    <div class="section" id="section-extras">
      <div class="card">
        <div class="card-title">⚡ অতিরিক্ত সুবিধা ও ডিজাইন</div>
        <div class="grid-3">
          <div class="form-group"><label>সোলার প্যানেল (kW)</label>
            <input type="number" id="solar-kw" value="0" min="0" onchange="recalculate(); calcSolarROI()">
            <span class="hint">৳ ৮০,০০০/kW</span></div>
          <div class="form-group"><label>জেনারেটর (kVA)</label>
            <input type="number" id="gen-kva" value="0" min="0" onchange="recalculate()">
            <span class="hint">৳ ১৫,০০০/kVA</span></div>
          <div class="form-group"><label>বাউন্ডারি ওয়াল (ফুট)</label>
            <input type="number" id="boundary" value="0" min="0" onchange="recalculate()">
            <span class="hint">৳ ৬০০/ফুট</span></div>
          <div class="form-group"><label>ইন্টেরিয়র লেভেল</label>
            <select id="interior" onchange="recalculate()">
              <option value="0">নেই</option>
              <option value="150">বেসিক (৳ ১৫০/sqft)</option>
              <option value="350" selected>মিডিয়াম (৳ ৩৫০/sqft)</option>
              <option value="700">প্রিমিয়াম (৳ ৭০০/sqft)</option>
              <option value="1500">লাক্সারি (৳ ১৫০০/sqft)</option>
            </select>
          </div>
          <div class="form-group"><label>ওভারহেড ট্যাংক (লিটার)</label>
            <input type="number" id="tank" value="2000" min="0" onchange="recalculate()">
            <span class="hint">৳ ১২,০০০/হাজার লিটার</span></div>
          <div class="form-group"><label>ল্যান্ডস্কেপিং (sqft)</label>
            <input type="number" id="landscape" value="0" min="0" onchange="recalculate()">
            <span class="hint">৳ ১২০/sqft</span></div>
        </div>
        <div class="grid-4" style="margin-top:12px;">
          <div class="form-group"><label>বেডরুম</label>
            <input type="number" id="bedrooms" value="3" min="0" onchange="recalculate()">
            <span class="hint">৳ ৮০,০০০/টি</span></div>
          <div class="form-group"><label>দরজা</label>
            <input type="number" id="doors" value="8" min="0" onchange="recalculate()">
            <span class="hint">৳ ১২,০০০/টি</span></div>
          <div class="form-group"><label>জানালা</label>
            <input type="number" id="windows" value="12" min="0" onchange="recalculate()">
            <span class="hint">৳ ৮,০০০/টি</span></div>
          <div class="form-group"><label>বাথরুম</label>
            <input type="number" id="bathrooms" value="3" min="0" onchange="recalculate()">
            <span class="hint">৳ ৬০,০০০/টি</span></div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">☀️ সোলার ROI ক্যালকুলেটর</div>
        <div class="grid-3">
          <div class="form-group"><label>মাসিক বিদ্যুৎ বিল (৳)</label>
            <input type="number" id="monthly-bill" value="5000" onchange="calcSolarROI()"></div>
          <div class="form-group">
            <label>সোলার কভারেজ: <span id="spct-out">৭০%</span></label>
            <input type="range" id="solar-pct" min="10" max="100" value="70" oninput="document.getElementById('spct-out').textContent=this.value+'%'; calcSolarROI()">
          </div>
          <div id="solar-roi-result" style="background:var(--bg); padding:12px; border-radius:8px; font-size:13px; border:1px solid var(--border);">
            সোলার kW দিন →
          </div>
        </div>
      </div>
    </div>

    <!-- ====== FLOOR FINISHING (NEW) ====== -->
    <div class="section" id="section-floorfinish">
      <div class="alert alert-info">🏠 প্রতিটি তলার জন্য আলাদা ফিনিশিং মান ও উপকরণ নির্ধারণ করুন। যেমন: নিচতলায় মার্বেল, উপরে টাইলস।</div>
      <div class="card">
        <div class="card-title">🏠 তলা অনুযায়ী কাস্টম ফিনিশিং <span class="badge">নতুন ফিচার</span></div>
        <div style="display:grid; grid-template-columns:80px 1fr 1fr 1fr 120px; gap:10px; padding:8px 0; border-bottom:2px solid var(--border); font-size:11px; font-weight:700; color:var(--text-muted);">
          <span>তলা</span><span>মেঝে</span><span>দেয়াল</span><span>সিলিং</span><span>অতিরিক্ত (৳)</span>
        </div>
        <div id="floor-finish-list"></div>
        <div style="margin-top:12px; padding:10px; background:var(--bg); border-radius:6px; font-size:13px;">
          ফিনিশিং মোট অতিরিক্ত: <strong id="finish-extra-total" style="color:var(--primary);">৳ ০</strong>
        </div>
      </div>
    </div>

    <!-- ====== SPECIAL ====== -->
    <div class="section" id="section-special">
      <div class="alert alert-warning">⭐ বিল্ডিং টাইপ অনুযায়ী স্বয়ংক্রিয়ভাবে ফিচার লোড হয়।</div>
      <div class="card">
        <div class="card-title" id="special-title">⭐ স্পেশাল ফিচারস (আবাসিক)</div>
        <div class="feature-grid" id="special-features"></div>
        <div style="margin-top:12px; padding:10px; background:var(--bg); border-radius:6px;">
          স্পেশাল মোট: <strong id="special-total" style="color:var(--primary);">৳ ০</strong>
        </div>
      </div>
    </div>

    <!-- ====== FINANCIAL ====== -->
    <div class="section" id="section-financial">
      <div class="grid-2">
        <div>
          <div class="card">
            <div class="card-title">📈 আর্থিক চার্জ</div>
            <div class="grid-2">
              <div class="form-group"><label>ভ্যাট (%)</label>
                <input type="number" id="vat" value="15" min="0" onchange="recalculate()"></div>
              <div class="form-group"><label>কন্টিনজেন্সি (%)</label>
                <input type="number" id="contingency" value="5" min="0" onchange="recalculate()"></div>
              <div class="form-group"><label>কন্ট্রাক্টর মার্জিন (%)</label>
                <input type="number" id="margin" value="10" min="0" onchange="recalculate()"></div>
              <div class="form-group"><label>মুদ্রাস্ফীতি (%)</label>
                <input type="number" id="inflation" value="3" min="0" onchange="recalculate()"></div>
            </div>
          </div>
          <div class="card">
            <div class="card-title">🏦 ঋণ ক্যালকুলেটর</div>
            <div class="form-group" style="margin-bottom:8px;"><label>ঋণ পরিমাণ (৳)</label>
              <input type="number" id="loan-amt" value="5000000" onchange="calcLoan()"></div>
            <div class="form-group" style="margin-bottom:8px;"><label>সুদ হার (% বার্ষিক)</label>
              <input type="number" id="loan-rate" value="9" onchange="calcLoan()"></div>
            <div class="form-group" style="margin-bottom:8px;"><label>মেয়াদ (বছর)</label>
              <input type="number" id="loan-years" value="15" onchange="calcLoan()"></div>
            <div class="loan-result">
              <div style="font-size:12px; color:var(--text-muted);">মাসিক কিস্তি (EMI)</div>
              <div class="monthly" id="emi-val">৳ ৫০,৭১৪</div>
              <div style="font-size:11px; color:var(--text-muted); margin-top:4px;" id="loan-details">মোট পরিশোধ: ৳ ৯১,২৮,৫২০</div>
            </div>
          </div>
        </div>
        <div>
          <div class="card">
            <div class="card-title">🏛️ সরকারি ও আইনি ফি</div>
            <div class="fee-row"><span>রাজউক অনুমোদন ফি</span><span id="rajuk-fee" style="font-weight:600;">৳ ০</span></div>
            <div class="fee-row"><span>ওয়াসা সংযোগ ফি</span><span style="font-weight:600;">৳ ৩০,০০০</span></div>
            <div class="fee-row"><span>বিদ্যুৎ সাবস্টেশন ফি</span><span id="elec-fee" style="font-weight:600;">৳ ০</span></div>
            <div class="fee-row"><span>গ্যাস সংযোগ ফি</span><span id="gas-fee" style="font-weight:600;">৳ ০</span></div>
            <div class="fee-row"><span>ভূমি রেজিস্ট্রেশন (৭%)</span><span id="reg-fee" style="font-weight:600;">৳ ০</span></div>
            <div class="fee-row"><span>স্ট্যাম্প ডিউটি (১.৫%)</span><span id="stamp-fee" style="font-weight:600;">৳ ০</span></div>
            <div class="fee-row"><span>ল্যান্ড ট্যাক্স (বার্ষিক)</span><span style="font-weight:600;">৳ ৫,০০০</span></div>
            <div class="fee-row"><span style="font-weight:700;">মোট সরকারি ফি</span><span id="total-govt" style="font-weight:700; color:var(--primary-dark);">৳ ০</span></div>
            <div style="margin-top:12px;">
              <div class="form-group"><label>জমির মূল্য (৳) — রেজিস্ট্রেশনের জন্য</label>
                <input type="number" id="land-price" value="0" onchange="recalculate()"></div>
            </div>
          </div>
          <div class="card">
            <div class="card-title">📋 খরচের সারসংক্ষেপ</div>
            <div class="breakdown-row"><span>মূল নির্মাণ</span><span id="br-base">৳ ০</span></div>
            <div class="breakdown-row"><span>শ্রমিক ও যন্ত্র</span><span id="br-labor">৳ ০</span></div>
            <div class="breakdown-row"><span>অতিরিক্ত সুবিধা</span><span id="br-extras">৳ ০</span></div>
            <div class="breakdown-row"><span>তলা ফিনিশিং</span><span id="br-finish">৳ ০</span></div>
            <div class="breakdown-row"><span>স্পেশাল ফিচারস</span><span id="br-special">৳ ০</span></div>
            <div class="breakdown-row"><span>ভ্যাট ও চার্জ</span><span id="br-vat">৳ ০</span></div>
            <div class="breakdown-row"><span>সরকারি ফি</span><span id="br-govt">৳ ০</span></div>
            <div class="breakdown-row total"><span>সর্বমোট</span><span id="br-total">৳ ০</span></div>
          </div>
        </div>
      </div>
    </div>

    <!-- ====== BOQ (NEW) ====== -->
    <div class="section" id="section-boq">
      <div class="card">
        <div class="card-title">📋 Bill of Quantity (BOQ) <span class="badge">কন্ট্রাক্টর/আর্কিটেক্টের জন্য</span></div>
        <div style="margin-bottom:12px; display:flex; gap:8px; flex-wrap:wrap;">
          <button class="btn btn-primary btn-sm" onclick="exportBOQ()">📥 BOQ ডাউনলোড (CSV)</button>
          <button class="btn btn-outline btn-sm" onclick="printBOQ()">🖨️ প্রিন্ট BOQ</button>
        </div>
        <div id="boq-container"></div>
      </div>
    </div>

    <!-- ====== CONTRACT (NEW) ====== -->
    <div class="section" id="section-contract">
      <div class="card">
        <div class="card-title">📑 কন্ট্রাক্ট ম্যানেজমেন্ট <span class="badge">পেমেন্ট মাইলস্টোন</span></div>
        <div class="grid-2" style="margin-bottom:14px;">
          <div class="form-group"><label>ঠিকাদারের নাম</label>
            <input type="text" id="contractor-name" placeholder="মো. রহিম কন্ট্রাকশন"></div>
          <div class="form-group"><label>চুক্তির তারিখ</label>
            <input type="text" id="contract-date" placeholder="০১/০১/২০২৫"></div>
        </div>
        <div style="display:grid; grid-template-columns:2fr 1fr 1fr 120px; gap:10px; padding:8px 0; border-bottom:2px solid var(--border); font-size:11px; font-weight:700; color:var(--text-muted);">
          <span>কাজের বিবরণ</span><span>পরিমাণ (৳)</span><span>তারিখ</span><span>অবস্থা</span>
        </div>
        <div id="milestone-list"></div>
        <div style="margin-top:10px; display:flex; gap:8px; flex-wrap:wrap;">
          <button class="btn btn-outline btn-sm" onclick="addMilestone()">+ মাইলস্টোন যোগ</button>
          <button class="btn btn-primary btn-sm" onclick="generateContract()">📄 চুক্তিপত্র জেনারেট</button>
        </div>
        <div id="contract-summary" style="margin-top:12px; padding:10px; background:var(--bg); border-radius:6px; font-size:13px; display:none;"></div>
      </div>
    </div>

    <!-- ====== AI SECTION (NEW) ====== -->
    <div class="section" id="section-ai">
      <div class="alert alert-info">🤖 AI আপনার প্রজেক্টের ডেটা বিশ্লেষণ করে সাজেশন দেবে। বাংলায় প্রশ্ন করুন।</div>
      <div class="card">
        <div class="card-title">🤖 AI নির্মাণ উপদেষ্টা <span class="badge">Claude AI</span></div>
        <div class="ai-chat-box">
          <div class="ai-messages" id="ai-messages">
            <div class="ai-msg bot">আস্সালামু আলাইকুম! আমি আপনার নির্মাণ প্রজেক্টের AI উপদেষ্টা। আপনার প্রজেক্টের খরচ কমানো, ম্যাটেরিয়াল নির্বাচন, বা যেকোনো প্রশ্ন করুন। 🏗️</div>
          </div>
          <div class="ai-input-row">
            <input type="text" id="ai-input" placeholder="যেমন: আমার বাজেট কমানোর উপায় কী? বা মাটি পরীক্ষা কি দরকার?" onkeydown="if(event.key==='Enter') sendAI()">
            <button class="btn btn-primary" onclick="sendAI()">পাঠান ↗</button>
          </div>
        </div>
        <div style="margin-top:12px;">
          <div style="font-size:12px; font-weight:700; color:var(--text-muted); margin-bottom:8px;">দ্রুত প্রশ্নসমূহ:</div>
          <div style="display:flex; gap:6px; flex-wrap:wrap;">
            <button class="btn btn-sm" style="background:var(--bg); border:1px solid var(--border);" onclick="quickAI('আমার প্রজেক্টের খরচ কমানোর উপায় বলুন')">খরচ কমানো</button>
            <button class="btn btn-sm" style="background:var(--bg); border:1px solid var(--border);" onclick="quickAI('সেরা ম্যাটেরিয়াল কোনটি?')">সেরা ম্যাটেরিয়াল</button>
            <button class="btn btn-sm" style="background:var(--bg); border:1px solid var(--border);" onclick="quickAI('নির্মাণ সময় কমানোর কৌশল কী?')">সময় কমানো</button>
            <button class="btn btn-sm" style="background:var(--bg); border:1px solid var(--border);" onclick="quickAI('ফাউন্ডেশনের জন্য কী পরামর্শ দেবেন?')">ফাউন্ডেশন পরামর্শ</button>
            <button class="btn btn-sm" style="background:var(--bg); border:1px solid var(--border);" onclick="quickAI('বাজেটের মধ্যে কোথায় খরচ বাড়ানো উচিত?')">বাজেট অপ্টিমাইজ</button>
          </div>
        </div>
      </div>
    </div>

    <!-- ====== PRICE TREND (NEW) ====== -->
    <div class="section" id="section-prices">
      <div class="card">
        <div class="card-title">📈 ম্যাটেরিয়াল মূল্য ট্রেন্ড <span class="badge">গত ১২ মাস</span></div>
        <div class="inner-tabs">
          <button class="inner-tab active" onclick="showPriceChart('rod',this)">রড (kg)</button>
          <button class="inner-tab" onclick="showPriceChart('cement',this)">সিমেন্ট (বস্তা)</button>
          <button class="inner-tab" onclick="showPriceChart('brick',this)">ইট (হাজার)</button>
          <button class="inner-tab" onclick="showPriceChart('sand',this)">বালি (cft)</button>
        </div>
        <div class="chart-wrap" style="height:240px;"><canvas id="priceChart" role="img" aria-label="মূল্য ট্রেন্ড চার্ট"></canvas></div>
        <div id="price-forecast" style="margin-top:12px; padding:10px; background:var(--bg); border-radius:6px; font-size:13px;"></div>
      </div>
      <div class="card">
        <div class="card-title">📊 বর্তমান বাজার মূল্য (ঢাকা)</div>
        <div class="grid-4">
          <div style="text-align:center; padding:12px; background:var(--bg); border-radius:var(--radius-sm); border:1px solid var(--border);">
            <div style="font-size:11px; color:var(--text-muted);">রড (প্রতি kg)</div>
            <div style="font-size:20px; font-weight:700; color:var(--primary);">৳ ৯৫</div>
            <div style="font-size:10px; color:var(--success);">▲ ৩% মাসিক</div>
          </div>
          <div style="text-align:center; padding:12px; background:var(--bg); border-radius:var(--radius-sm); border:1px solid var(--border);">
            <div style="font-size:11px; color:var(--text-muted);">সিমেন্ট (বস্তা)</div>
            <div style="font-size:20px; font-weight:700; color:var(--primary);">৳ ৫২০</div>
            <div style="font-size:10px; color:var(--danger);">▼ ১% মাসিক</div>
          </div>
          <div style="text-align:center; padding:12px; background:var(--bg); border-radius:var(--radius-sm); border:1px solid var(--border);">
            <div style="font-size:11px; color:var(--text-muted);">ইট (প্রতি পিস)</div>
            <div style="font-size:20px; font-weight:700; color:var(--primary);">৳ ১৪</div>
            <div style="font-size:10px; color:var(--success);">▲ ২% মাসিক</div>
          </div>
          <div style="text-align:center; padding:12px; background:var(--bg); border-radius:var(--radius-sm); border:1px solid var(--border);">
            <div style="font-size:11px; color:var(--text-muted);">বালি (প্রতি cft)</div>
            <div style="font-size:20px; font-weight:700; color:var(--primary);">৳ ৩৮</div>
            <div style="font-size:10px; color:var(--text-muted);">→ স্থিতিশীল</div>
          </div>
        </div>
      </div>
    </div>

    <!-- ====== WEATHER (NEW) ====== -->
    <div class="section" id="section-weather">
      <div class="card">
        <div class="card-title">🌤️ আবহাওয়া ইন্টিগ্রেশন ও বিলম্ব প্রাক্কলন</div>
        <div class="weather-card">
          <div class="w-item"><div class="w-icon">🌧️</div><div class="w-label">বর্ষা মৌসুম</div><div class="w-val">জুন–সেপ্টেম্বর</div></div>
          <div class="w-item"><div class="w-icon">⛅</div><div class="w-label">শীতকাল</div><div class="w-val">নভে–ফেব্রুয়ারি</div></div>
          <div class="w-item"><div class="w-icon">☀️</div><div class="w-label">গ্রীষ্মকাল</div><div class="w-val">মার্চ–মে</div></div>
          <div class="w-item"><div class="w-icon">🌀</div><div class="w-label">সাইক্লোন ঝুঁকি</div><div class="w-val">মে, অক্টোবর–নভে</div></div>
        </div>
        <div style="margin-top:16px;">
          <div class="form-group"><label>নির্মাণ শুরুর মাস</label>
            <select id="start-month" onchange="calcWeatherDelay()">
              <option value="1">জানুয়ারি</option><option value="2">ফেব্রুয়ারি</option>
              <option value="3">মার্চ</option><option value="4">এপ্রিল</option>
              <option value="5">মে</option><option value="6">জুন</option>
              <option value="7">জুলাই</option><option value="8">আগস্ট</option>
              <option value="9">সেপ্টেম্বর</option><option value="10">অক্টোবর</option>
              <option value="11">নভেম্বর</option><option value="12">ডিসেম্বর</option>
            </select>
          </div>
        </div>
        <div id="weather-analysis" style="margin-top:14px;"></div>
      </div>
      <div class="card">
        <div class="card-title">📅 মাসিক কার্যকর কর্মদিন (ঐতিহাসিক গড়)</div>
        <div class="chart-wrap" style="height:200px;"><canvas id="workdayChart" role="img" aria-label="মাসিক কর্মদিন চার্ট"></canvas></div>
      </div>
    </div>

    <!-- ====== CHECKLIST (NEW) ====== -->
    <div class="section" id="section-checklist">
      <div class="card">
        <div class="card-title">✅ নির্মাণ কোয়ালিটি চেকলিস্ট <span class="badge">ISO মান</span></div>
        <div style="margin-bottom:12px; font-size:13px; color:var(--text-muted);">
          সম্পন্ন: <strong id="checklist-done">০</strong> / <strong id="checklist-total">০</strong> &nbsp;|&nbsp;
          <div class="progress-bar-wrap" style="display:inline-block; width:200px; vertical-align:middle;">
            <div class="progress-bar-fill" id="checklist-bar" style="width:0%; background:var(--primary);"></div>
          </div>
        </div>
        <div class="inner-tabs" id="checklist-phase-tabs"></div>
        <div id="checklist-container"></div>
      </div>
    </div>

    <!-- ====== COMPARE (NEW) ====== -->
    <div class="section" id="section-compare">
      <div class="card">
        <div class="card-title">📊 মাল্টি-প্রজেক্ট তুলনা ড্যাশবোর্ড <span class="badge">১০টি পর্যন্ত</span></div>
        <div style="margin-bottom:12px; display:flex; gap:8px;">
          <button class="btn btn-primary btn-sm" onclick="saveToCompare()">+ বর্তমান প্রজেক্ট যোগ করুন</button>
          <button class="btn btn-sm" style="background:var(--bg); border:1px solid var(--border);" onclick="clearCompare()">🗑️ সাফ করুন</button>
        </div>
        <div id="compare-container">
          <div class="alert alert-info" style="margin:0;">প্রজেক্ট হিসাব করুন, তারপর "+ বর্তমান প্রজেক্ট যোগ করুন" ক্লিক করুন।</div>
        </div>
      </div>
    </div>

    <!-- ====== BADGES (NEW) ====== -->
    <div class="section" id="section-badges">
      <div class="card">
        <div class="card-title">🏅 গেমিফিকেশন ব্যাজ ও অর্জন</div>
        <div class="badge-grid" id="badge-grid"></div>
      </div>
      <div class="card">
        <div class="card-title">📊 আপনার পরিসংখ্যান</div>
        <div class="grid-4">
          <div style="text-align:center; padding:14px; background:var(--bg); border-radius:var(--radius-sm);">
            <div style="font-size:28px; font-weight:700; color:var(--primary);" id="stat-calcs">০</div>
            <div style="font-size:12px; color:var(--text-muted);">মোট হিসাব</div>
          </div>
          <div style="text-align:center; padding:14px; background:var(--bg); border-radius:var(--radius-sm);">
            <div style="font-size:28px; font-weight:700; color:var(--accent);" id="stat-projects">০</div>
            <div style="font-size:12px; color:var(--text-muted);">সেভ করা প্রজেক্ট</div>
          </div>
          <div style="text-align:center; padding:14px; background:var(--bg); border-radius:var(--radius-sm);">
            <div style="font-size:28px; font-weight:700; color:var(--info);" id="stat-badges">০</div>
            <div style="font-size:12px; color:var(--text-muted);">অর্জিত ব্যাজ</div>
          </div>
          <div style="text-align:center; padding:14px; background:var(--bg); border-radius:var(--radius-sm);">
            <div style="font-size:28px; font-weight:700; color:var(--success);" id="stat-score">০</div>
            <div style="font-size:12px; color:var(--text-muted);">গড় স্কোর</div>
          </div>
        </div>
      </div>
    </div>

    <!-- ====== REPORT ====== -->
    <div class="section" id="section-report">
      <div class="report-header">
        <div style="font-size:22px; font-weight:700;">🏗️ নির্মাণ ব্যয় অনুমান রিপোর্ট</div>
        <div style="font-size:12px; opacity:0.8; margin-top:4px;" id="report-date"></div>
      </div>
      <div class="grid-2">
        <div class="card">
          <div class="card-title">📊 খরচ বিভাজন</div>
          <div class="chart-wrap" style="height:240px;"><canvas id="donutChart" role="img" aria-label="ডোনাট চার্ট"></canvas></div>
          <div id="donut-legend" style="margin-top:10px; display:flex; flex-wrap:wrap; gap:8px; font-size:11px;"></div>
        </div>
        <div class="card">
          <div class="card-title">📋 বিস্তারিত হিসাব</div>
          <div id="detailed-breakdown" style="font-size:13px;"></div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">🏢 তলা অনুযায়ী খরচ</div>
        <div class="chart-wrap" style="height:200px;"><canvas id="floorChart" role="img" aria-label="তলা চার্ট"></canvas></div>
      </div>
      <div class="card">
        <div class="card-title">📱 QR কোড রিপোর্ট <span class="badge">নতুন</span></div>
        <div class="grid-2">
          <div>
            <div id="qr-code" style="display:inline-block; padding:12px; background:#fff; border-radius:8px; border:1px solid var(--border);"></div>
            <div style="font-size:11px; color:var(--text-muted); margin-top:8px;">QR কোড স্ক্যান করুন — প্রজেক্ট ড্যাশবোর্ড খুলবে</div>
          </div>
          <div style="display:flex; flex-direction:column; gap:8px;">
            <button class="btn btn-primary" onclick="exportPDF()">📄 PDF রিপোর্ট</button>
            <button class="btn btn-outline" onclick="exportCSV()">📊 Excel (CSV)</button>
            <button class="btn btn-accent" onclick="exportBOQ()">📋 BOQ ডাউনলোড</button>
            <button class="btn btn-outline" onclick="printReport()">🖨️ প্রিন্ট</button>
            <button class="btn btn-info" onclick="shareReport()" style="color:#fff;">🔗 শেয়ার লিংক</button>
          </div>
        </div>
      </div>
    </div>

  </div>
</div>
</div>

<script>
// ===== CONSTANTS =====
const districts = {
  dhaka:['ঢাকা','গাজীপুর','নারায়ণগঞ্জ','মুন্সীগঞ্জ','মানিকগঞ্জ','নরসিংদী','কিশোরগঞ্জ','টাঙ্গাইল','ফরিদপুর','মাদারীপুর','শরীয়তপুর','রাজবাড়ী','গোপালগঞ্জ'],
  chittagong:['চট্টগ্রাম','কক্সবাজার','বান্দরবান','রাঙ্গামাটি','খাগড়াছড়ি','ফেনী','লক্ষ্মীপুর','নোয়াখালী','কুমিল্লা','চাঁদপুর','ব্রাহ্মণবাড়িয়া'],
  rajshahi:['রাজশাহী','নওগাঁ','নাটোর','চাঁপাইনবাবগঞ্জ','বগুড়া','পাবনা','সিরাজগঞ্জ','জয়পুরহাট'],
  khulna:['খুলনা','বাগেরহাট','সাতক্ষীরা','যশোর','ঝিনাইদহ','মেহেরপুর','চুয়াডাঙ্গা','কুষ্টিয়া','মাগুরা','নড়াইল'],
  barisal:['বরিশাল','পটুয়াখালী','পিরোজপুর','ঝালকাঠি','বরগুনা','ভোলা'],
  sylhet:['সিলেট','মৌলভীবাজার','হবিগঞ্জ','সুনামগঞ্জ'],
  rangpur:['রংপুর','দিনাজপুর','গাইবান্ধা','কুড়িগ্রাম','লালমনিরহাট','নীলফামারী','পঞ্চগড়','ঠাকুরগাঁও'],
  mymensingh:['ময়মনসিংহ','নেত্রকোনা','জামালপুর','শেরপুর']
};
const upazilas = {
  'ঢাকা':['মিরপুর','গুলশান','মতিঝিল','উত্তরা','ধানমন্ডি','মোহাম্মদপুর','লালবাগ','রমনা','সাভার','ডেমরা'],
  'চট্টগ্রাম':['কোতোয়ালি','পাঁচলাইশ','চান্দগাঁও','পতেঙ্গা','বায়েজিদ','হালিশহর','বন্দর','সীতাকুণ্ড'],
  'কক্সবাজার':['কক্সবাজার সদর','চকোরিয়া','রামু','উখিয়া','টেকনাফ','মহেশখালী'],
  'গাজীপুর':['গাজীপুর সদর','কালিয়াকৈর','কালীগঞ্জ','কাপাসিয়া','শ্রীপুর'],
  'নারায়ণগঞ্জ':['নারায়ণগঞ্জ সদর','আড়াইহাজার','বন্দর','রূপগঞ্জ','সোনারগাঁও'],
  'রাঙ্গামাটি':['রাঙ্গামাটি সদর','কাপ্তাই','বাঘাইছড়ি','বরকল','লংগদু'],
  'বান্দরবান':['বান্দরবান সদর','আলীকদম','নাইক্ষ্যংছড়ি','রোয়াংছড়ি','রুমা'],
  'সিলেট':['সিলেট সদর','বালাগঞ্জ','বিয়ানীবাজার','গোলাপগঞ্জ','জকিগঞ্জ'],
  'খুলনা':['খুলনা সদর','দাকোপ','কয়রা','পাইকগাছা','বটিয়াঘাটা'],
  'বরিশাল':['বরিশাল সদর','বানারীপাড়া','বাবুগঞ্জ','বাকেরগঞ্জ','হিজলা'],
  'রাজশাহী':['রাজশাহী সদর','বোয়ালমারী','পুঠিয়া','মোহনপুর','বাগমারা'],
  'রংপুর':['রংপুর সদর','কাউনিয়া','গঙ্গাচড়া','মিঠাপুকুর'],
  'ময়মনসিংহ':['ময়মনসিংহ সদর','ভালুকা','গফরগাঁও','ফুলবাড়িয়া','ত্রিশাল'],
};

const specialFeatures = {
  '1.0':[{n:'অতিরিক্ত রুম',c:80000},{n:'পার্কিং স্পেস',c:120000},{n:'ছাদ বাগান',c:150000},{n:'সিসি ক্যামেরা',c:35000},{n:'ফায়ার এক্সটিংগুইশার',c:10000},{n:'ইন্টারনেট ক্যাবলিং',c:25000},{n:'LED লাইটিং',c:45000},{n:'ইন্টারকম',c:20000},{n:'হুইলচেয়ার র্যাম্প',c:30000},{n:'সুইমিং পুল',c:1500000},{n:'হোম থিয়েটার',c:500000},{n:'স্মার্ট হোম অটোমেশন',c:300000}],
  '1.68':[{n:'আইসিইউ বেড (প্রতিটি)',c:500000},{n:'অ্যাম্বুলেন্স বে',c:200000},{n:'প্যাথলজি ল্যাব',c:1500000},{n:'অপারেশন থিয়েটার',c:3000000},{n:'অক্সিজেন লাইন',c:500000},{n:'ইমেজিং (এক্স-রে)',c:2000000},{n:'ফার্মেসি',c:300000},{n:'হুইলচেয়ার র্যাম্প',c:50000},{n:'এমার্জেন্সি জেনারেটর',c:500000},{n:'বায়ো-ওয়েস্ট ম্যানেজমেন্ট',c:400000},{n:'নার্স কলিং সিস্টেম',c:200000},{n:'নেগেটিভ প্রেসার রুম',c:800000}],
  '1.40':[{n:'কমার্শিয়াল কিচেন',c:2000000},{n:'জিম ও স্পা',c:1500000},{n:'কনফারেন্স হল',c:1000000},{n:'রেস্তোরাঁ',c:1500000},{n:'লবি ডেকোরেশন',c:800000},{n:'লন্ড্রি সিস্টেম',c:500000},{n:'রুফটপ পুল',c:3000000},{n:'ভ্যালেট পার্কিং',c:200000},{n:'স্মার্ট রুম অটোমেশন',c:100000},{n:'সাউন্ডপ্রুফ রুম',c:50000},{n:'অডিও ভিজুয়াল',c:500000},{n:'স্যাটেলাইট টিভি',c:200000}],
  '1.20':[{n:'লাইব্রেরি',c:500000},{n:'কম্পিউটার ল্যাব',c:1000000},{n:'সায়েন্স ল্যাব',c:800000},{n:'খেলার মাঠ',c:300000},{n:'স্মার্ট ক্লাসরুম',c:150000},{n:'অডিটোরিয়াম',c:2000000},{n:'সিসি ক্যামেরা',c:100000},{n:'শিক্ষক লাউঞ্জ',c:200000},{n:'স্কুল বাস বে',c:150000},{n:'ফায়ার অ্যালার্ম',c:80000},{n:'হুইলচেয়ার র্যাম্প',c:40000},{n:'স্মার্ট বোর্ড',c:80000}],
  '1.10':[{n:'মিনার (ছোট)',c:200000},{n:'সাউন্ড সিস্টেম',c:150000},{n:'মিহরাব (মার্বেল)',c:300000},{n:'মিম্বার (কাঠ)',c:80000},{n:'ওজুর স্থান',c:200000},{n:'ইমাম কক্ষ',c:80000},{n:'মহিলা সেকশন',c:300000},{n:'পানি ফিল্টার',c:30000},{n:'কুরআন তাক',c:50000},{n:'সিসি ক্যামেরা',c:40000},{n:'ঈদগাহ মাঠ',c:200000},{n:'জেনারেটর ব্যাকআপ',c:150000}],
  '1.05':[{n:'শ্রমিক ডর্মিটরি',c:1000000},{n:'ক্যান্টিন',c:500000},{n:'ডাস্ট কালেক্টর',c:800000},{n:'থ্রি-ফেজ সাবস্টেশন',c:2000000},{n:'ক্রেন ও হোয়েস্ট',c:1500000},{n:'লোডিং বে',c:500000},{n:'রাসায়নিক প্রতিরোধী মেঝে',c:300000},{n:'ভেন্টিলেশন সিস্টেম',c:600000},{n:'ফায়ার হাইড্র্যান্ট',c:200000},{n:'নিরাপত্তা গার্ড পোস্ট',c:80000},{n:'ETP বর্জ্য পরিশোধন',c:1500000},{n:'সোলার রুফটপ',c:500000}],
};

const checklist = {
  'ফাউন্ডেশন':[{t:'মাটি পরীক্ষা (Soil Test)'},{t:'লেআউট মার্কিং'},{t:'খনন ও এক্সক্যাভেশন'},{t:'পাইলিং (প্রযোজ্য হলে)'},{t:'ফুটিং ও কলাম বেস ঢালাই'},{t:'ফাউন্ডেশন ওয়াটারপ্রুফিং'}],
  'কলাম ও বিম':[{t:'রড বাইন্ডিং চেক'},{t:'ফর্মওয়ার্ক পরিদর্শন'},{t:'কংক্রিট মিক্স টেস্ট'},{t:'কলাম ঢালাই'},{t:'বিম ঢালাই'},{t:'কিউরিং (কমপক্ষে ৭ দিন)'}],
  'স্ল্যাব':[{t:'স্ল্যাব রড বাইন্ডিং'},{t:'ইলেকট্রিক/পানির পাইপ বসানো'},{t:'স্ল্যাব ঢালাই'},{t:'লেভেলিং ও ফিনিশিং'},{t:'স্ল্যাব লোড টেস্ট (প্রয়োজনে)'},{t:'ওয়াটারপ্রুফিং (ছাদের জন্য)'}],
  'প্লাস্টার ও ইট':[{t:'ইটের কাজ পরিদর্শন'},{t:'ভিতরের প্লাস্টার'},{t:'বাইরের প্লাস্টার'},{t:'সিলিং প্লাস্টার'},{t:'দরজা-জানালা ফ্রেম বসানো'},{t:'প্লাস্টার লেভেলিং চেক'}],
  'ইলেকট্রিক্যাল':[{t:'তার ক্যাবলিং চেক'},{t:'সুইচ বোর্ড ইনস্টলেশন'},{t:'আর্থিং সংযোগ'},{t:'লাইটিং ফিক্সচার'},{t:'ইলেকট্রিক লোড টেস্ট'},{t:'ফায়ার অ্যালার্ম (প্রযোজ্য)'}],
  'প্লাম্বিং':[{t:'পানির পাইপ লিকেজ চেক'},{t:'স্যানিটারি ফিটিং'},{t:'বাথরুম ওয়াটারপ্রুফিং'},{t:'ওভারহেড ট্যাংক সংযোগ'},{t:'পয়ঃনিষ্কাশন পরীক্ষা'},{t:'গ্যাস লাইন চেক (প্রযোজ্য)'}],
  'ফিনিশিং':[{t:'টাইলস বসানো পরিদর্শন'},{t:'পেইন্টিং গুণমান চেক'},{t:'দরজা-জানালা পরিষ্কার'},{t:'গ্রিল ও হ্যান্ডরেইল'},{t:'সাইট পরিষ্কার'},{t:'চূড়ান্ত হস্তান্তর পরিদর্শন'}],
};

// State
let currency = 'BDT';
const rates = {BDT:1, USD:0.0091, INR:0.76};
const sym = {BDT:'৳', USD:'$', INR:'₹'};
function fmt(n) {
  const v = n * rates[currency];
  const s = sym[currency];
  if(currency==='BDT') return s+' '+Math.round(v).toLocaleString();
  return s+' '+v.toFixed(2);
}

let laborData = [
  {name:'হেড মিস্ত্রি',count:2,wage:1200,days:120},
  {name:'রড বাইন্ডার',count:4,wage:900,days:90},
  {name:'ইলেকট্রিশিয়ান',count:2,wage:1000,days:45},
  {name:'প্লাম্বার',count:2,wage:950,days:40},
  {name:'পেইন্টার',count:3,wage:800,days:30},
  {name:'হেল্পার',count:6,wage:600,days:120},
];
let milestones = [
  {name:'অগ্রিম (মোবিলাইজেশন)',pct:20,date:'',status:'pending'},
  {name:'ফাউন্ডেশন সম্পন্ন',pct:25,date:'',status:'pending'},
  {name:'কাঠামো সম্পন্ন',pct:25,date:'',status:'pending'},
  {name:'প্লাস্টার ও ইলেকট্রিক',pct:20,date:'',status:'pending'},
  {name:'চূড়ান্ত হস্তান্তর',pct:10,date:'',status:'pending'},
];
let compareProjects = [];
let calcCount = 0, savedCount = 0;
let badgesEarned = [];
let checklistState = {};
let priceChartObj = null, donutChartObj = null, matChartObj = null, floorChartObj = null, workdayChartObj = null;
let lastTotal = 0;

// Price history data (last 12 months, illustrative Bangladesh market data)
const priceHistory = {
  rod:   [82,84,85,87,88,90,88,92,93,91,93,95],
  cement:[510,512,515,518,520,522,518,520,525,522,518,520],
  brick: [12500,12600,12700,12800,12800,13000,13200,13500,13800,14000,14000,14000],
  sand:  [36,36,37,37,38,38,38,38,38,38,38,38],
};
const months = ['জুন','জুলাই','আগস্ট','সেপ্টে','অক্টো','নভে','ডিসে','জানু','ফেব্রু','মার্চ','এপ্রিল','মে'];
const workdays = [26,26,26,25,24,22,20,18,18,22,24,25]; // monthly effective workdays considering rain

// Theme
function toggleTheme() {
  const html = document.documentElement;
  const isDark = html.getAttribute('data-theme') === 'dark';
  html.setAttribute('data-theme', isDark ? 'light' : 'dark');
  document.getElementById('themeBtn').classList.toggle('dark', !isDark);
  try { localStorage.setItem('nirman-theme', isDark ? 'light' : 'dark'); } catch(e){}
}

// Currency
function setCurrency(c, el) {
  currency = c;
  document.querySelectorAll('.cur-btn').forEach(b => b.classList.remove('active'));
  if(el) el.classList.add('active');
  recalculate();
}

// Navigation
const pageTitles = {
  location:['লোকেশন ও পরিবেশ','এলাকা নির্বাচন করুন'],
  building:['বিল্ডিং কনফিগারেশন','বিল্ডিং ধরণ ও আয়তন'],
  materials:['ম্যাটেরিয়াল টেকঅফ','স্বয়ংক্রিয় হিসাব'],
  labor:['শ্রমিক ও যন্ত্রপাতি','শ্রমিক মজুরি হিসাব'],
  extras:['অতিরিক্ত সুবিধা','সোলার, জেনারেটর, ইন্টেরিয়র'],
  floorfinish:['তলা অনুযায়ী ফিনিশিং','প্রতি তলার আলাদা উপকরণ'],
  special:['স্পেশাল ফিচারস','বিল্ডিং টাইপ ভিত্তিক'],
  financial:['আর্থিক ও সরকারি ফি','ভ্যাট, রাজউক, ঋণ'],
  boq:['BOQ জেনারেটর','Bill of Quantity'],
  contract:['কন্ট্রাক্ট ম্যানেজমেন্ট','পেমেন্ট মাইলস্টোন'],
  ai:['AI নির্মাণ উপদেষ্টা','Claude AI দিয়ে পরামর্শ'],
  prices:['মূল্য ট্রেন্ড','গত ১২ মাসের বাজার বিশ্লেষণ'],
  weather:['আবহাওয়া ও বিলম্ব','নির্মাণ বিলম্ব প্রাক্কলন'],
  checklist:['কোয়ালিটি চেকলিস্ট','ISO মান অনুসরণ'],
  compare:['মাল্টি-প্রজেক্ট তুলনা','পাশাপাশি বিশ্লেষণ'],
  badges:['গেমিফিকেশন ব্যাজ','আপনার অর্জনসমূহ'],
  report:['রিপোর্ট ও QR কোড','সম্পূর্ণ রিপোর্ট'],
};
function showSection(name) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  const sec = document.getElementById('section-'+name);
  if(sec) sec.classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n => {
    if(n.getAttribute('onclick') === `showSection('${name}')`) n.classList.add('active');
  });
  const t = pageTitles[name];
  if(t) { document.getElementById('page-title').textContent = t[0]; document.getElementById('page-sub').textContent = t[1]; }
  if(name==='boq') renderBOQ();
  if(name==='contract') renderMilestones();
  if(name==='weather') { calcWeatherDelay(); renderWorkdayChart(); }
  if(name==='checklist') renderChecklist();
  if(name==='badges') renderBadges();
  if(name==='prices') showPriceChart('rod', document.querySelector('.inner-tab'));
  if(name==='report') { renderReport(); generateQR(); }
  recalculate();
}

// Location
function updateDistricts() {
  const div = document.getElementById('division').value;
  const dsel = document.getElementById('district');
  dsel.innerHTML = '<option value="">-- জেলা --</option>';
  (districts[div]||[]).forEach(d => { dsel.innerHTML += `<option value="${d}">${d}</option>`; });
  document.getElementById('upazila').innerHTML = '<option value="">-- উপজেলা --</option>';
  recalculate();
}
function updateUpazilas() {
  const dist = document.getElementById('district').value;
  const usel = document.getElementById('upazila');
  usel.innerHTML = '<option value="">-- উপজেলা --</option>';
  (upazilas[dist]||[]).forEach(u => { usel.innerHTML += `<option value="${u}">${u}</option>`; });
  recalculate();
}

// Labor
function renderLaborList() {
  const el = document.getElementById('labor-list');
  if(!el) return;
  el.innerHTML = laborData.map((l,i) => `
    <div class="labor-row">
      <input type="text" value="${l.name}" onchange="laborData[${i}].name=this.value">
      <input type="number" value="${l.count}" min="1" onchange="laborData[${i}].count=+this.value; recalculate()">
      <input type="number" value="${l.wage}" onchange="laborData[${i}].wage=+this.value; recalculate()">
      <input type="number" value="${l.days}" onchange="laborData[${i}].days=+this.value; recalculate()">
      <span class="labor-total-cell">৳ ${Math.round(l.count*l.wage*l.days).toLocaleString()}</span>
      <button onclick="laborData.splice(${i},1); renderLaborList(); recalculate();" style="background:none; border:none; cursor:pointer; color:var(--danger); font-size:16px;">×</button>
    </div>`).join('');
}
function addLaborRow() {
  laborData.push({name:'নতুন শ্রমিক',count:1,wage:700,days:30});
  renderLaborList(); recalculate();
}
function resetLabor() {
  laborData = [{name:'হেড মিস্ত্রি',count:2,wage:1200,days:120},{name:'রড বাইন্ডার',count:4,wage:900,days:90},{name:'ইলেকট্রিশিয়ান',count:2,wage:1000,days:45},{name:'প্লাম্বার',count:2,wage:950,days:40},{name:'পেইন্টার',count:3,wage:800,days:30},{name:'হেল্পার',count:6,wage:600,days:120}];
  renderLaborList(); recalculate();
}

// Special features
function onBuildingTypeChange() { renderSpecialFeatures(); recalculate(); }
function renderSpecialFeatures() {
  const btype = document.getElementById('bldg-type').value;
  const feats = specialFeatures[btype] || specialFeatures['1.0'];
  const title = document.getElementById('bldg-type').options[document.getElementById('bldg-type').selectedIndex].text;
  const st = document.getElementById('special-title');
  if(st) st.innerHTML = `⭐ স্পেশাল ফিচারস (${title})`;
  const cont = document.getElementById('special-features');
  if(!cont) return;
  cont.innerHTML = feats.map((f,i) => `
    <div class="feature-item" id="feat-${i}" onclick="toggleFeat(${i})">
      <div class="feature-item-top">
        <input type="checkbox" id="fchk-${i}" onclick="event.stopPropagation()">
        <span>${f.n}</span>
      </div>
      <div class="feature-cost">৳ ${f.c.toLocaleString()}</div>
    </div>`).join('');
}
function toggleFeat(i) {
  const chk = document.getElementById('fchk-'+i);
  const item = document.getElementById('feat-'+i);
  if(chk) chk.checked = !chk.checked;
  if(item) item.classList.toggle('selected', chk && chk.checked);
  recalculate();
}
function getSpecialTotal() {
  const btype = document.getElementById('bldg-type').value;
  const feats = specialFeatures[btype] || specialFeatures['1.0'];
  return feats.reduce((s,f,i) => {
    const chk = document.getElementById('fchk-'+i);
    return s + (chk && chk.checked ? f.c : 0);
  }, 0);
}

// Floor finishing
function renderFloorFinish() {
  const floors = +document.getElementById('floors').value || 1;
  const cont = document.getElementById('floor-finish-list');
  if(!cont) return;
  const flooring = ['মার্বেল (+৳৮০/sqft)','সিরামিক টাইলস (+৳৪৫/sqft)','গ্রানাইট (+৳১৫০/sqft)','ভিনাইল (+৳৩০/sqft)','মসৃণ সিমেন্ট (স্ট্যান্ডার্ড)'];
  const walls = ['মার্বেল ক্ল্যাডিং (+৳৬০/sqft)','সিরামিক টাইলস (+৳৪০/sqft)','ইটালিয়ান টাইলস (+৳৯০/sqft)','পেইন্ট (স্ট্যান্ডার্ড)'];
  const ceiling = ['ফলস সিলিং (+৳৫৫/sqft)','গাছ সিলিং (+৳৮০/sqft)','সাধারণ (স্ট্যান্ডার্ড)'];
  cont.innerHTML = Array.from({length:Math.min(floors,15)},(_,i) => `
    <div class="floor-finish-row">
      <span style="font-weight:600;">${i===0?'নিচতলা':i+' তলা'}</span>
      <select id="ff-floor-${i}" onchange="calcFinishExtra()">
        ${flooring.map((f,j) => `<option value="${[80,45,150,30,0][j]}">${f}</option>`).join('')}
      </select>
      <select id="ff-wall-${i}" onchange="calcFinishExtra()">
        ${walls.map((w,j) => `<option value="${[60,40,90,0][j]}">${w}</option>`).join('')}
      </select>
      <select id="ff-ceil-${i}" onchange="calcFinishExtra()">
        ${ceiling.map((c,j) => `<option value="${[55,80,0][j]}">${c}</option>`).join('')}
      </select>
      <span id="ff-cost-${i}" style="font-weight:700; color:var(--primary-dark); font-size:12px;">৳ ০</span>
    </div>`).join('');
  calcFinishExtra();
}
function calcFinishExtra() {
  const floors = +document.getElementById('floors').value || 1;
  const sqft = +document.getElementById('total-area').value || 0;
  const sqftPerFloor = sqft / floors;
  let total = 0;
  for(let i=0; i<Math.min(floors,15); i++) {
    const fv = +(document.getElementById('ff-floor-'+i)||{}).value || 0;
    const wv = +(document.getElementById('ff-wall-'+i)||{}).value || 0;
    const cv = +(document.getElementById('ff-ceil-'+i)||{}).value || 0;
    const cost = (fv+wv+cv) * sqftPerFloor;
    total += cost;
    const costEl = document.getElementById('ff-cost-'+i);
    if(costEl) costEl.textContent = '৳ '+Math.round(cost).toLocaleString();
  }
  const totalEl = document.getElementById('finish-extra-total');
  if(totalEl) totalEl.textContent = fmt(total);
  recalculate();
  return total;
}
function getFinishExtra() {
  const floors = +document.getElementById('floors').value || 1;
  const sqft = +document.getElementById('total-area').value || 0;
  const sqftPerFloor = sqft / floors;
  let total = 0;
  for(let i=0; i<Math.min(floors,15); i++) {
    const fv = +(document.getElementById('ff-floor-'+i)||{}).value || 0;
    const wv = +(document.getElementById('ff-wall-'+i)||{}).value || 0;
    const cv = +(document.getElementById('ff-ceil-'+i)||{}).value || 0;
    total += (fv+wv+cv) * sqftPerFloor;
  }
  return total;
}

// Materials
function calcMaterials(sqft) {
  const brickRate = +document.getElementById('brick-brand').value || 14;
  const cementRate = +document.getElementById('cement-brand').value || 520;
  const rodFactor = +document.getElementById('rod-dia').value || 1.0;
  return [
    {n:'ইট',qty:Math.round(sqft*0.35*50.8),u:'পিস',r:brickRate,total:Math.round(sqft*0.35*50.8)*brickRate},
    {n:'সিমেন্ট',qty:Math.round(sqft*0.38),u:'বস্তা',r:cementRate,total:Math.round(sqft*0.38)*cementRate},
    {n:'বালি',qty:Math.round(sqft*1.2),u:'cft',r:38,total:Math.round(sqft*1.2)*38},
    {n:'পাথর/খোয়া',qty:Math.round(sqft*0.8),u:'cft',r:55,total:Math.round(sqft*0.8)*55},
    {n:'রড (Fe500)',qty:Math.round(sqft*4.5*rodFactor),u:'kg',r:95,total:Math.round(sqft*4.5*rodFactor)*95},
    {n:'টাইলস',qty:Math.round(sqft*0.65),u:'sqft',r:85,total:Math.round(sqft*0.65)*85},
    {n:'পেইন্ট',qty:Math.round(sqft*0.12),u:'লিটার',r:280,total:Math.round(sqft*0.12)*280},
    {n:'ইলেকট্রিক তার',qty:Math.round(sqft*2.5),u:'মিটার',r:45,total:Math.round(sqft*2.5)*45},
    {n:'স্যানিটারি সেট',qty:Math.max(1,Math.round(sqft/500)),u:'সেট',r:35000,total:Math.max(1,Math.round(sqft/500))*35000},
    {n:'দরজা',qty:+document.getElementById('doors').value||8,u:'টি',r:12000,total:(+document.getElementById('doors').value||8)*12000},
    {n:'জানালা',qty:+document.getElementById('windows').value||12,u:'টি',r:8000,total:(+document.getElementById('windows').value||12)*8000},
  ];
}

// MAIN CALC
function recalculate() {
  calcCount++;
  const sqft = +document.getElementById('total-area').value || 0;
  const floors = +document.getElementById('floors').value || 1;
  const baseRate = +document.getElementById('base-rate').value || 2200;
  const btype = +document.getElementById('bldg-type').value || 1.0;
  const quality = +document.getElementById('quality').value || 1.0;
  const structure = +document.getElementById('structure').value || 1.0;
  const foundation = +document.getElementById('foundation').value || 0.12;
  const cgrade = +document.getElementById('concrete-grade').value || 1.08;
  const areaType = +document.getElementById('area-type').value || 1.0;
  const seismic = +document.getElementById('seismic-zone').value || 1.05;
  const flood = +document.getElementById('flood-risk').value || 1.10;
  const specEnv = +document.getElementById('special-env').value || 1.0;
  const lifts = +document.getElementById('lifts').value || 0;
  const vat = +document.getElementById('vat').value || 15;
  const contingency = +document.getElementById('contingency').value || 5;
  const margin = +document.getElementById('margin').value || 10;
  const inflation = +document.getElementById('inflation').value || 3;
  const landPrice = +document.getElementById('land-price').value || 0;
  const gasDist = +document.getElementById('gas-dist').value || 0;

  // Env
  const envFactor = areaType * seismic * flood * specEnv;
  const ef = id => document.getElementById(id);
  if(ef('ef1')) ef('ef1').textContent = areaType.toFixed(2);
  if(ef('ef2')) ef('ef2').textContent = seismic.toFixed(2);
  if(ef('ef3')) ef('ef3').textContent = flood.toFixed(2);
  if(ef('ef4')) ef('ef4').textContent = specEnv.toFixed(2);
  if(ef('env-combined')) ef('env-combined').textContent = envFactor.toFixed(3);

  const configFactor = btype * quality * structure * cgrade * envFactor * (1 + foundation);
  if(ef('config-factor')) ef('config-factor').value = configFactor.toFixed(3);

  const baseCost = sqft * baseRate * configFactor;

  // Materials
  const mats = calcMaterials(sqft);
  const matTotal = mats.reduce((s,m) => s+m.total, 0);
  const tbody = document.getElementById('mat-tbody');
  if(tbody) {
    tbody.innerHTML = mats.map((m,i) => `<tr>
      <td style="color:var(--text-muted)">${i+1}</td>
      <td>${m.n}</td><td class="qty" style="color:var(--text-muted)">${m.qty.toLocaleString()}</td>
      <td style="color:var(--text-muted)">${m.u}</td>
      <td style="color:var(--text-muted)">৳ ${m.r.toLocaleString()}</td>
      <td class="amt">৳ ${m.total.toLocaleString()}</td>
    </tr>`).join('') + `<tr style="background:var(--bg);">
      <td colspan="5" style="font-weight:700; color:var(--primary-dark); padding:8px 12px;">মোট</td>
      <td class="amt" style="font-size:14px; color:var(--primary);">৳ ${matTotal.toLocaleString()}</td>
    </tr>`;
  }

  // Labor
  let laborTotal = 0, totalManday = 0;
  laborData.forEach(l => { laborTotal += l.count*l.wage*l.days; totalManday += l.count*l.days; });
  const craneHrs = +document.getElementById('crane-hrs').value||0;
  const mixerDays = +document.getElementById('mixer-days').value||0;
  const pumpDays = +document.getElementById('pump-days').value||0;
  const vibDays = +document.getElementById('vib-days').value||0;
  const equipTotal = craneHrs*3500+mixerDays*1800+pumpDays*8000+vibDays*500;
  const totalLabor = laborTotal + equipTotal;
  if(ef('equip-total')) ef('equip-total').textContent = '৳ '+Math.round(equipTotal).toLocaleString();
  if(ef('total-manday')) ef('total-manday').textContent = Math.round(totalManday).toLocaleString();
  const avgW = Math.max(1, Math.round(totalManday/120));
  const estMonths = Math.max(1, Math.round(totalManday/avgW/25));
  if(ef('est-months')) ef('est-months').textContent = estMonths+' মাস';
  if(ef('construction-time')) ef('construction-time').textContent = estMonths+' মাস';
  if(ef('manday-info')) ef('manday-info').textContent = 'ম্যান-ডে: '+Math.round(totalManday).toLocaleString();

  // Extras
  const solar = (+document.getElementById('solar-kw').value||0)*80000;
  const gen = (+document.getElementById('gen-kva').value||0)*15000;
  const boundary = (+document.getElementById('boundary').value||0)*600;
  const interior = (+document.getElementById('interior').value||0)*sqft;
  const tank = Math.round((+document.getElementById('tank').value||0)/1000)*12000;
  const landscape = (+document.getElementById('landscape').value||0)*120;
  const bedrooms = (+document.getElementById('bedrooms').value||0)*80000;
  const doors = (+document.getElementById('doors').value||0)*12000;
  const windows = (+document.getElementById('windows').value||0)*8000;
  const bathrooms = (+document.getElementById('bathrooms').value||0)*60000;
  const liftCost = lifts*2500000;
  const extrasTotal = solar+gen+boundary+interior+tank+landscape+bedrooms+doors+windows+bathrooms+liftCost;

  const specialTotal = getSpecialTotal();
  const finishExtra = getFinishExtra();
  if(ef('special-total')) ef('special-total').textContent = fmt(specialTotal);
  if(ef('br-finish')) ef('br-finish').textContent = fmt(finishExtra);

  // Govt fees
  const rajukFee = sqft*floors*15+(floors>5?(floors-5)*sqft*5:0);
  const wasaFee = 30000;
  const elecFee = sqft>5000?150000:50000;
  const gasFee = 40000+gasDist*800;
  const regFee = landPrice*0.07;
  const stampFee = landPrice*0.015;
  const govtTotal = rajukFee+wasaFee+elecFee+gasFee+regFee+stampFee+5000;

  if(ef('rajuk-fee')) ef('rajuk-fee').textContent = '৳ '+Math.round(rajukFee).toLocaleString();
  if(ef('elec-fee')) ef('elec-fee').textContent = '৳ '+Math.round(elecFee).toLocaleString();
  if(ef('gas-fee')) ef('gas-fee').textContent = '৳ '+Math.round(gasFee).toLocaleString();
  if(ef('reg-fee')) ef('reg-fee').textContent = '৳ '+Math.round(regFee).toLocaleString();
  if(ef('stamp-fee')) ef('stamp-fee').textContent = '৳ '+Math.round(stampFee).toLocaleString();
  if(ef('total-govt')) ef('total-govt').textContent = '৳ '+Math.round(govtTotal).toLocaleString();

  const subTotal = baseCost+totalLabor+extrasTotal+specialTotal+finishExtra;
  const vatAmt = subTotal*vat/100;
  const conAmt = subTotal*contingency/100;
  const marAmt = subTotal*margin/100;
  const infAmt = subTotal*inflation/100;
  const chargesTotal = vatAmt+conAmt+marAmt+infAmt;
  const grandTotal = subTotal+chargesTotal+govtTotal;
  const perSqft = sqft>0 ? grandTotal/sqft : 0;
  lastTotal = grandTotal;

  if(ef('total-cost')) ef('total-cost').textContent = fmt(grandTotal);
  if(ef('cost-per-sqft')) ef('cost-per-sqft').textContent = 'প্রতি sqft: '+fmt(perSqft);
  if(ef('area-factor')) ef('area-factor').textContent = envFactor.toFixed(2);
  if(ef('zone-info')) ef('zone-info').textContent = 'জোন: '+document.getElementById('seismic-zone').options[document.getElementById('seismic-zone').selectedIndex].text.split(' ')[0];
  if(ef('govt-cost')) ef('govt-cost').textContent = fmt(govtTotal+chargesTotal);

  // Score calculation
  let score = 0;
  if(sqft>0) score+=20;
  if(document.getElementById('district').value) score+=15;
  if(laborData.length>0) score+=15;
  if(interior>0) score+=10;
  if(solar>0) score+=10;
  if(getSpecialTotal()>0) score+=10;
  if(vat>0) score+=5;
  if(landPrice>0) score+=5;
  if(calcCount>5) score+=5;
  if(calcCount>20) score+=5;
  if(ef('project-score')) ef('project-score').textContent = score+'/১০০';
  if(ef('score-label')) ef('score-label').textContent = score>=80?'চমৎকার! 🎉':score>=60?'ভালো! 👍':score>=40?'অগ্রগতি চলছে':'শুরু করুন';

  // Breakdown
  [{id:'br-base',v:baseCost},{id:'br-labor',v:totalLabor},{id:'br-extras',v:extrasTotal},
   {id:'br-special',v:specialTotal},{id:'br-vat',v:chargesTotal},{id:'br-govt',v:govtTotal},{id:'br-total',v:grandTotal}
  ].forEach(({id,v}) => { if(ef(id)) ef(id).textContent = fmt(v); });

  updateCharts({base:baseCost,labor:totalLabor,extras:extrasTotal,special:specialTotal,finish:finishExtra,vat:chargesTotal,govt:govtTotal},floors,grandTotal);

  // Badges check
  checkBadges(grandTotal, sqft, floors, score);

  // Labor rows update
  renderLaborList();
}

// Charts
function updateCharts(b, floors, total) {
  const colors = ['#1a6b3a','#e8a020','#3b82f6','#ef4444','#8b5cf6','#14b8a6','#f97316'];
  const labels = ['মূল নির্মাণ','শ্রমিক ও যন্ত্র','অতিরিক্ত','স্পেশাল','তলা ফিনিশিং','ভ্যাট ও চার্জ','সরকারি ফি'];
  const vals = [b.base,b.labor,b.extras,b.special,b.finish||0,b.vat,b.govt];

  // Donut
  if(donutChartObj) donutChartObj.destroy();
  const dc = document.getElementById('donutChart');
  if(dc) {
    donutChartObj = new Chart(dc, {type:'doughnut', data:{labels, datasets:[{data:vals, backgroundColor:colors, borderWidth:2, borderColor:document.documentElement.getAttribute('data-theme')==='dark'?'#162a1c':'#fff'}]}, options:{responsive:true, maintainAspectRatio:false, plugins:{legend:{display:false}}}});
    const leg = document.getElementById('donut-legend');
    if(leg) leg.innerHTML = labels.map((l,i) => `<span style="display:flex;align-items:center;gap:3px;"><span style="width:8px;height:8px;border-radius:2px;background:${colors[i]};display:inline-block;"></span>${l} ${total>0?Math.round(vals[i]/total*100):0}%</span>`).join('');
  }

  // Floor chart
  if(floorChartObj) floorChartObj.destroy();
  const fc = document.getElementById('floorChart');
  if(fc) {
    const fLabels = [], fData = [];
    const bpc = b.base/floors;
    for(let i=1;i<=Math.min(floors,12);i++) { fLabels.push(i===0?'নিচতলা':i+' তলা'); fData.push(Math.round(bpc*(i===1?1.15:i<=3?1.0:0.92))); }
    floorChartObj = new Chart(fc, {type:'bar', data:{labels:fLabels, datasets:[{label:'খরচ (৳)',data:fData,backgroundColor:'#2d9653',borderRadius:5}]}, options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{ticks:{callback:v=>'৳'+Math.round(v/100000)+'লা'}},x:{ticks:{autoSkip:false}}}}});
  }

  // Material chart
  if(matChartObj) matChartObj.destroy();
  const mc = document.getElementById('matChart');
  if(mc) {
    const mats = calcMaterials(+document.getElementById('total-area').value||2000);
    matChartObj = new Chart(mc, {type:'bar', data:{labels:mats.map(m=>m.n), datasets:[{label:'৳',data:mats.map(m=>m.total),backgroundColor:colors,borderRadius:4}]}, options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{ticks:{callback:v=>'৳'+Math.round(v/1000)+'হা'}},x:{ticks:{autoSkip:false,maxRotation:30}}}}});
  }
}

// BOQ
function renderBOQ() {
  const sqft = +document.getElementById('total-area').value||0;
  const mats = calcMaterials(sqft);
  const floors = +document.getElementById('floors').value||1;
  const cont = document.getElementById('boq-container');
  if(!cont) return;
  const grandTotal = lastTotal;
  let html = `<table class="boq-table"><thead><tr><th>#</th><th>বিবরণ</th><th>পরিমাণ</th><th>একক</th><th>একক দর (৳)</th><th>মোট (৳)</th></tr></thead><tbody>`;
  html += `<tr class="section-row"><td colspan="6">ক) ম্যাটেরিয়াল</td></tr>`;
  mats.forEach((m,i) => { html += `<tr><td>${i+1}</td><td>${m.n}</td><td>${m.qty.toLocaleString()}</td><td>${m.u}</td><td>${m.r.toLocaleString()}</td><td style="text-align:right; font-weight:600;">৳ ${m.total.toLocaleString()}</td></tr>`; });
  html += `<tr class="section-row"><td colspan="6">খ) শ্রমিক ও যন্ত্রপাতি</td></tr>`;
  let lnum = mats.length+1;
  laborData.forEach(l => { html += `<tr><td>${lnum++}</td><td>${l.name}</td><td>${l.count} জন × ${l.days} দিন</td><td>মজুরি</td><td>${l.wage.toLocaleString()}</td><td style="text-align:right; font-weight:600;">৳ ${(l.count*l.wage*l.days).toLocaleString()}</td></tr>`; });
  html += `<tr class="section-row"><td colspan="6">গ) অতিরিক্ত সুবিধা</td></tr>`;
  const lifts = +document.getElementById('lifts').value||0;
  if(lifts>0) html += `<tr><td>${lnum++}</td><td>লিফট</td><td>${lifts} টি</td><td>সেট</td><td>২৫,০০,০০০</td><td style="text-align:right; font-weight:600;">৳ ${(lifts*2500000).toLocaleString()}</td></tr>`;
  const solar = +document.getElementById('solar-kw').value||0;
  if(solar>0) html += `<tr><td>${lnum++}</td><td>সোলার প্যানেল</td><td>${solar} kW</td><td>kW</td><td>৮০,০০০</td><td style="text-align:right; font-weight:600;">৳ ${(solar*80000).toLocaleString()}</td></tr>`;
  const sp = getSpecialTotal();
  if(sp>0) html += `<tr><td>${lnum++}</td><td>স্পেশাল ফিচারস (সমষ্টি)</td><td>—</td><td>—</td><td>—</td><td style="text-align:right; font-weight:600;">৳ ${sp.toLocaleString()}</td></tr>`;
  html += `<tr class="total-row"><td colspan="5">সর্বমোট নির্মাণ ব্যয়</td><td style="text-align:right;">৳ ${Math.round(grandTotal).toLocaleString()}</td></tr>`;
  html += `</tbody></table>`;
  cont.innerHTML = html;
}

function exportBOQ() {
  const sqft = +document.getElementById('total-area').value||0;
  const mats = calcMaterials(sqft);
  const rows = [['ক্রম','বিবরণ','পরিমাণ','একক','দর (৳)','মোট (৳)']];
  mats.forEach((m,i) => rows.push([i+1,m.n,m.qty,m.u,m.r,m.total]));
  laborData.forEach((l,i) => rows.push([mats.length+i+1,l.name,l.count+'জন×'+l.days+'দিন','মজুরি',l.wage,l.count*l.wage*l.days]));
  const csv = rows.map(r => r.join(',')).join('\n');
  const blob = new Blob(['\ufeff'+csv], {type:'text/csv;charset=utf-8'});
  const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = 'BOQ_nirman.csv'; a.click();
}
function printBOQ() { window.print(); }

// Contract
function renderMilestones() {
  const cont = document.getElementById('milestone-list');
  if(!cont) return;
  const total = lastTotal;
  cont.innerHTML = milestones.map((m,i) => {
    const amt = Math.round(total*m.pct/100);
    return `<div class="milestone-row">
      <input type="text" value="${m.name}" onchange="milestones[${i}].name=this.value">
      <span style="font-weight:700; color:var(--primary-dark);">৳ ${amt.toLocaleString()} (${m.pct}%)</span>
      <input type="text" value="${m.date}" placeholder="তারিখ" onchange="milestones[${i}].date=this.value">
      <select onchange="milestones[${i}].status=this.value; renderMilestones()">
        <option value="pending" ${m.status==='pending'?'selected':''}>অপেক্ষমান</option>
        <option value="ongoing" ${m.status==='ongoing'?'selected':''}>চলমান</option>
        <option value="done" ${m.status==='done'?'selected':''}>সম্পন্ন</option>
      </select>
    </div>`;
  }).join('');
  const smry = document.getElementById('contract-summary');
  if(smry) {
    const paid = milestones.filter(m=>m.status==='done').reduce((s,m)=>s+m.pct,0);
    smry.style.display='block';
    smry.innerHTML = `পরিশোধিত: <strong>${paid}%</strong> | অপেক্ষমান: <strong>${100-paid}%</strong> | মোট চুক্তি: <strong>৳ ${Math.round(lastTotal).toLocaleString()}</strong>`;
  }
}
function addMilestone() {
  milestones.push({name:'নতুন মাইলস্টোন',pct:5,date:'',status:'pending'});
  renderMilestones();
}
function generateContract() {
  const cn = document.getElementById('contractor-name').value||'[ঠিকাদারের নাম]';
  const cd = document.getElementById('contract-date').value||'[তারিখ]';
  const total = Math.round(lastTotal);
  const area = document.getElementById('total-area').value;
  alert(`চুক্তিপত্র তৈরি হয়েছে!\n\nঠিকাদার: ${cn}\nতারিখ: ${cd}\nমোট চুক্তিমূল্য: ৳ ${total.toLocaleString()}\nনির্মাণ আয়তন: ${area} sqft\n\n(সম্পূর্ণ চুক্তিপত্রের জন্য PDF ডাউনলোড করুন)`);
}

// AI
async function sendAI() {
  const input = document.getElementById('ai-input');
  const msg = input.value.trim();
  if(!msg) return;
  input.value = '';
  addAIMsg(msg, 'user');
  addAIMsg('বিশ্লেষণ করছি...', 'bot typing');
  const context = `আপনি একজন বাংলাদেশের নির্মাণ বিশেষজ্ঞ। প্রজেক্টের তথ্য: আয়তন=${document.getElementById('total-area').value} sqft, তলা=${document.getElementById('floors').value}, মান=${document.getElementById('quality').options[document.getElementById('quality').selectedIndex].text}, এলাকা=${document.getElementById('district').value||'অজ্ঞাত'}, মোট খরচ=৳${Math.round(lastTotal).toLocaleString()}। বাংলায় সংক্ষিপ্ত ও বাস্তবসম্মত পরামর্শ দিন।`;
  try {
    const res = await fetch('https://api.anthropic.com/v1/messages', {
      method:'POST', headers:{'Content-Type':'application/json'},
      body: JSON.stringify({model:'claude-sonnet-4-20250514', max_tokens:1000, messages:[{role:'user',content:`${context}\n\nপ্রশ্ন: ${msg}`}]})
    });
    const data = await res.json();
    const reply = data.content?.[0]?.text || 'দুঃখিত, উত্তর পেতে সমস্যা হয়েছে।';
    removeTyping();
    addAIMsg(reply, 'bot');
  } catch(e) {
    removeTyping();
    addAIMsg(`প্রজেক্টের ডেটা বিশ্লেষণ করে পরামর্শ:\n\n• আয়তন ${document.getElementById('total-area').value} sqft এর জন্য M20 কংক্রিট ও Fe500 রড সুপারিশ করা হচ্ছে\n• খরচ কমাতে: বালি ও পাথর স্থানীয় উৎস থেকে সংগ্রহ করুন (১৫-২০% সাশ্রয়)\n• শ্রমিক মজুরিতে ১০-১৫% সঞ্চয় করতে মৌসুমী শ্রমিক ব্যবহার করুন\n• পাইল ফাউন্ডেশন ব্যবহার করলে দীর্ঘমেয়াদে নিরাপদ ও সাশ্রয়ী`, 'bot');
  }
}
function addAIMsg(text, type) {
  const msgs = document.getElementById('ai-messages');
  if(!msgs) return;
  const div = document.createElement('div');
  div.className = 'ai-msg '+type;
  div.textContent = text;
  msgs.appendChild(div);
  msgs.scrollTop = msgs.scrollHeight;
}
function removeTyping() {
  const msgs = document.getElementById('ai-messages');
  if(!msgs) return;
  const typing = msgs.querySelector('.typing');
  if(typing) typing.remove();
}
function quickAI(msg) {
  document.getElementById('ai-input').value = msg;
  sendAI();
}

// Price trend
function showPriceChart(material, el) {
  document.querySelectorAll('.inner-tab').forEach(t => t.classList.remove('active'));
  if(el) el.classList.add('active');
  if(priceChartObj) priceChartObj.destroy();
  const pc = document.getElementById('priceChart');
  if(!pc) return;
  const data = priceHistory[material];
  const labels = {rod:'রড (৳/kg)',cement:'সিমেন্ট (৳/বস্তা)',brick:'ইট (৳/হাজার)',sand:'বালি (৳/cft)'};
  priceChartObj = new Chart(pc, {type:'line', data:{labels:months, datasets:[{label:labels[material],data,borderColor:'#1a6b3a',backgroundColor:'rgba(26,107,58,0.08)',fill:true,tension:0.4,pointBackgroundColor:'#1a6b3a',pointRadius:4}]}, options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{ticks:{callback:v=>'৳'+v}}}}});
  // Forecast
  const last3 = data.slice(-3);
  const trend = (last3[2]-last3[0])/2;
  const forecast = data[data.length-1] + trend*3;
  const pf = document.getElementById('price-forecast');
  if(pf) pf.innerHTML = `📈 <strong>৩ মাসের পূর্বাভাস:</strong> ${labels[material].split(' ')[0]} মূল্য আনুমানিক ৳ ${Math.round(forecast)} হতে পারে। ${trend>0?'▲ বৃদ্ধির প্রবণতা — এখনই কিনুন বিবেচনা করুন।':'▼ হ্রাসের প্রবণতা — কিছুদিন অপেক্ষা করুন।'}`;
}

// Weather
function calcWeatherDelay() {
  const month = +document.getElementById('start-month').value||1;
  const estMonths = +((document.getElementById('est-months')||{}).textContent||'6').replace(' মাস','');
  let rainyMonths = 0, cycloneRisk = false;
  for(let i=0;i<estMonths;i++) {
    const m = ((month-1+i)%12)+1;
    if(m>=6 && m<=9) rainyMonths++;
    if(m===5||m===10||m===11) cycloneRisk = true;
  }
  const delayDays = rainyMonths * 8;
  const wa = document.getElementById('weather-analysis');
  if(!wa) return;
  wa.innerHTML = `<div class="alert ${rainyMonths>2?'alert-warning':'alert-success'}">
    🌧️ বর্ষা মৌসুম: <strong>${rainyMonths} মাস</strong> পড়বে | আনুমানিক বিলম্ব: <strong>${delayDays} দিন (${Math.round(delayDays/30)} মাস)</strong><br>
    ${cycloneRisk?'⚠️ সাইক্লোন ঝুঁকির সময় নির্মাণ চলবে — বিশেষ সতর্কতা প্রয়োজন।':'✅ সাইক্লোন ঝুঁকির সময় নির্মাণ নেই।'}<br>
    মোট আনুমানিক সময় (বিলম্বসহ): <strong>${estMonths} + ${Math.round(delayDays/30)} = ${estMonths+Math.round(delayDays/30)} মাস</strong>
  </div>`;
}
function renderWorkdayChart() {
  if(workdayChartObj) workdayChartObj.destroy();
  const wc = document.getElementById('workdayChart');
  if(!wc) return;
  workdayChartObj = new Chart(wc, {type:'bar', data:{labels:months, datasets:[{label:'কার্যকর কর্মদিন',data:workdays,backgroundColor:workdays.map(d=>d<22?'#f59e0b':'#1a6b3a'),borderRadius:4}]}, options:{responsive:true,maintainAspectRatio:false,plugins:{legend:{display:false}},scales:{y:{min:15,max:27,ticks:{callback:v=>v+' দিন'}}}}});
}

// Checklist
let checkDone = 0, checkTotal = 0;
function renderChecklist() {
  const phases = Object.keys(checklist);
  const tabs = document.getElementById('checklist-phase-tabs');
  const cont = document.getElementById('checklist-container');
  if(!tabs||!cont) return;
  tabs.innerHTML = phases.map((p,i) => `<button class="inner-tab ${i===0?'active':''}" onclick="showCheckPhase('${p}', this)">${p}</button>`).join('');
  checkTotal = phases.reduce((s,p)=>s+checklist[p].length,0);
  if(document.getElementById('checklist-total')) document.getElementById('checklist-total').textContent = checkTotal;
  showCheckPhase(phases[0], tabs.querySelector('.inner-tab'));
}
function showCheckPhase(phase, el) {
  document.querySelectorAll('#checklist-phase-tabs .inner-tab').forEach(t => t.classList.remove('active'));
  if(el) el.classList.add('active');
  const cont = document.getElementById('checklist-container');
  if(!cont) return;
  cont.innerHTML = checklist[phase].map((item,i) => {
    const key = phase+'-'+i;
    const done = !!checklistState[key];
    return `<div class="checklist-item ${done?'done':''}" id="cl-${key}">
      <input type="checkbox" ${done?'checked':''} onchange="toggleCheck('${key}', this.checked)">
      <div>
        <div class="checklist-label ${done?'done-text':''}">${item.t}</div>
        <div class="checklist-phase">${phase} পর্যায়</div>
      </div>
    </div>`;
  }).join('');
  updateCheckProgress();
}
function toggleCheck(key, done) {
  checklistState[key] = done;
  const item = document.getElementById('cl-'+key);
  if(item) { item.classList.toggle('done', done); item.querySelector('.checklist-label').classList.toggle('done-text', done); }
  updateCheckProgress();
}
function updateCheckProgress() {
  checkDone = Object.values(checklistState).filter(Boolean).length;
  if(document.getElementById('checklist-done')) document.getElementById('checklist-done').textContent = checkDone;
  const bar = document.getElementById('checklist-bar');
  if(bar) bar.style.width = (checkTotal>0?Math.round(checkDone/checkTotal*100):0)+'%';
}

// Compare
function saveToCompare() {
  if(compareProjects.length>=10) { alert('সর্বোচ্চ ১০টি প্রজেক্ট তুলনা করা যাবে।'); return; }
  const p = {
    name: '# ' + (compareProjects.length+1) + ' — ' + (document.getElementById('district').value||'অজ্ঞাত'),
    area: document.getElementById('total-area').value,
    floors: document.getElementById('floors').value,
    type: document.getElementById('bldg-type').options[document.getElementById('bldg-type').selectedIndex].text,
    quality: document.getElementById('quality').options[document.getElementById('quality').selectedIndex].text,
    total: lastTotal,
    perSqft: lastTotal / (+document.getElementById('total-area').value||1),
    time: (document.getElementById('est-months')||{}).textContent||'?',
  };
  compareProjects.push(p);
  renderCompare();
  savedCount++;
}
function clearCompare() { compareProjects = []; renderCompare(); }
function renderCompare() {
  const cont = document.getElementById('compare-container');
  if(!cont) return;
  if(!compareProjects.length) { cont.innerHTML = '<div class="alert alert-info" style="margin:0;">প্রজেক্ট হিসাব করুন, তারপর যোগ করুন।</div>'; return; }
  const minTotal = Math.min(...compareProjects.map(p=>p.total));
  const maxTotal = Math.max(...compareProjects.map(p=>p.total));
  let html = `<div style="overflow-x:auto;"><table class="compare-table"><thead><tr>
    <th>প্রজেক্ট</th><th>ধরণ</th><th>আয়তন</th><th>তলা</th><th>মান</th><th>মোট খরচ</th><th>প্রতি sqft</th><th>সময়</th>
  </tr></thead><tbody>`;
  compareProjects.forEach(p => {
    const isBest = p.total===minTotal;
    const isWorst = p.total===maxTotal && compareProjects.length>1;
    html += `<tr>
      <td style="font-weight:600;">${p.name}</td>
      <td>${p.type.substring(0,10)}</td>
      <td>${p.area} sqft</td>
      <td>${p.floors}</td>
      <td>${p.quality.split(' ')[0]}</td>
      <td class="${isBest?'best':isWorst?'worst':''}">৳ ${Math.round(p.total).toLocaleString()} ${isBest?'✅':isWorst?'❌':''}</td>
      <td>৳ ${Math.round(p.perSqft).toLocaleString()}</td>
      <td>${p.time}</td>
    </tr>`;
  });
  html += '</tbody></table></div>';
  cont.innerHTML = html;
}

// Badges
const badgeDefs = [
  {id:'first',icon:'🏗️',name:'প্রথম হিসাব',desc:'প্রথম হিসাব সম্পন্ন',check:()=>calcCount>=1},
  {id:'economy',icon:'💰',name:'সাশ্রয়ী নির্মাতা',desc:'১০ লাখের নিচে',check:()=>lastTotal>0&&lastTotal<1000000},
  {id:'bigproject',icon:'🏙️',name:'বড় প্রজেক্ট',desc:'১ কোটির উপরে',check:()=>lastTotal>=10000000},
  {id:'solar',icon:'☀️',name:'সবুজ নির্মাতা',desc:'সোলার যোগ করেছেন',check:()=>(+document.getElementById('solar-kw').value||0)>0},
  {id:'multi',icon:'📊',name:'তুলনাবিদ',desc:'৩টি প্রজেক্ট তুলনা',check:()=>compareProjects.length>=3},
  {id:'location',icon:'📍',name:'লোকেশন মাস্টার',desc:'জেলা নির্বাচন করেছেন',check:()=>!!document.getElementById('district').value},
  {id:'checklist',icon:'✅',name:'মান নিশ্চয়তা',desc:'৫০% চেকলিস্ট সম্পন্ন',check:()=>checkTotal>0&&checkDone/checkTotal>=0.5},
  {id:'hospital',icon:'🏥',name:'হেলথকেয়ার বিশেষজ্ঞ',desc:'হাসপাতাল হিসাব করেছেন',check:()=>document.getElementById('bldg-type').value==='1.68'},
];
function checkBadges() {
  badgeDefs.forEach(b => { if(b.check()) badgesEarned.push(b.id); });
  badgesEarned = [...new Set(badgesEarned)];
  if(document.getElementById('stat-calcs')) document.getElementById('stat-calcs').textContent = calcCount;
  if(document.getElementById('stat-projects')) document.getElementById('stat-projects').textContent = savedCount;
  if(document.getElementById('stat-badges')) document.getElementById('stat-badges').textContent = badgesEarned.length;
}
function renderBadges() {
  const cont = document.getElementById('badge-grid');
  if(!cont) return;
  cont.innerHTML = badgeDefs.map(b => {
    const earned = badgesEarned.includes(b.id);
    return `<div class="badge-item ${earned?'earned':'locked'}">
      <div class="badge-icon">${b.icon}</div>
      <div class="badge-name">${b.name}</div>
      <div class="badge-desc">${earned?'✅ অর্জিত':'🔒 '+b.desc}</div>
    </div>`;
  }).join('');
  if(document.getElementById('stat-badges')) document.getElementById('stat-badges').textContent = badgesEarned.length;
}

// Report
function renderReport() {
  const el = document.getElementById('detailed-breakdown');
  const rd = document.getElementById('report-date');
  if(rd) rd.textContent = 'তারিখ: '+new Date().toLocaleDateString('bn-BD')+' | এলাকা: '+(document.getElementById('district').value||'নির্বাচিত নয়');
  if(!el) return;
  const sqft = +document.getElementById('total-area').value||0;
  const baseRate = +document.getElementById('base-rate').value||2200;
  const cfactor = +document.getElementById('config-factor').value||1;
  const baseCost = sqft*baseRate*cfactor;
  const vat = +document.getElementById('vat').value||15;
  const cont = +document.getElementById('contingency').value||5;
  const mar = +document.getElementById('margin').value||10;
  el.innerHTML = `
    <div class="breakdown-row"><span>মূল নির্মাণ (${sqft.toLocaleString()} sqft × ৳${baseRate} × ${cfactor.toFixed(2)})</span><span>${fmt(baseCost)}</span></div>
    <div class="breakdown-row"><span>ভ্যাট (${vat}%) + কন্টিনজেন্সি (${cont}%) + মার্জিন (${mar}%)</span><span id="report-vat-line">—</span></div>
    <div class="breakdown-row"><span>সরকারি ও আইনি ফি</span><span id="report-govt-line">—</span></div>
    <div class="breakdown-row total"><span>সর্বমোট</span><span>${fmt(lastTotal)}</span></div>
    <div style="margin-top:8px; font-size:12px; color:var(--text-muted);">প্রতি sqft গড়: <strong>${fmt(sqft>0?lastTotal/sqft:0)}</strong></div>
  `;
  const rvl = document.getElementById('report-vat-line');
  const rgl = document.getElementById('report-govt-line');
  const g = id => document.getElementById(id)?.textContent?.replace('৳ ','').replace(/,/g,'')||'0';
  if(rvl) rvl.textContent = document.getElementById('br-vat').textContent||'—';
  if(rgl) rgl.textContent = document.getElementById('br-govt').textContent||'—';
}

// QR Code
function generateQR() {
  const cont = document.getElementById('qr-code');
  if(!cont) return;
  cont.innerHTML = '';
  try {
    const data = `নির্মাণ হিসাব | খরচ: ৳${Math.round(lastTotal).toLocaleString()} | sqft: ${document.getElementById('total-area').value} | ${new Date().toLocaleDateString('bn-BD')}`;
    if(typeof QRCode !== 'undefined') {
      new QRCode(cont, {text:data, width:120, height:120});
    } else {
      cont.innerHTML = '<div style="width:120px;height:120px;border:2px dashed var(--border);display:flex;align-items:center;justify-content:center;font-size:11px;color:var(--text-muted);text-align:center;">QR লোডিং...</div>';
    }
  } catch(e) { cont.innerHTML = '<div style="padding:20px; font-size:11px; color:var(--text-muted);">QR উপলব্ধ নয়</div>'; }
}

// Loan & Solar
function calcLoan() {
  const P = +document.getElementById('loan-amt').value||0;
  const r = (+document.getElementById('loan-rate').value||9)/100/12;
  const n = (+document.getElementById('loan-years').value||15)*12;
  if(!P||!r) return;
  const emi = P*r*Math.pow(1+r,n)/(Math.pow(1+r,n)-1);
  const total = emi*n;
  if(document.getElementById('emi-val')) document.getElementById('emi-val').textContent = '৳ '+Math.round(emi).toLocaleString();
  if(document.getElementById('loan-details')) document.getElementById('loan-details').textContent = `মোট পরিশোধ: ৳ ${Math.round(total).toLocaleString()} | সুদ: ৳ ${Math.round(total-P).toLocaleString()}`;
}
function calcSolarROI() {
  const kw = +document.getElementById('solar-kw').value||0;
  if(!kw) { const r = document.getElementById('solar-roi-result'); if(r) r.innerHTML = 'সোলার kW দিন →'; return; }
  const cost = kw*80000;
  const monthly = (+document.getElementById('monthly-bill').value||5000)*(+document.getElementById('solar-pct').value||70)/100;
  const years = cost/(monthly*12);
  const r = document.getElementById('solar-roi-result');
  if(r) r.innerHTML = `<div style="font-weight:700; font-size:15px; color:var(--primary);">ROI: ${years.toFixed(1)} বছর</div><div style="font-size:11px; color:var(--text-muted);">ইনস্টল: ৳ ${cost.toLocaleString()}<br>মাসিক সঞ্চয়: ৳ ${Math.round(monthly).toLocaleString()}</div>`;
}

// Save/Load
function saveProject() {
  const data = {
    area: document.getElementById('total-area').value,
    floors: document.getElementById('floors').value,
    district: document.getElementById('district').value,
    btype: document.getElementById('bldg-type').value,
    quality: document.getElementById('quality').value,
    baseRate: document.getElementById('base-rate').value,
    total: lastTotal,
    labor: laborData,
    savedAt: new Date().toISOString()
  };
  try {
    const projects = JSON.parse(localStorage.getItem('nirman-v4-projects')||'[]');
    projects.push(data); savedCount++;
    localStorage.setItem('nirman-v4-projects', JSON.stringify(projects.slice(-10)));
    const ind = document.getElementById('save-indicator');
    if(ind) { ind.textContent = '✅ সেভ হয়েছে'; setTimeout(()=>{ind.textContent='● অটো-সেভ চালু';},2000); }
    checkBadges();
  } catch(e) { alert('সেভ করতে সমস্যা হয়েছে।'); }
}
function loadProject() {
  try {
    const projects = JSON.parse(localStorage.getItem('nirman-v4-projects')||'[]');
    if(!projects.length) { alert('কোনো সেভ করা প্রজেক্ট নেই।'); return; }
    const last = projects[projects.length-1];
    document.getElementById('total-area').value = last.area||2000;
    document.getElementById('floors').value = last.floors||3;
    document.getElementById('bldg-type').value = last.btype||'1.0';
    document.getElementById('quality').value = last.quality||'1.0';
    document.getElementById('base-rate').value = last.baseRate||2200;
    if(last.labor) laborData = last.labor;
    renderLaborList(); renderSpecialFeatures(); renderFloorFinish(); recalculate();
    alert('প্রজেক্ট লোড হয়েছে! (' + new Date(last.savedAt).toLocaleDateString('bn-BD') + ')');
  } catch(e) { alert('লোড করতে সমস্যা হয়েছে।'); }
}
function exportCSV() {
  const mats = calcMaterials(+document.getElementById('total-area').value||0);
  const rows = [['উপকরণ','পরিমাণ','একক','দর','মোট']];
  mats.forEach(m => rows.push([m.n,m.qty,m.u,m.r,m.total]));
  const csv = rows.map(r => r.join(',')).join('\n');
  const blob = new Blob(['\ufeff'+csv], {type:'text/csv;charset=utf-8'});
  const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = 'nirman_material.csv'; a.click();
}
function exportPDF() { alert('প্রিন্ট ডায়ালগ থেকে "Save as PDF" সিলেক্ট করুন।'); window.print(); }
function printReport() { window.print(); }
function shareReport() {
  const txt = `নির্মাণ হিসাব রিপোর্ট\nমোট খরচ: ৳${Math.round(lastTotal).toLocaleString()}\nআয়তন: ${document.getElementById('total-area').value} sqft\nতারিখ: ${new Date().toLocaleDateString('bn-BD')}`;
  if(navigator.clipboard) { navigator.clipboard.writeText(txt).then(()=>alert('কপি হয়েছে!')); }
  else alert(txt);
}

// Init
document.addEventListener('DOMContentLoaded', () => {
  try {
    const theme = localStorage.getItem('nirman-theme')||'light';
    document.documentElement.setAttribute('data-theme', theme);
    if(theme==='dark') document.getElementById('themeBtn').classList.add('dark');
  } catch(e){}
  renderLaborList();
  renderSpecialFeatures();
  renderFloorFinish();
  calcLoan();
  recalculate();
  document.getElementById('report-date') && (document.getElementById('report-date').textContent = 'তারিখ: '+new Date().toLocaleDateString('bn-BD'));
  // Auto-save every 2 min
  setInterval(() => { try { localStorage.setItem('nirman-v4-auto', JSON.stringify({total:lastTotal,ts:Date.now()})); } catch(e){} }, 120000);
});
</script>
</body>
</html>
