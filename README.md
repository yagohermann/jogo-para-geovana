[index.html](https://github.com/user-attachments/files/34650850/index.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="mobile-web-app-capable" content="yes">
<meta name="theme-color" content="#4fb4f0">
<title>Lucky Blocks</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
<style>
:root{--o:#4a1259}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent;-webkit-touch-callout:none;-webkit-user-select:none;user-select:none}
html,body{margin:0;height:100%;overflow:hidden;background:#4fb4f0;overscroll-behavior:none;touch-action:none;color:#fff;font:400 16px 'Press Start 2P','Courier New',monospace}
canvas{position:fixed;left:0;top:0;image-rendering:crisp-edges;image-rendering:pixelated}
.msg,#title h1,#title p,#title small,#hint{text-shadow:.1em 0 var(--o),-.1em 0 var(--o),0 .1em var(--o),0 -.1em var(--o),.1em .1em var(--o),-.1em .1em var(--o),.1em -.1em var(--o),-.1em -.1em var(--o),0 .2em var(--o),.1em .2em var(--o),-.1em .2em var(--o)}
.hx{height:1.5em;width:auto;image-rendering:pixelated}
.beat{animation:beat .8s steps(4) infinite}
@keyframes beat{50%{transform:scale(1.28)}}
@keyframes pop{0%{transform:translateY(30px) scale(.2);opacity:0}60%{transform:translateY(-8px) scale(1.12);opacity:1}100%{transform:none;opacity:1}}
@keyframes bob{50%{transform:translateY(-7px)}}
@keyframes blink{50%{opacity:0}}
#msgs{position:fixed;left:0;right:0;top:calc(env(safe-area-inset-top,0px) + 3vh);display:flex;flex-direction:column;align-items:center;gap:2.2vh;pointer-events:none;z-index:5;font-size:clamp(10px,min(4.4vw,5vh),30px);line-height:1.6;text-align:center}
.msg{display:none}.msg.show{display:block}
.box{display:inline-flex;align-items:center;gap:.6em;opacity:0}
.show .box{animation:pop .9s steps(9) forwards,bob 2.4s ease-in-out .9s infinite}
.m1{color:#ffe45c}.m2{color:#fff;--o:#8a1244}
.btn{font:inherit;color:#7a3b00;background:#ffc61a;border:.2em solid #4a2200;border-radius:.3em;padding:.7em 1.4em;box-shadow:inset 0 .2em 0 #ffe97a,inset 0 -.25em 0 #e08a00,0 .3em 0 #4a2200;cursor:pointer;touch-action:manipulation}
.btn:active{transform:translateY(.25em);box-shadow:inset 0 .2em 0 #ffe97a,inset 0 -.25em 0 #e08a00,0 .05em 0 #4a2200}
#title{position:fixed;left:0;top:0;right:0;bottom:0;z-index:10;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:4vh;padding:0 5vw;text-align:center;background:rgba(60,20,90,.3);transition:opacity .6s}
body:not(.title) #title{opacity:0;visibility:hidden;pointer-events:none;transition:opacity .6s,visibility 0s .6s}
#title h1{margin:0;font-size:clamp(22px,min(10vw,12vh),68px);line-height:1.3;color:#ffe45c}
#title p{margin:0;display:flex;align-items:center;gap:.8em;font-size:clamp(9px,min(3vw,3.4vh),18px);line-height:1.6}
#title small{font-size:clamp(7px,2.1vmin,11px);line-height:2}
#play{font-size:clamp(16px,min(5.5vw,6vh),34px)}
#jump{position:fixed;right:calc(env(safe-area-inset-right,0px) + 4vmin);bottom:calc(env(safe-area-inset-bottom,0px) + 4vmin);width:clamp(88px,25vmin,150px);height:clamp(88px,25vmin,150px);border-radius:50%;font:inherit;font-size:clamp(9px,2.5vmin,15px);color:#7a3b00;background:#ffc61a;border:.4em solid #4a2200;box-shadow:inset 0 .35em 0 #ffe97a,inset 0 -.45em 0 #e08a00,0 .5em 0 #4a2200;display:none;flex-direction:column;align-items:center;justify-content:center;gap:.7em;z-index:6;touch-action:none}
#jump i{width:0;height:0;border:1em solid transparent;border-top:0;border-bottom:1.5em solid #7a3b00}
#jump:active{transform:translateY(.4em);box-shadow:inset 0 .35em 0 #ffe97a,inset 0 -.45em 0 #e08a00,0 .1em 0 #4a2200}
body.play #jump{display:flex}
#hint{position:fixed;left:0;right:0;bottom:calc(env(safe-area-inset-bottom,0px) + 3vmin);text-align:center;font-size:clamp(9px,2.6vmin,16px);z-index:4;display:none;pointer-events:none}
#hint.show{display:block;animation:blink 1s steps(2) infinite}
#again{position:fixed;left:0;right:0;margin:0 auto;width:max-content;bottom:calc(env(safe-area-inset-bottom,0px) + 4vmin);font-size:clamp(10px,3vmin,18px);z-index:7;display:none}
body.again #again{display:block}
@media(prefers-reduced-motion:reduce){.beat,#hint.show{animation:none}.show .box{animation:pop .01s forwards}}
</style>
</head>
<body class="title">
<canvas id="c"></canvas>
<div id="msgs">
<div class="msg m1"><span class="box"><span>FELIZ 1 MÊS<br>DE NAMORO</span></span></div>
<div class="msg m2"><span class="box"><img class="hx beat" alt=""><span>TE AMO GEOVANA<br>SACRAMENTO</span><img class="hx beat" alt=""></span></div>
</div>
<div id="hint"></div>
<button id="jump" aria-label="Pular"><i></i>PULAR</button>
<button id="again" class="btn">JOGAR DE NOVO</button>
<div id="title">
<h1>LUCKY<br>BLOCKS</h1>
<p><img class="hx beat" alt="">uma surpresa para você<img class="hx beat" alt=""></p>
<button id="play" class="btn">JOGAR</button>
<small>NO COMPUTADOR: ESPAÇO PULA<br>NO CELULAR: TOQUE EM PULAR</small>
</div>
<script>
(()=>{
'use strict';
const $=s=>document.querySelector(s),cv=$('#c'),ctx=cv.getContext('2d'),hint=$('#hint');
const BW=24,AL=6,AR=19,SP=52,JV=268,GR=620;
let LW=320,LH=180,GY=130,AC=null;
const rnd=Math.random,pick=a=>a[(rnd()*a.length)|0];
const H=n=>{n=Math.imul((n|0)^((n|0)>>>15),0x2c1b3c6d);n=Math.imul(n^(n>>>12),0x297a2d39);return(n^(n>>>15))>>>0};
const R=(x,y,w,h,c)=>{ctx.fillStyle=c;ctx.fillRect(Math.round(x),Math.round(y),w,h)};
const bump=(cx,cy,r,c)=>{ctx.fillStyle=c;for(let d=-r;d<=r;d++){const w=Math.round(Math.sqrt(r*r-d*d));ctx.fillRect(Math.round(cx-w),Math.round(cy+d),w*2,1)}};
const hx=c=>[1,3,5].map(i=>parseInt(c.substr(i,2),16));
const mix=(a,b,k)=>{const A=hx(a),B=hx(b);return'rgb('+A.map((v,i)=>Math.round(v+(B[i]-v)*k)).join()+')'};
const ease=t=>1+2.70158*Math.pow(t-1,3)+1.70158*Math.pow(t-1,2);

/* ---------- arte ---------- */
const spr=new Image();spr.src='data:image/png;base64,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';
const mk=(w,h,f)=>{const c=document.createElement('canvas');c.width=w;c.height=h;f(c.getContext('2d'));return c};
const px=(g,m,p,s,ox,oy)=>m.forEach((r,y)=>[...r].forEach((ch,x)=>{if(p[ch]){g.fillStyle=p[ch];g.fillRect((ox||0)+x*s,(oy||0)+y*s,s,s)}}));
const HM=['..OOO.OOO..','.OWWRORRRO.','OWRRRRRRRDO','ORRRRRRRRDO','ORRRRRRRRDO','.ORRRRRRDO.','..ORRRRDO..','...ORRRO...','....ORO....','.....O.....'];
const QM=['.XXXXX.','XX...XX','XX...XX','....XX.','...XX..','...XX..','.......','...XX..','...XX..'];
const HP=[{O:'#6b1034',R:'#ff4f86',W:'#ffd2e1',D:'#d92a66'},{O:'#4b1a6b',R:'#b58cff',W:'#ecdcff',D:'#8a5ad8'},{O:'#7a1020',R:'#ff6a5c',W:'#ffd9cf',D:'#d83a3a'}];
const hearts=HP.map(p=>mk(11,10,g=>px(g,HM,p,1)));
const HU=mk(44,40,g=>px(g,HM,HP[0],4)).toDataURL();
document.querySelectorAll('.hx').forEach(i=>i.src=HU);
const blk=[0,1].map(u=>mk(BW,BW,g=>{
 const O=u?'#4a2f1e':'#7a3b00',B=u?'#a9784f':'#ffc61a',L=u?'#c99a6b':'#ffe97a',D=u?'#8a5d3b':'#e08a00';
 g.fillStyle=O;g.fillRect(0,0,BW,BW);
 g.fillStyle=B;g.fillRect(1,1,BW-2,BW-2);
 g.fillStyle=L;g.fillRect(1,1,BW-2,2);g.fillRect(1,1,2,BW-2);
 g.fillStyle=D;g.fillRect(1,BW-3,BW-2,2);g.fillRect(BW-3,1,2,BW-2);
 [[0,0],[BW-1,0],[0,BW-1],[BW-1,BW-1]].forEach(([x,y])=>g.clearRect(x,y,1,1));
 [[4,4],[BW-6,4],[4,BW-6],[BW-6,BW-6]].forEach(([x,y])=>{g.fillStyle=O;g.fillRect(x,y,2,2);g.fillStyle=L;g.fillRect(x,y,1,1)});
 if(!u){px(g,QM,{X:'#a85a00'},1,9,8);px(g,QM,{X:'#fffbe6'},1,8,7)}
}));
const SKY=['#4fb4f0','#62bef3','#76c9f6','#8bd3f8','#a0ddfa','#b5e6fb','#c9eefc','#dcf5fd'];
const DSK=['#5b4aa8','#7d57b8','#a265c2','#c773c4','#e682b8','#ff96a8','#ffb29c','#ffd2a2'];
const FL=['#ff6fa8','#ffffff','#ffd84d','#b58cff','#ff8a5c'];
const COL=['#ffe45c','#ffffff','#ff7fb0','#8be4ff','#ffb347','#b58cff'];
const clouds=Array.from({length:8},(_,i)=>({x:i*83+H(i)%40,f:(i*.137+.06)%.9,s:1+H(i+9)%2,v:2+H(i+3)%4}));

/* ---------- estado ---------- */
const G={mode:'title',t:0,cam:0,shake:0,fl:0,sun:0,stage:1,fw:0,hr:0},g={},blocks=[],P=[],rings=[],Q=[],keys={};
const later=(s,f)=>Q.push({t:G.t+s,f});
const floorAt=()=>{let f=GY;for(const b of blocks)if(b.spawn>=1&&g.x+5>b.x&&g.x-5<b.x+BW&&g.y<=b.top+1&&b.top<f)f=b.top;return f};
function reset(){
 Object.assign(g,{x:36,y:GY,vx:0,vy:0,on:true,ph:0,sq:0,jb:0,co:0,cheer:false,flip:false,nh:1e9});
 blocks.length=P.length=rings.length=Q.length=0;
 blocks.push({id:1,x:150,top:GY-32,spawn:1,hit:false,bump:0});
 Object.assign(G,{cam:0,shake:0,fl:0,sun:0,stage:1});
 document.querySelectorAll('.msg').forEach(e=>e.classList.remove('show'));
 document.body.classList.remove('again');
}
function resize(){
 const d=window.devicePixelRatio||1,w=innerWidth,h=innerHeight,s=Math.max(1,Math.floor(Math.min(w,h)*d/200));
 LW=Math.ceil(w*d/s);LH=Math.ceil(h*d/s);cv.width=LW;cv.height=LH;
 cv.style.width=LW*s/d+'px';cv.style.height=LH*s/d+'px';ctx.imageSmoothingEnabled=false;
 GY=Math.round(LH*.74);blocks.forEach(b=>b.top=GY-32);
 if(g.on)g.y=floorAt();
}
function snd(f,d,type,sl,v,at){try{if(!AC)return;const o=AC.createOscillator(),n=AC.createGain(),t=AC.currentTime+(at||0);o.type=type||'square';o.frequency.setValueAtTime(f,t);if(sl)o.frequency.exponentialRampToValueAtTime(f*sl,t+d);n.gain.setValueAtTime(v||.05,t);n.gain.exponentialRampToValueAtTime(.001,t+d);o.connect(n);n.connect(AC.destination);o.start(t);o.stop(t+d)}catch(e){}}
function burst(x,y,n,gr,cols){for(let i=0;i<n;i++){const a=rnd()*6.283,v=25+rnd()*75;P.push({x,y,vx:Math.cos(a)*v,vy:Math.sin(a)*v-20,l:0,m:.6+rnd()*.7,g:gr,t:i%5?0:2,s:1+((rnd()*2)|0),c:pick(cols||COL)})}}
function love(x,y,n){for(let i=0;i<n;i++)P.push({x,y,vx:(rnd()-.5)*70,vy:-45-rnd()*45,l:0,m:1.5,g:90,t:1,h:(rnd()*3)|0,z:1})}

/* ---------- regras do jogo ---------- */
function activate(b){
 b.hit=true;b.bump=1;G.shake=1;G.fl=.7;
 const cx=b.x+BW/2;
 g.x=Math.min(Math.max(g.x,b.x+8),b.x+BW-8);
 burst(cx,b.top,30,260);love(cx,b.top-4,7);rings.push({x:cx,y:b.top+BW/2,t:0});
 [523,659,784,1047].forEach((f,i)=>snd(f,.14,'square',1,.05,i*.07));
 if(b.id===1){
  g.vy=-120;g.on=false;G.mode='hold';$('.m1').classList.add('show');
  later(.7,spawn2);later(1.2,()=>{G.mode='play';G.stage=2});
 }else final();
}
function spawn2(){
 const a=blocks[0],b={id:2,x:a.x+BW+130,top:GY-32,spawn:0,hit:false,bump:0};
 blocks.push(b);burst(b.x+BW/2,b.top+BW/2,20,60);rings.push({x:b.x+BW/2,y:b.top+BW/2,t:0});snd(880,.12,'triangle',1.5);
}
function final(){
 G.mode='end';g.cheer=true;g.nh=G.t+.3;G.fw=.2;G.hr=0;
 document.body.className='end';$('.m2').classList.add('show');
 [523,659,784,1047,1319,1568].forEach((f,i)=>snd(f,.2,'triangle',1,.06,.2+i*.09));
 later(5,()=>document.body.classList.add('again'));
}
function phys(dt){
 const play=G.mode==='play',sp=SP*(keys.run?1.45:1);
 g.vx=play?(g.on?sp:sp*.6):0;
 g.jb=Math.max(0,g.jb-dt);g.co=g.on?.1:Math.max(0,g.co-dt);
 if(play&&g.jb>0&&g.co>0){g.vy=-JV;g.on=false;g.co=g.jb=0;snd(280,.22,'square',2.4)}
 if(G.mode==='end'&&g.on&&G.t>g.nh){g.vy=-135;g.on=false;g.flip=!g.flip;g.nh=G.t+.55}
 let nx=g.x+g.vx*dt;
 for(const b of blocks)if(b.spawn>=1&&nx+7>b.x&&nx-7<b.x+BW&&g.y>b.top+1&&g.y-44<b.top+BW)nx=g.x<b.x+BW/2?b.x-7:b.x+BW+7;
 g.x=nx;
 g.vy+=GR*dt;const py=g.y;let ny=py+g.vy*dt,hit=null;
 for(const b of blocks)if(b.spawn>=1&&g.x+5>b.x&&g.x-5<b.x+BW&&g.vy>=0&&py<=b.top+1&&ny>=b.top){ny=b.top;hit=b}
 const land=hit||ny>=GY;
 if(!hit&&ny>=GY)ny=GY;
 if(land){if(g.vy>70)g.sq=1;g.vy=0}
 g.on=!!land;g.y=ny;g.sq=Math.max(0,g.sq-dt*7);
 if(g.on&&g.vx>1)g.ph+=dt*11;
 if(hit&&!hit.hit&&play)activate(hit);
}
function update(dt){
 G.t+=dt;
 for(let i=Q.length-1;i>=0;i--)if(G.t>=Q[i].t){const f=Q[i].f;Q.splice(i,1);f()}
 G.shake=Math.max(0,G.shake-dt*4);G.fl=Math.max(0,G.fl-dt*2.2);
 blocks.forEach(b=>{b.spawn=Math.min(1,b.spawn+dt*2.2);b.bump=Math.max(0,b.bump-dt*3)});
 phys(dt);
 if(G.mode==='end'){
  G.sun=Math.min(1,G.sun+dt*.3);
  if((G.fw-=dt)<=0){G.fw=.5+rnd()*.5;burst(G.cam+30+rnd()*(LW-60),15+rnd()*GY*.4,24,110)}
  if((G.hr-=dt)<=0){G.hr=.16;P.push({x:G.cam+rnd()*LW,y:-8,vx:0,vy:28+rnd()*30,g:0,l:0,m:10,t:1,h:(rnd()*3)|0,z:rnd()<.3?2:1,sw:1+rnd()*5})}
 }
 for(let i=P.length-1;i>=0;i--){const p=P[i];p.l+=dt;if(p.l>p.m){P.splice(i,1);continue}p.vy+=p.g*dt;p.x+=p.vx*dt+(p.sw?Math.sin(p.l*3+p.sw)*14*dt:0);p.y+=p.vy*dt}
 for(let i=rings.length-1;i>=0;i--){rings[i].t+=dt*1.4;if(rings[i].t>.75)rings.splice(i,1)}
 const tx=Math.max(0,g.x-LW*(G.mode==='end'?.5:.3));G.cam+=(tx-G.cam)*Math.min(1,dt*4);
 const tb=blocks[G.stage-1];
 hint.classList.toggle('show',!!(G.mode==='play'&&tb&&tb.spawn>=1&&!tb.hit&&g.on&&tb.x-g.x<70&&tb.x+BW>g.x));
}

/* ---------- desenho ---------- */
function hill(cam,p,b,a,s,c1,c2){for(let x=0;x<LW;x+=2){const w=x+cam*p,h=b+Math.round((Math.sin(w*.021+s)*a+Math.sin(w*.057+s*2)*a*.4)/2)*2;R(x,GY-h,2,h,c1);R(x,GY-h,2,2,c2)}}
function drawGirl(cam){
 if(!spr.complete||!spr.naturalWidth)return;
 const walk=g.on&&g.vx>1,s=Math.sin(g.ph);
 let bob=0,lL=0,lR=0,sw=0,up=0;
 if(walk){bob=Math.abs(s)>.7?-1:0;lL=Math.max(0,s)*3;lR=Math.max(0,-s)*3;sw=s*2.4}
 else if(!g.on){lL=4;lR=2;up=.7}
 else bob=Math.sin(G.t*3)>.6?-1:0;
 if(g.cheer)up=1;
 const ox=Math.round(g.x-cam-14),fy=Math.round(g.y),oy=fy-55,b=bob+Math.round(g.sq*2),top=oy+b+43;
 ctx.save();
 if(g.flip){ctx.translate(2*ox+28,0);ctx.scale(-1,1)}
 ctx.drawImage(spr,0,0,28,24,ox,oy+b,28,24);
 ctx.drawImage(spr,AL,24,AR-AL,19,ox+AL,oy+b+24,AR-AL,19);
 for(let r=24;r<43;r++){
  const t=(r-24)/18,o=Math.round(up*2*(.4+t)),dy=-Math.round(up*4),a=Math.round(sw*t);
  ctx.drawImage(spr,0,r,AL,1,ox+a-o,oy+b+r+dy,AL,1);
  ctx.drawImage(spr,AR,r,28-AR,1,ox+AR-a+o,oy+b+r+dy,28-AR,1);
 }
 ctx.drawImage(spr,0,43,13,10,ox,top,13,fy-Math.round(lL)-top);
 ctx.drawImage(spr,13,43,15,12,ox+13,top,15,fy-Math.round(lR)-top);
 ctx.restore();
}
function draw(){
 const cam=Math.round(G.cam),k=G.sun,t=G.t;
 ctx.save();
 if(G.shake>0)ctx.translate(Math.round((rnd()-.5)*G.shake*4),Math.round((rnd()-.5)*G.shake*4));
 const bh=Math.ceil(GY/8);
 for(let i=0;i<8;i++)R(-6,i*bh,LW+12,bh+1,mix(SKY[i],DSK[i],k));
 const sx=LW*.78,sy=GY*.2+k*GY*.45;
 ctx.globalAlpha=.25;bump(sx,sy,21,'#fff');ctx.globalAlpha=1;bump(sx,sy,13,mix('#fff4a8','#ff9a6a',k));
 const W2=LW+140,cw=mix('#ffffff','#ffd0e4',k),cs=mix('#d3e9f7','#d99ac8',k);
 clouds.forEach(c=>{const x=(((c.x-cam*.1+t*c.v)%W2)+W2)%W2-70,y=10+c.f*(GY-90),u=2*c.s;[[3,0,5],[1,1,9],[0,2,11],[1,3,9]].forEach((r,i)=>R(x+r[0]*u,y+r[1]*u,r[2]*u,u,i==3?cs:cw))});
 hill(cam,.15,38,14,1,mix('#a6dcb0','#b79ad0',k),mix('#c0ecc6','#d3b6e6',k));
 hill(cam,.3,18,8,4,mix('#79cc86','#9a78b8',k),mix('#95e09c','#b496d0',k));
 for(let i=Math.floor(cam*.5/140)-1;i<(cam*.5+LW)/140+1;i++){
  const x=i*140+H(i)%50-cam*.5;
  R(x+5,GY-20,4,20,'#7a4a2a');bump(x+7,GY-28,11,'#2f9a45');bump(x+2,GY-23,8,'#2f9a45');bump(x+13,GY-23,8,'#2f9a45');bump(x+5,GY-31,6,'#46b85a');bump(x+11,GY-27,4,'#62d06e');
 }
 R(0,GY,LW,LH-GY,'#8a5a33');
 const cm=((cam%8)+8)%8,c8=Math.floor(cam/8);
 for(let j=0;j<=(LH-GY)/8;j++)for(let i=-1;i<=LW/8;i++){const h=H((i+c8)*31+j*17);if(h%4==0)R(i*8-cm+(h>>>5)%6,GY+18+j*8+(h>>>9)%5,2,2,'#6e4425')}
 R(0,GY,LW,14,'#5fc840');R(0,GY+14,LW,3,'#2f9a3a');
 for(let i=-1;i<=LW/8;i++)if((i+c8)%2==0)R(i*8-cm,GY+3,8,11,'#69d04a');
 R(0,GY,LW,1,'#9af06a');
 for(let w=Math.ceil(cam/3)*3;w<cam+LW;w+=3)if(H(w)%7==0)R(w-cam,GY-2,1,2,'#5fc840');
 for(let i=Math.floor(cam/14)-1;i<(cam+LW)/14+1;i++){
  const x=i*14+H(i)%12-cam,y=GY+4+H(i*3)%9,c=FL[H(i*5)%5];
  R(x+1,y,1,3,'#2f9a3a');R(x+1,y-3,1,1,c);R(x,y-2,3,1,c);R(x+1,y-1,1,1,c);R(x+1,y-2,1,1,'#ffe14d');
 }
 for(let i=Math.floor(cam/90)-1;i<(cam+LW)/90+1;i++){
  const x=i*90+H(i+7)%40-cam,w=22+H(i)%12;
  [[6,6,7],[w-6,6,7],[w/2,9,9]].forEach(([a,b,r])=>{bump(x+a,GY-b,r,'#2e8b3e');bump(x+a-1,GY-b-1,r-2,'#43b04e');bump(x+a-2,GY-b-3,2,'#8be470')});
  if(H(i)%3==0){R(x+w/2,GY-10,2,2,'#ff5d8f');R(x+w/2-6,GY-6,2,2,'#ff5d8f')}
 }
 blocks.forEach(b=>{
  const sc=b.spawn<1?ease(b.spawn):1,s=Math.round(BW*sc),bx=b.x-cam+BW/2,bob=b.hit?0:Math.round(Math.sin(t*3+b.id)*2),by=b.top+bob-Math.round(Math.sin(b.bump*Math.PI)*6);
  if(s<1)return;
  ctx.globalAlpha=.2;R(b.x-cam+3,GY-1,BW-6,2,'#000');ctx.globalAlpha=1;
  ctx.drawImage(blk[b.hit?1:0],Math.round(bx-s/2),Math.round(by+BW/2-s/2),s,s);
  if(!b.hit&&sc==1&&Math.sin(t*5+b.id*2)>.85){const x=bx+8,y=by+1;R(x,y-2,1,5,'#fff');R(x-2,y,5,1,'#fff')}
 });
 const fl=floorAt(),shw=Math.max(8,16-(fl-g.y)*.1);
 ctx.globalAlpha=.2;R(g.x-cam-shw/2,fl-1,shw,2,'#000');ctx.globalAlpha=1;
 drawGirl(cam);
 rings.forEach(r=>{const rad=4+r.t*70;ctx.globalAlpha=Math.max(0,1-r.t*1.4);for(let a=0;a<6.28;a+=.12)R(r.x-cam+Math.cos(a)*rad,r.y+Math.sin(a)*rad,2,2,'#fff7b0');ctx.globalAlpha=1});
 P.forEach(p=>{
  ctx.globalAlpha=Math.max(0,Math.min(1,(p.m-p.l)*2.5));const x=p.x-cam;
  if(p.t==1){const z=p.z;ctx.drawImage(hearts[p.h],Math.round(x-5*z),Math.round(p.y-5*z),11*z,10*z)}
  else if(p.t==2){R(x,p.y-2,1,5,p.c);R(x-2,p.y,5,1,p.c)}
  else R(x,p.y,p.s,p.s,p.c);
 });
 ctx.globalAlpha=1;
 if(k>0){ctx.globalAlpha=.12*k;R(-6,-6,LW+12,LH+12,'#ff5fa0');ctx.globalAlpha=1}
 if(G.fl>0){ctx.globalAlpha=G.fl*.6;R(-6,-6,LW+12,LH+12,'#fff');ctx.globalAlpha=1}
 ctx.restore();
}

/* ---------- controles ---------- */
const press=()=>{g.jb=.12};
function start(){
 if(G.mode!=='title'&&!(G.mode==='end'&&document.body.classList.contains('again')))return;
 try{AC=AC||new(window.AudioContext||window.webkitAudioContext)();AC.resume()}catch(e){}
 reset();G.mode='intro';document.body.className='play';
 later(.6,()=>{G.mode='play'});
}
$('#play').onclick=start;$('#again').onclick=start;
cv.addEventListener('pointerdown',e=>{e.preventDefault();press()});
$('#jump').addEventListener('pointerdown',e=>{e.preventDefault();press()});
addEventListener('keydown',e=>{
 const c=e.code;
 if(c==='Space'||c==='ArrowUp'||c==='KeyW'){e.preventDefault();if(!e.repeat)press()}
 else if(c==='ArrowRight'||c==='KeyD'){keys.run=true;e.preventDefault()}
 else if(c==='Enter'&&!e.repeat){e.preventDefault();start()}
});
addEventListener('keyup',e=>{if(e.code==='ArrowRight'||e.code==='KeyD')keys.run=false});
addEventListener('resize',resize);
addEventListener('orientationchange',()=>setTimeout(resize,250));
if(window.visualViewport)visualViewport.addEventListener('resize',resize);
document.addEventListener('gesturestart',e=>e.preventDefault());
document.addEventListener('contextmenu',e=>e.preventDefault());
hint.textContent=matchMedia('(pointer:coarse)').matches?'TOQUE EM PULAR':'APERTE ESPAÇO';
let last=0;
function loop(ts){const dt=Math.min(.05,(ts-last)/1000||0);last=ts;update(dt);draw();requestAnimationFrame(loop)}
reset();resize();requestAnimationFrame(loop);
})();
</script>
</body>
</html>
