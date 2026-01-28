<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sun Flower CRM Strategy & Data Lab</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600;700&family=Sarabun:wght@300;400;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        body { font-family: 'Sarabun', sans-serif; background-color: #f3f4f6; }
        h1, h2, h3, .font-kanit { font-family: 'Kanit', sans-serif; }
        .slide-content { height: 600px; display: none; }
        .slide-content.active { display: flex; }
        .sidebar-link.active { background-color: #003366; color: white; border-left: 4px solid #E67E22; }
        .sunflower-orange { color: #E67E22; }
        .sunflower-bg { background-color: #E67E22; }
        .navy-bg { background-color: #003366; }
        .navy-text { color: #003366; }
        
        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #f1f1f1; }
        ::-webkit-scrollbar-thumb { background: #888; border-radius: 10px; }
        ::-webkit-scrollbar-thumb:hover { background: #555; }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade { animation: fadeIn 0.4s ease-out forwards; }

        /* Chart Bar Animations */
        .bar-animate { transition: width 1.5s cubic-bezier(0.4, 0, 0.2, 1); }
    </style>
</head>
<body class="h-screen overflow-hidden flex flex-col">

    <!-- ส่วนหัว / แถบนำทางด้านบน -->
    <header class="navy-bg text-white p-4 flex justify-between items-center shadow-lg z-50">
        <div class="flex items-center gap-3">
            <div class="w-10 h-10 sunflower-bg rounded-full flex items-center justify-center">
                <i class="fa-solid fa-sun text-white text-xl"></i>
            </div>
            <div>
                <h1 class="text-xl font-bold leading-none uppercase">Sun Flower</h1>
                <p class="text-xs sunflower-orange font-bold uppercase tracking-widest">Strategic CRM Unit</p>
            </div>
        </div>
        <div class="flex gap-4">
            <button onclick="switchView('data')" id="btn-view-data" class="px-4 py-2 rounded-lg bg-white/10 hover:bg-white/20 transition-all flex items-center gap-2 border border-white/20">
                <i class="fa-solid fa-database"></i> ข้อมูลดิบ (Raw Data)
            </button>
            <button onclick="switchView('presentation')" id="btn-view-presentation" class="px-4 py-2 rounded-lg sunflower-bg hover:bg-orange-600 transition-all flex items-center gap-2 shadow-lg">
                <i class="fa-solid fa-display"></i> เริ่มนำเสนอ (Presentation)
            </button>
        </div>
    </header>

    <main class="flex-grow flex overflow-hidden">
        
        <!-- แถบเมนูด้านข้างสำหรับหน้าข้อมูลดิบ -->
        <aside id="data-sidebar" class="w-64 bg-white border-r border-gray-200 overflow-y-auto hidden">
            <div class="p-6">
                <h3 class="font-kanit font-bold text-gray-500 uppercase text-xs tracking-wider mb-4">คลังข้อมูลดิบ</h3>
                <nav class="space-y-1">
                    <a href="#" onclick="showDataSection(event, 'stores')" id="link-stores" class="sidebar-link active block p-3 rounded-lg text-sm transition-all flex items-center gap-3">
                        <i class="fa-solid fa-store"></i> สาขาและยอดขาย
                    </a>
                    <a href="#" onclick="showDataSection(event, 'metrics')" id="link-metrics" class="sidebar-link block p-3 rounded-lg text-sm text-gray-600 hover:bg-gray-50 flex items-center gap-3">
                        <i class="fa-solid fa-chart-line"></i> ตัวชี้วัดประสิทธิภาพ
                    </a>
                    <a href="#" onclick="showDataSection(event, 'profiles')" id="link-profiles" class="sidebar-link block p-3 rounded-lg text-sm text-gray-600 hover:bg-gray-50 flex items-center gap-3">
                        <i class="fa-solid fa-users"></i> โปรไฟล์ลูกค้า (Index)
                    </a>
                    <a href="#" onclick="showDataSection(event, 'market')" id="link-market" class="sidebar-link block p-3 rounded-lg text-sm text-gray-600 hover:bg-gray-50 flex items-center gap-3">
                        <i class="fa-solid fa-pie-chart"></i> Market Share รายภาค
                    </a>
                </nav>
            </div>
        </aside>

        <!-- พื้นที่แสดงเนื้อหาหลัก -->
        <section id="content-container" class="flex-grow overflow-y-auto p-8 bg-gray-50">
            
            <!-- ส่วนข้อมูลดิบ (Raw Data) -->
            <div id="data-content-wrapper" class="hidden animate-fade space-y-12">
                
                <!-- 1. ข้อมูลสาขาและสัดส่วนยอดขาย -->
                <div id="data-stores" class="data-section">
                    <h2 class="text-3xl font-kanit font-bold navy-text mb-6">โครงสร้างสาขาและยอดขาย</h2>
                    <div class="grid grid-cols-1 gap-8">
                        <div class="bg-white rounded-xl shadow-sm border p-6">
                            <h3 class="font-bold mb-4 navy-text">จำนวนสาขา (Number of Stores)</h3>
                            <div class="overflow-x-auto">
                                <table class="w-full text-left text-sm">
                                    <thead class="bg-gray-50 border-b">
                                        <tr>
                                            <th class="p-3 font-kanit">Format</th>
                                            <th class="p-3">2015</th>
                                            <th class="p-3">2016</th>
                                            <th class="p-3">2017</th>
                                            <th class="p-3">2018</th>
                                            <th class="p-3">2019</th>
                                        </tr>
                                    </thead>
                                    <tbody class="divide-y">
                                        <tr><td class="p-3 font-bold">Hypermarket</td><td>195</td><td>200</td><td>207</td><td>213</td><td>220</td></tr>
                                        <tr><td class="p-3 font-bold">Supermarket</td><td>97</td><td>102</td><td>106</td><td>110</td><td>112</td></tr>
                                        <tr><td class="p-3 font-bold">Convenience Store</td><td>450</td><td>460</td><td>470</td><td>485</td><td>500</td></tr>
                                    </tbody>
                                </table>
                            </div>
                        </div>

                        <div class="bg-white rounded-xl shadow-sm border p-6">
                            <h3 class="font-bold mb-4 navy-text">สัดส่วนยอดขาย (Sales Contributions %)</h3>
                            <div class="overflow-x-auto">
                                <table class="w-full text-left text-sm">
                                    <thead class="bg-gray-50 border-b">
                                        <tr>
                                            <th class="p-3 font-kanit">Format</th>
                                            <th class="p-3">2015</th>
                                            <th class="p-3">2016</th>
                                            <th class="p-3">2017</th>
                                            <th class="p-3">2018</th>
                                            <th class="p-3">2019</th>
                                        </tr>
                                    </thead>
                                    <tbody class="divide-y">
                                        <tr class="bg-red-50"><td class="p-3 font-bold text-red-600">Hypermarket</td><td>56%</td><td>53%</td><td>50%</td><td>48%</td><td class="font-bold">44%</td></tr>
                                        <tr><td class="p-3 font-bold">Supermarket</td><td>19%</td><td>20%</td><td>21%</td><td>22%</td><td>23%</td></tr>
                                        <tr><td class="p-3 font-bold">Convenience Store</td><td>24%</td><td>25%</td><td>26%</td><td>26%</td><td>27%</td></tr>
                                        <tr class="bg-green-50"><td class="p-3 font-bold text-green-600">Online</td><td>1%</td><td>2%</td><td>3%</td><td>4%</td><td class="font-bold">6%</td></tr>
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- 2. ตัวชี้วัดประสิทธิภาพ (Metrics) -->
                <div id="data-metrics" class="data-section hidden">
                    <h2 class="text-3xl font-kanit font-bold navy-text mb-6">ประสิทธิภาพและการเจริญเติบโต</h2>
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                        <!-- Frequency Table -->
                        <div class="bg-white rounded-xl shadow-sm border p-6">
                            <h3 class="font-bold mb-4 navy-text">ความถี่ในการซื้อ (Frequency per year)</h3>
                            <table class="w-full text-left text-sm">
                                <thead class="bg-gray-50 border-b">
                                    <tr>
                                        <th class="p-3 font-kanit">Format</th>
                                        <th class="p-3">2015</th>
                                        <th class="p-3">2016</th>
                                        <th class="p-3">2017</th>
                                        <th class="p-3">2018</th>
                                        <th class="p-3">2019</th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y">
                                    <tr class="bg-red-50"><td class="p-3 font-bold">Hypermarket</td><td>12</td><td>11</td><td>10</td><td>9</td><td class="font-bold text-red-600">8</td></tr>
                                    <tr><td class="p-3 font-bold">Supermarket</td><td>20</td><td>22</td><td>24</td><td>26</td><td>28</td></tr>
                                    <tr><td class="p-3 font-bold">Convenience</td><td>48</td><td>49</td><td>50</td><td>51</td><td>51</td></tr>
                                    <tr><td class="p-3 font-bold">Online</td><td>3</td><td>4</td><td>5</td><td>8</td><td>10</td></tr>
                                </tbody>
                            </table>
                        </div>
                        <!-- Basket Size -->
                        <div class="bg-white rounded-xl shadow-sm border p-6">
                            <h3 class="font-bold mb-4 navy-text">ขนาดตะกร้าเฉลี่ย (Average Basket - THB)</h3>
                            <table class="w-full text-left text-sm">
                                <thead class="bg-gray-50 border-b">
                                    <tr>
                                        <th class="p-3 font-kanit">Format</th>
                                        <th class="p-3">2015</th>
                                        <th class="p-3">2019</th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y">
                                    <tr><td class="p-3 font-bold">Hypermarket</td><td>650</td><td>725</td></tr>
                                    <tr><td class="p-3 font-bold">Supermarket</td><td>350</td><td>375</td></tr>
                                    <tr><td class="p-3 font-bold">Convenience</td><td>100</td><td>130</td></tr>
                                    <tr class="bg-blue-50"><td class="p-3 font-bold text-blue-700">Online</td><td>950</td><td class="font-bold">1,100</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- 3. โปรไฟล์ลูกค้า (Profiles) -->
                <div id="data-profiles" class="data-section hidden">
                    <h2 class="text-3xl font-kanit font-bold navy-text mb-6">ดัชนีโปรไฟล์ลูกค้า (Shopper Index)</h2>
                    <div class="bg-white rounded-xl shadow-sm border p-6">
                        <h3 class="font-bold mb-4 navy-text">Index เทียบกับค่าเฉลี่ยประเทศ (100 = Average)</h3>
                        <table class="w-full text-left text-sm">
                            <thead class="bg-gray-50 border-b">
                                <tr>
                                    <th class="p-3 font-kanit">Segment / Brand</th>
                                    <th class="p-3 text-center">Sun Flower</th>
                                    <th class="p-3 text-center">Giant (Comp)</th>
                                    <th class="p-3 text-center">Orange (Comp)</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y text-center">
                                <tr><td class="p-3 font-bold text-left">กลุ่ม AB (รายได้สูง)</td><td>110</td><td>115</td><td class="text-red-500 font-bold">92</td></tr>
                                <tr><td class="p-3 font-bold text-left">กลุ่ม C (รายได้กลาง)</td><td>100</td><td>104</td><td>97</td></tr>
                                <tr><td class="p-3 font-bold text-left">กลุ่ม DE (รายได้น้อย)</td><td>90</td><td>81</td><td>111</td></tr>
                                <tr class="bg-blue-50"><td class="p-3 font-bold text-left">Family with children</td><td class="font-bold text-blue-700">120</td><td>85</td><td>90</td></tr>
                                <tr><td class="p-3 font-bold text-left">Young Adult (20-39)</td><td>77</td><td>90</td><td class="text-green-600 font-bold">125</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- 4. ข้อมูล Market Share รายภูมิภาค -->
                <div id="data-market" class="data-section hidden">
                    <h2 class="text-3xl font-kanit font-bold navy-text mb-6">ส่วนแบ่งการตลาด (Market Share Trends)</h2>
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                        <div class="bg-white rounded-xl shadow-sm border p-6">
                            <h3 class="font-bold mb-4 navy-text">Hypermarket Nationwide Share</h3>
                            <table class="w-full text-left text-sm">
                                <thead class="bg-gray-50 border-b">
                                    <tr><th>Brand</th><th>2015</th><th>2017</th><th>2019</th></tr>
                                </thead>
                                <tbody class="divide-y">
                                    <tr class="bg-red-50"><td class="p-3 font-bold">Sun Flower</td><td>44%</td><td>45%</td><td class="font-bold text-red-600">41%</td></tr>
                                    <tr><td class="p-3 font-bold">Giant</td><td>21%</td><td>18%</td><td>19%</td></tr>
                                    <tr class="bg-green-50"><td class="p-3 font-bold text-green-700">Orange</td><td>35%</td><td>37%</td><td class="font-bold text-green-700">40%</td></tr>
                                </tbody>
                            </table>
                        </div>
                        <div class="bg-white rounded-xl shadow-sm border p-6">
                            <h3 class="font-bold mb-4 navy-text">Central Region Share (Hypermarket)</h3>
                            <table class="w-full text-left text-sm">
                                <thead class="bg-gray-50 border-b">
                                    <tr><th>Brand</th><th>2015</th><th>2017</th><th>2019</th></tr>
                                </thead>
                                <tbody class="divide-y">
                                    <tr class="bg-red-100"><td class="p-3 font-bold">Sun Flower</td><td>52%</td><td>47%</td><td class="font-bold text-red-700">40%</td></tr>
                                    <tr><td class="p-3 font-bold">Giant</td><td>47%</td><td>49%</td><td>51%</td></tr>
                                    <tr><td class="p-3 font-bold">Orange</td><td>1%</td><td>4%</td><td>9%</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

            <!-- ส่วนการนำเสนอ (Presentation) -->
            <div id="presentation-content-wrapper" class="h-full flex flex-col items-center justify-center animate-fade">
                <div class="w-full max-w-5xl bg-white aspect-[16/9] shadow-2xl rounded-2xl overflow-hidden relative flex flex-col border border-gray-200">
                    
                    <!-- Progress Bar -->
                    <div class="w-full h-1 bg-gray-100">
                        <div id="progress-bar" class="h-full sunflower-bg transition-all duration-300" style="width: 0%"></div>
                    </div>

                    <!-- Slides เนื้อหา -->
                    <!-- สไลด์ 1: หน้าแรก -->
                    <div id="slide-1" class="slide-content active flex-col p-12 justify-center items-center text-center">
                        <div class="sunflower-bg text-white px-4 py-1 rounded-full text-xs font-bold mb-6 tracking-widest uppercase">Strategic CRM Roadmap</div>
                        <h1 class="text-6xl font-kanit font-bold navy-text mb-6">Sun Flower:<br>กลยุทธ์กู้คืนยอดขาย Hypermarket</h1>
                        <p class="text-xl text-gray-500 max-w-2xl Sarabun">การวิเคราะห์พฤติกรรมลูกค้าเชิงลึก และการใช้พลังข้อมูลร่วมกับเครือข่าย Tulip</p>
                        <div class="mt-12 flex gap-12">
                            <div class="text-left border-l-4 border-orange-500 pl-4">
                                <p class="text-[10px] uppercase font-bold text-gray-400 Sarabun">Prepared By</p>
                                <p class="font-kanit font-bold text-sm">CRM Strategy Manager</p>
                            </div>
                            <div class="text-left border-l-4 border-blue-900 pl-4">
                                <p class="text-[10px] uppercase font-bold text-gray-400 Sarabun">Audience</p>
                                <p class="font-kanit font-bold text-sm">CEO & Board Members</p>
                            </div>
                        </div>
                    </div>

                    <!-- สไลด์ 2: สถานการณ์วิกฤต -->
                    <div id="slide-2" class="slide-content flex-col p-12">
                        <div class="flex justify-between items-end mb-8 border-b-2 border-orange-500 pb-2">
                            <h2 class="text-3xl font-kanit font-bold navy-text">1. วิกฤตการณ์: ความถี่การซื้อที่หายไป</h2>
                            <button onclick="goToData('metrics')" class="text-xs text-blue-600 hover:underline font-bold"><i class="fa-solid fa-database mr-1"></i> ดูข้อมูลดิบ</button>
                        </div>
                        <div class="grid grid-cols-2 gap-8 h-full">
                            <div class="space-y-6">
                                <p class="text-sm text-gray-600">พฤติกรรมลูกค้า Hypermarket เปลี่ยนแปลงอย่างชัดเจน:</p>
                                <div class="bg-red-50 p-6 rounded-xl border-l-4 border-red-500">
                                    <h3 class="font-bold text-red-700 text-lg mb-2">Shopping Frequency Drop</h3>
                                    <p class="text-sm">จากมาซื้อของ 12 ครั้ง/ปี ในปี 2015 ลดลงเหลือเพียง <span class="text-xl font-bold">8 ครั้ง/ปี</span> ในปี 2019</p>
                                </div>
                                <div class="bg-gray-50 p-6 rounded-xl border-l-4 border-gray-400">
                                    <h3 class="font-bold text-gray-700 text-lg mb-2">Contribution Shift</h3>
                                    <p class="text-sm">สัดส่วนยอดขาย Hypermarket ลดลงจาก 56% เหลือ 44% ภายใน 4 ปี</p>
                                </div>
                            </div>
                            <div class="flex flex-col items-center justify-center">
                                <div class="w-full max-w-xs space-y-4">
                                    <p class="text-center font-bold text-xs uppercase text-gray-400 mb-2">สัดส่วนรายได้ที่หายไป (Hypermarket)</p>
                                    <div class="relative pt-1">
                                        <div class="flex mb-2 items-center justify-between">
                                            <div class="text-xs font-semibold inline-block py-1 px-2 uppercase rounded-full text-blue-600 bg-blue-200">2015: 56%</div>
                                        </div>
                                        <div class="overflow-hidden h-4 mb-4 text-xs flex rounded bg-blue-100">
                                            <div id="bar-2015" style="width:0%" class="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-blue-900 bar-animate"></div>
                                        </div>
                                        <div class="flex mb-2 items-center justify-between">
                                            <div class="text-xs font-semibold inline-block py-1 px-2 uppercase rounded-full text-red-600 bg-red-200">2019: 44%</div>
                                        </div>
                                        <div class="overflow-hidden h-4 mb-4 text-xs flex rounded bg-red-100">
                                            <div id="bar-2019" style="width:0%" class="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-red-600 bar-animate"></div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- สไลด์ 3: คู่แข่งและการเติบโตของ Orange -->
                    <div id="slide-3" class="slide-content flex-col p-12">
                        <div class="flex justify-between items-end mb-8 border-b-2 border-orange-500 pb-2">
                            <h2 class="text-3xl font-kanit font-bold navy-text">2. คู่แข่ง: การคุกคามของ 'Orange'</h2>
                            <button onclick="goToData('market')" class="text-xs text-blue-600 hover:underline font-bold"><i class="fa-solid fa-database mr-1"></i> ดูข้อมูลดิบ</button>
                        </div>
                        <div class="grid grid-cols-2 gap-12">
                            <div class="space-y-4">
                                <p class="text-sm font-bold text-gray-700">Nationwide Market Share Gap (Hypermarket):</p>
                                <div class="flex items-end gap-4 h-48 pt-8">
                                    <div class="flex-1 flex flex-col items-center">
                                        <div class="bg-blue-900 w-full rounded-t-lg transition-all duration-1000" id="chart-sf-share" style="height:0%"></div>
                                        <p class="text-[10px] mt-2 font-bold uppercase">SF (41%)</p>
                                    </div>
                                    <div class="flex-1 flex flex-col items-center">
                                        <div class="bg-orange-500 w-full rounded-t-lg transition-all duration-1000" id="chart-orange-share" style="height:0%"></div>
                                        <p class="text-[10px] mt-2 font-bold uppercase">Orange (40%)</p>
                                    </div>
                                    <div class="flex-1 flex flex-col items-center">
                                        <div class="bg-gray-400 w-full rounded-t-lg transition-all duration-1000" id="chart-giant-share" style="height:0%"></div>
                                        <p class="text-[10px] mt-2 font-bold uppercase">Giant (19%)</p>
                                    </div>
                                </div>
                            </div>
                            <div class="bg-white p-6 rounded-xl border border-gray-100 shadow-sm">
                                <h3 class="font-bold text-gray-700 mb-4"><i class="fa-solid fa-triangle-exclamation text-orange-500 mr-2"></i> ข้อสังเกตสำคัญ:</h3>
                                <ul class="text-sm space-y-3">
                                    <li class="flex gap-2">
                                        <span class="text-orange-500 font-bold">•</span>
                                        <span>ห่างกันเพียง 1% เท่านั้น ทั่วประเทศ</span>
                                    </li>
                                    <li class="flex gap-2">
                                        <span class="text-orange-500 font-bold">•</span>
                                        <span>ในภูมิภาค Central เราเสียส่วนแบ่งตลาดอย่างหนัก จาก 52% เหลือ 40% ขณะที่ Giant เติบโตขึ้น</span>
                                    </li>
                                    <li class="flex gap-2">
                                        <span class="text-orange-500 font-bold">•</span>
                                        <span>Orange ครองใจกลุ่ม <strong>Young Adult (Index 125)</strong> อย่างเหนียวแน่น</span>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>

                    <!-- สไลด์ 4: กลยุทธ์ผสาน Tulip -->
                    <div id="slide-4" class="slide-content flex-col p-12">
                        <div class="flex justify-between items-end mb-8 border-b-2 border-orange-500 pb-2">
                            <h2 class="text-3xl font-kanit font-bold navy-text">3. ทางรอด: Tulip Synergy Strategy</h2>
                            <button onclick="switchView('data')" class="text-xs text-blue-600 hover:underline font-bold"><i class="fa-solid fa-database mr-1"></i> ดูคลังข้อมูล</button>
                        </div>
                        <div class="grid grid-cols-3 gap-6 mt-4">
                            <div class="bg-white p-6 rounded-xl border border-blue-100 shadow-sm text-center">
                                <div class="w-12 h-12 sunflower-bg rounded-full flex items-center justify-center mx-auto mb-4">
                                    <i class="fa-solid fa-location-dot text-white text-xl"></i>
                                </div>
                                <h4 class="font-bold mb-2">Location-Based</h4>
                                <p class="text-[10px] text-gray-500">ใช้เสาสัญญาณ Tulip ส่ง SMS เฉพาะจุดเมื่อลูกค้า Tulip (25M คน) อยู่ใกล้ Sun Flower</p>
                            </div>
                            <div class="bg-white p-6 rounded-xl border border-blue-100 shadow-sm text-center">
                                <div class="w-12 h-12 sunflower-bg rounded-full flex items-center justify-center mx-auto mb-4">
                                    <i class="fa-solid fa-users-viewfinder text-white text-xl"></i>
                                </div>
                                <h4 class="font-bold mb-2">Look-alike Segment</h4>
                                <p class="text-[10px] text-gray-500">ดึงลูกค้าพรีเมียมจาก Tulip ที่ยังไม่ช้อปกับเราผ่านข้อเสนอพิเศษ Cross-Category</p>
                            </div>
                            <div class="bg-white p-6 rounded-xl border border-blue-100 shadow-sm text-center">
                                <div class="w-12 h-12 sunflower-bg rounded-full flex items-center justify-center mx-auto mb-4">
                                    <i class="fa-solid fa-mobile-screen-button text-white text-xl"></i>
                                </div>
                                <h4 class="font-bold mb-2">App Integration</h4>
                                <p class="text-[10px] text-gray-500">สะสมและใช้คะแนนข้ามเครือข่าย เพื่อเพิ่ม Engagement ในแอป Sun Flower Card</p>
                            </div>
                        </div>
                        <div class="mt-8 p-4 bg-blue-900 text-white rounded-lg flex items-center justify-between">
                            <div class="text-sm">
                                <span class="font-bold text-orange-400">Next Action:</span> มุ่งเป้าดึงกลุ่ม Young Family (Index 120) กลับมาซื้ออาหารสด (Fresh Food)
                            </div>
                            <i class="fa-solid fa-arrow-right-long animate-bounce-x"></i>
                        </div>
                    </div>

                    <!-- แถบนำทางสไลด์ -->
                    <div class="absolute bottom-6 right-6 flex gap-3">
                        <button onclick="changeSlide(-1)" class="w-10 h-10 rounded-full border border-gray-200 flex items-center justify-center hover:bg-gray-50 transition-all shadow-sm">
                            <i class="fa-solid fa-chevron-left text-gray-400"></i>
                        </button>
                        <button onclick="changeSlide(1)" class="w-10 h-10 rounded-full border border-gray-200 flex items-center justify-center hover:bg-gray-50 transition-all shadow-sm">
                            <i class="fa-solid fa-chevron-right navy-text"></i>
                        </button>
                    </div>
                    
                    <div class="absolute bottom-6 left-6 text-[10px] text-gray-400 flex items-center gap-2 font-bold Sarabun">
                        <span id="slide-indicator">สไลด์ 1 จาก 4</span>
                        <span class="w-1 h-1 bg-gray-300 rounded-full"></span>
                        <span class="uppercase">Confidential: Board Strategy</span>
                    </div>
                </div>
            </div>

        </section>
    </main>

    <!-- แถบแสดงสถานะด้านล่าง -->
    <footer class="bg-white border-t border-gray-200 px-6 py-2 flex justify-between items-center text-[10px] text-gray-500 font-bold uppercase tracking-widest Sarabun">
        <div class="flex gap-6">
            <span class="flex items-center gap-1"><i class="fa-solid fa-circle text-[6px] text-green-500"></i> Data Analysis Connected</span>
            <span class="flex items-center gap-1"><i class="fa-solid fa-lock"></i> Restricted Internal Use</span>
        </div>
        <div class="flex gap-4">
            <span>Market Share: 41%</span>
            <span>Frequency: 8/Yr</span>
        </div>
    </footer>

    <script>
        // การจัดการสถานะ
        let currentView = 'data'; 
        let currentSlideIndex = 1;
        const totalSlides = 4;

        // ฟังก์ชันสลับมุมมองระหว่างข้อมูลและพรีเซนต์
        function switchView(view) {
            currentView = view;
            const dataSidebar = document.getElementById('data-sidebar');
            const dataContent = document.getElementById('data-content-wrapper');
            const presentationContent = document.getElementById('presentation-content-wrapper');
            
            const btnData = document.getElementById('btn-view-data');
            const btnPres = document.getElementById('btn-view-presentation');

            if (view === 'data') {
                dataSidebar.classList.remove('hidden');
                dataContent.classList.remove('hidden');
                presentationContent.classList.add('hidden');
                
                btnData.classList.add('bg-white/30');
                btnPres.classList.remove('bg-orange-600');
                btnPres.classList.add('sunflower-bg');
            } else {
                dataSidebar.classList.add('hidden');
                dataContent.classList.add('hidden');
                presentationContent.classList.remove('hidden');
                
                btnData.classList.remove('bg-white/30');
                btnPres.classList.add('bg-orange-600');
                
                // เริ่มอนิเมชั่นกราฟในสไลด์ถ้าเปลี่ยนมาหน้าพรีเซนต์
                triggerSlideAnimations();
            }
        }

        // ฟังก์ชันนำทางใน Sidebar หน้าข้อมูลดิบ
        function showDataSection(event, sectionId) {
            if (event) event.preventDefault();

            const links = document.querySelectorAll('.sidebar-link');
            links.forEach(link => {
                link.classList.remove('active', 'bg-blue-900', 'text-white');
                link.classList.add('text-gray-600');
            });
            
            if (event && event.currentTarget) {
                event.currentTarget.classList.add('active');
            }

            const sections = document.querySelectorAll('.data-section');
            sections.forEach(sec => sec.classList.add('hidden'));
            
            const targetSection = document.getElementById(`data-${sectionId}`);
            if (targetSection) {
                targetSection.classList.remove('hidden');
            }
        }

        // ฟังก์ชันลิงก์จากสไลด์พรีเซนต์ไปหาหน้าข้อมูลดิบเฉพาะส่วน
        function goToData(sectionId) {
            switchView('data');
            const link = document.getElementById(`link-${sectionId}`);
            if (link) {
                link.click();
            }
        }

        // การนำทางสไลด์
        function changeSlide(direction) {
            const nextSlide = currentSlideIndex + direction;
            if (nextSlide >= 1 && nextSlide <= totalSlides) {
                document.getElementById(`slide-${currentSlideIndex}`).classList.remove('active');
                currentSlideIndex = nextSlide;
                document.getElementById(`slide-${currentSlideIndex}`).classList.add('active', 'flex');
                updateSlideUI();
                triggerSlideAnimations();
            }
        }

        function updateSlideUI() {
            document.getElementById('slide-indicator').innerText = `สไลด์ ${currentSlideIndex} จาก ${totalSlides}`;
            const progress = ((currentSlideIndex - 1) / (totalSlides - 1)) * 100;
            document.getElementById('progress-bar').style.width = `${progress}%`;
        }

        // อนิเมชั่นกราฟในสไลด์
        function triggerSlideAnimations() {
            if (currentSlideIndex === 2) {
                setTimeout(() => {
                    document.getElementById('bar-2015').style.width = '56%';
                    document.getElementById('bar-2019').style.width = '44%';
                }, 100);
            } else if (currentSlideIndex === 3) {
                setTimeout(() => {
                    document.getElementById('chart-sf-share').style.height = '82%'; // Scaling based on 41
                    document.getElementById('chart-orange-share').style.height = '80%'; // Scaling based on 40
                    document.getElementById('chart-giant-share').style.height = '38%'; // Scaling based on 19
                }, 100);
            }
        }

        window.onload = () => {
            switchView('data');
            updateSlideUI();
        };

        // การควบคุมด้วยคีย์บอร์ด
        document.addEventListener('keydown', (e) => {
            if (currentView === 'presentation') {
                if (e.key === 'ArrowRight') changeSlide(1);
                if (e.key === 'ArrowLeft') changeSlide(-1);
            }
        });
    </script>
</body>
</html>
