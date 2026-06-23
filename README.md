<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Mathe Casino</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet"/>
<style>
*{box-sizing:border-box;margin:0;padding:0;}
:root{
  --felt:#0D2B1F;--felt-l:#133728;--gold:#C9A84C;--gold-l:#E8C96A;
  --ivory:#F5F0E8;--red:#B03030;--blue:#1B4F8A;--text:#E8DFC8;--dim:#8A7D60;
}
body{background:var(--felt);font-family:'Inter',sans-serif;color:var(--text);min-height:100vh;}
/* Header */
.hdr{background:var(--felt);border-bottom:2px solid var(--gold);padding:14px 20px;display:flex;align-items:center;gap:12px;position:sticky;top:0;z-index:10;}
.hdr-title{font-family:'Playfair Display',serif;font-size:20px;font-weight:900;color:var(--gold);letter-spacing:2px;text-transform:uppercase;}
.hdr-sub{font-size:11px;color:var(--dim);letter-spacing:1px;}
.chips{margin-left:auto;background:var(--felt-l);border:1px solid var(--gold);border-radius:20px;padding:5px 14px;font-size:14px;font-weight:700;color:var(--gold);}
/* Nav */
.nav{display:flex;background:var(--felt-l);border-bottom:1px solid #C9A84C33;}
.nav-btn{flex:1;padding:13px 6px;background:none;border:none;cursor:pointer;font-family:'Inter',sans-serif;font-size:13px;font-weight:600;color:var(--dim);border-bottom:3px solid transparent;transition:all .2s;-webkit-tap-highlight-color:transparent;}
.nav-btn.active{color:var(--gold);border-bottom-color:var(--gold);background:var(--felt);}
/* Content */
.content{max-width:620px;margin:0 auto;padding:18px 14px;}
/* Panel */
.panel{background:var(--felt-l);border:1px solid #C9A84C33;border-radius:12px;padding:18px;margin-bottom:14px;}
.p-title{font-family:'Playfair Display',serif;font-size:18px;color:var(--gold);margin-bottom:3px;}
.p-sub{font-size:12px;color:var(--dim);margin-bottom:14px;}
/* Buttons */
.btn-g{background:linear-gradient(135deg,var(--gold),var(--gold-l));color:#1a1000;border:none;border-radius:8px;padding:12px 22px;font-weight:700;font-size:14px;cursor:pointer;letter-spacing:.5px;transition:transform .1s,box-shadow .1s;-webkit-tap-highlight-color:transparent;}
.btn-g:hover{transform:translateY(-1px);box-shadow:0 4px 16px #C9A84C44;}
.btn-g:active{transform:translateY(0);}
.btn-g:disabled{opacity:.45;cursor:default;transform:none;}
.btn-o{background:none;border:1px solid #C9A84C66;color:var(--gold);border-radius:8px;padding:10px 18px;font-size:13px;font-weight:600;cursor:pointer;transition:all .2s;-webkit-tap-highlight-color:transparent;}
.btn-o:hover{background:#C9A84C11;}
/* Insight */
.insight{background:#0a1f16;border-left:3px solid var(--gold);border-radius:0 8px 8px 0;padding:12px 16px;margin-top:14px;font-size:13px;line-height:1.65;color:var(--text);}
.insight strong{color:var(--gold);}
.formula{background:#0a1f16;border:1px solid #C9A84C33;border-radius:8px;padding:9px 13px;font-family:monospace;font-size:13px;color:var(--gold-l);margin:8px 0;letter-spacing:.5px;}
/* Stats */
.stat-row{display:flex;gap:10px;margin:12px 0;flex-wrap:wrap;}
.stat-box{flex:1;min-width:70px;background:#0a1f16;border-radius:8px;padding:10px;text-align:center;}
.stat-num{font-size:22px;font-weight:700;color:var(--gold);}
.stat-lbl{font-size:10px;color:var(--dim);margin-top:2px;text-transform:uppercase;letter-spacing:.5px;}
/* Result badge */
.badge{display:inline-flex;align-items:center;gap:6px;padding:6px 14px;border-radius:99px;font-weight:700;font-size:13px;margin:8px 0;}
.win{background:#1a4a1a;color:#5eda5e;border:1px solid #5eda5e44;}
.lose{background:#4a1a1a;color:#f07070;border:1px solid #f0707044;}
/* Progress */
.prog{background:#0a1f16;border-radius:99px;height:8px;overflow:hidden;margin:6px 0;}
.prog-fill{height:100%;background:linear-gradient(90deg,var(--gold),var(--gold-l));border-radius:99px;transition:width .5s;}
/* Dice */
.dice-row{display:flex;gap:16px;justify-content:center;margin:18px 0;}
.die{width:68px;height:68px;background:var(--ivory);border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:38px;box-shadow:0 4px 12px #00000066;transition:transform .2s;}
@keyframes roll{0%,100%{transform:rotate(0)}25%{transform:rotate(-15deg)}75%{transform:rotate(15deg)}}
.rolling{animation:roll .4s ease;}
/* Sum buttons */
.sum-grid{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:14px;}
.sum-btn{width:38px;height:38px;border-radius:8px;border:none;cursor:pointer;font-weight:700;font-size:13px;transition:all .15s;-webkit-tap-highlight-color:transparent;}
/* Hist bars */
.hist-wrap{margin-top:12px;}
.hist-row{display:flex;align-items:center;gap:8px;margin-bottom:5px;}
.hist-n{width:18px;text-align:right;font-size:11px;color:var(--dim);}
.hist-bars{flex:1;display:flex;flex-direction:column;gap:1px;}
.hb{height:7px;border-radius:3px;min-width:2px;transition:width .4s;}
.hist-pct{font-size:10px;color:var(--dim);width:56px;text-align:right;}
/* Roulette */
.board{display:grid;grid-template-columns:repeat(6,1fr);gap:4px;margin:10px 0;}
.cell{aspect-ratio:1;border-radius:6px;display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;cursor:pointer;transition:transform .15s,box-shadow .15s;border:2px solid transparent;-webkit-tap-highlight-color:transparent;}
.cell:hover{transform:scale(1.08);}
.cell.sel{border-color:var(--gold);box-shadow:0 0 8px #C9A84C88;}
@keyframes flash{0%,100%{opacity:1}50%{opacity:.25}}
.cell.flash{animation:flash .5s ease;}
.r{background:var(--red);color:#fff;}
.b{background:#1a1a1a;color:#fff;}
.g{background:#2d6a2d;color:#fff;}
/* Color bet */
.col-choice{display:flex;gap:10px;margin:14px 0;}
.col-btn{flex:1;height:60px;border-radius:10px;cursor:pointer;border:3px solid transparent;display:flex;align-items:center;justify-content:center;font-size:14px;font-weight:700;color:#fff;transition:all .2s;-webkit-tap-highlight-color:transparent;}
/* Dozen bet */
.doz-row{display:flex;gap:8px;margin:14px 0;}
.doz-btn{flex:1;height:56px;border-radius:10px;cursor:pointer;background:#0a1f16;display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;transition:all .2s;-webkit-tap-highlight-color:transparent;}
/* Cards */
.card-disp{display:flex;gap:8px;justify-content:center;flex-wrap:wrap;margin:14px 0;}
.card{width:54px;height:78px;background:var(--ivory);border-radius:8px;display:flex;flex-direction:column;align-items:center;justify-content:center;font-weight:700;color:#222;box-shadow:0 2px 8px #00000066;border:1px solid #ccc;}
.card.cr{color:var(--red);}
.card.back{background:#1B4F8A;}
.bet-opt{display:flex;align-items:center;justify-content:space-between;padding:10px 14px;border-radius:8px;margin-bottom:6px;cursor:pointer;transition:all .2s;-webkit-tap-highlight-color:transparent;}
.current-p{background:#0a1f16;border-radius:8px;padding:10px 14px;margin-bottom:12px;}
.row2{display:flex;gap:10px;margin-top:10px;}
</style>
</head>
<body>
<div class="hdr">
  <div>
    <div class="hdr-title">Mathe Casino</div>
    <div class="hdr-sub">Wahrscheinlichkeiten entdecken</div>
  </div>
  <div class="chips" id="chipDisplay">🟡 50 Chips</div>
</div>
<nav class="nav">
  <button class="nav-btn active" onclick="showTab('dice',this)">🎲 Würfel</button>
  <button class="nav-btn" onclick="showTab('roulette',this)">🎡 Roulette</button>
  <button class="nav-btn" onclick="showTab('cards',this)">🃏 Karten</button>
</nav>
<div class="content">
  <!-- DICE -->
  <div id="tab-dice">
    <div class="panel">
      <div class="p-title">🎲 Zwei Würfel</div>
      <div class="p-sub">Tippe eine Summe – dann würfle. Warum ist die 7 so mächtig?</div>
      <div class="dice-row">
        <div class="die" id="d1">?</div>
        <div class="die" id="d2">?</div>
      </div>
      <div style="font-size:12px;color:var(--dim);margin-bottom:8px;">Setze auf eine Summe (1 Chip):</div>
      <div class="sum-grid" id="sumBtns"></div>
      <div id="diceResult" style="min-height:32px;"></div>
      <button class="btn-g" id="rollBtn" onclick="rollDice()" disabled>Würfeln – wähle erst eine Summe</button>
    </div>
    <div class="panel" id="diceStats" style="display:none;">
      <div style="font-size:14px;font-weight:600;margin-bottom:10px;" id="rollCount">Nach 0 Würfen:</div>
      <div class="hist-wrap" id="histWrap"></div>
    </div>
    <div class="insight">
      <strong>Warum gewinnt die Bank?</strong><br/>
      Die Summe <strong>7</strong> kann auf 6 von 36 Wegen entstehen – Wahrscheinlichkeit <strong>1/6 ≈ 16,7 %</strong>. Bei einem fairen Spiel müsste die Auszahlung 5:1 sein. Im echten Casino zahlt die Bank aber nur 4:1 → Hausvorteil ~16 %.
      <div class="formula">P(Summe = 7) = 6/36 = 1/6 ≈ 16,7 %</div>
    </div>
  </div>

  <!-- ROULETTE -->
  <div id="tab-roulette" style="display:none;">
    <div class="panel">
      <div class="p-title">🎡 Roulette</div>
      <div class="p-sub">Erkunde, wie das Null-Feld die Bank reich macht.</div>
      <div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:14px;">
        <button class="btn-g" style="font-size:12px;padding:8px 12px;" onclick="setRoulBet('number',this)" id="rb-number">Einzelne Zahl (35:1)</button>
        <button class="btn-o" style="font-size:12px;padding:8px 12px;" onclick="setRoulBet('color',this)" id="rb-color">Farbe (1:1)</button>
        <button class="btn-o" style="font-size:12px;padding:8px 12px;" onclick="setRoulBet('dozen',this)" id="rb-dozen">Dutzend (2:1)</button>
      </div>
      <div id="roulBetArea"></div>
      <div id="roulResult" style="min-height:32px;"></div>
      <button class="btn-g" id="spinBtn" onclick="spinRoulette()" disabled>Drehen 🎡</button>
    </div>
    <div class="panel" id="roulStats" style="display:none;">
      <div style="font-size:13px;font-weight:600;margin-bottom:8px;" id="roulSpinCount"></div>
      <div class="stat-row">
        <div class="stat-box"><div class="stat-num" id="rs-red" style="color:var(--red);">0</div><div class="stat-lbl">Rot</div></div>
        <div class="stat-box"><div class="stat-num" id="rs-black" style="color:#aaa;">0</div><div class="stat-lbl">Schwarz</div></div>
        <div class="stat-box"><div class="stat-num" id="rs-green" style="color:#5da85d;">0</div><div class="stat-lbl">Grün (0)</div></div>
      </div>
    </div>
    <div class="insight">
      <strong>Der Null-Trick:</strong><br/>
      Ohne die 0 wäre Rot/Schwarz ein faires 50/50-Spiel. Die Null macht aus 50 % genau <strong>18/37 ≈ 48,6 %</strong>. Dieser kleine Unterschied ist der Hausvorteil – langfristig verliert jeder Spieler ~2,7 % seines Einsatzes pro Runde.
      <div class="formula">P(Rot) = 18/37 ≈ 48,6 % &nbsp;&nbsp; Hausvorteil = 1/37 ≈ 2,7 %</div>
    </div>
  </div>

  <!-- CARDS -->
  <div id="tab-cards" style="display:none;">
    <div class="panel">
      <div class="p-title">🃏 Karten ziehen</div>
      <div class="p-sub">Wie ändert sich die Wahrscheinlichkeit nach jedem Zug?</div>
      <div style="font-size:12px;color:var(--dim);margin-bottom:6px;">Deine Wette:</div>
      <div id="cardBetArea"></div>
      <div id="cardProbArea"></div>
      <div class="card-disp" id="drawnCards"></div>
      <div id="cardResult" style="min-height:32px;"></div>
      <div class="row2">
        <button class="btn-g" id="drawBtn" onclick="drawCard()" disabled style="flex:1;">Karte ziehen</button>
        <button class="btn-o" onclick="resetDeck()">Neu mischen</button>
      </div>
      <div id="deckEmpty" style="display:none;text-align:center;margin-top:10px;font-size:13px;color:var(--dim);">Stapel leer – neu mischen!</div>
    </div>
    <div class="panel" id="cardStats" style="display:none;">
      <div class="stat-row">
        <div class="stat-box"><div class="stat-num" id="cs-win">0</div><div class="stat-lbl">Gewonnen</div></div>
        <div class="stat-box"><div class="stat-num" id="cs-lose">0</div><div class="stat-lbl">Verloren</div></div>
        <div class="stat-box"><div class="stat-num" id="cs-pct" style="color:var(--gold);">–</div><div class="stat-lbl">Trefferquote</div></div>
      </div>
    </div>
    <div class="insight">
      <strong>Bedingte Wahrscheinlichkeit:</strong><br/>
      Jede gezogene Karte <em>verändert</em> die Wahrscheinlichkeit für die nächste. Das ist <strong>bedingte Wahrscheinlichkeit</strong> – ziehst du ein Ass, sinkt P(nächstes Ass) von 4/52 auf 3/51. Beim Kartenzählen im Blackjack nutzt man genau das aus.
      <div class="formula">P(Ass | 1 Ass gezogen) = 3/51 ≈ 5,9 %</div>
    </div>
  </div>
</div>

<script>
// ── State ──────────────────────────────────────────────────────────────────────
let totalChips = 50;
const DICE_FACES = ["⚀","⚁","⚂","⚃","⚄","⚅"];
const THEORY = {2:1,3:2,4:3,5:4,6:5,7:6,8:5,9:4,10:3,11:2,12:1};
const RED_NUMS = new Set([1,3,5,7,9,12,14,16,18,19,21,23,25,27,30,32,34,36]);

// Dice
let diceBet = null;
let diceHistory = [];
let diceRolls = 0;

// Roulette
let roulBetType = "number";
let roulSelected = null;
let roulStats = {red:0,black:0,green:0,total:0};

// Cards
const SUITS = ["♠","♥","♦","♣"];
const VALUES = ["A","2","3","4","5","6","7","8","9","10","J","Q","K"];
let deck = [];
let drawnCards = [];
let cardBet = null;
let cardStats = {wins:0,total:0};

const CARD_BETS = [
  {key:"ace",label:"Nächste = Ass",p:"4/52 ≈ 7,7 %",payout:10},
  {key:"face",label:"Nächste = Bild (J/Q/K)",p:"12/52 ≈ 23 %",payout:3},
  {key:"red",label:"Nächste = Rot",p:"26/52 = 50 %",payout:1},
];

// ── Chips ──────────────────────────────────────────────────────────────────────
function changeChips(d){
  totalChips = Math.max(0, totalChips + d);
  document.getElementById("chipDisplay").textContent = "🟡 " + totalChips + " Chips";
}

// ── Tab navigation ─────────────────────────────────────────────────────────────
function showTab(name, btn) {
  ["dice","roulette","cards"].forEach(t => {
    document.getElementById("tab-"+t).style.display = t===name?"":"none";
  });
  document.querySelectorAll(".nav-btn").forEach(b => b.classList.remove("active"));
  btn.classList.add("active");
}

// ── DICE ───────────────────────────────────────────────────────────────────────
(function initDice(){
  const wrap = document.getElementById("sumBtns");
  for(let n=2;n<=12;n++){
    const b = document.createElement("button");
    b.className = "sum-btn";
    b.textContent = n;
    b.id = "sb-"+n;
    b.style.background = "#0a1f16";
    b.style.color = "var(--text)";
    b.onclick = () => selectSum(n);
    wrap.appendChild(b);
  }
})();

function selectSum(n){
  diceBet = n;
  for(let i=2;i<=12;i++){
    const b = document.getElementById("sb-"+i);
    b.style.background = i===n ? "var(--gold)" : "#0a1f16";
    b.style.color = i===n ? "#1a1000" : "var(--text)";
  }
  const btn = document.getElementById("rollBtn");
  btn.disabled = false;
  btn.textContent = "Würfeln (Einsatz: "+n+")";
}

function rollDice(){
  if(diceBet===null||totalChips<=0) return;
  const d1el = document.getElementById("d1");
  const d2el = document.getElementById("d2");
  d1el.classList.add("rolling"); d2el.classList.add("rolling");
  document.getElementById("diceResult").innerHTML="";
  setTimeout(()=>{
    const d1=Math.ceil(Math.random()*6), d2=Math.ceil(Math.random()*6);
    const sum=d1+d2;
    d1el.textContent=DICE_FACES[d1-1]; d2el.textContent=DICE_FACES[d2-1];
    d1el.classList.remove("rolling"); d2el.classList.remove("rolling");
    diceRolls++;
    diceHistory.push(sum);
    if(diceHistory.length>60) diceHistory.shift();
    const won = diceBet===sum;
    const payout = Math.round(36/THEORY[diceBet]-1);
    const delta = won ? payout : -1;
    changeChips(delta);
    document.getElementById("diceResult").innerHTML =
      `<span class="badge ${won?"win":"lose"}">${won?"✓ Gewonnen! +"+payout+" Chips":"✗ Verloren – Summe war "+sum}</span>`;
    renderDiceStats();
  },400);
}

function renderDiceStats(){
  const panel = document.getElementById("diceStats");
  panel.style.display="";
  document.getElementById("rollCount").textContent="Nach "+diceRolls+" Würfen:";
  const countMap={};
  diceHistory.forEach(s=>{countMap[s]=(countMap[s]||0)+1;});
  const wrap = document.getElementById("histWrap");
  wrap.innerHTML="";
  for(let n=2;n<=12;n++){
    const obs=countMap[n]||0;
    const theoP=THEORY[n]/36;
    const obsP=diceRolls>0?obs/diceRolls:0;
    const row=document.createElement("div");
    row.className="hist-row";
    row.innerHTML=`<div class="hist-n">${n}</div>
      <div class="hist-bars" style="flex:1;">
        <div class="hb" style="width:${Math.min(obsP*100*1.8,100)}%;background:var(--gold);"></div>
        <div class="hb" style="width:${Math.min(theoP*100*1.8,100)}%;background:#C9A84C33;"></div>
      </div>
      <div class="hist-pct">${obs}× / ${(theoP*100).toFixed(1)}%</div>`;
    wrap.appendChild(row);
  }
  const legend=document.createElement("div");
  legend.style.cssText="font-size:11px;color:var(--dim);margin-top:4px;";
  legend.textContent="🟡 Beobachtet  🔲 Theoretisch";
  wrap.appendChild(legend);
}

// ── ROULETTE ───────────────────────────────────────────────────────────────────
function cellClass(n){ return n===0?"g":RED_NUMS.has(n)?"r":"b"; }

function setRoulBet(type, btn){
  roulBetType=type; roulSelected=null;
  ["number","color","dozen"].forEach(k=>{
    const b=document.getElementById("rb-"+k);
    if(k===type){b.className="btn-g";b.style.fontSize="12px";b.style.padding="8px 12px";}
    else{b.className="btn-o";b.style.fontSize="12px";b.style.padding="8px 12px";}
  });
  document.getElementById("spinBtn").disabled=true;
  document.getElementById("roulResult").innerHTML="";
  renderRoulBetArea();
}

function renderRoulBetArea(){
  const area=document.getElementById("roulBetArea");
  area.innerHTML="";
  if(roulBetType==="number"){
    const board=document.createElement("div"); board.className="board";
    for(let n=0;n<=36;n++){
      const c=document.createElement("div");
      c.className="cell "+cellClass(n); c.id="rc-"+n; c.textContent=n;
      c.onclick=()=>selectRoulNum(n);
      board.appendChild(c);
    }
    area.appendChild(board);
  } else if(roulBetType==="color"){
    const row=document.createElement("div"); row.className="col-choice";
    ["red","black"].forEach(col=>{
      const d=document.createElement("div"); d.className="col-btn";
      d.style.background=col==="red"?"var(--red)":"#111";
      d.id="rc-"+col;
      d.textContent=col==="red"?"🔴 Rot":"⚫ Schwarz";
      d.onclick=()=>selectRoulColor(col);
      row.appendChild(d);
    });
    area.appendChild(row);
  } else {
    const row=document.createElement("div"); row.className="doz-row";
    [1,2,3].forEach(d=>{
      const el=document.createElement("div"); el.className="doz-btn";
      el.style.border="3px solid #C9A84C22"; el.style.color="var(--dim)";
      el.id="rd-"+d;
      el.textContent=(d-1)*12+1+"–"+d*12;
      el.onclick=()=>selectRoulDozen(d);
      row.appendChild(el);
    });
    area.appendChild(row);
  }
}

function selectRoulNum(n){
  roulSelected=n;
  document.querySelectorAll(".cell").forEach(c=>c.classList.remove("sel"));
  document.getElementById("rc-"+n).classList.add("sel");
  document.getElementById("spinBtn").disabled=false;
}
function selectRoulColor(col){
  roulSelected=col;
  ["red","black"].forEach(c=>{
    const el=document.getElementById("rc-"+c);
    el.style.border=c===col?"3px solid var(--gold)":"3px solid transparent";
    el.style.boxShadow=c===col?"0 0 12px #C9A84C66":"none";
  });
  document.getElementById("spinBtn").disabled=false;
}
function selectRoulDozen(d){
  roulSelected=d;
  [1,2,3].forEach(i=>{
    const el=document.getElementById("rd-"+i);
    el.style.border=i===d?"3px solid var(--gold)":"3px solid #C9A84C22";
    el.style.color=i===d?"var(--gold)":"var(--dim)";
  });
  document.getElementById("spinBtn").disabled=false;
}

function spinRoulette(){
  if(roulSelected===null) return;
  document.getElementById("spinBtn").disabled=true;
  document.getElementById("spinBtn").textContent="Dreht...";
  document.getElementById("roulResult").innerHTML="";
  setTimeout(()=>{
    const n=Math.floor(Math.random()*37);
    const col=cellClass(n);
    roulStats.total++;
    if(col==="r") roulStats.red++;
    else if(col==="b") roulStats.black++;
    else roulStats.green++;

    // flash
    if(roulBetType==="number"){
      const el=document.getElementById("rc-"+n);
      if(el){el.classList.add("flash");setTimeout(()=>el.classList.remove("flash"),500);}
    }

    let won=false,payout=0;
    if(roulBetType==="number"){won=roulSelected===n;payout=won?35:-1;}
    else if(roulBetType==="color"){
      won=roulSelected==="red"?col==="r":col==="b";payout=won?1:-1;
    } else {
      const d=roulSelected;
      won=n>=(d-1)*12+1&&n<=d*12;payout=won?2:-1;
    }
    changeChips(payout);
    const colBg=col==="r"?"var(--red)":col==="g"?"#2d6a2d":"#1a1a1a";
    document.getElementById("roulResult").innerHTML=
      `<div style="background:#0a1f16;border-radius:8px;padding:10px 14px;display:flex;align-items:center;gap:10px;margin-bottom:10px;">
        <div style="width:36px;height:36px;border-radius:6px;background:${colBg};display:flex;align-items:center;justify-content:center;font-weight:700;font-size:14px;color:#fff;">${n}</div>
        <span class="badge ${won?"win":"lose"}" style="margin:0;">${won?"✓ +"+(payout)+" Chip"+(payout>1?"s":""):"✗ -1 Chip"}</span>
      </div>`;
    document.getElementById("spinBtn").disabled=false;
    document.getElementById("spinBtn").textContent="Drehen 🎡";
    // stats
    const sp=document.getElementById("roulStats"); sp.style.display="";
    document.getElementById("roulSpinCount").textContent="Nach "+roulStats.total+" Drehungen:";
    document.getElementById("rs-red").textContent=roulStats.red;
    document.getElementById("rs-black").textContent=roulStats.black;
    document.getElementById("rs-green").textContent=roulStats.green;
  },600);
}

// init roulette area
setRoulBet("number", document.getElementById("rb-number"));

// ── CARDS ───────────────────────────────────────────────────────────────────────
function freshDeck(){
  const d=[];
  for(const s of SUITS) for(const v of VALUES) d.push({s,v});
  for(let i=d.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[d[i],d[j]]=[d[j],d[i]];}
  return d;
}

function initCards(){
  deck=freshDeck(); drawnCards=[];
  document.getElementById("drawnCards").innerHTML="";
  document.getElementById("deckEmpty").style.display="none";
  renderCardBets();
  renderCardProb();
}

function renderCardBets(){
  const area=document.getElementById("cardBetArea"); area.innerHTML="";
  CARD_BETS.forEach(o=>{
    const d=document.createElement("div");
    d.className="bet-opt";
    d.id="cbo-"+o.key;
    d.style.background=cardBet===o.key?"#0a1f16":"transparent";
    d.style.border=`1px solid ${cardBet===o.key?"var(--gold)":"#C9A84C22"}`;
    d.style.cursor="pointer";
    d.innerHTML=`<div>
      <div style="font-weight:600;font-size:13px;color:${cardBet===o.key?"var(--gold)":"var(--text)"};">${o.label}</div>
      <div style="font-size:11px;color:var(--dim);">Basiswahrsch.: ${o.p} → Gewinn: ${o.payout}:1</div>
    </div>${cardBet===o.key?'<div style="color:var(--gold);font-size:18px;">✓</div>':""}`;
    d.onclick=()=>selectCardBet(o.key);
    area.appendChild(d);
  });
}

function selectCardBet(key){
  cardBet=key;
  renderCardBets();
  renderCardProb();
  document.getElementById("drawBtn").disabled=deck.length===0;
  document.getElementById("cardResult").innerHTML="";
}

function renderCardProb(){
  const area=document.getElementById("cardProbArea");
  if(!cardBet||deck.length===0){area.innerHTML="";return;}
  const rem=deck.length;
  let match=0;
  if(cardBet==="ace") match=deck.filter(c=>c.v==="A").length;
  else if(cardBet==="face") match=deck.filter(c=>["J","Q","K"].includes(c.v)).length;
  else match=deck.filter(c=>c.s==="♥"||c.s==="♦").length;
  const p=match/rem;
  area.innerHTML=`<div class="current-p">
    <div style="font-size:12px;color:var(--dim);">Aktuelle Wahrscheinlichkeit im Stapel (${rem} Karten):</div>
    <div style="font-size:24px;font-weight:700;color:var(--gold);margin:4px 0;">${(p*100).toFixed(1)} %</div>
    <div class="prog"><div class="prog-fill" style="width:${p*100}%;"></div></div>
  </div>`;
}

function drawCard(){
  if(!cardBet||deck.length===0) return;
  const card=deck.shift();
  drawnCards=[...drawnCards.slice(-4),card];
  const isRed=card.s==="♥"||card.s==="♦";
  const isAce=card.v==="A";
  const isFace=["J","Q","K"].includes(card.v);
  let won=false;
  if(cardBet==="ace") won=isAce;
  else if(cardBet==="face") won=isFace;
  else won=isRed;
  const opt=CARD_BETS.find(o=>o.key===cardBet);
  const payout=won?opt.payout:-1;
  changeChips(payout);
  cardStats.total++; if(won) cardStats.wins++;
  // draw display
  const wrap=document.getElementById("drawnCards"); wrap.innerHTML="";
  drawnCards.forEach(c=>{
    const el=document.createElement("div");
    const r=c.s==="♥"||c.s==="♦";
    el.className="card"+(r?" cr":"");
    el.innerHTML=`<div style="font-size:13px;">${c.v}</div><div style="font-size:20px;">${c.s}</div>`;
    wrap.appendChild(el);
  });
  document.getElementById("cardResult").innerHTML=
    `<span class="badge ${won?"win":"lose"}">${card.v}${card.s} — ${won?"✓ +"+payout+" Chips":"✗ -1 Chip"}</span>`;
  renderCardProb();
  if(deck.length===0){
    document.getElementById("drawBtn").disabled=true;
    document.getElementById("deckEmpty").style.display="";
  }
  // stats
  const sp=document.getElementById("cardStats"); sp.style.display="";
  document.getElementById("cs-win").textContent=cardStats.wins;
  document.getElementById("cs-lose").textContent=cardStats.total-cardStats.wins;
  const pctEl=document.getElementById("cs-pct");
  const pct=cardStats.wins/cardStats.total;
  pctEl.textContent=(pct*100).toFixed(0)+"%";
  pctEl.style.color=pct>0.4?"var(--gold)":"var(--red)";
}

function resetDeck(){
  deck=freshDeck(); drawnCards=[];
  document.getElementById("drawnCards").innerHTML="";
  document.getElementById("deckEmpty").style.display="none";
  document.getElementById("cardResult").innerHTML="";
  if(cardBet) document.getElementById("drawBtn").disabled=false;
  renderCardProb();
}

initCards();
</script>
</body>
</html>
