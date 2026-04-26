<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🏗️ 2025 Construction Cost Calculator - Bangladesh (24 Materials + Daily Labor)</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1500px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #2c3e50, #3498db);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        .header p {
            font-size: 1.2em;
        }

        .input-section {
            padding: 40px;
            background: #f8f9fa;
            border-bottom: 1px solid #eee;
        }

        .input-tabs {
            display: flex;
            justify-content: center;
            margin-bottom: 30px;
            background: white;
            border-radius: 50px;
            padding: 5px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            flex-wrap: wrap;
        }

        .tab-btn {
            padding: 12px 20px;
            border: none;
            background: transparent;
            border-radius: 40px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
            font-size: 0.95em;
            margin: 2px;
        }

        .tab-btn.active {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.4);
        }

        .input-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
            align-items: end;
        }

        .input-field {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
        }

        .input-field.full-width {
            grid-column: 1 / -1;
        }

        .custom-rates-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 15px;
            margin: 20px 0;
            max-height: 500px;
            overflow-y: auto;
            padding: 25px;
            background: white;
            border-radius: 15px;
            border: 2px solid #e9ecef;
            box-shadow: 0 5px 20px rgba(0,0,0,0.05);
        }

        .rate-item {
            display: flex;
            flex-direction: column;
            gap: 8px;
            padding: 20px 15px;
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border-radius: 12px;
            border-left: 5px solid #3498db;
            transition: all 0.3s;
        }

        .rate-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
        }

        .rate-item label {
            font-weight: bold;
            font-size: 0.95em;
            color: #2c3e50;
        }

        .rate-item input {
            width: 100%;
            padding: 12px 10px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1em;
            text-align: center;
            font-weight: bold;
        }

        .rate-item input:focus {
            border-color: #3498db;
            box-shadow: 0 0 15px rgba(52, 152, 219, 0.3);
            outline: none;
        }

        .rate-unit {
            font-size: 0.8em;
            color: #666;
            text-align: center;
            margin-top: -5px;
            font-weight: bold;
        }

        .daily-rate { border-left-color: #27ae60 !important; }
        .daily-rate .rate-unit { color: #27ae60 !important; }

        select, input[type="number"], input[type="range"] {
            width: 100%;
            padding: 15px;
            font-size: 1.2em;
            border: 3px solid #ddd;
            border-radius: 12px;
            text-align: center;
            transition: all 0.3s;
            background: white;
        }

        .calculate-btn, .reset-btn {
            border: none;
            padding: 20px 40px;
            font-size: 1.3em;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: bold;
            grid-column: 1 / -1;
        }

        .calculate-btn {
            background: linear-gradient(135deg, #27ae60, #2ecc71);
            color: white;
        }

        .calculate-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 30px rgba(39, 174, 96, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #e74c3c, #c0392b);
            color: white;
            margin-top: 15px;
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(231, 76, 60, 0.4);
        }

        /* Results styles */
        .results { padding: 40px; display: none; }
        .results.show { display: block; animation: slideIn 0.5s ease-out; }
        @keyframes slideIn { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }

        .summary-card { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; padding: 30px; border-radius: 20px; margin-bottom: 30px; text-align: center; }
        .total-cost { font-size: 3.5em; font-weight: bold; background: rgba(255,255,255,0.2); padding: 25px; border-radius: 15px; margin: 20px 0; }
        .cost-comparison { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-top: 20px; }
        .comparison-item { background: rgba(255,255,255,0.2); padding: 15px; border-radius: 10px; text-align: center; }
        .breakdown { display: grid; grid-template-columns: repeat(auto-fit, minmax(350px, 1fr)); gap: 25px; margin-top: 30px; }
        .card { background: white; padding: 30px; border-radius: 20px; box-shadow: 0 15px 35px rgba(0,0,0,0.1); border-top: 5px solid #3498db; }
        .group-title { font-size: 1.5em; font-weight: bold; margin-bottom: 25px; padding-bottom: 15px; border-bottom: 4px solid #3498db; color: #2c3e50; }
        .item { display: flex; justify-content: space-between; padding: 15px 0; border-bottom: 1px solid #eee; font-size: 1.1em; }
        .item:last-child { border-bottom: none; font-weight: bold; background: linear-gradient(135deg, #f8f9fa, #e9ecef); padding: 20px; border-radius: 12px; color: #27ae60; font-size: 1.3em; margin-top: 10px; }
        .labor-details { font-size: 0.9em; color: #666; margin-top: 5px; }
        .timeline-section { background: linear-gradient(135deg, #f39c12, #e67e22); color: white; padding: 30px; border-radius: 20px; text-align: center; margin: 30px 0; }
        .gantt-chart { display: flex; gap: 10px; justify-content: center; flex-wrap: wrap; margin-top: 20px; }
        .gantt-item { background: rgba(255,255,255,0.3); padding: 12px 20px; border-radius: 25px; font-size: 0.9em; font-weight: bold; }
        .print-btn { background: #e74c3c; color: white; border: none; padding: 15px 30px; border-radius: 25px; cursor: pointer; font-weight: bold; margin-top: 15px; transition: all 0.3s; font-size: 1.1em; }
        .print-btn:hover { transform: scale(1.05); box-shadow: 0 5px 15px rgba(231, 76, 60, 0.4); }
        .quality-badge { padding: 12px 25px; border-radius: 25px; font-weight: bold; font-size: 1em; margin: 5px; display: inline-block; }
        .normal { background: #f39c12; color: white; }
        .good { background: #27ae60; color: white; }
        .premium { background: #e74c3c; color: white; }

        @media (max-width: 768px) {
            .input-grid, .custom-rates-grid { grid-template-columns: 1fr; }
            .total-cost { font-size: 2.5em; }
            .breakdown { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🏗️ 2025 Construction Cost Calculator</h1>
            <p>চট্টগ্রাম সহ সম্পূর্ণ বাংলাদেশ | ২৪টি Material + Daily Labor Rates</p>
        </div>

        <div class="input-section">
            <div class="input-tabs">
                <button class="tab-btn active" onclick="switchTab('basic')">Basic</button>
                <button class="tab-btn" onclick="switchTab('advanced')">Advanced</button>
                <button class="tab-btn" onclick="switchTab('custom')">💰 Custom (24 Materials + Daily Labor)</button>
            </div>

            <div id="basic-tab" class="input-grid">
                <div class="input-field">
                    <label for="area">📏 Building Area</label>
                    <input type="number" id="area" placeholder="1000" min="100" step="50" value="1000">
                    <span>sq ft</span>
                </div>
                <div class="input-field">
                    <label for="floors">🏢 Floors</label>
                    <input type="number" id="floors" min="1" max="15" value="3">
                </div>
                <div class="input-field">
                    <label for="quality">⭐ Quality</label>
                    <select id="quality">
                        <option value="normal">Normal</option>
                        <option value="good" selected>Good</option>
                        <option value="premium">Premium</option>
                    </select>
                </div>
                <button class="calculate-btn" onclick="calculateCost()">🚀 Calculate 2025 Rates</button>
            </div>

            <div id="advanced-tab" class="input-grid" style="display: none;">
                <div class="input-field">
                    <label for="areaAdv">📏 Total Area</label>
                    <input type="number" id="areaAdv" placeholder="1000" min="100" step="50" value="1000">
                    <span>sq ft</span>
                </div>
                <div class="input-field">
                    <label for="locationMultiplier">📍 Location (2025)</label>
                    <select id="locationMultiplier">
                        <option value="1.10">Dhaka City (110%)</option>
                        <option value="0.95" selected>Chattogram City (95%)</option>
                        <option value="0.85">Dhaka Suburb (85%)</option>
                        <option value="0.78">Divisional City (78%)</option>
                        <option value="0.68">Chattogram Suburb (68%)</option>
                        <option value="0.65">Rural Area (65%)</option>
                    </select>
                </div>
                <div class="input-field">
                    <label for="inflationRate">📈 2025 Inflation</label>
                    <input type="range" id="inflationRate" min="0" max="40" value="15">
                    <div class="range-label">
                        <span>0%</span>
                        <span id="inflationValue">15%</span>
                        <span>40%</span>
                    </div>
                </div>
                <button class="calculate-btn" onclick="calculateCost()">💎 Advanced 2025 Calc</button>
            </div>

            <div id="custom-tab" class="input-grid" style="display: none;">
                <div class="input-field">
                    <label for="customArea">📏 Area</label>
                    <input type="number" id="customArea" placeholder="1000" min="100" step="50" value="1000">
                    <span>sq ft</span>
                </div>
                <div class="input-field full-width">
                    <label>💰 2025 Custom Material Rates (24 Items)</label>
                    <div class="custom-rates-grid" id="customRatesGrid"></div>
                </div>
                <div class="input-field full-width">
                    <label>👷 2025 Daily Labor Rates (৮ ধরন)</label>
                    <div class="custom-rates-grid" id="customLaborGrid"></div>
                </div>
                <button class="calculate-btn" onclick="calculateCost()">✨ Calculate Custom 2025</button>
                <button class="reset-btn" onclick="resetCustomRates()">🔄 Reset 2025 Default</button>
            </div>
        </div>

        <div class="results" id="results">
            <div class="summary-card">
                <h2 id="summaryTitle">2025 Building Cost Summary</h2>
                <div class="total-cost" id="totalCost">0 ৳</div>
                <div id="costPerSqft"></div>
                <div class="cost-comparison">
                    <div class="comparison-item">
                        <div style="font-size: 1.5em;">🏆 2025 Market Avg</div>
                        <div id="marketAvg" style="font-size: 1.8em; font-weight: bold;">2600</div>
                        <span>৳/sqft</span>
                    </div>
                    <div class="comparison-item">
                        <div>💰 Your Cost</div>
                        <div id="yourCost" style="font-size: 1.8em; font-weight: bold; color: #27ae60;">2600</div>
                        <span>৳/sqft</span>
                    </div>
                    <div class="comparison-item">
                        <div>⭐ Savings</div>
                        <div id="savings" style="font-size: 1.8em; font-weight: bold;">0%</div>
                        <span>vs Market</span>
                    </div>
                </div>
                <div id="qualityIndicator"></div>
                <button class="print-btn" onclick="printReport()">🖨️ Print 2025 Report</button>
            </div>

            <div class="timeline-section">
                <h3 id="timelineTitle">⏱️ 2025 Construction Timeline</h3>
                <div id="timeline"></div>
                <div class="gantt-chart" id="ganttChart"></div>
            </div>

            <div class="breakdown">
                <div class="card">
                    <div class="group-title">🔨 2025 Material Breakdown (24 Items)</div>
                    <div id="materialsList"></div>
                    <div id="totalMaterials"></div>
                </div>
                <div class="card">
                    <div class="group-title">👷 2025 Daily Labor Breakdown (৮ ধরন)</div>
                    <div id="laborList"></div>
                    <div id="totalLabor"></div>
                    <div id="laborManDays"></div>
                </div>
                <div class="card">
                    <div class="group-title">📊 2025 Additional Costs</div>
                    <div id="finalBreakdown"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 2025 Updated Material Rates (24 Materials) - Chattogram included
        let customMaterials = {
            // Foundation Materials
            bricks: { qty: 5.2, rate: 16, name: 'ব্রিক' },
            sand: { qty: 0.022, rate: 2200, name: 'বালি' },
                        cement: { qty: 0.062, rate: 680, name: 'সিমেন্ট (OPC)' },
            stone: { qty: 0.020, rate: 2900, name: 'স্টোন চিপস' },
            
            // Steel & Structure
            iron12mm: { qty: 1.2, rate: 125, name: '১২mm রড' },
            iron16mm: { qty: 0.8, rate: 125, name: '১৬mm রড' },
            iron20mm: { qty: 0.2, rate: 125, name: '২০mm রড' },
            
            // Concrete & Masonry
            crushed_stone: { qty: 0.015, rate: 2800, name: 'ক্রাশড স্টোন' },
            gravel: { qty: 0.012, rate: 2100, name: 'গ্রাভেল' },
            
            // Formwork & Carpentry
            plywood: { qty: 0.8, rate: 145, name: 'প্লাইউড' },
            shuttering: { qty: 1.2, rate: 85, name: 'শাটারিং' },
            timber: { qty: 0.008, rate: 11500, name: 'টিম্বার' },
            
            // Finishing Materials
            tiles: { qty: 0.92, rate: 92, name: 'সিরামিক টাইলস' },
            marble: { qty: 0.15, rate: 450, name: 'মার্বেল' },
            paint: { qty: 0.028, rate: 320, name: 'পেইন্ট' },
            
            // Doors & Windows
            aluminum: { qty: 0.18, rate: 420, name: 'অ্যালুমিনিয়াম' },
            glass: { qty: 0.15, rate: 380, name: 'গ্লাস' },
            hardware: { qty: 0.045, rate: 1250, name: 'হার্ডওয়্যার' },
            
            // Electrical & Plumbing
            electrical_wire: { qty: 0.75, rate: 45, name: 'ইলেকট্রিক ওয়্যার' },
            switch_socket: { qty: 0.035, rate: 2850, name: 'সুইচ/সকেট' },
            plumbing_pipe: { qty: 0.15, rate: 85, name: 'পিভিসি পাইপ' },
            sanitary: { qty: 0.032, rate: 8200, name: 'স্যানিটারি' },
            
            // Miscellaneous
            gypsum_board: { qty: 0.12, rate: 165, name: 'জিপসাম বোর্ড' },
            ac_sheet: { qty: 0.08, rate: 125, name: 'এসি শিট' }
        };

        // 2025 DAILY Labor Rates (BDT per DAY per worker)
        let customLabor = {
            mason: { rate: 1200, name: 'মিস্ত্রি', mandays: 0.12 },
            barbender: { rate: 950, name: 'বারবেন্ডার', mandays: 0.08 },
            carpenter: { rate: 1100, name: 'কার্পেন্টার', mandays: 0.09 },
            electrician: { rate: 1050, name: 'ইলেকট্রিশিয়ান', mandays: 0.06 },
            plumber: { rate: 900, name: 'প্লাম্বার', mandays: 0.05 },
            painter: { rate: 850, name: 'পেইন্টার', mandays: 0.07 },
            tile_mason: { rate: 1000, name: 'টাইল মিস্ত্রি', mandays: 0.08 },
            helper: { rate: 650, name: 'হেল্পার', mandays: 0.15 }
        };

        let currentTab = 'basic';

        // Create custom rates UI
        function createCustomRatesUI() {
            let materialsHtml = '';
            for (let key in customMaterials) {
                const item = customMaterials[key];
                materialsHtml += `
                    <div class="rate-item">
                        <label>${item.name}</label>
                        <input type="number" id="mat_${key}_qty" value="${item.qty}" step="0.001" min="0" placeholder="Qty">
                        <span class="rate-unit">/sqft</span>
                        <input type="number" id="mat_${key}_rate" value="${item.rate}" min="0" placeholder="Rate">
                        <span class="rate-unit">৳/unit</span>
                    </div>
                `;
            }
            document.getElementById('customRatesGrid').innerHTML = materialsHtml;

            let laborHtml = '';
            for (let key in customLabor) {
                const item = customLabor[key];
                laborHtml += `
                    <div class="rate-item daily-rate">
                        <label>${item.name}</label>
                        <input type="number" id="lab_${key}_rate" value="${item.rate}" min="0" step="50" placeholder="Daily Rate">
                        <span class="rate-unit">৳/দিন/জন</span>
                        <input type="number" id="lab_${key}_mandays" value="${item.mandays}" step="0.01" min="0" placeholder="Man-days">
                        <span class="rate-unit">/sqft</span>
                    </div>
                `;
            }
            document.getElementById('customLaborGrid').innerHTML = laborHtml;
        }

        function switchTab(tab) {
            currentTab = tab;
            document.getElementById('basic-tab').style.display = 'none';
            document.getElementById('advanced-tab').style.display = 'none';
            document.getElementById('custom-tab').style.display = 'none';
            
            document.getElementById(tab + '-tab').style.display = 'grid';
            
            if (tab === 'custom') {
                createCustomRatesUI();
            }
            
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
        }

        document.getElementById('inflationRate').addEventListener('input', function() {
            document.getElementById('inflationValue').textContent = this.value + '%';
        });

        function resetCustomRates() {
            customMaterials = {
                bricks: { qty: 5.2, rate: 16, name: 'ব্রিক' },
                sand: { qty: 0.022, rate: 2200, name: 'বালি' },
                cement: { qty: 0.062, rate: 680, name: 'সিমেন্ট (OPC)' },
                stone: { qty: 0.020, rate: 2900, name: 'স্টোন চিপস' },
                iron12mm: { qty: 1.2, rate: 125, name: '১২mm রড' },
                iron16mm: { qty: 0.8, rate: 125, name: '১৬mm রড' },
                iron20mm: { qty: 0.2, rate: 125, name: '২০mm রড' },
                crushed_stone: { qty: 0.015, rate: 2800, name: 'ক্রাশড স্টোন' },
                gravel: { qty: 0.012, rate: 2100, name: 'গ্রাভেল' },
                plywood: { qty: 0.8, rate: 145, name: 'প্লাইউড' },
                shuttering: { qty: 1.2, rate: 85, name: 'শাটারিং' },
                timber: { qty: 0.008, rate: 11500, name: 'টিম্বার' },
                tiles: { qty: 0.92, rate: 92, name: 'সিরামিক টাইলস' },
                marble: { qty: 0.15, rate: 450, name: 'মার্বেল' },
                paint: { qty: 0.028, rate: 320, name: 'পেইন্ট' },
                aluminum: { qty: 0.18, rate: 420, name: 'অ্যালুমিনিয়াম' },
                glass: { qty: 0.15, rate: 380, name: 'গ্লাস' },
                hardware: { qty: 0.045, rate: 1250, name: 'হার্ডওয়্যার' },
                electrical_wire: { qty: 0.75, rate: 45, name: 'ইলেকট্রিক ওয়্যার' },
                switch_socket: { qty: 0.035, rate: 2850, name: 'সুইচ/সকেট' },
                plumbing_pipe: { qty: 0.15, rate: 85, name: 'পিভিসি পাইপ' },
                sanitary: { qty: 0.032, rate: 8200, name: 'স্যানিটারি' },
                gypsum_board: { qty: 0.12, rate: 165, name: 'জিপসাম বোর্ড' },
                ac_sheet: { qty: 0.08, rate: 125, name: 'এসি শিট' }
            };

            customLabor = {
                mason: { rate: 1200, name: 'মিস্ত্রি', mandays: 0.12 },
                barbender: { rate: 950, name: 'বারবেন্ডার', mandays: 0.08 },
                carpenter: { rate: 1100, name: 'কার্পেন্টার', mandays: 0.09 },
                electrician: { rate: 1050, name: 'ইলেকট্রিশিয়ান', mandays: 0.06 },
                plumber: { rate: 900, name: 'প্লাম্বার', mandays: 0.05 },
                painter: { rate: 850, name: 'পেইন্টার', mandays: 0.07 },
                tile_mason: { rate: 1000, name: 'টাইল মিস্ত্রি', mandays: 0.08 },
                helper: { rate: 650, name: 'হেল্পার', mandays: 0.15 }
            };

            createCustomRatesUI();
            alert('✅ 2025 Default Daily Rates Restored!\n👷 ৮ ধরনের লেবার: প্রতিদিনের দর + Man-days');
        }

        function calculateCost() {
            let area, floors = 3;
            if (currentTab === 'basic') {
                area = parseFloat(document.getElementById('area').value);
                floors = parseInt(document.getElementById('floors').value);
            } else if (currentTab === 'advanced') {
                area = parseFloat(document.getElementById('areaAdv').value);
            } else {
                area = parseFloat(document.getElementById('customArea').value);
            }

            if (!area || area < 100) {
                alert('দয়া করে সঠিক এরিয়া দিন (ন্যূনতম ১০০ স্কয়ার ফুট)');
                return;
            }

            // Update custom rates
            if (currentTab === 'custom') {
                for (let key in customMaterials) {
                    customMaterials[key].qty = parseFloat(document.getElementById(`mat_${key}_qty`).value) || 0;
                    customMaterials[key].rate = parseFloat(document.getElementById(`mat_${key}_rate`).value) || 0;
                }
                for (let key in customLabor) {
                    customLabor[key].rate = parseFloat(document.getElementById(`lab_${key}_rate`).value) || 0;
                    customLabor[key].mandays = parseFloat(document.getElementById(`lab_${key}_mandays`).value) || 0;
                }
            }

            // Multipliers
            let materialMultiplier = 1.0, laborMultiplier = 1.0, locationMultiplier = 1.0, inflationMultiplier = 1.0;
            
            if (currentTab === 'basic') {
                const quality = document.getElementById('quality').value;
                materialMultiplier = quality === 'premium' ? 1.3 : quality === 'normal' ? 0.82 : 1.0;
                laborMultiplier = quality === 'premium' ? 1.2 : quality === 'normal' ? 0.88 : 1.0;
            } else if (currentTab === 'advanced') {
                locationMultiplier = parseFloat(document.getElementById('locationMultiplier').value);
                inflationMultiplier = 1 + (parseInt(document.getElementById('inflationRate').value) / 100);
            }

            // Calculate Materials (24 items)
            let totalMaterials = 0;
            let materialsHtml = '';
            for (let key in customMaterials) {
                const item = customMaterials[key];
                const qty = (item.qty * area).toFixed(1);
                const cost = item.qty * area * item.rate * materialMultiplier * locationMultiplier * inflationMultiplier;
                totalMaterials += cost;
                materialsHtml += `
                    <div class="item">
                        <span>${item.name}: ${qty} @${formatNumber(item.rate)}৳</span>
                        <span>${formatNumber(cost)}৳</span>
                    </div>
                `;
            }

            // Calculate DAILY Labor (8 types) - NEW FORMULA
            let totalLabor = 0;
            let totalManDays = 0;
            let laborHtml = '';
            for (let key in customLabor) {
                const item = customLabor[key];
                const manDaysPerSqft = item.mandays;
                const totalManDaysForProject = manDaysPerSqft * area * floors;
                const laborCost = totalManDaysForProject * item.rate * laborMultiplier * locationMultiplier * inflationMultiplier;
                totalLabor += laborCost;
                totalManDays += totalManDaysForProject;
                
                laborHtml += `
                    <div class="item">
                        <span>${item.name}</span>
                        <span>${formatNumber(laborCost)}৳</span>
                        <div class="labor-details">
                            ${totalManDaysForProject.toFixed(0)} man-days × ${formatNumber(item.rate)}৳/day
                        </div>
                    </div>
                `;
            }

            const baseCost = totalMaterials + totalLabor;
            const architectFee = baseCost * 0.055;
            const govtFee = baseCost * 0.03;
            const contractorProfit = baseCost * 0.13;
            const contingency = baseCost * 0.12;
            const utilities = baseCost * 0.035;
            const grandTotal = baseCost + architectFee + govtFee + contractorProfit + contingency + utilities;

            const days = Math.ceil((area * floors * 0.75) / 38);
            const months = Math.ceil(days / 28);
            const costPerSqft = Math.round(grandTotal / area);
            const marketAvg = 2600;
            const savings = Math.max(0, ((marketAvg - costPerSqft) / marketAvg * 100)).toFixed(1);

            let quality = 'Normal';
            if (costPerSqft > 3200) quality = 'Premium';
            else if (costPerSqft > 2400) quality = 'Good';

            // Update UI
            document.getElementById('materialsList').innerHTML = materialsHtml;
            document.getElementById('totalMaterials').innerHTML = `<div class="item"><span>💰 মোট ম্যাটেরিয়াল (২৪ Items)</span><span>${formatNumber(totalMaterials)}৳</span></div>`;
            document.getElementById('laborList').innerHTML = laborHtml;
            document.getElementById('totalLabor').innerHTML = `<div class="item"><span>💰 মোট লেবার (৮ ধরন)</span><span>${formatNumber(totalLabor)}৳</span></div>`;
            document.getElementById('laborManDays').innerHTML = `<div class="item" style="background: linear-gradient(135deg, #3498db, #2980b9); color: white; border-radius: 12px; padding: 15px;">
                <span>👥 মোট Man-Days: ${totalManDays.toFixed(0)}</span>
                <span>${Math.round(totalManDays/days)} জন/দিন (${days} দিন)</span>
            </div>`;
            
            document.getElementById('totalCost').textContent = formatNumber(grandTotal) + ' ৳';
            document.getElementById('costPerSqft').innerHTML = `<strong>${costPerSqft} ৳/স্কয়ারফুট (২০২৫)</strong>`;
            document.getElementById('summaryTitle').textContent = `🏠 ${area.toLocaleString()} স্কয়ারফুট বিল্ডিং`;
            document.getElementById('marketAvg').textContent = marketAvg;
            document.getElementById('yourCost').textContent = costPerSqft;
            document.getElementById('savings').textContent = savings + '%';
            
            document.getElementById('qualityIndicator').innerHTML = `<div class="quality-badge ${quality.toLowerCase()}">${quality} কোয়ালিটি ২০২৫</div>`;
            document.getElementById('timelineTitle').innerHTML = `⏱️ ২০২৫ নির্মাণ সময়: ${days} দিন (${months} মাস) | ${Math.round(totalManDays/days)} জন/দিন`;
            document.getElementById('ganttChart').innerHTML = `
                                <div class="gantt-item">🏗️ ফাউন্ডেশন: ${Math.ceil(days*0.22)} দিন</div>
                <div class="gantt-item">🔨 স্ট্রাকচার: ${Math.ceil(days*0.38)} দিন</div>
                <div class="gantt-item">⚡ ইলেকট্রিক: ${Math.ceil(days*0.18)} দিন</div>
                <div class="gantt-item">🪚 ফিনিশিং: ${Math.ceil(days*0.22)} দিন</div>
            `;

            document.getElementById('finalBreakdown').innerHTML = `
                <div class="item"><span>🏗️ মৌলিক খরচ (২৪ Materials + ৮ Labor)</span><span>${formatNumber(baseCost)}৳</span></div>
                <div class="item"><span>📐 আর্কিটেক্ট (৫.৫%)</span><span>${formatNumber(architectFee)}৳</span></div>
                <div class="item"><span>🏛️ RAJUK/সরকারি (৩%)</span><span>${formatNumber(govtFee)}৳</span></div>
                <div class="item"><span>💼 কন্ট্রাক্টর (১৩%)</span><span>${formatNumber(contractorProfit)}৳</span></div>
                <div class="item"><span>🛡️ কনটিনজেন্সি (১২%)</span><span>${formatNumber(contingency)}৳</span></div>
                <div class="item"><span>🔌 ইউটিলিটিস (৩.৫%)</span><span>${formatNumber(utilities)}৳</span></div>
                <div class="item" style="font-size:1.4em;color:#e74c3c;background:linear-gradient(135deg,#ffeaa7,#ffd93d);border-radius:12px;padding:20px;">
                    <span>🎯 ২০২৫ মোট খরচ</span><span>${formatNumber(grandTotal)}৳</span>
                </div>
            `;

            document.getElementById('results').classList.add('show');
            document.getElementById('results').scrollIntoView({ behavior: 'smooth' });
        }

        function formatNumber(num) {
            return num.toLocaleString('bn-BD', { maximumFractionDigits: 0 });
        }

        function printReport() {
            window.print();
        }

        document.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                const activeInput = document.activeElement;
                if (activeInput.type === 'number') {
                    calculateCost();
                }
            }
        });

        // Auto-save/load functionality
        window.addEventListener('load', function() {
            // Load saved areas
            const savedArea = localStorage.getItem('area') || '1000';
            document.getElementById('area').value = savedArea;
            document.getElementById('areaAdv').value = savedArea;
            document.getElementById('customArea').value = savedArea;

            // Save inputs to localStorage
            document.querySelectorAll('input, select').forEach(input => {
                const savedValue = localStorage.getItem(input.id);
                if (savedValue && input.type !== 'range') {
                    input.value = savedValue;
                }
                input.addEventListener('change', function() {
                    localStorage.setItem(this.id, this.value);
                });
            });

            // Update range display
            document.getElementById('inflationRate').dispatchEvent(new Event('input'));

            // Initial calculation with 2025 Daily Labor rates
            setTimeout(() => {
                calculateCost();
            }, 1000);
        });

        // Performance optimization for large lists
        console.log('🚀 2025 Construction Calculator Loaded Successfully!');
        console.log('✅ 24 Materials + 8 Daily Labor Types');
        console.log('✅ Chattogram Rates Included');
        console.log('✅ Labor: Daily Rate × Man-days × Floors');
        console.log('✅ Fully Customizable with Man-days control');
    </script>
</body>
</html>
