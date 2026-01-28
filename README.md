import React, { useState } from 'react';
import { 
  BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer, 
  Cell, PieChart, Pie
} from 'recharts';
import { 
  Database, Presentation, ChevronRight, ChevronLeft, 
  BarChart3, Users, Map, Target, TrendingDown, Info,
  Smartphone, MapPin, Zap, ShoppingBag, AlertTriangle
} from 'lucide-react';

const App = () => {
  const [view, setView] = useState('presentation'); // 'presentation' or 'data'
  const [currentSlide, setCurrentSlide] = useState(1);
  const totalSlides = 6;

  // --- Data Sections ---
  const salesContributionData = [
    { name: 'Hypermarket', '2015': 56, '2019': 44 },
    { name: 'Supermarket', '2015': 19, '2019': 23 },
    { name: 'Convenience', '2015': 24, '2019': 27 },
    { name: 'Online', '2015': 1, '2019': 6 },
  ];

  const marketShareCentral = [
    { name: 'Giant (เจ้าตลาด)', value: 51, color: '#94A3B8' },
    { name: 'Sun Flower', value: 40, color: '#003366' },
    { name: 'Orange (คู่แข่ง)', value: 9, color: '#E67E22' },
  ];

  const shopperIndexData = [
    { segment: 'Family with Kids', SF: 120, Orange: 90 },
    { segment: 'Young Adult (20-39)', SF: 77, Orange: 125 },
    { segment: 'AB (High Income)', SF: 110, Orange: 92 },
  ];

  // --- Navigation Logic ---
  const nextSlide = () => setCurrentSlide(prev => Math.min(prev + 1, totalSlides));
  const prevSlide = () => setCurrentSlide(prev => Math.max(prev - 1, 1));

  return (
    <div className="flex flex-col h-screen bg-[#F8FAFC] text-slate-900 overflow-hidden Sarabun">
      {/* Header Navigation */}
      <header className="bg-[#003366] text-white px-8 py-3 flex justify-between items-center z-50 shadow-lg">
        <div className="flex items-center gap-3">
          <div className="w-10 h-10 bg-[#E67E22] rounded-full flex items-center justify-center shadow-md">
            <BarChart3 size={20} />
          </div>
          <div>
            <h1 className="font-bold text-lg leading-none uppercase tracking-tight Kanit">Sun Flower CRM Strategy</h1>
            <p className="text-[10px] text-orange-400 font-bold uppercase tracking-widest Sarabun opacity-80">Board Confidential</p>
          </div>
        </div>
        <div className="flex gap-3">
          <button 
            onClick={() => setView('data')}
            className={`px-4 py-1.5 text-xs font-bold rounded-lg border transition-all flex items-center gap-2 ${view === 'data' ? 'bg-white text-[#003366]' : 'bg-white/10 border-white/20 hover:bg-white/20'}`}
          >
            <Database size={14} /> ข้อมูลดิบ
          </button>
          <button 
            onClick={() => setView('presentation')}
            className={`px-5 py-1.5 text-xs font-bold rounded-lg transition-all flex items-center gap-2 shadow-md ${view === 'presentation' ? 'bg-[#E67E22] text-white' : 'bg-white/10 border-white/20 hover:bg-white/20'}`}
          >
            <Presentation size={14} /> เริ่มนำเสนอ
          </button>
        </div>
      </header>

      {/* Main Workspace */}
      <main className="flex-grow relative overflow-hidden flex flex-col">
        
        {/* VIEW: DATA DASHBOARD */}
        {view === 'data' && (
          <div className="flex h-full animate-in fade-in duration-500 overflow-hidden">
            <aside className="w-64 bg-white border-r border-slate-200 p-6 flex flex-col gap-8 shadow-sm">
                <div>
                    <p className="text-[10px] font-bold text-slate-400 uppercase tracking-widest mb-4">Master Database</p>
                    <nav className="space-y-1">
                        <button className="w-full text-left p-3 rounded-xl bg-slate-50 text-[#003366] font-bold text-xs flex items-center gap-3 border-l-4 border-[#E67E22]"><ShoppingBag size={14}/> Sales Performance</button>
                        <button className="w-full text-left p-3 rounded-xl text-slate-500 font-medium text-xs flex items-center gap-3 hover:bg-slate-50 transition-colors"><Users size={14}/> Shopper Index</button>
                        <button className="w-full text-left p-3 rounded-xl text-slate-500 font-medium text-xs flex items-center gap-3 hover:bg-slate-50 transition-colors"><Map size={14}/> Regional Share</button>
                    </nav>
                </div>
            </aside>
            <div className="flex-grow p-8 overflow-y-auto bg-[#F1F5F9]">
                <div className="max-w-5xl mx-auto space-y-8">
                    <h2 className="text-2xl font-bold text-[#003366] Kanit mb-6">Database Insight Explorer</h2>
                    <div className="grid grid-cols-2 gap-6">
                        <div className="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm">
                            <h3 className="text-xs font-bold text-slate-400 mb-6 uppercase tracking-wider Sarabun">Store Contribution Trend (%)</h3>
                            <ResponsiveContainer width="100%" height={300}>
                                <BarChart data={salesContributionData}>
                                    <CartesianGrid strokeDasharray="3 3" vertical={false} stroke="#F1F5F9" />
                                    <XAxis dataKey="name" fontSize={11} axisLine={false} tickLine={false} />
                                    <YAxis fontSize={11} axisLine={false} tickLine={false} />
                                    <Tooltip contentStyle={{ borderRadius: '12px', border: 'none', boxShadow: '0 10px 15px -3px rgba(0,0,0,0.1)' }} />
                                    <Bar dataKey="2015" fill="#CBD5E1" radius={[4, 4, 0, 0]} />
                                    <Bar dataKey="2019" fill="#003366" radius={[4, 4, 0, 0]} />
                                </BarChart>
                            </ResponsiveContainer>
                        </div>
                        <div className="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm flex flex-col justify-center">
                            <h3 className="text-xs font-bold text-slate-400 mb-8 uppercase tracking-wider Sarabun">Key Growth Indicators</h3>
                            <div className="space-y-6">
                                <div className="flex justify-between items-center p-4 bg-red-50 rounded-2xl border border-red-100">
                                    <span className="text-sm font-bold text-red-800 Sarabun">Hypermarket Freq.</span>
                                    <span className="text-xl font-bold text-red-600">8 / ปี</span>
                                </div>
                                <div className="flex justify-between items-center p-4 bg-blue-50 rounded-2xl border border-blue-100">
                                    <span className="text-sm font-bold text-blue-800 Sarabun">Online Basket Size</span>
                                    <span className="text-xl font-bold text-blue-600">1,100 THB</span>
                                </div>
                                <div className="flex justify-between items-center p-4 bg-orange-50 rounded-2xl border border-orange-100">
                                    <span className="text-sm font-bold text-orange-800 Sarabun">Central Share Gap</span>
                                    <span className="text-xl font-bold text-orange-600">-11% vs Giant</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
          </div>
        )}

        {/* VIEW: PRESENTATION SLIDES */}
        {view === 'presentation' && (
          <div className="h-full flex flex-col p-6 items-center justify-center">
            <div className="w-full max-w-6xl aspect-[16/9] bg-white rounded-[2rem] shadow-2xl border border-slate-200 overflow-hidden relative flex flex-col">
                
                {/* Slide Content Area */}
                <div className="flex-grow p-10 flex flex-col relative overflow-hidden">
                    
                    {/* Slide 1: Welcome */}
                    {currentSlide === 1 && (
                      <div className="h-full flex flex-col items-center justify-center text-center animate-in fade-in zoom-in duration-700">
                        <div className="bg-[#E67E22] text-white px-5 py-1 rounded-full text-[10px] font-bold mb-8 tracking-[0.3em] uppercase shadow-md Sarabun">Strategic CRM Presentation</div>
                        <h1 className="text-5xl lg:text-7xl font-bold text-[#003366] mb-8 leading-tight Kanit">กู้ชีพ Sun Flower:<br/><span className="text-[#E67E22]">CRM Strategy 2025</span></h1>
                        <p className="text-lg text-slate-400 Sarabun max-w-2xl mx-auto leading-relaxed italic">"กอบกู้ยอดขาย Hypermarket ด้วยพลัง Synergy ข้ามขีดจำกัด"</p>
                        <div className="mt-12 flex gap-12 border-t border-slate-100 pt-10">
                            <div className="text-left border-l-4 border-[#E67E22] pl-4">
                                <p className="text-[10px] font-bold text-slate-400 uppercase tracking-widest Sarabun">Target Audience</p>
                                <p className="text-sm font-bold text-[#003366] Kanit">CEO & Board Directors</p>
                            </div>
                            <div className="text-left border-l-4 border-[#003366] pl-4">
                                <p className="text-[10px] font-bold text-slate-400 uppercase tracking-widest Sarabun">Focus Area</p>
                                <p className="text-sm font-bold text-[#003366] Kanit">Hypermarket Revival</p>
                            </div>
                        </div>
                      </div>
                    )}

                    {/* Slide 2: Diagnosis - Performance (HR Step 1) */}
                    {currentSlide === 2 && (
                      <div className="h-full flex flex-col animate-in slide-in-from-right duration-500">
                        <div className="flex justify-between items-end mb-8 border-b pb-4 border-slate-100">
                            <h2 className="text-3xl font-bold text-[#003366] Kanit flex items-center gap-4"><TrendingDown className="text-red-500" size={32}/> 1. วินิจฉัย: เมื่อรายได้หลักกำลังหายไป</h2>
                            <button onClick={() => setView('data')} className="text-xs font-bold text-blue-600 hover:underline transition-all flex items-center gap-1"><Info size={12}/> ข้อมูลสนับสนุน</button>
                        </div>
                        <div className="grid grid-cols-2 gap-10 flex-grow">
                            <div className="flex flex-col justify-center space-y-6">
                                <div className="p-6 bg-red-50 rounded-2xl border border-red-100">
                                    <h3 className="text-red-700 font-bold text-xl mb-1 Sarabun italic">Frequency Crisis</h3>
                                    <p className="text-sm text-slate-600">ลูกค้ามาซื้อของลดลงจาก 12 ครั้ง เหลือ <span className="text-red-600 font-black text-2xl">8 ครั้ง / ปี</span></p>
                                </div>
                                <div className="p-6 bg-orange-50 rounded-2xl border border-orange-100">
                                    <h3 className="text-orange-700 font-bold text-xl mb-1 Sarabun italic">The Churning Gap</h3>
                                    <p className="text-sm text-slate-600 font-medium">ยอดขาย Hypermarket ติดลบ <span className="text-orange-600 font-black text-2xl">-3%</span> สวนทางกับตลาด</p>
                                </div>
                            </div>
                            <div className="bg-white p-6 rounded-2xl shadow-lg border border-slate-50 flex flex-col justify-center">
                                <h4 className="text-[10px] font-bold text-slate-400 uppercase mb-8 text-center tracking-widest">Revenue Mix: Core Business is Shrinking</h4>
                                <div className="space-y-10">
                                    <div>
                                        <div className="flex justify-between text-xs font-bold mb-2"><span>2015 Contribution</span><span className="text-slate-400">56%</span></div>
                                        <div className="w-full bg-slate-100 h-4 rounded-full overflow-hidden"><div className="bg-[#003366] h-full" style={{width: '56%'}}></div></div>
                                    </div>
                                    <div>
                                        <div className="flex justify-between text-xs font-bold mb-2"><span>2019 Contribution</span><span className="text-red-500 font-black text-sm">44%</span></div>
                                        <div className="w-full bg-slate-100 h-4 rounded-full overflow-hidden"><div className="bg-red-500 h-full" style={{width: '44%'}}></div></div>
                                    </div>
                                </div>
                            </div>
                        </div>
                      </div>
                    )}

                    {/* Slide 3: Market Analysis - Central (HR Step 2) */}
                    {currentSlide === 3 && (
                      <div className="h-full flex flex-col animate-in slide-in-from-right duration-500">
                        <div className="flex justify-between items-end mb-8 border-b pb-4 border-slate-100">
                            <h2 className="text-3xl font-bold text-[#003366] Kanit flex items-center gap-4"><Map className="text-orange-500" size={32}/> 2. ตลาด: วิกฤตการณ์พื้นที่ "ภาคกลาง"</h2>
                            <p className="text-[10px] font-bold text-red-500 bg-red-50 px-3 py-1 rounded-full border border-red-100">Critical Threat</p>
                        </div>
                        <div className="grid grid-cols-2 gap-10 flex-grow">
                            <div className="bg-white p-8 rounded-3xl shadow-xl border border-slate-100 flex flex-col items-center justify-center">
                                <h4 className="text-xs font-bold text-slate-400 uppercase mb-8 tracking-widest">Market Share: Central Region (Hypermarket)</h4>
                                <div className="flex items-end justify-center gap-8 h-48 w-full border-b-2 border-slate-100 px-4">
                                    {marketShareCentral.map((item, i) => (
                                        <div key={i} className="flex-1 flex flex-col items-center">
                                            <div 
                                                className="w-full rounded-t-xl transition-all duration-1000 flex items-center justify-center text-white text-[10px] font-bold" 
                                                style={{ height: `${item.value * 1.8}%`, backgroundColor: item.color }}
                                            >
                                                {item.value}%
                                            </div>
                                            <p className="mt-4 text-[9px] font-bold text-slate-500 text-center uppercase Sarabun">{item.name}</p>
                                        </div>
                                    ))}
                                </div>
                            </div>
                            <div className="flex flex-col justify-center space-y-6">
                                <div className="p-6 bg-[#003366] text-white rounded-3xl shadow-lg relative overflow-hidden group">
                                    <div className="absolute top-0 right-0 w-24 h-24 bg-white/5 rounded-bl-full group-hover:scale-125 transition-transform"></div>
                                    <h3 className="text-xl font-bold mb-3 flex items-center gap-2"><AlertTriangle size={20} className="text-orange-400"/> The Giant Gap: 11%</h3>
                                    <p className="text-sm opacity-80 leading-relaxed Sarabun">ในภาคกลางซึ่งเป็นหัวใจหลัก เราตามหลัง Giant ถึง 11% ขณะที่ Orange ไล่จี้ส่วนแบ่งทั่วประเทศเหลือเพียง 1%</p>
                                </div>
                                <div className="bg-white p-6 rounded-2xl border border-dashed border-slate-200">
                                    <p className="text-xs text-slate-400 font-bold uppercase mb-2">Competitor Insight:</p>
                                    <p className="text-sm text-slate-500 Sarabun">Orange ชนะใจกลุ่ม <strong>Young Adult</strong> (Index 125) ได้อย่างเบ็ดเสร็จด้วยภาพลักษณ์แบรนด์ที่ทันสมัยกว่า</p>
                                </div>
                            </div>
                        </div>
                      </div>
                    )}

                    {/* Slide 4: Shopper Insights (HR Step 3) */}
                    {currentSlide === 4 && (
                      <div className="h-full flex flex-col animate-in slide-in-from-right duration-500">
                        <h2 className="text-3xl font-bold text-[#003366] mb-8 border-l-8 border-orange-500 pl-6 Kanit">3. ข้อมูลเชิงลึก: กลุ่มเป้าหมายที่ต้องกอบกู้</h2>
                        <div className="grid grid-cols-2 gap-10 flex-grow items-center">
                            <div className="bg-white p-6 rounded-3xl shadow-lg border border-slate-50">
                                <h3 className="text-center text-[10px] font-bold text-slate-400 uppercase tracking-widest mb-10">Shopper Index (SF vs Total Market Average 100)</h3>
                                <ResponsiveContainer width="100%" height={300}>
                                    <BarChart data={shopperIndexData} margin={{ top: 20, right: 30, left: 20, bottom: 5 }}>
                                        <CartesianGrid strokeDasharray="3 3" vertical={false} stroke="#F1F5F9" />
                                        <XAxis dataKey="segment" fontSize={9} interval={0} tickLine={false} axisLine={false} />
                                        <YAxis domain={[0, 150]} fontSize={10} axisLine={false} />
                                        <Tooltip cursor={{fill: '#F8FAFC'}} contentStyle={{borderRadius: '12px'}} />
                                        <Bar dataKey="SF" fill="#003366" radius={[4, 4, 0, 0]} name="Sun Flower Index" />
                                        <Bar dataKey="Orange" fill="#E67E22" radius={[4, 4, 0, 0]} name="Orange Index" />
                                    </BarChart>
                                </ResponsiveContainer>
                            </div>
                            <div className="space-y-6">
                                <div className="p-6 bg-white border border-blue-100 rounded-3xl shadow-sm border-l-8 border-blue-500">
                                    <h4 className="font-bold text-blue-800 text-lg flex items-center gap-2 mb-2 italic Sarabun"><Target size={22}/> Our Stronghold</h4>
                                    <p className="text-sm text-slate-500 leading-relaxed Sarabun">เรายังแกร่งมากในกลุ่ม <strong>ครอบครัวที่มีบุตร</strong> (Index 120) และกลุ่มรายได้สูง (AB Index 110)</p>
                                </div>
                                <div className="p-6 bg-orange-50 rounded-3xl shadow-sm border-l-8 border-orange-500">
                                    <h4 className="font-bold text-orange-800 text-lg flex items-center gap-2 mb-2 italic Sarabun"><Zap size={22}/> The Opportunity Gap</h4>
                                    <p className="text-sm text-orange-900/70 leading-relaxed Sarabun">ต้องใช้ Tulip Synergy เพื่อเข้าถึงกลุ่ม <strong>Young Adult</strong> (Index 77) ซึ่งเป็นกลุ่มที่เรากำลัง "แพ้ราบคาบ" ให้กับคู่แข่ง</p>
                                </div>
                            </div>
                        </div>
                      </div>
                    )}

                    {/* Slide 5: CRM Strategy - Synergy (HR Step 4) */}
                    {currentSlide === 5 && (
                      <div className="h-full flex flex-col animate-in slide-in-from-right duration-500">
                        <h2 className="text-3xl font-bold text-[#003366] mb-10 border-l-8 border-orange-500 pl-6 Kanit">4. กลยุทธ์ "Unfair Advantage" Synergy</h2>
                        <div className="grid grid-cols-3 gap-8 flex-grow">
                            {[
                                { title: 'Location-Based', icon: <MapPin className="text-white" size={32}/>, color: 'bg-orange-500', desc: 'ส่ง SMS พิเศษเฉพาะกลุ่มผ่านเสาสัญญาณ Tulip เมื่อลูกค้าอยู่ใกล้รัศมี Hypermarket' },
                                { title: 'Single Profile', icon: <Smartphone className="text-white" size={32}/>, color: 'bg-[#003366]', desc: 'ผสานพฤติกรรมการโทรและช้อปปิ้งเป็นโปรไฟล์เดียว เพื่อมอบ Personalized Offers ที่แม่นยำ' },
                                { title: 'Digital Burn', icon: <Zap className="text-white" size={32}/>, color: 'bg-orange-500', desc: 'แลกพอยต์ Tulip เป็นส่วนลด Sun Flower ดึงคนรุ่นใหม่มาช้อปผ่านช่องทาง Online ของเรา' }
                            ].map((card, i) => (
                                <div key={i} className="bg-white p-8 rounded-[3rem] border border-slate-100 shadow-lg hover:-translate-y-2 transition-all duration-300 text-center flex flex-col items-center group">
                                    <div className={`w-16 h-16 ${card.color} rounded-2xl flex items-center justify-center mb-8 shadow-xl group-hover:rotate-12 transition-transform`}>
                                        {card.icon}
                                    </div>
                                    <h4 className="font-bold text-xl text-[#003366] mb-4 Kanit uppercase tracking-tight">{card.title}</h4>
                                    <p className="text-xs text-slate-500 Sarabun leading-relaxed opacity-80">{card.desc}</p>
                                </div>
                            ))}
                        </div>
                      </div>
                    )}

                    {/* Slide 6: Measurement (HR Step 5) */}
                    {currentSlide === 6 && (
                      <div className="h-full flex flex-col animate-in slide-in-from-right duration-500 overflow-y-auto">
                        <h2 className="text-3xl font-bold text-[#003366] mb-8 border-l-8 border-orange-500 pl-6 Kanit">5. ตัวชี้วัดความสำเร็จ (Key KPIs)</h2>
                        <div className="flex-grow flex flex-col justify-center py-4">
                            <div className="bg-white rounded-[2.5rem] shadow-2xl border border-slate-100 overflow-hidden">
                                <table className="w-full text-left Sarabun">
                                    <thead className="bg-[#003366] text-white">
                                        <tr>
                                            <th className="p-6 text-sm font-bold uppercase tracking-widest">Key Metric</th>
                                            <th className="p-6 text-sm font-bold uppercase tracking-widest text-center">Base (2019)</th>
                                            <th className="p-6 text-sm font-bold uppercase tracking-widest text-center">Target (2025)</th>
                                            <th className="p-6 text-sm font-bold uppercase tracking-widest">Core Action</th>
                                        </tr>
                                    </thead>
                                    <tbody className="divide-y text-sm">
                                        <tr>
                                            <td className="p-6 font-bold text-slate-700">Visit Frequency</td>
                                            <td className="p-6 text-center text-red-500 font-bold italic">8 / ปี</td>
                                            <td className="p-6 text-center text-green-600 font-black text-lg underline">11 / ปี</td>
                                            <td className="p-6 text-slate-500 font-medium">Geo-Fencing Notifications</td>
                                        </tr>
                                        <tr>
                                            <td className="p-6 font-bold text-slate-700">High Loyalty %</td>
                                            <td className="p-6 text-center font-bold italic">26%</td>
                                            <td className="p-6 text-center text-green-600 font-black text-lg underline">32%</td>
                                            <td className="p-6 text-slate-500 font-medium">Personalized Retention App</td>
                                        </tr>
                                        <tr>
                                            <td className="p-6 font-bold text-slate-700">Online Contribution</td>
                                            <td className="p-6 text-center font-bold italic">6%</td>
                                            <td className="p-6 text-center text-green-600 font-black text-lg underline">15%</td>
                                            <td className="p-6 text-slate-500 font-medium">Tulip Look-alike Acquisition</td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                            <div className="mt-8 p-6 bg-slate-900 text-white rounded-3xl shadow-xl flex items-center justify-between">
                                <div className="flex items-center gap-4">
                                    <div className="p-3 bg-white/10 rounded-xl"><BarChart3 className="text-orange-400" size={28}/></div>
                                    <p className="text-lg font-bold Kanit italic">"พลิกข้อมูลเครือข่าย 25 ล้านราย ให้เป็นกำไรที่ยั่งยืนผ่าน ROI +18%"</p>
                                </div>
                                <div className="bg-orange-500 px-6 py-2 rounded-full font-black text-sm uppercase shadow-lg Sarabun tracking-tighter">Approved Plan</div>
                            </div>
                        </div>
                      </div>
                    )}
                </div>

                {/* Fixed Navigation Footer */}
                <footer className="bg-white border-t border-slate-100 px-12 py-6 flex justify-between items-center z-50">
                    <div className="flex items-center gap-4">
                        <span className="bg-slate-100 px-4 py-1.5 rounded-full text-[10px] font-bold text-[#003366] Sarabun tracking-widest">SLIDE {currentSlide} OF {totalSlides}</span>
                    </div>
                    <div className="flex gap-4">
                        <button 
                            onClick={prevSlide}
                            disabled={currentSlide === 1}
                            className={`px-6 py-2.5 rounded-xl border font-bold flex items-center gap-2 transition-all text-xs ${currentSlide === 1 ? 'opacity-20 cursor-not-allowed' : 'hover:bg-slate-50 text-slate-500 border-slate-200'}`}
                        >
                            <ChevronLeft size={16}/> ย้อนกลับ
                        </button>
                        <button 
                            onClick={nextSlide}
                            className={`px-8 py-2.5 rounded-xl text-white font-bold transition-all flex items-center gap-2 shadow-lg text-xs ${currentSlide === totalSlides ? 'bg-green-600 hover:bg-green-700' : 'bg-[#003366] hover:bg-slate-800'}`}
                        >
                            {currentSlide === totalSlides ? 'สิ้นสุดพรีเซนต์' : 'หน้าถัดไป'} <ChevronRight size={16}/>
                        </button>
                    </div>
                </footer>
            </div>
          </div>
        )}
      </main>

      {/* Persistent App Progress Status Bar */}
      <footer className="bg-white border-t border-slate-200 px-8 py-2 flex justify-between items-center text-[9px] text-slate-400 font-bold uppercase tracking-widest Sarabun z-50">
          <div className="flex gap-6 items-center">
              <span className="flex items-center gap-1.5"><div className="w-1.5 h-1.5 rounded-full bg-green-500 animate-pulse"></div> Analytics Synced</span>
              <span className="flex items-center gap-1.5"><Smartphone size={10}/> Data Lake: Tulip connectivity active</span>
          </div>
          <div className="flex gap-6 items-center">
              <span className="text-orange-500">Market Share Focus: 41% → 45%</span>
              <span className="text-[#003366]">CRM ID: SF-TULIP-2025</span>
          </div>
      </footer>
    </div>
  );
};

export default App;
