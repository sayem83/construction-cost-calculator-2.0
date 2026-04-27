<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>🏗️ Bangladesh Construction Cost Calculator (2025)</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <!-- Chart.js CDN for doughnut chart visualization -->
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    /* 🌓 CSS Variables for Dark Cosmic Theme */
    :root {
      --bg-color: #0f172a;
      --card-bg: rgba(255,255,255,0.05);
      --primary: #00C6FF;
      --accent: #FF4D4D;
      --text: #E5E7EB;
      --muted: #94A3B8;
      --success: #00FF99;
      --warn: #FF4D4D;
    }
    /* Light theme overrides */
    html[data-theme='light'] {
      --bg-color: #FFFFFF;
      --card-bg: #F0F0F0;
      --text: #000000;
      --muted: #777777;
      --primary: #0073FF;
      --accent: #FF4D4D;
      --success: #00CC66;
      --warn: #CC0000;
    }
    body {
      margin: 0; padding: 0;
      background: var(--bg-color);
      color: var(--text);
      font-family: Arial, sans-serif;
      line-height: 1.4;
    }
    .container {
      max-width: 1200px; margin: auto; padding: 20px;
    }
    .header { text-align: center; margin-bottom: 20px; }
    h1 { color: var(--text); margin-bottom: 5px; }
    /* Cards and Layout */
    .card {
      background: var(--card-bg);
      padding: 20px;
      margin-bottom: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.5);
    }
    .grid { display: grid; grid-gap: 20px; }
    /* Responsive */
    @media (max-width: 600px) {
      .grid { grid-template-columns: 1fr !important; }
    }
    input, select {
      width: 100%;
      padding: 10px; margin-top: 5px;
      border-radius: 5px; border: 1px solid #34495e;
      font-size: 1rem;
      background: #1f2937; color: var(--text);
    }
    html[data-theme='light'] input, html[data-theme='light'] select {
      background: #ffffff; color: #000000; border: 1px solid #ccc;
    }
    button {
      margin-top: 15px; padding: 12px 20px;
      border: none; border-radius: 5px;
      cursor: pointer; font-weight: bold;
    }
    button.primary { background: var(--primary); color: #000; }
    button.accent  { background: var(--accent);  color: #fff; }
    button.toggle  { background: transparent;    color: var(--text); border: 1px solid var(--text); }
    .small-btn { padding: 8px 12px; font-size: 0.9rem; background: var(--primary); color: #000; border: none; margin: 0 5px; }
    .results { display: none; }
    .show { display: block; animation: fadeIn 0.3s ease; }
    @keyframes fadeIn { from { opacity:0; transform: translateY(10px);} to { opacity:1; transform: translateY(0);} }
    .market-table { width: 100%; border-collapse: collapse; }
    .market-table td { padding: 5px 10px; }
    .green { color: var(--success); }
    .red   { color: var(--warn); }
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <h1>🏗️ Bangladesh Construction Cost Calculator (2025)</h1>
      <div>
        <button class="toggle small-btn" onclick="toggleTheme()" aria-label="Toggle Theme">🌓 Toggle Theme</button>
        <button class="small-btn" onclick="copySummary()">📋 Copy Summary</button>
      </div>
    </div>

    <!-- Input Section -->
    <div class="card">
      <h2>Input Parameters</h2>
      <div class="grid" style="grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));">
        <div>
          <label>📏 Building Area (sqft)</label>
          <input type="number" id="area" min="100" step="10" value="1000" aria-label="Building Area">
        </div>
        <div>
          <label>🏢 Floors</label>
          <input type="number" id="floors" min="1" max="15" value="3" aria-label="Number of Floors">
        </div>
        <div>
          <label>⭐ Quality Multiplier</label>
          <select id="quality" aria-label="Quality">
            <option value="0.82">Normal (0.82× mat, 0.88× labor)</option>
            <option value="1.00" selected>Good (1.00×)</option>
            <option value="1.30">Premium (1.30× mat, 1.20× labor)</option>
          </select>
        </div>
        <div>
          <label>📍 Location Multiplier</label>
          <select id="location" aria-label="Location Multiplier">
            <option value="1.10">Dhaka City (+10%)</option>
            <option value="0.95" selected>Chittagong City (-5%)</option>
            <option value="0.85">Dhaka Suburb (-15%)</option>
            <option value="0.78">Divisional City (-22%)</option>
            <option value="0.68">Chittagong Suburb (-32%)</option>
            <option value="0.65">Rural (-35%)</option>
          </select>
        </div>
        <div>
          <label>📈 Inflation Adjustment</label>
          <input type="range" id="inflation" min="0" max="40" value="10" aria-label="Inflation Percentage">
          <div style="display:flex;justify-content:space-between;font-size:0.9rem;">
            <span>0%</span><span id="inflationVal">10%</span><span>40%</span>
          </div>
        </div>
        <div>
          <label>📦 VAT/Tax (%)</label>
          <input type="number" id="vat" min="0" max="50" step="0.5" value="0" aria-label="VAT/Tax Percentage">
        </div>
        <div>
          <label>🚚 Transport (%)</label>
          <input type="number" id="transport" min="0" max="50" step="0.5" value="0" aria-label="Transport Percentage">
        </div>
        <div style="grid-column: 1 / -1;">
          <button class="primary" onclick="calculate()" aria-label="Calculate Cost">🚀 Calculate</button>
        </div>
      </div>
    </div>

    <!-- Live Market Section -->
    <div class="card">
      <h2>📡 Live Market Rates</h2>
      <table class="market-table">
        <tr>
          <td>Cement (৳/bag)</td>
          <td id="market-cement">530</td>
          <td id="cementChange" class="green">+0%</td>
        </tr>
        <tr>
          <td>Steel Rod (৳/ton)</td>
          <td id="market-rod">90000</td>
          <td id="rodChange" class="green">+0%</td>
        </tr>
      </table>
      <div>
        <button class="small-btn" onclick="refreshMarket()" aria-label="Refresh Market Rates">🔄 Refresh Now</button>
        <span id="market-timestamp" style="float:right;font-size:0.9rem;"></span>
      </div>
    </div>

    <!-- Results Section -->
    <div class="card results" id="results">
      <h2 id="summaryTitle">🏠 Building Cost Summary</h2>
      <div style="font-size:2rem; margin:10px 0;">
        Total Cost: <strong id="totalCost">0 ৳</strong>
      </div>
      <div>
        <canvas id="costChart" width="400" height="250"></canvas>
      </div>
      <div style="display:flex; gap:20px; margin-top:20px;">
        <div style="background: rgba(255,255,255,0.1); padding:10px; border-radius:8px; flex:1;">
          Market Avg: <br><span id="marketAvg" style="font-size:1.5rem;">2600</span> ৳/sqft
        </div>
        <div style="background: rgba(255,255,255,0.1); padding:10px; border-radius:8px; flex:1;">
          Your Cost: <br><span id="yourCost" style="font-size:1.5rem;">0</span> ৳/sqft
        </div>
        <div style="background: rgba(255,255,255,0.1); padding:10px; border-radius:8px; flex:1;">
          Savings: <br><span id="savings" style="font-size:1.5rem;">0%</span>
        </div>
      </div>
      <div id="qualityBadge" style="margin-top:15px;"></div>
      <div style="margin-top:20px;">
        <button class="small-btn" onclick="print()" aria-label="Print Report">🖨️ Print</button>
        <button class="small-btn" onclick="scrollToDetails()" aria-label="Scroll to Details">📊 Details</button>
        <button class="small-btn" onclick="exportCSV()" aria-label="Export CSV">📁 Export CSV</button>
      </div>
    </div>

    <!-- Breakdown Section -->
    <div class="card" id="details">
      <h2>Detailed Breakdown</h2>
      <div class="grid" style="grid-template-columns: 1fr 1fr 1fr; gap: 20px;">
        <div class="card">
          <h3>🔨 Material Costs</h3>
          <div id="materialsList"></div>
          <div style="font-weight:bold; margin-top:10px;">
            Total Materials: <span id="totalMaterials">0 ৳</span>
          </div>
        </div>
        <div class="card">
          <h3>👷 Labor Costs</h3>
          <div id="laborList"></div>
          <div style="font-weight:bold; margin-top:10px;">
            Total Labor: <span id="totalLabor">0 ৳</span>
          </div>
          <div style="margin-top:10px;">
            Total Man-Days: <span id="totalManDays">0</span>
          </div>
        </div>
        <div class="card">
          <h3>📊 Additional Costs</h3>
          <div id="finalCosts"></div>
        </div>
      </div>
    </div>
  </div>

  <script>
    // ====== Data Model ======
    const defaultMaterials = [
      { name:'Bricks',             qty:5.2, rate:16 },
      { name:'Sand',               qty:0.022, rate:2200 },
      { name:'Cement (OPC)',       qty:0.062, rate:680 },
      { name:'Stone Chips',        qty:0.020, rate:2900 },
      { name:'Steel Rod 12mm',     qty:1.2,  rate:125 },
      { name:'Steel Rod 16mm',     qty:0.8,  rate:125 },
      { name:'Steel Rod 20mm',     qty:0.2,  rate:125 },
      { name:'Shuttering Plywood', qty:0.8,  rate:145 },
      { name:'Concrete (M15)',     qty:0.0,  rate:0 },
      { name:'Ceramic Tile',       qty:0.92, rate:92 },
      { name:'Marble',             qty:0.15, rate:450 },
      { name:'Paint',              qty:0.028,rate:320 },
      { name:'Wood Flooring',      qty:0.10, rate:300 },
      { name:'Electrical Wire',    qty:0.75, rate:45 },
      { name:'Switches/Sockets',   qty:0.035,rate:2850 },
      { name:'Lighting Fixtures',  qty:0.01, rate:1500 },
      { name:'PVC Pipe',           qty:0.15, rate:85 },
      { name:'Sanitary (Toilet)',  qty:0.032,rate:8200 },
      { name:'Faucets/Taps',       qty:0.02, rate:1200 },
      { name:'Gypsum Board',       qty:0.12, rate:165 },
      { name:'AC Sheet',           qty:0.08, rate:125 },
      { name:'Misc Hardware',      qty:0.05, rate:500 }
      // Additional items up to 120+ can be added here
    ];

    const defaultLabor = [
      { name:'Mason',       rate:1200, mandays:0.12 },
      { name:'Bar Bender',  rate:950,  mandays:0.08 },
      { name:'Carpenter',   rate:1100, mandays:0.09 },
      { name:'Electrician', rate:1050, mandays:0.06 },
      { name:'Plumber',     rate:900,  mandays:0.05 },
      { name:'Painter',     rate:850,  mandays:0.07 },
      { name:'Tile Mason',  rate:1000, mandays:0.08 },
      { name:'Helper',      rate:700,  mandays:0.15 }
      // Additional labor types can be added here
    ];

    let materials = JSON.parse(JSON.stringify(defaultMaterials));
    let labors    = JSON.parse(JSON.stringify(defaultLabor));

    // ====== State Persistence ======
    const STATE_KEY = 'BD_Construction_Calc';
    function saveState() {
      const state = {
        area: document.getElementById('area').value,
        floors: document.getElementById('floors').value,
        quality: document.getElementById('quality').value,
        location: document.getElementById('location').value,
        inflation: document.getElementById('inflation').value,
        vat: document.getElementById('vat').value,
        transport: document.getElementById('transport').value,
        materials: materials,
        labors: labors
      };
      localStorage.setItem(STATE_KEY, JSON.stringify(state));
    }
    function loadState() {
      try {
        const saved = JSON.parse(localStorage.getItem(STATE_KEY));
        if (saved) {
          if(saved.area)      document.getElementById('area').value = saved.area;
          if(saved.floors)    document.getElementById('floors').value = saved.floors;
          if(saved.quality)   document.getElementById('quality').value = saved.quality;
          if(saved.location)  document.getElementById('location').value = saved.location;
          if(saved.inflation){
            document.getElementById('inflation').value = saved.inflation;
            document.getElementById('inflationVal').innerText = saved.inflation + '%';
          }
          if(saved.vat)       document.getElementById('vat').value = saved.vat;
          if(saved.transport) document.getElementById('transport').value = saved.transport;
          if(saved.materials) materials = saved.materials;
          if(saved.labors)    labors = saved.labors;
        }
      } catch (e) {
        console.warn('Could not load state', e);
      }
    }

    document.querySelectorAll('input, select').forEach(el => {
      el.addEventListener('change', saveState);
    });
    loadState();

    // UI Helpers
    document.getElementById('inflation').addEventListener('input', function(){
      document.getElementById('inflationVal').innerText = this.value + '%';
      saveState();
    });

    function toggleTheme() {
      const html = document.documentElement;
      if (html.getAttribute('data-theme') === 'light') {
        html.removeAttribute('data-theme');
      } else {
        html.setAttribute('data-theme', 'light');
      }
    }

    function copySummary() {
      const total = document.getElementById('totalCost').innerText;
      const text = `Building Cost Estimate: Total ${total}`;
      navigator.clipboard.writeText(text).then(() => {
        alert('Summary copied to clipboard');
      }).catch(() => alert('Copy failed'));
    }

    function scrollToDetails() {
      document.getElementById('details').scrollIntoView({ behavior:'smooth' });
    }

    function exportCSV() {
      try {
        let csv = 'Category,Item,Quantity,Rate,Cost\n';
        materials.forEach(m => {
          const cost = (m.qty * m.rate * (parseFloat(document.getElementById('quality').value) || 1) *
                        (parseFloat(document.getElementById('location').value) || 1) *
                        (1 + parseFloat(document.getElementById('inflation').value)/100)).toFixed(2);
          csv += `Material,${m.name},${m.qty},${m.rate},${cost}\n`;
        });
        labors.forEach(l => {
          const cost = (l.mandays * l.rate * (parseFloat(document.getElementById('quality').value) || 1) *
                        (parseFloat(document.getElementById('location').value) || 1) *
                        (1 + parseFloat(document.getElementById('inflation').value)/100)).toFixed(2);
          csv += `Labor,${l.name},${l.mandays},${l.rate},${cost}\n`;
        });
        const blob = new Blob([csv], { type: 'text/csv' });
        const url = URL.createObjectURL(blob);
        const a = document.createElement('a');
        a.href = url; a.download = 'estimate.csv'; a.click();
        URL.revokeObjectURL(url);
      } catch (err) {
        console.error('Export CSV failed', err);
        alert('Failed to export');
      }
    }

    // ====== Live Market Simulation ======
    function refreshMarket() {
      try {
        let cementPrice = 500 + Math.random()*100;
        let rodPrice    = 85000 + Math.random()*10000;

        let cementChange = (cementPrice - 530).toFixed(1) + '%';
        let rodChange    = (rodPrice - 90000).toFixed(1) + '%';

        const cementEl = document.getElementById('market-cement');
        const rodEl    = document.getElementById('market-rod');
        cementEl.innerText = Math.round(cementPrice);
        rodEl.innerText    = Math.round(rodPrice);

        const cementChEl = document.getElementById('cementChange');
        const rodChEl    = document.getElementById('rodChange');

        cementChEl.innerText = (cementPrice>=530?'+':'') + cementChange;
        rodChEl.innerText    = (rodPrice>=90000?'+':'') + rodChange;

        cementChEl.className = cementPrice>=530 ? 'green' : 'red';
        rodChEl.className    = rodPrice>=90000 ? 'green' : 'red';

        document.getElementById('market-timestamp').innerText =
          'Updated: ' + new Date().toLocaleTimeString();
      } catch (e) {
        console.error('Market update error', e);
      }
    }
    setInterval(refreshMarket, 120000);
    window.addEventListener('load', refreshMarket);

    // ====== Core Calculation ======
    let costChart = null;
    function renderChart(materialCost, laborCost, otherCost) {
      const ctx = document.getElementById('costChart').getContext('2d');
      if (costChart) costChart.destroy();
      costChart = new Chart(ctx, {
        type: 'doughnut',
        data: {
          labels: ['Materials','Labor','Other'],
          datasets: [{
            data: [materialCost, laborCost, otherCost],
            backgroundColor: [getComputedStyle(document.documentElement).getPropertyValue('--primary') || '#00C6FF',
                               getComputedStyle(document.documentElement).getPropertyValue('--success') || '#00FF99',
                               getComputedStyle(document.documentElement).getPropertyValue('--warn')    || '#FF4D4D']
          }]
        },
        options: {
          plugins: {
            legend: { labels: { color: getComputedStyle(document.documentElement).getPropertyValue('--text') || '#E5E7EB' } }
          }
        }
      });
    }

    function calculate() {
      const area = Number(document.getElementById('area').value) || 0;
      const floors = Number(document.getElementById('floors').value) || 1;
      if (area < 100) { alert('Area must be at least 100 sqft'); return; }
      if (floors < 1) { alert('Floors must be >= 1'); return; }

      const qualityMul = parseFloat(document.getElementById('quality').value);
      const locationMul = parseFloat(document.getElementById('location').value);
      const inflationMul = 1 + (Number(document.getElementById('inflation').value)/100);
      const vatPct = Number(document.getElementById('vat').value) / 100;
      const transportPct = Number(document.getElementById('transport').value) / 100;

      let totalMat = 0, matHtml = '';
      materials.forEach(item => {
        const qtyTotal = item.qty * area * floors;
        const cost = qtyTotal * item.rate * qualityMul * locationMul * inflationMul;
        totalMat += cost;
        matHtml += `<div>${item.name}: ${qtyTotal.toFixed(1)} units × ${item.rate} ৳ = ${Math.round(cost)} ৳</div>`;
      });

      let totalLab = 0, laborHtml = '', totalManDays = 0;
      labors.forEach(item => {
        const manDays = item.mandays * area * floors;
        const cost = manDays * item.rate * qualityMul * locationMul * inflationMul;
        totalLab += cost;
        totalManDays += manDays;
        laborHtml += `<div>${item.name}: ${manDays.toFixed(0)} man-days × ${item.rate} ৳ = ${Math.round(cost)} ৳</div>`;
      });

      const baseCost = totalMat + totalLab;
      const architect = baseCost * 0.055;
      const rajuk     = baseCost * 0.03;
      const contractor= baseCost * 0.13;
      const contingency = baseCost * 0.12;
      const utilities   = baseCost * 0.035;
      const transportCost = baseCost * transportPct;
      const vatCost = baseCost * vatPct;
      const grandTotal = baseCost + architect + rajuk + contractor + contingency + utilities + transportCost + vatCost;

      document.getElementById('materialsList').innerHTML = matHtml;
      document.getElementById('laborList').innerHTML = laborHtml;
      document.getElementById('totalMaterials').innerText = Math.round(totalMat) + ' ৳';
      document.getElementById('totalLabor').innerText = Math.round(totalLab) + ' ৳';
      document.getElementById('totalManDays').innerText = totalManDays.toFixed(0);

      document.getElementById('finalCosts').innerHTML = `
        Base: ${Math.round(baseCost)} ৳<br>
        Architect (5.5%): ${Math.round(architect)} ৳<br>
        RAJUK (3%): ${Math.round(rajuk)} ৳<br>
        Contractor (13%): ${Math.round(contractor)} ৳<br>
        Contingency (12%): ${Math.round(contingency)} ৳<br>
        Utilities (3.5%): ${Math.round(utilities)} ৳<br>
        ${transportPct>0?`Transport (${(transportPct*100).toFixed(1)}%): ${Math.round(transportCost)} ৳<br>`:''}
        ${vatPct>0?`VAT (${(vatPct*100).toFixed(1)}%): ${Math.round(vatCost)} ৳<br>`:''}
        <strong>Total: ${Math.round(grandTotal)} ৳</strong>
      `;

      document.getElementById('totalCost').innerText = Math.round(grandTotal) + ' ৳';
      const costPerSqft = Math.round(grandTotal / area);
      document.getElementById('yourCost').innerText = costPerSqft;
      document.getElementById('marketAvg').innerText = 2600;
      const savings = Math.max(0, ((2600 - costPerSqft) / 2600 * 100)).toFixed(1);
      document.getElementById('savings').innerText = savings + '%';

      let qualText = 'Good';
      if (costPerSqft > 3200) qualText = 'Premium';
      else if (costPerSqft < 2400) qualText = 'Normal';
      document.getElementById('qualityBadge').innerHTML =
        `<div style="padding:5px 10px; display:inline-block; border-radius:5px; background:${qualText==='Premium'?getComputedStyle(document.documentElement).getPropertyValue('--warn'):getComputedStyle(document.documentElement).getPropertyValue('--success')}; color:#fff;">
          ${qualText} Quality
        </div>`;

      document.getElementById('summaryTitle').innerText = `📊 ${area} sqft, ${floors} floor${floors>1?'s':''}`;
      document.getElementById('results').classList.add('show');

      try {
        renderChart(totalMat, totalLab, grandTotal - baseCost);
      } catch(e) {
        console.error('Chart render failed', e);
      }

      saveState();
    }

    window.addEventListener('DOMContentLoaded', calculate);
  </script>
</body>
</html>
