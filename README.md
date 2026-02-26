<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<title>손오공 원숭이</title>

<style>
  body{
    margin:0;
    height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    background:radial-gradient(circle,#222,#000);
    overflow:hidden;
    font-family:sans-serif;
  }

  /* 원숭이 */
  .monkey{
    width:180px;
    height:180px;
    cursor:pointer;
    animation: kungfu 3s infinite ease-in-out;
    transition: transform .2s;
  }

  .monkey:active{
    transform:scale(0.9);
  }

  /* 둥실둥실 무술 느낌 */
  @keyframes kungfu{
    0%   { transform:translateY(0) rotate(0deg); }
    25%  { transform:translateY(-12px) rotate(-3deg); }
    50%  { transform:translateY(0) rotate(3deg); }
    75%  { transform:translateY(-8px) rotate(-2deg); }
    100% { transform:translateY(0) rotate(0deg); }
  }

  /* 폭발 파티클 */
  .particle{
    position:absolute;
    width:10px;
    height:10px;
    border-radius:50%;
    pointer-events:none;
    animation: explode 700ms forwards;
  }

  @keyframes explode{
    from{
      opacity:1;
      transform:translate(0,0) scale(1);
    }
    to{
      opacity:0;
      transform:translate(var(--x),var(--y)) scale(0.2);
    }
  }
</style>
</head>

<body>

<!-- SVG로 만든 손오공 느낌 원숭이 (이미지 깨짐 없음) -->
<svg class="monkey" viewBox="0 0 200 200" id="monkey">
  <!-- 얼굴 -->
  <circle cx="100" cy="110" r="70" fill="#c68642"/>
  
  <!-- 귀 -->
  <circle cx="35" cy="100" r="25" fill="#a66a2b"/>
  <circle cx="165" cy="100" r="25" fill="#a66a2b"/>

  <!-- 얼굴 안 -->
  <ellipse cx="100" cy="125" rx="45" ry="35" fill="#f2d2a9"/>

  <!-- 눈 -->
  <circle cx="75" cy="105" r="8" fill="#000"/>
  <circle cx="125" cy="105" r="8" fill="#000"/>

  <!-- 눈썹 (손오공 느낌) -->
  <rect x="60" y="85" width="30" height="6" rx="3" fill="#000"/>
  <rect x="110" y="85" width="30" height="6" rx="3" fill="#000"/>

  <!-- 입 -->
  <path d="M80 140 Q100 155 120 140" stroke="#000" stroke-width="4" fill="none"/>

  <!-- 머리띠 -->
  <rect x="30" y="60" width="140" height="15" rx="8" fill="gold"/>
</svg>

<script>
const monkey = document.getElementById("monkey");

monkey.addEventListener("click", (e)=>{

  const rect = monkey.getBoundingClientRect();
  const centerX = rect.left + rect.width/2;
  const centerY = rect.top + rect.height/2;

  // 폭발 파티클 생성
  for(let i=0;i<40;i++){
    const p = document.createElement("div");
    p.className="particle";

    const angle = Math.random()*Math.PI*2;
    const distance = 120 + Math.random()*80;

    p.style.left = centerX+"px";
    p.style.top = centerY+"px";
    p.style.background =
      `hsl(${Math.random()*60},100%,50%)`;

    p.style.setProperty("--x",
      Math.cos(angle)*distance+"px");
    p.style.setProperty("--y",
      Math.sin(angle)*distance+"px");

    document.body.appendChild(p);

    setTimeout(()=>p.remove(),700);
  }

  // 충격 반응
  monkey.style.transform="scale(1.3)";
  setTimeout(()=>{
    monkey.style.transform="";
  },150);
});
</script>

</body>
</html>
