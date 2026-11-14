# memory-hunter


<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#080b12">
<title>THE MEMORY HUNTER</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800&family=Orbitron:wght@400;600;800&display=swap');

:root{
 --gold:#d6b36d;--light:#f3dfad;--bg:#080b12;
 --panel:#111925;--muted:#8792a1;--line:#394455;
 --green:#8bc7a4;--red:#e58e8e;
}
*{box-sizing:border-box}
body{
 margin:0;background:
 radial-gradient(ellipse at 50% -10%,#354054 0%,transparent 45%),
 linear-gradient(150deg,#080b12,#101722 55%,#080b12);
 color:#f4f0e8;font-family:'Cairo',sans-serif;
 min-height:100vh;padding:18px 13px 35px;
}
button,input{font:inherit}
button{cursor:pointer}
.app{max-width:520px;margin:auto}
.topbar{display:flex;justify-content:space-between;align-items:center;
 border-bottom:1px solid #ffffff18;padding:7px 0 14px}
.brand{font-family:Orbitron,sans-serif;font-size:10px;letter-spacing:2px;color:var(--gold)}
.sound{background:#151e2a;color:var(--light);border:1px solid #465064;
 border-radius:30px;padding:7px 12px;font-size:12px}
.hero{text-align:center;padding:35px 8px 22px}
.eyebrow{font-family:Orbitron,sans-serif;color:var(--gold);font-size:10px;letter-spacing:3px}
h1{font-family:Orbitron,sans-serif;font-size:clamp(27px,8vw,40px);
 letter-spacing:2px;line-height:1.25;margin:12px 0}
.gold{color:var(--gold)}
.sub{color:var(--muted);font-size:12px;letter-spacing:2px}
.panel{
 background:linear-gradient(145deg,#172231ed,#0c121ded);
 border:1px solid #b18c4c65;border-radius:17px;padding:23px 19px;
 box-shadow:0 20px 60px #0008;position:relative;overflow:hidden;
}
.panel:before{content:"";position:absolute;inset:0;pointer-events:none;
 background:linear-gradient(120deg,#ffffff06,transparent 35%,#d6b36d05)}
.panel>*{position:relative}
.scene{
 height:150px;border-radius:12px;overflow:hidden;position:relative;
 margin-bottom:19px;border:1px solid #ffffff20;
 background:
 linear-gradient(0deg,#070b12 0%,transparent 70%),
 url("https://images.unsplash.com/photo-1519608487953-e999c86e7455?w=1000") center/cover;
}
.scene:after{content:"";position:absolute;inset:0;
 background:linear-gradient(110deg,#07101a55,#d6b36d18,#07101a88)}
.scene-title{position:absolute;z-index:1;bottom:13px;right:15px;
 color:#fff;font-family:Orbitron,sans-serif;font-size:11px;letter-spacing:2px}
.scene-symbol{position:absolute;z-index:1;top:20px;left:22px;
 font-size:42px;color:var(--light);text-shadow:0 0 25px #d6b36d}
.scene.game{
 background-image:linear-gradient(0deg,#070b12,transparent 70%),
 url("https://images.unsplash.com/photo-1511512578047-dfb367046420?w=1000");
}
.scene.archive{
 background-image:linear-gradient(0deg,#070b12,transparent 70%),
 url("https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?w=1000");
}
.scene.safe{
 background-image:linear-gradient(0deg,#070b12,transparent 70%),
 url("https://images.unsplash.com/photo-1518709268805-4e9042af9f23?w=1000");
}
h2{font-size:21px;margin:7px 0 12px}
p{line-height:2;font-size:14px;color:#d0d5dd}
.small{font-size:11px;color:var(--muted)}
.center{text-align:center}
.ltr{direction:ltr}
.rule{height:1px;background:linear-gradient(90deg,transparent,#b18c4c88,transparent);margin:18px 0}
.btn{
 width:100%;padding:13px 15px;border:1px solid var(--gold);
 border-radius:8px;background:linear-gradient(110deg,#b58b49,#ead29a);
 color:#14120e;font-weight:800;margin-top:13px;transition:.2s
}
.btn:hover{filter:brightness(1.1);transform:translateY(-1px)}
.btn.secondary{background:#182231;color:var(--light);border-color:#59677a}
.btn.ghost{background:transparent;color:var(--gold);border-color:#74603e}
input{
 width:100%;background:#080e17;border:1px solid #596477;
 color:#fff;padding:14px;border-radius:8px;text-align:center;
 margin-top:13px;outline:none;font-size:17px
}
input:focus{border-color:var(--gold);box-shadow:0 0 0 3px #d6b36d18}
input::placeholder{color:#697687}
.progress{display:flex;gap:5px;margin:17px 0;direction:ltr}
.progress span{height:4px;flex:1;border-radius:8px;background:#344052}
.progress span.done{background:var(--gold);box-shadow:0 0 9px #d6b36d77}
.level-label{font-family:Orbitron,sans-serif;color:var(--gold);
 font-size:10px;letter-spacing:2px;direction:ltr;text-align:center}
.evidence{
 background:#090f18;border:1px solid #39475a;border-radius:10px;
 padding:15px;margin:17px 0
}
.evidence-title{font-family:Orbitron,sans-serif;color:var(--gold);
 font-size:10px;letter-spacing:2px;direction:ltr}
.clue{border-right:2px solid var(--gold);padding:8px 12px;
 background:#ffffff08;margin:13px 0;border-radius:5px}
.feedback{min-height:27px;text-align:center;font-size:12px;margin-top:10px;color:var(--gold)}
.hint{display:none;background:#171c26;border:1px dashed #8b754e;
 color:#d9c59d;padding:12px;border-radius:8px;font-size:12px;line-height:1.8;margin-top:10px}
.hint.show{display:block}
.stamp{display:inline-block;border:1px solid var(--gold);color:var(--gold);
 padding:5px 12px;font-family:Orbitron,sans-serif;font-size:10px;
 letter-spacing:2px;transform:rotate(-3deg);margin:8px}
.letters{display:flex;gap:7px;justify-content:center;flex-wrap:wrap;
 direction:rtl;margin:17px 0}
.letters span{border:1px solid #7c6949;background:#171f2b;
 color:var(--light);padding:7px 10px;border-radius:6px;font-size:19px}
.board{display:grid;grid-template-columns:1fr 1fr;gap:9px;margin:17px 0}
.board div{background:#0b121c;border:1px solid #39475a;border-radius:8px;padding:12px;text-align:center}
.board b{display:block;color:var(--gold);font-family:Orbitron,sans-serif;font-size:19px}
.board small{color:var(--muted);font-size:10px}
.secret{font-family:Orbitron,sans-serif;letter-spacing:10px;font-size:26px;direction:ltr}
.hidden{display:none!important}
.message-line{opacity:0;transform:translateY(12px);animation:reveal .9s forwards;
 margin:0 0 15px;text-align:right}
@keyframes reveal{to{opacity:1;transform:translateY(0)}}
.fadein{animation:fade .8s ease}
@keyframes fade{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
.scan{height:2px;width:100%;background:linear-gradient(90deg,transparent,var(--gold),transparent);
 animation:scan 3s linear infinite;margin:14px 0}
@keyframes scan{from{transform:translateX(-100%)}to{transform:translateX(100%)}}
.foot{text-align:center;font-family:Orbitron,sans-serif;color:#687487;
 font-size:9px;letter-spacing:2px;margin-top:22px;direction:ltr}
.heart{text-align:center;color:#d6a5a5;font-size:25px}
</style>
</head>
<body>
<div class="app">

 <div class="topbar">
  <div class="brand">M.H. // PRIVATE ARCHIVE</div>
  <button class="sound" id="soundBtn" onclick="toggleSound()">♫ SOUND ON</button>
 </div>

 <header class="hero">
  <div class="eyebrow">A SPECIAL OPERATION</div>
  <h1>THE <span class="gold">MEMORY</span><br>HUNTER</h1>
  <div class="sub">ONE FILE • FOUR CLUES • ONE STORY</div>
 </header>

 <!-- INTRO -->
 <section class="panel fadein" id="intro">
  <div class="scene">
   <div class="scene-symbol">✦</div>
   <div class="scene-title">CLASSIFIED // FILE 001</div>
  </div>
  <div class="eyebrow center">CONFIDENTIAL ACCESS</div>
  <h2 class="center">تم اختيارك لمهمة خاصة...</h2>
  <p class="center">في ملف اتقفل من فترة، لكن بعض الأدلة لسه موجودة. مهمتك إنك تجمعها وتفك الشفرات وتوصل للحقيقة.</p>
  <div class="rule"></div>
  <p class="center small">مش كل حاجة واضحة من أول مرة. ركّز في التفاصيل، واستخدم عقلك.</p>
  <button class="btn" onclick="start()">ACCEPT THE MISSION</button>
 </section>

 <!-- GAME -->
 <section class="panel hidden" id="game">
  <div class="level-label" id="levelLabel">LEVEL 01</div>
  <div class="progress" id="progress">
   <span></span><span></span><span></span><span></span>
  </div>
  <div class="scene game" id="levelScene">
   <div class="scene-symbol" id="sceneSymbol">⌖</div>
   <div class="scene-title" id="sceneTitle">THE ORIGIN</div>
  </div>
  <h2 class="center" id="levelTitle"></h2>
  <p id="levelQuestion"></p>
  <div class="evidence" id="evidence"></div>
  <div class="letters hidden" id="letters"></div>
  <input id="answer" placeholder="اكتب الإجابة هنا..." autocomplete="off">
  <button class="btn" onclick="submitAnswer()">DECODE & SUBMIT</button>
  <button class="btn ghost" id="hintBtn" onclick="showHint()">REQUEST A HINT</button>
  <div class="hint" id="hint"></div>
  <div class="feedback" id="feedback"></div>
 </section>

 <!-- LOCK -->
 <section class="panel hidden" id="lock">
  <div class="scene safe">
   <div class="scene-symbol">▣</div>
   <div class="scene-title">THE FINAL SECURITY LOCK</div>
  </div>
  <div class="eyebrow center">ALL CLUES COLLECTED</div>
  <h2 class="center">الخزنة الأخيرة</h2>
  <p class="center">كل دليل كشف رقم. اجمعهم بالترتيب وافتح الملف.</p>
  <div class="board">
   <div><b>04</b><small>LETTERS IN THE GAME</small></div>
   <div><b>08</b><small>LETTERS IN THE SECRET WORD</small></div>
   <div><b>03</b><small>LETTERS IN THE OTHER WORD</small></div>
   <div><b>???</b><small>FINAL ACCESS CODE</small></div>
  </div>
  <input id="code" class="secret" maxlength="3" inputmode="numeric" placeholder="•••">
  <button class="btn" onclick="unlock()">UNLOCK THE ARCHIVE</button>
  <div class="feedback" id="lockFeedback"></div>
 </section>

 <!-- COMPLETED -->
 <section class="panel hidden center" id="completed">
  <div class="stamp">ACCESS GRANTED</div>
  <div class="scene archive">
   <div class="scene-symbol">✧</div>
   <div class="scene-title">ARCHIVE RESTORED</div>
  </div>
  <div class="eyebrow">MISSION COMPLETED</div>
  <h2>كل الأدلة اتجمعت بنجاح.</h2>
  <p>بس في ملف أخير... مكنش موجود في أي خريطة.</p>
  <div class="scan"></div>
  <button class="btn" onclick="openFinal()">OPEN THE LAST FILE</button>
 </section>

 <!-- FINAL MESSAGE -->
 <section class="panel hidden" id="final">
  <div class="eyebrow center">A PERSONAL MESSAGE</div>
  <h2 class="center">إلى شخص يستحق كل خير...</h2>
  <div class="scene archive">
   <div class="scene-symbol">♡</div>
   <div class="scene-title">NOT A SECRET. JUST A MEMORY.</div>
  </div>
  <div class="rule"></div>
  <div id="messageText"></div>
  <div class="rule"></div>
  <p class="center gold">Some memories never lose their beauty.</p>
  <div class="heart">♥</div>
  <h2 class="center gold">HAPPY BIRTHDAY</h2>
  <p class="center small">END OF MISSION // BEGINNING OF ANOTHER YEAR</p>
 </section>

 <div class="foot">MEMORY HUNTER SYSTEM // 2026</div>
</div>

<script>
/* Original sound effects generated by the browser */
let soundOn = true;
let audioContext;

function tone(freq=440,duration=.12,type="sine",volume=.035){
 if(!soundOn)return;
 try{
  audioContext=audioContext||new (window.AudioContext||window.webkitAudioContext)();
  const osc=audioContext.createOscillator();
  const gain=audioContext.createGain();
  osc.type=type;osc.frequency.value=freq;
  gain.gain.setValueAtTime(volume,audioContext.currentTime);
  gain.gain.exponentialRampToValueAtTime(.001,audioContext.currentTime+duration);
  osc.connect(gain);gain.connect(audioContext.destination);
  osc.start();osc.stop(audioContext.currentTime+duration);
 }catch(e){}
}
function successSound(){
 tone(520,.12);setTimeout(()=>tone(660,.14),100);
 setTimeout(()=>tone(880,.25),220);
}
function errorSound(){tone(170,.22,"triangle");}
function openSound(){
 tone(330,.2);setTimeout(()=>tone(440,.2),130);
 setTimeout(()=>tone(590,.4),260);
}
function toggleSound(){
 soundOn=!soundOn;
 document.getElementById("soundBtn").textContent=soundOn?"♫ SOUND ON":"♫ SOUND OFF";
 if(soundOn)tone(600,.12);
}

const levels=[
 {
  label:"LEVEL 01 // THE ORIGIN",
  title:"أول خيط في الحكاية",
  scene:"THE DROP ZONE",symbol:"⌖",image:"game",
  question:"في عالم افتراضي، البداية بتكون من فوق... طيارة، قفزة، وباراشوت. كل لاعب بيبدأ من نفس النقطة، لكن مش كل الناس بتكمل للنهاية. إيه اسم اللعبة؟",
  evidence:"<div class='evidence-title'>EVIDENCE 01</div><div class='clue'>الدليل: أربع حروف بالإنجليزي.<br>والبداية كانت من لعبة جمعت اتنين في نفس العالم.</div>",
  hint:"فكّر في اللعبة اللي فيها Battle Royale، وبتبدأ بالنزول من طيارة.",
  answers:["pubg","بوبجي","ببجي"]
 },
 {
  label:"LEVEL 02 // THE CODE",
  title:"شفرة من ثلاث حروف",
  scene:"THE LANGUAGE",symbol:"⌘",
  question:"الكلمة دي مش كلمة سر عادية. بتتقال في مواقف كتير، بسيطة جدًا، لكن مع الوقت بقت جزء من لغة خاصة. عدد حروفها 3.",
  evidence:"<div class='evidence-title'>EVIDENCE 02</div><div class='clue'>أول حرف: ح<br>آخر حرف: و<br>والحرف اللي في النص بيكمل المعنى.</div>",
  hint:"الكلمة اللي بتوصف حاجة لطيفة أو كويسة... وبتتقال كتير: حـ _ ـو.",
  answers:["حلو"]
 },
 {
  label:"LEVEL 03 // THE HIDDEN WORD",
  title:"إعادة ترتيب الأدلة",
  scene:"THE HIDDEN MESSAGE",symbol:"✧",
  question:"في كلمة اتخبّت جوه الحروف دي. المطلوب إنك تعيد ترتيبها وتكتشف الكلمة اللي معناها مش واضح لأي حد غريب عن الحكاية.",
  evidence:"<div class='evidence-title'>EVIDENCE 03</div><div class='clue'>كل الحروف موجودة بالفعل. مفيش حرف ناقص، ومفيش حرف زيادة.</div>",
  letters:["ل","ي","ك","ر","و","س","ب","ا"],
  hint:"ابدأ بالحروف الأولى: ا ب س ... وبعدها كمّل ترتيب الكلمة الخاصة.",
  answers:["ابسروكلي"]
 },
 {
  label:"LEVEL 04 // THE FINAL DEDUCTION",
  title:"آخر استنتاج",
  scene:"THE MEMORY ARCHIVE",symbol:"◈",
  question:"وصلت لآخر مرحلة يا Detective... عندك 3 أدلة:<br><br>1. البداية كانت مجرد لعبة.<br>2. كلمة بسيطة بقت جزء من قاموس خاص.<br>3. كلمة غريبة محدش هيفهم معناها غير أصحابها.<br><br>إيه الحاجة المشتركة بين التلاتة؟ حاجة مش لعبة، ولا كلمة، ولا شفرة... لكنها السبب إن الأدلة دي كلها بقت ليها معنى.",
  evidence:"<div class='evidence-title'>FINAL EVIDENCE</div><div class='clue'>مش شيء تقدر تمسكه بإيدك... لكنه ممكن يفضل معاك سنين.</div>",
  hint:"فكّر في الحاجات اللي بنفتكرها ونبتسم لما نفتكرها.",
  answers:["الذكريات","ذكريات"]
 }
];

let current=0;
function showScreen(id){
 ["intro","game","lock","completed","final"].forEach(x=>
  document.getElementById(x).classList.add("hidden"));
 const el=document.getElementById(id);
 el.classList.remove("hidden");
 el.classList.add("fadein");
 window.scrollTo({top:0,behavior:"smooth"});
}
function start(){
 openSound();showScreen("game");loadLevel();
}
function normalize(s){
 return s.toLowerCase().trim().replace(/\s+/g,"")
 .replace(/[أإآ]/g,"ا").replace(/ى/g,"ي");
}
function loadLevel(){
 const l=levels[current];
 document.getElementById("levelLabel").textContent=l.label;
 document.getElementById("levelTitle").textContent=l.title;
 document.getElementById("levelQuestion").innerHTML=l.question;
 document.getElementById("evidence").innerHTML=l.evidence;
 document.getElementById("sceneTitle").textContent=l.scene;
 document.getElementById("sceneSymbol").textContent=l.symbol;
 document.getElementById("levelScene").className="scene "+(current===0?"game":current===3?"archive":"");
 const dots=document.querySelectorAll("#progress span");
 dots.forEach((d,i)=>d.classList.toggle("done",i<current));
 const letters=document.getElementById("letters");
 letters.innerHTML="";
 letters.classList.toggle("hidden",!l.letters);
 if(l.letters)l.letters.forEach(ch=>{
  const s=document.createElement("span");s.textContent=ch;letters.appendChild(s);
 });
 document.getElementById("answer").value="";
 document.getElementById("feedback").textContent="";
 document.getElementById("hint").classList.remove("show");
 document.getElementById("hint").textContent=l.hint;
 document.getElementById("hintBtn").textContent="REQUEST A HINT";
 document.getElementById("answer").focus();
}
function showHint(){
 document.getElementById("hint").classList.add("show");
 document.getElementById("hintBtn").textContent="HINT UNLOCKED";
 tone(420,.12);
}
function submitAnswer(){
 const val=normalize(document.getElementById("answer").value);
 const fb=document.getElementById("feedback");
 if(!val){fb.textContent="اكتب إجابتك الأول.";return;}
 const correct=levels[current].answers.some(a=>normalize(a)===val);
 if(!correct){
  fb.textContent="ACCESS DENIED — الدليل مش متطابق. حاول تاني.";
  errorSound();return;
 }
 fb.textContent="✓ EVIDENCE VERIFIED";
 successSound();
 current++;
 setTimeout(()=>{
  if(current<levels.length)loadLevel();
  else showScreen("lock");
 },1000);
}
function unlock(){
 const val=document.getElementById("code").value.trim();
 const fb=document.getElementById("lockFeedback");
 if(val==="483"){
  fb.textContent="ACCESS GRANTED ✓";
  successSound();
  setTimeout(()=>{openSound();showScreen("completed");},1000);
 }else{
  fb.textContent="WRONG CODE — راجع عدد الحروف في الأدلة.";
  errorSound();
 }
}
const finalMessage=[
"يمكن تكون دي آخر مرحلة في اللعبة، بس الحقيقة إن في حاجات ملهاش نهاية، حتى لو الأيام أخدتها في طريق تاني.",
"عايزة أقولك إنك من الأشخاص الجميلة والمميزة اللي قابلتهم في حياتي، وإنك شخص غالي عندي أكتر ما تتخيل.",
"إنت شخص طيب أوي، وجدع، وحنين، وفيك تفاصيل كتير تخلي أي حد يعرفك يحمد ربنا إن في حياته شخص زيك. ويا بخت أي حد عنده حد بقلبك وبأصلك وبجمال روحك.",
"يمكن اتخنقنا، ويمكن اختلفنا، ويمكن في وقت ما كل واحد فينا كمل طريقه بعيد عن التاني، بس ده عمره ما هيخليني أنكر إن كان بينا أيام وذكريات جميلة بجد.",
"وهتفضل من الذكريات اللي بحب أرجعلها من وقت للتاني، وأبتسم، وأفصل بيها شوية عن دوشة الدنيا. ذكريات ليها مكانتها الخاصة، ومش محتاجة تتكرر عشان تفضل حلوة.",
"مش كل شخص بنقابله بيكون مجرد مرحلة عابرة، في أشخاص بيسيبوا جوانا أثر حلو بيفضل معانا، وإنت من الناس دي.",
"في يوم ميلادك، أتمنى لك من قلبي إن الحياة تكون حنينة عليك قد طيبة قلبك، وإنك تفضل ناجح ومبسوط ومحقق كل اللي نفسك فيه، وإنك تلاقي دايمًا ناس تقدّرك وتعرف قيمتك وتديك من الحنية والجدعنة اللي بتديهُم للي حواليك.",
"كل سنة وإنت طيب، وكل سنة وإنت شخص جميل ومميز زي ما إنت.",
"ويا بخت الدنيا بالناس اللي زيك. ❤️"
];
function openFinal(){
 showScreen("final");openSound();
 const box=document.getElementById("messageText");
 box.innerHTML="";
 finalMessage.forEach((line,i)=>{
  const p=document.createElement("p");
  p.className="message-line";p.textContent=line;
  p.style.animationDelay=(i*1.8)+"s";
  box.appendChild(p);
 });
}
document.getElementById("answer").addEventListener("keydown",e=>{
 if(e.key==="Enter")submitAnswer();
});
document.getElementById("code").addEventListener("keydown",e=>{
 if(e.key==="Enter")unlock();
});
</script>
</body>
</html>
