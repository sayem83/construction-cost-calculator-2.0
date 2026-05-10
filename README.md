<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>নির্মাণ হিসাব - Bangladesh Construction Estimator</title>
<link href="https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@300;400;500;600;700&family=Noto+Sans+Bengali:wght@400;500;600;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<style>
:root {
  --primary: #1a6b3a;
  --primary-light: #2d9653;
  --primary-dark: #0f4526;
  --accent: #e8a020;
  --accent-dark: #c47d0a;
  --bg: #f0f4f1;
  --bg-card: #ffffff;
  --bg-sidebar: #0f3d22;
  --text: #1a2e20;
  --text-muted: #5a7060;
  --border: #d0dcd4;
  --success: #22c55e;
  --warning: #f59e0b;
  --danger: #ef4444;
  --info: #3b82f6;
  --shadow: 0 2px 12px rgba(0,0,0,0.08);
  --shadow-lg: 0 8px 32px rgba(0,0,0,0.14);
  --radius: 12px;
  --radius-sm: 8px;
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: 'Hind Siliguri', 'Noto Sans Bengali', sans-serif; background: var(--bg); color: var(--text); min-height: 100vh; }

/* Layout */
.app { display: flex; min-height: 100vh; }
.sidebar { width: 260px; background: var(--bg-sidebar); color: #e8f5eb; flex-shrink: 0; display: flex; flex-direction: column; position: sticky; top: 0; height: 100vh; overflow-y: auto; }
.main { flex: 1; overflow-x: hidden; }

/* Sidebar */
.logo { padding: 24px 20px 16px; border-bottom: 1px solid rgba(255,255,255,0.1); }
.logo-icon { font-size: 28px; margin-bottom: 4px; }
.logo-title { font-size: 18px; font-weight: 700; color: #fff; line-height: 1.2; }
.logo-sub { font-size: 11px; color: #8fbf9a; margin-top: 2px; }
.nav { padding: 12px 0; flex: 1; }
.nav-item { display: flex; align-items: center; gap: 10px; padding: 11px 20px; cursor: pointer; border-left: 3px solid transparent; transition: all 0.2s; font-size: 14px; color: #b8d4be; }
.nav-item:hover { background: rgba(255,255,255,0.07); color: #fff; }
.nav-item.active { background: rgba(255,255,255,0.12); border-left-color: var(--accent); color: #fff; font-weight: 600; }
.nav-icon { font-size: 18px; width: 22px; text-align: center; }
.sidebar-footer { padding: 16px 20px; border-top: 1px solid rgba(255,255,255,0.1); font-size: 12px; color: #6b9e77; }

/* Header */
.header { background: var(--bg-card); border-bottom: 1px solid var(--border); padding: 16px 28px; display: flex; align-items: center; justify-content: space-between; position: sticky; top: 0; z-index: 100; box-shadow: 0 1px 4px rgba(0,0,0,0.06); }
.header-left h1 { font-size: 20px; font-weight: 700; color: var(--primary-dark); }
.header-left p { font-size: 13px; color: var(--text-muted); margin-top: 1px; }
.header-right { display: flex; gap: 10px; align-items: center; }
.btn { padding: 8px 16px; border-radius: var(--radius-sm); border: none; cursor: pointer; font-family: inherit; font-size: 13px; font-weight: 600; transition: all 0.2s; display: inline-flex; align-items: center; gap: 6px; }
.btn-primary { background: var(--primary); color: #fff; }
.btn-primary:hover { background: var(--primary-light); }
.btn-accent { background: var(--accent); color: #fff; }
.btn-accent:hover { background: var(--accent-dark); }
.btn-outline { background: transparent; color: var(--primary); border: 1.5px solid var(--primary); }
.btn-outline:hover { background: var(--primary); color: #fff; }
.btn-sm { padding: 6px 12px; font-size: 12px; }
.btn-danger { background: var(--danger); color: #fff; }

/* Content */
.content { padding: 24px 28px; }
.section { display: none; }
.section.active { display: block; }

/* Cards */
.card { background: var(--bg-card); border: 1px solid var(--border); border-radius: var(--radius); padding: 20px 24px; margin-bottom: 20px; box-shadow: var(--shadow); }
.card-title { font-size: 16px; font-weight: 700; color: var(--primary-dark); margin-bottom: 16px; display: flex; align-items: center; gap: 8px; padding-bottom: 12px; border-bottom: 1px solid var(--border); }
.card-title .badge { font-size: 11px; background: var(--primary); color: #fff; padding: 2px 8px; border-radius: 20px; font-weight: 500; }

/* Form Grid */
.grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; }
.grid-4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; }
.form-group { display: flex; flex-direction: column; gap: 6px; }
.form-group label { font-size: 13px; font-weight: 600; color: var(--text-muted); }
.form-group select, .form-group input { padding: 9px 12px; border: 1.5px solid var(--border); border-radius: var(--radius-sm); font-family: inherit; font-size: 14px; color: var(--text); background: var(--bg); outline: none; transition: border-color 0.2s; }
.form-group select:focus, .form-group input:focus { border-color: var(--primary); background: #fff; }
.form-group .hint { font-size: 11px; color: var(--text-muted); }

/* Summary bar */
.summary-bar { display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px; margin-bottom: 24px; }
.stat-card { background: var(--bg-card); border: 1px solid var(--border); border-radius: var(--radius); padding: 16px 20px; text-align: center; box-shadow: var(--shadow); position: relative; overflow: hidden; }
.stat-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px; }
.stat-card.green::before { background: var(--primary); }
.stat-card.amber::before { background: var(--accent); }
.stat-card.blue::before { background: var(--info); }
.stat-card.red::before { background: var(--danger); }
.stat-label { font-size: 12px; color: var(--text-muted); font-weight: 500; margin-bottom: 6px; }
.stat-value { font-size: 22px; font-weight: 700; color: var(--primary-dark); line-height: 1; }
.stat-sub { font-size: 11px; color: var(--text-muted); margin-top: 4px; }

/* Special features */
.feature-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; }
.feature-item { display: flex; align-items: center; gap: 8px; padding: 10px 12px; border: 1.5px solid var(--border); border-radius: var(--radius-sm); cursor: pointer; transition: all 0.2s; font-size: 13px; }
.feature-item:hover { border-color: var(--primary); background: #f0f9f3; }
.feature-item.selected { border-color: var(--primary); background: #e8f5eb; color: var(--primary-dark); font-weight: 600; }
.feature-item input[type=checkbox] { accent-color: var(--primary); }
.feature-qty { width: 60px; padding: 4px 8px; border: 1px solid var(--border); border-radius: 4px; font-family: inherit; font-size: 12px; margin-left: auto; }

/* Material table */
.mat-table { width: 100%; border-collapse: collapse; font-size: 13px; }
.mat-table th { background: #f0f4f1; padding: 10px 14px; text-align: left; font-weight: 700; color: var(--text-muted); font-size: 12px; border-bottom: 1px solid var(--border); }
.mat-table td { padding: 10px 14px; border-bottom: 1px solid #f0f0f0; }
.mat-table tr:last-child td { border-bottom: none; }
.mat-table tr:hover td { background: #f9fafb; }
.mat-table .amount { font-weight: 700; color: var(--primary-dark); text-align: right; }
.mat-table .qty { color: var(--text-muted); }

/* Chart area */
.chart-wrap { position: relative; width: 100%; height: 300px; }

/* Labor rows */
.labor-row { display: grid; grid-template-columns: 2fr 1fr 1fr 1fr 120px; gap: 8px; align-items: center; padding: 8px 0; border-bottom: 1px solid #f0f0f0; font-size: 13px; }
.labor-row.header { font-weight: 700; font-size: 12px; color: var(--text-muted); padding-bottom: 6px; }
.labor-row input { padding: 6px 8px; border: 1px solid var(--border); border-radius: 6px; font-family: inherit; font-size: 13px; width: 100%; }
.labor-total { font-weight: 700; color: var(--primary-dark); text-align: right; }

/* Financial */
.fin-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
.fee-row { display: flex; justify-content: space-between; align-items: center; padding: 8px 0; border-bottom: 1px solid #f5f5f5; font-size: 14px; }
.fee-row:last-child { border-bottom: none; font-weight: 700; color: var(--primary-dark); }
.fee-val { font-weight: 600; }

/* Report */
.report-header { text-align: center; padding: 24px; background: linear-gradient(135deg, var(--primary-dark), var(--primary)); color: #fff; border-radius: var(--radius); margin-bottom: 20px; }
.report-title { font-size: 24px; font-weight: 700; }
.report-sub { font-size: 13px; opacity: 0.8; margin-top: 4px; }
.breakdown-row { display: flex; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid var(--border); font-size: 14px; }
.breakdown-row.total { font-weight: 700; font-size: 16px; color: var(--primary-dark); padding-top: 14px; border-top: 2px solid var(--primary); border-bottom: none; }

/* Tabs */
.tab-bar { display: flex; gap: 4px; padding: 6px; background: var(--bg); border-radius: var(--radius); margin-bottom: 20px; border: 1px solid var(--border); flex-wrap: wrap; }
.tab { padding: 8px 16px; border-radius: var(--radius-sm); border: none; background: transparent; cursor: pointer; font-family: inherit; font-size: 13px; font-weight: 500; color: var(--text-muted); transition: all 0.2s; }
.tab.active { background: var(--bg-card); color: var(--primary); font-weight: 700; box-shadow: var(--shadow); }
.tab-content { display: none; }
.tab-content.active { display: block; }

/* Currency toggle */
.currency-toggle { display: flex; gap: 6px; }
.cur-btn { padding: 6px 12px; border-radius: 20px; border: 1.5px solid var(--border); background: transparent; cursor: pointer; font-family: inherit; font-size: 12px; font-weight: 600; color: var(--text-muted); transition: all 0.2s; }
.cur-btn.active { background: var(--primary); color: #fff; border-color: var(--primary); }

/* Alert */
.alert { padding: 12px 16px; border-radius: var(--radius-sm); font-size: 13px; margin-bottom: 16px; display: flex; align-items: flex-start; gap: 10px; }
.alert-info { background: #eff6ff; border: 1px solid #bfdbfe; color: #1e40af; }
.alert-warning { background: #fffbeb; border: 1px solid #fde68a; color: #92400e; }
.alert-success { background: #f0fdf4; border: 1px solid #bbf7d0; color: #14532d; }

/* Range input */
input[type=range] { -webkit-appearance: none; width: 100%; height: 4px; border-radius: 2px; background: var(--border); outline: none; }
input[type=range]::-webkit-slider-thumb { -webkit-appearance: none; width: 18px; height: 18px; border-radius: 50%; background: var(--primary); cursor: pointer; border: 2px solid #fff; box-shadow: 0 0 0 2px var(--primary); }

/* Print */
@media print {
  .sidebar, .header-right, .btn, .nav-item { display: none; }
  .main { margin: 0; }
}

/* Scrollbar */
::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-track { background: #f0f4f1; }
::-webkit-scrollbar-thumb { background: #b0cbb8; border-radius: 3px; }

/* Loan calculator */
.loan-result { background: #f0fdf4; border: 1px solid #bbf7d0; border-radius: var(--radius-sm); padding: 16px; margin-top: 12px; }
.loan-result h3 { font-size: 14px; color: var(--primary-dark); margin-bottom: 8px; }
.loan-result .monthly { font-size: 28px; font-weight: 700; color: var(--primary); }
.loan-result .details { font-size: 12px; color: var(--text-muted); margin-top: 6px; }

/* Zone badge */
.zone-badge { display: inline-flex; align-items: center; gap: 4px; padding: 3px 10px; border-radius: 20px; font-size: 12px; font-weight: 600; }
.zone-1 { background: #fef2f2; color: #991b1b; }
.zone-2 { background: #fff7ed; color: #92400e; }
.zone-3 { background: #fefce8; color: #713f12; }
.zone-4 { background: #f0fdf4; color: #14532d; }

/* Construction time bar */
.time-bar { height: 20px; border-radius: 10px; background: linear-gradient(90deg, var(--primary), var(--accent)); transition: width 0.5s; }

.section-divider { font-size: 12px; font-weight: 700; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.05em; padding: 0 0 8px; margin: 16px 0 12px; border-bottom: 1px solid var(--border); }

input[type=number]::-webkit-inner-spin-button { opacity: 1; }

.dark-toggle { display: flex; align-items: center; gap: 6px; font-size: 13px; cursor: pointer; }
</style>
</head>
<body>
<div class="app">

<!-- Sidebar -->
<div class="sidebar">
  <div class="logo">
    <div class="logo-icon">🏗️</div>
    <div class="logo-title">নির্মাণ হিসাব</div>
    <div class="logo-sub">Bangladesh Construction Estimator v3.0</div>
  </div>
  <div class="nav">
    <div class="nav-item active" onclick="showSection('location')"><span class="nav-icon">📍</span> লোকেশন ও পরিবেশ</div>
    <div class="nav-item" onclick="showSection('building')"><span class="nav-icon">🏢</span> বিল্ডিং কনফিগারেশন</div>
    <div class="nav-item" onclick="showSection('materials')"><span class="nav-icon">🧱</span> ম্যাটেরিয়াল টেকঅফ</div>
    <div class="nav-item" onclick="showSection('labor')"><span class="nav-icon">👷</span> শ্রমিক ও যন্ত্রপাতি</div>
    <div class="nav-item" onclick="showSection('extras')"><span class="nav-icon">⚡</span> অতিরিক্ত সুবিধা</div>
    <div class="nav-item" onclick="showSection('financial')"><span class="nav-icon">💰</span> আর্থিক ও সরকারি ফি</div>
    <div class="nav-item" onclick="showSection('special')"><span class="nav-icon">⭐</span> স্পেশাল ফিচারস</div>
    <div class="nav-item" onclick="showSection('report')"><span class="nav-icon">📊</span> রিপোর্ট ও বিশ্লেষণ</div>
  </div>
  <div class="sidebar-footer">
    BNBC ২০২০ অনুসরণ করে<br>
    রাজউক অনুমোদিত হিসাব পদ্ধতি
  </div>
</div>

<!-- Main -->
<div class="main">
  <!-- Header -->
  <div class="header">
    <div class="header-left">
      <h1 id="page-title">লোকেশন ও পরিবেশ</h1>
      <p id="page-sub">এলাকা নির্বাচন করুন এবং পরিবেশ ফ্যাক্টর নির্ধারণ করুন</p>
    </div>
    <div class="header-right">
      <div class="currency-toggle">
        <button class="cur-btn active" onclick="setCurrency('BDT')">৳ BDT</button>
        <button class="cur-btn" onclick="setCurrency('USD')">$ USD</button>
        <button class="cur-btn" onclick="setCurrency('INR')">₹ INR</button>
      </div>
      <button class="btn btn-primary" onclick="saveProject()">💾 সেভ</button>
      <button class="btn btn-accent" onclick="showSection('report')">📊 রিপোর্ট দেখুন</button>
    </div>
  </div>

  <!-- Summary Bar -->
  <div style="padding: 16px 28px 0;">
    <div class="summary-bar">
      <div class="stat-card green">
        <div class="stat-label">মোট নির্মাণ খরচ</div>
        <div class="stat-value" id="total-cost">৳ ০</div>
        <div class="stat-sub" id="cost-per-sqft">প্রতি বর্গফুট: ৳ ০</div>
      </div>
      <div class="stat-card amber">
        <div class="stat-label">নির্মাণ সময়কাল</div>
        <div class="stat-value" id="construction-time">০ মাস</div>
        <div class="stat-sub" id="manday-info">মোট ম্যান-ডে: ০</div>
      </div>
      <div class="stat-card blue">
        <div class="stat-label">এলাকা ফ্যাক্টর</div>
        <div class="stat-value" id="area-factor">১.০০</div>
        <div class="stat-sub" id="zone-info">ভূমিকম্প জোন: —</div>
      </div>
      <div class="stat-card red">
        <div class="stat-label">সরকারি ফি + ভ্যাট</div>
        <div class="stat-value" id="govt-cost">৳ ০</div>
        <div class="stat-sub">রাজউক + ওয়াসা + বিদ্যুৎ</div>
      </div>
    </div>
  </div>

  <div class="content">

    <!-- LOCATION SECTION -->
    <div class="section active" id="section-location">
      <div class="alert alert-info">
        ℹ️ বিভাগ → জেলা → উপজেলা নির্বাচন করুন। প্রতিটি এলাকার জন্য আলাদা কস্ট ফ্যাক্টর স্বয়ংক্রিয়ভাবে প্রযোজ্য হবে।
      </div>
      <div class="card">
        <div class="card-title">🗺️ লোকেশন নির্বাচন <span class="badge">৬৪ জেলা | ৪৯৫+ উপজেলা</span></div>
        <div class="grid-3">
          <div class="form-group">
            <label>বিভাগ</label>
            <select id="division" onchange="updateDistricts()">
              <option value="">-- বিভাগ নির্বাচন --</option>
              <option value="dhaka">ঢাকা</option>
              <option value="chittagong">চট্টগ্রাম</option>
              <option value="rajshahi">রাজশাহী</option>
              <option value="khulna">খুলনা</option>
              <option value="barisal">বরিশাল</option>
              <option value="sylhet">সিলেট</option>
              <option value="rangpur">রংপুর</option>
              <option value="mymensingh">ময়মনসিংহ</option>
            </select>
          </div>
          <div class="form-group">
            <label>জেলা</label>
            <select id="district" onchange="updateUpazilas()">
              <option value="">-- জেলা নির্বাচন --</option>
            </select>
          </div>
          <div class="form-group">
            <label>উপজেলা / থানা</label>
            <select id="upazila" onchange="updateLocationFactor()">
              <option value="">-- উপজেলা নির্বাচন --</option>
            </select>
          </div>
        </div>
        <div class="grid-3" style="margin-top: 16px;">
          <div class="form-group">
            <label>এলাকার ধরণ</label>
            <select id="area-type" onchange="recalculate()">
              <option value="1.35">মেট্রো কোর (ঢাকা/চট্টগ্রাম)</option>
              <option value="1.15">সাব-আরবান</option>
              <option value="1.0" selected>শহর</option>
              <option value="0.85">উপজেলা সদর</option>
              <option value="0.68">গ্রামীণ</option>
            </select>
          </div>
          <div class="form-group">
            <label>সিটি কর্পোরেশন / পৌরসভা</label>
            <select id="city-corp" onchange="recalculate()">
              <option value="0">প্রযোজ্য নয়</option>
              <option value="1">ঢাকা উত্তর সিটি কর্পোরেশন</option>
              <option value="1">ঢাকা দক্ষিণ সিটি কর্পোরেশন</option>
              <option value="1">চট্টগ্রাম সিটি কর্পোরেশন</option>
              <option value="1">রাজশাহী সিটি কর্পোরেশন</option>
              <option value="1">খুলনা সিটি কর্পোরেশন</option>
              <option value="1">বরিশাল সিটি কর্পোরেশন</option>
              <option value="1">সিলেট সিটি কর্পোরেশন</option>
              <option value="1">রংপুর সিটি কর্পোরেশন</option>
              <option value="1">ময়মনসিংহ সিটি কর্পোরেশন</option>
              <option value="1">গাজীপুর সিটি কর্পোরেশন</option>
              <option value="1">নারায়ণগঞ্জ সিটি কর্পোরেশন</option>
              <option value="1">কুমিল্লা সিটি কর্পোরেশন</option>
              <option value="0.5">পৌরসভা (১ম শ্রেণী)</option>
              <option value="0.3">পৌরসভা (২য় শ্রেণী)</option>
              <option value="0.1">পৌরসভা (৩য় শ্রেণী)</option>
            </select>
          </div>
          <div class="form-group">
            <label>ভূমিকম্প ঝুঁকি জোন (BNBC)</label>
            <select id="seismic-zone" onchange="recalculate()">
              <option value="1.0">জোন-১ (কম ঝুঁকি) - খুলনা, বরিশাল</option>
              <option value="1.05" selected>জোন-২ (মাঝারি) - ঢাকা, চট্টগ্রাম</option>
              <option value="1.10">জোন-৩ (বেশি) - রাজশাহী, রংপুর</option>
              <option value="1.15">জোন-৪ (অতি বেশি) - সিলেট</option>
            </select>
          </div>
        </div>
        <div class="grid-3" style="margin-top: 16px;">
          <div class="form-group">
            <label>বন্যা ঝুঁকি</label>
            <select id="flood-risk" onchange="recalculate()">
              <option value="1.0">নেই</option>
              <option value="1.05">কম</option>
              <option value="1.10" selected>মাঝারি</option>
              <option value="1.15">বেশি</option>
              <option value="1.20">অতি বেশি (হাওর/বিল এলাকা)</option>
            </select>
          </div>
          <div class="form-group">
            <label>বিশেষ পরিবেশ</label>
            <select id="special-env" onchange="recalculate()">
              <option value="1.0">সাধারণ</option>
              <option value="1.07">সমুদ্র উপকূল (কক্সবাজার/চট্টগ্রাম)</option>
              <option value="1.20">পার্বত্য এলাকা (রাঙ্গামাটি/বান্দরবান/খাগড়াছড়ি)</option>
              <option value="1.12">হাওর এলাকা (সুনামগঞ্জ/কিশোরগঞ্জ)</option>
              <option value="1.08">মৌসুমী বন্যা প্রবণ</option>
            </select>
          </div>
          <div class="form-group">
            <label>গ্যাস সংযোগের দূরত্ব (মিটার)</label>
            <input type="number" id="gas-dist" value="50" min="0" onchange="recalculate()">
            <span class="hint">প্রতি মিটার ৳ ৮০০ অতিরিক্ত</span>
          </div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">🌡️ পরিবেশ ও জলবায়ু ফ্যাক্টর</div>
        <div id="env-summary" style="font-size: 14px; line-height: 2;">
          <table style="width: 100%; font-size: 14px;">
            <tr><td style="color: var(--text-muted); width: 200px;">এলাকা ধরণ ফ্যাক্টর</td><td id="ef1" style="font-weight: 700;">১.০০</td></tr>
            <tr><td style="color: var(--text-muted);">ভূমিকম্প ফ্যাক্টর</td><td id="ef2" style="font-weight: 700;">১.০৫</td></tr>
            <tr><td style="color: var(--text-muted);">বন্যা ফ্যাক্টর</td><td id="ef3" style="font-weight: 700;">১.১০</td></tr>
            <tr><td style="color: var(--text-muted);">বিশেষ পরিবেশ ফ্যাক্টর</td><td id="ef4" style="font-weight: 700;">১.০০</td></tr>
            <tr style="border-top: 2px solid var(--primary);"><td style="color: var(--primary-dark); font-weight: 700; padding-top: 8px;">সম্মিলিত ফ্যাক্টর</td><td id="ef-total" style="font-weight: 700; font-size: 18px; color: var(--primary);">১.১৬</td></tr>
          </table>
        </div>
      </div>
    </div>

    <!-- BUILDING SECTION -->
    <div class="section" id="section-building">
      <div class="card">
        <div class="card-title">🏢 বিল্ডিং টাইপ <span class="badge">৩০+ ধরণ</span></div>
        <div class="grid-3">
          <div class="form-group">
            <label>বিল্ডিং টাইপ</label>
            <select id="bldg-type" onchange="onBuildingTypeChange()">
              <option value="1.0">আবাসিক (বাড়ি/ফ্ল্যাট)</option>
              <option value="1.15">অ্যাপার্টমেন্ট বহুতল</option>
              <option value="1.25">বাণিজ্যিক অফিস</option>
              <option value="1.30">শোরুম</option>
              <option value="1.35">ব্যাংক</option>
              <option value="1.68">হাসপাতাল</option>
              <option value="1.45">ক্লিনিক</option>
              <option value="1.20">স্কুল</option>
              <option value="1.30">কলেজ/বিশ্ববিদ্যালয়</option>
              <option value="1.40">হোটেল ★★★</option>
              <option value="1.60">হোটেল ★★★★★</option>
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
          <div class="form-group">
            <label>নির্মাণ মান</label>
            <select id="quality" onchange="recalculate()">
              <option value="0.70">ইকোনমি (সাধারণ)</option>
              <option value="1.00" selected>স্ট্যান্ডার্ড</option>
              <option value="1.35">প্রিমিয়াম</option>
              <option value="1.85">লাক্সারি</option>
            </select>
          </div>
          <div class="form-group">
            <label>স্ট্রাকচার</label>
            <select id="structure" onchange="recalculate()">
              <option value="1.0" selected>RCC ফ্রেম</option>
              <option value="0.85">লোড বেয়ারিং</option>
              <option value="1.20">স্টিল ফ্রেম</option>
            </select>
          </div>
        </div>
        <div class="grid-4" style="margin-top: 16px;">
          <div class="form-group">
            <label>মোট আয়তন (বর্গফুট)</label>
            <input type="number" id="total-area" value="2000" min="100" onchange="recalculate()">
          </div>
          <div class="form-group">
            <label>তলা সংখ্যা</label>
            <input type="number" id="floors" value="3" min="1" max="50" onchange="recalculate()">
          </div>
          <div class="form-group">
            <label>ফাউন্ডেশন টাইপ</label>
            <select id="foundation" onchange="recalculate()">
              <option value="0.08">শ্যালো ফাউন্ডেশন</option>
              <option value="0.12" selected>পাইল ফাউন্ডেশন</option>
              <option value="0.10">র্যাফট ফাউন্ডেশন</option>
            </select>
          </div>
          <div class="form-group">
            <label>লিফট সংখ্যা</label>
            <input type="number" id="lifts" value="0" min="0" onchange="recalculate()">
            <span class="hint">প্রতি লিফট ৳ ২৫,০০,০০০</span>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="card-title">📐 বেস রেট তথ্য</div>
        <div class="grid-3">
          <div class="form-group">
            <label>কংক্রিট গ্রেড</label>
            <select id="concrete-grade" onchange="recalculate()">
              <option value="1.0">M15 (সাধারণ)</option>
              <option value="1.08" selected>M20 (স্ট্যান্ডার্ড)</option>
              <option value="1.15">M25 (প্রিমিয়াম)</option>
              <option value="1.22">M30 (হেভি ডিউটি)</option>
            </select>
          </div>
          <div class="form-group">
            <label>প্রতি বর্গফুট বেস রেট (৳)</label>
            <input type="number" id="base-rate" value="2200" onchange="recalculate()">
            <span class="hint">স্ট্যান্ডার্ড ঢাকা রেট: ৳ ২২০০-২৮০০</span>
          </div>
          <div class="form-group">
            <label>কনফিগ ফ্যাক্টর (গণনা)</label>
            <input type="text" id="config-factor" readonly style="background: #f0f9f3; font-weight: 700; color: var(--primary);">
          </div>
        </div>
      </div>
    </div>

    <!-- MATERIALS SECTION -->
    <div class="section" id="section-materials">
      <div class="alert alert-success">
        ✅ নিচের ম্যাটেরিয়াল পরিমাণ স্বয়ংক্রিয়ভাবে প্রমাণ সূত্র ব্যবহার করে গণনা করা হয়েছে।
      </div>
      <div class="card">
        <div class="card-title">🧱 ম্যাটেরিয়াল টেকঅফ <span class="badge">বিস্তারিত হিসাব</span></div>
        <table class="mat-table" id="materials-table">
          <thead>
            <tr>
              <th>উপকরণ</th>
              <th>পরিমাণ</th>
              <th>একক</th>
              <th>একক মূল্য (৳)</th>
              <th class="amount">মোট খরচ (৳)</th>
            </tr>
          </thead>
          <tbody id="mat-tbody"></tbody>
        </table>
      </div>
      <div class="card">
        <div class="card-title">📊 উপকরণ বন্টন চার্ট</div>
        <div class="chart-wrap">
          <canvas id="matChart" role="img" aria-label="উপকরণ খরচের পাই চার্ট"></canvas>
        </div>
      </div>
    </div>

    <!-- LABOR SECTION -->
    <div class="section" id="section-labor">
      <div class="card">
        <div class="card-title">👷 শ্রমিক তালিকা <span class="badge">সম্পাদনযোগ্য</span></div>
        <div class="labor-row header">
          <span>পদবী</span><span>সংখ্যা</span><span>দৈনিক মজুরি (৳)</span><span>কাজের দিন</span><span>মোট খরচ (৳)</span>
        </div>
        <div id="labor-list"></div>
        <div style="margin-top: 12px; display: flex; gap: 10px; flex-wrap: wrap;">
          <button class="btn btn-outline btn-sm" onclick="addLaborRow()">+ নতুন শ্রমিক যোগ</button>
        </div>
      </div>
      <div class="card">
        <div class="card-title">🔧 যন্ত্রপাতি ভাড়া</div>
        <div class="grid-2">
          <div class="form-group">
            <label>ক্রেন (ঘন্টা)</label>
            <input type="number" id="crane-hrs" value="0" min="0" onchange="recalculate()">
            <span class="hint">প্রতি ঘন্টা ৳ ৩,৫০০</span>
          </div>
          <div class="form-group">
            <label>কংক্রিট মিক্সার (দিন)</label>
            <input type="number" id="mixer-days" value="30" min="0" onchange="recalculate()">
            <span class="hint">প্রতি দিন ৳ ১,৮০০</span>
          </div>
          <div class="form-group">
            <label>কংক্রিট পাম্প (দিন)</label>
            <input type="number" id="pump-days" value="0" min="0" onchange="recalculate()">
            <span class="hint">প্রতি দিন ৳ ৮,০০০</span>
          </div>
          <div class="form-group">
            <label>ভাইব্রেটর (দিন)</label>
            <input type="number" id="vib-days" value="20" min="0" onchange="recalculate()">
            <span class="hint">প্রতি দিন ৳ ৫০০</span>
          </div>
        </div>
        <div style="margin-top: 12px; background: #f0f9f3; padding: 12px; border-radius: 8px;">
          মোট যন্ত্রপাতি ভাড়া: <strong id="equip-total">৳ ০</strong>
        </div>
      </div>
      <div class="card">
        <div class="card-title">⏱️ নির্মাণ সময়কাল</div>
        <div class="grid-3">
          <div>
            <div class="stat-label">মোট ম্যান-ডে</div>
            <div class="stat-value" id="total-manday" style="font-size: 20px;">০</div>
          </div>
          <div>
            <div class="stat-label">গড় দৈনিক শ্রমিক</div>
            <div class="stat-value" id="avg-workers" style="font-size: 20px;">০</div>
          </div>
          <div>
            <div class="stat-label">আনুমানিক সময়</div>
            <div class="stat-value" id="est-months" style="font-size: 20px; color: var(--accent);">০ মাস</div>
          </div>
        </div>
        <div style="margin-top: 12px; height: 12px; background: var(--border); border-radius: 6px; overflow: hidden;">
          <div class="time-bar" id="time-bar" style="width: 40%;"></div>
        </div>
        <div style="font-size: 12px; color: var(--text-muted); margin-top: 6px;">আনুমানিক নির্মাণ অগ্রগতি নির্দেশক</div>
      </div>
    </div>

    <!-- EXTRAS SECTION -->
    <div class="section" id="section-extras">
      <div class="card">
        <div class="card-title">⚡ অতিরিক্ত সুবিধা ও ডিজাইন</div>
        <div class="grid-3">
          <div class="form-group">
            <label>সোলার প্যানেল (kW)</label>
            <input type="number" id="solar-kw" value="0" min="0" onchange="recalculate()">
            <span class="hint">প্রতি kW ৳ ৮০,০০০</span>
          </div>
          <div class="form-group">
            <label>জেনারেটর (kVA)</label>
            <input type="number" id="gen-kva" value="0" min="0" onchange="recalculate()">
            <span class="hint">প্রতি kVA ৳ ১৫,০০০</span>
          </div>
          <div class="form-group">
            <label>বাউন্ডারি ওয়াল (ফুট)</label>
            <input type="number" id="boundary" value="0" min="0" onchange="recalculate()">
            <span class="hint">প্রতি ফুট ৳ ৬০০</span>
          </div>
          <div class="form-group">
            <label>ইন্টেরিয়র লেভেল</label>
            <select id="interior" onchange="recalculate()">
              <option value="0">নেই</option>
              <option value="150">বেসিক (৳ ১৫০/sqft)</option>
              <option value="350" selected>মিডিয়াম (৳ ৩৫০/sqft)</option>
              <option value="700">প্রিমিয়াম (৳ ৭০০/sqft)</option>
              <option value="1500">লাক্সারি (৳ ১৫০০/sqft)</option>
            </select>
          </div>
          <div class="form-group">
            <label>ওভারহেড ট্যাংক (লিটার)</label>
            <input type="number" id="tank" value="2000" min="0" onchange="recalculate()">
            <span class="hint">প্রতি ১০০০ লিটার ৳ ১২,০০০</span>
          </div>
          <div class="form-group">
            <label>ল্যান্ডস্কেপিং (বর্গফুট)</label>
            <input type="number" id="landscape" value="0" min="0" onchange="recalculate()">
            <span class="hint">প্রতি বর্গফুট ৳ ১২০</span>
          </div>
        </div>
        <div class="grid-4" style="margin-top: 16px;">
          <div class="form-group">
            <label>বেডরুম সংখ্যা</label>
            <input type="number" id="bedrooms" value="3" min="0" onchange="recalculate()">
            <span class="hint">প্রতি রুম ৳ ৮০,০০০</span>
          </div>
          <div class="form-group">
            <label>দরজার সংখ্যা</label>
            <input type="number" id="doors" value="8" min="0" onchange="recalculate()">
            <span class="hint">প্রতি দরজা ৳ ১২,০০০</span>
          </div>
          <div class="form-group">
            <label>জানালার সংখ্যা</label>
            <input type="number" id="windows" value="12" min="0" onchange="recalculate()">
            <span class="hint">প্রতি জানালা ৳ ৮,০০০</span>
          </div>
          <div class="form-group">
            <label>বাথরুম সংখ্যা</label>
            <input type="number" id="bathrooms" value="3" min="0" onchange="recalculate()">
            <span class="hint">প্রতি বাথরুম ৳ ৬০,০০০</span>
          </div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">☀️ সোলার ROI ক্যালকুলেটর</div>
        <div class="grid-3">
          <div class="form-group">
            <label>মাসিক বিদ্যুৎ বিল (৳)</label>
            <input type="number" id="monthly-bill" value="5000" onchange="calcSolarROI()">
          </div>
          <div class="form-group">
            <label>সোলার কভারেজ (%)</label>
            <input type="range" id="solar-pct" min="10" max="100" value="70" onchange="calcSolarROI(); document.getElementById('spct-out').textContent = this.value + '%'">
            <span id="spct-out" style="font-size: 13px; font-weight: 700;">৭০%</span>
          </div>
          <div id="solar-roi-result" style="background: #fffbeb; padding: 12px; border-radius: 8px; font-size: 13px;">
            ROI হিসাব করুন →
          </div>
        </div>
      </div>
    </div>

    <!-- FINANCIAL SECTION -->
    <div class="section" id="section-financial">
      <div class="fin-grid">
        <div>
          <div class="card">
            <div class="card-title">📈 আর্থিক চার্জ</div>
            <div class="form-group" style="margin-bottom: 12px;">
              <label>ভ্যাট (%)</label>
              <input type="number" id="vat" value="15" min="0" max="50" onchange="recalculate()">
            </div>
            <div class="form-group" style="margin-bottom: 12px;">
              <label>কন্টিনজেন্সি (%)</label>
              <input type="number" id="contingency" value="5" min="0" max="20" onchange="recalculate()">
            </div>
            <div class="form-group" style="margin-bottom: 12px;">
              <label>কন্ট্রাক্টর মার্জিন (%)</label>
              <input type="number" id="margin" value="10" min="0" max="30" onchange="recalculate()">
            </div>
            <div class="form-group">
              <label>মুদ্রাস্ফীতি প্রভিশন (%)</label>
              <input type="number" id="inflation" value="3" min="0" max="20" onchange="recalculate()">
            </div>
          </div>
          <div class="card">
            <div class="card-title">🏛️ ঋণ ক্যালকুলেটর</div>
            <div class="form-group" style="margin-bottom: 10px;">
              <label>ঋণের পরিমাণ (৳)</label>
              <input type="number" id="loan-amt" value="5000000" onchange="calcLoan()">
            </div>
            <div class="form-group" style="margin-bottom: 10px;">
              <label>বার্ষিক সুদ হার (%)</label>
              <input type="number" id="loan-rate" value="9" min="1" max="30" onchange="calcLoan()">
            </div>
            <div class="form-group" style="margin-bottom: 10px;">
              <label>মেয়াদ (বছর)</label>
              <input type="number" id="loan-years" value="15" min="1" max="30" onchange="calcLoan()">
            </div>
            <div class="loan-result" id="loan-result">
              <h3>মাসিক কিস্তি</h3>
              <div class="monthly" id="emi-val">৳ ৫০,৭১৪</div>
              <div class="details" id="loan-details">মোট পরিশোধ: ৳ ৯১,২৮,৫২০ | মোট সুদ: ৳ ৪১,২৮,৫২০</div>
            </div>
          </div>
        </div>
        <div>
          <div class="card">
            <div class="card-title">🏛️ সরকারি ও আইনি ফি</div>
            <div class="fee-row"><span>রাজউক অনুমোদন ফি</span><span class="fee-val" id="rajuk-fee">৳ ০</span></div>
            <div class="fee-row"><span>ওয়াসা সংযোগ ফি</span><span class="fee-val" id="wasa-fee">৳ ৩০,০০০</span></div>
            <div class="fee-row"><span>বিদ্যুৎ সাবস্টেশন ফি</span><span class="fee-val" id="elec-fee">৳ ০</span></div>
            <div class="fee-row"><span>গ্যাস সংযোগ ফি</span><span class="fee-val" id="gas-fee">৳ ৪০,০০০</span></div>
            <div class="fee-row"><span>ভূমি রেজিস্ট্রেশন (৭%)</span><span class="fee-val" id="reg-fee">৳ ০</span></div>
            <div class="fee-row"><span>স্ট্যাম্প ডিউটি (১.৫%)</span><span class="fee-val" id="stamp-fee">৳ ০</span></div>
            <div class="fee-row"><span>ল্যান্ড ট্যাক্স (বার্ষিক)</span><span class="fee-val">৳ ৫,০০০</span></div>
            <div class="fee-row"><span style="font-weight: 700;">মোট সরকারি ফি</span><span class="fee-val" id="total-govt">৳ ০</span></div>
            <div style="margin-top: 16px;">
              <div class="form-group">
                <label>জমির মূল্য (৳) — রেজিস্ট্রেশন হিসাবের জন্য</label>
                <input type="number" id="land-price" value="0" onchange="recalculate()">
              </div>
            </div>
          </div>
          <div class="card">
            <div class="card-title">📋 খরচের সারসংক্ষেপ</div>
            <div class="breakdown-row"><span>মূল নির্মাণ খরচ</span><span id="br-base">৳ ০</span></div>
            <div class="breakdown-row"><span>শ্রমিক ও যন্ত্রপাতি</span><span id="br-labor">৳ ০</span></div>
            <div class="breakdown-row"><span>অতিরিক্ত সুবিধা</span><span id="br-extras">৳ ০</span></div>
            <div class="breakdown-row"><span>স্পেশাল ফিচারস</span><span id="br-special">৳ ০</span></div>
            <div class="breakdown-row"><span>ভ্যাট ও চার্জ</span><span id="br-vat">৳ ০</span></div>
            <div class="breakdown-row"><span>সরকারি ফি</span><span id="br-govt">৳ ০</span></div>
            <div class="breakdown-row total"><span>সর্বমোট</span><span id="br-total">৳ ০</span></div>
          </div>
        </div>
      </div>
    </div>

    <!-- SPECIAL SECTION -->
    <div class="section" id="section-special">
      <div class="alert alert-warning">
        ⭐ বিল্ডিং টাইপ পরিবর্তন করলে এই তালিকা স্বয়ংক্রিয়ভাবে আপডেট হবে। পছন্দমতো ফিচার বেছে নিন।
      </div>
      <div class="card">
        <div class="card-title" id="special-title">⭐ স্পেশাল ফিচারস (আবাসিক)</div>
        <div class="feature-grid" id="special-features"></div>
        <div style="margin-top: 16px; background: #f0f9f3; padding: 12px; border-radius: 8px;">
          স্পেশাল ফিচার মোট: <strong id="special-total">৳ ০</strong>
        </div>
      </div>
    </div>

    <!-- REPORT SECTION -->
    <div class="section" id="section-report">
      <div class="report-header">
        <div class="report-title">🏗️ নির্মাণ ব্যয় অনুমান রিপোর্ট</div>
        <div class="report-sub" id="report-date"></div>
      </div>
      <div class="grid-2">
        <div class="card">
          <div class="card-title">📊 খরচ বিভাজন (ডোনাট চার্ট)</div>
          <div class="chart-wrap" style="height: 260px;">
            <canvas id="donutChart" role="img" aria-label="খরচ বিভাজন ডোনাট চার্ট"></canvas>
          </div>
          <div id="donut-legend" style="margin-top: 12px; font-size: 12px; display: flex; flex-wrap: wrap; gap: 10px;"></div>
        </div>
        <div class="card">
          <div class="card-title">📋 বিস্তারিত হিসাব</div>
          <div id="detailed-breakdown"></div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">🏢 তলা অনুযায়ী খরচ বিভাজন</div>
        <div class="chart-wrap" style="height: 220px;">
          <canvas id="floorChart" role="img" aria-label="তলা অনুযায়ী খরচ বার চার্ট"></canvas>
        </div>
      </div>
      <div class="card">
        <div class="card-title">📤 রিপোর্ট এক্সপোর্ট</div>
        <div style="display: flex; gap: 12px; flex-wrap: wrap;">
          <button class="btn btn-primary" onclick="exportPDF()">📄 PDF রিপোর্ট ডাউনলোড</button>
          <button class="btn btn-outline" onclick="exportCSV()">📊 Excel (CSV) এক্সপোর্ট</button>
          <button class="btn btn-accent" onclick="printReport()">🖨️ প্রিন্ট করুন</button>
          <button class="btn btn-outline" onclick="shareReport()">🔗 লিংক শেয়ার</button>
        </div>
      </div>
    </div>

  </div><!-- /content -->
</div><!-- /main -->
</div><!-- /app -->

<script>
// ===== DATA =====
const districts = {
  dhaka: ['ঢাকা','গাজীপুর','নারায়ণগঞ্জ','মুন্সীগঞ্জ','মানিকগঞ্জ','নরসিংদী','কিশোরগঞ্জ','টাঙ্গাইল','ফরিদপুর','মাদারীপুর','শরীয়তপুর','রাজবাড়ী','গোপালগঞ্জ'],
  chittagong: ['চট্টগ্রাম','কক্সবাজার','বান্দরবান','রাঙ্গামাটি','খাগড়াছড়ি','ফেনী','লক্ষ্মীপুর','নোয়াখালী','কুমিল্লা','চাঁদপুর','ব্রাহ্মণবাড়িয়া'],
  rajshahi: ['রাজশাহী','নওগাঁ','নাটোর','চাঁপাইনবাবগঞ্জ','বগুড়া','পাবনা','সিরাজগঞ্জ','জয়পুরহাট'],
  khulna: ['খুলনা','বাগেরহাট','সাতক্ষীরা','যশোর','ঝিনাইদহ','মেহেরপুর','চুয়াডাঙ্গা','কুষ্টিয়া','মাগুরা','নড়াইল'],
  barisal: ['বরিশাল','পটুয়াখালী','পিরোজপুর','ঝালকাঠি','বরগুনা','ভোলা'],
  sylhet: ['সিলেট','মৌলভীবাজার','হবিগঞ্জ','সুনামগঞ্জ'],
  rangpur: ['রংপুর','দিনাজপুর','গাইবান্ধা','কুড়িগ্রাম','লালমনিরহাট','নীলফামারী','পঞ্চগড়','ঠাকুরগাঁও'],
  mymensingh: ['ময়মনসিংহ','নেত্রকোনা','জামালপুর','শেরপুর']
};

const upazilas = {
  'ঢাকা': ['মিরপুর','গুলশান','মতিঝিল','উত্তরা','ধানমন্ডি','মোহাম্মদপুর','লালবাগ','রমনা','শাহবাগ','সাভার','ডেমরা','খিলগাঁও'],
  'চট্টগ্রাম': ['কোতোয়ালি','পাঁচলাইশ','চান্দগাঁও','পতেঙ্গা','বায়েজিদ','হালিশহর','বন্দর','সীতাকুণ্ড','মিরসরাই','রাউজান'],
  'কক্সবাজার': ['কক্সবাজার সদর','চকোরিয়া','রামু','উখিয়া','টেকনাফ','মহেশখালী','কুতুবদিয়া','পেকুয়া'],
  'রাজশাহী': ['রাজশাহী সদর','বোয়ালমারী','পুঠিয়া','মোহনপুর','বাগমারা','দুর্গাপুর'],
  'খুলনা': ['খুলনা সদর','দাকোপ','কয়রা','পাইকগাছা','বটিয়াঘাটা','রূপসা','দিঘলিয়া'],
  'সিলেট': ['সিলেট সদর','বালাগঞ্জ','বিয়ানীবাজার','গোলাপগঞ্জ','জকিগঞ্জ','কানাইঘাট'],
  'বরিশাল': ['বরিশাল সদর','বানারীপাড়া','বাবুগঞ্জ','বাকেরগঞ্জ','হিজলা','মেহেন্দিগঞ্জ'],
  'রংপুর': ['রংপুর সদর','কাউনিয়া','গঙ্গাচড়া','মিঠাপুকুর','পীরগাছা','পীরগঞ্জ'],
  'ময়মনসিংহ': ['ময়মনসিংহ সদর','ভালুকা','গফরগাঁও','ফুলবাড়িয়া','ত্রিশাল','হালুয়াঘাট'],
  'গাজীপুর': ['গাজীপুর সদর','কালিয়াকৈর','কালীগঞ্জ','কাপাসিয়া','শ্রীপুর'],
  'নারায়ণগঞ্জ': ['নারায়ণগঞ্জ সদর','আড়াইহাজার','বন্দর','রূপগঞ্জ','সোনারগাঁও'],
  'রাঙ্গামাটি': ['রাঙ্গামাটি সদর','কাপ্তাই','বাঘাইছড়ি','বরকল','লংগদু','রাজস্থলী'],
  'বান্দরবান': ['বান্দরবান সদর','আলীকদম','নাইক্ষ্যংছড়ি','রোয়াংছড়ি','রুমা','থানচি'],
  'খাগড়াছড়ি': ['খাগড়াছড়ি সদর','দিঘীনালা','লক্ষীছড়ি','মহালছড়ি','মানিকছড়ি']
};

const specialFeatures = {
  '1.0': [ // আবাসিক
    {name: 'অতিরিক্ত রুম', cost: 80000, unit: 'টি', qty: 1},
    {name: 'পার্কিং স্পেস', cost: 120000, unit: 'টি', qty: 1},
    {name: 'ছাদ বাগান (Rooftop Garden)', cost: 150000, unit: '', qty: 1},
    {name: 'সিসি ক্যামেরা সিস্টেম', cost: 35000, unit: 'সেট', qty: 1},
    {name: 'ফায়ার এক্সটিংগুইশার', cost: 5000, unit: 'টি', qty: 2},
    {name: 'ইন্টারনেট ক্যাবলিং', cost: 25000, unit: '', qty: 1},
    {name: 'LED লাইটিং সিস্টেম', cost: 45000, unit: '', qty: 1},
    {name: 'ইন্টারকম সিস্টেম', cost: 20000, unit: '', qty: 1},
    {name: 'হুইলচেয়ার র্যাম্প', cost: 30000, unit: '', qty: 1},
    {name: 'সুইমিং পুল', cost: 1500000, unit: '', qty: 1},
    {name: 'হোম থিয়েটার রুম', cost: 500000, unit: '', qty: 1},
    {name: 'স্মার্ট হোম অটোমেশন', cost: 300000, unit: '', qty: 1},
  ],
  '1.68': [ // হাসপাতাল
    {name: 'আইসিইউ বেড', cost: 500000, unit: 'টি', qty: 5},
    {name: 'অ্যাম্বুলেন্স বে', cost: 200000, unit: '', qty: 1},
    {name: 'প্যাথলজি ল্যাব', cost: 1500000, unit: '', qty: 1},
    {name: 'অপারেশন থিয়েটার', cost: 3000000, unit: 'টি', qty: 1},
    {name: 'অক্সিজেন লাইন', cost: 500000, unit: '', qty: 1},
    {name: 'ইমেজিং (এক্স-রে, আলট্রা)', cost: 2000000, unit: '', qty: 1},
    {name: 'ফার্মেসি', cost: 300000, unit: '', qty: 1},
    {name: 'হুইলচেয়ার র্যাম্প', cost: 50000, unit: '', qty: 1},
    {name: 'এমার্জেন্সি জেনারেটর ব্যাকআপ', cost: 500000, unit: '', qty: 1},
    {name: 'বায়ো-ওয়েস্ট ম্যানেজমেন্ট', cost: 400000, unit: '', qty: 1},
    {name: 'নার্স কলিং সিস্টেম', cost: 200000, unit: '', qty: 1},
    {name: 'নেগেটিভ প্রেসার রুম', cost: 800000, unit: 'টি', qty: 1},
  ],
  '1.40': [ // হোটেল ★★★
    {name: 'কমার্শিয়াল কিচেন', cost: 2000000, unit: '', qty: 1},
    {name: 'জিম ও স্পা', cost: 1500000, unit: '', qty: 1},
    {name: 'কনফারেন্স হল', cost: 1000000, unit: '', qty: 1},
    {name: 'রেস্তোরাঁ', cost: 1500000, unit: '', qty: 1},
    {name: 'লবি ডেকোরেশন', cost: 800000, unit: '', qty: 1},
    {name: 'লন্ড্রি সিস্টেম', cost: 500000, unit: '', qty: 1},
    {name: 'রুফটপ পুল', cost: 3000000, unit: '', qty: 1},
    {name: 'ভ্যালেট পার্কিং সিস্টেম', cost: 200000, unit: '', qty: 1},
    {name: 'স্মার্ট রুম অটোমেশন', cost: 100000, unit: 'রুম', qty: 20},
    {name: 'সাউন্ডপ্রুফ রুম', cost: 50000, unit: 'রুম', qty: 5},
    {name: 'অডিও ভিজুয়াল রুম', cost: 500000, unit: '', qty: 1},
    {name: 'স্যাটেলাইট টিভি সিস্টেম', cost: 200000, unit: '', qty: 1},
  ],
  '1.20': [ // স্কুল
    {name: 'লাইব্রেরি', cost: 500000, unit: '', qty: 1},
    {name: 'কম্পিউটার ল্যাব', cost: 1000000, unit: '', qty: 1},
    {name: 'সায়েন্স ল্যাব', cost: 800000, unit: '', qty: 1},
    {name: 'খেলার মাঠ সেটআপ', cost: 300000, unit: '', qty: 1},
    {name: 'স্মার্ট ক্লাসরুম', cost: 150000, unit: 'টি', qty: 5},
    {name: 'অডিটোরিয়াম', cost: 2000000, unit: '', qty: 1},
    {name: 'সিসি ক্যামেরা সিস্টেম', cost: 100000, unit: '', qty: 1},
    {name: 'শিক্ষক লাউঞ্জ', cost: 200000, unit: '', qty: 1},
    {name: 'স্কুল বাস বে', cost: 150000, unit: '', qty: 1},
    {name: 'ফায়ার অ্যালার্ম সিস্টেম', cost: 80000, unit: '', qty: 1},
    {name: 'হুইলচেয়ার র্যাম্প', cost: 40000, unit: '', qty: 1},
    {name: 'স্মার্ট বোর্ড', cost: 80000, unit: 'টি', qty: 5},
  ],
  '1.10': [ // মসজিদ
    {name: 'মিনার (ছোট)', cost: 200000, unit: 'টি', qty: 2},
    {name: 'সাউন্ড সিস্টেম', cost: 150000, unit: '', qty: 1},
    {name: 'মিহরাব (মার্বেল)', cost: 300000, unit: '', qty: 1},
    {name: 'মিম্বার (কাঠ)', cost: 80000, unit: '', qty: 1},
    {name: 'ওজুর স্থান (পূর্ণাঙ্গ)', cost: 200000, unit: '', qty: 1},
    {name: 'ইমাম কক্ষ', cost: 80000, unit: '', qty: 1},
    {name: 'মহিলা সেকশন', cost: 300000, unit: '', qty: 1},
    {name: 'পানি ফিল্টার', cost: 30000, unit: '', qty: 1},
    {name: 'কুরআন তাক', cost: 50000, unit: '', qty: 1},
    {name: 'সিসি ক্যামেরা', cost: 40000, unit: '', qty: 1},
    {name: 'ঈদগাহ মাঠ', cost: 200000, unit: '', qty: 1},
    {name: 'জেনারেটর ব্যাকআপ', cost: 150000, unit: '', qty: 1},
  ],
  '1.05': [ // শিল্প কারখানা
    {name: 'শ্রমিক ডর্মিটরি', cost: 1000000, unit: '', qty: 1},
    {name: 'ক্যান্টিন', cost: 500000, unit: '', qty: 1},
    {name: 'ডাস্ট কালেক্টর সিস্টেম', cost: 800000, unit: '', qty: 1},
    {name: 'থ্রি-ফেজ ইলেকট্রিক সাবস্টেশন', cost: 2000000, unit: '', qty: 1},
    {name: 'ক্রেন ও হোয়েস্ট', cost: 1500000, unit: 'টি', qty: 1},
    {name: 'লোডিং বে ও ডক লেভেলার', cost: 500000, unit: 'টি', qty: 2},
    {name: 'রাসায়নিক প্রতিরোধী ফ্লোরিং', cost: 300000, unit: '', qty: 1},
    {name: 'ভেন্টিলেশন সিস্টেম', cost: 600000, unit: '', qty: 1},
    {name: 'ফায়ার হাইড্র্যান্ট', cost: 200000, unit: '', qty: 1},
    {name: 'নিরাপত্তা গার্ড পোস্ট', cost: 80000, unit: 'টি', qty: 2},
    {name: 'ETP (বর্জ্য পরিশোধন)', cost: 1500000, unit: '', qty: 1},
    {name: 'সোলার রুফটপ', cost: 500000, unit: '', qty: 1},
  ]
};

// Currency
let currency = 'BDT';
const exchangeRates = {BDT: 1, USD: 0.0091, INR: 0.76};
const currencySymbol = {BDT: '৳', USD: '$', INR: '₹'};

function fmt(n) {
  const v = n * exchangeRates[currency];
  const sym = currencySymbol[currency];
  if (currency === 'BDT') return sym + ' ' + Math.round(v).toLocaleString('bn-BD');
  return sym + ' ' + v.toFixed(2);
}

function setCurrency(c) {
  currency = c;
  document.querySelectorAll('.cur-btn').forEach(b => b.classList.remove('active'));
  event.target.classList.add('active');
  recalculate();
}

// Labor data
let laborData = [
  {name: 'হেড মিস্ত্রি', count: 2, wage: 1200, days: 120},
  {name: 'রড বাইন্ডার', count: 4, wage: 900, days: 90},
  {name: 'ইলেকট্রিশিয়ান', count: 2, wage: 1000, days: 45},
  {name: 'প্লাম্বার', count: 2, wage: 950, days: 40},
  {name: 'পেইন্টার', count: 3, wage: 800, days: 30},
  {name: 'হেল্পার', count: 6, wage: 600, days: 120},
];

function renderLaborList() {
  const el = document.getElementById('labor-list');
  el.innerHTML = '';
  laborData.forEach((l, i) => {
    const total = l.count * l.wage * l.days;
    el.innerHTML += `<div class="labor-row">
      <span><input type="text" value="${l.name}" onchange="laborData[${i}].name=this.value" style="width:100%; border:none; background:transparent; font-family:inherit; font-size:13px;"></span>
      <input type="number" value="${l.count}" min="1" onchange="laborData[${i}].count=+this.value; recalculate();" class="labor-row" style="display:inline; width:60px; padding:4px 6px; border:1px solid var(--border); border-radius:4px;">
      <input type="number" value="${l.wage}" onchange="laborData[${i}].wage=+this.value; recalculate();" style="width:90px; padding:4px 6px; border:1px solid var(--border); border-radius:4px; font-family:inherit; font-size:13px;">
      <input type="number" value="${l.days}" onchange="laborData[${i}].days=+this.value; recalculate();" style="width:70px; padding:4px 6px; border:1px solid var(--border); border-radius:4px; font-family:inherit; font-size:13px;">
      <span class="labor-total">${Math.round(total).toLocaleString()}</span>
    </div>`;
  });
}

function addLaborRow() {
  laborData.push({name: 'নতুন শ্রমিক', count: 1, wage: 700, days: 30});
  renderLaborList();
  recalculate();
}

// Special features
let selectedFeatures = {};
function renderSpecialFeatures() {
  const btype = document.getElementById('bldg-type').value;
  const features = specialFeatures[btype] || specialFeatures['1.0'];
  const container = document.getElementById('special-features');
  const title = document.getElementById('bldg-type').options[document.getElementById('bldg-type').selectedIndex].text;
  document.getElementById('special-title').innerHTML = `⭐ স্পেশাল ফিচারস (${title})`;
  selectedFeatures = {};
  container.innerHTML = '';
  features.forEach((f, i) => {
    container.innerHTML += `<div class="feature-item" id="feat-${i}" onclick="toggleFeature(${i}, ${f.cost})" style="flex-direction:column; align-items:flex-start;">
      <div style="display:flex; align-items:center; gap:8px; width:100%;">
        <input type="checkbox" id="fchk-${i}" onchange="toggleFeature(${i}, ${f.cost})" onclick="event.stopPropagation()">
        <span style="flex:1;">${f.name}</span>
        ${f.unit ? `<input type="number" id="fqty-${i}" value="${f.qty}" min="1" style="width:50px; padding:3px 5px; border:1px solid var(--border); border-radius:4px; font-size:12px;" onclick="event.stopPropagation()" onchange="recalculate()">` : ''}
      </div>
      <div style="font-size:11px; color:var(--text-muted); padding-left:24px;">৳ ${(f.cost).toLocaleString()}${f.unit ? ' / ' + f.unit : ''}</div>
    </div>`;
  });
  recalculate();
}

function toggleFeature(i, cost) {
  const chk = document.getElementById(`fchk-${i}`);
  const item = document.getElementById(`feat-${i}`);
  chk.checked = !chk.checked;
  item.classList.toggle('selected', chk.checked);
  recalculate();
}

function getSpecialTotal() {
  const btype = document.getElementById('bldg-type').value;
  const features = specialFeatures[btype] || specialFeatures['1.0'];
  let total = 0;
  features.forEach((f, i) => {
    const chk = document.getElementById(`fchk-${i}`);
    if (chk && chk.checked) {
      const qtyEl = document.getElementById(`fqty-${i}`);
      const qty = qtyEl ? +qtyEl.value : 1;
      total += f.cost * qty;
    }
  });
  return total;
}

// Location data
function updateDistricts() {
  const div = document.getElementById('division').value;
  const dsel = document.getElementById('district');
  dsel.innerHTML = '<option value="">-- জেলা নির্বাচন --</option>';
  (districts[div] || []).forEach(d => {
    dsel.innerHTML += `<option value="${d}">${d}</option>`;
  });
  document.getElementById('upazila').innerHTML = '<option value="">-- উপজেলা নির্বাচন --</option>';
  recalculate();
}

function updateUpazilas() {
  const dist = document.getElementById('district').value;
  const usel = document.getElementById('upazila');
  usel.innerHTML = '<option value="">-- উপজেলা নির্বাচন --</option>';
  (upazilas[dist] || []).forEach(u => {
    usel.innerHTML += `<option value="${u}">${u}</option>`;
  });
  recalculate();
}

function updateLocationFactor() {
  recalculate();
}

function onBuildingTypeChange() {
  renderSpecialFeatures();
  recalculate();
}

// Material calculation
function calcMaterials(sqft) {
  const wallArea = sqft * 0.35;
  const bricks = Math.round(wallArea * 50.8);
  const cement = Math.round(sqft * 0.38);
  const sand = Math.round(sqft * 1.2);
  const stone = Math.round(sqft * 0.8);
  const rod = Math.round(sqft * 4.5);
  const tiles = Math.round(sqft * 0.65);
  const paint = Math.round(sqft * 0.12);
  const wire = Math.round(sqft * 2.5);
  const sanitary = Math.round(sqft / 500) + 1;
  const doors = +document.getElementById('doors').value || 8;
  const windows = +document.getElementById('windows').value || 12;

  return [
    {name: 'ইট', qty: bricks, unit: 'পিস', rate: 14, total: bricks * 14},
    {name: 'সিমেন্ট', qty: cement, unit: 'বস্তা (৫০ কেজি)', rate: 520, total: cement * 520},
    {name: 'বালি', qty: sand, unit: 'cft', rate: 38, total: sand * 38},
    {name: 'পাথর/খোয়া', qty: stone, unit: 'cft', rate: 55, total: stone * 55},
    {name: 'রড (Fe500)', qty: rod, unit: 'kg', rate: 95, total: rod * 95},
    {name: 'টাইলস', qty: tiles, unit: 'sqft', rate: 85, total: tiles * 85},
    {name: 'পেইন্ট', qty: paint, unit: 'লিটার', rate: 280, total: Math.round(paint) * 280},
    {name: 'ইলেকট্রিক তার', qty: wire, unit: 'মিটার', rate: 45, total: Math.round(wire) * 45},
    {name: 'স্যানিটারি সেট', qty: sanitary, unit: 'সেট', rate: 35000, total: sanitary * 35000},
    {name: 'দরজা (কাঠ/স্টিল)', qty: doors, unit: 'টি', rate: 12000, total: doors * 12000},
    {name: 'জানালা (অ্যালুমিনিয়াম)', qty: windows, unit: 'টি', rate: 8000, total: windows * 8000},
  ];
}

// Charts
let donutChartObj = null, matChartObj = null, floorChartObj = null;

function updateCharts(breakdown) {
  const colors = ['#1a6b3a','#e8a020','#3b82f6','#ef4444','#8b5cf6','#14b8a6'];
  // Donut
  if (donutChartObj) donutChartObj.destroy();
  const dCtx = document.getElementById('donutChart');
  if (dCtx) {
    donutChartObj = new Chart(dCtx, {
      type: 'doughnut',
      data: {
        labels: ['মূল নির্মাণ','শ্রমিক ও যন্ত্র','অতিরিক্ত','স্পেশাল','ভ্যাট ও চার্জ','সরকারি ফি'],
        datasets: [{
          data: [breakdown.base, breakdown.labor, breakdown.extras, breakdown.special, breakdown.vat, breakdown.govt],
          backgroundColor: colors,
          borderWidth: 2,
          borderColor: '#fff'
        }]
      },
      options: {responsive: true, maintainAspectRatio: false, plugins: {legend: {display: false}}}
    });
    // Legend
    const leg = document.getElementById('donut-legend');
    if (leg) {
      const labels = ['মূল নির্মাণ','শ্রমিক ও যন্ত্র','অতিরিক্ত','স্পেশাল','ভ্যাট ও চার্জ','সরকারি ফি'];
      const vals = [breakdown.base, breakdown.labor, breakdown.extras, breakdown.special, breakdown.vat, breakdown.govt];
      const total = vals.reduce((a,b) => a+b, 0);
      leg.innerHTML = labels.map((l,i) => `<span style="display:flex;align-items:center;gap:4px;"><span style="width:10px;height:10px;border-radius:2px;background:${colors[i]};display:inline-block;"></span>${l} ${total > 0 ? Math.round(vals[i]/total*100) : 0}%</span>`).join('');
    }
  }

  // Floor chart
  const floors = +document.getElementById('floors').value || 1;
  const baseCostPerFloor = breakdown.base / floors;
  const floorLabels = [], floorData = [];
  for (let i = 1; i <= Math.min(floors, 10); i++) {
    floorLabels.push(`${i} তলা`);
    const factor = i === 1 ? 1.15 : i <= 3 ? 1.0 : 0.92;
    floorData.push(Math.round(baseCostPerFloor * factor));
  }
  if (floorChartObj) floorChartObj.destroy();
  const fCtx = document.getElementById('floorChart');
  if (fCtx) {
    floorChartObj = new Chart(fCtx, {
      type: 'bar',
      data: {
        labels: floorLabels,
        datasets: [{label: 'খরচ (৳)', data: floorData, backgroundColor: '#2d9653', borderRadius: 6}]
      },
      options: {
        responsive: true, maintainAspectRatio: false,
        plugins: {legend: {display: false}},
        scales: {
          y: {ticks: {callback: v => '৳' + (v/100000).toFixed(1) + 'লা'}},
          x: {ticks: {autoSkip: false}}
        }
      }
    });
  }

  // Material chart
  const mats = calcMaterials(+document.getElementById('total-area').value || 2000);
  if (matChartObj) matChartObj.destroy();
  const mCtx = document.getElementById('matChart');
  if (mCtx) {
    matChartObj = new Chart(mCtx, {
      type: 'bar',
      data: {
        labels: mats.map(m => m.name),
        datasets: [{
          label: 'খরচ (৳)',
          data: mats.map(m => m.total),
          backgroundColor: mats.map((_, i) => colors[i % colors.length]),
          borderRadius: 4
        }]
      },
      options: {
        responsive: true, maintainAspectRatio: false,
        plugins: {legend: {display: false}},
        scales: {
          y: {ticks: {callback: v => '৳' + Math.round(v/1000) + 'হা'}},
          x: {ticks: {autoSkip: false, maxRotation: 30}}
        }
      }
    });
  }
}

// Solar ROI
function calcSolarROI() {
  const kw = +document.getElementById('solar-kw').value || 0;
  if (!kw) { document.getElementById('solar-roi-result').innerHTML = 'সোলার প্যানেলের পরিমাণ দিন'; return; }
  const cost = kw * 80000;
  const monthly = (+document.getElementById('monthly-bill').value || 5000) * (+document.getElementById('solar-pct').value || 70) / 100;
  const years = cost / (monthly * 12);
  document.getElementById('solar-roi-result').innerHTML = `
    <div style="font-weight:700; color:var(--primary-dark); font-size:15px;">ROI: ${years.toFixed(1)} বছর</div>
    <div style="font-size:12px; color:var(--text-muted); margin-top:4px;">ইনস্টলেশন: ৳ ${cost.toLocaleString()}<br>মাসিক সঞ্চয়: ৳ ${Math.round(monthly).toLocaleString()}</div>
  `;
}

// Loan calculator
function calcLoan() {
  const P = +document.getElementById('loan-amt').value || 0;
  const r = (+document.getElementById('loan-rate').value || 9) / 100 / 12;
  const n = (+document.getElementById('loan-years').value || 15) * 12;
  if (P === 0 || r === 0) return;
  const emi = P * r * Math.pow(1+r,n) / (Math.pow(1+r,n) - 1);
  const total = emi * n;
  document.getElementById('emi-val').textContent = '৳ ' + Math.round(emi).toLocaleString();
  document.getElementById('loan-details').textContent = `মোট পরিশোধ: ৳ ${Math.round(total).toLocaleString()} | মোট সুদ: ৳ ${Math.round(total - P).toLocaleString()}`;
}

// MAIN CALCULATION
function recalculate() {
  const sqft = +document.getElementById('total-area').value || 0;
  const floors = +document.getElementById('floors').value || 1;
  const baseRate = +document.getElementById('base-rate').value || 2200;
  const btype = +document.getElementById('bldg-type').value || 1.0;
  const quality = +document.getElementById('quality').value || 1.0;
  const structure = +document.getElementById('structure').value || 1.0;
  const foundation = +document.getElementById('foundation').value || 0.12;
  const concreteGrade = +document.getElementById('concrete-grade').value || 1.08;
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

  // Environment factor
  const envFactor = areaType * seismic * flood * specEnv;
  document.getElementById('ef1').textContent = areaType.toFixed(2);
  document.getElementById('ef2').textContent = seismic.toFixed(2);
  document.getElementById('ef3').textContent = flood.toFixed(2);
  document.getElementById('ef4').textContent = specEnv.toFixed(2);
  document.getElementById('ef-total').textContent = envFactor.toFixed(3);

  // Config factor
  const configFactor = btype * quality * structure * concreteGrade * envFactor * (1 + foundation);
  document.getElementById('config-factor') && (document.getElementById('config-factor').value = configFactor.toFixed(3));

  // Base cost
  const baseCost = sqft * baseRate * configFactor;

  // Materials
  const mats = calcMaterials(sqft);
  const matTotal = mats.reduce((s, m) => s + m.total, 0);

  // Render materials table
  const tbody = document.getElementById('mat-tbody');
  if (tbody) {
    tbody.innerHTML = mats.map(m => `
      <tr>
        <td>${m.name}</td>
        <td class="qty">${m.qty.toLocaleString()}</td>
        <td>${m.unit}</td>
        <td>৳ ${m.rate.toLocaleString()}</td>
        <td class="amount">৳ ${m.total.toLocaleString()}</td>
      </tr>
    `).join('') + `<tr style="font-weight:700; background:#f0f9f3;">
      <td colspan="4" style="padding:10px 14px; color:var(--primary-dark);">মোট ম্যাটেরিয়াল খরচ</td>
      <td class="amount" style="color:var(--primary);">৳ ${matTotal.toLocaleString()}</td>
    </tr>`;
  }

  // Labor
  let laborTotal = 0, totalManday = 0;
  laborData.forEach(l => {
    laborTotal += l.count * l.wage * l.days;
    totalManday += l.count * l.days;
  });
  const craneHrs = +document.getElementById('crane-hrs').value || 0;
  const mixerDays = +document.getElementById('mixer-days').value || 0;
  const pumpDays = +document.getElementById('pump-days').value || 0;
  const vibDays = +document.getElementById('vib-days').value || 0;
  const equipTotal = craneHrs * 3500 + mixerDays * 1800 + pumpDays * 8000 + vibDays * 500;
  const totalLabor = laborTotal + equipTotal;

  if (document.getElementById('equip-total')) document.getElementById('equip-total').textContent = '৳ ' + Math.round(equipTotal).toLocaleString();
  if (document.getElementById('total-manday')) document.getElementById('total-manday').textContent = Math.round(totalManday).toLocaleString();
  const avgWorkers = Math.round(totalManday / 120);
  if (document.getElementById('avg-workers')) document.getElementById('avg-workers').textContent = avgWorkers;
  const estMonths = Math.max(1, Math.round(totalManday / (avgWorkers || 1) / 25));
  if (document.getElementById('est-months')) document.getElementById('est-months').textContent = estMonths + ' মাস';

  // Extras
  const solar = (+document.getElementById('solar-kw').value || 0) * 80000;
  const gen = (+document.getElementById('gen-kva').value || 0) * 15000;
  const boundary = (+document.getElementById('boundary').value || 0) * 600;
  const interior = (+document.getElementById('interior').value || 0) * sqft;
  const tank = Math.round((+document.getElementById('tank').value || 0) / 1000) * 12000;
  const landscape = (+document.getElementById('landscape').value || 0) * 120;
  const bedrooms = (+document.getElementById('bedrooms').value || 0) * 80000;
  const doors = (+document.getElementById('doors').value || 0) * 12000;
  const windows = (+document.getElementById('windows').value || 0) * 8000;
  const bathrooms = (+document.getElementById('bathrooms').value || 0) * 60000;
  const liftCost = lifts * 2500000;
  const extrasTotal = solar + gen + boundary + interior + tank + landscape + bedrooms + doors + windows + bathrooms + liftCost;

  // Special
  const specialTotal = getSpecialTotal();
  if (document.getElementById('special-total')) document.getElementById('special-total').textContent = '৳ ' + Math.round(specialTotal).toLocaleString();

  // Government fees
  const rajukFee = sqft * floors * 15 + (floors > 5 ? (floors - 5) * sqft * 5 : 0);
  const wasaFee = 30000;
  const elecFee = sqft > 5000 ? 150000 : 50000;
  const gasFee = 40000 + gasDist * 800;
  const regFee = landPrice * 0.07;
  const stampFee = landPrice * 0.015;
  const govtTotal = rajukFee + wasaFee + elecFee + gasFee + regFee + stampFee + 5000;

  if (document.getElementById('rajuk-fee')) document.getElementById('rajuk-fee').textContent = '৳ ' + Math.round(rajukFee).toLocaleString();
  if (document.getElementById('wasa-fee')) document.getElementById('wasa-fee').textContent = '৳ ' + Math.round(wasaFee).toLocaleString();
  if (document.getElementById('elec-fee')) document.getElementById('elec-fee').textContent = '৳ ' + Math.round(elecFee).toLocaleString();
  if (document.getElementById('gas-fee')) document.getElementById('gas-fee').textContent = '৳ ' + Math.round(gasFee).toLocaleString();
  if (document.getElementById('reg-fee')) document.getElementById('reg-fee').textContent = '৳ ' + Math.round(regFee).toLocaleString();
  if (document.getElementById('stamp-fee')) document.getElementById('stamp-fee').textContent = '৳ ' + Math.round(stampFee).toLocaleString();
  if (document.getElementById('total-govt')) document.getElementById('total-govt').textContent = '৳ ' + Math.round(govtTotal).toLocaleString();

  // Subtotal before charges
  const subTotal = baseCost + totalLabor + extrasTotal + specialTotal;

  // VAT and charges
  const vatAmt = subTotal * vat / 100;
  const conAmt = subTotal * contingency / 100;
  const marAmt = subTotal * margin / 100;
  const infAmt = subTotal * inflation / 100;
  const chargesTotal = vatAmt + conAmt + marAmt + infAmt;

  const grandTotal = subTotal + chargesTotal + govtTotal;
  const perSqft = sqft > 0 ? grandTotal / sqft : 0;

  // Update summary
  document.getElementById('total-cost').textContent = fmt(grandTotal);
  document.getElementById('cost-per-sqft').textContent = 'প্রতি বর্গফুট: ' + fmt(perSqft);
  document.getElementById('construction-time').textContent = estMonths + ' মাস';
  document.getElementById('manday-info').textContent = 'মোট ম্যান-ডে: ' + Math.round(totalManday).toLocaleString();
  document.getElementById('area-factor').textContent = envFactor.toFixed(2);
  document.getElementById('zone-info').textContent = 'ভূমিকম্প জোন: ' + document.getElementById('seismic-zone').options[document.getElementById('seismic-zone').selectedIndex].text.split(' ')[0];
  document.getElementById('govt-cost').textContent = fmt(govtTotal + chargesTotal);

  // Breakdown
  const breakdownEls = {
    'br-base': baseCost,
    'br-labor': totalLabor,
    'br-extras': extrasTotal,
    'br-special': specialTotal,
    'br-vat': chargesTotal,
    'br-govt': govtTotal,
    'br-total': grandTotal
  };
  Object.entries(breakdownEls).forEach(([id, val]) => {
    const el = document.getElementById(id);
    if (el) el.textContent = fmt(val);
  });

  // Detailed breakdown in report
  const dBreak = document.getElementById('detailed-breakdown');
  if (dBreak) {
    dBreak.innerHTML = `
      <div class="breakdown-row"><span>বেস নির্মাণ (${sqft.toLocaleString()} sqft × ৳${baseRate} × ${configFactor.toFixed(2)})</span><span>${fmt(baseCost)}</span></div>
      <div class="breakdown-row"><span>শ্রমিক মজুরি</span><span>${fmt(laborTotal)}</span></div>
      <div class="breakdown-row"><span>যন্ত্রপাতি ভাড়া</span><span>${fmt(equipTotal)}</span></div>
      <div class="breakdown-row"><span>লিফট (${lifts}টি)</span><span>${fmt(liftCost)}</span></div>
      <div class="breakdown-row"><span>ইন্টেরিয়র ডিজাইন</span><span>${fmt(interior)}</span></div>
      <div class="breakdown-row"><span>সোলার প্যানেল</span><span>${fmt(solar)}</span></div>
      <div class="breakdown-row"><span>জেনারেটর</span><span>${fmt(gen)}</span></div>
      <div class="breakdown-row"><span>বাউন্ডারি ওয়াল</span><span>${fmt(boundary)}</span></div>
      <div class="breakdown-row"><span>স্পেশাল ফিচারস</span><span>${fmt(specialTotal)}</span></div>
      <div class="breakdown-row"><span>ভ্যাট (${vat}%)</span><span>${fmt(vatAmt)}</span></div>
      <div class="breakdown-row"><span>কন্টিনজেন্সি (${contingency}%)</span><span>${fmt(conAmt)}</span></div>
      <div class="breakdown-row"><span>কন্ট্রাক্টর মার্জিন (${margin}%)</span><span>${fmt(marAmt)}</span></div>
      <div class="breakdown-row"><span>মুদ্রাস্ফীতি (${inflation}%)</span><span>${fmt(infAmt)}</span></div>
      <div class="breakdown-row"><span>সরকারি ও আইনি ফি</span><span>${fmt(govtTotal)}</span></div>
      <div class="breakdown-row total"><span>সর্বমোট নির্মাণ ব্যয়</span><span>${fmt(grandTotal)}</span></div>
      <div style="margin-top:8px; font-size:13px; color:var(--text-muted);">প্রতি বর্গফুট গড় ব্যয়: <strong>${fmt(perSqft)}</strong></div>
    `;
  }

  // Time bar
  const bar = document.getElementById('time-bar');
  if (bar) bar.style.width = Math.min(100, (estMonths / 36) * 100) + '%';

  // Charts
  updateCharts({
    base: baseCost,
    labor: totalLabor,
    extras: extrasTotal,
    special: specialTotal,
    vat: chargesTotal,
    govt: govtTotal
  });

  // Date
  const repDate = document.getElementById('report-date');
  if (repDate) repDate.textContent = 'তারিখ: ' + new Date().toLocaleDateString('bn-BD') + ' | এলাকা: ' + (document.getElementById('district').value || 'নির্বাচিত নয়');

  calcLoan();
  calcSolarROI();
}

// Navigation
const titles = {
  location: ['লোকেশন ও পরিবেশ', 'এলাকা নির্বাচন করুন এবং পরিবেশ ফ্যাক্টর নির্ধারণ করুন'],
  building: ['বিল্ডিং কনফিগারেশন', 'বিল্ডিং ধরণ, মান ও আয়তন নির্ধারণ করুন'],
  materials: ['ম্যাটেরিয়াল টেকঅফ', 'স্বয়ংক্রিয় গণনা করা উপকরণের পরিমাণ ও খরচ'],
  labor: ['শ্রমিক ও যন্ত্রপাতি', 'শ্রমিক মজুরি ও যন্ত্রপাতি ভাড়ার হিসাব'],
  extras: ['অতিরিক্ত সুবিধা ও ডিজাইন', 'সোলার, জেনারেটর, ইন্টেরিয়র ও অন্যান্য'],
  financial: ['আর্থিক ও সরকারি ফি', 'ভ্যাট, কন্টিনজেন্সি, রাজউক ও ঋণ হিসাব'],
  special: ['স্পেশাল ফিচারস', 'বিল্ডিং ধরণ অনুযায়ী বিশেষ সুবিধাসমূহ'],
  report: ['রিপোর্ট ও বিশ্লেষণ', 'সম্পূর্ণ নির্মাণ ব্যয়ের রিপোর্ট ও চার্ট']
};

function showSection(name) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  const sec = document.getElementById('section-' + name);
  if (sec) sec.classList.add('active');
  const navItems = document.querySelectorAll('.nav-item');
  navItems.forEach(n => {
    if (n.getAttribute('onclick') === `showSection('${name}')`) n.classList.add('active');
  });
  const t = titles[name];
  if (t) {
    document.getElementById('page-title').textContent = t[0];
    document.getElementById('page-sub').textContent = t[1];
  }
  recalculate();
}

function saveProject() {
  const data = {
    area: document.getElementById('total-area').value,
    floors: document.getElementById('floors').value,
    district: document.getElementById('district').value,
    btype: document.getElementById('bldg-type').value,
    quality: document.getElementById('quality').value,
    savedAt: new Date().toISOString()
  };
  try {
    const projects = JSON.parse(localStorage.getItem('nirman-projects') || '[]');
    projects.push(data);
    localStorage.setItem('nirman-projects', JSON.stringify(projects));
    alert('প্রজেক্ট সেভ হয়েছে! ✅');
  } catch(e) {
    alert('সেভ করা সম্ভব হয়নি।');
  }
}

function exportCSV() {
  const mats = calcMaterials(+document.getElementById('total-area').value || 2000);
  const rows = [['উপকরণ','পরিমাণ','একক','একক মূল্য (৳)','মোট খরচ (৳)']];
  mats.forEach(m => rows.push([m.name, m.qty, m.unit, m.rate, m.total]));
  const csv = rows.map(r => r.join(',')).join('\n');
  const blob = new Blob(['\ufeff' + csv], {type: 'text/csv;charset=utf-8'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url; a.download = 'nirman-hisab.csv'; a.click();
}

function exportPDF() { alert('PDF রিপোর্ট: প্রিন্ট ডায়ালগ থেকে "Save as PDF" সিলেক্ট করুন।'); window.print(); }
function printReport() { window.print(); }
function shareReport() {
  const url = window.location.href;
  if (navigator.clipboard) navigator.clipboard.writeText(url).then(() => alert('লিংক কপি হয়েছে!'));
  else alert('লিংক: ' + url);
}

// Init
document.addEventListener('DOMContentLoaded', () => {
  renderLaborList();
  renderSpecialFeatures();
  recalculate();
  document.getElementById('report-date') && (document.getElementById('report-date').textContent = 'তারিখ: ' + new Date().toLocaleDateString('bn-BD'));
});
</script>
</body>
</html>
