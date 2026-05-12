# My-Website
This is my first wesite
Auther - Fazil
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>PixelRun Adventures</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

  *, *::before, *::after {
    margin: 0; padding: 0; box-sizing: border-box;
    image-rendering: pixelated;
    -webkit-tap-highlight-color: transparent;
    -webkit-touch-callout: none;
    user-select: none;
  }

  html, body {
    width: 100%; height: 100%;
    overflow: hidden;
    touch-action: none;
    background: #0a0a1a;
    font-family: 'Press Start 2P', monospace;
  }

  body {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: radial-gradient(ellipse at center, #1a0035 0%, #0a0a1a 70%);
  }

  #gameWrapper {
    position: relative;
    border: 3px solid #ffd700;
    box-shadow: 0 0 30px #ffd70055, 0 0 60px #ff6b0033;
    display: flex;
    flex-direction: column;
    flex-shrink: 0;
  }

  /* ── HUD ── */
  #hud {
    background: linear-gradient(180deg, #1a0030 0%, #0d001a 100%);
    border-bottom: 2px solid #ffd700;
    padding: 5px 10px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 8px;
    flex-wrap: nowrap;
    width: 100%;
  }

  .hud-group { display: flex; align-items: center; gap: 6px; flex-shrink: 0; }

  .hud-item {
    display: flex;
    align-items: center;
    gap: 3px;
    color: #fff;
    font-size: clamp(5px, 1.8vw, 9px);
    text-shadow: 1px 1px #000;
    white-space: nowrap;
  }
  .hud-item .val { color: #ffd700; }

  #shopBtn {
    background: linear-gradient(180deg, #ffd700, #ff8c00);
    color: #1a0030;
    border: 2px solid #fff;
    padding: 4px 8px;
    font-family: 'Press Start 2P', monospace;
    font-size: clamp(5px, 1.5vw, 8px);
    cursor: pointer;
    box-shadow: 0 3px 0 #7a4000;
    transition: transform 0.1s;
    white-space: nowrap;
    flex-shrink: 0;
  }
  #shopBtn:active { transform: translateY(2px); box-shadow: 0 1px 0 #7a4000; }

  /* ── CANVAS ── */
  #gameCanvas {
    display: block;
    background: #000;
    flex-shrink: 0;
  }

  /* ── TOUCH CONTROLS ── */
  #touchControls {
    background: linear-gradient(180deg, #0d001a, #0a0015);
    border-top: 2px solid #ffd700;
    display: none;
    align-items: center;
    justify-content: space-between;
    padding: 10px 18px 14px;
    gap: 12px;
    width: 100%;
    flex-shrink: 0;
  }

  /* D-PAD */
  .dpad {
    display: flex;
    align-items: center;
    gap: 5px;
  }

  .dpad-btn {
    background: linear-gradient(180deg, #2a2a5a, #161630);
    border: 2.5px solid #5555cc;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    box-shadow: 0 4px 0 #080820, inset 0 1px 0 #6666dd44;
    transition: background 0.06s, transform 0.06s, box-shadow 0.06s;
    flex-shrink: 0;
  }
  .dpad-btn:active, .dpad-btn.pressed {
    background: linear-gradient(180deg, #5555cc, #3333aa);
    transform: translateY(3px);
    box-shadow: 0 1px 0 #080820;
  }

  #btnLeft, #btnRight {
    width: 62px;
    height: 62px;
    font-size: 24px;
  }

  /* ACTION BUTTONS */
  .action-btns {
    display: flex;
    align-items: center;
    gap: 14px;
  }

  .action-btn {
    border-radius: 50%;
    border: 3px solid #fff3;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: transform 0.06s, box-shadow 0.06s;
    flex-shrink: 0;
    font-size: 22px;
  }
  .action-btn:active, .action-btn.pressed {
    transform: scale(0.9) translateY(3px);
  }

  #btnJump {
    width: 72px; height: 72px;
    background: linear-gradient(180deg, #ffd700, #ff8c00);
    color: #1a0030;
    box-shadow: 0 5px 0 #7a4000;
    font-size: 28px;
    font-weight: bold;
  }
  #btnJump:active, #btnJump.pressed {
    box-shadow: 0 2px 0 #7a4000;
  }

  #btnPause {
    width: 50px; height: 50px;
    background: linear-gradient(180deg, #4444cc, #2222aa);
    color: #fff;
    box-shadow: 0 4px 0 #111166;
    font-size: 18px;
  }
  #btnPause:active {
    box-shadow: 0 1px 0 #111166;
  }

  /* ── PC CONTROLS BAR ── */
  #pcControls {
    background: #0d001a;
    border-top: 2px solid #ffd700;
    padding: 5px 14px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    flex-wrap: wrap;
    width: 100%;
    flex-shrink: 0;
  }
  .ctrl-label { color: #888; font-size: 6px; }
  .key-badge {
    background: #222;
    border: 2px solid #555;
    border-bottom: 3px solid #333;
    color: #ffd700;
    font-size: 6px;
    padding: 2px 5px;
    border-radius: 2px;
  }

  /* ── OVERLAYS ── */
  .overlay {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 30;
    background: #00000055;
    backdrop-filter: blur(3px);
  }

  .overlay-box {
    background: linear-gradient(180deg, #1a0030f0, #0d001af0);
    border: 3px solid #ffd700;
    padding: clamp(14px, 4vw, 28px) clamp(16px, 5vw, 36px);
    text-align: center;
    box-shadow: 0 0 30px #ffd70066;
    width: clamp(240px, 88vw, 420px);
    max-height: 92%;
    overflow-y: auto;
    -webkit-overflow-scrolling: touch;
  }

  .overlay-box h2 {
    color: #ffd700;
    font-size: clamp(9px, 3vw, 14px);
    margin-bottom: 12px;
    text-shadow: 2px 2px #000;
  }

  .overlay-box p {
    color: #ccc;
    font-size: clamp(6px, 1.8vw, 8px);
    margin-bottom: 10px;
    line-height: 2;
  }

  .pixel-btn {
    background: linear-gradient(180deg, #ffd700, #ff8c00);
    color: #1a0030;
    border: 3px solid #fff;
    padding: clamp(7px, 2vw, 11px) clamp(12px, 3vw, 20px);
    font-family: 'Press Start 2P', monospace;
    font-size: clamp(7px, 2vw, 9px);
    cursor: pointer;
    margin: 5px;
    box-shadow: 0 4px 0 #7a4000;
    transition: transform 0.1s;
    display: inline-block;
  }
  .pixel-btn:active { transform: translateY(2px); box-shadow: 0 1px 0 #7a4000; }
  .pixel-btn.secondary {
    background: linear-gradient(180deg, #4444cc, #2222aa);
    color: #fff;
    box-shadow: 0 4px 0 #111166;
  }
  .pixel-btn.secondary:active { box-shadow: 0 1px 0 #111166; }
  .pixel-btn.danger {
    background: linear-gradient(180deg, #cc4444, #aa2222);
    color: #fff;
    box-shadow: 0 4px 0 #661111;
  }

  /* ── SHOP ── */
  #shopOverlay { display: none; }
  .map-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    margin: 12px 0;
  }
  .map-card {
    border: 3px solid #444;
    padding: 8px 6px;
    cursor: pointer;
    transition: border-color 0.15s;
    position: relative;
    text-align: center;
    background: #0d0020;
  }
  .map-card.owned  { border-color: #00cc44; }
  .map-card.active { border-color: #ffd700; box-shadow: 0 0 10px #ffd70066; }
  .map-card:active { opacity: 0.85; }
  .map-card canvas { display: block; margin: 0 auto 5px; width: 100%; height: auto; }
  .map-card .map-name  { color: #ffd700; font-size: clamp(5px, 1.5vw, 7px); margin-bottom: 3px; }
  .map-card .map-price { color: #aaa;    font-size: clamp(5px, 1.3vw, 6px); }
  .map-card .map-price span { color: #ffd700; }
  .map-badge {
    position: absolute; top: 3px; right: 3px;
    font-size: 5px; padding: 2px 3px;
    background: #00cc44; color: #000;
  }

  #gameOverOverlay, #winOverlay { display: none; }
</style>
</head>
<body>

<div id="gameWrapper">

  <!-- HUD -->
  <div id="hud">
    <div class="hud-group">
      <div class="hud-item">🗺&nbsp;<span id="hudMap">GRASS WORLD</span></div>
    </div>
    <div class="hud-group">
      <div class="hud-item">⭐&nbsp;<span class="val" id="hudScore">000000</span></div>
      <div class="hud-item">🪙&nbsp;<span class="val" id="hudCoins">0</span></div>
      <div class="hud-item">❤️&nbsp;<span class="val" id="hudLives">3</span></div>
      <div class="hud-item">⏱&nbsp;<span class="val" id="hudTime">120</span></div>
    </div>
    <button id="shopBtn" onclick="openShop()">🛒 SHOP</button>
  </div>

  <!-- CANVAS -->
  <canvas id="gameCanvas"></canvas>

  <!-- TOUCH CONTROLS (shown only on touch) -->
  <div id="touchControls">
    <div class="dpad">
      <button class="dpad-btn" id="btnLeft"
        ontouchstart="e=>{e.preventDefault();touchDown('left')}"
        ontouchend="e=>{e.preventDefault();touchUp('left')}">◀</button>
      <button class="dpad-btn" id="btnRight"
        ontouchstart="e=>{e.preventDefault();touchDown('right')}"
        ontouchend="e=>{e.preventDefault();touchUp('right')}">▶</button>
    </div>
    <div class="action-btns">
      <button class="action-btn" id="btnPause" onclick="togglePause()">⏸</button>
      <button class="action-btn" id="btnJump"
        ontouchstart="e=>{e.preventDefault();touchDown('jump')}"
        ontouchend="e=>{e.preventDefault();touchUp('jump')}">🅰</button>
    </div>
  </div>

  <!-- PC CONTROLS -->
  <div id="pcControls">
    <span class="ctrl-label">MOVE</span><span class="key-badge">← →</span>&nbsp;
    <span class="ctrl-label">JUMP</span><span class="key-badge">SPACE / ↑</span>&nbsp;
    <span class="ctrl-label">PAUSE</span><span class="key-badge">P</span>
  </div>

  <!-- OVERLAYS -->
  <div class="overlay" id="startOverlay">
    <div class="overlay-box">
      <h2>⭐ PIXELRUN ⭐</h2>
      <p>Collect coins · Stomp enemies<br>Reach the flag · Buy new worlds!</p>
      <p style="color:#ffd700">← → move &nbsp;·&nbsp; SPACE / ↑ jump<br>On mobile: use on-screen buttons!</p>
      <button class="pixel-btn" onclick="startGame()">▶ START GAME</button>
    </div>
  </div>

  <div class="overlay" id="pauseOverlay" style="display:none">
    <div class="overlay-box">
      <h2>⏸ PAUSED</h2>
      <button class="pixel-btn" onclick="resumeGame()">▶ RESUME</button><br>
      <button class="pixel-btn secondary" onclick="openShop()">🛒 MAP SHOP</button>
    </div>
  </div>

  <div class="overlay" id="gameOverOverlay">
    <div class="overlay-box">
      <h2 style="color:#ff4444">💀 GAME OVER</h2>
      <p id="goMsg">Better luck next time!</p>
      <p>COINS BANKED: <span id="goCoins" style="color:#ffd700">0</span> 🪙</p>
      <button class="pixel-btn" onclick="startGame()">🔄 TRY AGAIN</button>
      <button class="pixel-btn secondary" onclick="openShop()">🛒 SHOP</button>
    </div>
  </div>

  <div class="overlay" id="winOverlay">
    <div class="overlay-box">
      <h2>🎉 LEVEL CLEAR!</h2>
      <p id="winMsg">Amazing!</p>
      <p>TIME BONUS: <span id="winBonus" style="color:#ffd700">0</span> 🪙</p>
      <button class="pixel-btn" onclick="nextLevel()">▶ NEXT LEVEL</button>
      <button class="pixel-btn secondary" onclick="openShop()">🛒 SHOP</button>
    </div>
  </div>

  <div class="overlay" id="shopOverlay">
    <div class="overlay-box" style="max-width:460px">
      <h2>🛒 MAP SHOP</h2>
      <p>YOUR COINS: <span id="shopCoins" style="color:#ffd700">0</span> 🪙</p>
      <div class="map-grid" id="mapGrid"></div>
      <button class="pixel-btn danger" onclick="closeShop()">✕ CLOSE</button>
    </div>
  </div>

</div><!-- end #gameWrapper -->

<script>
// ═══════════════════════════════════════════════════════════════════
//  PIXELRUN ADVENTURES — PC + Mobile Responsive
// ═══════════════════════════════════════════════════════════════════

// ── CANVAS / SCALING ────────────────────────────────────────────────
const canvas  = document.getElementById('gameCanvas');
const ctx     = canvas.getContext('2d');
ctx.imageSmoothingEnabled = false;

// Fixed logical resolution
const LW = 800, LH = 400;

// These are always the logical dimensions for game maths
const W = LW, H = LH;

const gameWrapper = document.getElementById('gameWrapper');
const hudEl       = document.getElementById('hud');
const touchCtrl   = document.getElementById('touchControls');
const pcCtrl      = document.getElementById('pcControls');

let isTouch = false;

function resizeGame() {
  isTouch = ('ontouchstart' in window) || navigator.maxTouchPoints > 0;

  // Toggle UI
  if (isTouch) {
    touchCtrl.style.display = 'flex';
    pcCtrl.style.display    = 'none';
  } else {
    touchCtrl.style.display = 'none';
    pcCtrl.style.display    = 'flex';
  }

  // Must layout first to get real heights
  requestAnimationFrame(() => {
    const hudH    = hudEl.offsetHeight      || 34;
    const bottomH = isTouch
      ? (touchCtrl.offsetHeight || 110)
      : (pcCtrl.offsetHeight    || 26);
    const border  = 6; // 3px border top+bottom

    const availW = window.innerWidth  - border;
    const availH = window.innerHeight - hudH - bottomH - border;

    const scaleW = availW / LW;
    const scaleH = availH / LH;
    const scale  = Math.min(scaleW, scaleH, 2);

    const cw = Math.floor(LW * scale);
    const ch = Math.floor(LH * scale);

    canvas.width  = LW;
    canvas.height = LH;
    canvas.style.width  = cw + 'px';
    canvas.style.height = ch + 'px';

    gameWrapper.style.width = cw + 'px';
  });
}

window.addEventListener('resize', resizeGame);
window.addEventListener('orientationchange', () => setTimeout(resizeGame, 250));
resizeGame();

// ── INPUT ────────────────────────────────────────────────────────────
const keys  = {};
const touch = { left:false, right:false, jump:false };
let prevJumpState = false;

document.addEventListener('keydown', e => {
  keys[e.code] = true;
  if (e.code === 'KeyP') togglePause();
  if (['Space','ArrowUp','ArrowLeft','ArrowRight'].includes(e.code)) e.preventDefault();
});
document.addEventListener('keyup', e => { keys[e.code] = false; });

function touchDown(btn) {
  touch[btn] = true;
  const ids = { left:'btnLeft', right:'btnRight', jump:'btnJump' };
  document.getElementById(ids[btn])?.classList.add('pressed');
}
function touchUp(btn) {
  touch[btn] = false;
  const ids = { left:'btnLeft', right:'btnRight', jump:'btnJump' };
  document.getElementById(ids[btn])?.classList.remove('pressed');
}

// Wire up touch buttons properly (avoiding inline handler issues)
function wireTouchBtn(id, btn) {
  const el = document.getElementById(id);
  if (!el) return;
  el.addEventListener('touchstart', e => { e.preventDefault(); touchDown(btn); }, { passive: false });
  el.addEventListener('touchend',   e => { e.preventDefault(); touchUp(btn);   }, { passive: false });
  el.addEventListener('touchcancel',e => { e.preventDefault(); touchUp(btn);   }, { passive: false });
}
wireTouchBtn('btnLeft',  'left');
wireTouchBtn('btnRight', 'right');
wireTouchBtn('btnJump',  'jump');

function isLeft()  { return keys['ArrowLeft']  || keys['KeyA'] || touch.left; }
function isRight() { return keys['ArrowRight'] || keys['KeyD'] || touch.right; }
function isJump()  { return keys['Space'] || keys['ArrowUp'] || keys['KeyW'] || touch.jump; }

// Block native scroll on canvas touch
canvas.addEventListener('touchstart', e => e.preventDefault(), { passive: false });
canvas.addEventListener('touchmove',  e => e.preventDefault(), { passive: false });

// ── MAP DEFINITIONS ──────────────────────────────────────────────────
const MAPS = [
  { id:0, name:'GRASS WORLD', price:0,
    sky:['#5bb8f5','#90d8f5'], ground:'#4a7c3f', groundTop:'#5da832', groundBrick:'#6b4226',
    cloudColor:'#ffffffee', mountainColor:'#3a6b30',
    enemyColor:'#cc3333', enemyTop:'#ff5555', platformColor:'#6b4226', platformTop:'#5da832' },
  { id:1, name:'DESERT DUNES', price:80,
    sky:['#f5c842','#f5a623'], ground:'#c8913a', groundTop:'#e8b048', groundBrick:'#a0722a',
    cloudColor:'#fff8cccc', mountainColor:'#b07828',
    enemyColor:'#884400', enemyTop:'#cc6600', platformColor:'#a0722a', platformTop:'#e8b048' },
  { id:2, name:'ICE KINGDOM', price:150,
    sky:['#b8e4ff','#dff4ff'], ground:'#7ec8e3', groundTop:'#b0e0f0', groundBrick:'#5599bb',
    cloudColor:'#ffffffcc', mountainColor:'#99cce0',
    enemyColor:'#2244aa', enemyTop:'#4466dd', platformColor:'#5599bb', platformTop:'#b0e0f0' },
  { id:3, name:'LAVA CASTLE', price:250,
    sky:['#220000','#440011'], ground:'#553311', groundTop:'#ff6600', groundBrick:'#442200',
    cloudColor:'#ff440055', mountainColor:'#3a1100',
    enemyColor:'#880000', enemyTop:'#ff2200', platformColor:'#442200', platformTop:'#ff6600' },
];

// ── GAME STATE ────────────────────────────────────────────────────────
let state = {
  scene:'start', score:0, coins:0, lives:3, time:120,
  timeTimer:null, level:0, activeMap:0, ownedMaps:[0], camera:{ x:0 }
};

// ── LEVEL GENERATOR ──────────────────────────────────────────────────
const TILE = 32;
const GRAVITY    = 0.55;
const JUMP_FORCE = -13.5;
const MOVE_SPEED = 4.2;

function genLevel(mapId) {
  const map  = MAPS[mapId];
  const cols = 60;
  const rows = Math.floor(H / TILE);
  let tiles  = [];

  for (let c = 0; c < cols; c++)
    tiles.push({ x:c*TILE, y:H-TILE*2, w:TILE, h:TILE*2, type:'ground' });

  const plats = [
    {col:4,row:rows-5,len:3},{col:9,row:rows-6,len:2},{col:14,row:rows-5,len:4},
    {col:19,row:rows-7,len:2},{col:24,row:rows-5,len:3},{col:30,row:rows-6,len:3},
    {col:35,row:rows-8,len:2},{col:40,row:rows-5,len:4},{col:46,row:rows-6,len:3},
    {col:52,row:rows-7,len:2},
  ];
  plats.forEach(p => {
    for (let i = 0; i < p.len; i++)
      tiles.push({ x:(p.col+i)*TILE, y:p.row*TILE, w:TILE, h:TILE, type:'platform' });
  });

  let coins = [];
  [3,5,7,8,11,13,15,20,22,25,27,32,34,37,38,41,42,43,47,48,53].forEach(c =>
    coins.push({ x:c*TILE+TILE/2, y:H-TILE*3, collected:false }));
  plats.forEach(p => {
    for (let i = 0; i < p.len; i++)
      coins.push({ x:(p.col+i)*TILE+TILE/2, y:p.row*TILE-TILE, collected:false });
  });

 let enemies = [
    { x: 6 * TILE,  y: H - TILE * 2 - 30, vx: -1.2, vy: 0, alive: true, onGround: false, type: 'goomba', w: 28, h: 28 },
    { x: 12 * TILE, y: H - TILE * 2 - 30, vx: 1.5, vy: 0, alive: true, onGround: false, type: 'goomba', w: 28, h: 28 },
    { x: 22 * TILE, y: H - TILE * 2 - 30, vx: -1.3, vy: 0, alive: true, onGround: false, type: 'goomba', w: 28, h: 28 },
    { x: 31 * TILE, y: H - TILE * 2 - 30, vx: 1.6, vy: 0, alive: true, onGround: false, type: 'goomba', w: 28, h: 28 },
    { x: 38 * TILE, y: H - TILE * 2 - 30, vx: -1.4, vy: 0, alive: true, onGround: false, type: 'spiny', w: 28, h: 28 },
    { x: 45 * TILE, y: H - TILE * 2 - 30, vx: 1.8, vy: 0, alive: true, onGround: false, type: 'spiny', w: 28, h: 28 },
    { x: 50 * TILE, y: H - TILE * 2 - 30, vx: -1.5, vy: 0, alive: true, onGround: false, type: 'goomba', w: 28, h: 28 },
  ];
  return { tiles, coins, enemies, cols, map };
}

// ── PLAYER ────────────────────────────────────────────────────────────
let player = {};
function resetPlayer() {
  player = {
    x:64, y:H-TILE*2-48, w:28, h:36,
    vx:0, vy:0, onGround:false,
    dir:1, frame:0, frameTimer:0,
    dead:false, invincible:0,
  };
}

let level      = {};
let particles  = [];
let floatTexts = [];
let coinAnimTimer = 0;
const COIN_FRAMES = [14,10,6,10];

// ── PHYSICS ────────────────────────────────────────────────────────────
function rectOverlap(a, b) {
  return a.x < b.x+b.w && a.x+a.w > b.x && a.y < b.y+b.h && a.y+a.h > b.y;
}
function resolvePlatformCollisions(obj) {
  obj.onGround = false;
  for (const tile of level.tiles) {
    if (!rectOverlap(obj, tile)) continue;
    const ox = Math.min(obj.x+obj.w-tile.x, tile.x+tile.w-obj.x);
    const oy = Math.min(obj.y+obj.h-tile.y, tile.y+tile.h-obj.y);
    if (oy < ox) {
      if (obj.y+obj.h/2 < tile.y+tile.h/2) { obj.y=tile.y-obj.h; obj.vy=0; obj.onGround=true; }
      else { obj.y=tile.y+tile.h; obj.vy=Math.abs(obj.vy)*0.3; }
    } else {
      if (obj.x+obj.w/2 < tile.x+tile.w/2) { obj.x=tile.x-obj.w; obj.vx*=-1; }
      else { obj.x=tile.x+tile.w; obj.vx*=-1; }
    }
  }
}

// ── FX ─────────────────────────────────────────────────────────────────
function spawnParticles(x, y, color, n=8) {
  for (let i=0;i<n;i++) {
    const a=(Math.PI*2/n)*i+Math.random()*0.3, sp=2+Math.random()*3;
    particles.push({x,y,vx:Math.cos(a)*sp,vy:Math.sin(a)*sp-2,life:30,color});
  }
}
function spawnFloatText(x,y,text,color='#ffd700') {
  floatTexts.push({x,y,text,color,life:60,vy:-1.5});
}

// ── KILL PLAYER ────────────────────────────────────────────────────────
function killPlayer(reason='') {
  if (player.invincible>0) return;
  state.lives--;
  spawnParticles(player.x+player.w/2,player.y+player.h/2,'#ff4444',16);
  if (state.lives<=0) {
    clearInterval(state.timeTimer);
    state.scene='gameover';
    setTimeout(()=>{
      document.getElementById('goMsg').textContent=reason||'BETTER LUCK NEXT TIME!';
      document.getElementById('goCoins').textContent=state.coins;
      document.getElementById('gameOverOverlay').style.display='flex';
    },800);
  } else { resetPlayer(); player.invincible=120; }
  updateHUD();
}

// ── UPDATE ─────────────────────────────────────────────────────────────
function update() {
  if (state.scene!=='playing') return;
  coinAnimTimer++;

  const jumpNow = isJump();

  if (isLeft())       { player.vx=-MOVE_SPEED; player.dir=-1; }
  else if (isRight()) { player.vx= MOVE_SPEED; player.dir= 1; }
  else                { player.vx*=0.75; }

  // Edge-triggered jump
  if (jumpNow && !prevJumpState && player.onGround) {
    player.vy=JUMP_FORCE;
    player.onGround=false;
  }
  prevJumpState = jumpNow;

  player.vy += GRAVITY;
  player.x  += player.vx;
  player.y  += player.vy;

  if (player.x<0) player.x=0;
  if (player.x>level.cols*TILE-player.w) player.x=level.cols*TILE-player.w;

  resolvePlatformCollisions(player);
  if (player.y>H+100) killPlayer('FELL INTO THE VOID!');

  state.camera.x = Math.max(0, Math.min(player.x-W/2.5, level.cols*TILE-W));

  if (Math.abs(player.vx)>0.5 && player.onGround) {
    player.frameTimer++;
    if (player.frameTimer>8) { player.frame=(player.frame+1)%4; player.frameTimer=0; }
  } else player.frame=0;

  if (player.invincible>0) player.invincible--;

  // Enemies
  for (const e of level.enemies) {
    if (!e.alive) continue;
    e.vy+=GRAVITY; e.x+=e.vx; e.y+=e.vy;
    resolvePlatformCollisions(e);
    if (e.x<0||e.x+28>level.cols*TILE) e.vx*=-1;
    if (e.onGround) {
      const fx=e.vx>0?e.x+30:e.x-2;
      const below=level.tiles.find(t=>fx>=t.x&&fx<t.x+t.w&&Math.abs(t.y-(e.y+28))<4);
      if (!below) e.vx*=-1;
    }
    if (player.invincible===0 && rectOverlap(player,{x:e.x,y:e.y,w:28,h:28})) {
      if (player.vy>0 && player.y+player.h<e.y+16) {
        e.alive=false; player.vy=-8; state.score+=200;
        spawnParticles(e.x+14,e.y,'#ff5555',10);
        spawnFloatText(e.x,e.y-10,'+200');
      } else { killPlayer('HIT BY ENEMY!'); }
      updateHUD();
    }
  }

  // Coins
  for (const c of level.coins) {
    if (c.collected) continue;
    if (Math.abs(player.x+player.w/2-c.x)<22 && Math.abs(player.y+player.h/2-c.y)<22) {
      c.collected=true; state.coins++; state.score+=50;
      spawnParticles(c.x,c.y,'#ffd700',6);
      spawnFloatText(c.x,c.y-10,'+50');
      updateHUD();
    }
  }

  // Flag
  const flagX=(level.cols-3)*TILE+TILE/2;
  if (player.x+player.w>flagX-20 && player.x<flagX+20) {
    clearInterval(state.timeTimer);
    state.scene='win';
    const bonus=Math.floor(state.time*10);
    state.score+=bonus; state.coins+=Math.floor(bonus/50);
    document.getElementById('winMsg').textContent='LEVEL '+(state.level+1)+' CLEARED!';
    document.getElementById('winBonus').textContent=bonus;
    document.getElementById('winOverlay').style.display='flex';
    updateHUD();
  }

  for (const p of particles) { p.x+=p.vx; p.y+=p.vy; p.vy+=0.15; p.life--; }
  particles=particles.filter(p=>p.life>0);
  for (const f of floatTexts) { f.y+=f.vy; f.life--; }
  floatTexts=floatTexts.filter(f=>f.life>0);
}

// ── DRAW ────────────────────────────────────────────────────────────────
function drawTile(tile, m) {
  const sx=tile.x-state.camera.x;
  if (sx+tile.w<0||sx>W) return;
  if (tile.type==='ground') {
    ctx.fillStyle=m.groundBrick; ctx.fillRect(sx,tile.y,tile.w,tile.h);
    ctx.fillStyle=m.groundTop;   ctx.fillRect(sx,tile.y,tile.w,8);
    ctx.fillStyle=m.ground;
    ctx.fillRect(sx,tile.y+8,tile.w,3); ctx.fillRect(sx,tile.y+20,tile.w,3);
    const off=(Math.floor(tile.x/TILE)%2)*16;
    ctx.fillRect(sx+off,tile.y+8,3,tile.h-8);
    ctx.fillRect(sx+off+16,tile.y+8,3,tile.h-8);
  } else {
    ctx.fillStyle=m.platformColor; ctx.fillRect(sx,tile.y,tile.w,tile.h);
    ctx.fillStyle=m.platformTop;   ctx.fillRect(sx,tile.y,tile.w,6);
    ctx.fillStyle='#ffffff33';     ctx.fillRect(sx+2,tile.y+2,8,3);
  }
}

function drawCoin(c) {
  if (c.collected) return;
  const sx=c.x-state.camera.x;
  if (sx<-20||sx>W+20) return;
  const cw=COIN_FRAMES[Math.floor(coinAnimTimer/8)%4];
  ctx.fillStyle='#ffd70033';
  ctx.beginPath(); ctx.arc(sx,c.y,14,0,Math.PI*2); ctx.fill();
  ctx.fillStyle='#ffd700';   ctx.fillRect(sx-cw/2,c.y-10,cw,20);
  ctx.fillStyle='#ffffffaa'; ctx.fillRect(sx-cw/2+2,c.y-8,Math.max(2,cw/3),6);
  ctx.fillStyle='#cc9900';   ctx.fillRect(sx-cw/2+1,c.y-2,cw-2,4);
}

function drawEnemy(e, m) {
  if (!e.alive) return;
  const sx=e.x-state.camera.x;
  if (sx+28<0||sx>W) return;
  if (e.type==='goomba') {
    ctx.fillStyle=m.enemyColor; ctx.fillRect(sx+2,e.y+6,24,18);
    ctx.fillStyle=m.enemyTop;   ctx.fillRect(sx,e.y,28,12);
    ctx.fillStyle='#fff';
    ctx.fillRect(sx+4,e.y+3,7,6); ctx.fillRect(sx+17,e.y+3,7,6);
    ctx.fillStyle='#000';
    ctx.fillRect(sx+7,e.y+4,3,4); ctx.fillRect(sx+20,e.y+4,3,4);
    ctx.fillStyle='#222';
    ctx.fillRect(sx+2,e.y+22,10,6); ctx.fillRect(sx+16,e.y+22,10,6);
  } else {
    ctx.fillStyle=m.enemyColor; ctx.fillRect(sx+2,e.y+4,24,22);
    ctx.fillStyle=m.enemyTop;   ctx.fillRect(sx+4,e.y,20,10);
    ctx.fillStyle='#ffcc00';
    for(let i=0;i<4;i++) ctx.fillRect(sx+4+i*6,e.y-5,4,8);
    ctx.fillStyle='#fff';
    ctx.fillRect(sx+5,e.y+6,6,5); ctx.fillRect(sx+17,e.y+6,6,5);
    ctx.fillStyle='#f00';
    ctx.fillRect(sx+7,e.y+7,3,3); ctx.fillRect(sx+19,e.y+7,3,3);
  }
}

function drawPlayer() {
  const sx=player.x-state.camera.x, py=player.y;
  if (player.invincible>0 && Math.floor(player.invincible/4)%2===0) return;
  ctx.save();
  if (player.dir<0) { ctx.translate(sx+player.w,py); ctx.scale(-1,1); ctx.translate(-player.w,0); }
  else ctx.translate(sx,py);
  const PW=player.w, PH=player.h;
  const legOff=player.onGround?Math.sin(player.frame*1.5)*5:0;
  ctx.fillStyle='#00000033'; ctx.fillRect(2,PH-4,PW-4,4);
  ctx.fillStyle='#1a3a8c';
  ctx.fillRect(4+legOff,PH-12,9,12); ctx.fillRect(15-legOff,PH-12,9,12);
  ctx.fillStyle='#8B4513';
  ctx.fillRect(2+legOff,PH-6,12,6);  ctx.fillRect(14-legOff,PH-6,12,6);
  ctx.fillStyle='#1a3a8c'; ctx.fillRect(2,PH-24,PW-4,14);
  ctx.fillStyle='#cc2200'; ctx.fillRect(0,PH-28,PW,10);
  ctx.fillStyle='#1a3a8c';
  ctx.fillRect(8,PH-26,4,4); ctx.fillRect(16,PH-26,4,4);
  ctx.fillStyle='#f5c5a3'; ctx.fillRect(2,PH-36,PW-4,12);
  ctx.fillStyle='#cc2200';
  ctx.fillRect(0,PH-40,PW,8); ctx.fillRect(3,PH-44,PW-6,6);
  ctx.fillStyle='#000'; ctx.fillRect(16,PH-33,4,4);
  ctx.fillStyle='#5a2d00';
  ctx.fillRect(10,PH-27,14,3); ctx.fillRect(8,PH-29,6,2);
  ctx.fillStyle='#cc2200';
  if (!player.onGround) {
    ctx.fillRect(-4,PH-28,6,8); ctx.fillRect(PW-2,PH-28,6,8);
  } else {
    const as=Math.sin(player.frame)*5;
    ctx.fillRect(-4,PH-28+as,6,10); ctx.fillRect(PW-2,PH-28-as,6,10);
  }
  ctx.restore();
}

function drawMountain(x, baseY, w, h) {
  ctx.beginPath(); ctx.moveTo(x,baseY); ctx.lineTo(x+w/2,baseY-h); ctx.lineTo(x+w,baseY); ctx.fill();
  const fc=ctx.fillStyle;
  ctx.fillStyle='#ffffff55';
  ctx.beginPath(); ctx.moveTo(x+w*0.35,baseY-h*0.55); ctx.lineTo(x+w/2,baseY-h); ctx.lineTo(x+w*0.65,baseY-h*0.55); ctx.fill();
  ctx.fillStyle=fc;
}

function drawCloud(x, y, s=1) {
  ctx.beginPath();
  ctx.arc(x,y,22*s,0,Math.PI*2);
  ctx.arc(x+28*s,y-6*s,18*s,0,Math.PI*2);
  ctx.arc(x+52*s,y,20*s,0,Math.PI*2);
  ctx.arc(x+26*s,y+12*s,22*s,0,Math.PI*2);
  ctx.fill();
}

function drawBackground(m) {
  const gr=ctx.createLinearGradient(0,0,0,H);
  gr.addColorStop(0,m.sky[0]); gr.addColorStop(1,m.sky[1]);
  ctx.fillStyle=gr; ctx.fillRect(0,0,W,H);

  const mx=-(state.camera.x*0.3)%W;
  for (let i=-1;i<=2;i++) {
    const ox=i*W+mx;
    ctx.fillStyle=m.mountainColor+'88';
    for(let j=0;j<5;j++) drawMountain(ox+j*200-50,H-TILE*2,120,120);
    ctx.fillStyle=m.mountainColor+'bb';
    for(let j=0;j<4;j++) drawMountain(ox+j*240+80,H-TILE*2,90,100);
  }

  const cx=-(state.camera.x*0.15)%(W*1.5);
  ctx.fillStyle=m.cloudColor;
  [{x:80,y:55,s:1.3},{x:260,y:38,s:1},{x:430,y:60,s:1.5},
   {x:600,y:45,s:1.1},{x:720,y:70,s:0.9},{x:950,y:40,s:1.2}].forEach(cd=>{
    drawCloud(((cd.x+cx)%(W*1.5+200))-100, cd.y, cd.s);
  });
}

function drawFlag() {
  const fx=(level.cols-3)*TILE-state.camera.x;
  if (fx<-40||fx>W+40) return;
  ctx.fillStyle='#aaa'; ctx.fillRect(fx,H-TILE*2-160,8,160);
  const t=Date.now()/500;
  ctx.fillStyle='#00cc44';
  ctx.beginPath();
  ctx.moveTo(fx+8,H-TILE*2-160);
  ctx.lineTo(fx+8+44+Math.sin(t)*6,H-TILE*2-140+Math.sin(t)*3);
  ctx.lineTo(fx+8,H-TILE*2-120);
  ctx.fill();
  ctx.fillStyle='#ffd700'; ctx.fillRect(fx+2,H-TILE*2-168,12,12);
}

function drawParticles() {
  for(const p of particles){
    ctx.globalAlpha=p.life/30; ctx.fillStyle=p.color;
    ctx.fillRect(p.x-3,p.y-3,6,6);
  }
  ctx.globalAlpha=1;
}

function drawFloatTexts() {
  ctx.textAlign='center';
  for(const f of floatTexts){
    ctx.globalAlpha=f.life/60; ctx.fillStyle=f.color;
    ctx.font='8px "Press Start 2P"';
    ctx.fillText(f.text,f.x-state.camera.x,f.y);
  }
  ctx.globalAlpha=1; ctx.textAlign='left';
}

function draw() {
  ctx.clearRect(0,0,W,H);
  const m=level.map||MAPS[0];
  drawBackground(m);
  for(const t of level.tiles) drawTile(t,m);
  drawFlag();
  for(const c of level.coins) drawCoin(c);
  for(const e of level.enemies) drawEnemy(e,m);
  drawPlayer();
  drawParticles();
  drawFloatTexts();
  if(state.scene==='playing'){
    ctx.fillStyle='#00000055'; ctx.fillRect(0,H-20,W,20);
    ctx.fillStyle='#ffffff77'; ctx.font='7px "Press Start 2P"'; ctx.textAlign='center';
    ctx.fillText('LEVEL '+(state.level+1)+'  ·  '+m.name, W/2, H-7);
    ctx.textAlign='left';
  }
}

// ── GAME LOOP ────────────────────────────────────────────────────────────
function loop() { update(); draw(); requestAnimationFrame(loop); }

// ── HUD ──────────────────────────────────────────────────────────────────
function updateHUD() {
  document.getElementById('hudScore').textContent=state.score.toString().padStart(6,'0');
  document.getElementById('hudCoins').textContent=state.coins;
  document.getElementById('hudLives').textContent=state.lives;
  document.getElementById('hudTime').textContent=state.time;
  document.getElementById('hudMap').textContent=MAPS[state.activeMap].name;
  document.getElementById('shopCoins').textContent=state.coins;
}

// ── SHOP ─────────────────────────────────────────────────────────────────
function drawMapPreview(cvs, m) {
  const c=cvs.getContext('2d'); c.imageSmoothingEnabled=false;
  const w=cvs.width, h=cvs.height;
  const g=c.createLinearGradient(0,0,0,h);
  g.addColorStop(0,m.sky[0]); g.addColorStop(1,m.sky[1]);
  c.fillStyle=g; c.fillRect(0,0,w,h);
  c.fillStyle=m.mountainColor+'aa';
  c.beginPath(); c.moveTo(10,h-14); c.lineTo(35,h-40); c.lineTo(60,h-14); c.fill();
  c.fillStyle=m.groundBrick; c.fillRect(0,h-14,w,14);
  c.fillStyle=m.groundTop;   c.fillRect(0,h-14,w,4);
  c.fillStyle=m.platformColor; c.fillRect(20,h-28,30,6);
  c.fillStyle=m.platformTop;   c.fillRect(20,h-28,30,3);
  c.fillStyle='#cc2200'; c.fillRect(8,h-20,6,6);
  c.fillStyle='#f5c5a3'; c.fillRect(9,h-24,5,5);
  c.fillStyle='#ffd700'; c.fillRect(50,h-32,5,8);
  c.fillStyle=m.enemyColor; c.fillRect(70,h-20,10,8);
  c.fillStyle=m.enemyTop;   c.fillRect(70,h-24,10,6);
}

function renderShop() {
  const grid=document.getElementById('mapGrid');
  grid.innerHTML='';
  MAPS.forEach(map=>{
    const owned=state.ownedMaps.includes(map.id);
    const active=state.activeMap===map.id;
    const card=document.createElement('div');
    card.className='map-card'+(owned?' owned':'')+(active?' active':'');
    const pc=document.createElement('canvas'); pc.width=100; pc.height=60;
    drawMapPreview(pc,map); card.appendChild(pc);
    const nm=document.createElement('div'); nm.className='map-name'; nm.textContent=map.name; card.appendChild(nm);
    const pr=document.createElement('div'); pr.className='map-price';
    if(active){pr.innerHTML='✅ ACTIVE';pr.style.color='#ffd700';}
    else if(owned){pr.innerHTML='✔ OWNED — <span>TAP TO USE</span>';}
    else{pr.innerHTML='🪙 <span>'+map.price+'</span> COINS';}
    card.appendChild(pr);
    if(active){const b=document.createElement('div');b.className='map-badge';b.textContent='▶ ON';card.appendChild(b);}
    card.onclick=()=>{
      if(owned){state.activeMap=map.id;renderShop();initLevel();updateHUD();}
      else{
        if(state.coins>=map.price){
          state.coins-=map.price;state.ownedMaps.push(map.id);
          state.activeMap=map.id;initLevel();updateHUD();renderShop();
        } else { alert('Need '+(map.price-state.coins)+' more coins!'); }
      }
    };
    grid.appendChild(card);
  });
}

// ── LEVEL INIT ────────────────────────────────────────────────────────────
function initLevel() {
  level=genLevel(state.activeMap);
  resetPlayer(); particles=[]; floatTexts=[];
  state.time=120+state.level*20;
  clearInterval(state.timeTimer);
  state.timeTimer=setInterval(()=>{
    if(state.scene!=='playing') return;
    state.time--;
    if(state.time<=0) killPlayer('TIME UP!');
    updateHUD();
  },1000);
}

// ── SCENE CONTROL ──────────────────────────────────────────────────────────
function startGame() {
  state.scene='playing'; state.score=0; state.lives=3; state.level=0;
  ['startOverlay','gameOverOverlay','winOverlay'].forEach(id=>
    document.getElementById(id).style.display='none');
  initLevel(); updateHUD();
}

function nextLevel() {
  state.level++; state.scene='playing';
  document.getElementById('winOverlay').style.display='none';
  initLevel(); updateHUD();
}

function togglePause() {
  if(state.scene==='playing'){
    state.scene='paused';
    document.getElementById('pauseOverlay').style.display='flex';
  } else if(state.scene==='paused'){
    resumeGame();
  }
}

function pauseGame() {
  state.scene='paused';
  document.getElementById('pauseOverlay').style.display='flex';
}

function resumeGame() {
  state.scene='playing';
  document.getElementById('pauseOverlay').style.display='none';
  document.getElementById('shopOverlay').style.display='none';
}

function openShop() {
  if(state.scene==='playing') pauseGame();
  document.getElementById('pauseOverlay').style.display='none';
  renderShop();
  document.getElementById('shopCoins').textContent=state.coins;
  document.getElementById('shopOverlay').style.display='flex';
}

function closeShop() {
  document.getElementById('shopOverlay').style.display='none';
  if(state.scene==='paused') resumeGame();
}

// ── BOOT ──────────────────────────────────────────────────────────────────
level=genLevel(0);
resetPlayer();
updateHUD();
loop();
</script>
</body>
</html>
