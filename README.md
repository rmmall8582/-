<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🎊 축제 운세 뽑기 🎊</title>

<style>
body{
  margin:0;
  height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
  text-align:center;
  font-family:Arial,sans-serif;
  overflow:hidden;
  transition:background 0.5s;
}

/* 메인 */
.container{
  z-index:10;
  width:90%;
}

h1{ font-size:7vw; }
#fortune{
  font-size:8vw;
  font-weight:bold;
  margin:25px 0;
}
#score{ font-size:6vw; }
.small{ font-size:3.5vw; opacity:0.8; }

/* 컨페티 */
.confetti{
  position:absolute;
  width:8px;
  height:8px;
  top:-10px;
  animation:fall linear forwards;
}
@keyframes fall{
  to{ transform:translateY(110vh) rotate(360deg); }
}

/* 떠다니는 이모지 */
.floating{
  position:absolute;
  font-size:30px;
  animation:floatUp linear forwards;
}
@keyframes floatUp{
  from{ transform:translateY(100vh); opacity:1;}
  to{ transform:translateY(-10vh); opacity:0;}
}

/* ===== 원숭이 ===== */
#monkey{
  position:fixed;
  width:120px;
  height:120px;
  left:50px;
  top:50px;
  z-index:9999;
  cursor:pointer;
  animation:floatMonkey 3s infinite ease-in-out;
}

@keyframes floatMonkey{
  0%{transform:translateY(0);}
  50%{transform:translateY(-10px);}
  100%{transform:translateY(0);}
}

/* 춤 */
.dance{
  animation: danceMove 0.4s infinite alternate !important;
}
@keyframes danceMove{
  from{ transform:rotate(-12deg) scale(1.1);}
  to{ transform:rotate(12deg) scale(1.1);}
}

/* 화남 */
.angry{
  filter:hue-rotate(-50deg) saturate(2);
}

/* 폭발 파티클 */
.particle{
  position:fixed;
  width:10px;
  height:10px;
  border-radius:50%;
  pointer-events:none;
  animation:explode 700ms forwards;
}
@keyframes explode{
  from{opacity:1;transform:translate(0,0) scale(1);}
  to{opacity:0;transform:translate(var(--x),var(--y)) scale(0.2);}
}
</style>
</head>

<body>

<div class="container">
  <h1>🎉 오늘의 축제 운세 🎉</h1>
  <div id="fortune"></div>
  <div id="score"></div>
  <div class="small">📱 다시 QR 찍으면 새로운 운세!</div>
</div>

<!-- 손오공 원숭이 -->
<svg id="monkey" viewBox="0 0 200 200">
  <circle cx="100" cy="110" r="70" fill="#c68642"/>
  <circle cx="35" cy="100" r="25" fill="#a66a2b"/>
  <circle cx="165" cy="100" r="25" fill="#a66a2b"/>
  <ellipse cx="100" cy="125" rx="45" ry="35" fill="#f2d2a9"/>
  <circle cx="75" cy="105" r="8"/>
  <circle cx="125" cy="105" r="8"/>
  <rect x="60" y="85" width="30" height="6" rx="3"/>
  <rect x="110" y="85" width="30" height="6" rx="3"/>
  <path d="M80 140 Q100 155 120 140" stroke="#000" stroke-width="4" fill="none"/>
  <rect x="30" y="60" width="140" height="15" rx="8" fill="gold"/>
</svg>

<script>

/* ===== 운세 ===== */
const fortunes=[
"오늘 점심 메뉴 고민하다 하루 끝남 😂",
"운동은 마음속으로 완료 💪",
"배고프면 예민해진다 🍗",
"오늘은 눕는 게 이득 🛏️",
"계획은 완벽, 실행은 내일부터 😎",
"괜히 냉장고 세 번 열어본다 🧊",
"다이어트는 평행세계의 내가 한다 🌍",
"웃으면 복이 온다 😆",
"오늘의 적은 귀찮음 😴",
"치킨이 당신을 기다린다 🍗🔥"
];

const randomFortune=
fortunes[Math.floor(Math.random()*fortunes.length)];
fortune.innerText=randomFortune;

const score=Math.floor(Math.random()*41)+60;
scoreEl=document.getElementById("score");
scoreEl.innerText="✨ 오늘의 운세 점수: "+score+"점!";

/* 배경 */
const colors=["#FFD700","#FFB6C1","#87CEFA","#98FB98","#FFA07A"];
document.body.style.background=
colors[Math.floor(Math.random()*colors.length)];

/* 컨페티 */
for(let i=0;i<25;i++){
  const c=document.createElement("div");
  c.className="confetti";
  c.style.left=Math.random()*100+"vw";
  c.style.background=colors[Math.floor(Math.random()*colors.length)];
  c.style.animationDuration=(Math.random()*2+2)+"s";
  document.body.appendChild(c);
}

/* 이모지 */
const emojis=["🎉","✨","🎈","💖","🔥"];
for(let i=0;i<15;i++){
  const e=document.createElement("div");
  e.className="floating";
  e.innerText=emojis[Math.floor(Math.random()*emojis.length)];
  e.style.left=Math.random()*100+"vw";
  e.style.animationDuration=(Math.random()*3+3)+"s";
  document.body.appendChild(e);
}

/* ===== 원숭이 이동 ===== */
const monkey=document.getElementById("monkey");
let x=50,y=50,dx=2,dy=1.5;

function moveMonkey(){
  const w=window.innerWidth-120;
  const h=window.innerHeight-120;

  x+=dx;
  y+=dy;

  if(x<0||x>w) dx*=-1;
  if(y<0||y>h) dy*=-1;

  monkey.style.left=x+"px";
  monkey.style.top=y+"px";

  requestAnimationFrame(moveMonkey);
}
moveMonkey();

/* 점수 반응 */
if(score>=85){
  monkey.classList.add("dance");
}else if(score<=70){
  monkey.classList.add("angry");
}

/* 클릭 폭발 */
monkey.addEventListener("click",()=>{
  for(let i=0;i<35;i++){
    const p=document.createElement("div");
    p.className="particle";

    const angle=Math.random()*Math.PI*2;
    const dist=120+Math.random()*60;

    p.style.left=(x+60)+"px";
    p.style.top=(y+60)+"px";
    p.style.background=`hsl(${Math.random()*360},100%,50%)`;

    p.style.setProperty("--x",Math.cos(angle)*dist+"px");
    p.style.setProperty("--y",Math.sin(angle)*dist+"px");

    document.body.appendChild(p);
    setTimeout(()=>p.remove(),700);
  }
});
</script>

</body>
</html>
