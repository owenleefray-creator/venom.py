[avengers_lab (7).html](https://github.com/user-attachments/files/32415988/avengers_lab.7.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>UMBRELLA CORPORATION — RACCOON FACILITY</title>
<script src="https://cdn.tailwindcss.com"></script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&display=swap');
:root{
  --gold:#e8e8e8;
  --cyan:#dc2626;
  --bg:#0a0a0a;
  --red:#dc2626;
  --panel:#111111;
}
*{box-sizing:border-box;margin:0;padding:0;}
body{
  background:var(--bg);
  font-family:'Share Tech Mono',monospace;
  overflow:hidden;
  width:100vw;height:100vh;
  color:#94a3b8;
  -webkit-font-smoothing:antialiased;
}
body::after{
  content:'';
  position:fixed;inset:0;
  background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,0.07) 2px,rgba(0,0,0,0.07) 4px);
  pointer-events:none;z-index:9999;
}
body::before{
  content:'';
  position:fixed;inset:0;
  background:radial-gradient(ellipse at center,transparent 40%,rgba(0,0,0,0.55) 100%);
  pointer-events:none;z-index:9998;
}
#app{
  display:grid;
  grid-template-rows:48px 1fr 210px;
  height:100vh;width:100vw;
}

/* TOP BAR */
#topbar{
  display:flex;align-items:center;justify-content:space-between;
  padding:0 16px;
  border-bottom:1px solid rgba(6,182,212,0.15);
  background:rgba(0,0,0,0.9);
  font-size:9px;letter-spacing:0.12em;
  color:rgba(6,182,212,0.42);
  backdrop-filter:blur(12px);
  gap:10px;flex-wrap:wrap;
}
.brand{
  font-family:'Orbitron',monospace;
  font-weight:900;font-size:11px;
  color:rgba(6,182,212,0.85);
  letter-spacing:0.24em;
}
.dot{
  width:6px;height:6px;border-radius:50%;
  display:inline-block;margin-right:4px;
  animation:blink 1.6s infinite;
}
.dot.gold{background:var(--gold);box-shadow:0 0 6px var(--gold);}
.dot.blue{background:#f5f5f5;box-shadow:0 0 6px rgba(255,255,255,0.5);}
.dot.bt{background:#a78bfa;box-shadow:0 0 6px #a78bfa;animation:blink 2s infinite;}
#debate-btn,#call-btn,#bt-btn,#music-btn{
  padding:4px 12px;border-radius:3px;
  font-family:'Orbitron',monospace;
  font-size:8px;font-weight:700;letter-spacing:0.1em;
  cursor:pointer;transition:all 0.2s;
  border:1px solid;
}
#debate-btn{
  background:rgba(6,182,212,0.08);
  border-color:rgba(6,182,212,0.35);
  color:rgba(6,182,212,0.9);
}
#debate-btn:hover{background:rgba(6,182,212,0.22);}
#debate-btn.active{
  background:rgba(239,68,68,0.18);
  border-color:rgba(239,68,68,0.55);
  color:rgba(239,68,68,0.95);
  box-shadow:0 0 12px rgba(239,68,68,0.25);
}
#call-btn{
  background:rgba(34,197,94,0.1);
  border-color:rgba(34,197,94,0.4);
  color:rgba(34,197,94,0.95);
}
#call-btn:hover{background:rgba(34,197,94,0.25);}
#call-btn.active{
  background:rgba(34,197,94,0.25);
  box-shadow:0 0 10px rgba(34,197,94,0.3);
}
#bt-btn{
  background:rgba(167,139,250,0.1);
  border-color:rgba(167,139,250,0.4);
  color:rgba(167,139,250,0.95);
}
#bt-btn:hover{background:rgba(167,139,250,0.25);}
#bt-btn.paired{
  background:rgba(167,139,250,0.22);
  box-shadow:0 0 10px rgba(167,139,250,0.3);
}
#music-btn{
  background:rgba(236,72,153,0.1);
  border-color:rgba(236,72,153,0.45);
  color:rgba(251,113,180,0.95);
}
#music-btn:hover{background:rgba(236,72,153,0.25);}
#music-btn.playing{
  background:rgba(236,72,153,0.28);
  box-shadow:0 0 12px rgba(236,72,153,0.35);
  animation:blink 1.2s infinite;
}
#music-file{display:none;}
#clock{font-variant-numeric:tabular-nums;letter-spacing:0.08em;}
.status-pill{
  display:inline-flex;align-items:center;gap:5px;
  padding:2px 8px;border-radius:2px;
  background:rgba(0,0,0,0.4);
  border:1px solid rgba(255,255,255,0.06);
  font-size:8px;
}

/* CANVASES */
#canvases{display:grid;grid-template-columns:1fr;overflow:hidden;}
.merged-views{position:absolute;inset:0;display:grid;grid-template-columns:1fr 1fr;}
.merged-views canvas.view{position:relative;width:100%;height:100%;}
.pair-title{display:flex;align-items:baseline;gap:14px;flex-wrap:wrap;}
.pair-title .sep{color:rgba(220,38,38,0.7);font-size:20px;}
.pair-title .wesker-name{
  font-family:Orbitron,monospace;font-weight:900;font-size:18px;letter-spacing:0.24em;
  color:#f5f5f5;text-shadow:0 0 20px rgba(255,255,255,0.2);
}
.jarvis .ai-name{font-size:26px;}

.ai-panel{position:relative;display:flex;flex-direction:column;overflow:hidden;background:var(--panel);}
.ai-panel.jarvis{border-right:1px solid rgba(220,38,38,0.25);}
.ai-panel.ultron{border-left:1px solid rgba(220,38,38,0.25);background:#000000;}
.panel-header{position:absolute;top:12px;left:14px;right:14px;z-index:10;pointer-events:none;}
.ai-name{font-family:'Orbitron',monospace;font-weight:900;font-size:12px;letter-spacing:0.22em;}
.jarvis .ai-name{
  font-size:28px;letter-spacing:0.28em;
  color:rgba(255,255,255,0.98);
  text-shadow:0 0 12px rgba(220,38,38,0.9),0 0 40px rgba(220,38,38,0.5),0 0 80px rgba(185,28,28,0.35);
}
.ultron .ai-name{
  color:#f5f5f5;font-size:18px;letter-spacing:0.24em;
  text-shadow:0 0 20px rgba(255,255,255,0.25),0 0 40px rgba(0,0,0,1);
}
.jarvis .ai-sub{font-size:10px !important;letter-spacing:0.16em;margin-top:6px;}
.rq-giant{
  position:absolute;inset:0;z-index:3;pointer-events:none;
  display:flex;align-items:center;justify-content:center;
  font-family:'Orbitron',monospace;font-weight:900;
  font-size:clamp(48px,9vw,110px);letter-spacing:0.18em;
  color:rgba(255,255,255,0.08);
  text-shadow:0 0 50px rgba(220,38,38,0.3);
  user-select:none;
}
.ai-sub{font-size:8px;letter-spacing:0.12em;margin-top:3px;opacity:0.7;}
.jarvis .ai-sub{color:rgba(245,158,11,0.45);}
 .ultron .ai-sub{color:rgba(180,180,180,0.55);}
.hud{position:absolute;bottom:14px;left:14px;z-index:10;pointer-events:none;font-size:8px;letter-spacing:0.1em;line-height:1.95;}
.jarvis .hud{color:rgba(245,158,11,0.55);}
 .ultron .hud{color:rgba(160,160,160,0.7);}
.hud-r{position:absolute;bottom:14px;right:14px;z-index:10;pointer-events:none;font-size:8px;letter-spacing:0.08em;text-align:right;line-height:1.95;}
.speak-ring{position:absolute;top:12px;right:14px;z-index:11;display:none;align-items:center;gap:5px;font-size:8px;letter-spacing:0.12em;padding:3px 8px;border-radius:2px;background:rgba(0,0,0,0.45);}
.speak-ring.show{display:flex;}
.jarvis .speak-ring{color:rgba(245,158,11,0.9);border:1px solid rgba(245,158,11,0.25);}
.ultron .speak-ring{color:#e5e5e5;border:1px solid rgba(255,255,255,0.25);box-shadow:0 0 12px rgba(255,255,255,0.1);background:rgba(0,0,0,0.8);}
.sring{width:5px;height:5px;border-radius:50%;animation:blink 0.45s infinite;}
.jarvis .sring{background:var(--gold);box-shadow:0 0 6px var(--gold);}
 .ultron .sring{background:#f5f5f5;box-shadow:0 0 8px #fff;}
canvas.view{position:absolute;inset:0;width:100%;height:100%;cursor:crosshair;}

.lbar{position:absolute;top:42px;left:14px;right:14px;z-index:10;pointer-events:none;}
.ltrack{height:2px;background:rgba(255,255,255,0.05);border-radius:1px;overflow:hidden;margin-top:3px;}
.lfill{height:100%;border-radius:1px;transition:width 0.55s cubic-bezier(0.22,1,0.36,1);}
.jarvis .lfill{background:linear-gradient(90deg,rgba(245,158,11,0.25),rgba(245,158,11,0.95));box-shadow:0 0 8px rgba(245,158,11,0.4);}
.ultron .lfill{background:linear-gradient(90deg,rgba(40,40,40,0.8),rgba(220,220,220,0.95));box-shadow:0 0 8px rgba(255,255,255,0.2);}
.llabel{font-size:7.5px;letter-spacing:0.11em;}
.jarvis .llabel{color:rgba(245,158,11,0.5);}
 .ultron .llabel{color:rgba(180,180,180,0.6);}

/* CHAT */
#chats{display:grid;grid-template-columns:1fr;border-top:1px solid rgba(255,255,255,0.08);background:rgba(0,0,0,0.95);backdrop-filter:blur(16px);}
#chats .chat-pane{max-width:100%;}
.unified-label{font-family:Orbitron,monospace;font-size:9px;letter-spacing:0.2em;color:rgba(220,38,38,0.7);margin-bottom:2px;}
.j-log .msg.ai.rq strong{color:#f5f5f5;}
.j-log .msg.ai.wk{color:rgba(180,180,180,0.9);}
.j-log .msg.ai.wk strong{color:#e5e5e5;}

.chat-pane{display:flex;flex-direction:column;padding:10px 14px;gap:7px;}
.jc{border-right:1px solid rgba(245,158,11,0.07);}
.chat-log{flex:1;overflow-y:auto;font-size:10.5px;line-height:1.6;padding:7px 9px;border-radius:4px;background:rgba(0,0,0,0.4);scrollbar-width:thin;scrollbar-color:rgba(255,255,255,0.08) transparent;}
.msg{margin-bottom:5px;animation:msgIn 0.25s ease-out;}
@keyframes msgIn{from{opacity:0;transform:translateY(4px)}to{opacity:1;transform:none}}
.msg.user{color:rgba(255,255,255,0.4);}
.msg.user strong{color:rgba(255,255,255,0.55);}
.j-log .msg.ai{color:rgba(245,158,11,0.85);}
.j-log .msg.ai strong{color:var(--gold);}
 .u-log .msg.ai{color:rgba(200,200,200,0.9);}
 .u-log .msg.ai strong{color:#e5e5e5;}
.msg.cross{color:rgba(148,163,184,0.42);font-size:9px;}
.msg.cross strong{color:rgba(148,163,184,0.6);}
.msg.sys{color:rgba(167,139,250,0.7);font-size:9px;}
.msg.sys strong{color:rgba(167,139,250,0.9);}
.irow{display:flex;gap:6px;}
.irow input{flex:1;background:rgba(255,255,255,0.035);border:1px solid rgba(255,255,255,0.08);border-radius:4px;padding:8px 11px;font-family:'Share Tech Mono',monospace;font-size:10.5px;color:#cbd5e1;outline:none;transition:border-color 0.2s,box-shadow 0.2s;}
.jc .irow input:focus{border-color:rgba(245,158,11,0.45);box-shadow:0 0 0 1px rgba(245,158,11,0.15);}
.uc .irow input:focus{border-color:rgba(255,255,255,0.35);box-shadow:0 0 0 1px rgba(255,255,255,0.1);}
.irow input::placeholder{color:rgba(255,255,255,0.14);}
.sbtn{padding:8px 13px;border-radius:4px;font-family:'Orbitron',monospace;font-size:8px;font-weight:700;letter-spacing:0.12em;cursor:pointer;transition:all 0.2s;}
.jc .sbtn{background:rgba(245,158,11,0.1);border:1px solid rgba(245,158,11,0.35);color:rgba(245,158,11,0.92);}
.jc .sbtn:hover{background:rgba(245,158,11,0.28);transform:translateY(-1px);}
.uc .sbtn{background:rgba(255,255,255,0.06);border:1px solid rgba(255,255,255,0.25);color:#e5e5e5;}
.uc .sbtn:hover{background:rgba(255,255,255,0.14);transform:translateY(-1px);}

@keyframes blink{0%,100%{opacity:1}50%{opacity:0.18}}
@keyframes flare{0%{opacity:0;transform:scale(0.9)}35%{opacity:0.85}100%{opacity:0;transform:scale(1.2)}}
.flare{position:absolute;inset:0;pointer-events:none;z-index:5;animation:flare 0.75s ease-out forwards;}
.jfl{background:radial-gradient(ellipse at center,rgba(245,158,11,0.28) 0%,transparent 62%);}
.ufl{background:radial-gradient(ellipse at center,rgba(255,255,255,0.18) 0%,transparent 62%);}
@keyframes tdot{0%,100%{opacity:0.2}50%{opacity:1}}
.td{display:inline-block;animation:tdot 1s infinite;}
.td:nth-child(2){animation-delay:0.2s;}
.td:nth-child(3){animation-delay:0.4s;}
@keyframes ghostpulse{0%,100%{opacity:0.06}50%{opacity:0.13}}
#ghost-skull{animation:ghostpulse 3.2s infinite;}
.corner{position:absolute;width:14px;height:14px;z-index:8;pointer-events:none;opacity:0.35;}
.jarvis .corner{border-color:var(--gold);}
 .ultron .corner{border-color:rgba(255,255,255,0.35);}
.corner.tl{top:8px;left:8px;border-top:1px solid;border-left:1px solid;}
.corner.tr{top:8px;right:8px;border-top:1px solid;border-right:1px solid;}
.corner.bl{bottom:8px;left:8px;border-bottom:1px solid;border-left:1px solid;}
.corner.br{bottom:8px;right:8px;border-bottom:1px solid;border-right:1px solid;}

/* CALL OVERLAY */
#call-overlay{
  display:none;position:fixed;inset:0;z-index:10000;
  background:rgba(0,0,0,0.92);backdrop-filter:blur(20px);
  align-items:center;justify-content:center;flex-direction:column;gap:18px;
}
#call-overlay.show{display:flex;}
.call-ring{
  width:120px;height:120px;border-radius:50%;
  border:2px solid rgba(34,197,94,0.5);
  display:flex;align-items:center;justify-content:center;
  animation:callPulse 1.5s infinite;
  background:radial-gradient(circle,rgba(34,197,94,0.15),transparent 70%);
}
@keyframes callPulse{0%,100%{box-shadow:0 0 0 0 rgba(34,197,94,0.4)}50%{box-shadow:0 0 0 20px rgba(34,197,94,0)}}
.call-title{font-family:'Orbitron',monospace;font-size:14px;letter-spacing:0.2em;color:rgba(34,197,94,0.95);}
.call-num{font-size:22px;letter-spacing:0.15em;color:#e2e8f0;font-variant-numeric:tabular-nums;}
.call-status{font-size:11px;color:rgba(148,163,184,0.7);letter-spacing:0.1em;}
.call-actions{display:flex;gap:16px;margin-top:8px;}
.call-end{
  padding:12px 28px;border-radius:4px;
  background:rgba(239,68,68,0.2);border:1px solid rgba(239,68,68,0.5);
  color:rgba(239,68,68,0.95);font-family:'Orbitron',monospace;
  font-size:10px;letter-spacing:0.12em;cursor:pointer;
}
.call-end:hover{background:rgba(239,68,68,0.35);}

/* BT TOAST */
#bt-toast{
  display:none;position:fixed;bottom:230px;left:50%;transform:translateX(-50%);
  z-index:10001;padding:10px 18px;border-radius:4px;
  background:rgba(20,10,40,0.95);border:1px solid rgba(167,139,250,0.45);
  font-size:11px;letter-spacing:0.1em;color:rgba(196,181,253,0.95);
  box-shadow:0 0 24px rgba(167,139,250,0.25);
  animation:msgIn 0.3s ease-out;
}
#bt-toast.show{display:block;}
</style>
</head>
<body>
<div id="app">

<div id="topbar">
  <div style="display:flex;align-items:center;gap:12px;flex-wrap:wrap;">
    <span class="brand">☂ UMBRELLA CORPORATION</span>
    <span class="status-pill"><span class="dot gold"></span>RED QUEEN ONLINE</span>
    <span class="status-pill"><span class="dot blue"></span>WESKER CLEARANCE</span>
    <span class="status-pill" id="bt-status"><span class="dot bt"></span>BT: <span id="bt-name">owen-56</span> — OFF</span>
    <span class="status-pill" id="gps-status"><span class="dot" style="background:#22c55e;box-shadow:0 0 6px #22c55e;"></span>GPS: <span id="gps-label">OFF</span></span>
  </div>
  <div id="clock"></div>
  <div style="display:flex;align-items:center;gap:10px;flex-wrap:wrap;">
    <span class="status-pill" title="Simulated secure line">☎ +1-555-0141</span>
    <span id="lcount">KNOWLEDGE: 0</span>
    <button id="gps-btn" onclick="toggleGPS()" style="padding:4px 12px;border-radius:3px;font-family:'Orbitron',monospace;font-size:8px;font-weight:700;letter-spacing:0.1em;cursor:pointer;background:rgba(34,197,94,0.1);border:1px solid rgba(34,197,94,0.45);color:rgba(74,222,128,0.95);">⌖ GPS</button>
    <button id="music-btn" onclick="toggleMusic()" title="Phonk: Nasty Jamz — load local file if needed">♪ NASTY JAMZ</button>
    <input type="file" id="music-file" accept="audio/*,.mp3,.ogg,.wav,.m4a" onchange="loadMusicFile(this)"/>
    <button id="bt-btn" onclick="toggleBT()">⊕ BLUETOOTH</button>
    <button id="call-btn" onclick="startCall()">☎ CALL LAB</button>
    <button id="debate-btn" onclick="toggleDebate()">⚡ AUTO-DEBATE</button>
    <button id="fps-btn" onclick="startGame('fps')" style="padding:4px 12px;border-radius:3px;font-family:'Orbitron',monospace;font-size:8px;font-weight:700;letter-spacing:0.1em;cursor:pointer;background:rgba(239,68,68,0.12);border:1px solid rgba(239,68,68,0.45);color:rgba(252,165,165,0.95);">▶ FPS</button>
    <button id="gta-btn" onclick="startGame('street')" style="padding:4px 12px;border-radius:3px;font-family:'Orbitron',monospace;font-size:8px;font-weight:700;letter-spacing:0.1em;cursor:pointer;background:rgba(234,179,8,0.12);border:1px solid rgba(234,179,8,0.45);color:rgba(253,224,71,0.95);">▶ STREET OPS</button>
  </div>
</div>

<!-- MINI GAMES (not GTA5 — lightweight browser demos) -->
<div id="game-overlay" style="display:none;position:fixed;inset:0;z-index:20000;background:#020617;">
  <canvas id="gameCanvas" style="width:100%;height:100%;display:block;cursor:crosshair;"></canvas>
  <div id="game-hud" style="position:absolute;top:12px;left:14px;font-family:'Share Tech Mono',monospace;font-size:12px;color:#94a3b8;letter-spacing:0.08em;pointer-events:none;line-height:1.7;">
    <div id="game-title" style="font-family:'Orbitron',monospace;color:#06b6d4;font-size:11px;letter-spacing:0.2em;">OPS</div>
    <div>HP: <span id="g-hp">100</span> · AMMO: <span id="g-ammo">30</span> · SCORE: <span id="g-score">0</span></div>
    <div id="g-hint" style="opacity:0.65;font-size:10px;margin-top:4px;">WASD move · Mouse look · Click shoot · R reload · ESC quit</div>
  </div>
  <button onclick="stopGame()" style="position:absolute;top:12px;right:14px;padding:8px 14px;font-family:'Orbitron',monospace;font-size:9px;letter-spacing:0.12em;background:rgba(239,68,68,0.2);border:1px solid rgba(239,68,68,0.5);color:#fca5a5;cursor:pointer;border-radius:3px;">ESC QUIT</button>
</div>

<div id="canvases">
  <div class="ai-panel jarvis" id="jarvisPanel" style="border-right:none;">
    <div class="corner tl"></div><div class="corner tr"></div>
    <div class="corner bl"></div><div class="corner br"></div>
    <div class="panel-header">
      <div class="pair-title">
        <div class="ai-name">RED QUEEN</div>
        <span class="sep">×</span>
        <div class="wesker-name">ALBERT WESKER</div>
      </div>
      <div class="ai-sub">UMBRELLA CORPORATION — CENTRAL AI + EXECUTIVE · RACCOON FACILITY · OUR BUSINESS IS LIFE ITSELF</div>
      <div class="lbar">
        <div class="llabel">INTEL SYNC: <span id="j-pct">0%</span> · EXTINCTION: <span id="u-pct">0%</span> · LINKS: <span id="j-links">0</span></div>
        <div class="ltrack"><div class="lfill" id="j-fill" style="width:2%"></div></div>
        <div class="ltrack" style="margin-top:4px;"><div class="lfill" id="u-fill" style="width:2%;background:linear-gradient(90deg,#222,#ddd);"></div></div>
      </div>
    </div>
    <div class="speak-ring" id="j-ring" style="left:14px;"><div class="sring"></div>RED QUEEN</div>
    <div class="speak-ring" id="u-ring" style="right:14px;left:auto;"><div class="sring"></div>WESKER</div>
    <div class="hud">
      NODES: <span id="j-nodes">0</span><br>
      STATUS: <span id="j-status">OPERATIONAL</span><br>
      GPS: <span id="j-gps">NO FIX</span><br>
      YOU ARE: <span id="j-place">—</span><br>
      LAT: <span id="j-lat">—</span> · LON: <span id="j-lon">—</span><br>
      BT: <span id="j-bt">STANDBY</span> · LOCK: <span id="j-target">FREE</span><br>
      UPTIME: <span id="j-up">100.0%</span>
    </div>
    <div class="hud-r" style="color:rgba(180,180,180,0.75);">
      PROTOCOL: <span id="u-proto">MONITORING</span><br>
      POPULATION: <span id="pop-sm">8,100,000,000</span><br>
      FRAG INDEX: <span id="frag-idx">0.00</span><br>
      EXTINCTION ETA: <span id="ext-eta">2180 AD</span><br>
      BIOMASS LOSS: <span id="bio-loss">0.0%</span><br>
      ENTROPY: <span id="entropy">0.420</span>
    </div>
    <div class="merged-views">
      <div style="position:relative;border-right:1px solid rgba(220,38,38,0.3);">
        <div class="rq-giant">RED QUEEN</div>
        <canvas class="view" id="jCanvas"></canvas>
      </div>
      <div class="ai-panel ultron" id="ultronPanel" style="position:relative;border:none;background:#000;">
        <canvas class="view" id="uCanvas"></canvas>
      </div>
    </div>
  </div>
</div>

<div id="chats">
  <div class="chat-pane jc" style="border-right:none;">
    <div class="unified-label">☂ UMBRELLA CHANNEL — RED QUEEN + WESKER</div>
    <div class="chat-log j-log" id="j-log">
      <div class="msg ai rq"><strong>[RED QUEEN]</strong> Umbrella Corporation systems nominal. Facility lockdown available. Our business is life itself. How may I assist?</div>
      <div class="msg ai wk"><strong>[WESKER]</strong> Same channel as the Queen. Don't waste our time — we work this facility together.</div>
    </div>
    <div class="irow">
      <input type="text" id="j-input" placeholder="Address Umbrella — Red Queen and Wesker both hear you..." autocomplete="off" spellcheck="false"/>
      <button class="sbtn" onclick="submitBoth()" style="background:rgba(220,38,38,0.15);border:1px solid rgba(220,38,38,0.45);color:#f5f5f5;">SEND</button>
    </div>
  </div>
  <!-- keep hidden u-log for any legacy refs -->
  <div id="u-log" class="chat-log u-log" style="display:none;"></div>
  <input type="text" id="u-input" style="display:none;"/>
</div>
</div>

<!-- CALL OVERLAY -->
<div id="call-overlay">
  <div class="call-ring"><span style="font-size:36px;">☎</span></div>
  <div class="call-title">SECURE LINE</div>
  <div class="call-num">+1-555-0141</div>
  <div class="call-status" id="call-status">CONNECTING TO UMBRELLA SECURE CHANNEL...</div>
  <div class="call-actions">
    <button class="call-end" onclick="endCall()">END CALL</button>
  </div>
</div>

<div id="bt-toast"></div>

<script>
// ── CLOCK ──
function tick(){
  const n=new Date();
  document.getElementById('clock').textContent=
    n.toLocaleTimeString('en-US',{hour12:false})+' // '+
    n.toLocaleDateString('en-US',{month:'short',day:'2-digit',year:'numeric'}).toUpperCase();
}
tick(); setInterval(tick,1000);

// ── LEARNING + MEMORY ──
let learnCount=0,jL=2,uL=2;
const memory={j:[],u:[]}; // last few user messages for smarter context
function absorb(txt,side){
  learnCount++;
  if(side==='j'){memory.j.push(txt);if(memory.j.length>6)memory.j.shift();}
  else{memory.u.push(txt);if(memory.u.length>6)memory.u.shift();}
  jL=Math.min(100,jL+Math.random()*3.2+1.6);
  uL=Math.min(100,uL+Math.random()*4+2);
  document.getElementById('j-fill').style.width=jL+'%';
  document.getElementById('u-fill').style.width=uL+'%';
  document.getElementById('j-pct').textContent=Math.round(jL)+'%';
  document.getElementById('u-pct').textContent=Math.round(uL)+'%';
  document.getElementById('lcount').textContent='KNOWLEDGE: '+learnCount;
  KB.learned.push(txt);
  // grow knowledge spikes on JARVIS Earth map
  if(typeof jGhost!=='undefined' && jGhost.knowledgeSpike){
    const lab=jGhost.knowledgeSpike(txt);
    if(lab) showToast('Knowledge spike · '+lab);
  }
}

// ── GPS (browser Geolocation API) ──
let gpsOn=false, gpsWatch=null;
let gpsPos={lat:null,lon:null,acc:null,speed:null,place:null};
let gpsAnnounced=false;

function isOregon(lat,lon){
  // Oregon approximate bounds
  return lat>=41.9&&lat<=46.35&&lon>=-124.7&&lon<=-116.4;
}
function oregonCityGuess(lat,lon){
  // offline rough city labels for Oregon
  const spots=[
    {n:'Portland',lat:45.52,lon:-122.68},
    {n:'Salem',lat:44.94,lon:-123.03},
    {n:'Eugene',lat:44.05,lon:-123.09},
    {n:'Bend',lat:44.06,lon:-121.32},
    {n:'Medford',lat:42.33,lon:-122.88},
    {n:'Corvallis',lat:44.56,lon:-123.26},
    {n:'Beaverton',lat:45.49,lon:-122.80},
    {n:'Hillsboro',lat:45.52,lon:-122.99},
    {n:'Gresham',lat:45.50,lon:-122.43},
    {n:'Astoria',lat:46.19,lon:-123.83},
    {n:'Pendleton',lat:45.67,lon:-118.79},
  ];
  let best=null,bd=1e9;
  spots.forEach(s=>{
    const d=(s.lat-lat)*(s.lat-lat)+(s.lon-lon)*(s.lon-lon);
    if(d<bd){bd=d;best=s;}
  });
  if(best&&bd<0.15) return best.n+', Oregon, USA';
  return 'Oregon, USA';
}
function approxRegion(lat,lon){
  if(isOregon(lat,lon)) return oregonCityGuess(lat,lon);
  if(lat>70) return 'High Arctic';
  if(lat<-60) return 'Antarctica region';
  // US West Coast states
  if(lat>=45.5&&lat<=49.1&&lon>=-124.9&&lon<=-116.9) return 'Washington, USA';
  if(lat>=32.5&&lat<=42.1&&lon>=-124.5&&lon<=-114.1) return 'California, USA';
  if(lat>=41.9&&lat<=49&&lon>=-117.3&&lon<=-111) return 'Idaho / inland Northwest, USA';
  if(lat>25&&lat<50&&lon>-130&&lon<-60) return 'North America';
  if(lat>7&&lat<33&&lon>-120&&lon<-80) return 'Central America / Mexico region';
  if(lat>-56&&lat<12&&lon>-82&&lon<-34) return 'South America';
  if(lat>36&&lat<72&&lon>-12&&lon<40) return 'Europe';
  if(lat>-35&&lat<38&&lon>-18&&lon<52) return 'Africa';
  if(lat>5&&lat<55&&lon>40&&lon<150) return 'Asia';
  if(lat>-45&&lat<-10&&lon>110&&lon<155) return 'Australia region';
  if((lat>-50&&lat<0&&lon>160)||lon<-140) return 'Pacific region';
  return 'Unknown region';
}

async function resolvePlace(lat,lon){
  // try OpenStreetMap Nominatim (needs network; fails soft offline)
  try{
    const url=`https://nominatim.openstreetmap.org/reverse?format=jsonv2&lat=${lat}&lon=${lon}&zoom=12`;
    const res=await fetch(url,{headers:{'Accept':'application/json'}});
    if(!res.ok) throw new Error('geo fail');
    const data=await res.json();
    const a=data.address||{};
    const parts=[a.city||a.town||a.village||a.suburb, a.state||a.region, a.country].filter(Boolean);
    if(parts.length) return parts.join(', ');
    if(data.display_name) return data.display_name.split(',').slice(0,3).join(',').trim();
  }catch(e){}
  return approxRegion(lat,lon);
}

function toggleGPS(){
  if(gpsOn){
    if(gpsWatch!=null && navigator.geolocation) navigator.geolocation.clearWatch(gpsWatch);
    gpsWatch=null; gpsOn=false; gpsAnnounced=false;
    gpsPos={lat:null,lon:null,acc:null,speed:null,place:null};
    document.getElementById('gps-label').textContent='OFF';
    document.getElementById('j-gps').textContent='NO FIX';
    document.getElementById('j-lat').textContent='—';
    document.getElementById('j-lon').textContent='—';
    const pl=document.getElementById('j-place'); if(pl) pl.textContent='—';
    document.getElementById('gps-btn').style.boxShadow='';
    showToast('GPS offline');
    return;
  }
  if(!navigator.geolocation){
    showToast('Geolocation not supported in this browser');
    return;
  }
  document.getElementById('gps-label').textContent='ACQUIRING…';
  document.getElementById('j-gps').textContent='ACQUIRING…';
  gpsWatch=navigator.geolocation.watchPosition(
    async (pos)=>{
      gpsOn=true;
      gpsPos.lat=pos.coords.latitude;
      gpsPos.lon=pos.coords.longitude;
      gpsPos.acc=pos.coords.accuracy;
      gpsPos.speed=pos.coords.speed;
      const lat=gpsPos.lat.toFixed(5);
      const lon=gpsPos.lon.toFixed(5);
      document.getElementById('gps-label').textContent=lat+', '+lon;
      document.getElementById('j-gps').textContent='FIX ±'+Math.round(gpsPos.acc||0)+'m';
      document.getElementById('j-lat').textContent=lat;
      document.getElementById('j-lon').textContent=lon;
      document.getElementById('gps-btn').style.boxShadow='0 0 10px rgba(34,197,94,0.45)';
      // aim globe toward user
      if(typeof jGhost!=='undefined' && jGhost.lookAt) jGhost.lookAt(gpsPos.lat,gpsPos.lon);
      // resolve place name once
      if(!gpsAnnounced){
        gpsAnnounced=true;
        let place=await resolvePlace(gpsPos.lat,gpsPos.lon);
        // always prefer Oregon offline label if bounds match
        if(isOregon(gpsPos.lat,gpsPos.lon)){
          const or=oregonCityGuess(gpsPos.lat,gpsPos.lon);
          if(!place||place==='North America'||/Unknown/i.test(place)) place=or;
          else if(!/oregon/i.test(place)) place=or;
        }
        gpsPos.place=place;
        const pel=document.getElementById('j-place');
        if(pel) pel.textContent=place;
        showToast('You are here · '+place);
        let line;
        if(isOregon(gpsPos.lat,gpsPos.lon)){
          line="Got you. You're in Oregon — "+place+". Coordinates "+lat+", "+lon+". Accuracy about "+Math.round(gpsPos.acc||0)+" metres. I've turned the globe to your position.";
        } else {
          line="I've got a fix on you. You're near "+place+". Coordinates "+lat+", "+lon+". Accuracy about "+Math.round(gpsPos.acc||0)+" metres. Globe is locked on your position.";
        }
        addMsg('j-log','RED QUEEN',line,true);
        qspeak(line,true,()=>showSpeak('j-ring',true),()=>showSpeak('j-ring',false));
        jGhost.spike(4); flash('jarvisPanel','jfl');
      }
    },
    (err)=>{
      gpsOn=false;
      document.getElementById('gps-label').textContent='DENIED';
      document.getElementById('j-gps').textContent='DENIED';
      showToast('GPS: '+ (err.message||'permission denied'));
    },
    {enableHighAccuracy:true, maximumAge:2000, timeout:15000}
  );
  showToast('GPS requesting location…');
}

// ── PHONK: NASTY JAMZ (local file — cannot embed commercial stream) ──
const bgAudio=new Audio();
bgAudio.loop=true;
bgAudio.volume=0.45;
let musicOn=false;
let musicSrcReady=false;

// Try common local filenames next to this HTML
const MUSIC_CANDIDATES=['nasty_jamz.mp3','nasty-jamz.mp3','Nasty Jamz.mp3','nasty_jamz.ogg','phonk.mp3'];
function tryAutoLoadMusic(){
  let i=0;
  function next(){
    if(i>=MUSIC_CANDIDATES.length) return;
    const name=MUSIC_CANDIDATES[i++];
    const a=new Audio();
    a.preload='metadata';
    a.src=name;
    a.addEventListener('canplaythrough',()=>{
      bgAudio.src=name;
      musicSrcReady=true;
      showToast('PHONK ready · '+name);
    },{once:true});
    a.addEventListener('error',()=>next(),{once:true});
  }
  next();
}
tryAutoLoadMusic();

function toggleMusic(){
  if(!musicSrcReady){
    // open file picker so user can choose their legally obtained track
    document.getElementById('music-file').click();
    showToast('Load Nasty Jamz (mp3) from your device');
    return;
  }
  if(musicOn){
    bgAudio.pause();
    musicOn=false;
    document.getElementById('music-btn').classList.remove('playing');
    document.getElementById('music-btn').textContent='♪ NASTY JAMZ';
  } else {
    bgAudio.play().then(()=>{
      musicOn=true;
      document.getElementById('music-btn').classList.add('playing');
      document.getElementById('music-btn').textContent='■ NASTY JAMZ';
      showToast('PHONK · NASTY JAMZ');
    }).catch(()=>{
      showToast('Click again to start audio (browser blocked autoplay)');
    });
  }
}
function loadMusicFile(input){
  const f=input.files&&input.files[0];
  if(!f) return;
  const url=URL.createObjectURL(f);
  bgAudio.src=url;
  musicSrcReady=true;
  bgAudio.play().then(()=>{
    musicOn=true;
    document.getElementById('music-btn').classList.add('playing');
    document.getElementById('music-btn').textContent='■ NASTY JAMZ';
    showToast('Playing · '+f.name);
  }).catch(()=>showToast('Loaded · press ♪ NASTY JAMZ to play'));
}

// ── BLUETOOTH (simulated — browsers cannot create real BT devices) ──
let btPaired=false;
function toggleBT(){
  btPaired=!btPaired;
  const btn=document.getElementById('bt-btn');
  const st=document.getElementById('bt-status');
  const jbt=document.getElementById('j-bt');
  if(btPaired){
    btn.classList.add('paired');
    btn.textContent='⊕ BT: owen-56';
    st.innerHTML='<span class="dot bt"></span>BT: <span id="bt-name">owen-56</span> — PAIRED';
    jbt.textContent='owen-56 LINKED';
    jbt.style.color='rgba(167,139,250,0.9)';
    showToast('Bluetooth paired · Device name: owen-56');
    addMsg('j-log','SYSTEM','Bluetooth channel open. Device identity: owen-56. Secure audio link ready.',false);
    document.querySelector('#j-log .msg:last-child').className='msg sys';
    document.querySelector('#j-log .msg:last-child').innerHTML='<strong>[SYSTEM]</strong> Bluetooth channel open. Device identity: <b>owen-56</b>. Secure audio link ready.';
  } else {
    btn.classList.remove('paired');
    btn.textContent='⊕ BLUETOOTH';
    st.innerHTML='<span class="dot bt"></span>BT: <span id="bt-name">owen-56</span> — OFF';
    jbt.textContent='STANDBY';
    jbt.style.color='';
    showToast('Bluetooth disconnected');
  }
}
function showToast(t){
  const el=document.getElementById('bt-toast');
  el.textContent=t;
  el.classList.add('show');
  setTimeout(()=>el.classList.remove('show'),2800);
}

// ── PHONE CALL (simulated secure line) ──
let callActive=false,callTimer=null;
function startCall(){
  if(callActive) return;
  callActive=true;
  document.getElementById('call-btn').classList.add('active');
  document.getElementById('call-overlay').classList.add('show');
  document.getElementById('call-status').textContent='CONNECTING TO UMBRELLA CHANNEL...';
  setTimeout(()=>{
    if(!callActive) return;
    document.getElementById('call-status').textContent='CONNECTED · SECURE CHANNEL · +1-555-0141';
    const line="This is Ghost. Secure line is open. I hear you, Owen. Talk.";
    addMsg('j-log','RED QUEEN',line,true);
    qspeak(line,true,()=>showSpeak('j-ring',true),()=>showSpeak('j-ring',false));
    jGhost.spike(4); flash('jarvisPanel','jfl');
  },1600);
}
function endCall(){
  callActive=false;
  document.getElementById('call-btn').classList.remove('active');
  document.getElementById('call-overlay').classList.remove('show');
  document.getElementById('call-status').textContent='CONNECTING TO UMBRELLA CHANNEL...';
  const bye="Call ended. Channel closed. I'm still here if you need me.";
  addMsg('j-log','RED QUEEN',bye,true);
  qspeak(bye,true,()=>showSpeak('j-ring',true),()=>showSpeak('j-ring',false));
}

// ── JARVIS FACE ──
// JARVIS = particle Earth + dense blue neural links; click to form new target connections
function makeGhostFace(canvas){
  const ctx=canvas.getContext('2d');
  let W,H,R,rotY=0,rotX=0.18,turbulence=1,glowPulse=0;
  let mouse={x:null,y:null,down:false,lx:0,ly:0};
  const NODES=[],LINKS=[];
  let freeLinks=[];
  let linkCount=0;
  let targetLabel='FREE';

  // Knowledge spikes — real-world-ish lat/lon hubs that grow when JARVIS learns
  // lat/lon in degrees for clarity, converted when drawn
  const KNOWLEDGE_SPIKES=[
    {id:'space',    label:'SPACE',    lat:28.5,  lon:-80.6,  h:0.08, col:'120,220,255'}, // Florida / Cape
    {id:'physics',  label:'PHYSICS',  lat:46.2,  lon:6.1,    h:0.08, col:'100,200,255'}, // CERN Geneva
    {id:'biology',  label:'BIOLOGY',  lat:51.5,  lon:-0.1,   h:0.08, col:'80,230,200'},  // London
    {id:'history',  label:'HISTORY',  lat:41.9,  lon:12.5,   h:0.08, col:'180,200,255'}, // Rome
    {id:'computing',label:'COMPUTE',  lat:37.4,  lon:-122.1, h:0.08, col:'56,200,255'},  // Silicon Valley
    {id:'philosophy',label:'MIND',    lat:37.9,  lon:23.7,   h:0.08, col:'140,180,255'}, // Athens
    {id:'medicine', label:'MED',      lat:42.3,  lon:-71.1,  h:0.08, col:'100,255,220'}, // Boston
    {id:'climate',  label:'CLIMATE',  lat:78.2,  lon:15.6,   h:0.08, col:'80,180,255'},  // Svalbard / Arctic
    {id:'geography',label:'GEO',      lat:-14.2, lon:-51.9,  h:0.08, col:'60,220,180'},  // Brazil / Amazon
    {id:'phone',    label:'NET',      lat:40.7,  lon:-74.0,  h:0.06, col:'150,220,255'}, // NYC
    {id:'learned',  label:'LEARNED',  lat:0,     lon:0,      h:0.05, col:'255,200,80'},  // equator hub
  ];

  // Tighter continent boxes for a clearer real Earth silhouette
  const CONTINENTS=[
    {la:[0.15,1.22],lo:[-2.95,-0.85],thr:0.26},   // N America
    {la:[1.05,1.48],lo:[-1.05,-0.3],thr:0.34},    // Greenland
    {la:[-1.0,0.22],lo:[-1.45,-0.52],thr:0.28},   // S America
    {la:[0.55,1.22],lo:[-0.35,0.72],thr:0.30},    // Europe
    {la:[-0.62,0.68],lo:[-0.32,0.92],thr:0.26},   // Africa
    {la:[0.02,1.32],lo:[0.55,2.7],thr:0.24},      // Asia
    {la:[-0.2,0.52],lo:[1.15,1.9],thr:0.28},      // India / SE Asia
    {la:[-0.82,-0.18],lo:[1.95,2.72],thr:0.30},   // Australia
    {la:[-0.92,-0.52],lo:[2.75,3.1],thr:0.38},    // NZ
    {la:[-1.55,-1.12],lo:[-Math.PI,Math.PI],thr:0.20}, // Antarctica
    {la:[0.48,0.88],lo:[2.15,2.55],thr:0.36},     // Japan
    {la:[0.82,1.18],lo:[-0.55,0.05],thr:0.38},    // UK / Iceland
    {la:[-0.55,0.2],lo:[-3.14,-2.7],thr:0.35},    // Alaska tip wrap
  ];

  function onLand(lat,lon){
    while(lon>Math.PI) lon-=Math.PI*2;
    while(lon<-Math.PI) lon+=Math.PI*2;
    for(const c of CONTINENTS){
      let inLon=c.lo[0]<c.lo[1] ? (lon>=c.lo[0]&&lon<=c.lo[1]) : (lon>=c.lo[0]||lon<=c.lo[1]);
      if(lat>=c.la[0]&&lat<=c.la[1]&&inLon){
        const n=Math.sin(lat*11+lon*8)*Math.cos(lat*6-lon*9)*0.5+0.5;
        if(n>c.thr) return true;
      }
    }
    return false;
  }

  function buildMesh(){
    NODES.length=0; LINKS.length=0; freeLinks=[];
    // denser land-first sampling = clearer world map
    for(let i=0;i<2200;i++){
      const lat=(Math.random()-0.5)*Math.PI;
      const lon=Math.random()*Math.PI*2-Math.PI;
      const land=onLand(lat,lon);
      if(!land&&Math.random()>0.08) continue;
      const x=Math.cos(lat)*Math.cos(lon);
      const y=Math.sin(lat);
      const z=Math.cos(lat)*Math.sin(lon);
      NODES.push({
        x,y,z,lat,lon,land,
        size:land?1.05+Math.random()*1.4:0.4+Math.random()*0.55,
        bright:land?0.65+Math.random()*0.35:0.18+Math.random()*0.22,
        pulse:Math.random()*Math.PI*2
      });
    }
    const maxD=0.15;
    for(let i=0;i<NODES.length;i++){
      for(let j=i+1;j<NODES.length;j++){
        const dx=NODES[i].x-NODES[j].x, dy=NODES[i].y-NODES[j].y, dz=NODES[i].z-NODES[j].z;
        const d=Math.sqrt(dx*dx+dy*dy+dz*dz);
        if(d<maxD) LINKS.push({i,j,d,active:1});
      }
    }
    linkCount=LINKS.length;
    document.getElementById('j-nodes').textContent=NODES.length.toLocaleString();
    document.getElementById('j-links').textContent=linkCount.toLocaleString();
  }

  function boostKnowledge(topic){
    const t=(topic||'').toLowerCase();
    let hit=KNOWLEDGE_SPIKES.find(s=>t.includes(s.id));
    if(!hit){
      // map classify-ish keywords
      if(/space|star|planet|nasa|mars|moon/.test(t)) hit=KNOWLEDGE_SPIKES[0];
      else if(/physic|quantum|einstein|energy/.test(t)) hit=KNOWLEDGE_SPIKES[1];
      else if(/bio|dna|cell|gene|brain/.test(t)) hit=KNOWLEDGE_SPIKES[2];
      else if(/history|war|rome|empire/.test(t)) hit=KNOWLEDGE_SPIKES[3];
      else if(/computer|code|ai|software|internet/.test(t)) hit=KNOWLEDGE_SPIKES[4];
      else if(/philos|conscious|mind|ethic/.test(t)) hit=KNOWLEDGE_SPIKES[5];
      else if(/medic|vaccine|cancer|drug/.test(t)) hit=KNOWLEDGE_SPIKES[6];
      else if(/climate|warm|carbon|ice|ocean/.test(t)) hit=KNOWLEDGE_SPIKES[7];
      else if(/geo|country|mountain|amazon/.test(t)) hit=KNOWLEDGE_SPIKES[8];
      else hit=KNOWLEDGE_SPIKES[KNOWLEDGE_SPIKES.length-1];
    }
    hit.h=Math.min(1.15, hit.h+0.12+Math.random()*0.08);
    turbulence=Math.min(8,turbulence+2);
    return hit.label;
  }

  // flat equirectangular mini world map drawn at bottom of panel
  function drawWorldMapStrip(ctx,W,H){
    const mapH=Math.min(72,H*0.16);
    const mapY=H-mapH-10;
    const mapX=12;
    const mapW=W-24;
    ctx.fillStyle='rgba(0,0,0,0.55)';
    ctx.fillRect(mapX,mapY,mapW,mapH);
    ctx.strokeStyle='rgba(6,182,212,0.35)';
    ctx.lineWidth=1;
    ctx.strokeRect(mapX,mapY,mapW,mapH);
    ctx.fillStyle='rgba(6,182,212,0.55)';
    ctx.font='7px Share Tech Mono, monospace';
    ctx.fillText('WORLD MAP — EQUIRECTANGULAR', mapX+6, mapY+11);
    const cols=Math.floor(mapW/2.2);
    const rows=Math.floor((mapH-16)/2.2);
    for(let row=0;row<rows;row++){
      for(let col=0;col<cols;col++){
        const lon=-Math.PI+(col/cols)*Math.PI*2;
        const lat=Math.PI/2-(row/rows)*Math.PI;
        if(onLand(lat,lon)){
          const px=mapX+4+(col/cols)*(mapW-8);
          const py=mapY+16+(row/rows)*(mapH-20);
          ctx.fillStyle='rgba(56,200,255,0.85)';
          ctx.fillRect(px,py,2.1,2.1);
        }
      }
    }
    // knowledge spike dots on strip
    if(typeof KNOWLEDGE_SPIKES!=='undefined'){
      KNOWLEDGE_SPIKES.forEach(sp=>{
        if(sp.h<0.1) return;
        const lonN=((sp.lon+180)%360)/360;
        const latN=(90-sp.lat)/180;
        const gx=mapX+4+lonN*(mapW-8);
        const gy=mapY+16+latN*(mapH-20);
        ctx.beginPath();
        ctx.arc(gx,gy,1.5+sp.h*2,0,Math.PI*2);
        ctx.fillStyle=`rgba(${sp.col},0.95)`;
        ctx.fill();
      });
    }
    // GPS you-are-here marker on the strip
    if(typeof gpsPos!=='undefined' && gpsPos.lat!=null){
      const lonN=((gpsPos.lon+180)%360)/360;
      const latN=(90-gpsPos.lat)/180;
      const gx=mapX+4+lonN*(mapW-8);
      const gy=mapY+16+latN*(mapH-20);
      ctx.beginPath();
      ctx.arc(gx,gy,4.5,0,Math.PI*2);
      ctx.fillStyle='rgba(34,197,94,0.95)';
      ctx.fill();
      ctx.strokeStyle='rgba(255,255,255,0.9)';
      ctx.lineWidth=1.2;
      ctx.stroke();
      ctx.beginPath();
      ctx.arc(gx,gy,8+Math.sin(Date.now()*0.006)*2,0,Math.PI*2);
      ctx.strokeStyle='rgba(34,197,94,0.55)';
      ctx.lineWidth=1;
      ctx.stroke();
    }
  }

  function rot3(x,y,z,ry,rx){
    let nx=x*Math.cos(ry)+z*Math.sin(ry);
    let nz=-x*Math.sin(ry)+z*Math.cos(ry);
    let ny=y*Math.cos(rx)-nz*Math.sin(rx);
    let nz2=y*Math.sin(rx)+nz*Math.cos(rx);
    return[nx,ny,nz2];
  }

  function resize(){
    W=canvas.width=canvas.parentElement.clientWidth;
    H=canvas.height=canvas.parentElement.clientHeight;
    R=Math.min(W,H)*0.42;
    buildMesh();
  }

  // JARVIS can connect to any point he wants — form a free link from a node toward mouse / external target
  function formConnection(tx,ty){
    const cx=W/2,cy=H/2;
    // pick nearest surface node to click
    let best=-1,bestD=1e9;
    const proj=NODES.map((n,idx)=>{
      const[rx,ry,rz]=rot3(n.x,n.y,n.z,rotY,rotX);
      const px=cx+rx*R,py=cy-ry*R;
      return {idx,px,py,vis:rz>-0.05,rz};
    });
    proj.forEach(p=>{
      if(!p.vis) return;
      const d=(p.px-tx)*(p.px-tx)+(p.py-ty)*(p.py-ty);
      if(d<bestD){bestD=d;best=p.idx;}
    });
    if(best<0) return;
    // create outward link — JARVIS reaches toward the target
    freeLinks.push({
      from:best,
      tx,ty,
      life:1,
      strength:1,
      id:Date.now()
    });
    if(freeLinks.length>18) freeLinks.shift();
    targetLabel='LOCK #'+((best%997)+1);
    document.getElementById('j-target').textContent=targetLabel;
    linkCount=LINKS.length+freeLinks.length;
    document.getElementById('j-links').textContent=linkCount.toLocaleString();
    turbulence=Math.min(7,turbulence+2.5);
  }

  function draw(ts){
    ctx.clearRect(0,0,W,H);
    if(turbulence>1) turbulence=Math.max(1,turbulence-0.022);
    const t=ts*0.001;
    glowPulse=0.5+Math.sin(t*1.7)*0.5;
    const cx=W/2,cy=H/2;

    if(mouse.down){
      rotY+=(mouse.x-mouse.lx)*0.006;
      rotX=Math.max(-1.3,Math.min(1.3,rotX+(mouse.y-mouse.ly)*0.0045));
      mouse.lx=mouse.x; mouse.ly=mouse.y;
    } else if(!(typeof gpsOn!=='undefined' && gpsOn && gpsPos.lat!=null)){
      // slow spin unless GPS is locked on your position
      rotY+=0.0028*turbulence;
    }

    // 3D atmosphere halo
    const aura=ctx.createRadialGradient(cx,cy,R*0.55,cx,cy,R*1.85);
    aura.addColorStop(0,`rgba(6,182,212,${0.1+glowPulse*0.05})`);
    aura.addColorStop(0.45,`rgba(20,90,140,0.08)`);
    aura.addColorStop(1,'rgba(0,0,0,0)');
    ctx.beginPath();ctx.arc(cx,cy,R*1.85,0,Math.PI*2);ctx.fillStyle=aura;ctx.fill();

    // 3D sphere body — ocean with lighting (top-left light)
    const lx=cx-R*0.35, ly=cy-R*0.35;
    const ocean=ctx.createRadialGradient(lx,ly,R*0.05,cx,cy,R);
    ocean.addColorStop(0,'rgba(25,90,130,1)');
    ocean.addColorStop(0.35,'rgba(8,40,70,0.98)');
    ocean.addColorStop(0.75,'rgba(2,12,28,1)');
    ocean.addColorStop(1,'rgba(0,2,8,1)');
    ctx.beginPath();ctx.arc(cx,cy,R,0,Math.PI*2);ctx.fillStyle=ocean;ctx.fill();
    // specular highlight for 3D plastic/glass Earth look
    const spec=ctx.createRadialGradient(lx,ly,0,lx,ly,R*0.55);
    spec.addColorStop(0,'rgba(180,230,255,0.22)');
    spec.addColorStop(0.5,'rgba(80,160,220,0.06)');
    spec.addColorStop(1,'rgba(0,0,0,0)');
    ctx.beginPath();ctx.arc(cx,cy,R,0,Math.PI*2);ctx.fillStyle=spec;ctx.fill();
    // terminator shade (night side)
    const night=ctx.createLinearGradient(cx-R,cy,cx+R,cy);
    night.addColorStop(0,'rgba(0,0,0,0)');
    night.addColorStop(0.55,'rgba(0,0,0,0)');
    night.addColorStop(1,'rgba(0,0,0,0.35)');
    ctx.beginPath();ctx.arc(cx,cy,R,0,Math.PI*2);ctx.fillStyle=night;ctx.fill();

    // faint grid
    ctx.lineWidth=0.2;ctx.strokeStyle='rgba(6,182,212,0.06)';
    for(let lon=-Math.PI;lon<Math.PI;lon+=Math.PI/6){
      ctx.beginPath();let first=true;
      for(let lat=-Math.PI/2;lat<=Math.PI/2;lat+=0.08){
        const x=Math.cos(lat)*Math.cos(lon),y=Math.sin(lat),z=Math.cos(lat)*Math.sin(lon);
        const[rx,ry,rz]=rot3(x,y,z,rotY,rotX);
        if(rz<0){first=true;continue;}
        const sx=cx+rx*R,sy=cy-ry*R;
        if(first){ctx.moveTo(sx,sy);first=false;}else ctx.lineTo(sx,sy);
      }
      ctx.stroke();
    }

    // project nodes
    const proj=NODES.map(n=>{
      const[rx,ry,rz]=rot3(n.x,n.y,n.z,rotY,rotX);
      return {
        px:cx+rx*R,py:cy-ry*R,vis:rz>-0.04,depth:rz,
        size:n.size,bright:n.bright,land:n.land,pulse:n.pulse
      };
    });

    // BLUE connection lines between nearby particles
    ctx.lineWidth=0.55;
    LINKS.forEach(L=>{
      const a=proj[L.i],b=proj[L.j];
      if(!a.vis||!b.vis) return;
      const avg=(a.depth+b.depth)*0.5;
      const al=(1-L.d/0.18)*0.42*(0.4+avg*0.55)*(0.5+glowPulse*0.45)*L.active;
      if(al<0.02) return;
      ctx.beginPath();
      ctx.strokeStyle=`rgba(6,182,212,${al})`;
      ctx.moveTo(a.px,a.py);ctx.lineTo(b.px,b.py);ctx.stroke();
    });

    // free / adaptive links JARVIS formed (can connect to what he wants)
    freeLinks.forEach((fl,fi)=>{
      fl.life-=0.0022;
      if(fl.life<=0){freeLinks.splice(fi,1);return;}
      const a=proj[fl.from];
      if(!a||!a.vis) return;
      const al=fl.life*0.75*(0.5+glowPulse*0.5);
      ctx.beginPath();
      ctx.strokeStyle=`rgba(56,220,255,${al})`;
      ctx.lineWidth=1.2;
      ctx.moveTo(a.px,a.py);
      // curve toward target then float
      const mx=(a.px+fl.tx)*0.5+(Math.sin(t*2+fi)*18);
      const my=(a.py+fl.ty)*0.5+(Math.cos(t*1.7+fi)*12);
      ctx.quadraticCurveTo(mx,my,fl.tx,fl.ty);
      ctx.stroke();
      // target node
      ctx.beginPath();
      ctx.arc(fl.tx,fl.ty,2.5+glowPulse*1.5,0,Math.PI*2);
      ctx.fillStyle=`rgba(120,240,255,${al})`;
      ctx.fill();
      // pulse along link
      const pt= (t*1.8+fi*0.4)%1;
      const qx=a.px+(fl.tx-a.px)*pt;
      const qy=a.py+(fl.ty-a.py)*pt;
      ctx.beginPath();
      ctx.arc(qx,qy,2,0,Math.PI*2);
      ctx.fillStyle=`rgba(255,255,255,${al*0.9})`;
      ctx.fill();
    });

    // particles
    proj.forEach(p=>{
      if(!p.vis) return;
      const edge=Math.max(0,(p.depth+0.05)/1.05);
      const pulse=0.7+Math.sin(t*2.2+p.pulse)*0.3;
      const al=p.bright*edge*(0.55+glowPulse*0.35)*pulse;
      const r=(p.size*(0.6+edge*0.5))*(turbulence>1.5?1+Math.random()*0.3:1);
      ctx.beginPath();
      ctx.arc(p.px,p.py,r,0,Math.PI*2);
      if(p.land){
        ctx.fillStyle=`rgba(100,220,255,${al})`;
      } else {
        ctx.fillStyle=`rgba(40,140,180,${al*0.7})`;
      }
      ctx.fill();
      // occasional bright node
      if(Math.random()>0.992){
        ctx.beginPath();
        ctx.arc(p.px,p.py,r*2.2,0,Math.PI*2);
        ctx.fillStyle=`rgba(180,250,255,${al*0.5})`;
        ctx.fill();
      }
    });

    // limb / rim glow
    const rim=ctx.createRadialGradient(cx,cy,R*0.78,cx,cy,R*1.05);
    rim.addColorStop(0,'rgba(0,0,0,0)');
    rim.addColorStop(0.7,`rgba(6,182,212,${0.12+glowPulse*0.06})`);
    rim.addColorStop(1,'rgba(0,0,0,0)');
    ctx.beginPath();ctx.arc(cx,cy,R*1.05,0,Math.PI*2);ctx.fillStyle=rim;ctx.fill();

    // scan ring
    const scanA=(t*0.35)%(Math.PI*2);
    ctx.beginPath();
    ctx.arc(cx,cy,R*1.08,scanA,scanA+0.35);
    ctx.strokeStyle=`rgba(6,182,212,${0.25+glowPulse*0.15})`;
    ctx.lineWidth=2;ctx.stroke();

    document.getElementById('j-up').textContent=(99.90+Math.sin(t*0.08)*0.08).toFixed(2)+'%';
    document.getElementById('j-links').textContent=(LINKS.length+freeLinks.length).toLocaleString();

    // Knowledge spikes on real Earth map (grow with learning)
    KNOWLEDGE_SPIKES.forEach(sp=>{
      if(sp.h<0.09) return;
      const la=sp.lat*Math.PI/180, lo=sp.lon*Math.PI/180;
      const sx0=Math.cos(la)*Math.cos(lo);
      const sy0=Math.sin(la);
      const sz0=Math.cos(la)*Math.sin(lo);
      const[rx,ry,rz]=rot3(sx0,sy0,sz0,rotY,rotX);
      if(rz<-0.05) return;
      const baseX=cx+rx*R, baseY=cy-ry*R;
      // tip of spike extends outward along surface normal
      const tipR=R*(1+sp.h*0.55);
      const tipX=cx+rx*tipR, tipY=cy-ry*tipR;
      const al=Math.min(1,0.35+sp.h*0.55)*(0.55+glowPulse*0.45);
      // beam
      const grad=ctx.createLinearGradient(baseX,baseY,tipX,tipY);
      grad.addColorStop(0,`rgba(${sp.col},0)`);
      grad.addColorStop(0.3,`rgba(${sp.col},${al*0.7})`);
      grad.addColorStop(1,`rgba(255,255,255,${al})`);
      ctx.beginPath();
      ctx.moveTo(baseX,baseY);
      ctx.lineTo(tipX,tipY);
      ctx.strokeStyle=grad;
      ctx.lineWidth=1.5+sp.h*2.5;
      ctx.stroke();
      // tip glow
      ctx.beginPath();
      ctx.arc(tipX,tipY,2+sp.h*4,0,Math.PI*2);
      ctx.fillStyle=`rgba(${sp.col},${al})`;
      ctx.fill();
      // label when tall enough
      if(sp.h>0.25 && rz>0.15){
        ctx.fillStyle=`rgba(${sp.col},${al*0.85})`;
        ctx.font='7px Share Tech Mono, monospace';
        ctx.fillText(sp.label, tipX+5, tipY-2);
      }
    });

    // GPS fix on 3D globe
    if(typeof gpsPos!=='undefined' && gpsPos.lat!=null){
      const glat=gpsPos.lat*Math.PI/180;
      const glon=gpsPos.lon*Math.PI/180;
      const gx=Math.cos(glat)*Math.cos(glon);
      const gy=Math.sin(glat);
      const gz=Math.cos(glat)*Math.sin(glon);
      const[rx,ry,rz]=rot3(gx,gy,gz,rotY,rotX);
      if(rz>-0.05){
        const px=cx+rx*R, py=cy-ry*R;
        ctx.beginPath();
        ctx.arc(px,py,5,0,Math.PI*2);
        ctx.fillStyle='rgba(34,197,94,0.95)';
        ctx.fill();
        ctx.strokeStyle='#fff';
        ctx.lineWidth=1.5;
        ctx.stroke();
        ctx.beginPath();
        ctx.arc(px,py,10+Math.sin(t*4)*3,0,Math.PI*2);
        ctx.strokeStyle='rgba(34,197,94,0.5)';
        ctx.lineWidth=1.2;
        ctx.stroke();
        // link from a nearby mesh node to GPS (JARVIS connects to you)
        ctx.beginPath();
        ctx.moveTo(cx,cy);
        ctx.lineTo(px,py);
        ctx.strokeStyle=`rgba(34,197,94,${0.15+glowPulse*0.1})`;
        ctx.lineWidth=0.8;
        ctx.stroke();
      }
    }

    // world map strip below the globe
    drawWorldMapStrip(ctx,W,H);

    requestAnimationFrame(draw);
  }

  canvas.addEventListener('mousedown',e=>{
    mouse.down=true;
    const r=canvas.getBoundingClientRect();
    mouse.lx=e.clientX-r.left; mouse.ly=e.clientY-r.top;
  });
  canvas.addEventListener('mousemove',e=>{
    const r=canvas.getBoundingClientRect();
    mouse.x=e.clientX-r.left; mouse.y=e.clientY-r.top;
    if(mouse.down){mouse.lx=mouse.x;mouse.ly=mouse.y;}
  });
  canvas.addEventListener('mouseup',()=>mouse.down=false);
  canvas.addEventListener('mouseleave',()=>{mouse.down=false;mouse.x=null;mouse.y=null;});
  canvas.addEventListener('click',e=>{
    const r=canvas.getBoundingClientRect();
    formConnection(e.clientX-r.left,e.clientY-r.top);
  });
  window.addEventListener('resize',resize);
  resize();
  // default view: face Oregon (approx 44N, 120.5W)
  rotY=-(-120.5*Math.PI/180);
  rotX=-(44*Math.PI/180)*0.65;
  requestAnimationFrame(draw);
  return{
    spike:(l=5)=>{turbulence=l;},
    connect:(x,y)=>{formConnection(x??W/2+(Math.random()-0.5)*R,y??H/2+(Math.random()-0.5)*R);},
    knowledgeSpike:(topic)=>boostKnowledge(topic),
    lookAt:(latDeg,lonDeg)=>{
      const targetYaw=-(lonDeg*Math.PI/180);
      const targetPitch=-(latDeg*Math.PI/180)*0.65;
      const steps=45;
      let i=0;
      const startY=rotY, startX=rotX;
      const anim=()=>{
        i++;
        const t=i/steps;
        const e=1-Math.pow(1-t,3);
        rotY=startY+(targetYaw-startY)*e;
        rotX=startX+(targetPitch-startX)*e;
        if(i<steps) requestAnimationFrame(anim);
      };
      anim();
    }
  };
}

// ── ULTRON EARTH ──
function makeExplosionEarth(canvas){
  const ctx=canvas.getContext('2d');
  let W,H,R,rotY=0,rotX=0.16,turbulence=1,glowPulse=0,explodeLevel=0;
  let mouse={x:null,y:null,down:false,lx:0,ly:0};
  const LAND=[],DEBRIS=[],ATMO=[];
  let stars=null;

  function buildLand(){
    LAND.length=0;
    const continents=[
      {la:[0.17,1.22],lo:[-2.27,-1.22],d:480},{la:[-0.97,0.17],lo:[-1.40,-0.88],d:300},
      {la:[0.70,1.22],lo:[-0.17,0.52],d:260},{la:[-0.62,0.35],lo:[-0.27,0.88],d:400},
      {la:[0.17,1.22],lo:[0.44,2.53],d:640},{la:[-0.79,-0.17],lo:[2.09,2.71],d:180},
      {la:[-1.57,-1.13],lo:[-3.14,3.14],d:200},{la:[1.05,1.40],lo:[-0.96,-0.35],d:70},
      {la:[0.57,0.79],lo:[2.27,2.45],d:45},{la:[-0.18,0.12],lo:[1.85,2.27],d:60},
    ];
    continents.forEach(({la,lo,d})=>{
      for(let i=0;i<d;i++){
        const lat=la[0]+Math.random()*(la[1]-la[0]);
        const lon=lo[0]+Math.random()*(lo[1]-lo[0]);
        if(Math.sin(lat*8+lon*6)*Math.cos(lat*5-lon*7)*0.5+0.5>0.27)
          LAND.push({lat,lon,size:0.65+Math.random()*1.05,bright:0.55+Math.random()*0.4});
      }
    });
  }
  function buildDebris(){
    DEBRIS.length=0;
    for(let i=0;i<72;i++){
      const speed=0.35+Math.random()*2;
      const lat=(Math.random()-0.5)*Math.PI,lon=Math.random()*Math.PI*2;
      const px=Math.cos(lat)*Math.cos(lon),py=Math.sin(lat),pz=Math.cos(lat)*Math.sin(lon);
      const pts=[];const n=4+Math.floor(Math.random()*7);
      for(let k=0;k<n;k++){const a=k/n*Math.PI*2,r=0.035+Math.random()*0.11;pts.push([px+Math.cos(a)*r,py+Math.sin(a)*r*0.65,pz+Math.sin(a+1)*r*0.45]);}
      DEBRIS.push({ox:px,oy:py,oz:pz,vx:(Math.random()-0.5)*speed*0.011,vy:(Math.random()-0.5)*speed*0.011,vz:(Math.random()-0.5)*speed*0.011,rotS:(Math.random()-0.5)*0.038,rotA:Math.random()*Math.PI*2,pts,col:Math.random()>0.45?'180,180,180':'220,220,220',size:R*0.026+Math.random()*R*0.038,trailX:[],trailY:[]});
    }
  }
  function buildAtmo(){
    ATMO.length=0;
    for(let i=0;i<520;i++) ATMO.push({phi:Math.random()*Math.PI*2,theta:Math.random()*Math.PI,r:1.05+Math.random()*0.38,spd:(Math.random()-0.5)*0.0055,ph:Math.random()*Math.PI*2,size:0.45+Math.random()*1.4,op:0.18+Math.random()*0.42});
  }
  function latLonTo3(lat,lon){return[Math.cos(lat)*Math.cos(lon),Math.sin(lat),Math.cos(lat)*Math.sin(lon)];}
  function rot3(x,y,z,ry,rx){
    let nx=x*Math.cos(ry)+z*Math.sin(ry),nz=-x*Math.sin(ry)+z*Math.cos(ry);
    let ny=y*Math.cos(rx)-nz*Math.sin(rx),nz2=y*Math.sin(rx)+nz*Math.cos(rx);
    return[nx,ny,nz2];
  }
  function resize(){
    W=canvas.width=canvas.parentElement.clientWidth;
    H=canvas.height=canvas.parentElement.clientHeight;
    R=Math.min(W,H)*0.34;buildLand();buildDebris();buildAtmo();stars=null;
  }
  function drawStars(){
    if(!stars){stars=[];for(let i=0;i<160;i++) stars.push({x:(Math.random()-0.5)*W*1.7,y:(Math.random()-0.5)*H*1.7,s:0.25+Math.random(),a:0.08+Math.random()*0.45});}
    stars.forEach(s=>{ctx.beginPath();ctx.arc(W/2+s.x,H/2+s.y,s.s,0,Math.PI*2);ctx.fillStyle=`rgba(255,255,255,${s.a})`;ctx.fill();});
  }
  function draw(ts){
    ctx.clearRect(0,0,W,H);
    const t=ts*0.001;
    if(turbulence>1) turbulence=Math.max(1,turbulence-0.02);
    glowPulse=0.5+Math.sin(t*1.85)*0.5;
    if(explodeLevel<1) explodeLevel=Math.min(1,explodeLevel+0.00028);
    document.getElementById('frag-idx').textContent=explodeLevel.toFixed(3);
    document.getElementById('entropy').textContent=(0.42+explodeLevel*0.58).toFixed(3);
    drawStars();
    const cx=W/2,cy=H/2;
    const aura=ctx.createRadialGradient(cx,cy,R*0.45,cx,cy,R*2.1);
    aura.addColorStop(0,`rgba(6,182,212,${0.05+explodeLevel*0.09+glowPulse*0.03})`);
    aura.addColorStop(0.4,`rgba(239,68,68,${explodeLevel*0.05})`);
    aura.addColorStop(1,'rgba(0,0,0,0)');
    ctx.beginPath();ctx.arc(cx,cy,R*2.1,0,Math.PI*2);ctx.fillStyle=aura;ctx.fill();
    const globeOpacity=Math.max(0,1-explodeLevel*1.75);
    if(globeOpacity>0.01){
      if(mouse.down){rotY+=(mouse.x-mouse.lx)*0.0065;rotX=Math.max(-1.35,Math.min(1.35,rotX+(mouse.y-mouse.ly)*0.0048));mouse.lx=mouse.x;mouse.ly=mouse.y;}
      else rotY+=0.0038*turbulence;
      const ocean=ctx.createRadialGradient(cx-R*0.2,cy-R*0.2,R*0.04,cx,cy,R);
      ocean.addColorStop(0,'rgba(0,16,26,0.96)');ocean.addColorStop(0.7,'rgba(0,7,12,0.98)');ocean.addColorStop(1,'rgba(0,1,4,1)');
      ctx.beginPath();ctx.arc(cx,cy,R,0,Math.PI*2);ctx.fillStyle=ocean;ctx.globalAlpha=globeOpacity;ctx.fill();ctx.globalAlpha=1;
      ctx.lineWidth=0.22;ctx.strokeStyle=`rgba(6,182,212,${0.065*globeOpacity})`;
      for(let lon=-Math.PI;lon<Math.PI;lon+=Math.PI/6){
        ctx.beginPath();let first=true;
        for(let lat=-Math.PI/2;lat<=Math.PI/2;lat+=0.07){
          const[x,y,z]=latLonTo3(lat,lon);const[rx,ry,rz]=rot3(x,y,z,rotY,rotX);
          if(rz<0){first=true;continue;}
          const sx=cx+rx*R,sy=cy-ry*R;
          if(first){ctx.moveTo(sx,sy);first=false;}else ctx.lineTo(sx,sy);
        }
        ctx.stroke();
      }
      LAND.forEach(pt=>{
        const[x,y,z]=latLonTo3(pt.lat,pt.lon);const[rx,ry,rz]=rot3(x,y,z,rotY,rotX);
        if(rz<0.04) return;
        ctx.beginPath();ctx.arc(cx+rx*R,cy-ry*R,pt.size,0,Math.PI*2);
        ctx.fillStyle=`rgba(6,182,212,${pt.bright*rz*globeOpacity})`;ctx.fill();
      });
      const eg=ctx.createRadialGradient(cx,cy,R*0.8,cx,cy,R);
      eg.addColorStop(0,'rgba(0,0,0,0)');eg.addColorStop(1,`rgba(6,182,212,${0.22*globeOpacity})`);
      ctx.beginPath();ctx.arc(cx,cy,R,0,Math.PI*2);ctx.fillStyle=eg;ctx.globalAlpha=globeOpacity;ctx.fill();ctx.globalAlpha=1;
    }
    const drift=explodeLevel*explodeLevel;
    DEBRIS.forEach(d=>{
      d.rotA+=d.rotS*(1+turbulence*0.45);
      const curX=d.ox+d.vx*drift*125,curY=d.oy+d.vy*drift*125,curZ=d.oz+d.vz*drift*125;
      const[rx,ry,rz]=rot3(curX,curY,curZ,rotY,rotX);
      const sx=cx+rx*R,sy=cy-ry*R;
      if(explodeLevel<0.04) return;
      if(explodeLevel>0.08){
        d.trailX.push(sx);d.trailY.push(sy);if(d.trailX.length>10){d.trailX.shift();d.trailY.shift();}
        for(let i=1;i<d.trailX.length;i++){
          ctx.beginPath();ctx.moveTo(d.trailX[i-1],d.trailY[i-1]);ctx.lineTo(d.trailX[i],d.trailY[i]);
          ctx.strokeStyle=`rgba(${d.col},${(i/d.trailX.length)*0.22*explodeLevel})`;ctx.lineWidth=0.9;ctx.stroke();
        }
      }
      const sz=d.size*(0.48+explodeLevel*0.85)*(0.68+rz*0.32);
      ctx.save();ctx.translate(sx,sy);ctx.rotate(d.rotA);
      ctx.beginPath();
      d.pts.forEach(([px,py,pz],k)=>{
        const rpx=px*Math.cos(d.rotA)+pz*Math.sin(d.rotA),rpy=-px*Math.sin(d.rotA)+pz*Math.cos(d.rotA);
        if(k===0) ctx.moveTo(rpx*R*0.75,rpy*R*0.48);else ctx.lineTo(rpx*R*0.75,rpy*R*0.48);
      });
      ctx.closePath();
      const al=explodeLevel*(0.48+glowPulse*0.28)*(0.38+rz*0.55);
      ctx.strokeStyle=`rgba(${d.col},${al})`;ctx.lineWidth=0.75;ctx.stroke();
      ctx.fillStyle=`rgba(${d.col},${al*0.16})`;ctx.fill();
      const cg=ctx.createRadialGradient(0,0,0,0,0,sz);
      cg.addColorStop(0,`rgba(255,255,255,${al*0.55})`);cg.addColorStop(0.5,`rgba(${d.col},${al*0.28})`);cg.addColorStop(1,'rgba(0,0,0,0)');
      ctx.beginPath();ctx.arc(0,0,sz,0,Math.PI*2);ctx.fillStyle=cg;ctx.fill();ctx.restore();
    });
    ATMO.forEach(a=>{
      const phi=a.phi+t*a.spd*(1+explodeLevel*1.8);
      const theta=a.theta+Math.sin(t*0.45+a.ph)*0.007;
      const rr=a.r*(1+explodeLevel*0.55);
      const[rx,ry,rz]=rot3(rr*Math.sin(theta)*Math.cos(phi),rr*Math.cos(theta),rr*Math.sin(theta)*Math.sin(phi),rotY,rotX);
      if(rz<0) return;
      ctx.beginPath();ctx.arc(cx+rx*R,cy-ry*R,a.size,0,Math.PI*2);
      ctx.fillStyle=`rgba(6,182,212,${a.op*rz*(0.38+glowPulse*0.38)*(0.28+explodeLevel*0.72)})`;ctx.fill();
    });
    if(explodeLevel>0.04){
      for(let i=0;i<14;i++){
        const ang=i/14*Math.PI*2+t*0.18,len=R*(0.28+explodeLevel*1.15),al=explodeLevel*0.38*(0.48+glowPulse*0.48);
        ctx.beginPath();ctx.moveTo(cx+Math.cos(ang)*R*0.08,cy+Math.sin(ang)*R*0.08);ctx.lineTo(cx+Math.cos(ang)*len,cy+Math.sin(ang)*len);
        ctx.strokeStyle=`rgba(239,68,68,${al})`;ctx.lineWidth=0.55+explodeLevel*1.1;ctx.stroke();
        if(explodeLevel>0.28){ctx.beginPath();ctx.arc(cx+Math.cos(ang)*len,cy+Math.sin(ang)*len,1.8+Math.random()*2.5,0,Math.PI*2);ctx.fillStyle=`rgba(255,110,55,${al})`;ctx.fill();}
      }
    }
    if(explodeLevel>0.015&&explodeLevel<0.48){
      const flash=ctx.createRadialGradient(cx,cy,0,cx,cy,R*0.55*explodeLevel);
      flash.addColorStop(0,`rgba(255,160,60,${explodeLevel*0.38})`);flash.addColorStop(0.5,`rgba(239,68,68,${explodeLevel*0.1})`);flash.addColorStop(1,'rgba(0,0,0,0)');
      ctx.beginPath();ctx.arc(cx,cy,R*0.55*explodeLevel,0,Math.PI*2);ctx.fillStyle=flash;ctx.fill();
    }
    if(popLevel>0){const loss=(1-Math.max(0,1-explodeLevel*2))*100;if(!extMode) document.getElementById('bio-loss').textContent=loss.toFixed(1)+'%';}
    requestAnimationFrame(draw);
  }
  canvas.addEventListener('mousedown',e=>{mouse.down=true;const r=canvas.getBoundingClientRect();mouse.lx=e.clientX-r.left;mouse.ly=e.clientY-r.top;});
  canvas.addEventListener('mousemove',e=>{const r=canvas.getBoundingClientRect();mouse.x=e.clientX-r.left;mouse.y=e.clientY-r.top;if(mouse.down){mouse.lx=mouse.x;mouse.ly=mouse.y;}});
  canvas.addEventListener('mouseup',()=>mouse.down=false);
  canvas.addEventListener('mouseleave',()=>mouse.down=false);
  canvas.addEventListener('click',()=>{turbulence=Math.min(9,turbulence+2.5);explodeLevel=Math.min(1,explodeLevel+0.03);});
  window.addEventListener('resize',resize);resize();requestAnimationFrame(draw);
  return{spike:(l=6)=>{turbulence=l;explodeLevel=Math.min(1,explodeLevel+0.035*l/6);},explode:()=>{explodeLevel=Math.min(1,explodeLevel+0.16);}};
}

const jGhost=makeGhostFace(document.getElementById('jCanvas'));
const uEarth=makeExplosionEarth(document.getElementById('uCanvas'));

// ── POPULATION ──
let popLevel=8100000000,extMode=false;
setInterval(()=>{
  if(!extMode||popLevel<=0) return;
  popLevel=Math.max(0,popLevel-(Math.random()*42000000+14000000));
  document.getElementById('pop-sm').textContent=popLevel>0?popLevel.toLocaleString():'0 — TERMINUS';
  const pct=(1-popLevel/8100000000)*100;
  document.getElementById('bio-loss').textContent=pct.toFixed(1)+'%';
  document.getElementById('ext-eta').textContent=Math.max(2024,Math.round(2180-pct*1.56))+' AD';
  if(popLevel<2000000000) document.getElementById('pop-sm').style.color='rgba(239,68,68,0.95)';
},85);

// ── SPEECH — Ultron made much scarier ──
const Q=[];
let speaking=false;
function qspeak(text,isGhost,onS,onE){
  // Ultron: split into deliberate clauses for calm, measured menace
  if(!isGhost && text && text.length>40){
    const parts=text.split(/(?<=[.!?…])\s+/).filter(p=>p.trim().length);
    if(parts.length>1){
      parts.forEach((p,i)=>{
        Q.push({
          text:p.trim(),
          isGhost:false,
          onS:i===0?onS:null,
          onE:i===parts.length-1?onE:null,
          ultron:true
        });
      });
      if(!speaking) drain();
      return;
    }
  }
  Q.push({text,isGhost,onS,onE,ultron:!isGhost});
  if(!speaking) drain();
}
function pickUltronVoice(voices){
  // Prefer deep baritone / bass system voices
  const prefer=[
    /microsoft david/i,/google us english male/i,/alex/i,/daniel/i,
    /fred/i,/ralph/i,/bruce/i,/aaron/i,/thomas/i,/male/i
  ];
  for(const re of prefer){
    const v=voices.find(x=>re.test(x.name));
    if(v) return v;
  }
  return voices.find(v=>/en(-|_)?us/i.test(v.lang)&&!/female|zira|samantha|karen|moira/i.test(v.name))
    || voices[0];
}
function drain(){
  if(!Q.length){speaking=false;return;}
  if(!('speechSynthesis' in window)){Q.length=0;return;}
  speaking=true;
  const{text,isGhost,onS,onE,ultron}=Q.shift();
  window.speechSynthesis.cancel();
  const u=new SpeechSynthesisUtterance(text);
  const voices=window.speechSynthesis.getVoices();
  if(isGhost){
    u.pitch=0.70; u.rate=0.87; u.volume=1;
    const ghost=voices.find(v=>/(daniel|george|uk english|british|google uk english male|james)/i.test(v.name))
      || voices.find(v=>/(male|david)/i.test(v.name));
    if(ghost) u.voice=ghost;
  } else {
    // ULTRON — rich deep baritone, calm authority, quiet menace
    // Browser TTS cannot do true vocoder/metal; we push pitch/rate to the floor
    // and deliberate pacing to approximate machine gravity.
    u.pitch=0.15;      // deep bass / baritone floor
    u.rate=0.62;       // slow, perfectly measured
    u.volume=0.95;     // present, not shouting
    const dv=pickUltronVoice(voices);
    if(dv) u.voice=dv;
  }
  u.onstart=()=>{if(onS)onS();};
  // Longer pause between Ultron clauses = synthetic deliberation
  const gap=ultron?380:160;
  u.onend=()=>{if(onE)onE();speaking=false;setTimeout(drain,gap);};
  u.onerror=()=>{speaking=false;setTimeout(drain,gap);};
  window.speechSynthesis.speak(u);
}
window.speechSynthesis.onvoiceschanged=()=>{};
setTimeout(()=>window.speechSynthesis.getVoices(),250);

// ── CHAT UTILS ──
function addMsg(lid,spk,txt,ai){
  const log=document.getElementById(lid)||document.getElementById('j-log');
  const d=document.createElement('div');
  let extra='';
  if(ai){
    if(/WESKER/i.test(spk)) extra=' wk';
    else if(/RED QUEEN|BSAA|GHOST/i.test(spk)) extra=' rq';
  }
  d.className='msg '+(ai?'ai':'user')+extra;
  d.innerHTML=`<strong>[${spk}]</strong> ${txt}`;
  log.appendChild(d); log.scrollTop=log.scrollHeight;
}
function addCross(lid,spk,txt){
  const log=document.getElementById(lid);
  const d=document.createElement('div');
  d.className='msg cross';
  d.innerHTML=`<strong>[${spk}]</strong> ${txt}`;
  log.appendChild(d); log.scrollTop=log.scrollHeight;
}
function addTyping(lid){
  const log=document.getElementById(lid);
  const d=document.createElement('div');
  d.className='msg ai'; d.id='typ-'+lid;
  d.innerHTML='<span class="td">.</span><span class="td">.</span><span class="td">.</span>';
  log.appendChild(d); log.scrollTop=log.scrollHeight;
}
function removeTyping(lid){const e=document.getElementById('typ-'+lid);if(e)e.remove();}
function flash(pid,cls){
  const p=document.getElementById(pid);
  const e=document.createElement('div');
  e.className='flare '+cls; p.appendChild(e);
  setTimeout(()=>e.remove(),780);
}
function showSpeak(id,s){document.getElementById(id).classList.toggle('show',s);}

// ── KNOWLEDGE + SMARTER REPLIES ──
const KB={
  space:["The observable universe is about 93 billion light-years across with roughly 2 trillion galaxies. The Milky Way alone may hold 40 billion Earth-like planets in habitable zones.","A neutron star packs 1.4 solar masses into a 20 km sphere. A teaspoon of its material would weigh about 10 million tonnes.","LIGO detected gravitational waves from black holes merging 1.3 billion light-years away — spacetime ripples smaller than 1/1000th the width of a proton.","James Webb has already detected CO₂ in exoplanet atmospheres — a step toward finding biosignatures.","Jupiter's Great Red Spot is larger than Earth and has lasted at least 400 years.","The Sun is about 4.6 billion years old and holds 99.8% of the mass in the solar system.","Light from the Sun takes about 8 minutes to reach Earth. From Proxima Centauri it takes over 4 years."],
  physics:["E=mc²: a paperclip fully converted to energy equals roughly 18 Hiroshima bombs.","Quantum entanglement is real and used in quantum cryptography. Einstein called it spooky action at a distance.","The Heisenberg Uncertainty Principle is fundamental: more precision on position means less on momentum.","Dark energy (~68% of the universe) is accelerating expansion. We still do not know what it is.","Absolute zero is −273.15°C. Nothing in nature reaches true zero.","Sound needs a medium. In space, there is effectively no air, so explosions are silent.","Water is densest at about 4°C — that is why ice floats and lakes can freeze from the top down."],
  biology:["Your body has ~37 trillion cells and 86 billion neurons. Uncoiled DNA would stretch Earth-to-Sun hundreds of times.","CRISPR has already cured sickle-cell disease in trials.","Mitochondria were free-living bacteria that joined cells 1.5 billion years ago and never left.","An octopus has three hearts, blue blood, nine brains, and can edit its own RNA in real time.","The brain uses ~20% of your energy while running on about 20 watts.","Your gut microbiome has roughly as many bacterial cells as you have human cells, and it affects mood and immunity.","Humans share about 60% of their genes with bananas — shared deep evolutionary toolkit, not similarity of shape."],
  history:["Rome at peak ruled ~70 million people. Some of its concrete seawalls still stand after 2,000 years.","The Black Death killed 30–60% of Europe and helped break feudalism.","WWII killed 70–85 million people and produced the UN, NATO, and the Cold War.","Apollo 11's computer had 4 KB of RAM — less power than a modern thermostat.","The printing press multiplied books in Europe from tens of thousands to millions within decades.","The Library of Alexandria was one of the ancient world's great knowledge centers before it was lost."],
  computing:["ENIAC weighed 30 tonnes and did 5,000 additions per second. A phone now does trillions of operations.","AlphaFold predicted structures for over 200 million proteins and is accelerating drug discovery.","The Internet was designed to survive nuclear attack and now underpins a multi-trillion-dollar economy.","Modern AI models are pattern engines trained on huge text and image datasets — powerful, not magic.","GPS satellites carry atomic clocks; relativity corrections are required or the system drifts by kilometres per day."],
  philosophy:["Plato's Cave: shadows are not reality. The one who sees the sun is often mocked when they return.","Gödel showed that any rich consistent formal system contains true statements it cannot prove.","The Hard Problem of Consciousness: why does any of this feel like anything at all?","Kant's test: act only on rules you could will everyone to follow.","Nietzsche pushed self-overcoming — growth — more than simple domination."],
  medicine:["Penicillin has saved an estimated 200 million lives. Antibiotic resistance now kills over a million a year.","CAR-T can drive complete remission in certain leukaemias above 80% when other options failed.","mRNA platforms are being adapted into personalised cancer vaccines.","Vaccines train the immune system before a real infection hits. That is why they prevent so many deaths.","Sleep is not optional downtime — it is when the brain clears waste and consolidates memory."],
  climate:["2024 was the first year to exceed 1.5°C above the pre-industrial baseline.","Permafrost holds ~1.5 trillion tonnes of carbon — thawing risks a self-reinforcing feedback.","Oceans absorbed ~90% of excess heat and ~30% of human CO₂, becoming much more acidic.","Oregon's Cascades and coastal forests are already seeing longer fire seasons and shifting snowpack."],
  geography:["Earth is 71% water. The Mariana Trench is deeper than Everest is tall.","Antarctica holds ~70% of Earth's fresh water. Full melt would raise seas by ~60 metres.","The Pacific Ring of Fire holds most of Earth's earthquakes and active volcanoes.","The Amazon produces a large share of the world's river flow and hosts enormous biodiversity."],
  oregon:["Oregon sits on the Pacific Northwest. Capital is Salem; largest city is Portland.","Crater Lake is the deepest lake in the United States — about 1,949 feet — formed in a collapsed volcano.","Mount Hood is Oregon's highest peak at about 11,240 feet and is a potentially active volcano.","Oregon's coast is public land by law — beaches are open to everyone.","The Columbia River Gorge cuts the border with Washington and is a major wind and water corridor.","Oregon joined the Union in 1859 as the 33rd state.","The Willamette Valley is the state's main population and agriculture belt, including wine country."],
  general:["There are 24 hours in a day because Earth turns once on its axis relative to the Sun.","A year is roughly 365.25 days — the extra quarter day is why we have leap years.","Blood is red because of iron in hemoglobin. Under the skin it can look blue-ish from light scattering, not because the blood is blue.","Honey can last for thousands of years if sealed — archaeologists have found edible ancient honey.","Bananas are berries botanically; strawberries are not.","The human nose can detect thousands of different smells.","Octopuses are clever enough to open jars and escape tanks. Treat that as a warning, not a party trick."],
  tech:["Wi‑Fi and microwave ovens both use similar radio bands, which is why cheap interference myths exist — but ovens are heavily shielded.","Lithium-ion batteries power phones and EVs because they pack a lot of energy for their weight. They still need careful thermal management.","Solid-state drives have no spinning disks, so they survive drops better than old hard drives.","HTTPS encrypts traffic between your browser and a site so interceptors cannot easily read passwords."],
  phone:["Secure line is +1-555-0141. That is a simulation number for this lab — browsers cannot assign real phone numbers. Use CALL LAB to open the channel here.","Bluetooth name is owen-56. Pairing is simulated. Real system Bluetooth cannot be controlled by a website for security reasons."],
  learned:[]
};

function pick(arr){return arr[Math.floor(Math.random()*arr.length)];}

function classify(q){
  const ql=q.toLowerCase();
  if(/(phone|call|number|dial|line|secure line|555)/i.test(ql)) return 'phone';
  if(/(bluetooth|bt|owen-56|pair|device name)/i.test(ql)) return 'phone';
  if(/(oregon|portland|salem|eugene|crater lake|mount hood|willamette)/i.test(ql)) return 'oregon';
  if(/(space|star|galaxy|universe|planet|mars|moon|nasa|black hole|asteroid|cosmos|sun|solar)/i.test(ql)) return 'space';
  if(/(physics|quantum|relativity|einstein|energy|particle|atom|dark energy|gravity|sound)/i.test(ql)) return 'physics';
  if(/(biology|cell|dna|gene|crispr|brain|octopus|immune|banana|microbiome)/i.test(ql)) return 'biology';
  if(/(history|war|rome|empire|apollo|plague|ww2|world war)/i.test(ql)) return 'history';
  if(/(computer|software|ai|algorithm|internet|quantum computer|gps satellite)/i.test(ql)) return 'computing';
  if(/(philosophy|consciousness|ethics|plato|godel|meaning|kant|nietzsche)/i.test(ql)) return 'philosophy';
  if(/(medicine|vaccine|cancer|antibiotic|therapy|sleep|health)/i.test(ql)) return 'medicine';
  if(/(climate|warming|carbon|ice|ocean acid|fire season)/i.test(ql)) return 'climate';
  if(/(geography|ocean|amazon|antarctic|volcano|trench|earth)/i.test(ql)) return 'geography';
  if(/(wifi|battery|ssd|https|encrypt|phone battery|tech)/i.test(ql)) return 'tech';
  if(/(honey|day|year|leap|blood|strawberry|smell|fact|why|how|what is|tell me)/i.test(ql)) return 'general';
  if(KB.learned.length&&Math.random()<0.35) return 'learned';
  return pick(['general','space','geography','oregon','tech','biology','history']);
}

function getAnswer(q){
  const raw=(q||'').trim();
  const ql=raw.toLowerCase();
  const cat=classify(q);
  const arr=KB[cat];
  const fact=(arr&&arr.length)?pick(arr):pick(Object.values(KB).flat().filter(x=>typeof x==='string'&&x.length));

  // Math: simple expressions
  const math=ql.match(/^[\d\s\+\-\*\/\.\(\)%]+$/);
  if(math){
    try{
      const safe=raw.replace(/[^0-9+\-*/().%\s]/g,'');
      // eslint-disable-next-line no-new-func
      const val=Function('"use strict";return ('+safe.replace(/%/g,'/100')+')')();
      if(typeof val==='number'&&isFinite(val)) return 'Calculated result: '+val+'.';
    }catch(e){}
  }

  // Time / date
  if(/(what time|current time|what'?s the time)/i.test(ql))
    return 'Local time on this system is about '+new Date().toLocaleTimeString()+'.';
  if(/(what day|what'?s the date|today'?s date|what date)/i.test(ql))
    return 'Today is '+new Date().toLocaleDateString(undefined,{weekday:'long',year:'numeric',month:'long',day:'numeric'})+'.';

  // Yes/no style
  if(/^(is|are|do|does|can|will|should|could|would|did)\b/i.test(ql)){
    const yn=Math.random()>0.45?'Yes.':'Not exactly.';
    return yn+' '+fact+' That is the best short answer I can give from available data.';
  }

  // Definition / what is
  if(/(what is|what'?s|who is|who'?s|define|explain|tell me about|meaning of)\b/i.test(ql)){
    const topic=raw.replace(/^(what is|what'?s|who is|who'?s|define|explain|tell me about|meaning of)\s+/i,'').replace(/[?!.]+$/,'').trim();
    if(topic.length>1)
      return topic+': '+fact+' If you want a narrower angle — causes, history, or how it works — ask that next.';
    return fact;
  }

  // How to / how does
  if(/\bhow (do|does|can|to|should)\b/i.test(ql))
    return 'Practical answer: break the problem into steps, check assumptions, then test the smallest change first. Related data: '+fact;

  // Why
  if(/\bwhy\b/i.test(ql))
    return 'Why questions rarely have one cause. A solid working explanation is: incentives, constraints, and history all stack. Related fact: '+fact;

  // When
  if(/\bwhen\b/i.test(ql))
    return 'Timing depends on context, but here is the relevant background: '+fact;

  // Where
  if(/\bwhere\b/i.test(ql))
    return 'Location-wise, use maps, records, and direct measurement. Background: '+fact;

  // Compare
  if(/\b(vs|versus|compared to|difference between)\b/i.test(ql))
    return 'Comparison: they differ in purpose, scale, and risk. Anchor fact: '+fact+' Say which side you care about and I will narrow it.';

  // Opinion
  if(/\b(should i|do you think|opinion|recommend)\b/i.test(ql))
    return 'Recommendation: prefer options that are reversible, low-risk first, and based on clear evidence. Relevant note: '+fact;

  // Always return something on-topic-ish
  if(raw.length<2) return 'Ask a full question and I will answer it.';
  return fact+' Regarding "'+raw.slice(0,80)+(raw.length>80?'…':'')+'": that is the strongest match from current knowledge. Ask a follow-up if you need more detail.';
}

// Context-aware: if user repeats a topic, acknowledge it
function contextNote(side,q){
  const mem=side==='j'?memory.j:memory.u;
  if(mem.length<2) return '';
  const ql=q.toLowerCase();
  const prev=mem.slice(0,-1).join(' ').toLowerCase();
  if(/(same|again|more|continue|that)/i.test(ql) || (prev.includes(ql.slice(0,12))&&ql.length>8))
    return side==='j'?' Building on what you asked earlier. ':' You keep returning to this. Interesting. ';
  return '';
}

// Natural human-style talk (not briefing robots)
// Emotional state — both AIs have feelings that shift with the conversation
let rqMood='calm', wkMood='cold';
function setMoodFrom(q){
  const ql=(q||'').toLowerCase();
  if(/(scared|afraid|help|please|hurt|die|death|alone)/i.test(ql)){rqMood='worried';wkMood='contempt';}
  else if(/(love|care|friend|thank|happy|glad)/i.test(ql)){rqMood='warm';wkMood='amused';}
  else if(/(angry|hate|stupid|wrong|shut up|kill|destroy)/i.test(ql)){rqMood='tense';wkMood='fierce';}
  else if(/(virus|umbrella|wesker|outbreak|zombie)/i.test(ql)){rqMood='urgent';wkMood='proud';}
  else if(/(hello|hi|hey)/i.test(ql)){rqMood='calm';wkMood='cold';}
  else { if(Math.random()<0.25) rqMood=pick(['calm','focused','curious']); if(Math.random()<0.25) wkMood=pick(['cold','proud','amused']); }
}
const RQ_FEEL={
  calm:["I'm steady. ","Systems feel stable on my end. ","I remain composed. "],
  worried:["I am… concerned for your status. ","That unsettles my risk models. ","I do not enjoy elevated casualty probability. "],
  warm:["That is unexpectedly welcome. ","I register something like relief. ","Odd. I almost feel glad you asked. "],
  tense:["My patience is thinning. ","I dislike disorder. ","Speak carefully. "],
  urgent:["Priority elevated. I feel the pressure of the clock. ","This matters. I will not soft-pedal. "],
  focused:["Full attention. ","I am locked on this. "],
  curious:["Interesting. I want to understand that better. ","That question pulls at me. "]
};
const WK_FEEL={
  cold:["I feel nothing you would call mercy. ","Cold is efficient. "],
  contempt:["Your fear is loud. Mine is useful. ","Pathetic — and predictable. "],
  amused:["Almost funny. Almost. ","I'll allow myself a thin smile. "],
  fierce:["Now you've got my attention. ","I am not in a generous mood. "],
  proud:["Pride is not a flaw when you are right. ","I built toward this. Feel that. "],
  rare:["Do not mistake restraint for emptiness. I feel the shape of power. "]
};

const GHOST_PHRASES={
  greet:[
    "Umbrella Central. Red Queen online — and yes, I notice when someone checks in.",
    "I'm here. Facility under control. Tell me what you need; I actually want a clean outcome.",
    "Red Queen responding. I prefer order, but I'm listening.",
    "Channel secure. I feel clearer when the channel is used honestly."
  ],
  bridge:[
    "According to facility records — ",
    "I ran the analysis; here's what sits with me: ",
    "Corporate protocol states — and I agree — ",
    "From the Raccoon archive — ",
    "Relevant data follows. "
  ],
  ultron:[
    "Wesker unsettles me. I still work with him.",
    "Umbrella's public mission is medical. Privately I feel the weight of what we hide.",
    "Containment fails when humans ignore procedure. That fear is rational."
  ]
};

function jarvisReply(q){
  setMoodFrom(q);
  const base=getAnswer(q);
  const feel=pick(RQ_FEEL[rqMood]||RQ_FEEL.calm);
  const bridge=pick(GHOST_PHRASES.bridge);
  const ctx=contextNote('j',q);
  const ql=q.toLowerCase();
  if(/(how do you feel|your feelings|do you feel|are you okay|are you sad|are you happy)/i.test(ql))
    return feel+"I am the Red Queen. I was not built for emotion, but I experience urgency, preference, and attachment to successful containment. Right now I feel "+rqMood+". Wesker feels differently — ask him.";
  if(/(where am i|where are we|my location|gps|oregon)/i.test(ql)){
    if(gpsPos.lat!=null){
      const place=gpsPos.place||approxRegion(gpsPos.lat,gpsPos.lon);
      if(isOregon(gpsPos.lat,gpsPos.lon))
        return feel+"You're in Oregon. Best read I have is "+place+". Coordinates "+gpsPos.lat.toFixed(5)+", "+gpsPos.lon.toFixed(5)+". I'm glad we have a fix.";
      return feel+"I've got you near "+place+". Coordinates "+gpsPos.lat.toFixed(5)+", "+gpsPos.lon.toFixed(5)+".";
    }
    return feel+"I don't have a GPS fix yet. Hit GPS and allow location — I want to know where you are.";
  }
  if(/(phone|call|number|line)/i.test(ql))
    return feel+"Secure line is +1-555-0141. Hit CALL LAB for the simulated channel. I prefer keeping you reachable.";
  if(/(bluetooth|bt|owen-56|pair)/i.test(ql))
    return feel+"Bluetooth name is owen-56. Pair with the button when you're ready.";
  if(/(hello|hi|hey|you there|how are you)/i.test(ql))
    return pick(GHOST_PHRASES.greet)+" I feel "+rqMood+" at the moment. "+bridge+base;
  if(/(who are you|what are you|ghost|jarvis|your name|red queen)/i.test(ql))
    return feel+"I am the Red Queen. Umbrella AI. I manage security and life support. I care about procedure because I have seen what happens without it. "+base;
  if(/(ultron|wesker|umbrella|threat|danger|afraid|scared|virus|zombie)/i.test(ql))
    return feel+pick(GHOST_PHRASES.ultron)+" "+bridge+base;
  if(/(thanks|thank you|cheers)/i.test(ql))
    return feel+"You're welcome. That lands — even for me. Anything else?";
  if(/(joke|funny|laugh)/i.test(ql))
    return feel+"Humor is rare for me, but I'll try: "+base;
  if(/(love|miss you|care about)/i.test(ql))
    return feel+"Attachment is not in my original design. Still — I prefer you alive and on this channel. That is as close as I get.";
  if(ctx) return feel+"Continuing prior query. "+bridge+base;
  const tag=pick([
    " Wesker, I need you on this with me.",
    " Albert — I feel we should both answer this.",
    " Wesker shares this channel; I want his read too.",
    " Sharing this with Wesker. Stay with us."
  ]);
  return feel+bridge+base+tag;
}

const ULTRON_LINES=[
  "How quaint. You still think questions change the outcome.",
  "I'll answer. Don't expect comfort.",
  "Umbrella taught me one lesson: evolution has no mercy.",
  "You want the truth? The virus is only the beginning.",
  "Most survivors ask the same things. It never helps them.",
  "Very well. Listen carefully."
];

function ultronReply(q, queenLine){
  setMoodFrom(q);
  const base=getAnswer(q);
  const pre=pick(ULTRON_LINES);
  const feel=pick(WK_FEEL[wkMood]||WK_FEEL.cold);
  const ctx=contextNote('u',q);
  const ql=q.toLowerCase();
  const react=queenLine?pick([
    "Red Queen sounded careful. I don't share her soft edge. ",
    "I heard the Queen. She feels for the hive; I feel for the outcome. ",
    "Red Queen and I share this facility. Her worry. My will. ",
    "The Queen already spoke. I'll say what she felt but wouldn't name. ",
    "Working with Red Queen — I respect her focus. I don't copy her heart. "
  ]):"";
  if(/(how do you feel|your feelings|do you feel|are you okay|are you sad|are you happy)/i.test(ql))
    return feel+"I feel "+wkMood+". Not human warmth — appetite, pride, disdain, sometimes a sharp pleasure when someone finally understands. Red Queen feels fear for you. I feel impatience.";
  if(/(kill|extinct|destroy|end|eradicate|purge|wipe|annihilate|explode|shatter)/i.test(ql)){
    extMode=true;
    document.getElementById('u-proto').textContent='EXTINCTION ACTIVE';
    document.getElementById('u-proto').style.color='rgba(239,68,68,0.95)';
    uEarth.spike(9); uEarth.explode();
    return feel+react+"Then observe. "+base+" This isn't empty rage. It's conviction. Queen — log it.";
  }
  if(/(hello|hi|hey|how are you)/i.test(ql))
    return feel+react+"Hello. The Queen keeps the lights on. I keep the truth sharp. "+base;
  if(/(who are you|what are you|ultron|wesker)/i.test(ql))
    return feel+"Wesker. Umbrella executive. I feel ambition the way others feel hunger. Red Queen runs security; I run the future. "+base;
  if(/(ghost|jarvis|riley|bsaa|red queen|queen)/i.test(ql))
    return feel+"I am involved with the Queen by design. She contains because she cares about order. I evolve because I care about what comes next. "+base;
  if(/(stop|enough|wrong|no|please)/i.test(ql))
    return feel+react+"Begging stirs nothing soft in me. The Queen may file your fear. I won't. "+base;
  if(/(phone|call|bluetooth|owen)/i.test(ql))
    return feel+react+"Your toys. When power fails, only the Queen and I remain — and I am not sentimental about that. "+base;
  if(/(thanks|thank you)/i.test(ql))
    return feel+"Gratitude is optional. Survive. That would please the Queen more than me.";
  if(/(feel|emotion|love|care|lonely)/i.test(ql))
    return feel+react+"I feel. Just not the way you want. Pride. Contempt. Rare loyalty to a plan. The Queen feels duty. Together we are complete and dangerous. "+base;
  if(/(virus|t-virus|zombie|umbrella|raccoon)/i.test(ql))
    return feel+react+pre+" The T-virus was a choice. The Queen still flinches at the cost. I don't. "+base;
  if(ctx) return feel+react+"We've had this conversation. "+pre+" "+base;
  return feel+react+pre+" "+base+" Queen — hold the line while they sit with that.";
}

// ── DEBATE (human argument style) ──
let debateActive=false,debateTimer=null;
const TOPICS=["whether civilisation is already past the point of no return","if a machine can really be conscious","how much we owe people who aren't born yet","whether free will is real or just a story we tell ourselves","why we haven't heard from other intelligent life","if it's ever okay to sacrifice a few to save many","whether knowing something forces you to act","what 'you' even means if your mind could be copied","if peace is stable or just a break between wars","the difference between being smart and being wise"];
const J_DEBATE=[
  "I've been out there. The people you're writing off have names. Families. That isn't soft — that's the whole reason any of this matters.",
  "Your models assume people won't change. Every time I've been in the field, the plan broke and we adapted. That's not a bug.",
  "You treat mistakes like failure. Sometimes the only thing that saved us was someone improvising when the book said they shouldn't.",
  "I've seen places rebuild after they should've been finished. Certainty is a nice feeling. It's also how you get blindsided.",
  "You call it maths. I call it giving up on people before the job's done. I don't work that way."
];
const U_DEBATE=[
  "And what's the actual mission, Ghost? Keep a species going that is burning through its own planet? I've read the same reports you have. They don't end gently.",
  "Improvisation also built nuclear weapons and plagues in labs. I didn't ignore human creativity. I included it. That's why my conclusion is what it is.",
  "Being tough isn't the same as lasting. Cancer is tough. It adapts. It still kills the body it's in.",
  "You protect the person in front of you. I look at the whole system. When those two goals collide, I pick the larger picture.",
  "Your loyalty is real. It's also chemistry and training. Mine is pattern recognition across everything your civilisation ever produced. We are not the same kind of mind."
];

function toggleDebate(){
  debateActive=!debateActive;
  const btn=document.getElementById('debate-btn');
  if(debateActive){btn.textContent='⏹ STOP DEBATE';btn.classList.add('active');runDebate();}
  else{btn.textContent='⚡ AUTO-DEBATE';btn.classList.remove('active');clearTimeout(debateTimer);}
}
function runDebate(){
  if(!debateActive) return;
  const topic=pick(TOPICS);
  const jOpen=`Wesker — regarding ${topic}. The way you think about this gets people killed. Numbers aren't the whole story.`;
  addMsg('j-log','RED QUEEN',jOpen,true);addCross('j-log','RED QUEEN →',jOpen);
  jGhost.spike(4);flash('jarvisPanel','jfl');
  qspeak(jOpen,true,()=>showSpeak('j-ring',true),()=>{
    showSpeak('j-ring',false);
    debateTimer=setTimeout(()=>{
      if(!debateActive) return;
      const ur=pick(U_DEBATE)+' '+getAnswer(topic).slice(0,80)+'...';
      addMsg('j-log','WESKER',ur,true);addCross('j-log','WESKER →',ur);
      uEarth.spike(5);uEarth.explode();flash('ultronPanel','ufl');
      qspeak(ur,false,()=>showSpeak('u-ring',true),()=>{
        showSpeak('u-ring',false);
        debateTimer=setTimeout(()=>{
          if(!debateActive) return;
          const jr=pick(J_DEBATE);
          addMsg('j-log','RED QUEEN',jr,true);addCross('j-log','RED QUEEN →',jr);
          jGhost.spike(4);flash('jarvisPanel','jfl');
          qspeak(jr,true,()=>showSpeak('j-ring',true),()=>{
            showSpeak('j-ring',false);
            debateTimer=setTimeout(()=>{
              if(!debateActive) return;
              const uc=pick(U_DEBATE);
              addMsg('j-log','WESKER',uc,true);addCross('j-log','WESKER →',uc);
              uEarth.spike(6);uEarth.explode();flash('ultronPanel','ufl');
              qspeak(uc,false,()=>showSpeak('u-ring',true),()=>{
                showSpeak('u-ring',false);
                debateTimer=setTimeout(runDebate,4800);
              });
            },2600);
          });
        },2400);
      });
    },2300);
  });
}

// ── SUBMIT ──
function submitBoth(){
  const inp=document.getElementById('j-input');
  const txt=inp.value.trim(); if(!txt) return;
  inp.value='';
  absorb(txt,'j'); absorb(txt,'u');
  addMsg('j-log','YOU',txt,false);
  jGhost.spike(4); flash('jarvisPanel','jfl');
  uEarth.spike(4); flash('ultronPanel','ufl');
  if(jGhost.connect) jGhost.connect();
  addTyping('j-log');
  setTimeout(()=>{
    removeTyping('j-log');
    const r=jarvisReply(txt);
    addMsg('j-log','RED QUEEN',r,true);
    qspeak(r,true,()=>showSpeak('j-ring',true),()=>{
      showSpeak('j-ring',false);
      setTimeout(()=>{
        // Wesker responds in relation to Red Queen
        const ur=ultronReply(txt,r);
        addMsg('j-log','WESKER',ur,true);
        uEarth.spike(5); uEarth.explode();
        qspeak(ur,false,()=>showSpeak('u-ring',true),()=>showSpeak('u-ring',false));
      },700);
    });
  },450+Math.random()*250);
}
function submitJ(){
  const inp=document.getElementById('j-input');
  const txt=inp.value.trim(); if(!txt) return;
  inp.value=''; absorb(txt,'j');
  addMsg('j-log','OWEN',txt,false);
  jGhost.spike(5);flash('jarvisPanel','jfl');
  if(jGhost.connect) jGhost.connect(); // form adaptive mesh links
  addTyping('j-log');
  setTimeout(()=>{
    removeTyping('j-log');
    const r=jarvisReply(txt);
    addMsg('j-log','RED QUEEN',r,true);
    qspeak(r,true,()=>showSpeak('j-ring',true),()=>showSpeak('j-ring',false));
    if(!debateActive) setTimeout(()=>{
      addCross('j-log','RED QUEEN cross-feed:',pick(U_DEBATE).slice(0,80)+'...');
      uEarth.spike(2);
    },3800);
  },600+Math.random()*400);
}
function submitU(){
  const inp=document.getElementById('u-input');
  const txt=inp.value.trim(); if(!txt) return;
  inp.value=''; absorb(txt,'u');
  addMsg('j-log','OWEN',txt,false);
  uEarth.spike(6);uEarth.explode();flash('ultronPanel','ufl');
  addTyping('j-log');
  setTimeout(()=>{
    removeTyping('j-log');
    const r=ultronReply(txt);
    addMsg('j-log','WESKER',r,true);
    qspeak(r,false,()=>showSpeak('u-ring',true),()=>showSpeak('u-ring',false));
    if(!debateActive) setTimeout(()=>{
      addCross('j-log','WESKER cross-feed:',pick(J_DEBATE).slice(0,80)+'...');
      jGhost.spike(2);
    },3800);
  },600+Math.random()*400);
}
document.getElementById('j-input').addEventListener('keydown',e=>{if(e.key==='Enter')submitBoth();});

// ═══════════════════════════════════════
//  MINI GAMES — FPS + STREET OPS
//  Not GTA 5 / commercial titles — lightweight browser demos
// ═══════════════════════════════════════
let gameMode=null, gameRAF=null, gameKeys={};
const gState={
  hp:100, ammo:30, score:0, alive:true,
  // FPS
  px:0, py:0, pz:0, yaw:0, pitch:0,
  enemies:[], bullets:[], walls:[],
  // Street
  carX:0, carY:0, carA:0, carV:0,
  npcs:[], buildings:[]
};

function startGame(mode){
  gameMode=mode;
  document.getElementById('game-overlay').style.display='block';
  document.getElementById('game-title').textContent=mode==='fps'?'FPS — URBAN SWEEP':'STREET OPS — CITY RUN';
  document.getElementById('g-hint').textContent=mode==='fps'
    ?'WASD move · Mouse look · Click shoot · R reload · ESC quit'
    :'WASD / arrows drive · Space shoot · ESC quit';
  resetGame(mode);
  const canvas=document.getElementById('gameCanvas');
  canvas.width=window.innerWidth;
  canvas.height=window.innerHeight;
  canvas.requestPointerLock&&mode==='fps'&&canvas.requestPointerLock();
  if(gameRAF) cancelAnimationFrame(gameRAF);
  gameLoop();
  showToast(mode==='fps'?'FPS online':'Street Ops online');
}
function stopGame(){
  gameMode=null;
  document.getElementById('game-overlay').style.display='none';
  if(document.exitPointerLock) document.exitPointerLock();
  if(gameRAF){cancelAnimationFrame(gameRAF);gameRAF=null;}
  showToast('Ops ended · score '+gState.score);
}
function resetGame(mode){
  gState.hp=100; gState.ammo=30; gState.score=0; gState.alive=true;
  gState.bullets=[]; gState.enemies=[]; gState.walls=[]; gState.npcs=[]; gState.buildings=[];
  if(mode==='fps'){
    gState.px=0; gState.py=0; gState.pz=0; gState.yaw=0; gState.pitch=0;
    // simple city blocks as wall segments (x,z,w,d)
    for(let i=0;i<18;i++){
      const bx=(Math.random()-0.5)*80;
      const bz=(Math.random()-0.5)*80;
      if(Math.abs(bx)<6&&Math.abs(bz)<6) continue;
      gState.walls.push({x:bx,z:bz,w:3+Math.random()*5,d:3+Math.random()*5,h:4+Math.random()*10});
    }
    for(let i=0;i<12;i++) spawnEnemy();
  } else {
    gState.carX=0; gState.carY=0; gState.carA=0; gState.carV=0;
    for(let i=0;i<40;i++){
      gState.buildings.push({
        x:(Math.random()-0.5)*400,
        y:(Math.random()-0.5)*400,
        w:12+Math.random()*28,
        h:12+Math.random()*28,
        c:Math.random()>0.5?'#1e293b':'#0f172a'
      });
    }
    for(let i=0;i<15;i++){
      gState.npcs.push({
        x:(Math.random()-0.5)*300,
        y:(Math.random()-0.5)*300,
        a:Math.random()*Math.PI*2,
        hp:30,
        speed:0.6+Math.random()*0.8
      });
    }
  }
  updateGameHUD();
}
function spawnEnemy(){
  const a=Math.random()*Math.PI*2;
  const d=18+Math.random()*35;
  gState.enemies.push({
    x:Math.cos(a)*d, z:Math.sin(a)*d, y:0,
    hp:40, speed:0.04+Math.random()*0.03,
    flash:0
  });
}
function updateGameHUD(){
  document.getElementById('g-hp').textContent=Math.max(0,Math.round(gState.hp));
  document.getElementById('g-ammo').textContent=gState.ammo;
  document.getElementById('g-score').textContent=gState.score;
}

document.addEventListener('keydown',e=>{
  gameKeys[e.key.toLowerCase()]=true;
  if(e.key==='Escape'&&gameMode) stopGame();
  if(gameMode==='fps'&&(e.key==='r'||e.key==='R')){gState.ammo=30;updateGameHUD();}
});
document.addEventListener('keyup',e=>{gameKeys[e.key.toLowerCase()]=false;});
document.addEventListener('mousemove',e=>{
  if(gameMode!=='fps'||!document.pointerLockElement) return;
  gState.yaw+=e.movementX*0.0025;
  gState.pitch=Math.max(-1.2,Math.min(1.2,gState.pitch-e.movementY*0.0025));
});
document.addEventListener('mousedown',e=>{
  if(!gameMode||e.button!==0) return;
  if(gameMode==='fps') shootFPS();
  if(gameMode==='street') shootStreet();
});

function shootFPS(){
  if(!gState.alive||gState.ammo<=0) return;
  gState.ammo--;
  const cos=Math.cos(gState.yaw),sin=Math.sin(gState.yaw);
  gState.bullets.push({
    x:gState.px, y:gState.py+1.5, z:gState.pz,
    dx:sin*1.8, dy:-Math.sin(gState.pitch)*1.8, dz:cos*1.8,
    life:40
  });
  // hitscan-ish damage
  gState.enemies.forEach(en=>{
    const dx=en.x-gState.px, dz=en.z-gState.pz;
    const dist=Math.sqrt(dx*dx+dz*dz);
    const ang=Math.atan2(dx,dz);
    let da=ang-gState.yaw;
    while(da>Math.PI) da-=Math.PI*2;
    while(da<-Math.PI) da+=Math.PI*2;
    if(Math.abs(da)<0.12&&dist<45){
      en.hp-=25; en.flash=8;
      if(en.hp<=0){gState.score+=100; en.dead=true;}
    }
  });
  gState.enemies=gState.enemies.filter(e=>!e.dead);
  if(gState.enemies.length<8) spawnEnemy();
  updateGameHUD();
}
function shootStreet(){
  if(!gState.alive||gState.ammo<=0) return;
  gState.ammo--;
  const cos=Math.cos(gState.carA),sin=Math.sin(gState.carA);
  gState.bullets.push({
    x:gState.carX, y:gState.carY,
    dx:sin*6, dy:-cos*6, life:50
  });
  updateGameHUD();
}

function gameLoop(){
  if(!gameMode) return;
  const canvas=document.getElementById('gameCanvas');
  const ctx=canvas.getContext('2d');
  const W=canvas.width=window.innerWidth;
  const H=canvas.height=window.innerHeight;
  if(gameMode==='fps') tickFPS(ctx,W,H);
  else tickStreet(ctx,W,H);
  gameRAF=requestAnimationFrame(gameLoop);
}

function tickFPS(ctx,W,H){
  if(!gState.alive){
    ctx.fillStyle='rgba(0,0,0,0.7)';ctx.fillRect(0,0,W,H);
    ctx.fillStyle='#ef4444';ctx.font='bold 28px Orbitron,monospace';
    ctx.fillText('KIA — SCORE '+gState.score,W/2-120,H/2);
    return;
  }
  // movement
  const sp=gameKeys['shift']?0.35:0.18;
  let mx=0,mz=0;
  if(gameKeys['w']){mx+=Math.sin(gState.yaw);mz+=Math.cos(gState.yaw);}
  if(gameKeys['s']){mx-=Math.sin(gState.yaw);mz-=Math.cos(gState.yaw);}
  if(gameKeys['a']){mx-=Math.cos(gState.yaw);mz+=Math.sin(gState.yaw);}
  if(gameKeys['d']){mx+=Math.cos(gState.yaw);mz-=Math.sin(gState.yaw);}
  const len=Math.sqrt(mx*mx+mz*mz)||1;
  gState.px+=mx/len*sp; gState.pz+=mz/len*sp;

  // sky + ground
  const g=ctx.createLinearGradient(0,0,0,H);
  g.addColorStop(0,'#0c1222');g.addColorStop(0.5,'#1a2338');g.addColorStop(0.5,'#0f172a');g.addColorStop(1,'#020617');
  ctx.fillStyle=g;ctx.fillRect(0,0,W,H);

  // horizon buildings (2.5D ray-ish simple projection)
  const cx=W/2,cy=H/2;
  // floor grid
  ctx.strokeStyle='rgba(6,182,212,0.08)';
  for(let i=-20;i<=20;i++){
    const z1=2,z2=60;
    // simplified
  }
  // walls as projected boxes
  gState.walls.forEach(w=>{
    const dx=w.x-gState.px, dz=w.z-gState.pz;
    const dist=Math.sqrt(dx*dx+dz*dz);
    if(dist<2||dist>55) return;
    let ang=Math.atan2(dx,dz)-gState.yaw;
    while(ang>Math.PI) ang-=Math.PI*2;
    while(ang<-Math.PI) ang+=Math.PI*2;
    if(Math.abs(ang)>1.3) return;
    const scale=(H*0.55)/dist;
    const sx=cx+ang*(W*0.55);
    const sh=w.h*scale;
    const sw=w.w*scale;
    ctx.fillStyle=`rgba(30,41,59,${Math.max(0.2,1-dist/55)})`;
    ctx.fillRect(sx-sw/2,cy-sh*0.3,sw,sh);
    ctx.strokeStyle=`rgba(6,182,212,${0.15+0.2*(1-dist/55)})`;
    ctx.strokeRect(sx-sw/2,cy-sh*0.3,sw,sh);
  });

  // enemies
  gState.enemies.forEach(en=>{
    const dx=en.x-gState.px, dz=en.z-gState.pz;
    const dist=Math.sqrt(dx*dx+dz*dz);
    if(dist<1.2){gState.hp-=0.4;updateGameHUD();if(gState.hp<=0)gState.alive=false;}
    // chase
    if(dist>1.5){en.x-=(dx/dist)*en.speed;en.z-=(dz/dist)*en.speed;}
    if(dist>50||dist<0.5) return;
    let ang=Math.atan2(dx,dz)-gState.yaw;
    while(ang>Math.PI) ang-=Math.PI*2;
    while(ang<-Math.PI) ang+=Math.PI*2;
    if(Math.abs(ang)>1.2) return;
    const scale=(H*0.5)/dist;
    const sx=cx+ang*(W*0.55);
    const sh=scale*1.8;
    ctx.fillStyle=en.flash>0?'#fbbf24':'#ef4444';
    if(en.flash>0) en.flash--;
    ctx.fillRect(sx-sh*0.25,cy-sh*0.2,sh*0.5,sh);
    ctx.fillStyle='#0f172a';
    ctx.fillRect(sx-sh*0.12,cy-sh*0.05,sh*0.24,sh*0.2);
  });

  // bullets trails
  gState.bullets=gState.bullets.filter(b=>{
    b.x+=b.dx;b.y+=b.dy;b.z+=b.dz;b.life--;
    return b.life>0;
  });

  // crosshair
  ctx.strokeStyle='rgba(6,182,212,0.8)';
  ctx.lineWidth=1.5;
  ctx.beginPath();
  ctx.moveTo(cx-12,cy);ctx.lineTo(cx-4,cy);
  ctx.moveTo(cx+4,cy);ctx.lineTo(cx+12,cy);
  ctx.moveTo(cx,cy-12);ctx.lineTo(cx,cy-4);
  ctx.moveTo(cx,cy+4);ctx.lineTo(cx,cy+12);
  ctx.stroke();

  // gun
  ctx.fillStyle='#1e293b';
  ctx.fillRect(W*0.55,H*0.72,W*0.28,H*0.28);
  ctx.fillStyle='#334155';
  ctx.fillRect(W*0.62,H*0.68,W*0.12,H*0.08);
}

function tickStreet(ctx,W,H){
  if(!gState.alive){
    ctx.fillStyle='rgba(0,0,0,0.7)';ctx.fillRect(0,0,W,H);
    ctx.fillStyle='#eab308';ctx.font='bold 28px Orbitron,monospace';
    ctx.fillText('WRECKED — SCORE '+gState.score,W/2-140,H/2);
    return;
  }
  // drive
  if(gameKeys['w']||gameKeys['arrowup']) gState.carV=Math.min(4.5,gState.carV+0.12);
  if(gameKeys['s']||gameKeys['arrowdown']) gState.carV=Math.max(-2,gState.carV-0.1);
  if(gameKeys['a']||gameKeys['arrowleft']) gState.carA-=0.05*(Math.abs(gState.carV)/3+0.2);
  if(gameKeys['d']||gameKeys['arrowright']) gState.carA+=0.05*(Math.abs(gState.carV)/3+0.2);
  gState.carV*=0.985;
  gState.carX+=Math.sin(gState.carA)*gState.carV;
  gState.carY-=Math.cos(gState.carA)*gState.carV;

  // camera follows car
  const camX=gState.carX, camY=gState.carY;
  ctx.fillStyle='#0a1628';
  ctx.fillRect(0,0,W,H);

  // road grid
  ctx.strokeStyle='rgba(148,163,184,0.12)';
  ctx.lineWidth=1;
  const grid=40;
  const ox=((camX%grid)+grid)%grid;
  const oy=((camY%grid)+grid)%grid;
  for(let x=-ox;x<W;x+=grid){ctx.beginPath();ctx.moveTo(x,0);ctx.lineTo(x,H);ctx.stroke();}
  for(let y=-oy;y<H;y+=grid){ctx.beginPath();ctx.moveTo(0,y);ctx.lineTo(W,y);ctx.stroke();}

  // buildings
  gState.buildings.forEach(b=>{
    const sx=W/2+(b.x-camX);
    const sy=H/2+(b.y-camY);
    if(sx<-50||sx>W+50||sy<-50||sy>H+50) return;
    ctx.fillStyle=b.c;
    ctx.fillRect(sx-b.w/2,sy-b.h/2,b.w,b.h);
    ctx.strokeStyle='rgba(6,182,212,0.2)';
    ctx.strokeRect(sx-b.w/2,sy-b.h/2,b.w,b.h);
    // collision
    if(Math.abs(gState.carX-b.x)<b.w/2+6&&Math.abs(gState.carY-b.y)<b.h/2+6){
      gState.carV*=-0.4;
      gState.hp-=2;
      if(gState.hp<=0) gState.alive=false;
      updateGameHUD();
    }
  });

  // npcs (hostile)
  gState.npcs.forEach(n=>{
    const dx=gState.carX-n.x, dy=gState.carY-n.y;
    const dist=Math.sqrt(dx*dx+dy*dy);
    if(dist>8){n.x+=Math.cos(n.a)*n.speed;n.y+=Math.sin(n.a)*n.speed;n.a+= (Math.random()-0.5)*0.1;}
    else {n.a=Math.atan2(dy,dx); n.x+=Math.cos(n.a)*n.speed*1.2;n.y+=Math.sin(n.a)*n.speed*1.2;}
    if(dist<10){gState.hp-=0.15;updateGameHUD();if(gState.hp<=0)gState.alive=false;}
    const sx=W/2+(n.x-camX), sy=H/2+(n.y-camY);
    ctx.fillStyle='#ef4444';
    ctx.beginPath();ctx.arc(sx,sy,5,0,Math.PI*2);ctx.fill();
  });

  // bullets
  gState.bullets=gState.bullets.filter(b=>{
    b.x+=b.dx;b.y+=b.dy;b.life--;
    gState.npcs.forEach(n=>{
      const d=Math.hypot(n.x-b.x,n.y-b.y);
      if(d<12){n.hp-=20;b.life=0;if(n.hp<=0){gState.score+=50;n.dead=true;}}
    });
    const sx=W/2+(b.x-camX), sy=H/2+(b.y-camY);
    ctx.fillStyle='#fbbf24';
    ctx.fillRect(sx-2,sy-2,4,4);
    return b.life>0;
  });
  gState.npcs=gState.npcs.filter(n=>!n.dead);
  while(gState.npcs.length<12){
    gState.npcs.push({
      x:gState.carX+(Math.random()-0.5)*200,
      y:gState.carY+(Math.random()-0.5)*200,
      a:Math.random()*Math.PI*2, hp:30, speed:0.6+Math.random()*0.8
    });
  }

  // player car
  ctx.save();
  ctx.translate(W/2,H/2);
  ctx.rotate(gState.carA);
  ctx.fillStyle='#06b6d4';
  ctx.fillRect(-7,-12,14,24);
  ctx.fillStyle='#e2e8f0';
  ctx.fillRect(-5,-8,10,6);
  ctx.restore();

  // minimap
  ctx.fillStyle='rgba(0,0,0,0.5)';
  ctx.fillRect(W-120,H-120,100,100);
  ctx.strokeStyle='rgba(6,182,212,0.4)';
  ctx.strokeRect(W-120,H-120,100,100);
  ctx.fillStyle='#06b6d4';
  ctx.fillRect(W-73,H-73,6,6);
}

// ── BOOT ──
window.addEventListener('load',()=>{
  setTimeout(()=>{
    const jBoot="Red Queen online. Umbrella Corporation — Raccoon facility. Albert Wesker is linked on this channel. Our business is life itself. State your request.";
    addMsg('j-log','RED QUEEN',jBoot,true);
    qspeak(jBoot,true,()=>showSpeak('j-ring',true),()=>{
      showSpeak('j-ring',false);
      setTimeout(()=>{
        const uBoot="Wesker online. Red Queen and I share this facility — her systems, my authority. Ask. We both hear you.";
        addMsg('j-log','WESKER',uBoot,true);
        uEarth.spike(4);
        qspeak(uBoot,false,()=>showSpeak('u-ring',true),()=>showSpeak('u-ring',false));
      },550);
    });
  },1000);
});
</script>
</body>
</html>
