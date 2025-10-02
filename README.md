<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Birthday Gift for Shokhrukh</title>
<style>
  html, body {
    margin: 0; padding: 0;
    width: 100%; height: 100%;
    overflow: hidden;
    background: black;
    font-family: 'Arial', sans-serif;
    color: #ff6b81;
  }
  #overlay {
    position: absolute;
    width: 100%; height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    background: black;
    z-index: 10;
    text-align: center;
  }
  #overlay button {
    margin-top: 20px;
    padding: 15px 30px;
    font-size: 20px;
    border: none;
    border-radius: 10px;
    background: #ff6b81;
    color: white;
    cursor: pointer;
  }
  #overlay h1 {
    font-size: 28px;
    line-height: 1.4;
    max-width: 90%;
  }
  #scene {
    width: 100%; height: 100%;
    position: relative;
  }
  .girl, .boy, .tree, .seed, .heart, .petal {
    position: absolute;
    bottom: 0;
  }
  .girl, .boy {
    width: 50px; height: 100px;
    background: white;
    border-radius: 5px;
  }
  .seed {
    width: 10px; height: 10px;
    background: #ff6b81;
    border-radius: 50%;
    left: 50%; bottom: 20px;
    transform: translateX(-50%);
    opacity: 0;
  }
  .tree {
    width: 20px; height: 0;
    background: #4caf50;
    left: 50%; bottom: 20px;
    transform: translateX(-50%);
    opacity: 0;
  }
  .heart {
    width: 20px; height: 20px;
    background: #ff6b81;
    clip-path: polygon(50% 0%, 61% 15%, 75% 15%, 85% 30%, 85% 50%, 50% 100%, 15% 50%, 15% 30%, 25% 15%, 39% 15%);
    position: absolute;
    opacity: 0;
  }
  .petal {
    width: 10px; height: 10px;
    background: red;
    border-radius: 50%;
    position: absolute;
    top: -10px;
    animation: fall 5s linear infinite;
  }
  @keyframes fall {
    0% {top: -10px; transform: rotate(0deg);}
    100% {top: 100%; transform: rotate(360deg);}
  }
  #finalText {
    position: absolute;
    width: 100%;
    text-align: center;
    bottom: 30%;
    font-size: 28px;
    color: #ff6b81;
    opacity: 0;
  }
</style>
</head>
<body>
<div id="overlay">
  <h1>От Атии для самого доброго, милого, красивого и самого прекрасного Шохруха…</h1>
  <button id="startBtn">🌹 Открыть подарок 🌹</button>
</div>

<div id="scene">
  <div class="girl" id="girl"></div>
  <div class="boy" id="boy" style="opacity:0;"></div>
  <div class="seed" id="seed"></div>
  <div class="tree" id="tree"></div>
  <div id="finalText">Я от всего сердца желаю тебе, мой Шохрух, самого счастливого дня рождения, любовь моей жизни.</div>
</div>

<audio id="music" loop>
  <source src="https://cdn.pixabay.com/download/audio/2021/08/04/audio_5cfdf60b46.mp3?filename=romantic-piano-1102.mp3" type="audio/mpeg">
</audio>

<script>
const overlay = document.getElementById('overlay');
const startBtn = document.getElementById('startBtn');
const music = document.getElementById('music');
const girl = document.getElementById('girl');
const boy = document.getElementById('boy');
const seed = document.getElementById('seed');
const tree = document.getElementById('tree');
const finalText = document.getElementById('finalText');

startBtn.onclick = () => {
  overlay.style.display = 'none';
  music.play();
  startAnimation();
};

function startAnimation() {
  // Girl walks in
  girl.style.left = '-60px';
  girl.style.transition = 'all 2s linear';
  setTimeout(()=>{ girl.style.left = '45%'; }, 100);
  
  // Plant seed after 2.5s
  setTimeout(()=>{ seed.style.opacity = 1; }, 2500);
  
  // Hearts falling (love watering) 3 times
  for(let i=0;i<6;i++){
    setTimeout(()=>{
      createHeart(Math.random()*window.innerWidth/1.5 + window.innerWidth/4);
    }, 3000 + i*1000);
  }
  
  // Tree grows
  setTimeout(()=>{
    tree.style.opacity = 1;
    let height = 0;
    let grow = setInterval(()=>{
      height += 4;
      tree.style.height = height + 'px';
      if(height >= 150){
        clearInterval(grow);
        showBoy();
      }
    }, 50);
  }, 9000);
}

function createHeart(x){
  const heart = document.createElement('div');
  heart.className = 'heart';
  heart.style.left = x + 'px';
  heart.style.bottom = '20px';
  heart.style.opacity = 1;
  document.getElementById('scene').appendChild(heart);
  let up = 0;
  const rise = setInterval(()=>{
    up += 2;
    heart.style.bottom = 20 + up + 'px';
    if(up>100){
      clearInterval(rise);
      heart.remove();
    }
  },30);
}

function showBoy(){
  boy.style.opacity = 1;
  boy.style.left = '55%';
  boy.style.bottom = '0';
  boy.style.transition = 'all 2s linear';
  setTimeout(()=>{ showFinal(); }, 2000);
}

function showFinal(){
  // Petals shower
  for(let i=0;i<30;i++){
    const petal = document.createElement('div');
    petal.className = 'petal';
    petal.style.left = Math.random()*window.innerWidth + 'px';
    petal.style.animationDelay = Math.random()*3 + 's';
    document.getElementById('scene').appendChild(petal);
  }
  
  // Show final text
  finalText.style.transition = 'opacity 3s';
  finalText.style.opacity = 1;
}
</script>
</body>
</html>