<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>One Question 💖</title>

<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.9.3/dist/confetti.browser.min.js"></script>

<style>
:root{
  --pink:#ff3b7a;
  --bg1:#ffd6e7;
  --bg2:#fff0f6;
}
*{box-sizing:border-box}

body{
  margin:0;
  min-height:100svh;
  display:grid;
  place-items:center;
  background:radial-gradient(circle,var(--bg2),var(--bg1));
  font-family:system-ui,-apple-system;
  overflow:hidden;
  padding:16px;
}

.card{
  width:min(92vw,420px);
  background:#ffffffcc;
  backdrop-filter:blur(10px);
  border-radius:24px;
  padding:24px;
  text-align:center;
  box-shadow:0 20px 50px rgba(0,0,0,.2);
}

h1{
  font-size:clamp(24px,5vw,34px);
  margin-bottom:20px;
}

.zone{
  position:relative;
  height:140px;
  margin-top:20px;
  touch-action:none;
}

button{
  position:absolute;
  top:50%;
  transform:translateY(-50%);
  padding:14px 24px;
  font-size:18px;
  font-weight:700;
  border-radius:999px;
  border:none;
  cursor:pointer;
  user-select:none;
  -webkit-tap-highlight-color:transparent;
  box-shadow:0 10px 24px rgba(0,0,0,.2);
}

#yes{
  left:10%;
  background:var(--pink);
  color:white;
}

#no{
  left:60%;
  background:#e5e7eb;
}

#result{
  display:none;
  font-size:26px;
  animation:pop .4s ease;
}

@keyframes pop{
  from{opacity:0;transform:scale(.9)}
  to{opacity:1;transform:scale(1)}
}

canvas{
  position:fixed;
  inset:0;
  pointer-events:none;
}
</style>
</head>

<body>

<canvas id="confetti"></canvas>

<div class="card">
  <h1>Will you be mine? 💘</h1>

  <div class="zone" id="zone">
    <button id="yes">Yes 😍</button>
    <button id="no">No 🙈</button>
  </div>

  <div id="result">YAY!!! 🎉💖</div>
</div>

<script>
const zone=document.getElementById("zone");
const yes=document.getElementById("yes");
const no=document.getElementById("no");
const result=document.getElementById("result");

let scale=1;

const confettiCanvas=document.getElementById("confetti");
const confettiInstance=confetti.create(confettiCanvas,{resize:true,useWorker:true});

function boom(){
  confettiInstance({
    particleCount:250,
    spread:140,
    startVelocity:55,
    origin:{x:.5,y:.6}
  });
}

function vibrate(){
  navigator.vibrate && navigator.vibrate(60);
}

function teleport(){
  const z=zone.getBoundingClientRect();
  const b=no.getBoundingClientRect();
  no.style.left=Math.random()*(z.width-b.width)+"px";
  no.style.top=Math.random()*(z.height-b.height)+"px";
  scale=Math.min(scale+0.12,2.4);
  yes.style.transform=`translateY(-50%) scale(${scale})`;
  vibrate();
}

zone.addEventListener("pointermove",teleport);
zone.addEventListener("touchmove",e=>{
  teleport();
  e.preventDefault();
},{passive:false});

no.addEventListener("click",e=>e.preventDefault());

yes.addEventListener("click",()=>{
  zone.style.display="none";
  result.style.display="block";
  boom();
});
</script>

</body>
</html>
