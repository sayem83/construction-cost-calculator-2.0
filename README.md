<!DOCTYPE html>
<html lang="bn">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=2.5, user-scalable=yes" />
  <title>🏗️ বাংলাদেশ কনস্ট্রাকশন কস্ট ২০২৬ | কাস্টম লেবার সংখ্যা</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js">
  </script>
  <style>
    :root {
      --bg: #020817;
      --card: rgba(10, 20, 40, 0.97);
      --text: #e2e8f0;
      --pri: #3b82f6;
      --gold: #f59e0b;
      --green: #10b981;
      --red: #ef4444;
      --purple: #8b5cf6;
      --border: rgba(148, 163, 184, 0.15);
    }
    body.light-mode {
      --bg: #f8fafc;
      --card: rgba(255, 255, 255, 0.97);
      --text: #0f172a;
      --border: rgba(0, 0, 0, 0.08);
    }
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      background: var(--bg);
      font-family: 'Segoe UI', 'Noto Sans Bengali', system-ui, sans-serif;
      padding: 8px;
      color: var(--text);
      line-height: 1.5;
      min-height: 100vh;
      font-size: 0.88rem;
    }
    .container {
      max-width: 1600px;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
      gap: 12px;
    }
    .card {
      background: var(--card);
      backdrop-filter: blur(20px);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 16px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    }
    h1 {
      font-size: 1.6rem;
      font-weight: 800;
      background: linear-gradient(135deg, #60a5fa, #a78bfa, #f472b6);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }
    h2 {
      font-size: 1.15rem;
      font-weight: 700;
      margin-bottom: 10px;
      padding-left: 10px;
      border-left: 4px solid var(--pri);
    }
    h3 {
      font-size: 0.9rem;
      font-weight: 600;
      margin-bottom: 4px;
      color: #94a3b8;
    }
    .header-flex {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 6px;
    }
    .btn {
      padding: 5px 12px;
      border-radius: 16px;
      font-weight: 600;
      cursor: pointer;
      border: 1px solid var(--border);
      background: rgba(255, 255, 255, 0.05);
      color: var(--text);
      font-size: 0.76rem;
      transition: 0.2s;
    }
    .btn:hover {
      background: rgba(255, 255, 255, 0.12);
    }
    .btn-primary {
      background: #2563eb;
      border: none;
      color: #fff;
      font-weight: 700;
      font-size: 0.9rem;
      padding: 8px 20px;
    }
    .btn-primary:hover {
      background: #1d4ed8;
    }
    .btn-sm {
      padding: 3px 8px;
      font-size: 0.65rem;
    }
    .grid-2 {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
      gap: 8px;
    }
    .grid-3 {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 10px;
    }
    .grid-4 {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(170px, 1fr));
      gap: 8px;
    }
    label {
      font-size: 0.73rem;
      font-weight: 600;
      margin-bottom: 2px;
      color: #94a3b8;
      display: block;
    }
    input,
    select {
      width: 100%;
      padding: 6px 9px;
      background: rgba(0, 0, 0, 0.3);
      border: 1px solid var(--border);
      border-radius: 7px;
      color: var(--text);
      font-size: 0.8rem;
      outline: none;
    }
    body.light-mode input,
    body.light-mode select {
      background: #fff;
      border: 1px solid #cbd5e1;
    }
    input:focus,
    select:focus {
      border-color: #3b82f6;
    }
    .cost-big {
      font-size: 2rem;
      font-weight: 800;
      color: var(--gold);
    }
    .stat-row {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin: 8px 0;
    }
    .stat-box {
      flex: 1;
      min-width: 100px;
      background: rgba(0, 0, 0, 0.25);
      padding: 8px;
      border-radius: 8px;
      text-align: center;
      border: 1px solid var(--border);
      font-size: 0.78rem;
    }
    .list-scroll {
      max-height: 250px;
      overflow-y: auto;
    }
    .list-item {
      display: flex;
      justify-content: space-between;
      padding: 3px 0;
      border-bottom: 1px dashed rgba(148, 163, 184, 0.12);
      font-size: 0.76rem;
      gap: 4px;
    }
    .qty {
      color: #60a5fa;
      font-weight: 600;
      min-width: 50px;
      text-align: right;
      font-size: 0.73rem;
    }
    .total-row {
      background: rgba(59, 130, 246, 0.08);
      padding: 6px 8px;
      border-radius: 6px;
      font-weight: 700;
      margin-top: 3px;
      font-size: 0.8rem;
    }
    .badge {
      display: inline-block;
      padding: 2px 8px;
      border-radius: 12px;
      font-weight: 700;
      font-size: 0.74rem;
      background: rgba(59, 130, 246, 0.12);
      margin: 1px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.76rem;
    }
    th,
    td {
      padding: 6px 8px;
      border-bottom: 1px solid var(--border);
      text-align: left;
    }
    th {
      background: rgba(59, 130, 246, 0.08);
      font-weight: 700;
    }
    .struct-card {
      background: rgba(0, 0, 0, 0.2);
      border: 2px solid var(--border);
      border-radius: 12px;
      padding: 10px;
      text-align: center;
      cursor: pointer;
      transition: 0.3s;
    }
    .struct-card:hover {
      border-color: var(--pri);
      transform: translateY(-2px);
    }
    .struct-card.active {
      border-color: var(--gold);
      background: rgba(245, 158, 11, 0.08);
      box-shadow: 0 0 20px rgba(245, 158, 11, 0.3);
    }
    .struct-icon {
      font-size: 1.8rem;
    }
    .timeline-bar {
      height: 20px;
      background: rgba(0, 0, 0, 0.3);
      border-radius: 10px;
      overflow: hidden;
      margin: 5px 0 10px 0;
    }
    .progress-fill {
      height: 100%;
      border-radius: 10px;
      background: linear-gradient(90deg, #3b82f6, #8b5cf6, #ec4899);
      transition: width 0.5s;
      display: flex;
      align-items: center;
      justify-content: flex-end;
      padding-right: 6px;
      color: #fff;
      font-weight: 700;
      font-size: 0.62rem;
    }
    .phase-grid {
      display: flex;
      flex-wrap: wrap;
      gap: 3px;
    }
    .phase-chip {
      padding: 2px 7px;
      border-radius: 9px;
      font-size: 0.66rem;
      font-weight: 600;
      color: #fff;
    }
    .highlight-box {
      background: rgba(245, 158, 11, 0.06);
      border-left: 3px solid var(--gold);
      padding: 8px 12px;
      margin: 6px 0;
      border-radius: 6px;
      font-size: 0.8rem;
    }
    .labor-row {
      display: flex;
      align-items: center;
      gap: 6px;
      background: rgba(0, 0, 0, 0.2);
      border-radius: 10px;
      padding: 8px 10px;
      margin: 4px 0;
      flex-wrap: wrap;
      border: 1px solid var(--border);
      transition: 0.2s;
    }
    .labor-row:hover {
      border-color: var(--pri);
      box-shadow: 0 0 10px rgba(59, 130, 246, 0.15);
    }
    .labor-name {
      font-weight: 700;
      min-width: 100px;
      font-size: 0.8rem;
    }
    .worker-input {
      width: 50px;
      text-align: center;
      padding: 3px;
    }
    .rate-input {
      width: 65px;
      text-align: center;
      padding: 3px;
    }
    .days-input {
      width: 50px;
      text-align: center;
      padding: 3px;
    }
    .mini-label {
      font-size: 0.6rem;
      color: #94a3b8;
      white-space: nowrap;
    }
    .cost-preview {
      font-weight: 700;
      color: var(--gold);
      font-size: 0.75rem;
      min-width: 80px;
      text-align: right;
    }
    @media (max-width: 768px) {
      h1 {
        font-size: 1.2rem;
      }
      .cost-big {
        font-size: 1.4rem;
      }
      .card {
        padding: 10px 6px;
      }
      .labor-row {
        flex-direction: column;
        align-items: flex-start;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- Header -->
    <div class="card">
      <div class="header-flex">
        <div>
          <h1>🏗️ বাংলাদেশ কনস্ট্রাকশন কস্ট ২০২৬</h1>
          <p style="color:#94a3b8;font-size:0.72rem;">লেবার সংখ্যা কাস্টম • ডেইলি ওয়ার্কার • রিয়েল কস্ট</p>
        </div>
        <div style="display:flex;gap:3px;flex-wrap:wrap;">
          <button class="btn" onclick="toggleTheme()">🌓</button>
          <button class="btn" onclick="copyReport()">📋</button>
          <button class="btn" onclick="exportCSV()">📁</button>
        </div>
      </div>
    </div>

    <!-- Location & Building -->
    <div class="card">
      <h2>📍 লোকেশন ও বিল্ডিং</h2>
      <div class="grid-4">
        <div><label>🗺️ বিভাগ</label><select id="division" onchange="updateDistricts()"></select></div>
        <div><label>🏙️ জেলা</label><select id="district" onchange="updateUpazilas()"></select></div>
        <div><label>🏘️ উপজেলা</label><select id="upazila" onchange="updateLocation()"></select></div>
        <div><label>🏢 সিটি কর্পোরেশন</label><select id="cityCorp" onchange="updateLocation()"><option value="none">নেই</option></select></div>
        <div><label>🏷️ এরিয়া টাইপ</label><select id="areaType" onchange="updateLocation()"><option value="metro_core">মেট্রো কোর</option><option value="metro_suburb">সাব-আরবান</option><option value="city_main" selected>শহর</option><option value="town">উপজেলা সদর</option><option value="rural">গ্রামীণ</option></select></div>
        <div><label>🏗️ বিল্ডিং টাইপ</label><select id="buildingType" onchange="calculateAll()"><option value="residential">🏠 আবাসিক</option><option value="commercial">🏢 বাণিজ্যিক</option><option value="mixed">🏬 মিক্সড</option><option value="hotel">🏨 হোটেল</option><option value="resort">🏖️ রিসোর্ট</option><option value="hospital">🏥 হাসপাতাল</option><option value="educational">🏫 শিক্ষাপ্রতিষ্ঠান</option><option value="industrial">🏭 শিল্প</option></select></div>
        <div><label>📍 মাল্টিপ্লায়ার</label><input type="text" id="locMult" value="0.88" readonly style="font-weight:700;color:var(--gold);"></div>
      </div>
    </div>

    <!-- Project Config -->
    <div class="card">
      <h2>⚙️ প্রজেক্ট কনফিগ</h2>
      <div class="grid-4">
        <div><label>📏 ফ্লোর এরিয়া (sqft)</label><input type="number" id="areaPerFloor" value="2000" min="100" onchange="calculateAll()"></div>
        <div><label>🏬 ফ্লোর সংখ্যা</label><input type="number" id="floors" value="4" min="1" max="60" onchange="calculateAll()"></div>
        <div><label>🛏️ রুম/ইউনিট</label><input type="number" id="rooms" value="20" min="1" onchange="calculateAll()"></div>
        <div><label>⭐ কোয়ালিটি</label><select id="quality" onchange="calculateAll()"><option value="0.70">ইকোনমি</option><option value="1.00" selected>স্ট্যান্ডার্ড</option><option value="1.30">প্রিমিয়াম</option><option value="1.68">লাক্সারি</option><option value="2.15">সুপার লাক্সারি</option></select></div>
        <div><label>📅 কাজের দিন/মাস</label><input type="number" id="workingDays" value="26" min="20" max="30" onchange="calculateAll()"></div>
        <div><label>🛗 লিফট</label><select id="lift" onchange="calculateAll()"><option value="0">নেই</option><option value="1">১টি</option><option value="2">২টি</option><option value="3">৩টি</option><option value="4">৪টি</option></select></div>
        <div><label>🚗 পার্কিং</label><select id="parking" onchange="calculateAll()"><option value="none">নেই</option><option value="open">খোলা</option><option value="basement">বেজমেন্ট</option><option value="multi_level">মাল্টি-লেভেল</option></select></div>
        <div><label>🌳 ল্যান্ডস্কেপ</label><select id="landscape" onchange="calculateAll()"><option value="none">নেই</option><option value="basic">বেসিক</option><option value="medium">মিডিয়াম</option><option value="premium">প্রিমিয়াম</option></select></div>
        <div><label>🏊‍♂️ পুল</label><select id="pool" onchange="calculateAll()"><option value="none">নেই</option><option value="small">ছোট</option><option value="medium">মিডিয়াম</option><option value="large">অলিম্পিক</option></select></div>
        <div><label>📈 ইনফ্লেশন (%)</label><input type="number" id="inflation" value="7.0" step="0.1" onchange="calculateAll()"></div>
        <div><label>🧾 ভ্যাট (%)</label><input type="number" id="vat" value="5.0" step="0.5" onchange="calculateAll()"></div>
        <div><label>🚚 ট্রান্সপোর্ট (%)</label><input type="number" id="transport" value="4.0" onchange="calculateAll()"></div>
        <div><label>🔧 কন্টিনজেন্সি (%)</label><input type="number" id="contingency" value="10" onchange="calculateAll()"></div>
        <div><label>📋 রাজউক ফি (%)</label><input type="number" id="rajukFee" value="3.2" step="0.1" onchange="calculateAll()"></div>
      </div>
      <div style="margin-top:10px;"><button class="btn btn-primary" onclick="calculateAll()">📊 সঠিক হিসাব</button></div>
    </div>

    <!-- Structural -->
    <div class="card">
      <h2>🏗️ স্ট্রাকচারাল</h2>
      <div class="grid-4" style="margin-bottom:10px;">
        <div class="struct-card active" id="struct_rc_frame" onclick="selectStructural('rc_frame')">
          <div class="struct-icon">🏛️</div><div style="font-weight:700;">RCC ফ্রেম</div>
        </div>
        <div class="struct-card" id="struct_load_bearing" onclick="selectStructural('load_bearing')">
          <div class="struct-icon">🧱</div><div style="font-weight:700;">লোড বেয়ারিং</div>
        </div>
        <div class="struct-card" id="struct_steel" onclick="selectStructural('steel')">
          <div class="struct-icon">🏗️</div><div style="font-weight:700;">স্টিল</div>
        </div>
        <div class="struct-card" id="struct_composite" onclick="selectStructural('composite')">
          <div class="struct-icon">🏢</div><div style="font-weight:700;">কম্পোজিট</div>
        </div>
        <input type="hidden" id="structural" value="rc_frame">
      </div>
    </div>

    <!-- LABOR WORKER COUNT CUSTOMIZATION -->
    <div class="card">
      <h2>👷 ডেইলি লেবার সংখ্যা (নিজের ইচ্ছামতো)</h2>
      <div class="highlight-box">
        💡 <strong>প্রতিদিন কতজন লেবার কাজ করবে, কতদিন কাজ করবে, এবং দৈনিক মজুরি - সব নিজের মতো সেট করুন।</strong> 
        উদাহরণ: ৩ জন মিস্ত্রি, ৭ জন হেল্পার প্রতিদিন কাজ করলে যেমন খরচ হবে।
      </div>

      <!-- Header -->
      <div class="labor-row" style="background:rgba(59,130,246,0.15);font-weight:700;border:none;">
        <span class="labor-name">লেবার</span>
        <span style="min-width:60px;text-align:center;">👤 দৈনিক লোক</span>
        <span style="min-width:70px;text-align:center;">💰 দৈনিক রেট (৳)</span>
        <span style="min-width:70px;text-align:center;">📅 মোট দিন</span>
        <span style="min-width:80px;text-align:center;">👷‍♂️ মোট ম্যান-ডে</span>
        <span class="cost-preview">মোট খরচ</span>
      </div>

      <div id="laborWorkersList"></div>

      <div class="total-row" style="margin-top:10px;background:rgba(245,158,11,0.1);">
        <div style="display:flex;justify-content:space-between;flex-wrap:wrap;gap:10px;">
          <span>👥 <strong>দৈনিক মোট লেবার:</strong> <span id="totalDailyWorkers" style="color:var(--gold);">০</span> জন</span>
          <span>👷‍♂️ <strong>মোট ম্যান-ডে:</strong> <span id="totalManDays" style="color:var(--gold);">০</span></span>
          <span>💰 <strong>মোট লেবার খরচ:</strong> <span id="totalLaborCost" style="color:var(--gold);">০ ৳</span></span>
          <span>⏱️ <strong>নির্মাণ সময়:</strong> <span id="totalMonths" style="color:var(--gold);">০ মাস</span></span>
        </div>
      </div>

      <div style="margin-top:8px;display:flex;gap:6px;flex-wrap:wrap;">
        <button class="btn btn-sm" onclick="resetLaborToDefault()">🔄 ডিফল্ট রিসেট</button>
        <button class="btn btn-sm" onclick="quickSetWorkers('low')">👤 কম (২-৫ জন)</button>
        <button class="btn btn-sm" onclick="quickSetWorkers('medium')">👥 মধ্যম (৫-১০)</button>
        <button class="btn btn-sm" onclick="quickSetWorkers('high')">👥👥 বেশি (১০-২০)</button>
      </div>
    </div>

    <!-- Results -->
    <div class="card">
      <h2>💰 মোট খরচ</h2>
      <div class="cost-big" id="grandTotal">০ ৳</div>
      <div id="perSqftInfo" style="margin:3px 0;"></div>
      <div class="stat-row">
        <div class="stat-box"><strong>📊 বাজার</strong><br>২,৮০০ ৳/sqft</div>
        <div class="stat-box"><strong>💰 আপনার</strong><br><span id="yourRate">০</span> ৳/sqft</div>
        <div class="stat-box"><strong>⏰ সময়</strong><br><span id="buildTimeDisplay">০</span> মাস</div>
        <div class="stat-box"><strong>📉 সঞ্চয়</strong><br><span id="savings">০%</span></div>
        <div class="stat-box"><strong>🛏️ প্রতি রুম</strong><br><span id="perRoom">০</span> ৳</div>
      </div>
      <div style="max-width:380px;margin:8px auto;"><canvas id="pieChart"></canvas></div>
      <div id="badgeArea"></div>
    </div>

    <!-- Timeline -->
    <div class="card">
      <h2>⏳ টাইমলাইন</h2>
      <div class="timeline-bar"><div class="progress-fill" id="progressBar" style="width:0%;">0%</div></div>
      <div class="phase-grid" id="phaseContainer"></div>
    </div>

    <!-- Materials -->
    <div class="card">
      <h2>🧱 ম্যাটেরিয়াল</h2>
      <div class="grid-3">
        <div><h3>বেসিক</h3><div class="list-scroll" id="basicMat"></div></div>
        <div><h3>স্টিল</h3><div class="list-scroll" id="steelMat"></div></div>
        <div><h3>ফিনিশিং</h3><div class="list-scroll" id="finishMat"></div></div>
      </div>
      <div class="total-row">মোট ম্যাটেরিয়াল: <span id="totalMatCost">০ ৳</span></div>
    </div>

    <!-- Other Costs -->
    <div class="card">
      <div class="grid-3">
        <div><h2>📊 ফি</h2><div id="profFees"></div></div>
        <div><h2>🛗 লিফট/পার্কিং</h2><div id="liftInfo"></div><div class="total-row"><span id="liftCost">০ ৳</span></div><div id="parkInfo"></div><div class="total-row"><span id="parkCost">০ ৳</span></div></div>
        <div><h2>🌳 ল্যান্ডস্কেপ/পুল</h2><div id="landInfo"></div><div class="total-row"><span id="landCost">০ ৳</span></div><div id="poolInfo"></div><div class="total-row"><span id="poolCost">০ ৳</span></div><div class="total-row">মোট অন্যান্য: <span id="totalOtherCost">০ ৳</span></div></div>
      </div>
    </div>

    <!-- Special -->
    <div class="card" id="specialCard" style="display:none;"><h2>🏨 বিশেষ</h2><div class="grid-3" id="specialCosts"></div></div>
  </div>

  <script>
    (function() {
      const BD = {
        "ঢাকা": { dist: { "ঢাকা": { up: ["ধানমন্ডি", "গুলশান", "মিরপুর", "উত্তরা", "সাভার"], cc: ["ঢাকা উত্তর", "ঢাকা দক্ষিণ"] },
            "গাজীপুর": { up: ["সদর", "কালিয়াকৈর"], cc: ["গাজীপুর"] }, "নারায়ণগঞ্জ": { up: ["সদর", "ফতুল্লা", "রূপগঞ্জ"],
            cc: ["নারায়ণগঞ্জ"] }, "টাঙ্গাইল": { up: ["সদর", "মধুপুর"], cc: [] }, "ফরিদপুর": { up: ["সদর", "ভাঙ্গা"],
            cc: [] }, "কিশোরগঞ্জ": { up: ["সদর", "ভৈরব"], cc: [] } } },
        "চট্টগ্রাম": { dist: { "চট্টগ্রাম": { up: ["সদর", "আনোয়ারা", "পটিয়া"], cc: ["চট্টগ্রাম"] }, "কক্সবাজার": { up: ["সদর",
              "চকরিয়া", "টেকনাফ"], cc: [] }, "কুমিল্লা": { up: ["সদর", "চান্দিনা"], cc: ["কুমিল্লা"] }, "ফেনী": { up: ["সদর"],
            cc: [] }, "নোয়াখালী": { up: ["সদর", "বেগমগঞ্জ"], cc: [] }, "ব্রাহ্মণবাড়িয়া": { up: ["সদর", "আখাউড়a"],
          cc: [] } } },
        "রাজশাহী": { dist: { "রাজশাহী": { up: ["সদর", "বাঘা"], cc: ["রাজশাহী"] }, "নওগাঁ": { up: ["সদর"], cc: [] },
            "পাবনা": { up: ["সদর", "ঈশ্বরদী"], cc: [] }, "বগুড়া": { up: ["সদর", "শেরপুর"], cc: [] } } },
        "খুলনা": { dist: { "খুলনা": { up: ["সদর", "ডুমুরিয়া"], cc: ["খুলনা"] }, "বাগেরহাট": { up: ["সদর", "মোংলা"],
            cc: [] }, "যশোর": { up: ["সদর", "অভয়নগর"], cc: [] }, "কুষ্টিয়া": { up: ["সদর", "ভেড়ামারা"], cc: [] } } },
        "বরিশাল": { dist: { "বরিশাল": { up: ["সদর", "বাকেরগঞ্জ"], cc: ["বরিশাল"] }, "ভোলা": { up: ["সদর"], cc: [] } } },
        "সিলেট": { dist: { "সিলেট": { up: ["সদর", "গোলাপগঞ্জ"], cc: ["সিলেট"] }, "মৌলভীবাজার": { up: ["সদর", "শ্রীমঙ্গল"],
            cc: [] }, "হবিগঞ্জ": { up: ["সদর"], cc: [] } } },
        "রংপুর": { dist: { "রংপুর": { up: ["সদর", "পীরগঞ্জ"], cc: ["রংপুর"] }, "দিনাজপুর": { up: ["সদর"], cc: [] },
            "নীলফামারী": { up: ["সদর", "সৈয়দপুর"], cc: [] } } },
        "ময়মনসিংহ": { dist: { "ময়মনসিংহ": { up: ["সদর", "ভালুকা", "ত্রিশাল"], cc: ["ময়মনসিংহ"] }, "জামালপুর": { up: ["সদর"],
            cc: [] }, "নেত্রকোণা": { up: ["সদর", "কেন্দুয়া"], cc: [] } } }
      };

      const $ = (id) => document.getElementById(id);
      const fmt = (n) => Math.round(n).toLocaleString('en-IN') + ' ৳';
      const fmtQ = (n, u) => Math.round(n).toLocaleString('en-IN') + ' ' + u;
      const v = (id) => { const el = $(id); return el ? (parseFloat(el.value) || 0) : 0; };
      const vs = (id) => { const el = $(id); return el ? el.value : ''; };

      const BASIC = [{ n: "ইট", q: 5.8, r: 17, u: "পিস" }, { n: "বালি", q: 0.033, r: 2450, u: "cft" }, { n: "সিমেন্ট", q: 0.082,
        r: 740, u: "বস্তা" }, { n: "পাথর", q: 0.031, r: 3350, u: "cft" }, { n: "কংক্রিট", q: 0.58, r: 138, u: "cft" },
      { n: "শাটারিং", q: 0.98, r: 165, u: "sqft" }, { n: "ওয়াটারপ্রুফ", q: 0.036, r: 440, u: "sqft" }];
      const STEEL = [{ n: "রড 10mm", q: 1.15, r: 132, u: "kg" }, { n: "রড 12mm", q: 1.65, r: 138, u: "kg" }, { n: "রড 16mm",
        q: 0.98, r: 140, u: "kg" }, { n: "রড 20mm", q: 0.48, r: 145, u: "kg" }, { n: "রড 25mm", q: 0.20, r: 150,
      u: "kg" }, { n: "গ্রিল", q: 0.28, r: 235, u: "kg" }];
      const FINISH = [{ n: "টাইলস", q: 1.08, r: 108, u: "sqft" }, { n: "মার্বেল", q: 0.26, r: 540, u: "sqft" }, { n: "পেইন্ট",
        q: 0.046, r: 390, u: "লিটার" }, { n: "কাঠের ফ্লোর", q: 0.19, r: 370, u: "sqft" }, { n: "জিপসাম", q: 0.25, r: 198,
        u: "sqft" }, { n: "ইলেকট্রিক", q: 1.15, r: 56, u: "মি" }, { n: "সুইচ", q: 0.058, r: 3350, u: "সেট" },
      { n: "লাইট", q: 0.026, r: 1850, u: "পিস" }, { n: "পিভিসি", q: 0.31, r: 100, u: "ফিট" }, { n: "স্যানিটারি", q: 0.052,
        r: 9300, u: "সেট" }, { n: "কল", q: 0.038, r: 1420, u: "পিস" }, { n: "অন্যান্য", q: 0.088, r: 590, u: "lump" }];

      const DEFAULT_LABOR = [
        { name: "হেড মিস্ত্রি", workers: 3, rate: 1500, days: 120 },
        { name: "রড বাইন্ডার", workers: 4, rate: 1100, days: 80 },
        { name: "কার্পেন্টার", workers: 3, rate: 1300, days: 90 },
        { name: "ইলেকট্রিশিয়ান", workers: 2, rate: 1250, days: 45 },
        { name: "প্লাম্বার", workers: 2, rate: 1100, days: 40 },
        { name: "পেইন্টার", workers: 4, rate: 1000, days: 50 },
        { name: "টাইলস মিস্ত্রি", workers: 3, rate: 1200, days: 55 },
        { name: "হেল্পার", workers: 7, rate: 850, days: 150 },
        { name: "সুপারভাইজার", workers: 1, rate: 1800, days: 130 }
      ];

      let laborData = JSON.parse(JSON.stringify(DEFAULT_LABOR));
      const PHASES = [{ n: "ফাউন্ডেশন", p: 14, c: "#3b82f6" }, { n: "কলাম/বিম", p: 16, c: "#6366f1" }, { n: "স্ল্যাব", p: 12,
        c: "#8b5cf6" }, { n: "ওয়াল", p: 17, c: "#10b981" }, { n: "ইলেক/প্লাম্ব", p: 13, c: "#f59e0b" }, { n: "টাইলস",
        p: 14, c: "#ef4444" }, { n: "পেইন্ট", p: 14, c: "#ec4899" }];
      let chart = null;

      function getLocMult() {
        const cc = vs('cityCorp'),
          at = vs('areaType');
        let b = 1.0;
        if (cc.includes('ঢাকা') && at === 'metro_core') b = 1.38;
        else if (cc.includes('চট্টগ্রাম') && at === 'metro_core') b = 1.28;
        else if (cc.includes('ঢাকা')) b = 1.25;
        else if (cc.includes('চট্টগ্রাম')) b = 1.18;
        else if (cc !== 'none' && cc !== '') b = 1.10;
        else if (at === 'metro_suburb') b = 0.95;
        else if (at === 'city_main') b = 0.88;
        else if (at === 'town') b = 0.68;
        else if (at === 'rural') b = 0.55;
        return b;
      }

      function updateLocation() { const el = $('locMult'); if (el) el.value = getLocMult().toFixed(2);
        calculateAll();
        saveState(); }

      function selectStructural(type) { $('structural').value = type;
        document.querySelectorAll('.struct-card').forEach(c => c.classList.remove('active')); const card = $('struct_' +
          type); if (card) card.classList.add('active');
        calculateAll();
        saveState(); }

      function buildLaborUI() {
        const container = $('laborWorkersList');
        if (!container) return;
        let html = '';
        laborData.forEach((l, i) => {
          html += `
            <div class="labor-row">
              <span class="labor-name">👤 ${l.name}</span>
              <div style="text-align:center;"><span class="mini-label">লোক/দিন</span><br><input type="number" class="worker-input" id="lw_${i}" value="${l.workers}" min="0" max="100" onchange="updateLabor(${i})"></div>
              <div style="text-align:center;"><span class="mini-label">রেট (৳)</span><br><input type="number" class="rate-input" id="lr_${i}" value="${l.rate}" min="300" max="5000" step="50" onchange="updateLabor(${i})"></div>
              <div style="text-align:center;"><span class="mini-label">দিন</span><br><input type="number" class="days-input" id="ld_${i}" value="${l.days}" min="1" max="400" onchange="updateLabor(${i})"></div>
              <div style="text-align:center;"><span class="mini-label">ম্যান-ডে</span><br><span id="lmd_${i}" style="font-weight:700;">${l.workers * l.days}</span></div>
              <span class="cost-preview" id="lcost_${i}">${fmt(l.workers * l.days * l.rate)}</span>
            </div>`;
        });
        container.innerHTML = html;
      }

      window.updateLabor = function(i) {
        const wEl = $('lw_' + i),
          rEl = $('lr_' + i),
          dEl = $('ld_' + i);
        if (wEl) laborData[i].workers = parseInt(wEl.value) || 0;
        if (rEl) laborData[i].rate = parseInt(rEl.value) || 0;
        if (dEl) laborData[i].days = parseInt(dEl.value) || 0;
        const md = laborData[i].workers * laborData[i].days;
        const cost = md * laborData[i].rate;
        const mdEl = $('lmd_' + i);
        if (mdEl) mdEl.textContent = md;
        const cEl = $('lcost_' + i);
        if (cEl) cEl.textContent = fmt(cost);
        calculateAll();
        saveState();
      };

      window.resetLaborToDefault = function() { laborData = JSON.parse(JSON.stringify(DEFAULT_LABOR));
        buildLaborUI();
        calculateAll();
        saveState(); };

      window.quickSetWorkers = function(level) {
        const settings = { low: [2, 2, 2, 1, 2, 2, 2, 4, 1], medium: [5, 6, 5, 3, 3, 5, 4, 8, 1], high: [10, 12, 8, 5, 5,
            8, 6, 15, 1] };
        const w = settings[level] || settings.medium;
        laborData.forEach((l, i) => { l.workers = w[i] || l.workers; });
        buildLaborUI();
        calculateAll();
        saveState();
      };

      function popDivs() { const s = $('division'); if (!s) return;
        s.innerHTML = '<option value="">বিভাগ</option>';
        Object.keys(BD).forEach(d => s.innerHTML += `<option value="${d}">${d}</option>`); }

      function updateDistricts() { const div = vs('division'),
          ds = $('district'); if (!ds) return;
        ds.innerHTML = '<option value="">জেলা</option>'; const us = $('upazila'); if (us) us.innerHTML =
          '<option value="">উপজেলা</option>'; if (div && BD[div]) Object.keys(BD[div].dist).forEach(d => ds.innerHTML +=
          `<option value="${d}">${d}</option>`);
        updateLocation(); }

      function updateUpazilas() { const div = vs('division'),
          dist = vs('district'),
          us = $('upazila'),
          cs = $('cityCorp'); if (!us) return;
        us.innerHTML = '<option value="">উপজেলা</option>'; if (cs) cs.innerHTML = '<option value="none">নেই</option>'; if (
          div && dist && BD[div]?.dist[dist]) { const data = BD[div].dist[dist];
          data.up.forEach(u => us.innerHTML += `<option value="${u}">${u}</option>`); if (cs && data.cc.length) data.cc
            .forEach(c => cs.innerHTML += `<option value="${c}">${c}</option>`); }
        updateLocation(); }

      function calcMat(arr, elId, area, qf, lf, inf, tm, sm) { let h = '',
          t = 0;
        arr.forEach(m => { const qty = m.q * area * tm * sm,
            cost = qty * m.r * qf * lf * inf;
          t += cost;
          h +=
            `<div class="list-item"><span>${m.n}</span><span class="qty">${fmtQ(qty,m.u)}</span><span>${fmt(cost)}</span></div>`; });
        const el = $(elId); if (el) el.innerHTML = h; return t; }

      function calculateAll() {
        const areaPerFloor = v('areaPerFloor') || 2000,
          floors = v('floors') || 2,
          area = areaPerFloor * floors,
          rooms = v('rooms') || 1;
        const qf = parseFloat(vs('quality')) || 1.0,
          lf = getLocMult(),
          inf = 1 + (v('inflation') || 5) / 100,
          bt = vs('buildingType') || 'residential',
          st = vs('structural') || 'rc_frame';
        const tm = { residential: 1.0, commercial: 1.15, mixed: 1.12, hotel: 1.45, resort: 1.55, hospital: 1.50,
          educational: 1.20, industrial: 1.25 } [bt] || 1.0;
        const sm = { rc_frame: 1.0, load_bearing: 0.82, steel: 1.22, composite: 1.32 } [st] || 1.0;
        const lme = $('locMult'); if (lme) lme.value = lf.toFixed(2);

        const bm = calcMat(BASIC, 'basicMat', area, qf, lf, inf, tm, sm),
          smt = calcMat(STEEL, 'steelMat', area, qf, lf, inf, tm, sm),
          fm = calcMat(FINISH, 'finishMat', area, qf, lf, inf, tm, sm);
        const totalMat = bm + smt + fm;
        const tme = $('totalMatCost'); if (tme) tme.textContent = fmt(totalMat);

        // Labor calculation based on workers × days × rate
        let totalLab = 0,
          totalMD = 0,
          totalDaily = 0;
        laborData.forEach((l, i) => {
          const md = l.workers * l.days;
          const cost = md * l.rate * qf * lf * inf;
          totalLab += cost;
          totalMD += md;
          totalDaily += l.workers;
          const mdEl = $('lmd_' + i); if (mdEl) mdEl.textContent = md;
          const cEl = $('lcost_' + i); if (cEl) cEl.textContent = fmt(cost);
        });

        const tlce = $('totalLaborCost'); if (tlce) tlce.textContent = fmt(totalLab);
        const tmd = $('totalManDays'); if (tmd) tmd.textContent = Math.round(totalMD).toLocaleString('en-IN');
        const tdw = $('totalDailyWorkers'); if (tdw) tdw.textContent = totalDaily;
        const workingDays = v('workingDays') || 26;
        const months = Math.max(4, Math.ceil(Math.max(...laborData.map(l => l.days)) / workingDays));
        const tmEl = $('totalMonths'); if (tmEl) tmEl.textContent = months + ' মাস';

        const base = totalMat + totalLab;
        const arch = base * 0.06,
          sEng = base * 0.05,
          rajuk = base * (v('rajukFee') / 100),
          util = base * 0.045,
          soil = 55000 * floors * lf,
          design = base * 0.032,
          contractor = base * 0.13,
          contingency = base * (v('contingency') / 100),
          transport = base * (v('transport') / 100),
          vatAmt = base * (v('vat') / 100),
          insurance = base * 0.02,
          mob = base * 0.028;
        const liftCount = parseInt(vs('lift')) || 0;
        let liftCost = 0,
          liftHtml = '';
        if (liftCount > 0) { liftCost = liftCount * 3500000 * qf * lf;
          liftHtml = liftCount + 'টি লিফট'; } else liftHtml = 'নেই';
        const lie = $('liftInfo'); if (lie) lie.innerHTML = liftHtml;
        const lce = $('liftCost'); if (lce) lce.textContent = fmt(liftCost);
        const park = vs('parking');
        let pCost = 0,
          pHtml = '';
        if (park === 'open') { pCost = area * 100 * lf;
          pHtml = 'খোলা'; } else if (park === 'basement') { pCost = area * 450 * lf * qf;
          pHtml = 'বেজমেন্ট'; } else if (park === 'multi_level') { pCost = area * 800 * lf * qf;
          pHtml = 'মাল্টি'; } else pHtml = 'নেই';
        const pie = $('parkInfo'); if (pie) pie.innerHTML = pHtml;
        const pce = $('parkCost'); if (pce) pce.textContent = fmt(pCost);
        const land = vs('landscape');
        let lCost = 0,
          lHtml = '';
        if (land === 'basic') { lCost = area * 35;
          lHtml = 'বেসিক'; } else if (land === 'medium') { lCost = area * 85;
          lHtml = 'মিডিয়াম'; } else if (land === 'premium') { lCost = area * 200;
          lHtml = 'প্রিমিয়াম'; } else lHtml = 'নেই';
        const lie2 = $('landInfo'); if (lie2) lie2.innerHTML = lHtml;
        const lce2 = $('landCost'); if (lce2) lce2.textContent = fmt(lCost);
        const pool = vs('pool');
        let poolCost = 0,
          poolHtml = '';
        if (pool === 'small') { poolCost = 800000 * lf;
          poolHtml = 'ছোট'; } else if (pool === 'medium') { poolCost = 1800000 * lf;
          poolHtml = 'মিডিয়াম'; } else if (pool === 'large') { poolCost = 3500000 * lf;
          poolHtml = 'অলিম্পিক'; } else poolHtml = 'নেই';
        const ppe = $('poolInfo'); if (ppe) ppe.innerHTML = poolHtml;
        const ppc = $('poolCost'); if (ppc) ppc.textContent = fmt(poolCost);
        const otherTotal = arch + sEng + rajuk + util + soil + design + contractor + contingency + transport + vatAmt +
          insurance + mob + liftCost + pCost + lCost + poolCost;
        const grand = base + otherTotal,
          cpsf = grand / area;
        const gte = $('grandTotal'); if (gte) gte.textContent = fmt(grand);
        const psi = $('perSqftInfo'); if (psi) psi.innerHTML =
          `প্রতি sqft: <strong>${Math.round(cpsf).toLocaleString('en-IN')} ৳</strong> | এরিয়া: ${area.toLocaleString('en-IN')} sqft`;
        const yre = $('yourRate'); if (yre) yre.textContent = Math.round(cpsf).toLocaleString('en-IN');
        const bte = $('buildTimeDisplay'); if (bte) bte.textContent = months;
        const pre = $('perRoom'); if (pre) pre.textContent = fmt(grand / Math.max(1, rooms));
        const sv = ((2800 - cpsf) / 2800 * 100).toFixed(1);
        const se = $('savings'); if (se) { se.textContent = sv + '%';
          se.style.color = parseFloat(sv) >= 0 ? '#10b981' : '#ef4444'; }
        const bae = $('badgeArea'); if (bae) bae.innerHTML =
          `<span class="badge">⭐ ${cpsf>4000?'সুপার লাক্সারি':cpsf>3200?'লাক্সারি':cpsf>2500?'প্রিমিয়াম':'স্ট্যান্ডার্ড'}</span>`;
        const pfe = $('profFees'); if (pfe) pfe.innerHTML = `
          <div class="list-item"><span>স্থপতি</span><span>${fmt(arch)}</span></div><div class="list-item"><span>ইঞ্জিনিয়ার</span><span>${fmt(sEng)}</span></div><div class="list-item"><span>রাজউক</span><span>${fmt(rajuk)}</span></div><div class="list-item"><span>ইউটিলিটি</span><span>${fmt(util)}</span></div><div class="list-item"><span>সয়েল</span><span>${fmt(soil)}</span></div><div class="list-item"><span>ডিজাইন</span><span>${fmt(design)}</span></div><div class="list-item"><span>কন্ট্রাক্টর</span><span>${fmt(contractor)}</span></div><div class="list-item"><span>কন্টিনজেন্সি</span><span>${fmt(contingency)}</span></div><div class="list-item"><span>পরিবহন</span><span>${fmt(transport)}</span></div><div class="list-item"><span>ভ্যাট</span><span>${fmt(vatAmt)}</span></div><div class="list-item"><span>ইনস্যুরেন্স</span><span>${fmt(insurance)}</span></div><div class="list-item"><span>মোবিলাইজেশন</span><span>${fmt(mob)}</span></div>`;
        const toce = $('totalOtherCost'); if (toce) toce.textContent = fmt(otherTotal);
        const sc = $('specialCard'),
          scd = $('specialCosts'); if (sc && scd && ['hotel', 'resort', 'hospital'].includes(bt)) { sc.style.display =
            'block';
          const kc = rooms * 180000 * qf * lf,
            fc = rooms * 250000 * qf * lf,
            hc = area * 120 * qf,
            sec = area * 25,
            lc2 = rooms * 40000,
            spc = bt === 'resort' ? area * 80 : 0;
          scd.innerHTML =
            `<div><h3>🍽️ কিচেন</h3><div class="total-row">${fmt(kc)}</div></div><div><h3>🛏️ ফার্নিচার</h3><div class="total-row">${fmt(fc)}</div></div><div><h3>❄️ HVAC</h3><div class="total-row">${fmt(hc)}</div></div><div><h3>🔒 সিকিউরিটি</h3><div class="total-row">${fmt(sec)}</div></div><div><h3>🧺 লন্ড্রি</h3><div class="total-row">${fmt(lc2)}</div></div>${spc>0?`<div><h3>💆‍♂️ স্পা</h3><div class="total-row">${fmt(spc)}</div></div>`:''}`; } else if (sc) sc.style
          .display = 'none';
        const ph = $('phaseContainer'); if (ph) { let h = '';
          PHASES.forEach(p => { const m = Math.max(0.5, months * p.p / 100);
            h += `<span class="phase-chip" style="background:${p.c};">${p.n}: ${m.toFixed(1)}মা</span>`; });
          ph.innerHTML = h; }
        const pb = $('progressBar'); if (pb) { pb.style.width = '100%';
          pb.textContent = months + ' মাস'; }
        const ctx = $('pieChart')?.getContext('2d'); if (ctx) { if (chart) chart.destroy();
          chart = new Chart(ctx, { type: 'doughnut', data: { labels: ['ম্যাটেরিয়াল', 'শ্রমিক', 'অন্যান্য'],
              datasets: [{ data: [totalMat, totalLab, otherTotal], backgroundColor: ['#3b82f6', '#10b981',
                  '#f59e0b'
                ], borderWidth: 2 }] }, options: { responsive: true,
              plugins: { legend: { labels: { color: '#e2e8f0' } } } } }); }
        saveState();
      }

      function saveState() { const d = {}; ['division', 'district', 'upazila', 'cityCorp', 'areaType', 'buildingType',
          'areaPerFloor', 'floors', 'rooms', 'quality', 'structural', 'lift', 'parking', 'landscape', 'pool', 'inflation',
          'vat', 'transport', 'contingency', 'rajukFee', 'workingDays'
        ].forEach(id => { const el = $(id); if (el) d[id] = el.value; });
        d.laborData = JSON.stringify(laborData); try { localStorage.setItem('bd_calc_workers_v10', JSON.stringify(
        d)); } catch (e) {} }

      function loadState() { try { const d = JSON.parse(localStorage.getItem('bd_calc_workers_v10')); if (d) { Object.keys(
            d).forEach(id => { if (id !== 'laborData') { const el = $(id); if (el && d[id] !== undefined) el.value =
                d[id]; } }); if (d.laborData) { laborData = JSON.parse(d.laborData); } if (d.division) { updateDistricts(); if (
              d.district) updateUpazilas(); } if (d.structural) selectStructural(d.structural); } } catch (e) {} }

      window.toggleTheme = function() { document.body.classList.toggle('light-mode'); try { localStorage.setItem(
          'bd_theme_w', document.body.classList.contains('light-mode') ? 'light' : 'dark'); } catch (e) {} };
      if (localStorage.getItem('bd_theme_w') === 'light') document.body.classList.add('light-mode');
      window.copyReport = () => navigator.clipboard?.writeText('মোট খরচ: ' + ($('grandTotal')?.textContent || '')).then(() =>
        alert('✅'));
      window.exportCSV = function() { let csv = 'Type,Item,Quantity,Rate,Cost\n';
        document.querySelectorAll('.list-item').forEach(r => { const c = r.querySelectorAll('span'); if (c.length >= 2) csv +=
            `"Material","${c[0].textContent}","${c[1]?.textContent||''}","","${c[2]?.textContent||c[1]?.textContent||''}"\n`; });
        laborData.forEach(l => { csv +=
            `"Labor","${l.name}","${l.workers} workers × ${l.days} days","${l.rate} ৳","${Math.round(l.workers*l.days*l.rate).toLocaleString('en-IN')} ৳"\n`; });
        const b = new Blob(['\uFEFF' + csv], { type: 'text/csv' });
        const a = document.createElement('a');
        a.href = URL.createObjectURL(b);
        a.download = 'bd_construction_workers.csv';
        a.click(); };

      popDivs();
      buildLaborUI();
      window.updateDistricts = updateDistricts;
      window.updateUpazilas = updateUpazilas;
      window.updateLocation = updateLocation;
      window.selectStructural = selectStructural;
      window.calculateAll = calculateAll;
      window.addEventListener('DOMContentLoaded', () => { loadState();
        buildLaborUI();
        updateLocation();
        calculateAll(); });
    })();
  </script>
</body>
</html>
