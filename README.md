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
  transition:background .5s;
  position:relative;
}

.container{
  padding:20px;
  animation:fadeIn 1s ease;
  width:90%;
  z-index:10;
}

h1{font-size:7vw;margin-bottom:20px;}
#fortune{font-size:8vw;font-weight:bold;margin:25px 0;}
#score{font-size:6vw;margin-top:15px;}
.small{font-size:3.5vw;margin-top:20px;opacity:.8;}

@keyframes fadeIn{
  from{opacity:0;transform:scale(.9);}
  to{opacity:1;transform:scale(1);}
}

/* 컨페티 */
.confetti{
  position:absolute;
  width:8px;
  height:8px;
  top:-10px;
  animation:fall linear forwards;
}

@keyframes fall{
  to{transform:translateY(110vh) rotate(360deg);}
}

/* ===== 손오공 원숭이 ===== */
.monkey{
  position:absolute;
  bottom:15%;
  z-index:9999;
  animation:
    entrance 1.2s ease-out forwards,
    kungfu 3s infinite ease-in-out 1.2s;
}

.monkey img{
  width:90px;
  filter:drop-shadow(0 8px 6px rgba(0,0,0,.3));
}

/* 등장 */
@keyframes entrance{
  0%{transform:translateY(-120vh) scale(.5) rotate(-180deg);opacity:0;}
  70%{transform:translateY(20px) scale(1.1);opacity:1;}
  100%{transform:translateY(0) scale(1);}
}

/* 무술 이동 */
@keyframes kungfu{
  0%{transform:translateX(-40vw) translateY(0);}
  25%{transform:translateX(-10vw) translateY(-35px) rotate(-10deg);}
  50%{transform:translateX(20vw) translateY(0) rotate(10deg);}
  75%{transform:translateX(10vw) translateY(-25px) rotate(-8deg);}
  100%{transform:translateX(-40vw) translateY(0);}
}

/* 착지 폭발 */
.burst{
  position:absolute;
  width:12px;
  height:12px;
  border-radius:50%;
  animation:burstMove .8s ease-out forwards;
}

@keyframes burstMove{
  to{
    transform:translate(var(--x),var(--y));
    opacity:0;
  }
}

/* 떠다니는 이모지 */
.floating{
  position:absolute;
  font-size:30px;
  animation:floatUp linear forwards;
}

@keyframes floatUp{
  from{transform:translateY(100vh);opacity:1;}
  to{transform:translateY(-10vh);opacity:0;}
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

<!-- 원숭이 -->
<div class="monkey">
  <img src="son_goku_monkey.png">
</div>

<script>
const fortunes=[
"오늘 점심 메뉴 고민하다 하루 끝남 😂",
"운동은 마음속으로 완료 💪",
"배고프면 예민해진다. 먼저 먹어라 🍗",
"오늘은 눕는 게 이득 🛏️",
"계획은 완벽, 실행은 내일부터 😎",
"괜히 냉장고를 세 번 열어본다 🧊",
"다이어트는 평행세계의 내가 한다 🌍",
"웃으면 복이 오고, 안 웃어도 하루는 간다 😆",
"오늘의 적은 귀찮음 😴",
"치킨이 당신을 기다린다 🍗🔥"
];

document.getElementById("fortune").innerText=
fortunes[Math.floor(Math.random()*fortunes.length)];

const score=Math.floor(Math.random()*41)+60;
document.getElementById("score").innerText=
"✨ 오늘의 운세 점수: "+score+"점!";

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

/* 떠다니는 이모지 */
const emojis=["🎉","✨","🎈","💖","🔥"];
for(let i=0;i<15;i++){
  const el=document.createElement("div");
  el.className="floating";
  el.innerText=emojis[Math.floor(Math.random()*emojis.length)];
  el.style.left=Math.random()*100+"vw";
  el.style.animationDuration=(Math.random()*3+3)+"s";
  document.body.appendChild(el);
}

/* 착지 폭발 */
setTimeout(()=>{
  const monkey=document.querySelector(".monkey");
  const rect=monkey.getBoundingClientRect();

  for(let i=0;i<35;i++){
    const p=document.createElement("div");
    p.className="burst";

    const angle=Math.random()*Math.PI*2;
    const distance=Math.random()*120+40;

    p.style.left=rect.left+rect.width/2+"px";
    p.style.top=rect.top+rect.height/2+"px";
    p.style.background=colors[Math.floor(Math.random()*colors.length)];

    p.style.setProperty("--x",Math.cos(angle)*distance+"px");
    p.style.setProperty("--y",Math.sin(angle)*distance+"px");

    document.body.appendChild(p);
    setTimeout(()=>p.remove(),800);
  }
},1100);
</script>

</body>
</html>
