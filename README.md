# medidiagnose
MediDiagnose is an AI-powered healthcare platform that helps users assess potential health conditions based on symptoms and personal health information. It provides fast, user-friendly disease predictions and health insights, supporting early awareness and informed healthcare decisions through accessible technology.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>HealthDx — KASAMA</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,400&family=Inter:wght@300;400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
html{scroll-behavior:smooth;}
body{font-family:'Inter',sans-serif;font-size:15px;line-height:1.6;background:#f0fdf4;color:#1a2e22;overflow-x:hidden;}
 
/* WELCOME */
#welcome{position:fixed;inset:0;z-index:9999;background:linear-gradient(145deg,#e8f5ee,#eaf4fb 40%,#f3eeff 70%,#fff8ee);display:flex;align-items:center;justify-content:center;overflow:hidden;transition:opacity .8s ease,transform .8s ease;}
#welcome.exit{opacity:0;transform:scale(1.05);pointer-events:none;}
.orb{position:absolute;border-radius:50%;filter:blur(80px);animation:drift 14s ease-in-out infinite alternate;}
.orb1{width:520px;height:520px;background:rgba(134,239,172,.5);top:-160px;left:-160px;}
.orb2{width:440px;height:440px;background:rgba(147,197,253,.5);bottom:-100px;right:-120px;animation-delay:-5s;}
.orb3{width:320px;height:320px;background:rgba(196,181,253,.45);top:30%;left:52%;animation-delay:-9s;}
.orb4{width:260px;height:260px;background:rgba(253,186,116,.4);top:8%;right:18%;animation-delay:-3s;}
@keyframes drift{from{transform:translate(0,0);}to{transform:translate(35px,25px) scale(1.08);}}
.grid-bg{position:absolute;inset:0;background-image:linear-gradient(rgba(0,140,70,.05) 1px,transparent 1px),linear-gradient(90deg,rgba(0,140,70,.05) 1px,transparent 1px);background-size:44px 44px;}
#ecg-cv{position:absolute;inset:0;width:100%;height:100%;}
.wc{position:relative;z-index:10;text-align:center;padding:42px 36px 36px;max-width:660px;width:calc(100% - 32px);background:rgba(255,255,255,.82);backdrop-filter:blur(22px);border-radius:28px;border:1px solid rgba(255,255,255,.95);box-shadow:0 24px 80px rgba(0,120,60,.13);}
.w-logo{font-family:'Playfair Display',serif;font-size:clamp(46px,9vw,82px);font-weight:700;color:#14532d;letter-spacing:-3px;line-height:1;animation:popIn .9s cubic-bezier(.175,.885,.32,1.275) both;}
.w-logo span{color:#16a34a;}
.w-sub{font-family:'Space Mono',monospace;font-size:11px;letter-spacing:9px;color:#0369a1;margin-top:7px;animation:popIn .9s ease .15s both;}
@keyframes popIn{from{opacity:0;transform:translateY(20px) scale(.96);}to{opacity:1;transform:none;}}
.w-line{width:56px;height:2px;background:linear-gradient(90deg,transparent,#16a34a,transparent);margin:20px auto;animation:popIn .9s ease .28s both;}
.qbox{min-height:82px;display:flex;flex-direction:column;align-items:center;justify-content:center;animation:popIn .9s ease .38s both;margin-bottom:24px;background:rgba(22,163,74,.07);border-radius:14px;padding:16px 18px;border:1px solid rgba(22,163,74,.12);}
.qt{font-family:'Playfair Display',serif;font-style:italic;font-size:clamp(14px,2.2vw,17px);color:#166534;line-height:1.65;max-width:480px;transition:opacity .45s;}
.qa{font-size:11px;color:#0369a1;margin-top:8px;letter-spacing:2px;text-transform:uppercase;font-weight:600;transition:opacity .45s;}
.qt.fade,.qa.fade{opacity:0;}
.qdots{display:flex;gap:5px;justify-content:center;margin-top:8px;}
.qdot{width:6px;height:6px;border-radius:50%;background:rgba(22,163,74,.2);cursor:pointer;transition:background .3s;}
.qdot.on{background:#16a34a;}
.cta-btn{display:inline-flex;align-items:center;gap:10px;background:linear-gradient(135deg,#16a34a,#22c55e);color:#fff;font-family:'Inter',sans-serif;font-weight:700;font-size:clamp(14px,2.2vw,17px);padding:16px 44px;border-radius:50px;border:none;cursor:pointer;animation:popIn .9s ease .52s both,glow 2.6s ease-in-out 1.6s infinite;transition:transform .2s,box-shadow .2s;box-shadow:0 8px 28px rgba(22,163,74,.35);}
.cta-btn:hover{transform:translateY(-3px) scale(1.04);box-shadow:0 16px 48px rgba(22,163,74,.45);}
@keyframes glow{0%,100%{box-shadow:0 8px 28px rgba(22,163,74,.35);}50%{box-shadow:0 8px 40px rgba(22,163,74,.6);}}
.pills{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin-top:22px;animation:popIn .9s ease .68s both;}
.pill{background:rgba(255,255,255,.85);border:1px solid rgba(22,163,74,.18);border-radius:20px;padding:6px 15px;font-size:12px;color:#166534;display:flex;align-items:center;gap:6px;box-shadow:0 1px 3px rgba(0,0,0,.06);}
.pdot{width:6px;height:6px;border-radius:50%;}
 
/* MAIN APP */
#app{display:none;background:#f0fdf4;min-height:100vh;}
#app.show{display:block;}
.app-header{background:#fff;border-bottom:1px solid #d1fae5;padding:14px 28px;display:flex;align-items:center;gap:12px;position:sticky;top:0;z-index:100;box-shadow:0 1px 8px rgba(0,120,60,.08);}
.a-logo{font-family:'Playfair Display',serif;font-size:22px;color:#14532d;}
.a-logo span{color:#16a34a;}
.a-badge{font-family:'Space Mono',monospace;font-size:10px;letter-spacing:.05em;background:#dcfce7;color:#16a34a;border:1px solid #bbf7d0;padding:2px 9px;border-radius:20px;}
.container{max-width:880px;margin:0 auto;padding:36px 20px 80px;}
.hero{text-align:center;margin-bottom:36px;}
.hero h1{font-family:'Playfair Display',serif;font-size:clamp(24px,5vw,40px);color:#14532d;line-height:1.2;margin-bottom:10px;}
.hero h1 em{color:#16a34a;font-style:italic;}
.hero p{color:#4b7260;max-width:500px;margin:0 auto;font-size:14px;}
.step-row{display:flex;gap:8px;margin-bottom:28px;overflow-x:auto;padding-bottom:4px;}
.step-item{flex:1;min-width:88px;background:#fff;border:1px solid #d1fae5;border-radius:12px;padding:11px 10px;text-align:center;font-size:12px;color:#6b9e85;transition:all .2s;}
.step-item.active{border-color:#16a34a;background:#f0fdf4;color:#16a34a;}
.step-item.done{border-color:#bbf7d0;}
.step-num{font-family:'Space Mono',monospace;font-size:17px;font-weight:700;display:block;margin-bottom:2px;}
.step-item.active .step-num{color:#16a34a;}
.card{background:#fff;border:1px solid #d1fae5;border-radius:14px;padding:24px 26px;margin-bottom:16px;box-shadow:0 2px 12px rgba(0,100,50,.05);}
.card-title{font-family:'Playfair Display',serif;font-size:19px;color:#14532d;margin-bottom:16px;display:flex;align-items:center;gap:10px;}
.cicon{width:30px;height:30px;background:#dcfce7;border:1px solid #bbf7d0;border-radius:8px;display:grid;place-items:center;font-size:15px;}
.form-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
.form-grid.full{grid-template-columns:1fr;}
@media(max-width:560px){.form-grid{grid-template-columns:1fr;}}
.field{display:flex;flex-direction:column;gap:5px;}
label{font-size:11px;font-weight:700;letter-spacing:.05em;color:#4b7260;text-transform:uppercase;}
input,select,textarea{background:#f0fdf4;border:1px solid #bbf7d0;border-radius:8px;color:#1a2e22;font-family:'Inter',sans-serif;font-size:14px;padding:10px 13px;transition:all .2s;outline:none;width:100%;}
input:focus,select:focus,textarea:focus{border-color:#16a34a;box-shadow:0 0 0 3px rgba(22,163,74,.12);background:#fff;}
select option{background:#fff;}
textarea{resize:vertical;min-height:82px;}
.sym-group-label{width:100%;margin:12px 0 5px;font-size:11px;font-weight:700;letter-spacing:.05em;color:#166534;text-transform:uppercase;padding:6px 10px;background:#dcfce7;border-radius:6px;}
.tag-container{display:flex;flex-wrap:wrap;gap:7px;margin-top:4px;}
.sym-tag{background:#f0fdf4;border:1px solid #bbf7d0;border-radius:20px;padding:5px 13px;font-size:13px;cursor:pointer;transition:all .18s;user-select:none;color:#166534;}
.sym-tag:hover{background:#dcfce7;border-color:#86efac;}
.sym-tag.selected{background:#16a34a;border-color:#16a34a;color:#fff;box-shadow:0 2px 8px rgba(22,163,74,.3);}
.slider-row{display:flex;align-items:center;gap:12px;}
input[type=range]{-webkit-appearance:none;appearance:none;height:5px;border-radius:5px;background:#bbf7d0;border:none;padding:0;cursor:pointer;flex:1;}
input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:18px;height:18px;border-radius:50%;background:#16a34a;cursor:pointer;border:2px solid #fff;box-shadow:0 1px 4px rgba(0,0,0,.15);}
.sev-lbl{font-family:'Space Mono',monospace;font-size:12px;color:#16a34a;min-width:82px;text-align:right;}
.btn{display:inline-flex;align-items:center;gap:8px;background:#16a34a;color:#fff;font-weight:700;font-size:15px;padding:12px 26px;border-radius:10px;border:none;cursor:pointer;transition:all .15s;font-family:'Inter',sans-serif;box-shadow:0 4px 14px rgba(22,163,74,.3);}
.btn:hover{transform:translateY(-1px);box-shadow:0 6px 22px rgba(22,163,74,.4);}
.btn.sec{background:#fff;color:#166534;border:1px solid #bbf7d0;box-shadow:0 2px 8px rgba(0,0,0,.06);}
.btn.sec:hover{border-color:#16a34a;}
.btn-row{display:flex;gap:12px;justify-content:flex-end;flex-wrap:wrap;margin-top:20px;}
 
/* RESULTS */
#result-section{display:none;}
#result-section.visible{display:block;}
.dx-header{background:linear-gradient(135deg,#f0fdf4,#eff6ff);border:1px solid #86efac;border-radius:14px;padding:22px 24px;margin-bottom:16px;display:flex;align-items:flex-start;gap:14px;box-shadow:0 2px 12px rgba(22,163,74,.1);}
.dx-ico{font-size:36px;flex-shrink:0;}
.dx-title{font-family:'Playfair Display',serif;font-size:26px;color:#14532d;margin-bottom:5px;}
.dx-conf{font-family:'Space Mono',monospace;font-size:11px;color:#16a34a;background:#dcfce7;border:1px solid #86efac;padding:2px 10px;border-radius:12px;display:inline-block;margin-bottom:8px;}
.dx-sum{color:#374151;font-size:14px;line-height:1.7;}
.res-grid{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
@media(max-width:620px){.res-grid{grid-template-columns:1fr;}}
.res-card{background:#fff;border:1px solid #d1fae5;border-radius:14px;padding:20px;box-shadow:0 2px 10px rgba(0,100,50,.05);}
.res-card h3{font-size:12px;text-transform:uppercase;letter-spacing:.06em;color:#4b7260;margin-bottom:12px;display:flex;align-items:center;gap:7px;font-weight:700;padding-bottom:8px;border-bottom:1px solid #f0fdf4;}
.res-card h3 .dot{width:8px;height:8px;border-radius:2px;flex-shrink:0;}
.res-card ul{list-style:none;}
.res-card ul li{padding:7px 0;border-bottom:1px solid #f9fafb;font-size:13.5px;color:#374151;display:flex;gap:8px;align-items:flex-start;line-height:1.6;}
.res-card ul li:last-child{border-bottom:none;}
.res-card ul li::before{content:'→';color:#16a34a;flex-shrink:0;font-size:12px;margin-top:2px;font-weight:700;}
.res-card.blue ul li::before{color:#3b82f6;}
.res-card.warn{border-color:#fed7aa;}
.res-card.warn ul li::before{content:'⚠';color:#f97316;}
.full{grid-column:1/-1;}
.disc{background:#fff7ed;border:1px solid #fed7aa;border-radius:12px;padding:13px 17px;margin-top:16px;font-size:12px;color:#9a3412;line-height:1.6;}
.sel-count{background:#dcfce7;border:1px solid #86efac;border-radius:8px;padding:8px 14px;font-size:13px;color:#166534;margin-top:12px;font-weight:600;}
</style>
</head>
<body>
 
<!-- WELCOME -->
<div id="welcome">
  <div class="orb orb1"></div><div class="orb orb2"></div><div class="orb orb3"></div><div class="orb orb4"></div>
  <div class="grid-bg"></div>
  <canvas id="ecg-cv"></canvas>
  <div id="ptc"></div>
  <div class="wc">
    <div class="w-logo">Health<span>Dx</span></div>
    <div class="w-sub">K &nbsp; A &nbsp; S &nbsp; A &nbsp; M &nbsp; A</div>
    <div class="w-line"></div>
    <div class="qbox">
      <div class="qt" id="qt"></div>
      <div class="qa" id="qa"></div>
      <div class="qdots" id="qdots"></div>
    </div>
    <button class="cta-btn" onclick="enterApp()">🩺&nbsp; Start My Health Check &nbsp;→</button>
    <div class="pills">
      <div class="pill"><div class="pdot" style="background:#16a34a"></div>Instant Results</div>
      <div class="pill"><div class="pdot" style="background:#0369a1"></div>Home Remedies</div>
      <div class="pill"><div class="pdot" style="background:#7c3aed"></div>Medicine Guide</div>
      <div class="pill"><div class="pdot" style="background:#ea580c"></div>No Internet Needed</div>
    </div>
  </div>
</div>
 
<!-- APP -->
<div id="app">
<header class="app-header">
  <div class="a-logo">Health<span>Dx</span></div>
  <div class="a-badge">KASAMA</div>
</header>
<div class="container">
  <div class="hero">
    <h1>Your health, understood<br><em>clearly &amp; instantly.</em></h1>
    <p>Select even one symptom — get instant home remedies, medicines, and health advice. No internet needed.</p>
  </div>
  <div class="step-row">
    <div class="step-item active" id="st1"><span class="step-num">01</span>Profile</div>
    <div class="step-item" id="st2"><span class="step-num">02</span>History</div>
    <div class="step-item" id="st3"><span class="step-num">03</span>Symptoms</div>
    <div class="step-item" id="st4"><span class="step-num">04</span>Results</div>
  </div>
 
  <!-- S1 -->
  <div id="s1">
    <div class="card">
      <div class="card-title"><div class="cicon">👤</div>Basic Profile</div>
      <div class="form-grid">
        <div class="field"><label>Full Name (optional)</label><input id="v-name" placeholder="e.g. Priya Sharma"></div>
        <div class="field"><label>Age (years)</label><input type="number" id="v-age" placeholder="e.g. 28" min="1" max="120"></div>
        <div class="field"><label>Gender</label><select id="v-gender"><option value="">Select</option><option>Male</option><option>Female</option><option>Other</option></select></div>
        <div class="field"><label>Weight (kg)</label><input type="number" id="v-weight" placeholder="e.g. 58"></div>
        <div class="field"><label>Height (cm)</label><input type="number" id="v-height" placeholder="e.g. 162"></div>
        <div class="field"><label>Blood Group</label><select id="v-blood"><option value="">Unknown</option><option>A+</option><option>A−</option><option>B+</option><option>B−</option><option>AB+</option><option>AB−</option><option>O+</option><option>O−</option></select></div>
      </div>
    </div>
    <div class="btn-row"><button class="btn" onclick="goSec(2)">Continue →</button></div>
  </div>
 
  <!-- S2 -->
  <div id="s2" style="display:none">
    <div class="card">
      <div class="card-title"><div class="cicon">📋</div>Medical History</div>
      <div class="form-grid">
        <div class="field"><label>Existing Conditions</label><input id="v-cond" placeholder="e.g. Diabetes, Thyroid"></div>
        <div class="field"><label>Current Medications</label><input id="v-meds" placeholder="e.g. Metformin 500mg"></div>
        <div class="field"><label>Known Allergies</label><input id="v-allergy" placeholder="e.g. Penicillin"></div>
        <div class="field"><label>Recent Surgery</label><input id="v-surg" placeholder="e.g. None"></div>
        <div class="field"><label>Smoking</label><select id="v-smoke"><option>No</option><option>Occasional</option><option>Regular</option><option>Ex-smoker</option></select></div>
        <div class="field"><label>Alcohol</label><select id="v-alc"><option>No</option><option>Occasional</option><option>Regular</option></select></div>
      </div>
      <div class="form-grid full" style="margin-top:12px">
        <div class="field"><label>Family Medical History</label><textarea id="v-fam" placeholder="e.g. Father has diabetes, mother has thyroid..."></textarea></div>
      </div>
    </div>
    <div class="btn-row"><button class="btn sec" onclick="goSec(1)">← Back</button><button class="btn" onclick="goSec(3)">Continue →</button></div>
  </div>
 
  <!-- S3 -->
  <div id="s3" style="display:none">
    <div class="card">
      <div class="card-title"><div class="cicon">🩺</div>Current Symptoms <span style="font-family:Inter;font-size:13px;color:#6b9e85;font-weight:400;margin-left:6px;">(select minimum 1)</span></div>
      <div class="tag-container" id="sym-tags"></div>
      <div id="sel-count" class="sel-count" style="display:none"></div>
      <div class="form-grid" style="margin-top:18px">
        <div class="field"><label>Duration</label><select id="v-dur"><option>Less than 24 hours</option><option>1–3 days</option><option>4–7 days</option><option>1–2 weeks</option><option>2–4 weeks</option><option>More than 1 month</option></select></div>
        <div class="field"><label>Onset</label><select id="v-onset"><option>Gradual</option><option>Sudden</option><option>After eating</option><option>During activity</option><option>At rest / night</option></select></div>
      </div>
      <div class="field" style="margin-top:14px">
        <label>Overall Severity: <span id="sev-num">5</span>/10</label>
        <div class="slider-row"><input type="range" id="v-sev" min="1" max="10" value="5" oninput="updSev(this.value)"><span class="sev-lbl" id="sev-lbl">Moderate</span></div>
      </div>
      <div class="field" style="margin-top:14px"><label>Describe other symptoms</label><textarea id="v-extra" placeholder="Add any other symptoms or details..."></textarea></div>
    </div>
    <div id="errbox" style="background:#fef2f2;border:1px solid #fecaca;border-radius:10px;padding:12px 16px;color:#dc2626;font-size:14px;display:none;margin-top:10px;"></div>
    <div class="btn-row"><button class="btn sec" onclick="goSec(2)">← Back</button><button class="btn" onclick="diagnose()">🔬 Get Diagnosis</button></div>
  </div>
 
  <!-- RESULTS -->
  <div id="result-section">
    <div class="dx-header">
      <div class="dx-ico" id="r-ico">🏥</div>
      <div>
        <div class="dx-conf" id="r-conf">Assessment</div>
        <div class="dx-title" id="r-title">—</div>
        <div class="dx-sum" id="r-sum"></div>
      </div>
    </div>
    <div class="res-grid" id="r-grid"></div>
    <div class="disc">⚠ <strong>Disclaimer:</strong> This information is for educational purposes only and does not replace professional medical advice. Please consult a qualified doctor for actual diagnosis and treatment.</div>
    <div class="btn-row" style="margin-top:18px">
      <button class="btn sec" onclick="resetApp()">← Check Again</button>
      <button class="btn" onclick="window.print()">🖨 Print Report</button>
    </div>
  </div>
</div>
</div>
 
<script>
/* QUOTES */
const QS=[
  {t:"The greatest wealth is health.",a:"— Virgil"},
  {t:"Take care of your body. It's the only place you have to live.",a:"— Jim Rohn"},
  {t:"It is health that is real wealth, not pieces of gold and silver.",a:"— Mahatma Gandhi"},
  {t:"The first wealth is health.",a:"— Ralph Waldo Emerson"},
  {t:"A healthy outside starts from the inside.",a:"— Robert Urich"},
  {t:"Your body hears everything your mind says.",a:"— Naomi Judd"},
  {t:"Health is not valued till sickness comes.",a:"— Thomas Fuller"},
  {t:"To keep the body in good health is a duty — otherwise we cannot keep our mind strong.",a:"— Buddha"},
  {t:"An apple a day keeps the doctor away.",a:"— English Proverb"},
  {t:"Let food be thy medicine and medicine be thy food.",a:"— Hippocrates"},
];
let qi=0;
const qtEl=document.getElementById('qt'),qaEl=document.getElementById('qa'),dotsEl=document.getElementById('qdots');
QS.forEach((_,i)=>{const d=document.createElement('div');d.className='qdot'+(i===0?' on':'');d.onclick=()=>showQ(i);dotsEl.appendChild(d);});
function showQ(i){qtEl.classList.add('fade');qaEl.classList.add('fade');setTimeout(()=>{qi=i;qtEl.textContent='"'+QS[i].t+'"';qaEl.textContent=QS[i].a;qtEl.classList.remove('fade');qaEl.classList.remove('fade');document.querySelectorAll('.qdot').forEach((d,j)=>d.classList.toggle('on',j===i));},400);}
showQ(0);setInterval(()=>showQ((qi+1)%QS.length),4000);
 
/* ECG */
const cv=document.getElementById('ecg-cv'),cx=cv.getContext('2d');let off=0;
function rsz(){cv.width=window.innerWidth;cv.height=window.innerHeight;}rsz();window.addEventListener('resize',rsz);
function ecgY(x){const p=((x+off)%120+120)%120;if(p<10)return 0;if(p<18)return -22;if(p<22)return 32;if(p<28)return -60;if(p<34)return 36;if(p<44)return -8;return 0;}
function drawECG(){const w=cv.width,h=cv.height;cx.clearRect(0,0,w,h);const cy=h*.65;cx.beginPath();cx.strokeStyle='rgba(22,163,74,.08)';cx.lineWidth=1;cx.setLineDash([5,9]);cx.moveTo(0,cy);cx.lineTo(w,cy);cx.stroke();cx.setLineDash([]);cx.beginPath();cx.strokeStyle='rgba(22,163,74,.3)';cx.lineWidth=2;cx.lineJoin='round';cx.lineCap='round';for(let x=0;x<=w;x++){const y=cy+ecgY(x);x===0?cx.moveTo(x,y):cx.lineTo(x,y);}cx.stroke();off-=1.6;requestAnimationFrame(drawECG);}
drawECG();
 
/* PARTICLES */
const ptc=document.getElementById('ptc');Object.assign(ptc.style,{position:'absolute',inset:0,pointerEvents:'none',zIndex:1});
const ptcols=['rgba(22,163,74,.5)','rgba(3,105,161,.4)','rgba(124,58,237,.35)','rgba(234,88,12,.35)'];
for(let i=0;i<18;i++){const p=document.createElement('div'),sz=Math.random()*5+2;p.style.cssText=`position:absolute;border-radius:50%;width:${sz}px;height:${sz}px;background:${ptcols[Math.floor(Math.random()*ptcols.length)]};left:${Math.random()*100}%;bottom:${Math.random()*20}%;opacity:0;animation:rise ${4+Math.random()*6}s linear ${Math.random()*5}s infinite;`;ptc.appendChild(p);}
 
/* ENTER APP */
function enterApp(){const w=document.getElementById('welcome');w.classList.add('exit');setTimeout(()=>{w.style.display='none';document.getElementById('app').classList.add('show');},800);}
 
/* ══════════════════════════════════════════
   COMPLETE OFFLINE MEDICAL KNOWLEDGE BASE
   ══════════════════════════════════════════ */
const KB={
  "Fever":{
    ico:"🌡️",diagnosis:"Fever — Immune System Response to Infection",confidence:"High",
    summary:"Fever is the body raising its temperature to fight off infection. It is a natural immune defense most commonly triggered by viral infections (flu, cold), bacterial infections, or inflammation. Your immune system is actively working to protect you. Most fevers in adults resolve in 3-5 days.",
    matched:["Fever","Chills","Body ache","Fatigue","Night sweats","Loss of appetite"],
    home:[
      "🍵 Tulsi-Ginger-Honey Tea: Boil 8 fresh tulsi (basil) leaves + 1 inch grated ginger in 1.5 cups water for 5-7 min. Strain, add 1 tbsp honey. Drink hot 3-4 times/day — powerful antiviral and immune booster",
      "💧 Coriander Seed Water: Boil 1 tbsp coriander (dhania) seeds in 2 cups water until reduced to 1 cup. Strain, cool slightly. Drink 2-3 times/day — traditional fever reducer",
      "🧊 Cool Compress: Soak a soft cloth in cool (not ice cold) water. Place on forehead, wrists, and back of neck. Replace every 10 min — brings temperature down quickly",
      "🥛 Turmeric Milk (Haldi Doodh): Mix 1 tsp turmeric + pinch of black pepper in warm milk at bedtime. Add honey to taste — anti-inflammatory, improves sleep during fever",
      "🌿 Fenugreek (Methi) Water: Soak 1 tbsp methi seeds in a glass of water overnight. Drink on an empty stomach next morning — breaks fever and detoxifies",
      "🍋 Lime Juice + Honey Water: Mix juice of half lime + 1 tbsp honey in warm water. Drink every 2 hours — replenishes Vitamin C and soothes",
      "🛁 Lukewarm Sponge Bath: Sponge the body with lukewarm water focusing on armpits, groin, and neck — brings down temperature effectively"
    ],
    medicine:[
      "💊 Paracetamol 500mg (Crocin/Calpol) — Take 1 tablet every 6 hours. Do not exceed 4 tablets/day. Best taken with water after light food",
      "💊 Dolo 650 (Paracetamol 650mg) — For adults with higher fever (>101°F). Take every 6-8 hours, max 3 tablets/day. Most prescribed in India",
      "💊 Ibuprofen 400mg (Brufen/Combiflam) — Take with food every 8 hours. Reduces fever AND body ache. Avoid if stomach is empty or you have acidity",
      "💊 Nimesulide 100mg (Nise) — For fever with severe body pain. Take twice daily after meals. Not recommended for children under 12",
      "🧴 Vicks VapoRub — Apply on chest and back at night for comfort and to ease breathing",
      "🩺 See doctor if: fever above 103°F (39.4°C), lasts more than 3 days, or is accompanied by severe headache, rash, or difficulty breathing"
    ],
    lifestyle:[
      "Rest completely — do not go to work or exercise. Your body needs all energy to fight infection",
      "Drink fluids every 30 min — water, ORS, coconut water, clear soups, lemon water",
      "Eat light, easily digestible food — khichdi, dal soup, banana, toast, plain rice",
      "Avoid fans blowing directly on you — this can cause chills without lowering fever"
    ],
    flags:["Fever above 103°F (39.4°C) in adults — go to emergency","Fever with stiff neck + severe headache — possible meningitis, call doctor immediately","Febrile seizures (body shaking/convulsions)","Fever lasting more than 5 days","Fever with skin rash, especially petechiae (small red dots)"]
  },
 
  "Headache":{
    ico:"🧠",diagnosis:"Tension Headache / Stress & Lifestyle-Related Headache",confidence:"High",
    summary:"Headache is the world's most common pain complaint. Most headaches (90%) are tension-type caused by stress, dehydration, poor posture, eye strain, skipped meals, or hormonal changes. Understanding your trigger is the most effective way to prevent recurrence.",
    matched:["Headache","Fatigue","Anxiety","Dizziness","Blurred vision","Difficulty concentrating"],
    home:[
      "💧 Instant Hydration: Drink 2-3 glasses of water immediately — dehydration is the #1 most common and most overlooked cause of headache",
      "🌿 Peppermint Oil on Temples: Dilute 2 drops peppermint essential oil in 1 tsp coconut oil. Massage in small circles on temples and forehead for 5 min — natural pain relief equal to Paracetamol",
      "🍵 Ginger-Lemon Tea: Boil 1 inch fresh ginger in 1.5 cups water for 5 min. Add honey and lemon juice. Sip slowly — reduces inflammation, relieves nausea from headache",
      "🧊 Cold Compress (for migraine): Wrap ice cubes in cloth, apply on forehead or back of neck for 15 min — constricts blood vessels",
      "🔥 Warm Compress (for tension): Apply warm towel on neck and shoulder muscles for 15 min — releases muscle tension",
      "🧄 Clove + Rock Salt Remedy: Crush 4-5 cloves, mix with pinch of rock salt in 1 tsp coconut oil. Massage on temples for 5 min — traditional pain reliever",
      "🛌 Dark, Quiet Room: Lie down in a dark, silent room with eyes closed for 20-30 min — most effective for migraine attacks"
    ],
    medicine:[
      "💊 Paracetamol 500-1000mg (Crocin) — First choice for tension headache. Take at the very first sign of headache for best effect",
      "💊 Ibuprofen 400mg (Brufen) with food — Better for throbbing, pulsating headache. Anti-inflammatory action",
      "💊 Combiflam (Ibuprofen 400mg + Paracetamol 325mg) — For moderate headache with body ache",
      "💊 Saridon (Paracetamol + Propyphenazone + Caffeine) — Fast-acting for severe headache, caffeine helps absorption",
      "💊 Sumatriptan 50mg — Prescription only, specifically for migraine attacks. Very effective",
      "🩺 See neurologist if: headaches occur more than 3 times/week, progressively worsening, or not relieved by regular pain medicine"
    ],
    lifestyle:[
      "Eat meals at fixed times — low blood sugar from skipped meals causes headaches within hours",
      "20-20-20 Rule: Every 20 min, look 20 feet away for 20 seconds — prevents eye strain from screens",
      "Fix posture: sit upright with monitor at eye level — forward-head posture causes chronic tension headaches",
      "Limit caffeine to 1-2 cups/day — too much OR sudden withdrawal both cause headaches"
    ],
    flags:["Sudden severe 'thunderclap' headache — worst headache of your life, sudden onset — call emergency immediately","Headache with stiff neck + fever + sensitivity to light — possible meningitis","Headache after head injury or fall","Headache with facial weakness, slurred speech, vision loss — possible stroke","Headache that wakes you from sleep repeatedly"]
  },
 
  "Cough":{
    ico:"🫁",diagnosis:"Viral Upper Respiratory Infection / Acute Cough",confidence:"High",
    summary:"Cough is the body's way of clearing irritants from the airways. Most coughs (90%) are caused by viral infections like the common cold or flu, and DO NOT need antibiotics. Dry cough is tickly with no mucus. Wet/productive cough brings up phlegm. Most resolve in 7-14 days.",
    matched:["Cough","Cold / Runny nose","Sore throat","Chest pain","Wheezing","Fatigue"],
    home:[
      "🍯 Honey + Ginger + Lemon: Mix 1 tbsp raw honey + 1 tsp fresh ginger juice + 1 tsp lemon juice in half cup warm water. Drink 3-4 times/day — clinically proven cough suppressant, as effective as cough medicines",
      "🌬️ Steam Inhalation with Eucalyptus: Boil water, add 4-5 drops eucalyptus oil or Vicks. Lean over, cover head with towel, inhale steam for 10 min, 2x/day — opens airways, clears mucus",
      "🥛 Turmeric Milk at Night: Mix 1 tsp turmeric + pinch of black pepper in warm milk. Drink before bed — antibacterial, relieves chest cough",
      "🧂 Salt Water Gargle: Mix ½ tsp salt in warm water. Gargle for 40 seconds, 5-6 times/day — reduces throat irritation and kills bacteria",
      "🍵 Tulsi-Black Pepper Tea: Boil 8 tulsi leaves + 5 black peppercorns + 1 inch ginger. Strain, add honey. Drink 3x/day — most effective Indian remedy for cough",
      "🌿 Mulethi (Licorice Root): Suck on a small piece OR boil 2 mulethi sticks in water and drink as tea with honey — natural expectorant, soothes throat",
      "🧅 Onion Juice + Honey: Extract juice of ½ onion, mix equal amount of honey. Take 1 tsp 3-4 times/day — traditional expectorant"
    ],
    medicine:[
      "💊 Dextromethorphan Syrup (Benadryl DX / Cofsils DX) — For dry, irritating cough. Take 10ml every 6-8 hours — suppresses cough reflex",
      "💊 Ambroxol Syrup (Ambrolite-S / Muco-Clear) — For wet cough with phlegm. Thins mucus so it comes out easily. Take 10ml 3x/day",
      "💊 Levocetrizine 5mg + Montelukast (Telekast-L) — For allergic or post-nasal drip cough. Take 1 tablet at bedtime",
      "💊 Bromhexine 8mg (Bisolvon) — Mucolytic for thick phlegm. Take with plenty of water",
      "🩺 Antibiotics (e.g., Azithromycin 500mg) — ONLY if doctor confirms bacterial infection (thick green phlegm + fever). NEVER use for viral cough",
      "🩺 See doctor if: cough with blood, lasts more than 3 weeks, high fever, or significant breathing difficulty"
    ],
    lifestyle:[
      "Stay well hydrated — warm water and herbal teas thin mucus better than cold drinks",
      "Sleep with head elevated (2 pillows) — reduces post-nasal drip and nighttime coughing",
      "Avoid cold drinks, ice cream, dust, smoke, and strong perfumes completely during cough",
      "Honey before bed reduces nighttime cough — take 1 tbsp plain honey at bedtime"
    ],
    flags:["Blood in cough (haemoptysis) — see doctor immediately","Cough lasting more than 3 weeks","High fever (>102°F) with green/yellow thick phlegm — possible pneumonia","Severe difficulty breathing or wheezing — possible asthma","Weight loss + night sweats + chronic cough — rule out tuberculosis"]
  },
 
  "Cold / Runny nose":{
    ico:"🤧",diagnosis:"Common Cold — Viral Rhinitis",confidence:"High",
    summary:"The common cold is a viral infection of the upper respiratory tract caused by rhinovirus. It produces a runny/blocked nose as the immune system responds by flooding the nasal passages with mucus. Colds last 5-10 days and resolve on their own. Antibiotics have NO effect on colds.",
    matched:["Cold / Runny nose","Sore throat","Cough","Fatigue","Headache","Watery eyes"],
    home:[
      "🌿 Steam with Ajwain: Add 1 tsp ajwain (carom seeds) to boiling water. Inhale steam with towel over head for 10 min — opens blocked nose almost instantly",
      "🍵 Ginger-Tulsi-Turmeric Tea: 1 inch ginger + 6 tulsi leaves + ¼ tsp turmeric in 1.5 cups water. Boil 7 min, strain, add honey. Drink hot 4x/day",
      "🧄 Raw Garlic: Eat 2-3 raw garlic cloves with honey — allicin in garlic is a powerful natural antiviral",
      "🌊 Saline Nasal Rinse: Mix ¼ tsp salt + pinch of baking soda in 1 cup warm boiled water. Tilt head, pour into one nostril — flushes virus and mucus directly",
      "🛢️ Mustard Oil Nasal Drops: Warm a few drops of mustard oil, put 1-2 drops in each nostril — traditional nasal decongestant, very effective",
      "🧴 Vicks VapoRub: Apply under nose, on chest, and back of neck at bedtime — menthol opens airways during sleep"
    ],
    medicine:[
      "💊 Cetirizine 10mg (Zyrtec/Okacet) — Take 1 tablet at night. Dries runny nose and reduces sneezing without drowsiness",
      "💊 Levocetrizine 5mg (Xyzal) — Stronger antihistamine, very effective for runny nose, take at bedtime",
      "💊 Phenylephrine Nasal Spray (Nasivion/Otrivin) — Use 1-2 sprays per nostril, max 3 days only — powerful decongestant",
      "💊 Paracetamol 500mg (Crocin) — For associated fever or sinus headache",
      "💊 Zinc supplement 50mg — Reduces cold duration by up to 33% if taken within first 24 hours",
      "🩺 NO antibiotics needed — colds are 100% viral. Antibiotics do not help and cause harm"
    ],
    lifestyle:[
      "Drink warm fluids all day (warm water, soups, teas) — thins nasal mucus",
      "Rest and sleep 9 hours — immune system is most active during sleep",
      "Vitamin C-rich foods daily: amla, guava, citrus — boosts immunity and shortens cold",
      "Wash hands frequently and avoid touching face — prevent spreading to others"
    ],
    flags:["Symptoms lasting more than 10 days — may have become bacterial sinusitis","Fever above 102°F with cold symptoms","Green/yellow discharge from only one nostril","Swelling around eyes or severe face pain — possible sinus infection","Cold with ear pain (especially in children)"]
  },
 
  "Sore throat":{
    ico:"😮",diagnosis:"Pharyngitis — Sore Throat (Viral or Bacterial)",confidence:"High",
    summary:"A sore throat is painful inflammation of the pharynx. Most cases (70-80%) are viral and resolve in 5-7 days without antibiotics. Bacterial strep throat is less common but needs antibiotics. Key difference: viral sore throat comes with runny nose and mild symptoms; strep throat has severe pain, white patches, and high fever.",
    matched:["Sore throat","Cold / Runny nose","Cough","Fever","Difficulty swallowing","Fatigue"],
    home:[
      "🧂 Warm Salt Water Gargle: Mix ½ tsp rock salt in 1 glass warm water. Gargle for 40-60 seconds. Repeat 5-6 times/day — reduces inflammation and kills surface bacteria",
      "🍯 Honey + Ginger + Black Pepper Lick: Mix 1 tbsp honey + ½ tsp ginger juice + pinch of black pepper. Lick slowly — coats and soothes throat lining, reduces pain within minutes",
      "🌿 Mulethi (Licorice Root) Tea: Boil 2-3 mulethi pieces in 2 cups water for 10 min. Add honey. Drink twice daily — anti-inflammatory, soothes mucous membranes, reduces cough",
      "🌶️ Clove Gargle: Boil 5 cloves in 2 cups water for 10 min. Cool to warm. Gargle or sip slowly — eugenol in cloves is a natural anaesthetic that numbs throat pain",
      "🥛 Turmeric + Honey Warm Milk: Mix ½ tsp turmeric + 1 tbsp honey in warm milk. Drink at bedtime — antibacterial, anti-inflammatory",
      "🍋 Warm Lemon Water with Honey: Mix juice of ½ lemon + 1 tbsp honey in warm water. Sip slowly throughout the day"
    ],
    medicine:[
      "💊 Strepsils Lozenges (Amylmetacresol) — Suck slowly 1 lozenge every 3-4 hours, max 8/day. Antiseptic and soothing",
      "💊 Benzydamine Gargle (Tantum Verde) — Dilute and gargle 15ml every 3 hours — local anti-inflammatory, very effective",
      "💊 Paracetamol 500mg — For pain relief and fever reduction",
      "💊 Ibuprofen 400mg with food — Stronger anti-inflammatory pain relief for very sore throat",
      "💊 Amoxicillin 500mg 3x/day for 10 days — ONLY if doctor confirms strep throat (bacterial). Not for viral sore throat",
      "🩺 See doctor if: severe pain preventing swallowing saliva, visible white patches + high fever, breathing difficulty"
    ],
    lifestyle:[
      "Drink ONLY warm liquids — herbal tea, warm water, soup. Avoid cold water and ice cream completely",
      "Rest your voice — avoid shouting, prolonged talking, or singing",
      "Eat soft, easy-to-swallow foods — porridge, khichdi, mashed potato, soup",
      "Avoid tobacco smoke and pollution — already inflamed throat is extremely sensitive"
    ],
    flags:["Throat pain so severe you cannot swallow saliva — possible peritonsillar abscess, emergency","White/yellow patches on tonsils + fever above 102°F — likely strep, needs antibiotics urgently","Difficulty breathing or stridor (high-pitched sound while breathing)","Sore throat lasting more than 2 weeks","Sore throat in a child under 5 with drooling — emergency"]
  },
 
  "Fatigue":{
    ico:"😴",diagnosis:"Fatigue — Likely Nutritional Deficiency or Thyroid Imbalance",confidence:"Moderate",
    summary:"Persistent fatigue (feeling tired all the time) is most commonly caused by iron-deficiency anaemia, Vitamin B12 deficiency, Vitamin D deficiency, or hypothyroidism. These are all very common in India, especially in women. All are easily treated once diagnosed. Simple blood tests identify the cause.",
    matched:["Fatigue","Loss of appetite","Dizziness","Difficulty concentrating","Pale skin","Muscle weakness"],
    home:[
      "🥬 Iron-Rich Power Breakfast: Eat a bowl of sautéed spinach with lemon juice + 5 soaked dates + a glass of pomegranate juice — provides iron, Vitamin C (for iron absorption), and natural energy",
      "🥛 Ashwagandha Milk: Mix 1 tsp ashwagandha powder in warm milk with 1 tbsp honey. Drink at night — clinically proven to reduce fatigue, cortisol, and improve energy by 28%",
      "🌿 Moringa (Drumstick) Leaves: Add 1 tbsp moringa leaf powder to smoothie, dal, or warm water daily — extremely rich in iron, B12, and 92 nutrients",
      "🌰 Soaked Nuts Morning Ritual: 5 soaked almonds + 2 walnuts + 1 tsp pumpkin seeds every morning on empty stomach — rich in B vitamins, zinc, and healthy fats for sustained energy",
      "☀️ Morning Sunlight: 15-20 minutes of direct sunlight on skin before 10am — triggers natural Vitamin D production which directly impacts energy levels",
      "🍵 Shatavari + Ashwagandha Tea: Both available in powder form at chemist. Mix ½ tsp each in warm water with honey. Adaptogenic herbs that restore energy"
    ],
    medicine:[
      "🩸 CBC Blood Test — First and essential test. Checks for anaemia, low haemoglobin, and white cell count",
      "🩸 Thyroid Function Test (TSH, T3, T4) — Hypothyroidism causes fatigue in 1 in 10 people. Very treatable",
      "🩸 Vitamin B12, Vitamin D3, Serum Ferritin (iron stores) — Three most common deficiency causes of fatigue in India",
      "💊 Iron + Folic Acid Tablet (Ferrous Sulphate 200mg / Dexorange syrup) — If anaemia confirmed. Take with Vitamin C, not tea/coffee",
      "💊 Vitamin D3 60,000 IU weekly (Calcirol/Uprise D3 sachets) — If Vitamin D deficient. Take with fatty meal",
      "💊 Methylcobalamin 1500mcg (Methycobal/Neurobion Forte) — Vitamin B12 supplement. Take daily for 3 months"
    ],
    lifestyle:[
      "Sleep at consistent times (10pm-6am if possible) — same wake time even on weekends. Irregular sleep causes fatigue regardless of hours",
      "Eat every 3-4 hours — low blood sugar causes extreme fatigue. Never skip breakfast",
      "Cut sugar and refined carbs (white bread, biscuits, maida) — they cause energy spikes followed by severe crashes",
      "Light exercise (20 min walking) actually INCREASES energy — sedentary lifestyle worsens fatigue in a vicious cycle"
    ],
    flags:["Fatigue with chest pain or shortness of breath — possible cardiac or lung issue","Extreme fatigue + weight gain + hair loss + feeling cold — thyroid problem","Fatigue with yellow skin or eyes — possible liver disease","Unexplained weight loss with fatigue — needs urgent investigation","Fatigue so severe you cannot function in daily life"]
  },
 
  "Body ache":{
    ico:"💪",diagnosis:"Viral Myalgia — Body Ache from Viral Infection",confidence:"High",
    summary:"Widespread body ache and muscle pain (myalgia) is a hallmark symptom of viral infections — especially influenza (flu), dengue, chikungunya, or COVID-19. The virus triggers immune cells to release cytokines, causing muscle inflammation. Rest and hydration are the most important treatments.",
    matched:["Body ache","Fever","Fatigue","Chills","Muscle weakness","Joint pain"],
    home:[
      "🛁 Epsom Salt Bath: Dissolve 2 cups Epsom salt (magnesium sulphate — available at chemist) in warm bathwater. Soak for 20-25 min — magnesium absorbs through skin, directly relaxes muscle fibres",
      "🌿 Turmeric-Ginger Oil Massage: Mix 1 tbsp turmeric powder + 1 tbsp grated ginger with warm mustard oil into a paste. Massage into aching muscles for 10 min, cover with cloth for 30 min",
      "🔥 Clove Oil Massage: Mix 10 drops clove oil in 3 tbsp coconut oil. Massage into aching areas — eugenol in cloves is a natural COX-2 inhibitor (same mechanism as Ibuprofen)",
      "🍵 Anti-Inflammatory Broth: Boil 1 inch ginger + 1 tsp turmeric + 1 tsp pepper + garlic in water. Strain and drink warm 3x/day — reduces systemic inflammation",
      "💧 Methi (Fenugreek) Water: Soak 1 tbsp fenugreek seeds overnight, drink the water next morning — reduces inflammation and body temperature",
      "🛌 Complete Bed Rest + Warmth: Wear comfortable warm clothes. Use a hot water bottle on worst aching areas. Your body heals fastest during rest"
    ],
    medicine:[
      "💊 Paracetamol 650mg (Dolo 650) — Every 6-8 hours. Reduces pain and fever simultaneously. Most commonly prescribed",
      "💊 Ibuprofen 400mg (Brufen) with food — Anti-inflammatory, very effective for muscle pain. Take every 8 hours",
      "💊 Combiflam tablet (Ibuprofen + Paracetamol) — For severe body ache. Take after food",
      "💊 ORS (Electral powder) sachets — Mix 1 sachet in 1 litre water. Sip throughout day — replaces electrolytes lost through fever and sweating",
      "💊 Thiocolchicoside 4mg (Myoril) — Muscle relaxant for very severe muscle pain. Take twice daily with food",
      "🩺 Do a dengue NS1 Antigen test and blood test if body ache + high fever persists beyond 3 days — dengue needs immediate medical care"
    ],
    lifestyle:[
      "Complete bed rest for 2-3 days — do not push through the pain",
      "Eat light foods: khichdi, dal-rice, vegetable soup. Avoid heavy protein during acute illness",
      "Drink warm water every 30 minutes throughout the day",
      "Keep room temperature comfortable — neither too hot nor too cold"
    ],
    flags:["Severe body ache + fever + rash — possible dengue or chikungunya, see doctor immediately","Extreme muscle weakness where you cannot stand — possible myositis","Body ache lasting more than 2 weeks without improvement","Body ache with yellow skin — possible hepatitis"]
  },
 
  "Nausea":{
    ico:"🤢",diagnosis:"Nausea — Likely Gastritis or Viral Gastroenteritis",confidence:"Moderate",
    summary:"Nausea is an unpleasant sensation of wanting to vomit. Common causes include indigestion, food poisoning, viral gastroenteritis (stomach bug), acid reflux, motion sickness, or medication side effects. The most important thing during nausea is preventing dehydration by sipping fluids frequently.",
    matched:["Nausea","Vomiting","Stomach pain","Loss of appetite","Bloating","Diarrhoea"],
    home:[
      "🫚 Fresh Ginger: Chew a small piece of raw ginger OR drink ginger tea with honey — most studied natural anti-nausea remedy. Works within 20 min",
      "🌿 Fennel Seeds (Saunf): Chew ½ tsp roasted saunf slowly OR boil in water and drink as tea — settles stomach, reduces gas and cramps",
      "🍋 Lemon Smell + Cold Lemon Water: Smell a freshly cut lemon for 1-2 min OR sip cold lemon water slowly — smell of citrus reduces nausea sensation quickly",
      "🍵 Peppermint Tea: Steep peppermint leaves in hot water for 5 min. Sip slowly — relaxes stomach muscles, reduces nausea and gas",
      "🧂 Ginger + Salt + Lemon: Mix juice of ½ lemon + pinch of salt + ½ tsp ginger juice + 1 tsp honey in ½ cup water. Sip slowly",
      "🍞 Dry Plain Toast or Crackers: Eating something bland and dry settles an upset stomach — the BRAT diet (Banana, Rice, Applesauce, Toast) is ideal"
    ],
    medicine:[
      "💊 Ondansetron 4mg (Emeset/Vomikind) — Dissolve under tongue for fast action. Most effective anti-nausea medicine. Take 1 tablet every 8 hours",
      "💊 Domperidone 10mg (Domstal/Vomistop) — Take 30 min before meals. Improves gut motility and reduces nausea",
      "💊 Metoclopramide 10mg (Perinorm) — Take before meals. Helps move food through stomach faster",
      "💊 ORS Sachets (Electral/Pedialyte) — Mix in water and sip 1 cup every hour to prevent dehydration",
      "💊 Rantac 150mg (Ranitidine) OR Pan-D (Pantoprazole + Domperidone) — If nausea is from acid reflux/gastritis. Take before food",
      "🩺 See doctor immediately: vomiting blood, severe abdominal pain, signs of dehydration, nausea in early pregnancy, or nausea with severe headache"
    ],
    lifestyle:[
      "Eat small meals every 2-3 hours — empty stomach makes nausea worse",
      "Avoid fatty, fried, spicy, or strong-smelling foods until fully recovered",
      "Sit upright for 30 min after eating — do not lie down immediately",
      "Fresh cool air helps — open a window or step outside briefly"
    ],
    flags:["Vomiting blood or coffee-ground material — emergency","Severe abdominal pain with nausea — possible appendicitis","Signs of dehydration: no urination for 8+ hours, dry mouth, extreme weakness","Nausea with severe headache + neck stiffness","Vomiting for more than 24 hours in adults, 12 hours in children"]
  },
 
  "Diarrhoea":{
    ico:"🚽",diagnosis:"Acute Diarrhoea — Gastroenteritis",confidence:"High",
    summary:"Diarrhoea (3 or more loose stools per day) is most commonly caused by viral gastroenteritis, food poisoning, or bacterial infection. The most dangerous complication is dehydration. Preventing dehydration with ORS is far more important than stopping the diarrhoea immediately.",
    matched:["Diarrhoea","Nausea","Vomiting","Stomach pain","Fatigue","Loss of appetite"],
    home:[
      "🧂 ORS (Oral Rehydration Salt) — Make at home: mix ½ tsp salt + 6 tsp sugar in 1 litre clean water. Drink 200ml after every loose stool — most important treatment",
      "🍚 Rice Water (Kanji): Boil 1 cup rice in 3 cups water, strain, drink the starchy water. Add pinch of salt — soothes gut and firms stools",
      "🍌 Ripe Banana: Eat 2-3 ripe bananas throughout the day — pectin in banana absorbs excess fluid, potassium replaces lost electrolytes",
      "🍵 Curd + Cumin (Jeera) Buttermilk: Mix 1 cup curd in water with 1 tsp roasted cumin powder + pinch of salt. Drink 3x/day — probiotic cultures restore healthy gut bacteria",
      "🌿 Psyllium Husk (Isabgol): Mix 1 tbsp isabgol in a glass of curd or water. Drink immediately — absorbs water in the gut, forms a soft bulk",
      "🧄 Ginger + Coriander Tea: Boil 1 inch ginger + 1 tbsp coriander seeds in 2 cups water. Strain, add pinch of salt. Drink warm — reduces gut inflammation"
    ],
    medicine:[
      "💊 ORS Sachets (Electral) — Most important. 1 sachet in 1 litre water. Drink 200ml after every loose stool",
      "💊 Loperamide 2mg (Eldoper/Imodium) — Slows gut movement. Take after first loose stool. Do NOT use if there is blood in stool or high fever",
      "💊 Racecadotril 100mg (Redotil) — Reduces secretion without slowing gut. Safer than Loperamide",
      "💊 Norfloxacin 400mg + Tinidazole 600mg (Norflox-TZ) — For bacterial or parasitic diarrhoea. Take twice daily with food for 5 days",
      "💊 Probiotic capsules (Sporlac / Vibact) — Restore gut bacteria. Take 2 capsules twice daily for 5 days",
      "🩺 See doctor if: blood or mucus in stool, fever above 102°F, more than 10 stools/day, diarrhoea in children under 2"
    ],
    lifestyle:[
      "BRAT diet: Banana, Rice, Applesauce, Toast — bland foods that are easy on the stomach",
      "Avoid dairy, fatty foods, spicy food, alcohol, and caffeine until fully recovered",
      "Drink fluids continuously — you lose a lot with each loose stool",
      "Wash hands thoroughly with soap before eating and after toilet — most diarrhoea is preventable"
    ],
    flags:["Blood or mucus in stool — doctor immediately","Fever above 102°F with diarrhoea","Signs of severe dehydration: sunken eyes, no urination, extreme weakness, confusion","More than 10 stools in one day","Diarrhoea in infants or elderly lasting more than 24 hours"]
  },
 
  "Joint pain":{
    ico:"🦴",diagnosis:"Arthralgia — Joint Pain (Inflammatory or Wear-and-Tear)",confidence:"Moderate",
    summary:"Joint pain (arthralgia) can come from osteoarthritis (wear and tear, common after 40), rheumatoid arthritis (autoimmune), gout (uric acid crystals), post-viral arthritis after chikungunya/dengue, or vitamin D deficiency. Identifying whether it is one joint or multiple, with morning stiffness, helps narrow the cause.",
    matched:["Joint pain","Swelling in joints","Stiffness","Body ache","Fatigue","Back pain"],
    home:[
      "🥛 Turmeric Golden Milk: Boil ½ tsp turmeric + ¼ tsp ginger powder + pinch of black pepper in milk. Drink daily — curcumin is one of the most studied natural anti-inflammatories",
      "🛢️ Castor Oil + Warm Compress: Warm castor oil, massage into painful joints. Cover with warm cloth and leave for 1 hour — reduces swelling and inflammation",
      "🧄 Mustard Oil + Garlic Massage: Heat mustard oil with 4-5 crushed garlic cloves until garlic turns brown. Cool to warm. Massage joints daily — traditional Ayurvedic joint pain treatment",
      "🧊🔥 Hot and Cold Therapy: Ice pack for 15 min on acute swollen joint; warm compress for 15 min on stiff, aching joints. Alternate. Use 3-4 times/day",
      "🌿 Methi (Fenugreek) Seeds: Soak 1 tbsp overnight, eat with warm water in morning — reduces uric acid and joint inflammation. Especially helpful for gout",
      "💊 Shallaki (Boswellia) + Ashwagandha: Both available as capsules. Take as directed — clinically proven to reduce joint pain and inflammation"
    ],
    medicine:[
      "💊 Ibuprofen 400mg (Brufen) with food — First choice for joint pain. Anti-inflammatory. Take every 8 hours with food",
      "💊 Diclofenac 50mg (Voveran) with food + Pantoprazole — Stronger anti-inflammatory, protect stomach with pantoprazole",
      "💊 Glucosamine 500mg + Chondroitin 400mg (Rejoint/Osteofit) — For knee/hip osteoarthritis. Takes 4-6 weeks to show effect",
      "💊 Uric acid blood test — If big toe, ankle, or knee joint affected. Gout is common and treated with Allopurinol 100-300mg daily",
      "💊 Calcium 500mg + Vitamin D3 1000IU (Shelcal) — Essential for joint and bone health",
      "🩺 Rheumatoid Factor (RF) and anti-CCP blood tests — if multiple small joints of hands are affected with morning stiffness"
    ],
    lifestyle:[
      "Low-impact exercise: swimming, cycling, walking — keeps joints mobile without stress. Even 20 min walking daily helps",
      "Anti-inflammatory diet: omega-3 rich foods (flaxseed, walnuts, fish), olive oil. Reduce red meat and refined sugar",
      "Maintain healthy weight — every extra kg puts 4kg extra pressure on knee joints",
      "Avoid high-purine foods if gout: red meat, organ meats, alcohol, beer, shellfish, spinach"
    ],
    flags:["Sudden severe joint pain + swelling + fever + warmth — possible septic arthritis, emergency","Joint deformity developing over weeks","Joint pain in a child — paediatric specialist needed","Joint pain after rash or tick bite — possible reactive arthritis or Lyme disease"]
  },
 
  "Back pain":{
    ico:"🔙",diagnosis:"Mechanical Back Pain — Postural / Musculoskeletal",confidence:"High",
    summary:"Back pain is the most common musculoskeletal complaint worldwide. Over 90% of cases are mechanical — caused by poor posture, sedentary lifestyle, muscle strain, or disc problems. The good news: most episodes resolve within 4-6 weeks with the right treatment. Movement and exercise are better than bed rest.",
    matched:["Back pain","Stiffness","Neck pain","Fatigue","Muscle weakness","Body ache"],
    home:[
      "🔥❄️ Hot-Cold Alternating Therapy: First 48 hours: ice pack 15 min every 2 hours (reduces inflammation). After 48 hours: heating pad 20 min 3x/day (relaxes muscles). Alternating = maximum relief",
      "🧘 Cat-Cow Yoga Stretch: On all fours, inhale while arching back down, exhale while rounding back up. Do 10 slow repetitions every morning — most effective stretch for lower back",
      "🧘 Child's Pose: Kneel, sit back on heels, stretch arms forward on floor, hold 30 sec — decompresses spine",
      "🌿 Ginger + Turmeric Anti-Inflammatory Paste: Mix 1 tbsp each of ginger and turmeric powder with warm mustard oil. Apply on back, massage gently. Cover with warm cloth for 30 min",
      "🧂 Epsom Salt Bath: 2 cups Epsom salt in warm bath. Soak 20 min — magnesium relaxes back muscles effectively",
      "🪑 Posture Correction: Sit with lower back supported, feet flat on floor, screen at eye level. Roll a towel and place at the curve of your lower back — immediate tension relief"
    ],
    medicine:[
      "💊 Ibuprofen 400mg (Brufen) with food — Best first choice. Anti-inflammatory, take every 8 hours",
      "💊 Diclofenac Gel (Voveran Emulgel) — Apply on painful area 3-4 times/day, massage gently — local pain relief without affecting stomach",
      "💊 Thiocolchicoside 4mg + Aceclofenac 100mg (Myprodol/Dolowin Plus) — Muscle relaxant combination. Very effective for spasm-type back pain",
      "💊 Methyl Salicylate + Menthol Cream (Volini Gel / Moov) — Apply and massage on back 4x/day — immediate cooling and pain relief",
      "🩺 Physiotherapy — 6-10 sessions with a physiotherapist dramatically improve chronic back pain",
      "🩺 See doctor / get MRI if: pain shoots down the leg (sciatica), numbness in legs, or bladder/bowel problems with back pain"
    ],
    lifestyle:[
      "Do NOT stay in bed rest for more than 2 days — prolonged rest weakens back muscles and makes pain worse",
      "Walk 20-30 min daily — the single most beneficial activity for back pain",
      "Sleep on your side with a pillow between knees — reduces spinal compression",
      "Avoid lifting heavy objects. When lifting, bend at knees not waist — keep object close to body"
    ],
    flags:["Back pain + loss of bladder or bowel control — medical emergency (cauda equina syndrome)","Pain shooting down the leg to below the knee — sciatica, needs physiotherapy/imaging","Back pain after trauma or fall","Progressive weakness in legs with back pain","Back pain that is worse at night and in the morning — may be inflammatory arthritis"]
  },
 
  "Skin rash":{
    ico:"🧴",diagnosis:"Skin Rash — Contact Dermatitis or Allergic Reaction",confidence:"Moderate",
    summary:"Skin rashes have many causes: allergic reactions (contact dermatitis), eczema, fungal infections, viral rashes (chickenpox, measles), heat rash, or autoimmune conditions. Identifying the pattern, location, and what triggered it is key. Most rashes respond well to topical treatment.",
    matched:["Skin rash","Itching","Dry skin","Eye redness","Swelling in joints"],
    home:[
      "🌿 Aloe Vera Gel: Apply fresh aloe vera gel (scoop from leaf) directly on rash. Leave on 30 min, rinse with cool water. Do 3x/day — most soothing and anti-inflammatory natural remedy",
      "🧴 Coconut Oil: Apply virgin coconut oil on rash and leave overnight — antimicrobial, moisturising, reduces inflammation",
      "🌼 Chamomile Tea Compress: Brew strong chamomile tea, cool to room temperature, soak cloth and apply as compress 15 min — antihistamine properties",
      "🧊 Cold Compress: Apply ice wrapped in cloth on itchy area for 10 min — reduces itching and inflammation immediately",
      "🌿 Neem Leaves Paste: Grind fresh neem leaves with water into paste. Apply on rash 20 min. Rinse — powerful antifungal and antibacterial",
      "🛁 Oatmeal Bath: Add 2 cups colloidal oatmeal (or finely ground regular oats) to lukewarm bath. Soak 15-20 min — extremely soothing for itchy rash"
    ],
    medicine:[
      "💊 Cetirizine 10mg (Zyrtec) at bedtime — Antihistamine for allergic rash. Reduces itching and swelling within 1-2 hours",
      "💊 Levocetrizine 5mg (Xyzal) — Stronger antihistamine with less drowsiness",
      "🧴 Hydrocortisone Cream 1% (available OTC) — Apply thin layer on rash twice daily for max 7 days — reduces inflammation for contact dermatitis",
      "🧴 Clotrimazole Cream (Candid B) — For fungal rash (ringworm, tinea) in skin folds. Apply twice daily for 2-4 weeks",
      "🧴 Calamine Lotion — Apply on itchy rash freely. Cooling, soothing, dries oozing rash",
      "🩺 See dermatologist if: rash spreads rapidly, blisters, fever with rash, rash doesn't improve in 7 days"
    ],
    lifestyle:[
      "Identify and avoid trigger: new soap, detergent, food, fabric, jewelry — eliminate one at a time",
      "Wear loose, 100% cotton clothing on affected areas — synthetic fabrics worsen rash",
      "Keep nails short and clean — scratching introduces bacteria and worsens rash",
      "Use fragrance-free, hypoallergenic soap and moisturiser"
    ],
    flags:["Rash + high fever + widespread blistering — emergency","Rash with difficulty breathing — anaphylaxis, call emergency","Rapidly spreading rash with pain — possible cellulitis","Rash that looks like a bull's-eye — possible Lyme disease (if in tick-prone area)","Rash on face with joint pain and butterfly pattern — lupus, see doctor"]
  },
 
  "Irregular periods":{
    ico:"🩸",diagnosis:"Irregular Menstrual Cycle — Hormonal Imbalance",confidence:"High",
    summary:"Irregular periods (cycles shorter than 21 days, longer than 35 days, or unpredictable) are extremely common and usually caused by PCOS, thyroid disorders, stress, significant weight changes, or perimenopause. Most causes are very treatable once identified. A hormonal blood test and pelvic ultrasound are the key diagnostic steps.",
    matched:["Irregular periods","Bloating before periods","Mood swings / PMS","Hormonal acne","Weight gain","Hair loss"],
    home:[
      "🍵 Cinnamon Tea Daily: Boil 1 tsp cinnamon powder in 1 cup water for 5 min. Add honey and a pinch of ginger. Drink every morning — regulates insulin (key for PCOS), reduces androgen levels, and promotes regular cycles",
      "🌿 Ginger + Jaggery Tea: Boil 1 inch fresh ginger in 2 cups water. Add jaggery (not sugar) to taste. Drink 2x/day especially in the second half of cycle — stimulates blood flow to uterus",
      "🥭 Unripe Papaya: Eat unripe green papaya as vegetable (sabzi) or raw daily for 2-3 weeks — papain enzyme stimulates uterine contractions and estrogen",
      "🌱 Seed Cycling Protocol: Days 1-14: 1 tbsp freshly ground flaxseed + 1 tbsp raw pumpkin seeds. Days 15-28: 1 tbsp sesame seeds + 1 tbsp sunflower seeds. Add to food or smoothie — balances estrogen and progesterone",
      "🌿 Shatavari Powder: Mix 1 tsp shatavari in warm milk with honey at bedtime — Ayurvedic herb proven to balance female reproductive hormones",
      "🧘 Yoga Daily (20 min): Butterfly pose, Supta Baddha Konasana, Viparita Karani, Malasana — these poses specifically stimulate reproductive organs and regulate the HPA-HPG hormone axis"
    ],
    medicine:[
      "🩸 Essential Blood Tests: FSH, LH, Estradiol, Progesterone, Prolactin, AMH, Testosterone, DHEA-S — full hormonal panel",
      "🩸 Thyroid Function Test (TSH, Free T3, Free T4) — Hypothyroidism is one of the most common and overlooked causes of irregular periods",
      "📷 Pelvic Ultrasound — Checks for PCOS (polycystic ovaries), fibroids, ovarian cysts, endometrial thickness",
      "💊 Duphaston (Dydrogesterone 10mg) / Susten 200 — Progesterone supplement to regulate cycle. Take as prescribed by gynaecologist",
      "💊 Combined OCP (Yasmin/Loette/Femilon) — Regulates cycle, treats PCOS symptoms, reduces acne and cramps. Needs gynaecologist prescription",
      "💊 Levothyroxine — If hypothyroidism confirmed, this directly restores regular periods within 1-3 months"
    ],
    lifestyle:[
      "Maintain BMI between 18.5-24.9 — both underweight and overweight significantly disrupt ovulation and cycle regularity",
      "Stress management is critical — high cortisol directly suppresses LH and FSH, disrupting ovulation",
      "Sleep 7-9 hours at consistent times — melatonin and reproductive hormones are deeply interconnected",
      "Reduce processed food, refined sugar, and dairy if PCOS is suspected — all spike insulin which drives androgen production"
    ],
    flags:["No period for 3+ consecutive months (amenorrhoea) without pregnancy — needs medical evaluation urgently","Sudden complete change in cycle pattern after years of regularity","Irregular periods with excessive facial or body hair + acne + weight gain — PCOS assessment needed","Bleeding between periods or after intercourse"]
  },
 
  "Painful periods":{
    ico:"🩸",diagnosis:"Dysmenorrhoea — Painful Menstruation",confidence:"High",
    summary:"Period pain (dysmenorrhoea) affects up to 80% of women and is the leading cause of missed school and work days in women. Primary dysmenorrhoea has no underlying disease — prostaglandins cause uterine contractions. Secondary dysmenorrhoea is caused by endometriosis or fibroids. Both are very treatable.",
    matched:["Painful periods","Bloating before periods","Back pain","Nausea","Fatigue","Mood swings / PMS"],
    home:[
      "🔥 Heat Pad on Lower Abdomen: Apply a hot water bottle or heating pad to lower abdomen for 20-30 min — clinical trials show heat is as effective as Ibuprofen for period pain. Use from 1 day before expected period",
      "🍵 Fennel Seed Tea (Saunf): Boil 1 tsp fennel seeds in 1 cup water for 5 min. Add honey. Drink warm 3x/day starting 2 days before period — antispasmodic, reduces uterine cramping",
      "🌿 Ginger Tea with Jaggery: Boil 1 inch ginger, add jaggery. Drink 3-4 times/day starting 2 days before period — reduces prostaglandin production by up to 25%",
      "🐟 Omega-3 Rich Foods: Eat flaxseeds, walnuts, chia seeds, fatty fish daily throughout the month — omega-3 reduces prostaglandin levels over time, significantly reducing period pain",
      "🛢️ Sesame Oil Abdominal Massage: Warm sesame oil slightly. Massage on lower abdomen in gentle clockwise circles for 10 min — relaxes uterine muscles",
      "🧘 Yoga Poses: Child's Pose, Reclining Bound Angle (Supta Baddha Konasana), Cat-Cow — hold each 30-60 seconds. Gentle movement during periods significantly reduces pain"
    ],
    medicine:[
      "💊 Mefenamic Acid 500mg (Meftal-Spas / Ponstan) — Best first choice for period pain. Start 1-2 DAYS BEFORE your period begins, not after pain starts. Take every 8 hours with food",
      "💊 Ibuprofen 400mg (Brufen) every 8 hours with food — Highly effective prostaglandin inhibitor",
      "💊 Drotaverine 40mg (No-Spa / Drotin) — Antispasmodic. Specifically relaxes uterine smooth muscle cramps",
      "💊 Combiflam (Ibuprofen + Paracetamol) — For moderate period pain with backache",
      "💊 Combined OCP — Significantly reduces period pain by thinning uterine lining and suppressing ovulation. Needs gynaecologist prescription",
      "🩺 See gynaecologist if pain is not controlled by Mefenamic acid + Drotaverine, or if pain occurs outside of period days — may indicate endometriosis"
    ],
    lifestyle:[
      "Start pain medicine 1-2 days before period begins — prevents prostaglandins from building up. Do NOT wait for pain to become severe",
      "Cut salt, sugar, and caffeine in the week before period — significantly reduces bloating and cramping",
      "Magnesium supplement 300-400mg daily — clinical studies show magnesium reduces period pain by relaxing uterine muscle",
      "Light exercise (walking, gentle yoga) in days leading up to period reduces cramping on period day"
    ],
    flags:["Period pain not relieved by Ibuprofen + Mefenamic acid — may indicate endometriosis","Pelvic pain throughout the month, not just during period","Pain during sexual intercourse — possible endometriosis or ovarian cyst","Sudden severe pelvic pain with missed period — possible ectopic pregnancy, emergency","Heavy bleeding + severe pain + fever — possible pelvic inflammatory disease (PID)"]
  },
 
  "PCOS symptoms":{
    ico:"🩸",diagnosis:"Polycystic Ovary Syndrome (PCOS)",confidence:"Moderate",
    summary:"PCOS is the most common hormonal disorder in women of reproductive age, affecting 1 in 5 women. It involves insulin resistance, excess androgen hormones, and irregular ovulation. It is highly manageable with lifestyle changes — even a 5-10% weight loss can restore regular periods and significantly improve symptoms.",
    matched:["PCOS symptoms","Irregular periods","Hormonal acne","Weight gain","Excessive facial or body hair","Hair loss"],
    home:[
      "🌿 Spearmint Tea: Drink 2 cups of spearmint herbal tea daily — multiple clinical studies show spearmint significantly reduces free testosterone within 30 days, improving acne and facial hair",
      "🍵 Cinnamon + Warm Water: Take 1 tsp cinnamon powder in warm water every morning before breakfast — improves insulin sensitivity in PCOS patients, helps regulate cycle",
      "🌱 Low-GI Diet Overhaul: Replace white rice/bread/maida with brown rice, oats, millets (ragi, bajra, jowar), and lentils. This single change reduces insulin spikes that drive all PCOS symptoms",
      "🥗 Flaxseed Daily: Add 1-2 tbsp freshly ground flaxseed to food daily — binds excess androgens (testosterone) in the gut and reduces free testosterone levels",
      "🍎 Apple Cider Vinegar: Mix 1 tbsp ACV in a full glass of water before meals — improves insulin sensitivity. Start with ½ tbsp to avoid stomach upset",
      "🏃 Exercise 30 Min Daily: Brisk walking + strength training (even bodyweight) improves insulin sensitivity within 4-6 weeks, more effectively than metformin in early PCOS"
    ],
    medicine:[
      "💊 Metformin 500-1500mg (Glycomet) — Cornerstone of PCOS treatment. Improves insulin resistance, lowers testosterone, regularises periods. Take with meals",
      "💊 Combined OCP (Yasmin/Diane-35/Femilon) — Regulates menstrual cycle, dramatically reduces acne and facial hair, and protects uterine lining",
      "💊 Spironolactone 25-100mg — Reduces excess facial/body hair and hormonal acne by blocking androgens. Needs prescription",
      "💊 Inositol (Myo-inositol + D-chiro-inositol 40:1) — Supplement, clinically proven to improve insulin sensitivity and restore ovulation in PCOS",
      "🩸 Essential tests: LH:FSH ratio, testosterone, DHEAS, AMH, fasting insulin, fasting glucose, pelvic ultrasound",
      "🩺 See gynaecologist/endocrinologist for personalised PCOS management plan"
    ],
    lifestyle:[
      "Weight loss of 5-10% of body weight restores ovulation and regular periods in over 60% of women with PCOS — the single most impactful intervention",
      "Completely eliminate sugar, soft drinks, processed foods, and refined carbohydrates — they drive insulin resistance which is the root cause of PCOS",
      "Sleep 7-9 hours consistently — poor sleep worsens insulin resistance significantly",
      "Stress management: yoga, meditation, deep breathing — high cortisol worsens all PCOS symptoms"
    ],
    flags:["Difficulty conceiving after 6+ months of trying — fertility specialist needed","Fasting blood sugar above 100 mg/dL — pre-diabetes developing","Severe excess hair growth with voice deepening — very high androgens, urgent evaluation","Depression and anxiety are very common with PCOS — seek support if feeling overwhelmed"]
  },
 
  "Acne":{
    ico:"😤",diagnosis:"Acne Vulgaris — Hormonal or Bacterial Origin",confidence:"High",
    summary:"Acne occurs when hair follicles become clogged with sebum (oil) and dead skin cells, allowing bacteria to grow. In teenagers it is driven by puberty hormones; in adult women it is often linked to PCOS, the menstrual cycle, or stress. Diet, dairy, and high-sugar foods are major triggers.",
    matched:["Acne","Hormonal acne","Skin rash","Hair loss","Excessive facial or body hair"],
    home:[
      "🌿 Tea Tree Oil Spot Treatment: Mix 1 drop tea tree oil + 9 drops jojoba or coconut oil. Apply directly on pimple with cotton bud. Leave overnight — clinical studies show as effective as 5% Benzoyl Peroxide",
      "🌱 Fresh Aloe Vera Gel: Scoop fresh aloe gel from leaf, apply on entire face or just on acne spots. Leave overnight or 30 min — anti-inflammatory, healing, reduces redness",
      "🍃 Neem Paste: Grind 10-15 fresh neem leaves with water into paste. Apply on acne 20 min, rinse with cool water 2x/week — powerful antibacterial against Propionibacterium acnes",
      "🍯 Honey + Cinnamon Mask: Mix 2 tbsp raw honey + 1 tsp cinnamon powder. Apply on face 15-20 min, rinse — honey is antibacterial, cinnamon is antimicrobial",
      "🧊 Ice Compress: Wrap ice in cloth, hold on inflamed pimple for 5 min — reduces redness, swelling, and pain of a pimple immediately",
      "🥗 Eliminate Dairy + Sugar: Cut out dairy products and high-GI foods (sugar, white bread, biscuits) — clinical studies show 70% of people see significant improvement within 4-6 weeks"
    ],
    medicine:[
      "🧴 Benzoyl Peroxide 2.5% Gel (Persol AC) — Apply thin layer on acne-affected areas at night. Kills acne bacteria. Start with 2.5% to avoid dryness",
      "🧴 Adapalene 0.1% Gel (Adaferin/Differin) — Apply at night with moisturiser. Retinoid that unclogs pores and prevents new acne formation. Takes 8-12 weeks",
      "🧴 Clindamycin 1% Gel (Clincin) — Antibiotic gel for inflamed pimples. Apply twice daily",
      "💊 Doxycycline 100mg — For moderate-severe acne. Take once daily for 3 months. Needs dermatologist prescription",
      "💊 For hormonal acne in women: Spironolactone 50-100mg OR Diane-35/Yasmin OCP — dramatically improves hormonal acne",
      "💊 Isotretinoin (Accutane/Acutret) — For severe cystic acne only. Very effective but needs dermatologist monitoring"
    ],
    lifestyle:[
      "Wash face with gentle, non-comedogenic cleanser only twice daily — over-washing stimulates more oil production",
      "NEVER pop or squeeze pimples — this pushes bacteria deeper, causes scarring, and spreads infection",
      "Change pillowcase every 2-3 days — pillow harbours bacteria, sweat, and oil",
      "Apply SPF 30 sunscreen daily — UV exposure darkens acne marks and scars permanently"
    ],
    flags:["Large, painful cystic acne covering face, chest, or back — see dermatologist","Acne in adult women with irregular periods and excess hair — PCOS evaluation needed","Acne with fever or warm skin — possible skin infection","Severe scarring developing — early aggressive treatment prevents permanent marks"]
  },
 
  "Anxiety":{
    ico:"😰",diagnosis:"Anxiety / Generalised Anxiety Disorder",confidence:"Moderate",
    summary:"Anxiety is excessive worry and nervousness that can manifest as racing thoughts, heart palpitations, sweating, and restlessness. It is extremely common — affecting 1 in 4 people at some point. Stress, lifestyle factors, nutritional deficiencies (B12, magnesium), and gut health all play roles. Very treatable.",
    matched:["Anxiety","Insomnia","Irregular heartbeat","Palpitations","Fatigue","Difficulty concentrating","Headache"],
    home:[
      "🧘 4-7-8 Breathing (Instant Calm): Inhale for 4 counts, hold for 7 counts, exhale for 8 counts. Repeat 4 times — activates parasympathetic nervous system within 2 minutes",
      "🍵 Ashwagandha Tea: Mix 1 tsp ashwagandha powder in warm milk with honey at night — clinically proven to reduce cortisol by 27% and anxiety by 44% within 8 weeks",
      "🌼 Chamomile Tea: Steep 2 chamomile tea bags in hot water 5 min. Drink 2-3 cups/day — contains apigenin which binds to same brain receptors as anti-anxiety medications",
      "🌿 Brahmi (Bacopa Monnieri) Powder: Mix ½ tsp in warm milk with honey at bedtime — Ayurvedic herb proven to reduce anxiety and improve cognitive function",
      "🛁 Lavender Oil Bath: Add 10 drops lavender essential oil to warm bath. Soak 20 min — aromatherapy with lavender is clinically proven to reduce anxiety",
      "📓 Worry Journal: Write down all worries before bed — transferring worries from mind to paper reduces anxiety and improves sleep quality significantly"
    ],
    medicine:[
      "💊 Magnesium Glycinate 300-400mg at bedtime — Magnesium deficiency is linked to anxiety. Supplement relieves muscle tension and promotes calm",
      "💊 Vitamin B Complex (Neurobion/Becosules) — B vitamins are essential for neurotransmitter production. B12 and B6 deficiency worsens anxiety",
      "💊 Buspirone 5-10mg — Non-sedating anti-anxiety medication. Takes 2-4 weeks to work. Needs doctor prescription",
      "💊 Sertraline 25-50mg (Zoloft) OR Escitalopram 5-10mg — SSRIs, first-line treatment for chronic anxiety. Needs psychiatrist/doctor prescription",
      "💊 Clonazepam 0.25-0.5mg — For acute panic attacks only. Short-term use. Needs prescription. Can be habit-forming",
      "🩺 See psychiatrist or psychologist — CBT (Cognitive Behavioural Therapy) is as effective as medication for anxiety with no side effects"
    ],
    lifestyle:[
      "Exercise 30 min daily — proven to reduce anxiety as effectively as medication. Any aerobic exercise works",
      "Limit caffeine to 1 cup/day or eliminate completely — caffeine directly increases anxiety and heart rate",
      "Sleep 7-9 hours — sleep deprivation is one of the most powerful anxiety triggers",
      "Reduce social media and news consumption — constant stimulation keeps the nervous system in fight-or-flight"
    ],
    flags:["Panic attacks with chest pain, shortness of breath, feeling of dying — rule out cardiac cause","Anxiety preventing normal daily functioning for weeks","Thoughts of self-harm — please reach out to a mental health professional immediately","Anxiety with sudden onset after age 50 — needs medical investigation for underlying cause"]
  },
 
  "Insomnia":{
    ico:"🌙",diagnosis:"Insomnia — Sleep Disorder (Stress / Lifestyle Related)",confidence:"High",
    summary:"Insomnia is difficulty falling asleep, staying asleep, or waking too early. It affects 30% of adults. Most insomnia is linked to stress, anxiety, poor sleep hygiene, excessive screen use, caffeine, or irregular schedules. Chronic insomnia can be treated very effectively with CBT-I (cognitive behavioural therapy for insomnia) and simple habit changes.",
    matched:["Insomnia","Anxiety","Fatigue","Headache","Difficulty concentrating","Night sweats"],
    home:[
      "🥛 Ashwagandha + Nutmeg Milk: Warm 1 cup milk, add 1 tsp ashwagandha powder + a pinch of freshly grated nutmeg (jaiphal) + honey. Drink 45 min before bed — proven to improve sleep onset and quality",
      "🍵 Chamomile Tea: Steep 2 bags of chamomile tea 10 min. Drink 1 hour before bed — most widely used natural sleep aid",
      "🌿 Brahmi Oil Head Massage: Warm Brahmi or sesame oil, massage onto scalp and temples for 10 min before bed — calms nervous system",
      "🧘 Body Scan Relaxation: Lie in bed, progressively relax each body part from toes to head, focusing on releasing tension — 90% effective for sleep onset within 20 min",
      "📵 No Screens 1 Hour Before Bed: Blue light from phone suppresses melatonin production by 50%. This single habit change improves sleep in 2-3 days",
      "🌡️ Cool Bedroom (18-21°C): Body temperature must drop to initiate sleep. A cool, dark room cuts sleep onset time in half"
    ],
    medicine:[
      "💊 Melatonin 0.5-3mg (Meloset) — Take 30-60 min before desired sleep time. Start with 0.5mg and increase if needed. Non-habit-forming",
      "💊 Doxylamine 25mg (Unisom/Dozile) — OTC antihistamine sleep aid. Use short-term only (max 2 weeks). Can cause next-day drowsiness",
      "💊 Magnesium Glycinate 400mg at bedtime — Relaxes muscles, calms nervous system, improves sleep quality significantly",
      "💊 Zolpidem 5-10mg — Prescription only. For short-term (2 weeks) severe insomnia. Can be habit-forming",
      "💊 Clonazepam 0.25-0.5mg — Prescription only for anxiety-related insomnia. Short-term only",
      "🩺 CBT-I (Cognitive Behavioural Therapy for Insomnia) — Gold standard treatment. Consult a psychologist. More effective than medication long-term"
    ],
    lifestyle:[
      "Fixed wake time every day (even weekends) is the single most important sleep habit — do not vary by more than 30 min",
      "Get out of bed if not asleep within 20 min — go to another room, do something calm, return only when sleepy (stimulus control therapy)",
      "Avoid alcohol — alcohol may cause drowsiness initially but disrupts REM sleep, causing waking at 2-3am",
      "No caffeine after 12 noon — caffeine has a half-life of 6-8 hours, so a 3pm coffee still has 50% caffeine at 9pm"
    ],
    flags:["Insomnia with loud snoring + daytime sleepiness — possible sleep apnoea, needs sleep study","Insomnia after a traumatic event — possible PTSD, seek mental health support","Insomnia with racing thoughts, decreased need for sleep, high energy — possible bipolar, see psychiatrist","Insomnia causing severe daily impairment for more than 3 months"]
  }
};
 
/* DEFAULT FALLBACK for symptoms without specific entry */
function defaultResult(syms){
  return {
    ico:"🏥",
    diagnosis: syms.length>0 ? "Assessment for: "+syms.join(", ") : "General Health Assessment",
    confidence:"Moderate",
    summary:"Based on your selected symptoms, this appears to be a common health concern. General wellness measures and monitoring are recommended. Please follow the advice below and consult a doctor if symptoms worsen or persist beyond a week.",
    matched: syms,
    home:["Stay well hydrated — drink 8-10 glasses of water daily","Get adequate rest — 7-9 hours of sleep per night","Eat light, nutritious meals — avoid junk food, fried food, and excess sugar","Drink warm herbal teas (ginger, tulsi, chamomile) throughout the day","Avoid stress — practice deep breathing or meditation for 10 min daily","Monitor your symptoms — note when they worsen and what triggers them"],
    medicine:["Paracetamol 500mg (Crocin) — For fever or pain, every 6-8 hours","Stay hydrated with ORS if any vomiting or diarrhoea","Consult a doctor for proper diagnosis and prescription medication","Do not self-medicate with antibiotics without medical advice","Get a basic blood test (CBC) if symptoms persist more than a week"],
    lifestyle:["Rest and avoid strenuous activity","Eat home-cooked, easily digestible food","Avoid cold drinks, ice cream, and packaged foods","Maintain good hygiene — wash hands regularly"],
    flags:["High fever above 103°F","Symptoms rapidly worsening or spreading","Severe pain, difficulty breathing, or chest pain","Symptoms lasting more than 5-7 days without improvement"]
  };
}
 
/* SYMPTOMS */
const SYM_GROUPS=[
  {g:"🌡️ General",s:["Fever","Chills","Fatigue","Night sweats","Loss of appetite","Weight loss","Weight gain","Body ache","Muscle weakness"]},
  {g:"🧠 Head & Neurological",s:["Headache","Dizziness","Blurred vision","Insomnia","Anxiety","Difficulty concentrating","Fainting"]},
  {g:"🫁 Respiratory",s:["Cough","Cold / Runny nose","Sore throat","Shortness of breath","Chest pain","Wheezing"]},
  {g:"🍽️ Digestive",s:["Nausea","Vomiting","Diarrhoea","Constipation","Stomach pain","Bloating","Heartburn / Acidity","Difficulty swallowing"]},
  {g:"🦴 Muscles & Joints",s:["Joint pain","Back pain","Neck pain","Stiffness","Swelling in joints"]},
  {g:"🧴 Skin & Hair",s:["Skin rash","Itching","Acne","Hair loss","Dry skin","Pale skin","Yellowing of skin"]},
  {g:"👁️ Eyes & Ears",s:["Eye redness","Ear pain","Ringing in ears","Watery eyes","Sensitivity to light"]},
  {g:"💧 Urinary",s:["Frequent urination","Burning urination","Excessive thirst","Dark urine","Blood in urine"]},
  {g:"❤️ Heart & Circulation",s:["Irregular heartbeat","Palpitations","Swelling in legs","Cold hands and feet"]},
  {g:"🩸 Menstrual & Hormonal",s:["Irregular periods","Missed periods","Heavy bleeding during periods","Painful periods","Spotting between periods","Bloating before periods","Mood swings / PMS","Breast tenderness","Excessive facial or body hair","Pelvic pain","Hot flashes","Vaginal dryness","Hormonal acne","PCOS symptoms"]}
];
const selSym=new Set();
function buildTags(){
  const c=document.getElementById('sym-tags');
  SYM_GROUPS.forEach(grp=>{
    const lbl=document.createElement('div');lbl.className='sym-group-label';lbl.textContent=grp.g;c.appendChild(lbl);
    grp.s.forEach(s=>{
      const el=document.createElement('span');el.className='sym-tag';el.textContent=s;
      el.onclick=()=>{
        el.classList.toggle('selected');
        selSym.has(s)?selSym.delete(s):selSym.add(s);
        const cnt=document.getElementById('sel-count');
        if(selSym.size>0){cnt.style.display='block';cnt.textContent='✓ '+selSym.size+' symptom'+(selSym.size>1?'s':'')+' selected: '+[...selSym].join(', ');}
        else{cnt.style.display='none';}
      };
      c.appendChild(el);
    });
  });
}
buildTags();
 
function updSev(v){
  document.getElementById('sev-num').textContent=v;
  const labs=['','Very mild','Mild','Mild','Moderate','Moderate','Moderate','Severe','Severe','Very severe','Critical'];
  document.getElementById('sev-lbl').textContent=labs[+v];
}
 
function goSec(n){
  [1,2,3].forEach(i=>{document.getElementById('s'+i).style.display=i===n?'block':'none';const s=document.getElementById('st'+i);s.classList.toggle('active',i===n);s.classList.toggle('done',i<n);});
  document.getElementById('result-section').classList.remove('visible');
  window.scrollTo({top:0,behavior:'smooth'});
}
 
/* DIAGNOSE — 100% OFFLINE, NO API */
function diagnose(){
  const syms=[...selSym];
  const extra=document.getElementById('v-extra').value.trim();
  const errEl=document.getElementById('errbox');
 
  if(syms.length===0&&!extra){
    errEl.textContent='Please select at least 1 symptom.';
    errEl.style.display='block';return;
  }
  errEl.style.display='none';
 
  // Find best match in KB
  let result=null;
  // First: exact match
  for(const s of syms){if(KB[s]){result=KB[s];break;}}
  // If no exact match: use default
  if(!result) result=defaultResult(syms);
 
  // Personalise with patient info
  const name=document.getElementById('v-name').value;
  const age=document.getElementById('v-age').value;
  const gender=document.getElementById('v-gender').value;
  const sev=document.getElementById('v-sev').value;
  const dur=document.getElementById('v-dur').value;
 
  // Show results
  [1,2,3].forEach(i=>document.getElementById('s'+i).style.display='none');
  document.getElementById('st4').classList.add('active');
  document.getElementById('r-ico').textContent=result.ico||'🏥';
  document.getElementById('r-conf').textContent='Confidence: '+result.confidence+(age?' | Age: '+age:'')+(gender?' | '+gender:'');
  document.getElementById('r-title').textContent=result.diagnosis;
  document.getElementById('r-sum').textContent=result.summary+(dur?' Duration reported: '+dur+'.':'')+(sev>7?' Severity is high ('+sev+'/10) — please monitor closely.':'');
 
  // Render cards
  const grid=document.getElementById('r-grid');
  grid.innerHTML='';
  const cards=[
    {t:'🔍 Matched Symptoms',c:'',dot:'#16a34a',items:syms.length>0?syms:result.matched},
    {t:'🌿 Home Recipes & Remedies',c:'',dot:'#16a34a',items:result.home},
    {t:'💊 Medicines & Treatment',c:'blue',dot:'#3b82f6',items:result.medicine},
    {t:'🏃 Lifestyle & Diet Advice',c:'blue',dot:'#0369a1',items:result.lifestyle},
    {t:'🚨 Red Flags — See Doctor If:',c:'warn full',dot:'#f97316',items:result.flags}
  ];
  cards.forEach(card=>{
    if(!card.items||!card.items.length)return;
    const div=document.createElement('div');
    div.className='res-card '+card.c;
    div.innerHTML='<h3><span class="dot" style="background:'+card.dot+'"></span>'+card.t+'</h3><ul>'+card.items.map(i=>'<li>'+i+'</li>').join('')+'</ul>';
    grid.appendChild(div);
  });
 
  document.getElementById('result-section').classList.add('visible');
  window.scrollTo({top:0,behavior:'smooth'});
}
 
function resetApp(){
  selSym.clear();
  document.querySelectorAll('.sym-tag.selected').forEach(t=>t.classList.remove('selected'));
  document.querySelectorAll('input:not([type=range]),select,textarea').forEach(el=>el.value='');
  document.getElementById('v-sev').value=5;updSev(5);
  document.getElementById('result-section').classList.remove('visible');
  document.getElementById('sel-count').style.display='none';
  document.getElementById('errbox').style.display='none';
  goSec(1);
}
</script>
</body>
</html>
