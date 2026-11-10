<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Mint Run — A Coin-Collecting Adventure</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
:root{--ink:#183e34;--paper:#f2f0df;--green:#bce05e;--muted:#617467;--line:#cbd0bb}
*{box-sizing:border-box}
body{margin:0;background:var(--paper);color:var(--ink);font-family:"Space Grotesk",sans-serif}
button{font:inherit;cursor:pointer}
button:focus-visible,a:focus-visible{outline:3px solid #dc7439;outline-offset:5px}
header{max-width:1200px;margin:auto;padding:25px 30px;display:flex;justify-content:space-between;align-items:center;border-bottom:1px solid var(--line)}
.brand{font-weight:700;font-size:23px;letter-spacing:-1px;display:flex;align-items:center;gap:10px}
.brand-mark{height:26px;width:26px;border:7px solid var(--ink);border-radius:50%;box-shadow:inset 0 0 0 2px var(--paper);background:#edbd4b}
.micro{font-family:"Space Mono",monospace;font-size:11px;text-transform:uppercase;letter-spacing:1.5px}
.header-note{color:var(--muted)}
main{max-width:1200px;margin:auto;padding:42px 30px 25px}
.intro{display:flex;justify-content:space-between;gap:30px;align-items:end;margin-bottom:28px;animation:enter .7s both}
h1{font-size:clamp(40px,6vw,72px);line-height:1.02;letter-spacing:-4px;margin:12px 0 0;font-weight:700}
h1 span{color:#6b8850}
.intro p{max-width:300px;font-size:15px;line-height:1.65;margin:0 0 4px;color:var(--muted)}
.game-shell{background:var(--ink);padding:14px;border-radius:15px;box-shadow:0 10px 0 #d9ddc7;animation:enter .7s .12s both}
.hud{color:var(--paper);display:flex;align-items:center;justify-content:space-between;gap:15px;padding:8px 12px 20px}
.stats{display:flex;gap:35px}
.stat label{display:block;font-family:"Space Mono",monospace;font-size:9px;letter-spacing:1.5px;color:#a6bdac;margin-bottom:5px}
.stat strong{font-family:"Space Mono",monospace;font-size:20px;font-weight:400}
.stat strong small{font-size:12px;color:#a6bdac}
.hearts{color:#edbd4b;letter-spacing:3px}
.tools{display:flex;gap:8px}
.icon-btn{border:1px solid #617a6b;background:transparent;color:var(--paper);padding:10px 13px;border-radius:6px;font-size:12px;transition:.2s}
.icon-btn:hover{background:#365949;transform:translateY(-2px)}
button:active{transform:translateY(1px)}
.stage{position:relative;background:#c4d5a4;border-radius:7px;overflow:hidden;aspect-ratio:2.13}
canvas{display:block;width:100%;height:100%;image-rendering:pixelated}
.overlay{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;background:rgba(22, fifty,40,.3);background:#163e3438;backdrop-filter:blur(4px);text-align:center;padding:20px}
.overlay[hidden]{display:none}
.overlay-inner{max-width:440px;padding:32px;background:#f2f0dfed;border:1px solid #fff9;box-shadow:9px 9px 0 #183e3433}
.stamp{display:inline-block;color:#607d43;border:1px solid #a7b391;padding:6px 10px;margin-bottom:12px}
.overlay h2{font-size:clamp(24px,4vw,42px);line-height:1.05;letter-spacing:-2px;margin:8px 0 14px}
.overlay p{color:var(--muted);font-size:14px;line-height:1.6;margin:0 0 23px}
.primary{background:var(--ink);color:var(--paper);border:0;padding:14px 28px;font-weight:600;transition:.2s;box-shadow:4px 4px 0 #b4c29d}
.primary:hover{background:#365d43;transform:translate(-2px,-2px);box-shadow:6px 6px 0 #b4c29d}
.game-bottom{display:flex;justify-content:space-between;gap:15px;color:#bacbb7;padding:15px 10px 1px;font-family:"Space Mono",monospace;font-size:10px}
.status{color:#daec8b}
.below{display:grid;grid-template-columns:1fr 1.3fr;gap:60px;margin-top:36px;animation:enter .7s .25s both}
.instructions{display:flex;gap:17px;align-items:start}
.key-group{display:flex;gap:4px}
kbd{display:inline-flex;align-items:center;justify-content:center;width:26px;height:28px;border:1px solid #acb49d;border-bottom-width:3px;border-radius:4px;font:12px "Space Mono",monospace;background:#f9f8ed}
.instructions h3{font-size:13px;margin:1px 0 6px}
.instructions p{font-size:12px;line-height:1.7;margin:0;color:var(--muted)}
.levels{display:flex;gap:18px}
.level-item{flex:1;border-top:2px solid var(--line);padding-top:11px;color:var(--muted);transition:.3s}
.level-item.active{border-color:var(--ink);color:var(--ink)}
.level-item strong{display:block;font-size:13px;margin-top:5px}
.level-item small{font-size:11px}
footer{max-width:1200px;margin:35px auto 0;padding:20px 30px;border-top:1px solid var(--line);display:flex;justify-content:space-between;color:var(--muted);font-size:10px}
.touch{display:none;justify-content:center;gap:7px;margin-top:20px}
.touch button{height:46px;width:52px;background:var(--ink);color:var(--paper);border:0;border-radius:6px;touch-action:none;font-size:21px}
@keyframes enter{from{opacity:0;transform:translateY(15px)}to{opacity:1;transform:translateY(0)}}
@media(max-width:700px){header{padding:20px}.header-note{display:none}main{padding:26px 15px}.intro{display:block}.intro p{margin-top:18px;max-width:100%}h1{letter-spacing:-2px}.stats{gap:18px}.hud{padding:6px 3px 15px;gap:7px}.stat strong{font-size:16px}.icon-btn{padding:8px;font-size:11px}.stage{aspect-ratio:1.3}.below{grid-template-columns:1fr;gap:25px}.touch{display:flex}.game-bottom{font-size:8px}.overlay-inner{padding:22px}.overlay p{font-size:12px;margin-bottom:14px}.overlay h2{margin-top:0}footer{padding:20px 15px;gap:20px}}
@media(prefers-reduced-motion:reduce){*{animation:none!important;transition:none!important}}
</style>
</head>
<body>
<header>
<div class="brand"><span class="brand-mark" aria-hidden="true"></span>mint run.</div>
<div class="micro header-note">A little adventure. A lot of gold.</div>
</header>
<main>
<section class="intro">
<div><div class="micro">Coin collector / original browser game</div><h1>Small explorer.<br><span>Golden ambitions.</span></h1></div>
<p>Find every coin. Dodge the wandering thorns. Explore three little worlds, one golden trail at a time.</p>
</section>
<section class="game-shell" aria-label="Mint Run game">
<div class="hud">
<div class="stats">
<div class="stat"><label>LEVEL</label><strong id="level">01 <small>/ 03</small></strong></div>
<div class="stat"><label>SCORE</label><strong id="score">0000</strong></div>
<div class="stat"><label>LIVES</label><strong id="lives" class="hearts" aria-label="3 lives">♥♥♥</strong></div>
</div>
<div class="tools"><button class="icon-btn" id="sound" aria-pressed="false">Sound off</button><button class="icon-btn" id="pause" aria-label="Pause game">Ⅱ</button></div>
</div>
<div class="stage">
<canvas id="game" width="960" height="450" aria-label="Collect gold coins using the arrow keys or WASD. Avoid red moving thorns and dark stone walls."></canvas>
<div class="overlay" id="overlay">
<div class="overlay-inner">
<span class="micro stamp" id="overlayTag">Your expedition starts here</span>
<h2 id="overlayTitle">Follow the gold.</h2>
<p id="overlayText">Collect all the coins to unlock the next world. You have three lives per level. Hit a thorn? Keep going. Lose them all? That level restarts.</p>
<button class="primary" id="start">Let's play ↗</button>
</div>
</div>
</div>
<div class="game-bottom"><span id="status" class="status" role="status">READY WHEN YOU ARE</span><span id="collection">COINS 00 / 10</span></div>
</section>
<div class="touch" aria-label="Touch movement controls">
<button data-dir="ArrowLeft" aria-label="Move left">←</button><button data-dir="ArrowUp" aria-label="Move up">↑</button><button data-dir="ArrowDown" aria-label="Move down">↓</button><button data-dir="ArrowRight" aria-label="Move right">→</button>
</div>
<section class="below" aria-label="How to play">
<div class="instructions">
<div class="key-group" aria-hidden="true"><kbd>↑</kbd><kbd>←</kbd><kbd>↓</kbd><kbd>→</kbd></div>
<div><h3>Aim for gold. Stay curious.</h3><p>Arrow keys or WASD to move. P to pause.<br>On mobile, use the direction buttons.</p></div>
</div>
<div class="levels">
<div class="level-item active"><span class="micro">01 / Meadow</span><strong>The green beginning</strong><small>10 coins · easy does it</small></div>
<div class="level-item"><span class="micro">02 / Dunes</span><strong>A warmer welcome</strong><small>12 coins · watch your step</small></div>
<div class="level-item"><span class="micro">03 / Twilight</span><strong>The final wander</strong><small>14 coins · make it count</small></div>
</div>
</section>
</main>
<footer><span class="micro">Made for the joy of the little things.</span><span>Original artwork & synthesized sound. No borrowed assets.</span></footer>
<script>
(()=>{
const canvas=document.getElementById('game'),ctx=canvas.getContext('2d');
const $=id=>document.getElementById(id);
const W=960,H=450,keys=new Set();
let level=0,score=0,baseScore=0,lives=3,coins=[],walls=[],enemies=[],player={x:55,y:225},state='ready',invulnerable=0,time=0,last=0,audio=null,sound=false;
const themes=[
{bg:'#c5d7a6',grid:'#b4c796',wall:'#64816b',edge:'#3e6355',flower:'#e5eed0',name:'THE MEADOW'},
{bg:'#e3c99c',grid:'#d6b98b',wall:'#a68058',edge:'#775d43',flower:'#efdfb8',name:'THE DUNES'},
{bg:'#aab8c8',grid:'#9eacbd',wall:'#647489',edge:'#414f69',flower:'#cdd6df',name:'TWILIGHT GARDEN'}
];
const coinPositions=[
[[150,80],[310,70],[480,80],[660,75],[825,80],[150,370],[320,365],[490,375],[675,365],[830,365]],
[[145,75],[310,75],[485,75],[660,75],[825,75],[145,375],[310,375],[485,375],[660,375],[825,375],[440,225],[850,225]],
[[140,60],[315,60],[480,60],[650,60],[840,60],[140,390],[315,390],[480,390],[650,390],[840,390],[250,225],[480,225],[710,225],[890,225]]
];
function tone(freq,duration=.1,type='sine',volume=.06){
if(!sound||!audio)return;
const o=audio.createOscillator(),g=audio.createGain();o.type=type;o.frequency.setValueAtTime(freq,audio.currentTime);
g.gain.setValueAtTime(volume,audio.currentTime);g.gain.exponentialRampToValueAtTime(.001,audio.currentTime+duration);
o.connect(g);g.connect(audio.destination);o.start();o.stop(audio.currentTime+duration);
}
function initLevel(){
player={x:55,y:225};lives=3;score=baseScore;invulnerable=1.5;
coins=coinPositions[level].map(([x,y])=>({x,y,taken:false}));
walls=level===0?[{x:215,y:125,w:95,h:65},{x:430,y:260,w:95,h:65},{x:640,y:125,w:95,h:65}]:
level===1?[{x:210,y:120,w:65,h:175},{x:370,y:115,w:130,h:50},{x:550,y:285,w:130,h:50},{x:740,y:125,w:65,h:175}]:
[{x:185,y:110,w:140,h:55},{x:185,y:285,w:140,h:55},{x:420,y:115,w:115,h:55},{x:420,y:285,w:115,h:55},{x:650,y:110,w:140,h:55},{x:650,y:285,w:140,h:55}];
enemies=Array.from({length:level+2},(_,i)=>({x:350+i*190,y:220,r:15,phase:i*2.2}));
hud();$('status').textContent=themes[level].name+' — COLLECT EVERY COIN';
document.querySelectorAll('.level-item').forEach((el,i)=>el.classList.toggle('active',i===level));
}
function hud(){
$('level').innerHTML=`0${level+1} <small>/ 03</small>`;
$('score').textContent=String(score).padStart(4,'0');
$('lives').textContent='♥'.repeat(lives)+'♡'.repeat(3-lives);
$('lives').setAttribute('aria-label',lives+' lives');
$('collection').textContent=`COINS ${String(coins.filter(c=>c.taken).length).padStart(2,'0')} / ${coins.length}`;
}
function show(tag,title,text,button){
$('overlayTag').textContent=tag;$('overlayTitle').textContent=title;$('overlayText').textContent=text;$('start').textContent=button;$('overlay').hidden=false;
}
function togglePause(){
if(state==='playing'){state='paused';keys.clear();show('Take a breather','Gold can wait.','Your adventure is right where you left it.','Keep exploring ↗');$('pause').textContent='▶';}
else if(state==='paused'){state='playing';$('overlay').hidden=true;$('pause').textContent='Ⅱ';}
}
$('start').onclick=()=>{
if(audio)audio.resume();
if(state==='paused'){togglePause();return;}
if(state==='won'){level=0;baseScore=0;initLevel();}
state='playing';$('overlay').hidden=true;tone(440);setTimeout(()=>tone(660),90);
};
$('pause').onclick=togglePause;
$('sound').onclick=()=>{
sound=!sound;if(sound){audio=audio||new(window.AudioContext||window.webkitAudioContext)();audio.resume();tone(660);}
$('sound').textContent=sound?'Sound on':'Sound off';$('sound').setAttribute('aria-pressed',sound);
};
document.addEventListener('keydown',e=>{
if(['ArrowUp','ArrowDown','ArrowLeft','ArrowRight','w','a','s','d','W','A','S','D',' '].includes(e.key)&&!['BUTTON','INPUT'].includes(document.activeElement.tagName))e.preventDefault();
keys.add(e.key.toLowerCase());
if(e.key.toLowerCase()==='p'&&!e.repeat)togglePause();
});
document.addEventListener('keyup',e=>keys.delete(e.key.toLowerCase()));
window.addEventListener('blur',()=>{keys.clear();if(state==='playing')togglePause();});
document.querySelectorAll('[data-dir]').forEach(b=>{
b.addEventListener('pointerdown',e=>{e.preventDefault();b.setPointerCapture(e.pointerId);keys.add(b.dataset.dir.toLowerCase());});
['pointerup','pointercancel','lostpointercapture'].forEach(type=>b.addEventListener(type,()=>keys.delete(b.dataset.dir.toLowerCase())));
});
function blocked(x,y){
return x<18||x>W-18||y<18||y>H-18||walls.some(w=>x+13>w.x&&x-13<w.x+w.w&&y+13>w.y&&y-13<w.y+w.h);
}
function update(dt){
invulnerable=Math.max(0,invulnerable-dt);
let dx=(keys.has('arrowright')||keys.has('d')?1:0)-(keys.has('arrowleft')||keys.has('a')?1:0);
let dy=(keys.has('arrowdown')||keys.has('s')?1:0)-(keys.has('arrowup')||keys.has('w')?1:0);
let norm=Math.hypot(dx,dy)||1,speed=190;
let x=player.x+dx/norm*speed*dt,y=player.y+dy/norm*speed*dt;
if(!blocked(x,player.y))player.x=x;if(!blocked(player.x,y))player.y=y;
enemies.forEach((e,i)=>{
e.x=340+i*190+Math.sin(time*(.8+level*.25)+e.phase)*65;
e.y=225+Math.sin(time*(1.1+level*.2)+e.phase)*130;
if(invulnerable<=0&&Math.hypot(player.x-e.x,player.y-e.y)<27){
lives--;tone(130,.25,'sawtooth',.035);invulnerable=2;hud();
if(lives<=0){initLevel();$('status').textContent='FRESH START — THIS LEVEL HAS RESTARTED';}
}
});
coins.forEach(c=>{
if(!c.taken&&Math.hypot(player.x-c.x,player.y-c.y)<25){c.taken=true;score+=100;tone(760+coins.filter(a=>a.taken).length*35,.13,'triangle');hud();}
});
if(coins.every(c=>c.taken)){
if(level<2){baseScore=score;level++;initLevel();tone(1040,.3);}
else{state='won';show('All three worlds explored','Pure gold. Nicely done.',`You collected all 36 coins and earned ${score.toLocaleString()} points. Another expedition?`,'Play again ↗');$('status').textContent='EXPEDITION COMPLETE';tone(1200,.4);}
}
}
function rounded(x,y,w,h,r,color){ctx.fillStyle=color;ctx.beginPath();ctx.roundRect(x,y,w,h,r);ctx.fill();}
function draw(){
const t=themes[level];ctx.fillStyle=t.bg;ctx.fillRect(0,0,W,H);
ctx.strokeStyle=t.grid;ctx.lineWidth=1;
for(let x=0;x<W;x+=40){ctx.beginPath();ctx.moveTo(x,0);ctx.lineTo(x,H);ctx.stroke();}
for(let y=0;y<H;y+=40){ctx.beginPath();ctx.moveTo(0,y);ctx.lineTo(W,y);ctx.stroke();}
for(let i=0;i<48;i++){
let x=(i*137+25)%W,y=(i*83+17)%H;ctx.fillStyle=t.flower;
ctx.fillRect(x,y,3,8);ctx.fillRect(x-3,y+3,9,2);
}
ctx.strokeStyle=t.edge+'40';ctx.lineWidth=3;ctx.strokeRect(10,10,W-20,H-20);
walls.forEach(w=>{
rounded(w.x+4,w.y+6,w.w,w.h,6,t.edge+'60');
rounded(w.x,w.y,w.w,w.h,6,t.edge);
rounded(w.x+3,w.y+3,w.w-6,w.h-9,4,t.wall);
ctx.fillStyle='#ffffff18';ctx.fillRect(w.x+9,w.y+8,w.w-18,3);
for(let i=20;i<w.w;i+=28){ctx.fillStyle=t.edge+'55';ctx.fillRect(w.x+i,w.y+20,3,12);}
});
coins.forEach((c,i)=>{
if(c.taken)return;let bob=Math.sin(time*3+i)*3;
ctx.fillStyle='#183e3420';ctx.beginPath();ctx.ellipse(c.x,c.y+13,11,4,0,0,Math.PI*2);ctx.fill();
ctx.fillStyle='#926326';ctx.beginPath();ctx.arc(c.x,c.y+bob,11,0,Math.PI*2);ctx.fill();
ctx.fillStyle='#f4c94e';ctx.beginPath();ctx.arc(c.x,c.y+bob-2,10,0,Math.PI*2);ctx.fill();
ctx.strokeStyle='#fff0a4';ctx.lineWidth=2;ctx.beginPath();ctx.arc(c.x,c.y+bob-2,6,0,Math.PI*2);ctx.stroke();
ctx.fillStyle='#a57625';ctx.fillRect(c.x-1,c.y+bob-6,2,8);
});
enemies.forEach(e=>{
ctx.fillStyle='#183e3422';ctx.beginPath();ctx.ellipse(e.x,e.y+17,18,5,0,0,Math.PI*2);ctx.fill();
ctx.save();ctx.translate(e.x,e.y);ctx.rotate(time*.5);
ctx.fillStyle='#a75043';ctx.beginPath();
for(let j=0;j<16;j++){let a=j*Math.PI/8,r=j%2?12:20;ctx.lineTo(Math.cos(a)*r,Math.sin(a)*r);}ctx.closePath();ctx.fill();ctx.restore();
rounded(e.x-10,e.y-10,20,20,7,'#cb7655');
ctx.fillStyle='#3a3830';ctx.fillRect(e.x-6,e.y-3,3,4);ctx.fillRect(e.x+3,e.y-3,3,4);
});
if(invulnerable>0&&Math.floor(time*12)%2===0&&state==='playing')return;
let p=player;
ctx.fillStyle='#183e3430';ctx.beginPath();ctx.ellipse(p.x,p.y+17,15,5,0,0,Math.PI*2);ctx.fill();
rounded(p.x-11,p.y-4,22,23,5,'#274f42');
ctx.fillStyle='#d7e8ad';ctx.fillRect(p.x-7,p.y+5,14,7);
rounded(p.x-12,p.y-18,24,22,7,'#f3e4b9');
rounded(p.x-15,p.y-23,30,10,4,'#294e40');
ctx.fillStyle='#bce05e';ctx.fillRect(p.x-10,p.y-21,20,3);
ctx.fillStyle='#234539';ctx.fillRect(p.x-6,p.y-9,3,4);ctx.fillRect(p.x+4,p.y-9,3,4);
}
function loop(now){
let dt=Math.min((now-last)/1000,.035);last=now;
if(state==='playing'){time+=dt;update(dt);}else if(state==='ready')time+=dt;
draw();requestAnimationFrame(loop);
}
initLevel();requestAnimationFrame(loop);
})();
</script>
</body>
</html>
