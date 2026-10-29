
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no, viewport-fit=cover">
<title>BUBBLEGUM GALAXY — 3D Action Adventure</title>
<style>
:root{--pink:#ff5fc8;--cyan:#4df8ff;--purple:#8e65ff;--ink:#100c2c}
*{box-sizing:border-box}html,body{margin:0;width:100%;height:100%;overflow:hidden;background:#100c2c;color:#fff;font-family:system-ui,-apple-system,Segoe UI,sans-serif;touch-action:manipulation}
#game{position:fixed;inset:0;overflow:hidden;background:radial-gradient(ellipse at 50% 20%,#442a88,#120c2e 70%)}
canvas{display:block;width:100%;height:100%;touch-action:none}
.overlay{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;background:linear-gradient(135deg,rgba(12,7,39,.72),rgba(40,10,65,.48));backdrop-filter:blur(5px);padding:18px;z-index:5}
.panel{width:min(620px,96vw);max-height:94vh;overflow:auto;border:1px solid rgba(111,246,255,.55);border-radius:26px;padding:clamp(18px,4vw,32px);background:linear-gradient(145deg,rgba(31,18,72,.94),rgba(71,22,98,.91));box-shadow:0 0 40px #8c44ff35,inset 0 0 24px #ff67d51a;text-align:center}
.logo{font-weight:1000;line-height:.9;letter-spacing:-.055em;font-size:clamp(36px,8vw,68px);color:#ff82d8;text-shadow:3px 4px 0 #8538c8,0 0 18px #ff6acb,0 0 36px #5cf7ff;transform:rotate(-2deg);margin:8px 0 16px}
.logo span{display:block;color:#fff;font-size:.48em;letter-spacing:.2em;margin-top:12px;text-shadow:0 0 14px #4df8ff}
.subtitle{color:#d9d4ff;font-size:14px;line-height:1.5;margin:12px auto 20px;max-width:480px}
button{font:inherit;font-weight:800;color:white;border:1px solid #8ffaffa8;border-radius:14px;padding:12px 18px;background:linear-gradient(135deg,#ff4fc2,#8c55ff);box-shadow:0 5px 0 #512d9b,0 0 18px #ff53c65c;cursor:pointer;touch-action:manipulation}
button:active{transform:translateY(3px);box-shadow:0 2px 0 #512d9b}
button.secondary{background:linear-gradient(135deg,#167f9a,#5157c7);box-shadow:0 5px 0 #203c81}
button.ghost{background:#24194d;box-shadow:none}
.menuButtons{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px;margin-top:18px}
.menuButtons button:first-child{grid-column:1/-1;font-size:20px;padding:15px}
#hud{position:absolute;inset:0;pointer-events:none;z-index:2;display:none}
.hudTop{position:absolute;top:max(12px,env(safe-area-inset-top));left:12px;right:12px;display:flex;justify-content:space-between;align-items:flex-start;gap:10px}
.hudCard{background:#170f3cbb;border:1px solid #8b79ff80;border-radius:14px;padding:9px 12px;box-shadow:0 0 16px #5e52ff20;backdrop-filter:blur(8px);font-size:12px}
.stat{width:min(220px,40vw)}.statLabel{display:flex;justify-content:space-between;font-weight:800;margin-bottom:5px}.bar{height:9px;background:#ffffff20;border-radius:99px;overflow:hidden;margin:4px 0 7px}.fill{height:100%;width:100%;border-radius:99px;background:linear-gradient(90deg,#ff53b9,#ff9bda)}#energyFill{background:linear-gradient(90deg,#36d9ff,#a3fff9)}
#objective{position:absolute;top:104px;left:12px;max-width:230px;color:#fff}
#bossHUD{display:none;position:absolute;top:14%;left:50%;transform:translateX(-50%);width:min(380px,70vw);text-align:center}
#bossHUD .bar{height:13px;border:1px solid #ffb5f4;background:#280d36}
#crystalCount{font-size:14px;font-weight:900;color:#9afaff}
#pauseBtn{pointer-events:auto;padding:8px 12px}
#toast{position:absolute;top:22%;left:50%;transform:translateX(-50%);background:#24104ddd;border:1px solid #ff7ed9;border-radius:999px;padding:9px 18px;font-weight:900;opacity:0;transition:opacity .2s;white-space:nowrap}
#mobileControls{display:none;position:absolute;inset:0;pointer-events:none}
#stickBase{position:absolute;left:22px;bottom:25px;width:124px;height:124px;border:2px solid #ffffff70;border-radius:50%;background:#22154c88;pointer-events:auto;touch-action:none}
#stickKnob{position:absolute;left:35px;top:35px;width:50px;height:50px;border-radius:50%;background:linear-gradient(135deg,#ff73cf,#5cecff);box-shadow:0 0 18px #6efaff88}
.mobileBtns{position:absolute;right:15px;bottom:20px;display:grid;grid-template-columns:repeat(2,64px);gap:9px;pointer-events:auto}
.mobileBtns button{padding:0;width:64px;height:58px;border-radius:18px;font-size:11px;box-shadow:0 3px 0 #512d9b;background:linear-gradient(135deg,#ec49b8,#7255ff)}
#lookHint{position:absolute;right:18px;bottom:155px;font-size:10px;color:#ffffff99;text-align:right}
.small{font-size:12px;color:#c9c4ec;line-height:1.5}
.settingsRow{display:flex;align-items:center;justify-content:space-between;gap:12px;margin:15px 0;text-align:left}.settingsRow input{width:48%}
#gameOver,#victory,#pauseMenu,#settingsMenu,#worldMenu,#customMenu{display:none}
@media (pointer:coarse),(max-width:800px){#mobileControls{display:block}#objective{top:110px;max-width:190px}.hudCard{padding:8px;font-size:11px}.stat{width:150px}.menuButtons{gap:9px}.menuButtons button{font-size:13px;padding:10px}}
@media (orientation:portrait){#rotateNotice{display:flex!important}}
#rotateNotice{display:none;position:absolute;z-index:10;inset:0;background:#100c2c;color:white;align-items:center;justify-content:center;text-align:center;padding:35px;font-weight:800}
</style>
</head>
<body>
<div id="game">
  <div id="rotateNotice">↻<br><br>Rotate your device to landscape for the best Bubblegum Galaxy experience.</div>
  <div id="hud">
    <div class="hudTop">
      <div class="hudCard stat"><div class="statLabel"><span>💗 GUMI</span><span id="healthText">100 / 100</span></div><div class="bar"><div class="fill" id="healthFill"></div></div><div class="statLabel"><span>⚡ ENERGY</span><span id="energyText">100%</span></div><div class="bar"><div class="fill" id="energyFill"></div></div></div>
      <div class="hudCard" style="text-align:center"><div id="worldName">WORLD 1 · BUBBLEGUM MEADOWS</div><div id="crystalCount">💎 0 / 20</div><div id="scoreText">SCORE 0000</div></div>
      <button id="pauseBtn" class="ghost">Ⅱ</button>
    </div>
    <div id="objective" class="hudCard">✨ <b>MISSION</b><br><span id="objectiveText">Collect 20 Gum Crystals and find the guardian!</span></div>
    <div id="bossHUD"><b id="bossName">MINI GUM GUARDIAN</b><div class="bar"><div class="fill" id="bossFill" style="width:100%;background:linear-gradient(90deg,#ff4c8d,#ffbe6b)"></div></div></div>
    <div id="toast"></div>
  </div>
  <div id="mobileControls">
    <div id="stickBase"><div id="stickKnob"></div></div>
    <div id="lookHint">DRAG RIGHT SIDE TO LOOK</div>
    <div class="mobileBtns">
      <button id="attackTouch">🫧<br>ATTACK</button><button id="jumpTouch">⬆<br>JUMP</button>
      <button id="dashTouch">💨<br>DASH</button><button id="shieldTouch">🛡<br>SHIELD</button>
      <button id="specialTouch">💥<br>MEGA</button><button id="interactTouch">✦<br>GRAPPLE</button>
    </div>
  </div>
  <div id="mainMenu" class="overlay">
    <div class="panel">
      <div class="logo">BUBBLEGUM<span>GALAXY ✦</span></div>
      <div class="subtitle">A candy-cosmic action adventure. The Sugar Void has invaded the galaxy — suit up as GUMI, blast the bots, collect cosmic gum crystals, and face the Mini Gum Guardian!</div>
      <div class="menuButtons">
        <button id="startBtn">▶ START ADVENTURE</button>
        <button id="continueBtn" class="secondary">↻ CONTINUE</button>
        <button id="worldBtn" class="secondary">✦ WORLD MAP</button>
        <button id="customBtn" class="secondary">🎨 HERO LAB</button>
        <button id="settingsBtn" class="ghost">⚙ SETTINGS</button>
        <button id="helpBtn" class="ghost">⌨ HELP & CONTROLS</button>
      </div>
      <p class="small">3D browser prototype · Best in landscape · Progress saves locally on this device</p>
    </div>
  </div>
  <div id="pauseMenu" class="overlay"><div class="panel"><div class="logo" style="font-size:48px">PAUSED<span>TIME TO BREATHE</span></div><p class="subtitle">The galaxy can wait a moment.</p><div class="menuButtons"><button id="resumeBtn">▶ RESUME</button><button id="restartBtn" class="secondary">↻ RESTART LEVEL</button><button id="pauseWorldBtn" class="secondary">✦ WORLD MAP</button><button id="pauseSettingsBtn" class="ghost">⚙ SETTINGS</button><button id="homeBtn" class="ghost">⌂ MAIN MENU</button></div></div></div>
  <div id="settingsMenu" class="overlay"><div class="panel"><h2>⚙ GAME SETTINGS</h2><div class="settingsRow"><label for="musicVol">Music volume</label><input id="musicVol" type="range" min="0" max="1" step=".05" value=".35"></div><div class="settingsRow"><label for="sfxVol">Sound effects</label><input id="sfxVol" type="range" min="0" max="1" step=".05" value=".6"></div><div class="settingsRow"><label for="effectsToggle">Visual effects</label><input id="effectsToggle" type="checkbox" checked></div><p class="small">Sound starts after your first tap due to browser audio rules.</p><button id="settingsBack">← BACK</button></div></div>
  <div id="worldMenu" class="overlay"><div class="panel"><h2>✦ GALAXY MAP</h2><p class="subtitle">World 1 is playable in this prototype. Other worlds are preview destinations.</p><div class="menuButtons"><button id="meadowBtn">🌸 BUBBLEGUM MEADOWS · PLAY</button><button class="secondary" data-locked="Lollipop Nebula">🪐 LOLLIPOP NEBULA · LOCKED</button><button class="secondary" data-locked="Jelly Crystal Caverns">💎 JELLY CRYSTAL CAVERNS · LOCKED</button><button class="secondary" data-locked="Chocolate Comet">🍫 CHOCOLATE COMET · LOCKED</button><button class="secondary" data-locked="Sugar Void Citadel">👑 SUGAR VOID CITADEL · LOCKED</button></div><br><button id="worldBack" class="ghost">← BACK</button></div></div>
  <div id="customMenu" class="overlay"><div class="panel"><h2>🎨 GUMI HERO LAB</h2><p class="subtitle">Choose GUMI's armor glow. Cosmetic changes apply instantly.</p><div class="menuButtons"><button data-color="#ff59c8">NEON PINK</button><button data-color="#4df8ff" class="secondary">GALACTIC CYAN</button><button data-color="#ffca54" class="secondary">GOLDEN GUM</button><button data-color="#a3ff70" class="secondary">MINT POP</button></div><br><button id="customBack" class="ghost">← BACK</button></div></div>
  <div id="victory" class="overlay"><div class="panel"><div class="logo">GALAXY SAVED!<span>✦ SWEET VICTORY ✦</span></div><p class="subtitle">The Mini Gum Guardian has been defeated! Bubblegum Meadows are safe — for now.</p><div id="victoryStats" class="hudCard"></div><div class="menuButtons"><button id="replayBtn">↻ PLAY AGAIN</button><button id="victoryHome" class="secondary">⌂ MAIN MENU</button></div></div></div>
  <div id="gameOver" class="overlay"><div class="panel"><div class="logo" style="font-size:48px">POP! TRY AGAIN<span>GUMI NEEDS A RECHARGE</span></div><p class="subtitle">A little setback is just a springboard to the next attempt.</p><div class="menuButtons"><button id="retryBtn">↻ RETRY CHECKPOINT</button><button id="overHome" class="secondary">⌂ MAIN MENU</button></div></div></div>
</div>
<script src="https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.min.js"></script>
<script>
(()=> {
'use strict';
const $=id=>document.getElementById(id);
const ui=['mainMenu','pauseMenu','settingsMenu','worldMenu','customMenu','victory','gameOver'];
let scene,camera,renderer,clock,player,playerCore,playerGlow,ground,worldGroup;
let running=false,state='menu',health=100,energy=100,score=0,crystals=0,kills=0,elapsed=0,bossActive=false,boss=null,bossHP=100;
let enemies=[],gems=[],projectiles=[],effects=[],platforms=[],keys={},joy={x:0,y:0},cameraYaw=0,cameraPitch=.22,camTouch=null,lastAttack=0,lastDash=0,lastShield=0,lastSpecial=0,invuln=0,combo=0,comboTimer=0,checkpoint=new THREE.Vector3(0,0,5),armorColor='#ff59c8',musicVolume=.35,sfxVolume=.6,effectsOn=true,audioCtx=null;
const worldSize=150;
function showOnly(id){ui.forEach(k=>$(k).style.display=k===id?'flex':'none');}
function toast(s){const t=$('toast');t.textContent=s;t.style.opacity=1;clearTimeout(toast._t);toast._t=setTimeout(()=>t.style.opacity=0,1800)}
function save(){try{localStorage.setItem('bubblegumGalaxySave',JSON.stringify({best:Math.max(score,Number(JSON.parse(localStorage.getItem('bubblegumGalaxySave')||'{}').best||0)),color:armorColor,settings:{musicVolume,sfxVolume,effectsOn}}))}catch(e){}}
function loadSave(){try{const d=JSON.parse(localStorage.getItem('bubblegumGalaxySave')||'{}');armorColor=d.color||armorColor;if(d.settings){musicVolume=d.settings.musicVolume??musicVolume;sfxVolume=d.settings.sfxVolume??sfxVolume;effectsOn=d.settings.effectsOn??true;$('musicVol').value=musicVolume;$('sfxVol').value=sfxVolume;$('effectsToggle').checked=effectsOn}}catch(e){}}
function sound(freq=500,dur=.08,type='sine',vol=.08){if(!audioCtx||sfxVolume<=0)return;try{let o=audioCtx.createOscillator(),g=audioCtx.createGain();o.type=type;o.frequency.setValueAtTime(freq,audioCtx.currentTime);g.gain.setValueAtTime(vol*sfxVolume,audioCtx.currentTime);g.gain.exponentialRampToValueAtTime(.001,audioCtx.currentTime+dur);o.connect(g);g.connect(audioCtx.destination);o.start();o.stop(audioCtx.currentTime+dur)}catch(e){}}
function initAudio(){if(!audioCtx){try{audioCtx=new(window.AudioContext||window.webkitAudioContext)()}catch(e){}}if(audioCtx&&audioCtx.state==='suspended')audioCtx.resume()}
function mat(color,rough=.35,metal=0,emissive=null){return new THREE.MeshStandardMaterial({color,roughness:rough,metalness:metal,emissive:emissive||0,emissiveIntensity:emissive?1.1:0})}
function candyBall(radius,color,rough=.22,emissive=null){return new THREE.Mesh(new THREE.SphereGeometry(radius,20,16),mat(color,rough,0,emissive))}
function addGlow(obj,color,intensity=.8){const l=new THREE.PointLight(color,intensity,7);l.position.set(0,0,0);obj.add(l);return l}
function makeTextSprite(text,color='#fff'){const c=document.createElement('canvas');c.width=256;c.height=64;const x=c.getContext('2d');x.font='bold 28px system-ui';x.textAlign='center';x.fillStyle=color;x.strokeStyle='#25104d';x.lineWidth=5;x.strokeText(text,128,42);x.fillText(text,128,42);const tx=new THREE.CanvasTexture(c);const s=new THREE.Sprite(new THREE.SpriteMaterial({map:tx,transparent:true}));s.scale.set(3,0.75,1);return s}
function buildScene(){
 scene=new THREE.Scene();scene.background=new THREE.Color('#170b3a');scene.fog=new THREE.FogExp2('#24104b',.006);
 camera=new THREE.PerspectiveCamera(65,innerWidth/innerHeight,.1,450);
 renderer=new THREE.WebGLRenderer({antialias:!matchMedia('(pointer:coarse)').matches,alpha:false,powerPreference:'high-performance'});
 renderer.setPixelRatio(Math.min(devicePixelRatio,1.7));renderer.setSize(innerWidth,innerHeight);renderer.shadowMap.enabled=true;renderer.shadowMap.type=THREE.PCFSoftShadowMap;renderer.outputColorSpace=THREE.SRGBColorSpace;renderer.toneMapping=THREE.ACESFilmicToneMapping;renderer.toneMappingExposure=1.15;
 $('game').prepend(renderer.domElement);
 clock=new THREE.Clock();
 scene.add(new THREE.HemisphereLight('#b9dcff','#59266c',2.0));
 const sun=new THREE.DirectionalLight('#ffe1ff',3.2);sun.position.set(-15,28,12);sun.castShadow=true;sun.shadow.mapSize.set(1024,1024);sun.shadow.camera.left=-45;sun.shadow.camera.right=45;sun.shadow.camera.top=45;sun.shadow.camera.bottom=-45;scene.add(sun);
 worldGroup=new THREE.Group();scene.add(worldGroup);
 // star field
 const starGeo=new THREE.BufferGeometry(),arr=[];for(let i=0;i<950;i++){arr.push((Math.random()-.5)*300,Math.random()*150-10,(Math.random()-.5)*300)}
 starGeo.setAttribute('position',new THREE.Float32BufferAttribute(arr,3));scene.add(new THREE.Points(starGeo,new THREE.PointsMaterial({color:'#bcefff',size:.38,transparent:true,opacity:.9})));
 // pastel planetary backdrops
 for(let i=0;i<8;i++){let p=candyBall(3+Math.random()*5,['#ff68ca','#8e62ff','#43ddff','#ffbf69'][i%4],.38);p.position.set((Math.random()-.5)*100,10+Math.random()*50,-40-Math.random()*100);scene.add(p);let ring=new THREE.Mesh(new THREE.TorusGeometry(p.geometry.parameters.radius*1.3,.09,8,64),mat('#6cf8ff',.3,.4,'#6cf8ff'));ring.rotation.x=1.1;ring.rotation.y=.25;p.add(ring)}
 createLevel();
}
function createLevel(){
 while(worldGroup.children.length)worldGroup.remove(worldGroup.children[0]);
 enemies=[];gems=[];projectiles=[];effects=[];platforms=[];boss=null;bossActive=false;bossHP=100;
 // central floating island ground
 const g=new THREE.Mesh(new THREE.CylinderGeometry(42,48,5,64),mat('#e85fc7',.27,0,'#5d175f'));g.position.y=-2.7;g.receiveShadow=true;g.castShadow=true;worldGroup.add(g);ground=g;
 const top=new THREE.Mesh(new THREE.CircleGeometry(42,64),mat('#ff9add',.28,0,'#7b2977'));top.rotation.x=-Math.PI/2;top.position.y=-.17;top.receiveShadow=true;worldGroup.add(top);
 // paths/platforms
 const platformDefs=[[-17,1,0,7],[-25,3,-12,5],[-11,5,-20,5],[5,7,-23,5],[20,4,-18,6],[28,2,-5,6],[18,5,12,5],[0,3,20,6],[-20,2,18,6]];
 platformDefs.forEach(([x,y,z,r],i)=>{const m=new THREE.Mesh(new THREE.CylinderGeometry(r,r*1.08,1.1,24),mat(i%2?'#62e9ff':'#bd78ff',.22,0,i%2?'#1b789c':'#5c2a9b'));m.position.set(x,y,z);m.castShadow=true;m.receiveShadow=true;worldGroup.add(m);platforms.push({mesh:m,x,z,r,y});const rim=new THREE.Mesh(new THREE.TorusGeometry(r*.94,.12,8,32),mat(i%2?'#d5ffff':'#ffd5f5',.2,0,'#ffffff'));rim.rotation.x=Math.PI/2;rim.position.set(x,y+.56,z);worldGroup.add(rim)});
 // rainbow bridges as glowing beams
 for(let i=0;i<5;i++){const beam=new THREE.Mesh(new THREE.BoxGeometry(13,.28,1.5),mat(['#ff65c9','#ffd36b','#7fffe4','#8b7bff'][i%4],.25,0,['#ff65c9','#ffd36b','#7fffe4','#8b7bff'][i%4]));beam.position.set(-23+i*11,.1,8-i*4);beam.rotation.y=-.32;worldGroup.add(beam)}
 // candy forest
 for(let i=0;i<30;i++){const a=Math.random()*Math.PI*2,r=15+Math.random()*25,x=Math.cos(a)*r,z=Math.sin(a)*r;if(Math.hypot(x,z)<9)continue;const trunk=new THREE.Mesh(new THREE.CylinderGeometry(.25,.45,2.2,8),mat('#a94c87'));trunk.position.set(x,.8,z);trunk.castShadow=true;worldGroup.add(trunk);const crown=candyBall(.9+Math.random()*.7,['#ff67c9','#ffce73','#8bf5ed','#b19aff'][i%4]);crown.position.set(x,2.3,z);crown.castShadow=true;worldGroup.add(crown);for(let b=0;b<2;b++){const bubble=candyBall(.12+Math.random()*.16,'#fff0ff',.1,'#ff8bdf');bubble.material.transparent=true;bubble.material.opacity=.6;bubble.position.set(x+(Math.random()-.5)*2,3+Math.random()*2,z+(Math.random()-.5)*2);worldGroup.add(bubble)}}
 // lollipop props
 for(let i=0;i<10;i++){let x=(Math.random()-.5)*65,z=(Math.random()-.5)*65;if(Math.hypot(x,z)<10)continue;let stick=new THREE.Mesh(new THREE.CylinderGeometry(.16,.2,3.4,8),mat('#f4d9ff'));stick.position.set(x,1.5,z);worldGroup.add(stick);let lol=candyBall(.85,['#ff59c8','#4df8ff','#ffd15b'][i%3]);lol.position.set(x,3.35,z);worldGroup.add(lol);let swirl=new THREE.Mesh(new THREE.TorusGeometry(.48,.12,8,24),mat('#fff1fb'));swirl.position.copy(lol.position);swirl.rotation.x=.4;worldGroup.add(swirl)}
 // crystals
 const gemPositions=[];for(let i=0;i<20;i++){const a=i*2.399,r=7+(i%5)*5;gemPositions.push([Math.cos(a)*r,1.1+(i%3)*.5,Math.sin(a)*r])}
 gemPositions.forEach((p,i)=>{const mesh=new THREE.Mesh(new THREE.OctahedronGeometry(.52,0),mat(i%4===0?'#ffe67c':i%2?'#58f7ff':'#ff68d2',.16,.15,i%4===0?'#ffca4b':i%2?'#39e9ff':'#ff39bb'));mesh.position.set(...p);mesh.castShadow=true;worldGroup.add(mesh);const glow=new THREE.PointLight(i%2?'#4df8ff':'#ff62d4',.55,4);glow.position.copy(mesh.position);worldGroup.add(glow);gems.push({mesh,baseY:mesh.position.y,got:false})});
 // enemies scattered
 for(let i=0;i<7;i++)spawnEnemy(new THREE.Vector3((Math.random()-.5)*48,0,(Math.random()-.5)*48),i%3===0?'drone':'bot');
 // start platform player spawn
 makePlayer();
 // boss arena at far edge
 const arena=new THREE.Mesh(new THREE.CylinderGeometry(10,12,1,32),mat('#5a2aa0',.28,.1,'#4d1b95'));arena.position.set(0,.2,-34);arena.receiveShadow=true;worldGroup.add(arena);const ring=new THREE.Mesh(new THREE.TorusGeometry(9.7,.24,8,64),mat('#ff72dc',.2,0,'#ff5cc8'));ring.rotation.x=Math.PI/2;ring.position.set(0,.8,-34);worldGroup.add(ring);
 // floating donut props
 for(let i=0;i<8;i++){const d=new THREE.Mesh(new THREE.TorusGeometry(1.7,.55,12,32),mat(['#ff83c9','#ffc968','#73f5ee'][i%3],.25,0,'#ff7bd6'));d.position.set((Math.random()-.5)*65,5+Math.random()*7,(Math.random()-.5)*65);d.rotation.x=Math.random()*Math.PI;worldGroup.add(d);d.userData.float=true;d.userData.phase=Math.random()*6}
}
function makePlayer(){
 if(player)scene.remove(player);
 player=new THREE.Group();
 const body=new THREE.Mesh(new THREE.CapsuleGeometry(.62,.95,5,10),mat('#f6eaff',.27,.12));body.position.y=1.25;body.castShadow=true;player.add(body);
 const armor=new THREE.Mesh(new THREE.SphereGeometry(.68,20,16),mat(armorColor,.22,.18,armorColor));armor.scale.set(1,1.05,.8);armor.position.set(0,1.4,0);armor.castShadow=true;player.add(armor);playerGlow=armor.material;
 const visor=new THREE.Mesh(new THREE.SphereGeometry(.43,20,14),new THREE.MeshStandardMaterial({color:'#31185b',metalness:.4,roughness:.12,emissive:'#4df8ff',emissiveIntensity:.5}));visor.scale.set(1,.62,.5);visor.position.set(0,1.75,-.48);player.add(visor);
 for(let s of [-1,1]){const eye=candyBall(.09,'#d7ffff',.1,'#4df8ff');eye.position.set(s*.16,1.78,-.73);player.add(eye);const arm=new THREE.Mesh(new THREE.SphereGeometry(.28,12,10),mat(armorColor,.2,.2,'#4df8ff'));arm.position.set(s*.78,1.35,-.02);arm.scale.set(.8,1.1,.8);player.add(arm);const leg=new THREE.Mesh(new THREE.CapsuleGeometry(.18,.48,3,8),mat('#8e65ff',.28,.2));leg.position.set(s*.28,.42,0);player.add(leg);const shoe=candyBall(.25,'#4df8ff',.2,'#4df8ff');shoe.scale.set(1,.5,1.2);shoe.position.set(s*.28,.12,-.1);player.add(shoe)}
 const pack=new THREE.Mesh(new THREE.BoxGeometry(.65,.7,.35),mat('#8b59ff',.25,.25,'#5d42ff'));pack.position.set(0,1.2,.52);player.add(pack);const core=candyBall(.22,'#a9ffff',.12,'#4df8ff');core.position.set(0,1.35,-.59);player.add(core);addGlow(core,'#4df8ff',.9);
 player.position.set(0,0,7);player.userData.velY=0;player.userData.grounded=true;player.userData.facing=0;scene.add(player);
}
function spawnEnemy(pos,type='bot'){
 const e=new THREE.Group();const color=type==='drone'?'#6df8ff':'#9d68ff';const body=candyBall(type==='drone'?.62:.7,color,.24,.25?color:null);body.position.y=type==='drone'?1.8:1;body.castShadow=true;e.add(body);
 const eye=candyBall(.18,'#ffdf7a',.12,'#ffbd42');eye.position.set(0,type==='drone'?1.95:1.18,-.52);e.add(eye);
 if(type==='drone'){const ring=new THREE.Mesh(new THREE.TorusGeometry(.72,.12,8,24),mat('#ff61ca',.2,0,'#ff61ca'));ring.rotation.x=Math.PI/2;ring.position.y=1.8;e.add(ring)}
 else for(let s of [-1,1]){const foot=candyBall(.22,'#ff61ca');foot.position.set(s*.45,.35,0);e.add(foot)}
 e.position.copy(pos);e.userData={type,hp:type==='drone'?35:45,max:type==='drone'?35:45,phase:Math.random()*6,attack:1+Math.random()*2,alive:true,home:pos.clone(),hitFlash:0};worldGroup.add(e);enemies.push(e);return e;
}
function spawnBoss(){if(boss)return;bossActive=true;bossHP=100;boss=new THREE.Group();const body=new THREE.Mesh(new THREE.SphereGeometry(2.7,28,20),mat('#7d3ed8',.2,.35,'#7c35ff'));body.scale.set(1,1.2,.85);body.position.y=3;body.castShadow=true;boss.add(body);const crown=new THREE.Mesh(new THREE.ConeGeometry(1.5,.9,7),mat('#ffcf6c',.18,.25,'#ffb82e'));crown.position.set(0,5.1,0);crown.rotation.y=.25;boss.add(crown);for(let s of [-1,1]){const arm=new THREE.Mesh(new THREE.CapsuleGeometry(.42,2,5,10),mat('#ff62cb',.22,.25,'#ff50c8'));arm.position.set(s*3,3,0);arm.rotation.z=s*.45;arm.castShadow=true;boss.add(arm);const fist=candyBall(.65,'#55f6ff',.15,'#42eaff');fist.position.set(s*3.6,2.1,0);boss.add(fist)}const eye=candyBall(.4,'#aaffff',.1,'#4df8ff');eye.position.set(0,3.3,-2.25);boss.add(eye);boss.position.set(0,0,-34);boss.userData={attack:2.5,phase:0,hit:0,alive:true};worldGroup.add(boss);$('bossHUD').style.display='block';$('bossName').textContent='MINI GUM GUARDIAN';toast('⚠ MINI GUM GUARDIAN AWAKENS!');sound(180,.4,'sawtooth',.12)}
function spawnProjectile(from,to,kind='enemy',speed=12){
 const mesh=candyBall(kind==='player'? .24:.28,kind==='player'?'#69ffff':'#ff5c91',.14,kind==='player'?'#4df8ff':'#ff3275');mesh.position.copy(from);worldGroup.add(mesh);const dir=to.clone().sub(from).normalize();projectiles.push({mesh,dir,speed,kind,life:3,damage:kind==='player'?20:12});if(kind==='player')addGlow(mesh,'#4df8ff',.25)
}
function popEffect(pos,color='#ff77d9',count=8){if(!effectsOn)return;for(let i=0;i<count;i++){const m=candyBall(.08+Math.random()*.12,color,.18,color);m.position.copy(pos);worldGroup.add(m);effects.push({mesh:m,vel:new THREE.Vector3((Math.random()-.5)*5,Math.random()*5,(Math.random()-.5)*5),life:.65})}}
function playerAttack(special=false){if(state!=='playing'||!player)return;let now=performance.now();if(special){if(now-lastSpecial<5000||energy<35){toast('Mega Bubble charging…');return}lastSpecial=now;energy-=35;const from=player.position.clone().add(new THREE.Vector3(0,1.5,0));const dir=new THREE.Vector3(Math.sin(cameraYaw),0,-Math.cos(cameraYaw));const m=candyBall(.75,'#ff7bdf',.12,'#ff52c9');m.position.copy(from);worldGroup.add(m);projectiles.push({mesh:m,dir,speed:20,kind:'mega',life:2.4,damage:55});addGlow(m,'#ff4bc4',1.2);toast('💥 MEGA BUBBLE!');sound(260,.25,'sawtooth',.12);return}
 if(now-lastAttack<260)return;lastAttack=now;energy=Math.min(100,energy+2);const from=player.position.clone().add(new THREE.Vector3(0,1.5,0));const dir=new THREE.Vector3(Math.sin(cameraYaw),0,-Math.cos(cameraYaw));spawnProjectile(from,from.clone().add(dir.multiplyScalar(20)),'player',24);sound(640,.07,'sine',.08)}
function useDash(){if(state!=='playing'||performance.now()-lastDash<1100||energy<12)return;lastDash=performance.now();energy-=12;const dir=new THREE.Vector3(Math.sin(cameraYaw),0,-Math.cos(cameraYaw));player.position.addScaledVector(dir,4.5);player.userData.velY=Math.max(player.userData.velY||0,.5);invuln=.45;popEffect(player.position.clone().add(new THREE.Vector3(0,1,0)),'#63f8ff',5);sound(320,.13,'triangle',.09)}
function useShield(){if(state!=='playing'||performance.now()-lastShield<5000||energy<20)return;lastShield=performance.now();energy-=20;invuln=2.2;const sh=new THREE.Mesh(new THREE.SphereGeometry(1.5,24,16),new THREE.MeshBasicMaterial({color:'#6ffaff',wireframe:true,transparent:true,opacity:.5}));sh.position.set(0,1,0);player.add(sh);setTimeout(()=>{if(sh.parent)sh.parent.remove(sh)},2200);toast('🛡 BUBBLE SHIELD!');sound(440,.16,'sine',.1)}
function jump(){if(state!=='playing')return;if(player.userData.grounded){player.userData.velY=10;player.userData.grounded=false;sound(400,.08,'triangle',.06)}else if(!player.userData.double){player.userData.velY=9;player.userData.double=true;popEffect(player.position.clone(),'#ff75d7',5);sound(620,.1,'triangle',.06)}}
function movePlayer(dt){
 const f=(keys.KeyW||keys.ArrowUp?1:0)-(keys.KeyS||keys.ArrowDown?1:0)-joy.y;
 const r=(keys.KeyD||keys.ArrowRight?1:0)-(keys.KeyA||keys.ArrowLeft?1:0)+joy.x;
 let v=new THREE.Vector3(r,0,-f);if(v.length()>1)v.normalize();
 if(v.length()>.05){const angle=Math.atan2(v.x,-v.z)+cameraYaw;player.position.x+=Math.sin(angle)*10*dt;player.position.z+=-Math.cos(angle)*10*dt;player.rotation.y=angle}
 if(keys.ShiftLeft||keys.ShiftRight)useDash();
 player.userData.velY-=24*dt;player.position.y+=player.userData.velY*dt;
 let floorY=0;let grounded=false;
 if(Math.hypot(player.position.x,player.position.z)<40 && player.position.y<=0){floorY=0;grounded=true}
 platforms.forEach(p=>{if(Math.abs(player.position.x-p.x)<p.r*.82&&Math.abs(player.position.z-p.z)<p.r*.82&&player.userData.velY<=0&&player.position.y<=p.y+.7&&player.position.y>=p.y-1.5){if(p.y>floorY){floorY=p.y;grounded=true}}});
 if(grounded&&player.position.y<=floorY){player.position.y=floorY;player.userData.velY=0;player.userData.grounded=true;player.userData.double=false}else player.userData.grounded=false;
 if(player.position.y < -12 || Math.hypot(player.position.x,player.position.z)>52){player.position.copy(checkpoint);player.userData.velY=0;health=Math.max(health-10,1);toast('Checkpoint bounce! -10 health');}
 player.position.x=THREE.MathUtils.clamp(player.position.x,-47,47);player.position.z=THREE.MathUtils.clamp(player.position.z,-45,45);
}
function updateEnemies(dt){
 enemies.forEach(e=>{const d=e.position.distanceTo(player.position);if(!e.userData.alive)return;e.userData.phase+=dt;const drone=e.userData.type==='drone';e.position.y=(drone?1.7:0)+Math.sin(e.userData.phase*2)*.2;
 if(d<22){const toward=player.position.clone().sub(e.position);toward.y=0;if(d>3.3)e.position.addScaledVector(toward.normalize(),(drone?2.3:3)*dt);e.lookAt(player.position.x,e.position.y,player.position.z);e.userData.attack-=dt;if(e.userData.attack<=0){e.userData.attack=drone?2.2:1.8;if(drone){const from=e.position.clone().add(new THREE.Vector3(0,1.5,0));spawnProjectile(from,player.position.clone().add(new THREE.Vector3(0,1,0)),'enemy',8)}else if(d<4&&invuln<=0){damagePlayer(8);popEffect(player.position.clone(),'#ff649a',5)}}}
 });
}
function damagePlayer(n){if(invuln>0)return;health-=n;invuln=.5;popEffect(player.position.clone().add(new THREE.Vector3(0,1,0)),'#ff4c7d',7);sound(140,.16,'sawtooth',.1);if(health<=0){health=0;state='over';running=false;showOnly('gameOver');$('hud').style.display='none';$('mobileControls').style.display='none'}updateHUD()}
function updateProjectiles(dt){
 for(let i=projectiles.length-1;i>=0;i--){const p=projectiles[i];p.life-=dt;p.mesh.position.addScaledVector(p.dir,p.speed*dt);let remove=p.life<=0;
 if(p.kind==='player'||p.kind==='mega'){for(const e of enemies){if(!e.userData.alive)continue;if(p.mesh.position.distanceTo(e.position.clone().add(new THREE.Vector3(0,1,0)))<1.3){e.userData.hp-=p.damage;e.userData.hitFlash=.12;popEffect(p.mesh.position,'#70ffff',7);remove=true;combo++;comboTimer=2;score+=100+combo*5;if(e.userData.hp<=0){e.userData.alive=false;worldGroup.remove(e);kills++;score+=250;popEffect(e.position,'#ff7bd8',16);toast('BOT POPPED! +250');sound(780,.12,'sine',.1)}break}}
 if(boss&&boss.userData.alive&&p.mesh.position.distanceTo(boss.position.clone().add(new THREE.Vector3(0,3,0)))<3.5){bossHP-=p.damage;popEffect(p.mesh.position,'#ff9ee7',12);remove=true;score+=150;if(bossHP<=0){bossHP=0;boss.userData.alive=false;worldGroup.remove(boss);bossActive=false;$('bossHUD').style.display='none';winGame()}}
 }else if(p.kind==='enemy'&&p.mesh.position.distanceTo(player.position.clone().add(new THREE.Vector3(0,1,0)))<1.2){damagePlayer(p.damage);remove=true}
 if(remove){worldGroup.remove(p.mesh);projectiles.splice(i,1)}
 }
}
function updateGems(dt){gems.forEach(g=>{if(g.got)return;g.mesh.rotation.y+=dt*1.5;g.mesh.position.y=g.baseY+Math.sin(elapsed*2+g.baseY)*.18;if(player.position.distanceTo(g.mesh.position)<1.5){g.got=true;worldGroup.remove(g.mesh);crystals++;score+=100;energy=Math.min(100,energy+4);sound(850,.1,'sine',.08);popEffect(g.mesh.position,'#74ffff',8);if(crystals===20)toast('💎 ALL 20 CRYSTALS FOUND!');updateHUD();save()}})}
function updateBoss(dt){if(!bossActive||!boss)return;const dist=player.position.distanceTo(boss.position);if(dist<17){boss.userData.attack-=dt;boss.rotation.y+=dt*.4;boss.position.y=Math.sin(elapsed*1.5)*.4;if(boss.userData.attack<=0){boss.userData.attack=2.1;const from=boss.position.clone().add(new THREE.Vector3(0,3,0));spawnProjectile(from,player.position.clone().add(new THREE.Vector3(0,1,0)),'enemy',9);if(dist<6&&invuln<=0){damagePlayer(13);toast('GUARDIAN SLAM!')}else toast('⚠ DODGE THE BUBBLE!')}}}
function updateHUD(){$('healthText').textContent=Math.ceil(health)+' / 100';$('healthFill').style.width=Math.max(0,health)+'%';$('energyText').textContent=Math.ceil(energy)+'%';$('energyFill').style.width=energy+'%';$('crystalCount').textContent='💎 '+crystals+' / 20';$('scoreText').textContent='SCORE '+String(score).padStart(4,'0');$('bossFill').style.width=bossHP+'%';$('objectiveText').textContent=bossActive?'Defeat the Mini Gum Guardian!':crystals<20?'Collect Gum Crystals ('+crystals+'/20), pop the Gum Bots, then head to the guardian arena.':'Crystals secured! Enter the glowing guardian arena at the north edge.'}
function winGame(){state='victory';running=false;score+=1000;save();$('hud').style.display='none';$('mobileControls').style.display='none';$('victoryStats').innerHTML='💎 Crystals: <b>'+crystals+'/20</b> &nbsp; 🤖 Bots popped: <b>'+kills+'</b><br>⭐ Score: <b>'+score+'</b><br>⏱ Time: <b>'+Math.floor(elapsed)+'s</b>';showOnly('victory');sound(900,.3,'sine',.12)}
function update(dt){
 elapsed+=dt;invuln=Math.max(0,invuln-dt);energy=Math.min(100,energy+dt*3);comboTimer-=dt;if(comboTimer<=0)combo=0;
 movePlayer(dt);updateEnemies(dt);updateProjectiles(dt);updateGems(dt);updateBoss(dt);
 // ambient floating props
 worldGroup.children.forEach(o=>{if(o.userData.float){o.rotation.y+=dt*.2;o.position.y+=Math.sin(elapsed+o.userData.phase)*dt*.25}});
 // camera follows with stable shoulder view
 const target=player.position.clone().add(new THREE.Vector3(0,1.3,0));const distance=10;const offset=new THREE.Vector3(Math.sin(cameraYaw)*distance,3.8+cameraPitch*5,Math.cos(cameraYaw)*distance);camera.position.lerp(target.clone().add(offset),1-Math.pow(.001,dt));camera.lookAt(target);
 if(!bossActive&&player.position.z<-27&&Math.abs(player.position.x)<12){spawnBoss()}
 updateHUD();
}
function loop(){requestAnimationFrame(loop);const dt=Math.min(clock.getDelta(),.04);if(state==='playing'&&running)update(dt);if(renderer&&scene&&camera)renderer.render(scene,camera)}
function startGame(){initAudio();health=100;energy=100;score=0;crystals=0;kills=0;elapsed=0;combo=0;state='playing';running=true;checkpoint.set(0,0,7);createLevel();showOnly('');$('hud').style.display='block';$('mobileControls').style.display='block';updateHUD();clock.getDelta();toast('GO GUMI! Collect 20 crystals!');}
function pause(){if(state!=='playing')return;state='paused';running=false;showOnly('pauseMenu')}
function resume(){if(state!=='paused')return;state='playing';running=true;showOnly('');clock.getDelta()}
function goHome(){state='menu';running=false;$('hud').style.display='none';$('mobileControls').style.display='none';showOnly('mainMenu')}
function openSettings(from){$('settingsMenu').dataset.from=from;showOnly('settingsMenu')}
function backSettings(){const f=$('settingsMenu').dataset.from;showOnly(f==='pause'?'pauseMenu':'mainMenu')}
function initControls(){
 addEventListener('keydown',e=>{keys[e.code]=true;if(['Space','ArrowUp','ArrowDown','ArrowLeft','ArrowRight'].includes(e.code))e.preventDefault();if(e.code==='Space'&&!e.repeat)jump();if(e.code==='Escape'){if(state==='playing')pause();else if(state==='paused')resume()}if(e.code==='KeyQ')useShield();if(e.code==='KeyE')playerAttack(true);if(e.code==='KeyF'){if(player&&player.position.z<-20){player.position.z-=4;toast('✦ GUM GRAPPLE!')}}});
 addEventListener('keyup',e=>keys[e.code]=false);
 renderer.domElement.addEventListener('pointerdown',e=>{if(e.pointerType==='mouse'){initAudio();if(e.button===0)playerAttack(false);if(e.button===2)cameraYaw+=0} else if(e.clientX<innerWidth*.42){return}else{camTouch={x:e.clientX,y:e.clientY,id:e.pointerId};try{renderer.domElement.setPointerCapture(e.pointerId)}catch(_){}}});
 renderer.domElement.addEventListener('pointermove',e=>{if(camTouch&&e.pointerId===camTouch.id){cameraYaw-=(e.clientX-camTouch.x)*.008;cameraPitch=THREE.MathUtils.clamp(cameraPitch+(e.clientY-camTouch.y)*.003,-.25,.7);camTouch.x=e.clientX;camTouch.y=e.clientY}});
 renderer.domElement.addEventListener('pointerup',e=>{if(camTouch&&e.pointerId===camTouch.id)camTouch=null});
 renderer.domElement.addEventListener('contextmenu',e=>e.preventDefault());
 $('stickBase').addEventListener('pointerdown',e=>{e.preventDefault();$('stickBase').setPointerCapture(e.pointerId);stickMove(e)});
 $('stickBase').addEventListener('pointermove',e=>{if(e.buttons)stickMove(e)});
 $('stickBase').addEventListener('pointerup',()=>{joy.x=joy.y=0;$('stickKnob').style.transform='translate(0,0)'});
 function stickMove(e){const r=$('stickBase').getBoundingClientRect(),dx=e.clientX-(r.left+r.width/2),dy=e.clientY-(r.top+r.height/2),len=Math.hypot(dx,dy),scale=Math.min(1,48/(len||1));joy.x=dx/48*scale;joy.y=dy/48*scale;$('stickKnob').style.transform=`translate(${dx*scale}px,${dy*scale}px)`}
 $('attackTouch').onclick=()=>playerAttack();$('jumpTouch').onclick=jump;$('dashTouch').onclick=useDash;$('shieldTouch').onclick=useShield;$('specialTouch').onclick=()=>playerAttack(true);$('interactTouch').onclick=()=>{if(player){const target=new THREE.Vector3(0,0,-34);if(player.position.distanceTo(target)<28){player.position.lerp(target,.18);toast('✦ GUM GRAPPLE!')}else toast('Move closer to the glowing grapple anchor!')}};
 $('pauseBtn').onclick=pause;
}
function wireUI(){
 $('startBtn').onclick=startGame;$('continueBtn').onclick=()=>{startGame();toast('Welcome back, Gum Guardian!')};$('resumeBtn').onclick=resume;$('restartBtn').onclick=startGame;$('homeBtn').onclick=goHome;$('victoryHome').onclick=goHome;$('overHome').onclick=goHome;$('retryBtn').onclick=startGame;$('replayBtn').onclick=startGame;
 $('settingsBtn').onclick=()=>openSettings('main');$('pauseSettingsBtn').onclick=()=>openSettings('pause');$('settingsBack').onclick=backSettings;
 $('musicVol').oninput=e=>{musicVolume=+e.target.value;save()};$('sfxVol').oninput=e=>{sfxVolume=+e.target.value;save()};$('effectsToggle').onchange=e=>{effectsOn=e.target.checked;save()};
 $('worldBtn').onclick=()=>showOnly('worldMenu');$('pauseWorldBtn').onclick=()=>showOnly('worldMenu');$('worldBack').onclick=()=>showOnly(state==='paused'?'pauseMenu':'mainMenu');$('meadowBtn').onclick=startGame;
 document.querySelectorAll('[data-locked]').forEach(b=>b.onclick=()=>toast(b.dataset.locked+' unlocks after this prototype level!'));
 $('customBtn').onclick=()=>showOnly('customMenu');$('customBack').onclick=()=>showOnly('mainMenu');document.querySelectorAll('[data-color]').forEach(b=>b.onclick=()=>{armorColor=b.dataset.color;if(player&&playerGlow)playerGlow.color.set(armorColor);if(playerGlow)playerGlow.emissive.set(armorColor);save();toast('GUMI style updated!')});
 $('helpBtn').onclick=()=>alert('DESKTOP\\nWASD / arrows: move\\nMouse: aim / rotate camera\\nLeft click: Bubble Blaster\\nSpace: jump / double jump\\nShift: Gum Dash\\nQ: Bubble Shield\\nE: Mega Bubble (uses energy)\\nF: Gum Grapple near arena\\nEsc: pause\\n\\nMOBILE\\nUse the left joystick to move, drag the right side to look, and tap the action buttons. Collect 20 crystals, defeat bots, then enter the glowing arena.');
}
function boot(){
 loadSave();buildScene();initControls();wireUI();$('hud').style.display='none';$('mobileControls').style.display='none';showOnly('mainMenu');
 addEventListener('resize',()=>{if(!camera||!renderer)return;camera.aspect=innerWidth/innerHeight;camera.updateProjectionMatrix();renderer.setSize(innerWidth,innerHeight);renderer.setPixelRatio(Math.min(devicePixelRatio,1.7))});
 loop();
}
if(!window.THREE){$('mainMenu').innerHTML='<div class="panel"><h2>3D engine could not load</h2><p>Please check your internet connection and reload. This prototype loads Three.js from a CDN.</p></div>'}else boot();
})();
</script>
</body></html>
