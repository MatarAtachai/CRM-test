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
    </style>
</head>
<body class="h-screen overflow-hidden flex flex-col">

    <!-- Header / Top Navigation -->
    <header class="navy-bg text-white p-4 flex justify-between items-center shadow-lg z-50">
        <div class="flex items-center gap-3">
            <div class="w-10 h-10 sunflower-bg rounded-full flex items-center justify-center">
                <i class="fa-solid fa-sun text-white text-xl"></i>
            </div>
            <div>
                <h1 class="text-xl font-bold leading-none">SUN FLOWER</h1>
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
        
        <!-- DATA VIEW SIDEBAR -->
        <aside id="data-sidebar" class="w-64 bg-white border-r border-gray-200 overflow-y-auto hidden">
            <div class="p-6">
                <h3 class="font-kanit font-bold text-gray-500 uppercase text-xs tracking-wider mb-4">หมวดหมู่ข้อมูล</h3>
                <nav class="space-y-1">
                    <a href="#" onclick="showDataSection(event, 'stores')" class="sidebar-link active block p-3 rounded-lg text-sm transition-all flex items-center gap-3">
                        <i class="fa-solid fa-store"></i> จำนวนสาขา
                    </a>
                    <a href="#" onclick="showDataSection(event, 'sales')" class="sidebar-link block p-3 rounded-lg text-sm text-gray-600 hover:bg-gray-50 flex items-center gap-3">
                        <i class="fa-solid fa-chart-pie"></i> สัดส่วนยอดขาย
                    </a>
                    <a href="#" onclick="showDataSection(event, 'loyalty')" class="sidebar-link block p-3 rounded-lg text-sm text-gray-600 hover:bg-gray-50 flex items-center gap-3">
                        <i class="fa-solid fa-id-card"></i> พฤติกรรมสมาชิก
                    </a>
                    <a href="#" onclick="showDataSection(event, 'competition')" class="sidebar-link block p-3 rounded-lg text-sm text-gray-600 hover:bg-gray-50 flex items-center gap-3">
                        <i class="fa-solid fa-users-rays"></i> คู่แข่งและการเติบโต
                    </a>
                </nav>
            </div>
        </aside>

        <!-- MAIN CONTENT AREA -->
        <section id="content-container" class="flex-grow overflow-y-auto p-8 bg-gray-50">
            
            <!-- DATA CONTENT (Visible by default in 'data' mode) -->
            <div id="data-content-wrapper" class="hidden animate-fade">
                <div id="data-stores" class="data-section">
                    <h2 class="text-3xl font-kanit font-bold navy-text mb-6">ข้อมูลจำนวนสาขา (Number of Stores)</h2>
                    <div class="bg-white rounded-xl shadow-sm border border-gray-200 overflow-hidden">
                        <table class="w-full text-left">
                            <thead class="bg-gray-50 border-b border-gray-200">
                                <tr>
                                    <th class="p-4 font-kanit">ประเภทสาขา</th>
                                    <th class="p-4">2015</th>
                                    <th class="p-4">2016</th>
                                    <th class="p-4">2017</th>
                                    <th class="p-4">2018</th>
                                    <th class="p-4">2019</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-gray-100">
                                <tr><td class="p-4 font-bold">Hypermarket</td><td class="p-4">195</td><td class="p-4">200</td><td class="p-4">207</td><td class="p-4">213</td><td class="p-4 font-bold text-blue-600">220</td></tr>
                                <tr><td class="p-4 font-bold">Supermarket</td><td class="p-4">97</td><td class="p-4">102</td><td class="p-4">106</td><td class="p-4">110</td><td class="p-4">112</td></tr>
                                <tr><td class="p-4 font-bold">Convenience Stores</td><td class="p-4">450</td><td class="p-4">460</td><td class="p-4">470</td><td class="p-4">485</td><td class="p-4">500</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <div id="data-sales" class="data-section hidden">
                    <h2 class="text-3xl font-kanit font-bold navy-text mb-6">สัดส่วนยอดขาย (Sales Contribution)</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="bg-white p-6 rounded-xl shadow-sm border border-gray-200">
                            <h3 class="font-bold mb-4">Sun Flower: ยอดขายแยกตามสาขา (%)</h3>
                            <div class="space-y-4">
                                <div>
                                    <div class="flex justify-between text-sm mb-1"><span>Hypermarket</span><span class="font-bold text-red-500">44% (ลดจาก 56%)</span></div>
                                    <div class="w-full bg-gray-100 h-2 rounded-full overflow-hidden"><div class="bg-blue-900 h-full" style="width: 44%"></div></div>
                                </div>
                                <div>
                                    <div class="flex justify-between text-sm mb-1"><span>Convenience Stores</span><span class="font-bold">27%</span></div>
                                    <div class="w-full bg-gray-100 h-2 rounded-full overflow-hidden"><div class="bg-orange-500 h-full" style="width: 27%"></div></div>
                                </div>
                                <div>
                                    <div class="flex justify-between text-sm mb-1"><span>Supermarket</span><span class="font-bold">23%</span></div>
                                    <div class="w-full bg-gray-100 h-2 rounded-full overflow-hidden"><div class="bg-slate-500 h-full" style="width: 23%"></div></div>
                                </div>
                                <div>
                                    <div class="flex justify-between text-sm mb-1"><span>Online</span><span class="font-bold text-green-500">6% (โตจาก 1%)</span></div>
                                    <div class="w-full bg-gray-100 h-2 rounded-full overflow-hidden"><div class="bg-green-500 h-full" style="width: 6%"></div></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div id="data-loyalty" class="data-section hidden">
                    <h2 class="text-3xl font-kanit font-bold navy-text mb-6">พฤติกรรมสมาชิก (Loyalty Data)</h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="bg-white p-6 rounded-xl shadow-sm border border-gray-200">
                            <h3 class="font-bold mb-4">สถานะความภักดี (2019)</h3>
                            <div class="space-y-4">
                                <div>
                                    <div class="flex justify-between text-sm mb-1"><span>High Loyalty</span><span class="font-bold text-red-500">26% (ลดจาก 30%)</span></div>
                                    <div class="w-full bg-gray-100 h-2 rounded-full overflow-hidden"><div class="bg-blue-800 h-full" style="width: 26%"></div></div>
                                </div>
                                <div>
                                    <div class="flex justify-between text-sm mb-1"><span>Mid-Tier Loyalty</span><span class="font-bold">37%</span></div>
                                    <div class="w-full bg-gray-100 h-2 rounded-full overflow-hidden"><div class="bg-blue-500 h-full" style="width: 37%"></div></div>
                                </div>
                                <div>
                                    <div class="flex justify-between text-sm mb-1"><span>Low Loyalty</span><span class="font-bold">37%</span></div>
                                    <div class="w-full bg-gray-100 h-2 rounded-full overflow-hidden"><div class="bg-gray-400 h-full" style="width: 37%"></div></div>
                                </div>
                            </div>
                        </div>
                        <div class="bg-white p-6 rounded-xl shadow-sm border border-gray-200">
                            <h3 class="font-bold mb-4">ความถี่ในการมาใช้บริการ (Frequency)</h3>
                            <div class="flex items-center gap-6 h-full justify-center">
                                <div class="text-center">
                                    <p class="text-xs font-bold text-gray-400 uppercase">ปี 2015</p>
                                    <p class="text-5xl font-bold navy-text">12</p>
                                    <p class="text-xs">ครั้ง/ปี</p>
                                </div>
                                <i class="fa-solid fa-arrow-right text-gray-300 text-2xl"></i>
                                <div class="text-center">
                                    <p class="text-xs font-bold text-orange-500 uppercase">ปี 2019</p>
                                    <p class="text-5xl font-bold text-orange-500">9</p>
                                    <p class="text-xs">ครั้ง/ปี</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div id="data-competition" class="data-section hidden">
                    <h2 class="text-3xl font-kanit font-bold navy-text mb-6">คู่แข่งและการเติบโต (Competition)</h2>
                    <div class="bg-white rounded-xl shadow-sm border border-gray-200 overflow-hidden mb-6">
                        <table class="w-full text-left">
                            <thead class="bg-gray-50 border-b border-gray-200">
                                <tr>
                                    <th class="p-4 font-kanit">Market Share</th>
                                    <th class="p-4">Nationwide</th>
                                    <th class="p-4">Central Region</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-gray-100">
                                <tr><td class="p-4 font-bold text-blue-900">Sun Flower</td><td class="p-4">41%</td><td class="p-4">47%</td></tr>
                                <tr><td class="p-4 font-bold text-orange-600">Orange (Competitor)</td><td class="p-4">40%</td><td class="p-4">35%</td></tr>
                            </tbody>
                        </table>
                    </div>
                    <div class="bg-orange-50 border border-orange-200 p-4 rounded-lg">
                        <p class="text-sm text-orange-800 italic"><strong>Insight:</strong> ในเขตภาคกลาง คู่แข่ง Orange กำลังเติบโตอย่างรวดเร็วและไล่จี้เราอย่างน่ากังวล โดยช่องว่าง Market Share ทั่วประเทศเหลือเพียง 1% เท่านั้น</p>
                    </div>
                </div>
            </div>

            <!-- PRESENTATION VIEW -->
            <div id="presentation-content-wrapper" class="h-full flex flex-col items-center justify-center animate-fade">
                <div class="w-full max-w-5xl bg-white aspect-[16/9] shadow-2xl rounded-2xl overflow-hidden relative flex flex-col border border-gray-200">
                    
                    <!-- Progress Bar -->
                    <div class="w-full h-1 bg-gray-100">
                        <div id="progress-bar" class="h-full sunflower-bg transition-all duration-300" style="width: 0%"></div>
                    </div>

                    <!-- Slides -->
                    <div id="slide-1" class="slide-content active flex-col p-12 justify-center items-center text-center">
                        <div class="bg-orange-100 text-orange-600 px-4 py-1 rounded-full text-sm font-bold mb-6">STRATEGIC PROPOSAL 2025</div>
                        <h1 class="text-6xl font-kanit font-bold navy-text mb-6">พลิกฟื้น Sun Flower<br>ด้วยพลังแห่ง CRM</h1>
                        <p class="text-xl text-gray-500 max-w-2xl">แผนงานเจาะลึกการกู้คืนลูกค้ากลุ่ม Hypermarket และการผสานข้อมูลกับเครือข่าย Tulip</p>
                        <div class="mt-12 flex gap-4">
                            <div class="text-left border-l-4 border-orange-500 pl-4">
                                <p class="text-xs uppercase font-bold text-gray-400">ผู้นำเสนอ</p>
                                <p class="font-kanit font-bold">Candidate: Senior CRM</p>
                            </div>
                            <div class="text-left border-l-4 border-blue-900 pl-4">
                                <p class="text-xs uppercase font-bold text-gray-400">เป้าหมาย</p>
                                <p class="font-kanit font-bold">CEO & Board Directors</p>
                            </div>
                        </div>
                    </div>

                    <div id="slide-2" class="slide-content flex-col p-12">
                        <h2 class="text-3xl font-kanit font-bold navy-text border-b-2 border-orange-500 pb-2 mb-8">Executive Summary: แผลใหญ่ที่เราต้องรีบรักษา</h2>
                        <div class="grid grid-cols-2 gap-8 h-full">
                            <div class="space-y-6">
                                <div class="bg-red-50 p-6 rounded-xl border-l-4 border-red-500">
                                    <h3 class="font-bold text-red-700 mb-2"><i class="fa-solid fa-circle-exclamation mr-2"></i> วิกฤต Hypermarket</h3>
                                    <p class="text-sm">ยอดขายหดตัวต่อเนื่อง ความถี่การซื้อลดลงจาก 12 ครั้ง เหลือ 9 ครั้งต่อปี เสี่ยงต่อการโดน Orange แย่งส่วนแบ่งตลาดที่ห่างกันเพียง 1%</p>
                                </div>
                                <div class="bg-green-50 p-6 rounded-xl border-l-4 border-green-500">
                                    <h3 class="font-bold text-green-700 mb-2"><i class="fa-solid fa-lightbulb mr-2"></i> ทางออกเชิงกลยุทธ์</h3>
                                    <p class="text-sm">ใช้ฐานลูกค้าสมาชิก 80% ผสานกับ Big Data ของ Tulip (25 ล้านคน) เพื่อทำ Hyper-Personalization กู้คืนความถี่การซื้อให้กลับมา</p>
                                </div>
                            </div>
                            <div class="flex items-center justify-center">
                                <div class="text-center">
                                    <div class="text-7xl font-bold text-blue-900">44%</div>
                                    <p class="text-sm text-gray-400 font-bold">สัดส่วนยอดขาย Hypermarket ในปัจจุบัน<br>(ลดลงจาก 56% ในปี 2015)</p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 3: Tulip Synergy (The "Unfair Advantage") -->
                    <div id="slide-3" class="slide-content flex-col p-12">
                        <h2 class="text-3xl font-kanit font-bold navy-text border-b-2 border-orange-500 pb-2 mb-8">ความได้เปรียบ: พลังแห่งเครือข่าย Tulip</h2>
                        <div class="grid grid-cols-3 gap-6">
                            <div class="bg-white p-6 rounded-xl border shadow-sm text-center">
                                <i class="fa-solid fa-map-location-dot text-4xl sunflower-orange mb-4"></i>
                                <h4 class="font-bold mb-2">Geo-Marketing</h4>
                                <p class="text-xs text-gray-500">ส่งข้อเสนอเมื่อลูกค้า Tulip อยู่ใกล้รัศมี Hypermarket ของเรา</p>
                            </div>
                            <div class="bg-white p-6 rounded-xl border shadow-sm text-center">
                                <i class="fa-solid fa-user-gear text-4xl sunflower-orange mb-4"></i>
                                <h4 class="font-bold mb-2">Single ID Profile</h4>
                                <p class="text-xs text-gray-500">เชื่อมโยงข้อมูลไลฟ์สไตล์การโทรและการช้อปเป็นหนึ่งเดียว</p>
                            </div>
                            <div class="bg-white p-6 rounded-xl border shadow-sm text-center">
                                <i class="fa-solid fa-gift text-4xl sunflower-orange mb-4"></i>
                                <h4 class="font-bold mb-2">Cross-Rewards</h4>
                                <p class="text-xs text-gray-500">แลกคะแนนข้ามค่ายเพื่อเพิ่มความผูกพัน (Tulip Points → SF Discounts)</p>
                            </div>
                        </div>
                        <div class="mt-8 p-6 bg-slate-900 text-white rounded-xl">
                            <p class="italic text-center text-sm">"เราไม่ได้แค่ขายของ แต่เราอยู่ในทุกจังหวะชีวิตของลูกค้าผ่านเครือข่ายมือถือและร้านค้าใกล้บ้าน"</p>
                        </div>
                    </div>

                    <!-- Slide 4: Roadmap -->
                    <div id="slide-4" class="slide-content flex-col p-12">
                        <h2 class="text-3xl font-kanit font-bold navy-text border-b-2 border-orange-500 pb-2 mb-8">Implementation: แผนการดำเนินงาน 12 เดือน</h2>
                        <div class="relative py-8">
                            <div class="absolute top-1/2 left-0 right-0 h-1 bg-gray-100 -translate-y-1/2"></div>
                            <div class="flex justify-between relative z-10">
                                <div class="w-1/4 text-center">
                                    <div class="w-10 h-10 navy-bg text-white rounded-full flex items-center justify-center mx-auto mb-4 border-4 border-white shadow">1</div>
                                    <h4 class="font-bold text-xs">Q1: Data Sync</h4>
                                    <p class="text-[10px] text-gray-400">เชื่อมฐานข้อมูล SF Card และ Tulip</p>
                                </div>
                                <div class="w-1/4 text-center">
                                    <div class="w-10 h-10 sunflower-bg text-white rounded-full flex items-center justify-center mx-auto mb-4 border-4 border-white shadow">2</div>
                                    <h4 class="font-bold text-xs">Q2: Pilot</h4>
                                    <p class="text-[10px] text-gray-400">เริ่มทดลอง Geo-fencing ในภาคกลาง</p>
                                </div>
                                <div class="w-1/4 text-center">
                                    <div class="w-10 h-10 sunflower-bg text-white rounded-full flex items-center justify-center mx-auto mb-4 border-4 border-white shadow">3</div>
                                    <h4 class="font-bold text-xs">Q3: Scale Up</h4>
                                    <p class="text-[10px] text-gray-400">ขยายผล AI Personalized Offer ทั่วประเทศ</p>
                                </div>
                                <div class="w-1/4 text-center">
                                    <div class="w-10 h-10 navy-bg text-white rounded-full flex items-center justify-center mx-auto mb-4 border-4 border-white shadow">4</div>
                                    <h4 class="font-bold text-xs">Q4: Review</h4>
                                    <p class="text-[10px] text-gray-400">วัดผล ROI และกู้คืน Churn Rate</p>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Slide Navigation -->
                    <div class="absolute bottom-6 right-6 flex gap-3">
                        <button onclick="changeSlide(-1)" class="w-12 h-12 rounded-full border border-gray-200 flex items-center justify-center hover:bg-gray-50 transition-all shadow-sm">
                            <i class="fa-solid fa-chevron-left text-gray-400"></i>
                        </button>
                        <button onclick="changeSlide(1)" class="w-12 h-12 rounded-full border border-gray-200 flex items-center justify-center hover:bg-gray-50 transition-all shadow-sm">
                            <i class="fa-solid fa-chevron-right navy-text"></i>
                        </button>
                    </div>
                    
                    <div class="absolute bottom-6 left-6 text-[10px] text-gray-400 flex items-center gap-2">
                        <span id="slide-indicator">Slide 1 of 4</span>
                        <span class="w-1 h-1 bg-gray-300 rounded-full"></span>
                        <span>Sun Flower x Tulip Group</span>
                    </div>
                </div>
            </div>

        </section>
    </main>

    <!-- Footer Stats / Status Bar -->
    <footer class="bg-white border-t border-gray-200 px-6 py-2 flex justify-between items-center text-[10px] text-gray-500 font-bold uppercase tracking-widest">
        <div class="flex gap-6">
            <span class="flex items-center gap-1"><i class="fa-solid fa-circle text-[6px] text-green-500"></i> Data Synced</span>
            <span class="flex items-center gap-1"><i class="fa-solid fa-lock"></i> Confidential</span>
        </div>
        <div>&copy; 2025 Sun Flower Strategic CRM Proposal</div>
    </footer>

    <script>
        // State Management
        let currentView = 'data'; // 'data' or 'presentation'
        let currentSlideIndex = 1;
        const totalSlides = 4;

        // View Switching Logic
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
            }
        }

        // Sidebar Navigation Logic
        function showDataSection(event, sectionId) {
            if (event) event.preventDefault();

            // Update UI Links
            const links = document.querySelectorAll('.sidebar-link');
            links.forEach(link => {
                link.classList.remove('active', 'bg-blue-900', 'text-white');
                link.classList.add('text-gray-600');
            });
            
            // Add active class to current target safely
            if (event && event.currentTarget) {
                event.currentTarget.classList.add('active');
            }

            // Show Section
            const sections = document.querySelectorAll('.data-section');
            sections.forEach(sec => sec.classList.add('hidden'));
            
            const targetSection = document.getElementById(`data-${sectionId}`);
            if (targetSection) {
                targetSection.classList.remove('hidden');
            }
        }

        // Slide Navigation Logic
        function changeSlide(direction) {
            const nextSlide = currentSlideIndex + direction;
            if (nextSlide >= 1 && nextSlide <= totalSlides) {
                document.getElementById(`slide-${currentSlideIndex}`).classList.remove('active');
                currentSlideIndex = nextSlide;
                document.getElementById(`slide-${currentSlideIndex}`).classList.add('active', 'flex');
                updateSlideUI();
            }
        }

        function updateSlideUI() {
            document.getElementById('slide-indicator').innerText = `Slide ${currentSlideIndex} of ${totalSlides}`;
            const progress = ((currentSlideIndex - 1) / (totalSlides - 1)) * 100;
            document.getElementById('progress-bar').style.width = `${progress}%`;
        }

        // Initialize with Data View
        window.onload = () => {
            switchView('data');
            updateSlideUI();
        };

        // Keyboard Navigation
        document.addEventListener('keydown', (e) => {
            if (currentView === 'presentation') {
                if (e.key === 'ArrowRight') changeSlide(1);
                if (e.key === 'ArrowLeft') changeSlide(-1);
            }
        });
    </script>
</body>
</html>
