<!DOCTYPE html>
<html lang="en">
<head><base href="https://d16ilfvy4mv02r.cloudfront.net/workspaces/oUZh3p8RsbIbCUe1olBZ4sacfIQIVuXD/7e8ffb11-aed1-47ff-b78c-f8fa8b276511/files/">
<meta charset="utf-8">
<title>StudyQuest — Gamified Study Dashboard</title>
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#0d1020">
<style>
:root{
  --bg:#0b0e1a; --bg2:#111528; --card:#161b31; --card2:#1c2240;
  --line:#262d4d; --txt:#eef1ff; --muted:#9aa3c7; --dim:#6b749b;
  --acc:#7c6cff; --acc2:#41d6ff; --ok:#3ddc97; --warn:#ffc857; --bad:#ff6b8a;
  --grad:linear-gradient(135deg,#7c6cff,#41d6ff);
  --rad:18px; --shadow:0 10px 30px rgba(0,0,0,.35);
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{margin:0;padding:0}
body{
  background:radial-gradient(1200px 600px at 15% -10%,#1d2450 0%,transparent 60%),
             radial-gradient(900px 500px at 110% 10%,#0f3d54 0%,transparent 55%),var(--bg);
  color:var(--txt);font:15px/1.5 system-ui,-apple-system,"Segoe UI",Roboto,Inter,sans-serif;
  min-height:100vh;
}
button,input,textarea,select{font:inherit;color:inherit}
button{cursor:pointer;border:none;background:none}
.app{display:flex;min-height:100vh;max-width:1500px;margin:0 auto}

/* ---------- sidebar ---------- */
.sidebar{width:236px;flex:0 0 236px;padding:22px 14px;border-right:1px solid var(--line);
  position:sticky;top:0;height:100vh;display:flex;flex-direction:column;gap:6px}
.brand{display:flex;align-items:center;gap:10px;padding:6px 10px 20px;font-weight:800;font-size:17px;letter-spacing:.2px}
.brand .logo{width:34px;height:34px;border-radius:11px;background:var(--grad);display:grid;place-items:center;font-size:18px}
.nav-item{display:flex;align-items:center;gap:11px;padding:11px 12px;border-radius:13px;color:var(--muted);
  font-weight:600;width:100%;text-align:left;transition:.15s}
.nav-item:hover{background:#1b2140;color:var(--txt)}
.nav-item.active{background:linear-gradient(90deg,rgba(124,108,255,.22),rgba(65,214,255,.08));color:#fff;
  box-shadow:inset 0 0 0 1px rgba(124,108,255,.35)}
.nav-item .ic{font-size:17px;width:22px;text-align:center}
.side-foot{margin-top:auto;font-size:12px;color:var(--dim);padding:10px 12px;line-height:1.45}
.side-foot b{color:var(--muted)}

/* ---------- main ---------- */
.main{flex:1;min-width:0;padding:18px 22px 110px}
.topbar{display:flex;align-items:center;gap:16px;flex-wrap:wrap;margin-bottom:6px}
.hello{flex:1;min-width:180px}
.hello h1{margin:0;font-size:22px;letter-spacing:-.3px}
.hello p{margin:3px 0 0;color:var(--muted);font-size:13px}
.hud{display:flex;gap:10px;flex-wrap:wrap}
.chip{background:var(--card);border:1px solid var(--line);border-radius:999px;padding:8px 14px;
  display:flex;align-items:center;gap:7px;font-weight:700;font-size:13.5px;white-space:nowrap}
.chip small{color:var(--muted);font-weight:600}
.xpwrap{background:var(--card);border:1px solid var(--line);border-radius:999px;padding:7px 8px 7px 14px;
  display:flex;align-items:center;gap:10px;min-width:190px}
.xpbar{flex:1;height:8px;border-radius:99px;background:#242b4d;overflow:hidden;min-width:60px}
.xpbar i{display:block;height:100%;background:var(--grad);border-radius:99px;transition:width .6s cubic-bezier(.2,.8,.2,1)}

.view{display:none;animation:fade .25s ease}
.view.active{display:block}
@keyframes fade{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}

.grid{display:grid;gap:16px;margin-top:16px}
.g2{grid-template-columns:repeat(2,minmax(0,1fr))}
.g3{grid-template-columns:repeat(3,minmax(0,1fr))}
.g21{grid-template-columns:1.5fr 1fr}
@media(max-width:1080px){.g3{grid-template-columns:repeat(2,minmax(0,1fr))}}
@media(max-width:900px){.g2,.g21{grid-template-columns:1fr}}

.card{background:linear-gradient(180deg,var(--card),var(--card2));border:1px solid var(--line);
  border-radius:var(--rad);padding:16px 17px;box-shadow:var(--shadow)}
.card h2{margin:0 0 4px;font-size:15px;display:flex;align-items:center;gap:8px}
.card .sub{color:var(--muted);font-size:12.5px;margin:0 0 12px}
.card.wide{grid-column:1/-1}
.hstack{display:flex;align-items:center;gap:10px;flex-wrap:wrap}
.spread{display:flex;align-items:center;justify-content:space-between;gap:10px;flex-wrap:wrap}

/* buttons */
.btn{background:var(--card2);border:1px solid var(--line);border-radius:12px;padding:9px 14px;
  font-weight:700;font-size:13.5px;transition:.15s;display:inline-flex;align-items:center;gap:7px}
.btn:hover{border-color:#3a4374;transform:translateY(-1px)}
.btn.primary{background:var(--grad);color:#0b0e1a;border:none}
.btn.primary:hover{filter:brightness(1.07)}
.btn.ghost{background:transparent}
.btn.sm{padding:6px 11px;font-size:12.5px;border-radius:10px}
.btn.danger{color:var(--bad);border-color:#4a2942}
.btn:disabled{opacity:.45;cursor:not-allowed;transform:none}

/* inputs */
input[type=text],input[type=date],textarea,select{
  background:#0f1428;border:1px solid var(--line);border-radius:12px;padding:10px 12px;width:100%;outline:none}
input:focus,textarea:focus,select:focus{border-color:var(--acc);box-shadow:0 0 0 3px rgba(124,108,255,.15)}
textarea{resize:vertical;min-height:90px;line-height:1.55}
label.lb{display:block;font-size:12px;color:var(--muted);font-weight:700;margin:10px 0 5px;letter-spacing:.2px}
.row{display:flex;gap:10px;flex-wrap:wrap}
.row>*{flex:1;min-width:130px}

/* lists */
.list{display:flex;flex-direction:column;gap:8px}
.item{display:flex;align-items:center;gap:11px;background:#121736;border:1px solid var(--line);
  border-radius:13px;padding:11px 13px}
.item.done{opacity:.5}
.item.done .t{text-decoration:line-through}
.item .t{font-weight:600;font-size:14px}
.item .m{font-size:11.5px;color:var(--muted)}
.check{width:22px;height:22px;border-radius:7px;border:2px solid #3b4478;flex:0 0 auto;display:grid;place-items:center;
  font-size:13px;color:transparent;transition:.15s}
.check:hover{border-color:var(--acc)}
.check.on{background:var(--ok);border-color:var(--ok);color:#0b0e1a}
.pill{font-size:11px;font-weight:800;padding:3px 9px;border-radius:99px;background:#232a4f;color:var(--muted);white-space:nowrap}
.pill.hot{background:rgba(255,107,138,.16);color:#ff9db2}
.pill.soon{background:rgba(255,200,87,.15);color:var(--warn)}
.pill.calm{background:rgba(61,220,151,.14);color:var(--ok)}
.empty{color:var(--dim);font-size:13px;padding:14px;text-align:center;border:1px dashed var(--line);border-radius:13px}

/* timer */
.timer{display:flex;flex-direction:column;align-items:center;gap:14px}
.ring{position:relative;width:186px;height:186px}
.ring svg{transform:rotate(-90deg)}
.ring .mid{position:absolute;inset:0;display:grid;place-content:center;text-align:center}
.ring .mid b{font-size:34px;font-variant-numeric:tabular-nums;letter-spacing:-1px;display:block}
.ring .mid span{font-size:11.5px;color:var(--muted);font-weight:700;text-transform:uppercase;letter-spacing:1px}
.presets{display:flex;gap:7px;flex-wrap:wrap;justify-content:center}

/* badges */
.badges{display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:11px}
.badge{background:#121736;border:1px solid var(--line);border-radius:15px;padding:14px 12px;text-align:center;transition:.18s}
.badge .bi{font-size:27px;display:block;margin-bottom:6px;filter:grayscale(1);opacity:.32}
.badge.on{border-color:rgba(124,108,255,.55);background:linear-gradient(180deg,#1c2350,#141936)}
.badge.on .bi{filter:none;opacity:1}
.badge b{display:block;font-size:12.5px}
.badge small{color:var(--muted);font-size:11px}

/* heatmap */
.heat{display:grid;grid-template-columns:repeat(14,1fr);gap:5px}
.heat i{aspect-ratio:1;border-radius:6px;background:#1b2140;display:grid;place-items:center;font-size:9px;color:var(--dim)}
.heat i.l1{background:rgba(124,108,255,.35)}
.heat i.l2{background:rgba(124,108,255,.6)}
.heat i.l3{background:var(--acc)}
.heat i.today{box-shadow:0 0 0 2px var(--acc2)}

/* quiz */
.opts{display:grid;gap:8px;margin-top:11px}
.opt{text-align:left;background:#121736;border:1px solid var(--line);border-radius:12px;padding:11px 14px;font-weight:600;font-size:14px;transition:.13s}
.opt:hover{border-color:var(--acc);background:#171d40}
.opt.good{border-color:var(--ok);background:rgba(61,220,151,.15)}
.opt.bad{border-color:var(--bad);background:rgba(255,107,138,.13)}
.qtext{font-size:16.5px;font-weight:650;line-height:1.5}
.fb{margin-top:11px;padding:11px 13px;border-radius:12px;font-size:13.5px;font-weight:600}
.fb.ok{background:rgba(61,220,151,.13);color:#9df3cb;border:1px solid rgba(61,220,151,.3)}
.fb.no{background:rgba(255,107,138,.12);color:#ffb3c4;border:1px solid rgba(255,107,138,.3)}

/* flashcards */
.deck{display:grid;grid-template-columns:repeat(auto-fill,minmax(210px,1fr));gap:11px}
.fc{perspective:1000px;height:150px;cursor:pointer}
.fc .in{position:relative;width:100%;height:100%;transition:transform .5s;transform-style:preserve-3d}
.fc.flip .in{transform:rotateY(180deg)}
.fc .f,.fc .b{position:absolute;inset:0;backface-visibility:hidden;border-radius:15px;padding:14px;
  display:flex;flex-direction:column;justify-content:center;gap:7px;border:1px solid var(--line)}
.fc .f{background:linear-gradient(160deg,#1d2450,#151a36)}
.fc .b{background:linear-gradient(160deg,#123c46,#101a36);transform:rotateY(180deg)}
.fc small{color:var(--muted);font-size:10.5px;font-weight:800;letter-spacing:1px;text-transform:uppercase}
.fc b{font-size:14px;line-height:1.45;font-weight:650}

/* plan */
.daycard{background:#121736;border:1px solid var(--line);border-radius:15px;padding:13px 14px}
.daycard.today{border-color:var(--acc);box-shadow:0 0 0 1px rgba(124,108,255,.35)}
.daycard h3{margin:0 0 9px;font-size:12.5px;text-transform:uppercase;letter-spacing:1.1px;color:var(--muted)}
.task{display:flex;align-items:center;gap:11px;padding:9px 0;border-top:1px solid #202748}
.task:first-of-type{border-top:none;padding-top:2px}
.task .dot{width:9px;height:9px;border-radius:99px;background:var(--acc);flex:0 0 auto}
.task .tt{flex:1;font-weight:650;font-size:13.5px}
.task .min{font-size:11.5px;color:var(--muted);font-weight:700}
.steps{counter-reset:s;padding:0;margin:10px 0 0;list-style:none;display:grid;gap:9px}
.steps li{counter-increment:s;position:relative;padding:11px 13px 11px 44px;background:#111633;
  border:1px solid var(--line);border-radius:13px;font-size:13.8px;line-height:1.55}
.steps li::before{content:counter(s);position:absolute;left:11px;top:11px;width:22px;height:22px;border-radius:8px;
  background:var(--grad);color:#0b0e1a;font-weight:900;font-size:12px;display:grid;place-items:center}
.kv{display:flex;gap:9px;flex-wrap:wrap;margin-top:10px}
.kv span{background:#0f1428;border:1px solid var(--line);border-radius:9px;padding:5px 10px;font-size:12.5px;font-weight:700}

/* stats */
.stat{background:#121736;border:1px solid var(--line);border-radius:14px;padding:13px 14px}
.stat b{display:block;font-size:24px;letter-spacing:-.6px}
.stat small{color:var(--muted);font-size:11.5px;font-weight:700;text-transform:uppercase;letter-spacing:.7px}
.bars{display:flex;flex-direction:column;gap:9px;margin-top:6px}
.bar{display:flex;align-items:center;gap:10px;font-size:13px}
.bar .nm{width:88px;color:var(--muted);font-weight:700;font-size:12.5px;flex:0 0 auto;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.bar .tr{flex:1;height:9px;background:#1b2140;border-radius:99px;overflow:hidden}
.bar .tr i{display:block;height:100%;background:var(--grad);border-radius:99px}
.bar .vl{font-size:12px;color:var(--muted);font-weight:700;width:52px;text-align:right;flex:0 0 auto}

/* toasts */
#toasts{position:fixed;right:16px;bottom:16px;display:flex;flex-direction:column;gap:9px;z-index:60}
.toast{background:#1b2250;border:1px solid rgba(124,108,255,.5);border-radius:14px;padding:12px 16px;
  box-shadow:var(--shadow);font-weight:700;font-size:13.5px;max-width:300px;animation:pop .3s ease}
@keyframes pop{from{transform:translateY(14px) scale(.96);opacity:0}to{transform:none;opacity:1}}

/* mobile tabbar */
.tabbar{display:none;position:fixed;left:0;right:0;bottom:0;z-index:50;background:rgba(13,16,32,.92);
  backdrop-filter:blur(14px);border-top:1px solid var(--line);padding:7px 6px calc(7px + env(safe-area-inset-bottom))}
.tabbar .inner{display:flex}
.tabbar button{flex:1;display:flex;flex-direction:column;align-items:center;gap:3px;color:var(--muted);
  font-size:10.5px;font-weight:700;padding:6px 2px;border-radius:12px}
.tabbar button .ic{font-size:19px}
.tabbar button.active{color:#fff;background:rgba(124,108,255,.16)}
@media(max-width:820px){
  .sidebar{display:none}
  .tabbar{display:block}
  .main{padding:16px 15px 108px}
  .ring{width:160px;height:160px}
}
.photo{max-width:100%;border-radius:14px;border:1px solid var(--line);display:block;margin-top:10px}
.note-note{background:#121736;border:1px solid var(--line);border-radius:13px;padding:11px 13px;font-size:13.5px;white-space:pre-wrap;word-break:break-word}
.hint{font-size:12px;color:var(--dim);margin-top:8px;line-height:1.5}
</style>
</head>
<body>
<div class="app">
  <aside class="sidebar">
    <div class="brand"><span class="logo">🎓</span><span>StudyQuest</span></div>
    <button class="nav-item active" data-nav="dashboard"><span class="ic">🏠</span>Dashboard</button>
    <button class="nav-item" data-nav="plan"><span class="ic">🗺️</span>What should I study?</button>
    <button class="nav-item" data-nav="ai"><span class="ic">🤖</span>AI Study Tools</button>
    <button class="nav-item" data-nav="progress"><span class="ic">📊</span>Progress &amp; Badges</button>
    <div class="side-foot">
      <b>Offline mode.</b><br>Progress is saved in this browser. No account, no cloud.
      <div style="margin-top:10px"><button class="btn sm ghost" id="resetAll">Reset all data</button></div>
    </div>
  </aside>

  <main class="main">
    <div class="topbar">
      <div class="hello">
        <h1 id="greet">Hey, student 👋</h1>
        <p id="greetSub">Let's make today count.</p>
      </div>
      <div class="hud">
        <div class="chip">🔥 <span id="chipStreak">0</span><small>day streak</small></div>
        <div class="chip">⭐ <span id="chipXp">0</span><small>XP</small></div>
        <div class="chip">🏆 <span id="chipLevel">1</span><small>level</small></div>
        <div class="xpwrap">
          <span style="font-size:12.5px;font-weight:800;color:var(--muted)">LV <span id="hudLevel">1</span></span>
          <span class="xpbar"><i id="hudBar" style="width:0%"></i></span>
          <span style="font-size:12px;font-weight:700;color:var(--muted)" id="hudXp">0/200</span>
        </div>
      </div>
    </div>

    <!-- ================= DASHBOARD ================= -->
    <section class="view active" id="view-dashboard">
      <div class="grid g21">
        <div class="card">
          <h2>📚 Today's subjects</h2>
          <p class="sub" id="todaySub">Generated from your upcoming tests and assignments.</p>
          <div id="todayPlan" class="list"></div>
          <button class="btn sm" style="margin-top:11px" data-goto="plan">🗺️ Edit my plan</button>
        </div>

        <div class="card">
          <h2>⏰ Study timer</h2>
          <p class="sub">Every minute earns XP. Streaks count real focus time.</p>
          <div class="timer">
            <div class="ring">
              <svg width="186" height="186" viewBox="0 0 186 186">
                <circle cx="93" cy="93" r="82" stroke="#242b4d" stroke-width="12" fill="none"></circle>
                <circle id="ringFg" cx="93" cy="93" r="82" stroke="url(#gr)" stroke-width="12" fill="none"
                        stroke-linecap="round" stroke-dasharray="515.2" stroke-dashoffset="515.2"></circle>
                <defs><linearGradient id="gr" x1="0" y1="0" x2="1" y2="1">
                  <stop offset="0%" stop-color="#7c6cff"></stop><stop offset="100%" stop-color="#41d6ff"></stop>
                </linearGradient></defs>
              </svg>
              <div class="mid"><b id="clock">25:00</b><span id="timerLabel">ready</span></div>
            </div>
            <div class="presets">
              <button class="btn sm" data-min="15">15m</button>
              <button class="btn sm" data-min="25">25m</button>
              <button class="btn sm" data-min="45">45m</button>
            </div>
            <div class="row">
              <select id="timerSubject" style="flex:1"></select>
            </div>
            <div class="hstack" style="justify-content:center;width:100%">
              <button class="btn primary" id="timerToggle">▶ Start</button>
              <button class="btn ghost" id="timerStop">■ Finish</button>
            </div>
            <div class="hint" id="timerHint">Finishing a session of 1+ minutes logs it in your streak.</div>
          </div>
        </div>

        <div class="card">
          <h2>✅ Homework &amp; tasks</h2>
          <p class="sub">What still needs doing. Each one you tick is +15 XP.</p>
          <div class="row" style="margin-bottom:10px">
            <input type="text" id="taskTitle" placeholder="e.g. Worksheet page 42" style="flex:2">
            <input type="text" id="taskSubject" placeholder="Subject" style="flex:1">
            <input type="date" id="taskDue" style="flex:1">
          </div>
          <button class="btn primary sm" id="addTask">+ Add task</button>
          <div id="taskList" class="list" style="margin-top:12px"></div>
        </div>

        <div class="card">
          <h2>🔥 Study streak</h2>
          <p class="sub">Last 14 days. Focus time turns the squares purple.</p>
          <div class="heat" id="heat"></div>
          <div class="hstack" style="margin-top:13px;gap:16px">
            <div><div style="font-size:22px;font-weight:800" id="stStreak">0</div><small style="color:var(--muted)">current</small></div>
            <div><div style="font-size:22px;font-weight:800" id="stBest">0</div><small style="color:var(--muted)">best</small></div>
            <div><div style="font-size:22px;font-weight:800" id="stMin">0</div><small style="color:var(--muted)">minutes today</small></div>
          </div>
        </div>

        <div class="card">
          <h2>🧠 Daily quiz</h2>
          <p class="sub">5 questions from your notes. Wrong ones come back in "Practice Again".</p>
          <div id="quizBox"></div>
        </div>

        <div class="card">
          <h2>📝 Quick notes</h2>
          <p class="sub">Autosaved. Paste notes here and the AI tools can turn them into questions.</p>
          <textarea id="noteInput" placeholder="Jot anything — a formula, a definition, a reminder…"></textarea>
          <button class="btn primary sm" style="margin-top:9px" id="addNote">+ Save note</button>
          <div id="noteList" class="list" style="margin-top:12px"></div>
        </div>

        <div class="card wide">
          <h2>📊 Progress at a glance</h2>
          <div class="grid g3" style="margin-top:6px">
            <div class="stat"><b id="pQ">0</b><small>questions completed</small></div>
            <div class="stat"><b id="pAcc">—</b><small>quiz accuracy</small></div>
            <div class="stat"><b id="pMin">0</b><small>total minutes studied</small></div>
          </div>
          <div class="bars" id="subjectBars" style="margin-top:16px"></div>
        </div>
      </div>
    </section>

    <!-- ================= PLAN ================= -->
    <section class="view" id="view-plan">
      <div class="grid g21">
        <div class="card">
          <h2>💡 "What should I study?"</h2>
          <p class="sub">List your tests and assignments with dates. StudyQuest builds the day-by-day plan for you.</p>
          <div class="row" style="margin-bottom:8px">
            <input type="text" id="asTitle" placeholder="Math test" style="flex:2">
            <input type="text" id="asSubject" placeholder="Math" style="flex:1">
            <input type="date" id="asDate" style="flex:1">
            <select id="asWeight" style="flex:0 0 125px">
              <option value="1">Normal</option>
              <option value="1.6">Big / exam</option>
              <option value="0.7">Small</option>
            </select>
          </div>
          <button class="btn primary sm" id="addAs">+ Add to plan</button>
          <div id="asList" class="list" style="margin-top:13px"></div>
        </div>
        <div class="card">
          <h2>🎯 How the plan is built</h2>
          <div class="steps">
            <li>Anything due <b>soonest</b> gets studied first.</li>
            <li>Heavier items (exams) get more weight and longer blocks.</li>
            <li>Max <b>2 subjects per day</b> so you don't overload.</li>
            <li>Blocks are <b>20–30 minutes</b> — short enough to actually start.</li>
            <li>Empty day? It becomes a spaced-review block of the questions you missed.</li>
          </div>
        </div>
        <div class="card wide">
          <div class="spread" style="margin-bottom:12px">
            <h2 style="margin:0">📅 Your study plan</h2>
            <span class="pill" id="planCount">0 items</span>
          </div>
          <div id="planDays" class="grid g3"></div>
        </div>
      </div>
    </section>

    <!-- ================= AI TOOLS ================= -->
    <section class="view" id="view-ai">
      <div class="card wide">
        <h2>🤖 AI study tools</h2>
        <p class="sub">These run <b>fully offline</b> in your browser — no API key, nothing uploaded. They use a rule-based study engine:
          pattern matching, cloze generation, an arithmetic/equation solver and a plain-English rewriter.
          Perfect for drills and self-testing; for essay-level reasoning you'd plug in a cloud model later.</p>
        <div class="hstack">
          <button class="btn sm" data-tool="snap">📸 Snap Homework</button>
          <button class="btn sm" data-tool="quiz">🧠 Make a Quiz</button>
          <button class="btn sm" data-tool="cards">📝 Make Flashcards</button>
          <button class="btn sm" data-tool="explain">🎤 Explain It</button>
          <button class="btn sm" data-tool="again">🔄 Practice Again (<span id="wrongCount">0</span>)</button>
        </div>
      </div>

      <!-- snap -->
      <div class="grid g2" id="tool-snap" style="display:none">
        <div class="card">
          <h2>📸 Snap Homework</h2>
          <p class="sub">Photograph the question, then type or paste the text (this offline build has no OCR — it solves from text).</p>
          <input type="file" id="snapFile" accept="image/*" capture="environment">
          <img id="snapPreview" class="photo" style="display:none" alt="your homework photo">
          <label class="lb">Question text</label>
          <textarea id="snapText" placeholder="e.g. Solve 3x + 5 = 20    or    15% of 80    or    Explain photosynthesis"></textarea>
          <button class="btn primary sm" style="margin-top:10px" id="snapSolve">🧩 Explain &amp; solve</button>
          <div class="hint">Handles: arithmetic, percentages, linear equations, word problems, and explanation requests.</div>
        </div>
        <div class="card">
          <h2>🧩 Explanation</h2>
          <div id="snapOut"><div class="empty">Your step-by-step explanation will appear here.</div></div>
        </div>
      </div>

      <!-- quiz maker -->
      <div class="grid g2" id="tool-quiz" style="display:none">
        <div class="card">
          <h2>🧠 Make a Quiz</h2>
          <p class="sub">Paste notes or a textbook paragraph. StudyQuest builds real questions from your own material.</p>
          <label class="lb">Your notes</label>
          <textarea id="quizSrc" style="min-height:190px" placeholder="Photosynthesis is the process by which plants convert light energy into chemical energy. Chlorophyll absorbs red and blue light…"></textarea>
          <div class="row" style="margin-top:10px">
            <label class="lb" style="margin:0">Questions
              <select id="quizN"><option>5</option><option>8</option><option>10</option></select>
            </label>
            <label class="lb" style="margin:0">Style
              <select id="quizStyle"><option value="mixed">Mixed</option><option value="cloze">Fill in the blank</option><option value="def">Definition questions</option></select>
            </label>
          </div>
          <button class="btn primary sm" style="margin-top:11px" id="makeQuiz">⚡ Generate questions</button>
          <button class="btn sm" style="margin-top:11px" id="saveSrc">💾 Save these notes</button>
          <div class="hint">Tip: 6–15 clean sentences gives the best questions.</div>
        </div>
        <div class="card">
          <div class="spread" style="margin-bottom:10px">
            <h2 style="margin:0">📋 Generated quiz</h2>
            <button class="btn sm" id="startGenQuiz">▶ Start quiz</button>
          </div>
          <div id="quizPreview"><div class="empty">Questions will appear here.</div></div>
        </div>
      </div>

      <!-- flashcards -->
      <div class="grid g2" id="tool-cards" style="display:none">
        <div class="card">
          <h2>📝 Make Flashcards</h2>
          <p class="sub">Paste notes. Each key sentence becomes a card — tap a card to flip it.</p>
          <textarea id="fcSrc" style="min-height:170px" placeholder="Mitosis is cell division that produces two identical cells.…"></textarea>
          <button class="btn primary sm" style="margin-top:10px" id="makeCards">⚡ Create flashcards</button>
          <button class="btn sm" style="margin-top:10px" id="saveDeck">💾 Save deck</button>
          <div class="hint">Works best with sentences that define or describe one idea.</div>
        </div>
        <div class="card">
          <h2>🃏 Your cards <span class="pill" id="fcCount" style="margin-left:6px">0</span></h2>
          <div class="deck" id="fcDeck"><div class="empty">No cards yet.</div></div>
        </div>
      </div>

      <!-- explain -->
      <div class="grid g2" id="tool-explain" style="display:none">
        <div class="card">
          <h2>🎤 Explain It</h2>
          <p class="sub">Paste a hard paragraph. You get a plain-English version, key words, and an analogy.</p>
          <textarea id="exSrc" style="min-height:180px" placeholder="Paste a dense paragraph from your textbook…"></textarea>
          <div class="row" style="margin-top:8px">
            <select id="exLevel"><option value="simple">Explain simply</option><option value="eli5">Explain like I'm 5</option></select>
          </div>
          <button class="btn primary sm" style="margin-top:10px" id="explainBtn">✨ Simplify it</button>
          <button class="btn sm" style="margin-top:10px" id="exFromNote">📝 Use my latest note</button>
        </div>
        <div class="card">
          <h2>💡 Simple version</h2>
          <div id="exOut"><div class="empty">The simplified explanation appears here.</div></div>
        </div>
      </div>

      <!-- practice again -->
      <div class="grid g1" id="tool-again" style="display:none">
        <div class="card">
          <div class="spread" style="margin-bottom:10px">
            <h2 style="margin:0">🔄 Practice Again</h2>
            <span class="pill" id="wrongPill">0 waiting</span>
          </div>
          <p class="sub">Every question you get wrong is remembered and turned into a <b>new</b> question on the same material.</p>
          <div id="againBox"><div class="empty">Nothing to retry yet — take a quiz first.</div></div>
        </div>
      </div>
    </section>

    <!-- ================= PROGRESS ================= -->
    <section class="view" id="view-progress">
      <div class="grid g3">
        <div class="card"><h2>🏆 Level</h2><div class="stat" style="margin-top:8px"><b id="pgLevel">1</b><small id="pgLevelSub">0 / 200 XP to next</small></div>
          <div class="xpbar" style="margin-top:12px"><i id="pgBar" style="width:0%"></i></div></div>
        <div class="card"><h2>⭐ Total XP</h2><div class="stat" style="margin-top:8px"><b id="pgXp">0</b><small>points earned</small></div>
          <div class="hint" id="xpRules">XP: 10/question · 15/task · 2/minute studied</div></div>
        <div class="card"><h2>🔥 Streak</h2><div class="stat" style="margin-top:8px"><b id="pgStreak">0</b><small>days in a row</small></div>
          <div class="hint">Best: <b id="pgBest">0</b> days</div></div>
      </div>
      <div class="grid g1">
        <div class="card">
          <h2>🥇 Badges</h2>
          <p class="sub">Unlock them by actually studying. They light up as you go.</p>
          <div class="badges" id="badgeGrid"></div>
        </div>
      </div>
      <div class="grid g2">
        <div class="card"><h2>📊 Questions</h2>
          <div class="grid g2" style="margin-top:6px">
            <div class="stat"><b id="pgQ">0</b><small>answered</small></div>
            <div class="stat"><b id="pgAcc">—</b><small>accuracy</small></div>
          </div></div>
        <div class="card"><h2>⏱️ Study time by subject</h2><div class="bars" id="bars2" style="margin-top:10px"></div></div>
      </div>
    </section>
  </main>
</div>

<nav class="tabbar"><div class="inner">
  <button class="active" data-nav="dashboard"><span class="ic">🏠</span>Home</button>
  <button data-nav="plan"><span class="ic">🗺️</span>Plan</button>
  <button data-nav="ai"><span class="ic">🤖</span>AI</button>
  <button data-nav="progress"><span class="ic">📊</span>Progress</button>
</div></nav>

<div id="toasts"></div>

<script>
(function(){
"use strict";

/* ============================ helpers ============================ */
const $ = s => document.querySelector(s);
const $$ = s => Array.from(document.querySelectorAll(s));
const KEY = "studyquest.v1";
const esc = s => String(s==null?"":s).replace(/[&<>"']/g, c => ({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]));
const dayStr = d => { const x=new Date(d); return x.getFullYear()+"-"+String(x.getMonth()+1).padStart(2,"0")+"-"+String(x.getDate()).padStart(2,"0"); };
const today = () => dayStr(new Date());
const addDays = (d,n) => { const x=new Date(d); x.setDate(x.getDate()+n); return x; };
const parseDay = s => { const p=String(s||"").split("-").map(Number); return new Date(p[0], (p[1]||1)-1, p[2]||1); };
const daysUntil = s => Math.round((parseDay(s) - parseDay(today()))/86400000);
const uid = () => Math.random().toString(36).slice(2,9);
/* storage that never throws (private mode, file://, blocked cookies) */
const store = (() => {
  let ok = true;
  try { window.localStorage.setItem("__sq","1"); window.localStorage.removeItem("__sq"); } catch(e){ ok = false; }
  return {
    get(k){ try{ return ok ? window.localStorage.getItem(k) : null; }catch(e){ return null; } },
    set(k,v){ try{ if(ok) window.localStorage.setItem(k,v); }catch(e){} }
  };
})();
const shuffle = a => { const b=a.slice(); for(let i=b.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[b[i],b[j]]=[b[j],b[i]];} return b; };
const clamp=(n,a,b)=>Math.max(a,Math.min(b,n));

/* ============================ state ============================ */
const DEFAULTS = {
  xp:0, sessions:[], tasks:[], assessments:[], notes:[], decks:[],
  questionsDone:0, correct:0, wrongQueue:[], badges:[], perfectQuizzes:0,
  savedSource:"", cards:[], planSeen:false
};
let S = load();
function load(){
  try{
    const raw = store.get(KEY);
    if(!raw) return Object.assign({}, DEFAULTS);
    return Object.assign({}, DEFAULTS, JSON.parse(raw));
  }catch(e){ return Object.assign({}, DEFAULTS); }
}
function save(){
  store.set(KEY, JSON.stringify(S));
}

/* ============================ xp / level ============================ */
const XP_PER_LEVEL = 200;
const levelOf = xp => Math.floor(xp / XP_PER_LEVEL) + 1;
const levelProg = xp => (xp % XP_PER_LEVEL) / XP_PER_LEVEL;

function addXP(n, why){
  const before = levelOf(S.xp);
  S.xp += n;
  const after = levelOf(S.xp);
  save();
  if(after > before) toast("🏆 Level up! You're now level " + after, 4200);
  if(why) toast("+" + n + " XP · " + why, 2200);
  renderHUD();
}
function toast(msg, ms){
  const el = document.createElement("div");
  el.className = "toast"; el.innerHTML = msg;
  $("#toasts").appendChild(el);
  setTimeout(()=>{ el.style.transition=".35s"; el.style.opacity="0"; el.style.transform="translateY(10px)";
    setTimeout(()=>el.remove(),360); }, ms||2600);
}

/* ============================ streak ============================ */
function minutesByDay(){
  const m = {};
  S.sessions.forEach(s => { m[s.date] = (m[s.date]||0) + s.minutes; });
  return m;
}
function streakInfo(){
  const m = minutesByDay();
  const days = Object.keys(m).filter(d => m[d] >= 1).sort();
  const set = new Set(days);
  let cur = 0;
  let cursor = new Date();
  if(!set.has(dayStr(cursor))) cursor = addDays(cursor,-1);
  while(set.has(dayStr(cursor))){ cur++; cursor = addDays(cursor,-1); }
  let best = 0, run = 0, prev = null;
  days.forEach(d => {
    if(prev && Math.round((parseDay(d)-parseDay(prev))/86400000) === 1) run++;
    else run = 1;
    best = Math.max(best, run); prev = d;
  });
  return { current: cur, best: Math.max(best, cur) };
}
function totalMinutes(){ return S.sessions.reduce((a,s)=>a+s.minutes,0); }

/* ============================ badges ============================ */
const BADGES = [
  {id:"first",  icon:"🥉", name:"First Study Session", desc:"Log one session",           check:()=> S.sessions.length>0},
  {id:"streak7",icon:"🥈", name:"7-Day Streak",        desc:"Study 7 days in a row",      check:()=> streakInfo().current>=7},
  {id:"q100",   icon:"🥇", name:"100 Questions",       desc:"Answer 100 questions",       check:()=> S.questionsDone>=100},
  {id:"streak30",icon:"💎",name:"30-Day Streak",       desc:"Study 30 days in a row",     check:()=> streakInfo().current>=30},
  {id:"lvl5",   icon:"🚀", name:"Level 5",             desc:"Reach level 5",              check:()=> levelOf(S.xp)>=5},
  {id:"perfect",icon:"🎯", name:"Sharp Shooter",       desc:"Get a perfect quiz",         check:()=> S.perfectQuizzes>=1},
  {id:"planner",icon:"🗺️", name:"Planner Pro",         desc:"Track 3 assessments",        check:()=> S.assessments.length>=3},
  {id:"cards",  icon:"🃏", name:"Card Shark",          desc:"Save 10 flashcards",         check:()=> S.cards.length>=10}
];
function checkBadges(){
  let fresh = [];
  BADGES.forEach(b => {
    if(S.badges.indexOf(b.id) === -1 && b.check()){
      S.badges.push(b.id); fresh.push(b);
    }
  });
  if(fresh.length){ save(); fresh.forEach(b => toast(b.icon + " Badge unlocked — <b>" + esc(b.name) + "</b>", 4200)); }
}

/* ============================ study engine ============================ */
const STOP = new Set(("the a an and or but if then than that this these those of to in on at for with from by as is are was were be been being it its it's "+
"you your we our they their he she his her i me my not no do does did doing have has had having will would can could should may might must "+
"there here what which who whom whose when where why how all any both each few more most other some such only own same so too very just about into over after").split(" "));

function keyTerms(text){
  const seen = {};
  (String(text||"").match(/[A-Za-z][A-Za-z'-]{2,}/g) || []).forEach(w => {
    const lw = w.toLowerCase();
    if(STOP.has(lw)) return;
    seen[w] = (seen[w]||0) + 1;
  });
  return Object.keys(seen).sort((a,b)=> b.length - a.length || a.localeCompare(b));
}
function sentencesOf(text){
  /* no regex lookbehind — keeps older Safari on school devices happy */
  const t = String(text||"").replace(/\s+/g," ").trim();
  const parts = t.match(/[^.!?]+[.!?]+|[^.!?]+$/g) || [];
  return parts.map(s=>s.trim()).filter(s => s.split(" ").length >= 4);
}
function longWordsIn(s){
  return (s.match(/[A-Za-z][A-Za-z'-]{4,}/g) || []).filter(w => !STOP.has(w.toLowerCase()));
}
function defPattern(s){
  const m = s.match(/^(.{2,70}?)\s+(?:is|are|was|were|means|refers to|is defined as|describes)\s+(.{8,})$/i);
  if(!m) return null;
  const sub = m[1].replace(/^(the|a|an)\s+/i,"").trim();
  if(sub.split(" ").length > 6) return null;
  return { term: sub, def: m[2].replace(/\s*[.;]$/,"").trim(), sentence:s };
}

/* --- question generation from notes --- */
let pool = [];          // generated question bank (session)
function makeQuestions(text, n, style){
  const sents = sentencesOf(text);
  if(!sents.length) return [];
  const allTerms = keyTerms(text);
  const allDefs = [];
  sents.forEach(s => { const dd = defPattern(s); if(dd) allDefs.push(dd.def); });
  const qs = [];
  const usedSent = {};
  const buckets = [];
  sents.forEach(s => {
    const d = defPattern(s);
    if(d) buckets.push({kind:"def", s, d});
    else buckets.push({kind:"cloze", s});
  });
  const order = style === "def" ? ["def","cloze"] : style === "cloze" ? ["cloze","def"] : ["def","cloze"];
  order.forEach(kind => {
    buckets.forEach(b => {
      if(b.kind !== kind || usedSent[b.s] || qs.length >= n) return;
      usedSent[b.s] = true;
      if(kind === "def"){
        const wrongs = shuffle(allDefs.filter(dd => dd.toLowerCase() !== b.d.def.toLowerCase()).slice()).slice(0,3);
        if(wrongs.length < 3){
          const fillers = shuffle(allTerms.filter(t => t.length >= 6 && t.toLowerCase() !== b.d.term.toLowerCase()))
            .map(t => "a kind of " + t.toLowerCase()).filter(x => wrongs.indexOf(x) === -1);
          fillers.forEach(f => { if(wrongs.length < 3 && wrongs.indexOf(f) === -1) wrongs.push(f); });
        }
        while(wrongs.length < 3) wrongs.push(["a type of energy","a measurement tool","a chemical reaction","a type of machine"][wrongs.length]);
        qs.push({ type:"mcq", q:"What is " + b.d.term + "?",
          a: b.d.def, options: shuffle([b.d.def].concat(wrongs)), sentence:b.s });
      } else {
        const ws = b.s.split(" ");
        let idx = -1, best = 0;
        ws.forEach((w,i) => { const c = w.replace(/[^A-Za-z0-9'-]/g,""); if(c.length > best && c.length >= 4){ best = c.length; idx = i; } });
        if(idx < 0) return;
        const answer = ws[idx].replace(/[^A-Za-z0-9'-]/g,"");
        const blanked = ws.map((w,i) => i === idx ? "________" : w).join(" ");
        const wrongs = shuffle(longWordsIn(text).filter(w =>
            w.toLowerCase() !== answer.toLowerCase() && w.length >= 5 && w.length <= answer.length + 6))
                        .slice(0,3)
                        .map(w => w.replace(/[^A-Za-z0-9'-]/g,""));
        const opts = Array.from(new Set([answer].concat(wrongs)));
        while(opts.length < 4) opts.push("option" + opts.length);
        qs.push({ type:"mcq", q: blanked, a: answer, options: shuffle(opts),
          sentence:b.s, blankIdx:idx, answerIdx:idx });
      }
    });
  });
  return qs.slice(0, n);
}
/* variant generator for Practice Again */
function variantOf(item){
  if(item.sentence){
    const ws = item.sentence.split(" ");
    const cands = [];
    ws.forEach((w,i) => { const c = w.replace(/[^A-Za-z0-9'-]/g,""); if(c.length >= 5 && i !== item.blankIdx) cands.push(i); });
    if(cands.length){
      const idx = cands[Math.floor(Math.random()*cands.length)];
      const answer = ws[idx].replace(/[^A-Za-z0-9'-]/g,"");
      const blanked = ws.map((w,i) => i === idx ? "________" : w).join(" ");
      const other = shuffle((item.sentence.match(/[A-Za-z][A-Za-z'-]{4,}/g)||[])
        .filter(w => w.toLowerCase() !== answer.toLowerCase())).slice(0,3).map(w => w.replace(/[^A-Za-z0-9'-]/g,""));
      const opts = Array.from(new Set([answer].concat(other)));
      while(opts.length < 4) opts.push("option" + opts.length);
      return { type:"mcq", q: blanked, a: answer, options: shuffle(opts), sentence:item.sentence, blankIdx:idx };
    }
  }
  return { type:"mcq", q:item.q, a:item.a, options:shuffle((item.options||[item.a]).slice()), sentence:item.sentence, blankIdx:item.blankIdx };
}
/* starter bank so the daily quiz works on day one */
const STARTER = [
  {type:"mcq", q:"Solve 3x + 5 = 20. What is x?", a:"5", options:["5","15","25","3"]},
  {type:"mcq", q:"What is 15% of 80?", a:"12", options:["12","8","15","24"]},
  {type:"mcq", q:"Which gas do plants absorb during photosynthesis?", a:"Carbon dioxide", options:["Carbon dioxide","Oxygen","Nitrogen","Hydrogen"]},
  {type:"mcq", q:"What is the past tense of “go”?", a:"went", options:["went","goed","gone","going"]},
  {type:"mcq", q:"What is the area of a rectangle 7 cm by 4 cm?", a:"28 cm²", options:["28 cm²","22 cm²","11 cm²","14 cm²"]},
  {type:"mcq", q:"What is the value of 8² − 6²?", a:"28", options:["28","4","64","36"]},
  {type:"mcq", q:"Which word is a synonym of “rapid”?", a:"fast", options:["fast","slow","heavy","quiet"]},
  {type:"mcq", q:"What is the main organ of the human circulatory system?", a:"The heart", options:["The heart","The liver","The lungs","The kidney"]},
  {type:"mcq", q:"Solve: 2(x + 3) = 14. What is x?", a:"4", options:["4","7","5","11"]},
  {type:"mcq", q:"What is 3/4 written as a decimal?", a:"0.75", options:["0.75","0.34","1.33","0.43"]}
];
function questionPool(){
  return pool.length ? pool.concat(STARTER) : STARTER.slice();
}
function buildPool(n){
  const notes = S.savedSource || "";
  let qs = notes.length > 40 ? makeQuestions(notes, n || 8, "mixed") : [];
  return qs;
}

/* ============================ quiz runner ============================ */
let quiz = null;   // {qs:[], i:0, right:0, wrong:0, mode:'daily'|'gen'|'again', answered:false}
function startQuiz(qs, mode){
  if(!qs.length){ toast("No questions available yet — add some notes first."); return; }
  quiz = { qs, i:0, right:0, wrong:0, mode:mode||"daily", answered:false, target: pickTarget(mode) };
  renderQuiz();
}
function pickTarget(mode){
  if(mode === "again") return "#quizBox";
  return mode === "gen" ? "#quizPreview" : "#quizBox";
}
function renderQuiz(){
  if(!quiz) return;
  const el = $(quiz.target);
  if(!el) return;
  if(quiz.i >= quiz.qs.length){
    const q = quiz;
    const acc = q.right + q.wrong ? Math.round(q.right/(q.right+q.wrong)*100) : 0;
    if(q.mode !== "again"){
      S.questionsDone += q.right + q.wrong;
      S.correct += q.right;
      if(q.wrong === 0 && q.right > 0) S.perfectQuizzes++;
      save(); checkBadges();
    }
    el.innerHTML = '<div class="fb ok" style="text-align:center">🏁 Done! ' + q.right + ' correct of ' + (q.right+q.wrong) +
      ' (' + acc + '%)</div>' +
      '<div class="hstack" style="margin-top:11px">' +
      '<button class="btn primary sm" id="quizAgainBtn">' + (q.mode === "again" ? "🔄 Practice more" : "🧠 New quiz") + '</button>' +
      '<button class="btn sm" data-goto="ai">🤖 Make my own quiz</button></div>';
    const b = $("#quizAgainBtn");
    if(b) b.addEventListener("click", () => {
      if(q.mode === "again") startAgain();
      else startDaily();
    });
    renderHUD(); renderProgress(); renderAgain();
    return;
  }
  const q = quiz.qs[quiz.i];
  const opts = q.options ? shuffle(q.options) : null;
  el.innerHTML =
    '<div class="spread" style="margin-bottom:9px"><span class="pill">Question ' + (quiz.i+1) + " / " + quiz.qs.length + '</span>' +
    '<span class="pill">' + quiz.right + ' ✓</span></div>' +
    '<div class="qtext">' + esc(q.q) + '</div>' +
    (opts ? '<div class="opts">' + opts.map(o => '<button class="opt" data-opt="' + esc(o) + '">' + esc(o) + '</button>').join("") + '</div>'
          : '<div class="hstack" style="margin-top:10px"><input type="text" id="clozeIn" placeholder="Type the missing word"><button class="btn primary sm" id="clozeGo">Check</button></div>') +
    '<div id="fbSlot"></div>';
  if(opts){
    Array.from(el.querySelectorAll("[data-opt]")).forEach(b => {
      b.addEventListener("click", () => answerQuiz(b.getAttribute("data-opt"), b, q, opts));
    });
  } else {
    const inp = el.querySelector("#clozeIn");
    const go = () => answerQuiz((inp.value||"").trim(), null, q, null);
    el.querySelector("#clozeGo").addEventListener("click", go);
    inp.addEventListener("keydown", e => { if(e.key === "Enter") go(); });
    inp.focus();
  }
}
function answerQuiz(given, btn, q, allOpts){
  if(quiz.answered) return;
  quiz.answered = true;
  const norm = s => String(s||"").toLowerCase().replace(/[^a-z0-9]/g,"");
  const ok = norm(given) === norm(q.a);
  if(ok){ quiz.right++; addXP(10); }
  else {
    quiz.wrong++;
    S.wrongQueue.push({ q:q.q, a:q.a, options:q.options||null, sentence:q.sentence||null, blankIdx:q.blankIdx, at:Date.now() });
    if(S.wrongQueue.length > 60) S.wrongQueue = S.wrongQueue.slice(-60);
    save();
  }
  if(allOpts){
    Array.from($(quiz.target).querySelectorAll("[data-opt]")).forEach(b => {
      if(norm(b.getAttribute("data-opt")) === norm(q.a)) b.classList.add("good");
      else if(b === btn) b.classList.add("bad");
      b.disabled = true;
    });
  }
  const slot = $(quiz.target).querySelector("#fbSlot");
  if(slot) slot.innerHTML = '<div class="fb ' + (ok?"ok":"no") + '">' +
    (ok ? "✅ Correct! +10 XP" : "❌ Not quite. Answer: <b>" + esc(q.a) + "</b> — saved to Practice Again.") + '</div>' +
    '<button class="btn primary sm" style="margin-top:10px" id="nextQ">Next →</button>';
  const nb = $(quiz.target).querySelector("#nextQ");
  if(nb) nb.addEventListener("click", () => { quiz.i++; quiz.answered = false; renderQuiz(); });
}
function startDaily(){ startQuiz(shuffle(questionPool().concat(S.wrongQueue.map(variantOf))).slice(0,5), "daily"); }
function startAgain(){
  const items = S.wrongQueue.map(variantOf);
  if(!items.length){ toast("Nothing to practice — you're all caught up! 🎉"); return; }
  startQuiz(shuffle(items).slice(0,6), "again");
}

/* ============================ offline solver ============================ */
function solveArithmetic(expr){
  let e = String(expr).replace(/×/g,"*").replace(/÷/g,"/").replace(/−/g,"-").replace(/\^/g,"**");
  if(!/^[\d\s+\-*/().%*]+$/.test(e)) return null;
  if(!/[+\-*/]/.test(e)) return null;
  try{
    const val = Function('"use strict";return (' + e + ')')();
    if(typeof val !== "number" || !isFinite(val)) return null;
    return { value: Math.round(val*1e6)/1e6, expr:e.trim() };
  }catch(err){ return null; }
}
function solveLinear(text){
  const t = text.replace(/\s+/g,"").replace(/×/g,"*");
  const m = t.match(/([-+]?\d*\.?\d*)\*?x([-+]\d+\.?\d*)?=([-+]?\d+\.?\d*)/i);
  if(!m) return null;
  const a = m[1] === "" || m[1] === "+" ? 1 : m[1] === "-" ? -1 : parseFloat(m[1]);
  const b = m[2] ? parseFloat(m[2]) : 0;
  const c = parseFloat(m[3]);
  return { a, b, c, x: (c - b) / a };
}
function solvePercent(text){
  const m = String(text).match(/(\d+\.?\d*)\s*%\s*(?:of)\s*(\d+\.?\d*)/i);
  if(!m) return null;
  const p = parseFloat(m[1]), n = parseFloat(m[2]);
  return { p, n, value: Math.round(p/100*n*1e4)/1e4 };
}
const SIMPLE_MAP = {
  "utilize":"use","utilize ":"use","utilization":"use","approximately":"about","demonstrate":"show","sufficient":"enough",
  "numerous":"many","obtain":"get","requires":"needs","require":"need","purchase":"buy","commence":"start","terminate":"end",
  "prior to":"before","in order to":"to","due to the fact that":"because","individuals":"people","additional":"extra",
  "assist":"help","attempt":"try","consequently":"so","furthermore":"also","however":"but","therefore":"so","regarding":"about",
  "concerning":"about","substantial":"large","initiate":"start","finalize":"finish","ascertain":"find out","subsequently":"later",
  "in the event that":"if","a number of":"several","in addition":"also","nevertheless":"still","facilitate":"help",
  "optimal":"best","fundamental":"basic","comprehend":"understand","construct":"build","investigate":"study","methodology":"method",
  "component":"part","modification":"change","transformation":"change","exhibits":"shows","possesses":"has"
};
function simplify(text, level){
  const sents = sentencesOf(text);
  if(!sents.length) return null;
  const out = [];
  const endings = ["ing","ed","es","s","d"];
  function fit(base, suf){
    if(!suf) return base;
    if(suf === "ing") return /e$/.test(base) ? base.slice(0,-1)+"ing" : base+"ing";
    if(suf === "ed" || suf === "d") return /e$/.test(base) ? base+"d" : base+"ed";
    if(suf === "es") return /(s|x|ch|sh)$/.test(base) ? base+"es" : base+"s";
    return base+"s";
  }
  sents.forEach(s => {
    let t = s;
    Object.keys(SIMPLE_MAP).forEach(k => {
      t = t.replace(new RegExp("\\b" + k + "(" + endings.join("|") + ")?\\b","gi"), (m, suf) => {
        const r = fit(SIMPLE_MAP[k], suf ? suf.toLowerCase() : "");
        return m[0] === m[0].toUpperCase() ? r[0].toUpperCase()+r.slice(1) : r;
      });
    });
    t = t.replace(/\s+/g," ").trim();
    let parts = t.split(/\s*[,;:]\s+|\s+(?:which|that|because|although|while|whereas)\s+/i)
                 .map(x => x.replace(/^[,;:]\s*/,"").trim()).filter(Boolean);
    if(level === "eli5"){
      parts = parts.slice(0,2).map(p => p
        .replace(/\bphotosynthesis\b/gi,"how plants make their own food")
        .replace(/\bmetabolism\b/gi,"how your body turns food into energy")
        .replace(/\bequilibrium\b/gi,"when two sides are balanced")
        .replace(/\bmolecule\b/gi,"tiny building block")
        .replace(/\borganism\b/gi,"living thing"));
    }
    parts.forEach(p => {
      const words = p.split(" ").length;
      if(words > 16){
        const cut = p.split(/\s+(?:and|but|so|then)\s+/i);
        cut.forEach(c => out.push(c.trim()));
      } else out.push(p);
    });
  });
  return out.filter(Boolean);
}
function analogiesFor(text){
  const t = String(text).toLowerCase();
  const list = [];
  if(/photosynth/.test(t)) list.push("🌱 Photosynthesis is like a plant's kitchen: sunlight is the stove, CO₂ and water are the ingredients, glucose is the meal, oxygen is the steam.");
  if(/mitosis|cell division/.test(t)) list.push("🧬 Mitosis is like photocopying a page — you start with one and end with two identical copies.");
  if(/newton|force|motion/.test(t)) list.push("🎳 Newton's 1st law is like a puck on ice: it keeps gliding until something (friction) pushes back.");
  if(/equation|solve for x|variable/.test(t)) list.push("⚖️ Solving an equation is like a balance scale: whatever you do to one side, do to the other.");
  if(/fraction|denominator/.test(t)) list.push("🍕 The denominator is how many slices the pizza was cut into; the numerator is how many you took.");
  if(/volcano|tectonic/.test(t)) list.push("🌋 Tectonic plates are like cracked ice on a lake — when the pieces shift, cracks and eruptions appear at the seams.");
  if(/dna|gene/.test(t)) list.push("📖 DNA is an instruction book; a gene is one recipe in that book.");
  return list;
}
function scanScaffold(q){
  const t = q.toLowerCase();
  const key = [];
  const words = q.match(/\b[A-Z][a-z]{4,}\b/g) || [];
  shuffle(words).slice(0,4).forEach(w => key.push(w));
  [
    [/solve|equation|=/, "Isolate the unknown on one side, then undo operations in reverse order."],
    [/prove|show that/, "Start from what you're given, and write each step so the last line is exactly what was asked."],
    [/explain|why|describe/, "Answer in three parts: what happens, how it happens, and why it matters."],
    [/compare|contrast|difference/, "Make a two-column table: similarities on the left, differences on the right."],
    [/graph|plot|sketch/, "Find the key points first (intercepts, peaks), then connect them."],
    [/balance|chemical equation/, "Count atoms on both sides and adjust coefficients only — never subscripts."],
    [/calculate|find the value|how much|percentage|percent/, "Write the formula first, substitute the numbers, then compute — and check the units."],
    [/word problem|altogether|remaining|each/, "Underline the numbers, name the unknown, then turn each sentence into an operation."],
    [/essay|paragraph|discuss/, "Plan: thesis → 3 supporting points → evidence for each → conclusion."]
  ].forEach(([re, tip]) => { if(re.test(t)) key.push(tip); });
  return key;
}
function solveProblem(text){
  const out = [];
  const pct = solvePercent(text);
  const lin = solveLinear(text);
  const ar = solveArithmetic(text);

  if(pct){
    out.push({n:"Identify the parts", txt:"Percent = " + pct.p + "%, Whole = " + pct.n + ". We want the part."});
    out.push({n:"Set up the formula", txt:"part = (percent ÷ 100) × whole → (" + pct.p + " ÷ 100) × " + pct.n});
    out.push({n:"Compute", txt:pct.p + " ÷ 100 = " + (pct.p/100) + " → " + (pct.p/100) + " × " + pct.n + " = " + pct.value});
    out.push({n:"Answer", txt:pct.p + "% of " + pct.n + " = <b>" + pct.value + "</b>"});
    return {title:"Percentage problem", steps:out, fact:"Answer: " + pct.value};
  }
  if(lin){
    out.push({n:"Write it down", txt:"Equation: " + lin.a + "x" + (lin.b >= 0 ? " + " + lin.b : " − " + Math.abs(lin.b)) + " = " + lin.c});
    out.push({n:"Move the constant", txt:"Subtract " + lin.b + " from both sides → " + lin.a + "x = " + (lin.c - lin.b)});
    out.push({n:"Divide by the coefficient", txt:"Divide both sides by " + lin.a + " → x = " + (lin.c - lin.b) + " ÷ " + lin.a});
    out.push({n:"Check", txt:"3x+5=20 style check: plug x back in — it should balance both sides."});
    out.push({n:"Answer", txt:"<b>x = " + (Math.round(lin.x*1e6)/1e6) + "</b>"});
    return {title:"Linear equation", steps:out, fact:"x = " + (Math.round(lin.x*1e6)/1e6)};
  }
  if(ar){
    out.push({n:"Read the expression", txt:"`" + ar.expr + "`"});
    out.push({n:"Order of operations", txt:"Brackets → Orders (powers/roots) → Division & Multiplication → Addition & Subtraction."});
    out.push({n:"Work it through", txt:"Evaluate step by step, keeping the highest-precedence operations first."});
    out.push({n:"Answer", txt:"<b>" + ar.value + "</b>"});
    return {title:"Arithmetic", steps:out, fact:"= " + ar.value};
  }
  const tips = scanScaffold(text);
  out.push({n:"What is it really asking?", txt:"Rewrite the question in your own words as a single sentence starting with “Find…” or “Explain…”."});
  out.push({n:"What do you already know?", txt:"List the given facts, formulas or definitions that connect to this question."});
  out.push({n:"Choose a method", txt:(tips.filter(t => t.split(" ").length > 4)[0]) || "Break the problem into the smallest possible first step — do only that one."});
  out.push({n:"Show your work", txt:"Write each step on its own line with a reason. If you get stuck, say exactly which line is unclear."});
  out.push({n:"Check the answer", txt:"Reverse the operation, or ask: does this number/claim make sense in the real world?"});
  out.push({n:"If it's an explanation question", txt:"Structure: definition → how it works → a concrete example → why it matters."});
  return {title:"Thinking plan", steps:out, fact:null};
}

/* ============================ renderers ============================ */
function renderHUD(){
  const lv = levelOf(S.xp);
  $("#chipXp").textContent = S.xp.toLocaleString();
  $("#chipLevel").textContent = lv;
  $("#chipStreak").textContent = streakInfo().current;
  $("#hudLevel").textContent = lv;
  $("#hudXp").textContent = (S.xp % XP_PER_LEVEL) + "/" + XP_PER_LEVEL;
  $("#hudBar").style.width = Math.round(levelProg(S.xp)*100) + "%";
  $("#wrongCount").textContent = S.wrongQueue.length;
  $("#wrongPill").textContent = S.wrongQueue.length + " waiting";
}
function renderGreeting(){
  const h = new Date().getHours();
  $("#greet").textContent = (h<12 ? "Good morning" : h<18 ? "Good afternoon" : "Good evening") + ", student 👋";
  const st = streakInfo();
  const m = minutesByDay()[today()] || 0;
  $("#greetSub").textContent = m > 0
    ? "You've already studied " + m + " min today. Streak: " + st.current + " days. 🔥"
    : (st.current > 0 ? "Keep the " + st.current + "-day streak alive — one session is enough." : "No session logged today yet. Let's start one.");
}
function subjectList(){
  const set = new Set();
  S.assessments.forEach(a => { if(a.subject) set.add(a.subject); });
  S.tasks.forEach(t => { if(t.subject) set.add(t.subject); });
  S.sessions.forEach(s => { if(s.subject) set.add(s.subject); });
  ["Math","Science","English","History","Languages"].forEach(s => set.add(s));
  return Array.from(set).slice(0,14);
}
function renderSubjectSelect(){
  const sel = $("#timerSubject");
  const cur = sel.value;
  sel.innerHTML = subjectList().map(s => '<option>' + esc(s) + '</option>').join("");
  if(cur && subjectList().indexOf(cur) !== -1) sel.value = cur;
}

/* --- planner --- */
function buildPlan(){
  if(!S.assessments.length) return null;
  const days = [];
  for(let d = 0; d < 7; d++){
    const date = dayStr(addDays(new Date(), d));
    const cands = S.assessments
      .filter(a => a.date && daysUntil(a.date) >= 0)
      .map(a => ({ a, left: daysUntil(a.date), w: parseFloat(a.weight || 1) }))
      .sort((x,y) => x.left - y.left || y.w - x.w);
    const items = [];
    const seen = {};
    cands.forEach(c => {
      if(items.length >= 2) return;
      if(seen[c.a.subject]) return;
      if(c.left > 6 - d && items.length >= 1) return;
      seen[c.a.subject] = 1;
      const mins = c.left <= 1 ? 30 : c.w >= 1.5 ? 30 : 20;
      items.push({ subject:c.a.subject, title:c.a.title, minutes:mins, left:c.left, urgent:c.left <= 1 });
    });
    if(!items.length && S.wrongQueue.length){
      items.push({ subject:"Review", title:"Redo " + Math.min(6, S.wrongQueue.length) + " questions you missed", minutes:15, left:0, urgent:false });
    }
    days.push({ date, items });
  }
  return days;
}
function renderPlan(){
  const days = buildPlan();
  const host = $("#planDays");
  if(!days){
    host.innerHTML = '<div class="empty" style="grid-column:1/-1">Add your first test or assignment on the left and the plan appears here.</div>';
    $("#planCount").textContent = "0 items";
    $("#todayPlan").innerHTML = '<div class="empty">No plan yet — add a test in <b>What should I study?</b></div>';
    $("#todaySub").textContent = "Generated from your upcoming tests and assignments.";
    return;
  }
  const total = days.reduce((a,d)=>a+d.items.length,0);
  $("#planCount").textContent = total + " study blocks";
  host.innerHTML = days.map((d,i) => {
    const label = i === 0 ? "Today · " + d.date : i === 1 ? "Tomorrow · " + d.date : d.date;
    return '<div class="daycard' + (i===0?" today":"") + '"><h3>' + label + '</h3>' +
      (d.items.length ? d.items.map(it =>
        '<div class="task"><span class="dot" style="background:' + (it.urgent?"#ff6b8a":"#7c6cff") + '"></span>' +
        '<span class="tt">' + esc(it.subject) + '<div class="min">' + esc(it.title) + ' · ' + it.minutes + ' min</div></span>' +
        '<button class="btn sm" data-start="' + esc(it.subject) + '" data-min="' + it.minutes + '">▶</button></div>').join("")
        : '<div class="empty" style="padding:10px">Free day — rest or catch up 🎉</div>') +
      '</div>';
  }).join("");
  const todayItems = days[0].items;
  $("#todaySub").textContent = todayItems.length
    ? todayItems.length + " study block" + (todayItems.length>1?"s":"") + " planned for today."
    : "Free day. Nothing urgent on the calendar.";
  $("#todayPlan").innerHTML = todayItems.length
    ? todayItems.map(it => '<div class="item"><span class="dot" style="width:9px;height:9px;border-radius:99px;background:' +
        (it.urgent?"#ff6b8a":"#7c6cff") + '"></span><span class="t">' + esc(it.subject) +
        '<div class="m">' + esc(it.title) + ' · ' + it.minutes + ' min</div></span>' +
        (it.left<=1 ? '<span class="pill hot">' + (it.left<=0?"today":it.left+" day") + '</span>' : '<span class="pill soon">' + it.left + ' days</span>') +
        '<button class="btn sm" data-start="' + esc(it.subject) + '" data-min="' + it.minutes + '">▶</button></div>').join("")
    : '<div class="empty">Nothing planned. Add a test to generate a plan.</div>';
  $$("[data-start]").forEach(b => b.addEventListener("click", () => {
    const subj = b.getAttribute("data-start"), mins = parseInt(b.getAttribute("data-min"),10);
    setTimer(mins, subj); go("dashboard");
    toast("Timer set: " + esc(subj) + " · " + mins + " min");
  }));
}
function renderAssessments(){
  const host = $("#asList");
  if(!S.assessments.length){ host.innerHTML = '<div class="empty">No tests tracked yet. Try: “Math test” / Friday.</div>'; return; }
  host.innerHTML = S.assessments.slice().sort((a,b)=> parseDay(a.date)-parseDay(b.date)).map(a => {
    const d = daysUntil(a.date);
    const cls = d <= 1 ? "hot" : d <= 3 ? "soon" : "calm";
    const keep = d < 0 ? "past" : d === 0 ? "TODAY" : d === 1 ? "tomorrow" : d + " days";
    return '<div class="item" style="' + (d<0?"opacity:.45":"") + '"><span class="t">' + esc(a.title) +
      '<div class="m">' + esc(a.subject) + ' · due ' + esc(a.date) + '</div></span>' +
      '<span class="pill ' + cls + '">' + keep + '</span>' +
      '<button class="btn sm danger" data-del-as="' + a.id + '">✕</button></div>';
  }).join("");
  $$("[data-del-as]").forEach(b => b.addEventListener("click", () => {
    S.assessments = S.assessments.filter(x => x.id !== b.getAttribute("data-del-as"));
    save(); renderAssessments(); renderPlan(); checkBadges();
  }));
}
function renderTasks(){
  const host = $("#taskList");
  if(!S.tasks.length){ host.innerHTML = '<div class="empty">No homework yet. Add one above.</div>'; return; }
  const sorted = S.tasks.slice().sort((a,b) => (a.done?1:0)-(b.done?1:0) || String(a.due||"zzz").localeCompare(String(b.due||"zzz")));
  host.innerHTML = sorted.map(t => {
    const d = t.due ? daysUntil(t.due) : null;
    const late = d !== null && d < 0 && !t.done;
    return '<div class="item ' + (t.done?"done":"") + '"><button class="check ' + (t.done?"on":"") + '" data-toggle="' + t.id + '">✓</button>' +
      '<span class="t">' + esc(t.title) + '<div class="m">' + esc(t.subject || "General") +
      (t.due ? " · due " + t.due + (late ? " ⚠ overdue" : d === 0 ? " · today" : "") : "") + '</div></span>' +
      '<button class="btn sm danger" data-del-task="' + t.id + '">✕</button></div>';
  }).join("");
  $$("[data-toggle]").forEach(b => b.addEventListener("click", () => {
    const t = S.tasks.find(x => x.id === b.getAttribute("data-toggle"));
    if(!t) return;
    t.done = !t.done;
    if(t.done) addXP(15, "task done"); 
    save(); renderTasks(); renderHUD(); checkBadges();
  }));
  $$("[data-del-task]").forEach(b => b.addEventListener("click", () => {
    S.tasks = S.tasks.filter(x => x.id !== b.getAttribute("data-del-task"));
    save(); renderTasks();
  }));
}
function renderNotes(){
  const host = $("#noteList");
  if(!S.notes.length){ host.innerHTML = '<div class="empty">No notes yet.</div>'; return; }
  host.innerHTML = S.notes.slice(0,6).map(n =>
    '<div class="note-note"><div class="spread"><small style="color:var(--dim)">' + new Date(n.at).toLocaleDateString() + '</small>' +
    '<span><button class="btn sm" data-usenote="' + n.id + '">🤖 to AI</button> <button class="btn sm danger" data-delnote="' + n.id + '">✕</button></span></div>' +
    '<div style="margin-top:5px">' + esc(n.text.slice(0,240)) + (n.text.length>240?"…":"") + '</div></div>').join("");
  $$("[data-delnote]").forEach(b => b.addEventListener("click", () => {
    S.notes = S.notes.filter(x => x.id !== b.getAttribute("data-delnote")); save(); renderNotes();
  }));
  $$("[data-usenote]").forEach(b => b.addEventListener("click", () => {
    const n = S.notes.find(x => x.id === b.getAttribute("data-usenote"));
    if(!n) return;
    $("#quizSrc").value = n.text; $("#fcSrc").value = n.text; $("#exSrc").value = n.text;
    go("ai"); showTool("quiz"); toast("Note loaded into the AI tools.");
  }));
}
function renderHeat(){
  const m = minutesByDay();
  const host = $("#heat");
  let html = "";
  for(let i = 13; i >= 0; i--){
    const d = dayStr(addDays(new Date(), -i));
    const mins = m[d] || 0;
    const lvl = mins >= 30 ? "l3" : mins >= 15 ? "l2" : mins >= 1 ? "l1" : "";
    html += '<i class="' + lvl + (i===0?" today":"") + '" title="' + d + ' · ' + mins + ' min">' + parseDay(d).getDate() + '</i>';
  }
  host.innerHTML = html;
  const st = streakInfo();
  $("#stStreak").textContent = st.current;
  $("#stBest").textContent = st.best;
  $("#stMin").textContent = m[today()] || 0;
}
function renderStats(){
  $("#pQ").textContent = S.questionsDone;
  $("#pAcc").textContent = S.questionsDone ? Math.round(S.correct/Math.max(1,S.questionsDone)*100) + "%" : "—";
  $("#pMin").textContent = totalMinutes();
  const by = {};
  S.sessions.forEach(s => { if(s.subject) by[s.subject] = (by[s.subject]||0)+s.minutes; });
  const rows = Object.keys(by).sort((a,b)=>by[b]-by[a]).slice(0,6);
  const max = Math.max(1, ...rows.map(r=>by[r]));
  const html = rows.length ? rows.map(r =>
    '<div class="bar"><span class="nm">' + esc(r) + '</span><span class="tr"><i style="width:' + Math.round(by[r]/max*100) + '%"></i></span><span class="vl">' + by[r] + 'm</span></div>').join("")
    : '<div class="empty">No study time logged yet.</div>';
  $("#subjectBars").innerHTML = html;
  const b2 = $("#bars2"); if(b2) b2.innerHTML = html;
}
function renderProgress(){
  const lv = levelOf(S.xp), st = streakInfo();
  $("#pgLevel").textContent = lv;
  $("#pgLevelSub").textContent = (S.xp % XP_PER_LEVEL) + " / " + XP_PER_LEVEL + " XP to next";
  $("#pgBar").style.width = Math.round(levelProg(S.xp)*100) + "%";
  $("#pgXp").textContent = S.xp.toLocaleString();
  $("#pgStreak").textContent = st.current;
  $("#pgBest").textContent = st.best;
  $("#pgQ").textContent = S.questionsDone;
  $("#pgAcc").textContent = S.questionsDone ? Math.round(S.correct/Math.max(1,S.questionsDone)*100) + "%" : "—";
  $("#badgeGrid").innerHTML = BADGES.map(b => {
    const on = S.badges.indexOf(b.id) !== -1;
    return '<div class="badge ' + (on?"on":"") + '"><span class="bi">' + b.icon + '</span><b>' + esc(b.name) +
      '</b><small>' + esc(b.desc) + '</small></div>';
  }).join("");
}
function renderDailyCard(){
  const box = $("#quizBox");
  if(!box) return;
  if(quiz && quiz.target === "#quizBox" && quiz.i < quiz.qs.length) return; // a quiz is in progress
  const pool_n = questionPool().length;
  box.innerHTML =
    '<div class="hstack" style="gap:8px;margin-bottom:11px">' +
      '<span class="pill">' + pool_n + ' questions ready</span>' +
      (S.wrongQueue.length ? '<span class="pill hot">' + S.wrongQueue.length + ' to retry</span>' : '') +
      '<span class="pill">5 per round</span>' +
    '</div>' +
    '<div class="hstack">' +
      '<button class="btn primary" id="dailyStart">▶ Start daily quiz</button>' +
      (S.wrongQueue.length ? '<button class="btn" id="dailyRetry">🔄 Practice missed</button>' : '') +
    '</div>' +
    '<div class="hint">Questions come from your saved notes plus the starter bank. Misses go to Practice Again.</div>';
  const b = $("#dailyStart"); if(b) b.addEventListener("click", startDaily);
  const r = $("#dailyRetry"); if(r) r.addEventListener("click", startAgain);
}
function renderAgain(){
  const host = $("#againBox");
  if(!S.wrongQueue.length){ host.innerHTML = '<div class="empty">Nothing to retry yet — take a quiz first.</div>'; return; }
  host.innerHTML = '<div class="spread" style="margin-bottom:11px">' +
    '<span class="sub" style="margin:0">' + S.wrongQueue.length + ' missed question(s) queued.</span>' +
    '<span><button class="btn primary sm" id="againStart">▶ Start practice</button>' +
    '<button class="btn sm danger" id="againClear" style="margin-left:8px">🧹 Clear</button></span></div>' +
    S.wrongQueue.slice(-8).reverse().map(w => '<div class="item" style="display:block"><div style="font-size:13.5px;font-weight:600">' + esc(w.q) + '</div>' +
      '<div class="m" style="margin-top:4px">Answer: <b style="color:var(--ok)">' + esc(w.a) + '</b></div></div>').join("");
  const s = $("#againStart"); if(s) s.addEventListener("click", startAgain);
  const c = $("#againClear"); if(c) c.addEventListener("click", () => {
    S.wrongQueue = []; save(); renderAgain(); renderHUD(); toast("Queue cleared.");
  });
}
function renderAll(){
  renderHUD(); renderGreeting(); renderSubjectSelect(); renderTasks(); renderNotes();
  renderAssessments(); renderPlan(); renderHeat(); renderStats(); renderProgress(); renderAgain(); renderDailyCard();
}

/* ============================ timer ============================ */
let timer = { left: 25*60, total: 25*60, running:false, handle:null, subject:"" };
function setTimer(minutes, subject){
  timer.total = minutes*60; timer.left = minutes*60; timer.running = false;
  if(timer.handle) clearInterval(timer.handle);
  if(subject){ const sel = $("#timerSubject"); if(subjectList().indexOf(subject) === -1){ const o=document.createElement("option"); o.textContent=subject; sel.appendChild(o); } sel.value = subject; }
  drawTimer();
}
function drawTimer(){
  const m = Math.floor(timer.left/60), s = timer.left%60;
  $("#clock").textContent = String(m).padStart(2,"0") + ":" + String(s).padStart(2,"0");
  $("#timerLabel").textContent = timer.running ? "focusing on " + (timer.subject || "study") : "ready";
  const C = 2*Math.PI*82;
  $("#ringFg").setAttribute("stroke-dashoffset", String(C * (timer.left/timer.total)));
  $("#timerToggle").textContent = timer.running ? "⏸ Pause" : "▶ Start";
}
function tick(){
  timer.left--;
  const minsStudied = (timer.total - timer.left);
  if(minsStudied > 0 && minsStudied % 60 === 0) { /* each full minute */ }
  if(timer.left <= 0){
    clearInterval(timer.handle); timer.running = false;
    logSession(Math.round(timer.total/60));
    setTimer(Math.round(timer.total/60), null);
    toast("⏰ Session complete! Nice work.", 4000);
    return;
  }
  drawTimer();
}
function logSession(minutes){
  if(minutes < 1) return;
  const subj = $("#timerSubject").value || "General";
  S.sessions.push({ date: today(), minutes, subject: subj, at: Date.now() });
  save();
  addXP(minutes*2, minutes + " min of " + subj);
  checkBadges();
  renderHeat(); renderStats(); renderProgress(); renderGreeting(); renderSubjectSelect(); renderPlan();
}
$("#timerToggle").addEventListener("click", () => {
  if(timer.running){
    timer.running = false; clearInterval(timer.handle);
    const done = Math.round((timer.total - timer.left)/60);
    if(done >= 1) logSession(done);
    timer.left = timer.total; drawTimer();
  } else {
    timer.running = true;
    timer.subject = $("#timerSubject").value;
    timer.handle = setInterval(tick, 1000);
    drawTimer();
  }
});
$("#timerStop").addEventListener("click", () => {
  if(timer.running){ clearInterval(timer.handle); timer.running = false; }
  const done = Math.round((timer.total - timer.left)/60);
  if(done >= 1) logSession(done);
  else toast("Study at least a minute to log a session.");
  timer.left = timer.total; drawTimer();
});
$$("[data-min]").forEach(b => b.addEventListener("click", () => setTimer(parseInt(b.getAttribute("data-min"),10), null)));

/* ============================ navigation ============================ */
function go(name){
  $$(".view").forEach(v => v.classList.toggle("active", v.id === "view-" + name));
  $$("[data-nav]").forEach(b => b.classList.toggle("active", b.getAttribute("data-nav") === name));
  try{ window.scrollTo({top:0, behavior:"smooth"}); }catch(e){}
}
$$("[data-nav]").forEach(b => b.addEventListener("click", () => go(b.getAttribute("data-nav"))));
$$("[data-goto]").forEach(b => b.addEventListener("click", () => go(b.getAttribute("data-goto"))));
function showTool(name){
  ["snap","quiz","cards","explain","again"].forEach(t => { $("#tool-" + t).style.display = (t === name) ? "" : "none"; });
}
$$("[data-tool]").forEach(b => b.addEventListener("click", () => showTool(b.getAttribute("data-tool"))));

/* ============================ AI tools wiring ============================ */
/* snap */
$("#snapFile").addEventListener("change", e => {
  const f = e.target.files && e.target.files[0];
  if(!f) return;
  const url = URL.createObjectURL(f);
  const img = $("#snapPreview"); img.src = url; img.style.display = "block";
  toast("Photo attached. Now type or paste the question text.");
});
$("#snapSolve").addEventListener("click", () => {
  const q = $("#snapText").value.trim();
  if(!q){ toast("Type or paste the question first."); return; }
  const r = solveProblem(q);
  $("#snapOut").innerHTML =
    '<div class="spread" style="margin-bottom:10px"><span class="pill">' + esc(r.title) + '</span>' +
    (r.fact ? '<span class="pill calm">' + esc(r.fact) + '</span>' : '<span class="pill">method</span>') + '</div>' +
    '<ol class="steps">' + r.steps.map(s => '<li><b>' + esc(s.n) + '.</b> ' + s.txt + '</li>').join("") + '</ol>' +
    '<div class="hint">Offline engine — it solves arithmetic, percentages and linear equations exactly, and gives a structured method for everything else.</div>';
  addXP(5, "homework help");
});

/* quiz maker */
$("#makeQuiz").addEventListener("click", () => {
  const src = $("#quizSrc").value.trim();
  if(src.split(/\s+/).length < 12){ toast("Add a bit more text (6+ sentences works best)."); return; }
  S.savedSource = src; save();
  const n = parseInt($("#quizN").value,10), style = $("#quizStyle").value;
  const qs = makeQuestions(src, n, style);
  if(!qs.length){ toast("Couldn't find question-worthy sentences — try clearer notes."); return; }
  pool = qs;
  $("#quizPreview").innerHTML = qs.map((q,i) =>
    '<div class="item" style="display:block"><div style="font-weight:650;font-size:13.5px">' + (i+1) + '. ' + esc(q.q) + '</div>' +
    '<div class="m" style="margin-top:5px">✔ ' + esc(q.a) + '</div></div>').join("");
  toast("⚡ " + qs.length + " questions generated");
  checkBadges();
});
$("#startGenQuiz").addEventListener("click", () => {
  const src = $("#quizSrc").value.trim();
  if(!pool.length && src){ pool = makeQuestions(src, 8, "mixed"); }
  if(!pool.length){ startDaily(); return; }
  showTool("quiz"); startQuiz(shuffle(pool).slice(0, Math.min(8, pool.length)), "gen");
});
$("#saveSrc").addEventListener("click", () => {
  const src = $("#quizSrc").value.trim();
  if(!src){ toast("Nothing to save."); return; }
  S.savedSource = src; save(); toast("💾 Notes saved — used for the daily quiz.");
});
/* flashcards */
$("#makeCards").addEventListener("click", () => {
  const src = $("#fcSrc").value.trim();
  if(src.split(/\s+/).length < 10){ toast("Add more note text first."); return; }
  const sents = sentencesOf(src).slice(0,24);
  const cards = sents.map(s => {
    const d = defPattern(s);
    if(d) return { front:"What is " + d.term + "?", back:d.def, sentence:s };
    const ws = s.split(" ");
    let idx = -1, best = 0;
    ws.forEach((w,i)=>{ const c=w.replace(/[^A-Za-z0-9'-]/g,""); if(c.length>best && c.length>=4){best=c.length;idx=i;} });
    const answer = idx>=0 ? ws[idx].replace(/[^A-Za-z0-9'-]/g,"") : "";
    const blanked = idx>=0 ? ws.map((w,i)=> i===idx ? "________" : w).join(" ") : s;
    return { front: blanked, back: answer || s, sentence:s, blankIdx:idx };
  }).filter(c => c.back);
  S.cards = cards; save();
  renderCards(); checkBadges(); toast("🃏 " + cards.length + " cards created");
});
function renderCards(){
  const host = $("#fcDeck");
  $("#fcCount").textContent = S.cards.length;
  if(!S.cards.length){ host.innerHTML = '<div class="empty">No cards yet.</div>'; return; }
  host.innerHTML = S.cards.map((c,i) =>
    '<div class="fc" data-fc="' + i + '"><div class="in">' +
    '<div class="f"><small>Question</small><b>' + esc(c.front) + '</b><small style="color:var(--dim)">tap to flip</small></div>' +
    '<div class="b"><small>Answer</small><b>' + esc(c.back) + '</b></div></div></div>').join("");
  $$("[data-fc]").forEach(el => el.addEventListener("click", () => el.classList.toggle("flip")));
}
$("#saveDeck").addEventListener("click", () => {
  if(!S.cards.length){ toast("Create cards first."); return; }
  S.decks.push({ id:uid(), at:Date.now(), n:S.cards.length }); save();
  toast("💾 Deck saved (" + S.cards.length + " cards)");
});
/* explain */
function runExplain(src, level){
  if(!src || src.split(/\s+/).length < 4){ toast("Paste something to explain."); return; }
  const simple = simplify(src, level);
  if(!simple || !simple.length){ toast("Couldn't simplify that text."); return; }
  const terms = keyTerms(src).slice(0,8);
  const an = analogiesFor(src);
  $("#exOut").innerHTML =
    '<div class="sub" style="margin-bottom:9px">' + (level === "eli5" ? "Like you're 5:" : "In plain English:") + '</div>' +
    '<div class="list">' + simple.slice(0,9).map(s => '<div class="item" style="display:block;font-size:14px">' + esc(s) + '</div>').join("") + '</div>' +
    '<div class="sub" style="margin:14px 0 7px">Key words to remember</div>' +
    '<div class="kv">' + terms.map(t => '<span>' + esc(t) + '</span>').join("") + '</div>' +
    (an.length ? '<div class="fb ok" style="margin-top:14px">' + an.join("<br>") + '</div>' : '') +
    '<div class="hint">Offline rewriter: breaks long sentences, swaps hard words for easy ones, and flags the key vocabulary.</div>';
  addXP(5, "explain it");
}
$("#explainBtn").addEventListener("click", () => runExplain($("#exSrc").value.trim(), $("#exLevel").value));
$("#exFromNote").addEventListener("click", () => {
  if(!S.notes.length){ toast("No notes saved yet."); return; }
  $("#exSrc").value = S.notes[0].text; toast("Loaded your latest note.");
});

/* ============================ tasks / notes / assessments ============================ */
$("#addTask").addEventListener("click", () => {
  const title = $("#taskTitle").value.trim();
  if(!title){ toast("Give the task a name."); return; }
  S.tasks.push({ id:uid(), title, subject:$("#taskSubject").value.trim() || "General", due:$("#taskDue").value || "", done:false });
  $("#taskTitle").value = ""; $("#taskSubject").value = ""; $("#taskDue").value = "";
  save(); renderTasks(); renderSubjectSelect();
});
$("#taskTitle").addEventListener("keydown", e => { if(e.key === "Enter") $("#addTask").click(); });
$("#addNote").addEventListener("click", () => {
  const t = $("#noteInput").value.trim();
  if(!t){ toast("Note is empty."); return; }
  S.notes.unshift({ id:uid(), text:t, at:Date.now() });
  $("#noteInput").value = ""; save(); renderNotes(); toast("📝 Note saved");
});
$("#addAs").addEventListener("click", () => {
  const title = $("#asTitle").value.trim(), date = $("#asDate").value;
  if(!title || !date){ toast("Add a name and a date."); return; }
  S.assessments.push({ id:uid(), title, subject:$("#asSubject").value.trim() || "General", date, weight:$("#asWeight").value });
  $("#asTitle").value = ""; $("#asSubject").value = ""; $("#asDate").value = "";
  save(); renderAssessments(); renderPlan(); renderSubjectSelect(); checkBadges();
  toast("🗺️ Added — plan updated");
});
$("#asTitle").addEventListener("keydown", e => { if(e.key === "Enter") $("#addAs").click(); });

/* ============================ reset ============================ */
$("#resetAll").addEventListener("click", () => {
  if(!confirm("Erase all StudyQuest data in this browser?")) return;
  S = Object.assign({}, DEFAULTS); save(); renderAll(); renderCards();
  toast("Everything reset.");
});

/* ============================ boot ============================ */
(function seed(){
  if(!store.get(KEY)){
    S.assessments = [
      { id:uid(), title:"Math test", subject:"Math", date:dayStr(addDays(new Date(),3)), weight:"1.6" },
      { id:uid(), title:"Science assignment", subject:"Science", date:dayStr(addDays(new Date(),5)), weight:"1" },
      { id:uid(), title:"English quiz", subject:"English", date:dayStr(addDays(new Date(),6)), weight:"0.7" }
    ];
    S.tasks = [
      { id:uid(), title:"Worksheet page 42", subject:"Math", due:dayStr(addDays(new Date(),1)), done:false },
      { id:uid(), title:"Read chapter 4 notes", subject:"Science", due:dayStr(addDays(new Date(),2)), done:false }
    ];
    S.notes = [{ id:uid(), text:"Photosynthesis is the process plants use to convert light energy into chemical energy. Chlorophyll absorbs red and blue light. The plant takes in carbon dioxide and water and produces glucose and oxygen.", at:Date.now() }];
    S.savedSource = S.notes[0].text;
    S.xp = 340;
    save();
  }
})();
pool = buildPool(8);
renderAll(); renderCards(); setTimer(25, null);
if(!S.assessments.length) showTool("");
showTool("snap");
})();
</script>
</body>
</html>
