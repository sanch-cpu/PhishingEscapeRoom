<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Phishing Escape Room</title>
</head>
<body style="margin:0;padding:0;background:#0f1923;min-height:100vh">
<style>
@import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Rajdhani:wght@400;600;700&display=swap');
*{box-sizing:border-box}
body{padding:12px;font-family:'Rajdhani',sans-serif}
.w{font-family:'Rajdhani',sans-serif;color:#e2f0ff;max-width:640px;margin:0 auto}
.hdr{background:#0a1628;border-radius:10px;padding:1.25rem 1.5rem;margin-bottom:1rem;border:1px solid #1e3a5f}
.hdr-title{font-size:24px;font-weight:700;color:#e2f0ff;margin:0 0 6px}
.prog{display:flex;gap:5px;margin:0}
.dot{flex:1;height:5px;border-radius:3px;background:#1e3a5f;transition:background .4s}
.dot.done{background:#4ade80}.dot.active{background:#60a5fa}
.panel{background:#1a2535;border:.5px solid #2d3f55;border-radius:12px;padding:1.25rem;margin-bottom:1rem;color:#e2f0ff}
.ptitle{font-size:20px;font-weight:700;margin:0 0 6px;color:#e2f0ff}
.pdesc{font-size:15px;margin:0 0 1rem;line-height:1.5;opacity:.85;color:#e2f0ff}
.email{background:#fff;border-radius:8px;border:.5px solid #d1d5db;overflow:hidden;font-size:14px;color:#111}
.email-hdr{background:#f3f4f6;padding:10px 14px;border-bottom:1px solid #d1d5db}
.erow{display:flex;gap:6px;margin-bottom:4px}
.elbl{font-weight:700;color:#111827;min-width:55px}
.eval{color:#1f2937}
.ebody{padding:14px;line-height:1.8;color:#1f2937}
.flag{cursor:pointer;border-radius:3px;padding:1px 4px;display:inline;color:#1f2937}
.flag.fd{cursor:pointer;border-radius:3px;padding:1px 4px;display:inline;color:#1f2937}
.flag.fd:hover{background:rgba(0,0,0,.06)}
.flag.found{background:rgba(74,222,128,.3);border-bottom:2px solid #16a34a;color:#14532d;font-weight:600}
.ucard{border:1px solid #2d3f55;border-radius:8px;padding:11px 14px;margin-bottom:8px;cursor:pointer;transition:all .2s;display:flex;align-items:center;gap:12px;background:#121e2d}
.ucard:hover{border-color:#3b82f6;background:#0f1923}
.ucard.ok{border-color:#16a34a;background:rgba(74,222,128,.1);cursor:default}
.ucard.bad{border-color:#dc2626;background:rgba(248,113,113,.1)}
.url-icon{width:28px;height:28px;border-radius:6px;flex-shrink:0;display:flex;align-items:center;justify-content:center;background:#0f1923;border:1px solid #2d3f55;color:#93c5fd}
.url-icon svg{width:15px;height:15px}
.mono{font-family:'Share Tech Mono',monospace;font-size:13px;flex:1;word-break:break-all;color:#e2f0ff}
.opt{border:1px solid #2d3f55;border-radius:8px;padding:11px 14px;margin-bottom:8px;cursor:pointer;font-size:15px;line-height:1.4;transition:all .2s;color:#e2f0ff;background:#121e2d}
.opt:hover{border-color:#3b82f6;background:#0f1923}
.opt.cor{border-color:#16a34a;background:rgba(74,222,128,.12);color:#4ade80;font-weight:600;cursor:default}
.opt.wrg{border-color:#dc2626;background:rgba(248,113,113,.1);color:#f87171}
.att-grid{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin-bottom:10px}
.att{border:1px solid #2d3f55;border-radius:8px;padding:11px 13px;cursor:pointer;display:flex;align-items:center;gap:10px;transition:all .2s;background:#121e2d}
.att:hover{border-color:#3b82f6;background:#0f1923}
.att.flagged-correct{border-color:#16a34a;background:rgba(74,222,128,.12);cursor:default}
.att.flash-bad{border-color:#dc2626;background:rgba(248,113,113,.1)}
.att-name{font-family:'Share Tech Mono',monospace;font-size:12px;word-break:break-all;font-weight:600;color:#e2f0ff}
.att-meta{font-size:12px;color:#93c5fd;margin-top:2px}
.fi{width:40px;height:48px;flex-shrink:0;position:relative;border-radius:3px 6px 3px 3px;display:flex;flex-direction:column;overflow:hidden}
.fi-body{flex:1;display:flex;align-items:center;justify-content:center}
.fi-fold{position:absolute;top:0;right:0;width:12px;height:12px;background:rgba(0,0,0,.15);clip-path:polygon(100% 0,0 0,100% 100%)}
.fi-tag{font-size:8px;font-weight:700;letter-spacing:.5px;text-align:center;padding:3px 2px;font-family:'Rajdhani',sans-serif;line-height:1}
.fi-pdf{background:#fff0f0;border:1.5px solid #fca5a5}.fi-pdf .fi-tag{background:#dc2626;color:#fff}
.fi-docm{background:#eff6ff;border:1.5px solid #93c5fd}.fi-docm .fi-tag{background:#2563eb;color:#fff}
.fi-jpg{background:#fffbeb;border:1.5px solid #fcd34d}.fi-jpg .fi-tag{background:#d97706;color:#fff}
.fi-zip{background:#faf5ff;border:1.5px solid #c4b5fd}.fi-zip .fi-tag{background:#7c3aed;color:#fff}
.fi-xlsx{background:#f0fdf4;border:1.5px solid #86efac}.fi-xlsx .fi-tag{background:#16a34a;color:#fff}
.tf-row{display:flex;align-items:center;justify-content:space-between;border:1px solid #2d3f55;border-radius:8px;padding:11px 14px;margin-bottom:8px;gap:12px;font-size:15px;line-height:1.4;color:#e2f0ff;background:#121e2d}
.tf-row.answered{border-color:#16a34a;background:rgba(74,222,128,.08)}
.tf-btns{display:flex;gap:6px;flex-shrink:0}
.tfbtn{padding:6px 14px;border-radius:6px;border:1px solid #2d3f55;cursor:pointer;font-size:14px;font-weight:700;font-family:'Rajdhani',sans-serif;background:#0f1923;color:#e2f0ff;transition:all .2s}
.tfbtn:hover{background:#1a2535}
.tfbtn.correct-ans{background:rgba(74,222,128,.2);border-color:#16a34a;color:#4ade80;cursor:default}
.tfbtn.wrong-pick{background:rgba(248,113,113,.15);border-color:#dc2626;color:#f87171;cursor:default}
.fake-browser{border-radius:8px;overflow:hidden;border:1px solid #cbd5e1;margin-bottom:14px}
.browser-bar{background:#f1f5f9;padding:7px 12px;display:flex;align-items:center;gap:8px;border-bottom:1px solid #cbd5e1}
.browser-dots{display:flex;gap:4px}
.bdot{width:10px;height:10px;border-radius:50%}
.url-bar{flex:1;background:#fff;border:1px solid #cbd5e1;border-radius:99px;padding:4px 12px;font-family:'Share Tech Mono',monospace;font-size:12px;display:flex;align-items:center;gap:6px}
.pflag{cursor:pointer;display:inline-block}
.pflag.found{outline:2.5px solid #16a34a;border-radius:4px;background:rgba(74,222,128,.15)}
.fake-body{background:#fff;padding:24px 20px;text-align:center}
.pp-input{width:100%;border:1px solid #d1d5db;border-radius:6px;padding:8px 10px;margin-bottom:10px;font-size:13px;color:#374151;text-align:left;display:block}
.pp-btn{width:100%;background:#0070ba;color:#fff;border:none;border-radius:6px;padding:10px;font-size:14px;font-weight:700;cursor:default;margin-top:4px}
.sms-phone{background:#1c1c1e;border-radius:16px;padding:12px;max-width:340px;margin:0 auto 14px;border:1px solid #3a3a3c}
.sms-topbar{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;padding:0 4px}
.sms-contact{text-align:center;flex:1}
.sms-contact-name{font-size:14px;font-weight:700;color:#fff}
.sms-contact-sub{font-size:11px;color:#98989f;font-family:'Share Tech Mono',monospace}
.sms-bubble-wrap{display:flex;flex-direction:column;gap:8px;padding:4px}
.sms-bubble{max-width:80%;padding:9px 13px;border-radius:14px;font-size:13px;line-height:1.5}
.sms-in{background:#2c2c2e;color:#f2f2f7;align-self:flex-start;border-bottom-left-radius:4px}
.sms-out{background:#0a7ff5;color:#fff;align-self:flex-end;border-bottom-right-radius:4px}
.sms-time{font-size:10px;color:#98989f;text-align:center;margin:2px 0}
.sflag{cursor:pointer;border-radius:3px;padding:1px 3px;display:inline;color:inherit}
.sflag.found{background:rgba(74,222,128,.35);border-bottom:2px solid #4ade80;font-weight:600}
.clue{background:#0a1628;border:1px solid #1e3a5f;border-radius:8px;padding:10px 14px;margin-top:10px;font-family:'Share Tech Mono',monospace;font-size:14px;color:#4ade80}
.clue-lbl{font-size:11px;letter-spacing:2px;color:#93c5fd;margin-bottom:3px}
.fb{font-size:14px;margin-top:8px;padding:10px 12px;border-radius:6px;line-height:1.5;font-weight:600}
.fb.ok{background:rgba(74,222,128,.15);color:#4ade80;border:1px solid #16a34a}
.fb.bad{background:rgba(248,113,113,.15);color:#f87171;border:1px solid #dc2626}
.btn{display:inline-block;padding:10px 24px;border-radius:8px;border:1px solid;cursor:pointer;font-family:'Rajdhani',sans-serif;font-weight:700;font-size:16px;transition:all .15s;margin-top:10px}
.btn-p{background:#1e3a5f;border-color:#3b82f6;color:#bfdbfe}
.btn-p:hover{background:#2d4f7f}
.btn-s{background:#14532d;border-color:#16a34a;color:#bbf7d0}
.field-label{font-size:14px;font-weight:600;display:block;text-align:left;margin-bottom:6px;color:#93c5fd}
.text-input{width:100%;border:1px solid #2d3f55;border-radius:8px;padding:12px 14px;font-size:16px;font-family:'Rajdhani',sans-serif;background:#0f1923;color:#e2f0ff;margin-bottom:14px;outline:none}
.text-input:focus{border-color:#3b82f6}
.intro-list{font-size:14px;line-height:2;color:#93c5fd;margin:0 0 1.4rem;padding-left:1.2rem}
.code-row{display:flex;gap:7px;justify-content:center;margin:1rem 0;flex-wrap:wrap}
.cc{width:44px;height:56px;background:#0a1628;border:2px solid #1e3a5f;border-radius:7px;display:flex;align-items:center;justify-content:center;font-family:'Share Tech Mono',monospace;font-size:22px;font-weight:700;color:#4ade80;transition:all .3s}
.cc.lit{border-color:#4ade80}.cc.bad{border-color:#dc2626;color:#f87171}
.code-inp{font-family:'Share Tech Mono',monospace;font-size:20px;letter-spacing:6px;text-align:center;padding:9px;border-radius:8px;width:100%;max-width:300px;display:block;margin:0 auto;border:1px solid #2d3f55;background:#0f1923;color:#e2f0ff}
.success{background:#0a1628;border-radius:12px;padding:1.75rem;text-align:center;border:1px solid #16a34a}
.score-row{display:flex;justify-content:center;gap:16px;margin:.75rem 0;flex-wrap:wrap}
.score-box{background:rgba(74,222,128,.08);border:.5px solid rgba(74,222,128,.3);border-radius:8px;padding:10px 18px;text-align:center}
.score-val{font-size:28px;font-weight:700;color:#4ade80;font-family:'Share Tech Mono',monospace}
.score-lbl{font-size:12px;color:#93c5fd;margin-top:2px}
.breakdown-grid{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin:.75rem 0;text-align:left}
.breakdown-item{background:rgba(74,222,128,.06);border:.5px solid rgba(74,222,128,.25);border-radius:8px;padding:8px 12px;font-size:13px}
.breakdown-item.had-wrong{background:rgba(248,113,113,.08);border-color:rgba(248,113,113,.3)}
.breakdown-name{font-size:12px;color:#93c5fd;margin-bottom:2px;font-family:'Share Tech Mono',monospace}
.breakdown-val{font-size:16px;font-weight:700;color:#4ade80}
.breakdown-item.had-wrong .breakdown-val{color:#f87171}
.ctr{font-family:'Share Tech Mono',monospace;font-size:13px;color:#93c5fd;margin-bottom:8px;font-weight:600}
.transcript{background:#0f1923;border:1px solid #2d3f55;border-radius:8px;padding:13px 15px;font-size:14px;line-height:1.9;margin-bottom:12px;color:#e2f0ff}
.tc{color:#60a5fa;font-weight:700}.ty{color:#4ade80;font-weight:700}
.err{font-size:13px;color:#dc2626;margin-top:-10px;margin-bottom:10px;display:none}
</style>

<div class="w" id="app">
  <div class="hdr">
    <div class="hdr-title">PHISHING ESCAPE ROOM</div>
    <div class="prog" id="prog"></div>
  </div>
  <div id="pa"></div>
</div>

<script>
const SCRIPT_URL='https://script.google.com/macros/s/AKfycby4HjC-o3gDFajRJ5tdsn6ABlBF_mZ5pOGAE36Eyan7XKeAtuwoOGQiHoeZqg5dr-Uijw/exec';

const S={started:false,submitted:false,room:0,flags:[],clues:[],tfd:[],pf:[],sf:[],lastFb:{}};
const T={age:'',startTime:null,w:{p1:0,p2:0,p3:0,p4:0,p5:0,p6:0,p7:0,p8:0}};
function totalWrong(){return Object.values(T.w).reduce((a,b)=>a+b,0);}
function addWrong(p){T.w[p]++;}

const CODEWORD='PHISHING',LETTERS=['P','H','I','S','H','I','N','G'];
const FTIPS={fs:'Spoofed sender &mdash; "c0mpany.net" uses a zero instead of the letter O.',fu:'False urgency &mdash; attackers create panic so you act before thinking.',fl:'Suspicious link &mdash; never click unverified links in emails.'};
const Q3=[{q:'A caller claims to be from Microsoft Support and says your PC is infected. They ask you to install remote access software. What do you do?',opts:['Install it &mdash; they sound official','Hang up and contact Microsoft via their official website','Give them your password so they can fix it'],c:1,tip:'Microsoft never cold-calls users about infections. This is a vishing (voice phishing) attack.'},{q:'An email offers a $500 gift card if you verify your account. The sender is: rewards@amazon-giftcards-promo.co. What is this?',opts:['A legitimate Amazon promotion','A phishing attempt using a spoofed domain','A harmless marketing campaign'],c:1,tip:'Real companies use their own domain (amazon.com). Subdomains like amazon-giftcards-promo.co are classic spoofing.'}];
const ATTS=[{id:'a1',cls:'fi-pdf',tag:'PDF',svg:'pdf',name:'Q4_Report.pdf',meta:'PDF &middot; 842 KB',d:false,r:'Standard PDF document &mdash; no executable code.'},{id:'a2',cls:'fi-pdf',tag:'PDF',svg:'pdf',name:'Invoice_2024.pdf.exe',meta:'PDF &middot; 1.2 MB',d:true,r:'Double extension attack &mdash; the icon shows PDF but the real extension is .exe.'},{id:'a3',cls:'fi-docm',tag:'DOCM',svg:'word',name:'HR_Update.docm',meta:'DOCM &middot; 56 KB',d:true,r:'Macro-enabled Word doc &mdash; often used to execute malicious code when opened.'},{id:'a4',cls:'fi-jpg',tag:'JPG',svg:'img',name:'team_photo.jpg',meta:'JPEG &middot; 3.1 MB',d:false,r:'Standard image file &mdash; no executable risk.'},{id:'a5',cls:'fi-zip',tag:'ZIP',svg:'zip',name:'Bonus_Details.zip',meta:'ZIP &middot; 900 KB',d:true,r:'Unexpected archive from an unknown sender &mdash; zips frequently hide malware.'},{id:'a6',cls:'fi-xlsx',tag:'XLSX',svg:'xls',name:'Budget_Draft.xlsx',meta:'XLSX &middot; 120 KB',d:false,r:'Regular spreadsheet from a known colleague &mdash; low risk.'}];
const TFQ=[{id:'tf0',s:'It is safe to reuse the same password across multiple work accounts as long as it is long.',a:false,tip:'Reusing passwords means one breach exposes all accounts. Use a unique password for each.'},{id:'tf1',s:'A padlock icon (HTTPS) in the browser bar means a website is definitely legitimate and trustworthy.',a:false,tip:'HTTPS only encrypts the connection &mdash; phishing sites use HTTPS too. Always verify the domain.'},{id:'tf2',s:'You should verify unexpected wire transfer or payment requests via a separate communication channel.',a:true,tip:'CEO fraud relies on email only. A quick phone call to the requester stops most attacks.'},{id:'tf3',s:'Enabling multi-factor authentication (MFA) makes your account virtually impossible to compromise via phishing alone.',a:true,tip:'MFA is one of the most effective defences &mdash; stolen credentials alone are not enough to log in.'}];
const PFLAGS=[{id:'pf-url',tip:'The URL uses "paypa1.com" &mdash; the letter l has been replaced with the digit 1. This is typosquatting.',d:true},{id:'pf-logo',tip:'The logo is blurry &mdash; phishing pages often use low-quality stolen images.',d:true},{id:'pf-card',tip:'Legitimate login pages never ask for your card number. This is harvesting payment data.',d:true},{id:'pf-email',tip:'Asking for an email on a login page is normal &mdash; not a red flag.',d:false},{id:'pf-pass',tip:'Asking for a password is standard &mdash; not a red flag by itself.',d:false},{id:'pf-btn',tip:'A login button is standard on any login page &mdash; not a red flag.',d:false},{id:'pf-subtitle',tip:'A subtitle prompting login is standard on any login page &mdash; not a red flag.',d:false},{id:'pf-dots',tip:'Browser window controls are a normal part of any browser &mdash; not a red flag.',d:false}];
const VQ=[{q:'What critical mistake did the employee make?',opts:['They answered the phone','They read the one-time MFA code to the caller','They confirmed their username'],c:1,tip:'Reading an MFA code to any caller hands attackers the second factor &mdash; a real-time phishing technique.'},{q:'What should the employee have done first?',opts:['Hung up and called IT Helpdesk back using the official company number','Asked the caller for their employee ID','Checked their emails for a related message'],c:0,tip:'Always verify unexpected IT calls by hanging up and dialling the official number yourself.'}];
const SFLAGS=[{id:'sf-num',tip:'Spoofed sender ID &mdash; "NatWest-Alert" can be faked by anyone. Real banks use verified shortcodes.',d:true},{id:'sf-urg',tip:'Urgency and threat of account suspension &mdash; a classic pressure tactic to stop you thinking clearly.',d:true},{id:'sf-link',tip:"Shortened URL in a bank text &mdash; legitimate banks never send bit.ly links. Go directly to your bank's official app.",d:true},{id:'sf-name',tip:'Being addressed by name is not a red flag &mdash; attackers can obtain names from data breaches.',d:false},{id:'sf-dear',tip:'"Dear" is a common greeting in messages &mdash; not a red flag by itself.',d:false},{id:'sf-account',tip:'Mentioning your account is standard for a bank notification &mdash; not a red flag.',d:false},{id:'sf-verify',tip:'"Verify now" on its own is not a red flag &mdash; the suspicious part is the shortened link that follows.',d:false},{id:'sf-sub',tip:'"Unknown sender" is shown by your phone automatically &mdash; not something attackers control.',d:false}];

const GLOBE_SVG=`<svg viewBox="0 0 16 16" fill="none"><circle cx="8" cy="8" r="6" stroke="currentColor" stroke-width="1.2"/><ellipse cx="8" cy="8" rx="2.5" ry="6" stroke="currentColor" stroke-width="1.2"/><line x1="2" y1="8" x2="14" y2="8" stroke="currentColor" stroke-width="1.2"/><line x1="3" y1="5" x2="13" y2="5" stroke="currentColor" stroke-width="1.2"/><line x1="3" y1="11" x2="13" y2="11" stroke="currentColor" stroke-width="1.2"/></svg>`;
const ICONS={pdf:`<svg viewBox="0 0 20 24" fill="none"><rect width="8" height="2.5" rx=".8" x="4" y="9" fill="#dc2626"/><rect width="6" height="2" rx=".8" x="4" y="13" fill="#dc2626" opacity=".6"/><rect width="7" height="2" rx=".8" x="4" y="17" fill="#dc2626" opacity=".4"/></svg>`,word:`<svg viewBox="0 0 20 24" fill="none"><text x="4" y="17" font-size="11" font-weight="700" fill="#2563eb" font-family="serif">W</text></svg>`,img:`<svg viewBox="0 0 20 24" fill="none"><rect x="3" y="8" width="14" height="10" rx="1.5" fill="#fcd34d" opacity=".5"/><circle cx="7" cy="12" r="2" fill="#d97706"/><path d="M3 17l4-4 3 3 3-3 4 4" stroke="#d97706" stroke-width="1.2" fill="none"/></svg>`,zip:`<svg viewBox="0 0 20 24" fill="none"><rect x="8" y="3" width="4" height="3" rx=".5" fill="#7c3aed" opacity=".4"/><rect x="8" y="8" width="4" height="3" rx=".5" fill="#7c3aed" opacity=".7"/><rect x="8" y="13" width="4" height="3" rx=".5" fill="#7c3aed"/></svg>`,xls:`<svg viewBox="0 0 20 24" fill="none"><line x1="4" y1="9" x2="10" y2="17" stroke="#16a34a" stroke-width="2" stroke-linecap="round"/><line x1="10" y1="9" x2="4" y2="17" stroke="#16a34a" stroke-width="2" stroke-linecap="round"/><line x1="12" y1="9" x2="16" y2="17" stroke="#16a34a" stroke-width="2" stroke-linecap="round"/></svg>`};

const PUZZLE_LABELS={p1:'P1: Suspicious Inbox',p2:'P2: URL Forensics',p3:'P3: Threat ID',p4:'P4: Attachments',p5:'P5: Vishing Call',p6:'P6: True or False',p7:'P7: Fake Login Page',p8:'P8: Smishing Text'};
const TOTAL=9;

function fi(a){return`<div class="fi ${a.cls}"><div class="fi-fold"></div><div class="fi-body">${ICONS[a.svg]||''}</div><div class="fi-tag">${a.tag}</div></div>`;}
function prog(){const b=document.getElementById('prog');b.innerHTML=S.started?[...Array(TOTAL)].map((_,i)=>`<div class="dot${i<S.room?' done':i===S.room?' active':''}"></div>`).join(''):'';}
function render(){prog();document.getElementById('pa').innerHTML=S.started?([p0,p1,p2,p3,p4,p5,p6,p7,p8,pWin][S.room]||pWin)():pIntro();bind();}
function clue(n){return`<div class="clue"><div class="clue-lbl">CLUE UNLOCKED</div>Letter ${n}: <strong>${LETTERS[n-1]}</strong></div>`;}
function nextBtn(){return`<button class="btn btn-p" id="bn">NEXT PUZZLE</button>`;}
function setFb(k,h){S.lastFb[k]=h;}
function getFb(k){return S.lastFb[k]||'';}
function ok(m){return`<div class="fb ok">&#x2714; ${m}</div>`;}
function bad(m){return`<div class="fb bad">&#x2718; ${m}</div>`;}

async function submitResults(mins){
  const params=new URLSearchParams({timestamp:new Date().toISOString(),age:T.age,time_minutes:mins,total_wrong:totalWrong(),p1_wrong:T.w.p1,p2_wrong:T.w.p2,p3_wrong:T.w.p3,p4_wrong:T.w.p4,p5_wrong:T.w.p5,p6_wrong:T.w.p6,p7_wrong:T.w.p7,p8_wrong:T.w.p8});
  try{await fetch(SCRIPT_URL+'?'+params.toString(),{method:'GET',mode:'no-cors'});}catch(e){}
}

function pIntro(){return`<div class="panel" style="text-align:center;padding:2rem 1.5rem"><div style="font-size:32px;margin-bottom:8px">&#x1F512;</div><div class="ptitle" style="text-align:center;font-size:22px">Welcome to the Phishing Escape Room</div><p style="font-size:15px;color:#93c5fd;margin:.5rem 0 1.5rem;line-height:1.6">8 puzzles covering real-world phishing threats. Collect all 8 letters to crack the escape code.</p><ul class="intro-list" style="text-align:left;display:inline-block"><li>Spot red flags in a phishing email</li><li>Identify a fake URL</li><li>Recognise social engineering attacks</li><li>Flag dangerous file attachments</li><li>Analyse a vishing phone call</li><li>True or false security quiz</li><li>Spot the fake login page</li><li>Identify a smishing text message</li></ul><div style="max-width:320px;margin:0 auto;text-align:left"><label class="field-label">YOUR AGE</label><input class="text-input" id="inp-age" placeholder="Enter your age..." maxlength="3" type="number" min="10" max="99"/><div class="err" id="err-age">Please enter a valid age (10&ndash;99).</div><button class="btn btn-p" id="start-btn" style="width:100%;text-align:center;margin-top:4px">START GAME</button></div></div>`;}

function p0(){const f=S.flags;return`<div class="panel"><div class="ptitle">PUZZLE 1 &mdash; The Suspicious Inbox</div><div class="pdesc">Your colleague forwarded this email. Something is off. Read it carefully and click the 3 red flags hidden inside it.</div><div class="ctr">FLAGS FOUND: ${f.length} / 3</div><div class="email"><div class="email-hdr"><div class="erow"><span class="elbl">From:</span><span class="eval"><span class="flag${f.includes('fs')?' found':''}" id="fl-fs">it-support@c0mpany.net</span></span></div><div class="erow"><span class="elbl">To:</span><span class="eval"><span class="flag fd" id="fl-to">you@company.com</span></span></div><div class="erow"><span class="elbl">Subject:</span><span class="eval"><span class="flag fd" id="fl-subj">ACTION REQUIRED &mdash; Your account expires in 1 hour</span></span></div></div><div class="ebody"><span class="flag fd" id="fl-greeting">Dear Employee,</span><br><br>Our security system has detected <span class="flag${f.includes('fu')?' found':''}" id="fl-fu">unusual activity. You must verify your identity within 60 minutes or your account will be permanently suspended.</span><br><br><span class="flag fd" id="fl-please">Please click the link below immediately:</span><br><br><span class="flag${f.includes('fl')?' found':''}" id="fl-fl">Click here to verify your identity now</span><br><br><span class="flag fd" id="fl-failure">Failure to act will result in loss of all data access.</span><br><br><span class="flag fd" id="fl-regards">Regards,<br>IT Support Team</span></div></div>${getFb('p0')}${f.length===3?clue(1)+nextBtn():''}</div>`;}
function p1(){const urls=[{id:'u1',u:'https://mycompany-portal.com/reset',r:false},{id:'u2',u:'https://mycompany.com/portal/reset',r:true},{id:'u3',u:'http://mycompany.com.resetpassword.xyz/login',r:false},{id:'u4',u:'https://myc0mpany.com/reset?token=abc',r:false}];return`<div class="panel"><div class="ptitle">PUZZLE 2 &mdash; URL Forensics</div><div class="pdesc">You received a password reset email. Only one URL is the real company portal. Read each one carefully and find it.</div>${urls.map(u=>`<div class="ucard${S.clues.includes('url')&&u.r?' ok':''}" id="${u.id}"><div class="url-icon" style="color:#93c5fd">${GLOBE_SVG}</div><span class="mono">${u.u}</span></div>`).join('')}${getFb('p1')}${S.clues.includes('url')?clue(2)+nextBtn():''}</div>`;}
function p2(){const done=S.clues.filter(c=>c.startsWith('q')).length;if(done>=2)return`<div class="panel"><div class="ptitle">PUZZLE 3 &mdash; Threat Identification</div><div class="pdesc">Both scenarios handled correctly!</div>${getFb('p2')}${clue(3)}${nextBtn()}</div>`;const q=Q3[done],pick=S.lastFb['q'+done+'pick'];return`<div class="panel"><div class="ptitle">PUZZLE 3 &mdash; Threat Identification (${done+1}/2)</div><div class="pdesc">${q.q}</div>${q.opts.map((o,i)=>{let c='opt';if(pick!==undefined){if(i===q.c)c='opt cor';else if(i===pick)c='opt wrg';}return`<div class="${c}" id="q${i}">${o}</div>`;}).join('')}${getFb('p2')}</div>`;}
function p3(){const found=S.clues.filter(c=>c.startsWith('att')).length;return`<div class="panel"><div class="ptitle">PUZZLE 4 &mdash; Dangerous Attachments</div><div class="pdesc">An email arrived with 6 attachments. Three are dangerous. Click only the ones you would NOT open.</div><div class="ctr">DANGEROUS FOUND: ${found} / 3</div><div class="att-grid">${ATTS.map(a=>`<div class="att${S.clues.includes('att'+a.id)?' flagged-correct':''}" id="${a.id}">${fi(a)}<div><div class="att-name">${a.name}</div><div class="att-meta">${a.meta}</div></div></div>`).join('')}</div>${getFb('p3')}${found===3?clue(4)+nextBtn():''}</div>`;}
function p4(){const vd=S.clues.filter(c=>c.startsWith('v')).length;return`<div class="panel"><div class="ptitle">PUZZLE 5 &mdash; The Vishing Call</div><div class="pdesc">Read this phone call transcript carefully. Then answer 2 questions about what went wrong.</div><div class="transcript"><span class="tc">CALLER:</span> "Hi, this is David from the IT Helpdesk. We are seeing suspicious login attempts on your account from overseas. I need to verify your identity quickly before we lock you out."<br><span class="ty">YOU:</span> "Oh okay, what do you need?"<br><span class="tc">CALLER:</span> "Can you confirm your username, then I will send a one-time code to your phone &mdash; just read it back to me so I can verify your account."<br><span class="ty">YOU:</span> "Sure, my username is jsmith. I got the code &mdash; it is 847291."<br><span class="tc">CALLER:</span> "Perfect, all sorted. You are safe now."</div>${vd>=2?'':`<div id="vq"></div>`}${getFb('p4')}${vd>=2?clue(5)+nextBtn():''}</div>`;}
function p5(){return`<div class="panel"><div class="ptitle">PUZZLE 6 &mdash; True or False?</div><div class="pdesc">Test your security knowledge. Answer all 4 statements. The correct answer is always highlighted green.</div>${TFQ.map(q=>{const p=S.tfd.find(d=>d.id===q.id);const rc=p?'tf-row answered':'tf-row';let tC='tfbtn',fC='tfbtn';if(p){if(q.a===true)tC='tfbtn correct-ans';else fC='tfbtn correct-ans';if(!p.ok){if(p.pick===true)tC='tfbtn wrong-pick';else fC='tfbtn wrong-pick';}}return`<div class="${rc}" id="tfr${q.id}"><span style="flex:1">${q.s}</span><div class="tf-btns"><div class="${tC}" id="tft${q.id}">TRUE</div><div class="${fC}" id="tff${q.id}">FALSE</div></div></div>`;}).join('')}${getFb('p5')}${S.tfd.length===4?clue(6)+nextBtn():''}</div>`;}
function p6(){const pf=S.pf,found=pf.length;return`<div class="panel"><div class="ptitle">PUZZLE 7 &mdash; Spot the Fake Login Page</div><div class="pdesc">This page appeared after clicking a link in an email. It claims to be PayPal. Click the 3 suspicious elements you can spot.</div><div class="ctr">FLAGS FOUND: ${found} / 3</div><div class="fake-browser"><div class="browser-bar"><div class="pflag${pf.includes('pf-dots')?' found':''}" id="pf-dots" style="display:flex;gap:4px"><div class="bdot" style="background:#f87171"></div><div class="bdot" style="background:#fbbf24"></div><div class="bdot" style="background:#4ade80"></div></div><div class="url-bar"><span class="pflag${pf.includes('pf-url')?' found':''}" id="pf-url" style="font-size:12px;font-family:'Share Tech Mono',monospace;color:#374151">http://paypa1.com/login</span></div></div><div class="fake-body"><div class="pflag${pf.includes('pf-logo')?' found':''}" id="pf-logo"><div style="font-size:22px;font-weight:700;color:#003087;margin-bottom:16px;display:inline-block;filter:blur(1.2px) contrast(0.9);opacity:0.85;letter-spacing:1px">PayPal</div></div><div class="pflag${pf.includes('pf-subtitle')?' found':''}" id="pf-subtitle" style="display:block;margin-bottom:14px"><span style="font-size:13px;color:#374151">Log in to your account</span></div><div class="pflag${pf.includes('pf-email')?' found':''}" id="pf-email" style="display:block"><input class="pp-input" placeholder="Email address" readonly/></div><div class="pflag${pf.includes('pf-pass')?' found':''}" id="pf-pass" style="display:block"><input class="pp-input" type="password" placeholder="Password" readonly/></div><div class="pflag${pf.includes('pf-card')?' found':''}" id="pf-card" style="display:block"><input class="pp-input" placeholder="Card number + CVV (security verification)" readonly/></div><div class="pflag${pf.includes('pf-btn')?' found':''}" id="pf-btn" style="display:block"><button class="pp-btn">Log In</button></div></div></div>${getFb('p6')}${found===3?clue(7)+nextBtn():''}</div>`;}
function p7(){const sf=S.sf;return`<div class="panel"><div class="ptitle">PUZZLE 8 &mdash; The Smishing Text</div><div class="pdesc">You received this text message. Smishing uses SMS to steal your information. Click the 3 red flags hidden inside the message.</div><div class="ctr">FLAGS FOUND: ${sf.length} / 3</div><div class="sms-phone"><div class="sms-topbar"><div style="font-size:16px;color:#fff">&lt;</div><div class="sms-contact"><div class="sms-contact-name"><span class="sflag${sf.includes('sf-num')?' found':''}" id="sf-num">NatWest-Alert</span></div><div class="sms-contact-sub"><span class="sflag${sf.includes('sf-sub')?' found':''}" id="sf-sub">Unknown sender</span></div></div><div style="font-size:16px;color:#fff">...</div></div><div class="sms-bubble-wrap"><div class="sms-time">Today 09:14</div><div class="sms-bubble sms-in"><span class="sflag${sf.includes('sf-dear')?' found':''}" id="sf-dear">Dear</span> <span class="sflag${sf.includes('sf-name')?' found':''}" id="sf-name">Alex</span>, <span class="sflag${sf.includes('sf-account')?' found':''}" id="sf-account">your NatWest account has been</span> <span class="sflag${sf.includes('sf-urg')?' found':''}" id="sf-urg">temporarily suspended due to suspicious activity. Immediate action required or your account will be permanently closed.</span> <span class="sflag${sf.includes('sf-verify')?' found':''}" id="sf-verify">Verify now:</span> <span class="sflag${sf.includes('sf-link')?' found':''}" id="sf-link">bit.ly/natwest-verify</span></div><div class="sms-time">Delivered</div><div class="sms-bubble sms-out" style="font-size:12px;opacity:.7">Is this real?</div></div></div>${getFb('p7')}${sf.length===3?clue(8)+nextBtn():''}</div>`;}
function p8(){return`<div class="panel"><div class="ptitle">PUZZLE 9 &mdash; The Escape Code</div><div class="pdesc">You have collected all 8 letters. Enter the escape code to lock down the breach.</div><div class="code-row">${[...Array(8)].map((_,i)=>`<div class="cc" id="cc${i}">?</div>`).join('')}</div><input class="code-inp" id="ci" maxlength="8" placeholder="_ _ _ _ _ _ _ _"/><div style="text-align:center;margin-top:10px;font-size:14px;color:#93c5fd">Hint: what kind of attack have you been defending against all along?</div><div id="fb8" style="text-align:center;margin-top:8px"></div></div>`;}

function pWin(){
  const mins=T.startTime?Math.round((Date.now()-T.startTime)/60000):0;
  if(!S.submitted){S.submitted=true;submitResults(mins);}
  return`<div class="success">
    <div style="font-size:30px;font-weight:700;color:#4ade80;margin:0 0 8px">YOU ESCAPED!</div>
    <div style="font-size:15px;color:#93c5fd;margin-bottom:1rem">All 8 puzzles solved. Here are your results.</div>
    <div class="score-row">
      <div class="score-box"><div class="score-val">${T.age}</div><div class="score-lbl">AGE</div></div>
      <div class="score-box"><div class="score-val">${totalWrong()}</div><div class="score-lbl">TOTAL WRONG</div></div>
      <div class="score-box"><div class="score-val">${mins}m</div><div class="score-lbl">TIME TAKEN</div></div>
    </div>
    <div style="font-size:13px;color:#93c5fd;font-family:'Share Tech Mono',monospace;margin:.75rem 0 .4rem;text-align:left">WRONG ANSWERS BY PUZZLE</div>
    <div class="breakdown-grid">
      ${Object.entries(T.w).map(([key,val])=>`<div class="breakdown-item${val>0?' had-wrong':''}"><div class="breakdown-name">${PUZZLE_LABELS[key]}</div><div class="breakdown-val">${val} wrong</div></div>`).join('')}
    </div>
    <div style="background:rgba(74,222,128,.1);border:1px solid rgba(74,222,128,.4);border-radius:8px;padding:12px;margin-top:8px;text-align:left">
      <div style="font-size:11px;letter-spacing:2px;color:#93c5fd;font-family:'Share Tech Mono',monospace;margin-bottom:6px">KEY TAKEAWAYS</div>
      <div style="font-size:14px;color:#bbf7d0;line-height:2">&#x2714; Check sender addresses for character substitutions (0 for O)<br>&#x2714; Urgency and threats are pressure tactics &mdash; pause before acting<br>&#x2714; Verify URLs &mdash; extra subdomains and wrong TLDs are red flags<br>&#x2714; Never open .exe, .docm, or unexpected .zip attachments<br>&#x2714; Never read MFA codes back to anyone &mdash; ever<br>&#x2714; HTTPS does not guarantee a site is legitimate<br>&#x2714; Banks never send shortened links &mdash; go to their official app<br>&#x2714; MFA + unique passwords are your strongest defences</div>
    </div>
    <button class="btn btn-s" style="margin-top:1rem" id="br">PLAY AGAIN</button>
  </div>`;
}

function bind(){
  if(!S.started){
    const sb=document.getElementById('start-btn'),ai=document.getElementById('inp-age'),ea=document.getElementById('err-age');
    if(sb)sb.onclick=()=>{const age=parseInt(ai?ai.value:'');if(!age||age<10||age>99){if(ea)ea.style.display='block';return;}if(ea)ea.style.display='none';T.age=age;T.startTime=Date.now();S.started=true;render();};
    if(ai)ai.onkeydown=(e)=>{if(e.key==='Enter')sb&&sb.click();};
    return;
  }
  const nb=document.getElementById('bn');if(nb)nb.onclick=()=>{S.room++;S.lastFb={};render();};
  const br=document.getElementById('br');if(br)br.onclick=()=>{Object.assign(S,{started:false,submitted:false,room:0,flags:[],clues:[],tfd:[],pf:[],sf:[],lastFb:{}});Object.assign(T,{age:'',startTime:null,w:{p1:0,p2:0,p3:0,p4:0,p5:0,p6:0,p7:0,p8:0}});render();};

  if(S.room===0){
    [['fl-fs','fs',FTIPS.fs],['fl-fu','fu',FTIPS.fu],['fl-fl','fl',FTIPS.fl]].forEach(([eid,fid,tip])=>{const el=document.getElementById(eid);if(!el)return;el.onclick=()=>{if(S.flags.includes(fid))return;S.flags.push(fid);setFb('p0',ok(tip));render();};});
    ['fl-to','fl-subj','fl-greeting','fl-please','fl-failure','fl-regards'].forEach(eid=>{const el=document.getElementById(eid);if(!el)return;el.onclick=()=>{addWrong('p1');setFb('p0',bad('Not a red flag &mdash; this is normal email content. Look for spoofed addresses, urgency tactics, and suspicious links.'));render();};});
  }
  if(S.room===1){[{id:'u1',r:false},{id:'u2',r:true},{id:'u3',r:false},{id:'u4',r:false}].forEach(u=>{const el=document.getElementById(u.id);if(!el)return;el.onclick=()=>{if(S.clues.includes('url'))return;if(u.r){S.clues.push('url');setFb('p1',ok('Correct! mycompany.com is the real domain over HTTPS.'));render();}else{addWrong('p2');el.className='ucard bad';setFb('p1',bad('Look more carefully &mdash; check for extra subdomains, wrong TLDs, or character swaps.'));render();setTimeout(()=>{el.className='ucard';},800);}};});}
  if(S.room===2){const done=S.clues.filter(c=>c.startsWith('q')).length;if(done<2){const q=Q3[done];q.opts.forEach((_,i)=>{const el=document.getElementById('q'+i);if(!el)return;el.onclick=()=>{const key='q'+done;if(S.clues.includes(key))return;S.lastFb[key+'pick']=i;if(i===q.c){S.clues.push(key);setFb('p2',ok(q.tip));render();}else{addWrong('p3');setFb('p2',bad(q.tip));render();setTimeout(()=>{delete S.lastFb[key+'pick'];render();},1200);}};});}}
  if(S.room===3){ATTS.forEach(a=>{const el=document.getElementById(a.id);if(!el)return;el.onclick=()=>{const key='att'+a.id;if(S.clues.includes(key))return;if(a.d){S.clues.push(key);setFb('p3',ok('Correct &mdash; dangerous! '+a.r));const n=S.clues.filter(c=>c.startsWith('att')).length;const ct=document.querySelector('.ctr');if(ct)ct.textContent='DANGEROUS FOUND: '+n+' / 3';render();}else{addWrong('p4');el.className='att flash-bad';setFb('p3',bad('That one is safe &mdash; '+a.r));render();setTimeout(()=>{el.className='att';},800);}};});}
  if(S.room===4){const vd=document.getElementById('vq');const done=S.clues.filter(c=>c.startsWith('v')).length;if(vd&&done<2){const q=VQ[done],pk='v'+done+'pick',pick=S.lastFb[pk];vd.innerHTML=`<div style="font-size:15px;font-weight:700;margin-bottom:10px">${q.q}</div>${q.opts.map((o,i)=>{let c='opt';if(pick!==undefined){if(i===q.c)c='opt cor';else if(i===pick)c='opt wrg';}return`<div class="${c}" id="vo${i}">${o}</div>`;}).join('')}`;q.opts.forEach((_,i)=>{const el=document.getElementById('vo'+i);if(!el)return;el.onclick=()=>{const key='v'+done;if(S.clues.includes(key))return;S.lastFb[pk]=i;if(i===q.c){el.className='opt cor';S.clues.push(key);setFb('p4',ok(q.tip));render();}else{addWrong('p5');setFb('p4',bad(q.tip));render();setTimeout(()=>{delete S.lastFb[pk];render();},1200);}};});}}
  if(S.room===5){TFQ.forEach(q=>{if(S.tfd.find(d=>d.id===q.id))return;const t=document.getElementById('tft'+q.id),f=document.getElementById('tff'+q.id);const handle=(ans)=>{if(S.tfd.find(d=>d.id===q.id))return;const isOk=(ans===q.a);if(!isOk)addWrong('p6');S.tfd.push({id:q.id,ok:isOk,pick:ans});setFb('p5',isOk?ok(q.tip):bad(q.tip));render();};if(t)t.onclick=()=>handle(true);if(f)f.onclick=()=>handle(false);});}
  if(S.room===6){PFLAGS.forEach(pf=>{const el=document.getElementById(pf.id);if(!el)return;el.onclick=(e)=>{e.stopPropagation();if(S.pf.includes(pf.id))return;if(pf.d){S.pf.push(pf.id);setFb('p6',ok('Red flag! '+pf.tip));render();}else{addWrong('p7');setFb('p6',bad('That is normal on a login page &mdash; '+pf.tip));render();}};});}
  if(S.room===7){SFLAGS.forEach(sf=>{const el=document.getElementById(sf.id);if(!el)return;el.onclick=(e)=>{e.stopPropagation();if(S.sf.includes(sf.id))return;if(sf.d){S.sf.push(sf.id);setFb('p7',ok('Red flag! '+sf.tip));render();}else{addWrong('p8');setFb('p7',bad('Not a red flag &mdash; '+sf.tip));render();}};});}
  if(S.room===8){const ci=document.getElementById('ci');if(!ci)return;ci.oninput=()=>{const val=ci.value.toUpperCase();for(let i=0;i<8;i++){const el=document.getElementById('cc'+i);if(!el)continue;if(i<val.length){el.textContent=val[i];el.className='cc'+(val[i]===CODEWORD[i]?' lit':' bad');}else{el.textContent='?';el.className='cc';}}const fb=document.getElementById('fb8');if(val===CODEWORD){if(fb)fb.innerHTML=ok('PHISHING &mdash; Code accepted! Locking down breach...');const nb2=document.createElement('button');nb2.className='btn btn-p';nb2.style.cssText='display:block;margin:10px auto 0';nb2.textContent='SEE RESULTS';nb2.onclick=()=>{S.room=9;render();};setTimeout(()=>{const f8=document.getElementById('fb8');if(f8)f8.appendChild(nb2);},50);}else if(val.length===8){if(fb)fb.innerHTML=bad('Wrong code. Review your clues.');}};}}

render();
</script>
</body>
</html>
