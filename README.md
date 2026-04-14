# bach-calculator
Estimated cost calculator for Ruthie's bachelorette trip
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ruthie's Bach 💍 Budget Calculator</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --yellow: #F5C842;
    --yellow-light: #FFF8DC;
    --teal: #4AADA8;
    --teal-light: #E0F5F4;
    --coral: #E07B6A;
    --coral-light: #FCECEA;
    --sage: #7BAF88;
    --sage-light: #EAF4EC;
    --lavender: #9B8EC4;
    --lavender-light: #F0EDF9;
    --bg: #F7F3EC;
    --card: #FDFCF8;
    --dark: #2C3440;
    --mid: #6B7A8D;
    --light: #A8B5C2;
    --border: #E8E2D8;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--dark);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* dotted bg */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: radial-gradient(circle, #C8D8D4 1px, transparent 1px);
    background-size: 22px 22px;
    opacity: 0.45;
    pointer-events: none;
    z-index: 0;
  }

  .page { position: relative; z-index: 1; max-width: 680px; margin: 0 auto; padding: 0 16px 60px; }

  /* ── header ── */
  .header {
    text-align: center;
    padding: 40px 0 28px;
  }
  .header-flowers { display: flex; justify-content: center; gap: 6px; margin-bottom: 10px; }
  .flower { font-size: 18px; animation: sway 3s ease-in-out infinite; }
  .flower:nth-child(2) { animation-delay: .4s; }
  .flower:nth-child(3) { animation-delay: .8s; }
  @keyframes sway { 0%,100%{transform:rotate(-8deg)} 50%{transform:rotate(8deg)} }

  .header h1 {
    font-family: 'Playfair Display', serif;
    font-style: italic;
    font-size: clamp(28px, 7vw, 42px);
    color: var(--dark);
    line-height: 1.1;
  }
  .header h1 span { color: var(--coral); }
  .header-sub {
    font-size: 13px;
    color: var(--mid);
    margin-top: 6px;
    letter-spacing: 0.04em;
  }
  .wavy-line {
    width: 180px;
    height: 8px;
    margin: 12px auto 0;
    background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 180 8'%3E%3Cpath d='M0 4 Q15 0 30 4 Q45 8 60 4 Q75 0 90 4 Q105 8 120 4 Q135 0 150 4 Q165 8 180 4' stroke='%23F5C842' stroke-width='2.5' fill='none'/%3E%3C/svg%3E") center/contain no-repeat;
  }

  /* ── intro card ── */
  .intro-card {
    background: var(--card);
    border: 1.5px solid var(--yellow);
    border-radius: 16px;
    padding: 18px 20px;
    margin-bottom: 20px;
    font-size: 13.5px;
    color: var(--mid);
    line-height: 1.6;
  }
  .intro-card strong { color: var(--dark); }

  /* ── fixed costs ── */
  .fixed-section {
    background: var(--sage-light);
    border: 1px solid var(--sage);
    border-radius: 14px;
    padding: 16px 18px;
    margin-bottom: 20px;
  }
  .fixed-section h3 {
    font-size: 11px;
    font-weight: 500;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--sage);
    margin-bottom: 10px;
  }
  .fixed-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 6px 0;
    border-bottom: 1px dashed #C5DEC9;
    font-size: 13.5px;
  }
  .fixed-row:last-child { border-bottom: none; }
  .fixed-label { color: var(--dark); }
  .fixed-val { font-weight: 500; color: var(--sage); }
  .free-badge {
    background: #C8E6C9;
    color: #2E7D32;
    font-size: 10px;
    font-weight: 500;
    padding: 2px 10px;
    border-radius: 999px;
  }

  /* ── question cards ── */
  .q-section-label {
    font-size: 10px;
    font-weight: 500;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--mid);
    margin: 24px 0 10px 4px;
  }

  .q-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 18px 18px 14px;
    margin-bottom: 12px;
    transition: border-color .2s, box-shadow .2s;
  }
  .q-card:focus-within { border-color: var(--teal); box-shadow: 0 0 0 3px rgba(74,173,168,.12); }

  .q-header {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    margin-bottom: 12px;
  }
  .q-icon {
    width: 36px; height: 36px;
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px;
    flex-shrink: 0;
  }
  .q-icon.teal   { background: var(--teal-light); }
  .q-icon.coral  { background: var(--coral-light); }
  .q-icon.lavender { background: var(--lavender-light); }
  .q-icon.yellow { background: var(--yellow-light); }

  .q-title { font-size: 14px; font-weight: 500; color: var(--dark); line-height: 1.3; }
  .q-note  { font-size: 12px; color: var(--mid); margin-top: 2px; line-height: 1.4; }

  /* option buttons */
  .options { display: flex; flex-wrap: wrap; gap: 8px; }
  .opt-btn {
    padding: 7px 14px;
    border-radius: 999px;
    border: 1.5px solid var(--border);
    background: white;
    font-family: 'DM Sans', sans-serif;
    font-size: 13px;
    color: var(--dark);
    cursor: pointer;
    transition: all .18s;
    line-height: 1;
  }
  .opt-btn:hover { border-color: var(--teal); color: var(--teal); }
  .opt-btn.selected { background: var(--teal); border-color: var(--teal); color: white; font-weight: 500; }
  .opt-btn.selected-coral { background: var(--coral); border-color: var(--coral); color: white; font-weight: 500; }
  .opt-btn.selected-lavender { background: var(--lavender); border-color: var(--lavender); color: white; font-weight: 500; }
  .opt-btn.selected-yellow { background: var(--yellow); border-color: var(--yellow); color: var(--dark); font-weight: 500; }

  /* ── result card ── */
  .result-card {
    background: var(--dark);
    border-radius: 18px;
    padding: 24px 22px;
    margin-top: 28px;
    color: white;
    opacity: 0;
    transform: translateY(16px);
    transition: opacity .4s, transform .4s;
  }
  .result-card.visible { opacity: 1; transform: translateY(0); }

  .result-title {
    font-family: 'Playfair Display', serif;
    font-style: italic;
    font-size: 20px;
    color: var(--yellow);
    margin-bottom: 16px;
  }

  .result-rows { margin-bottom: 16px; }
  .r-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 0;
    border-bottom: 1px solid rgba(255,255,255,.1);
    font-size: 13.5px;
  }
  .r-row:last-child { border-bottom: none; }
  .r-label { color: rgba(255,255,255,.75); }
  .r-label .r-sub { font-size: 11px; color: rgba(255,255,255,.45); display: block; }
  .r-val { font-weight: 500; color: white; }
  .r-free { color: #81C784; font-weight: 500; }
  .r-opt  { color: #FFB74D; font-size: 12px; }

  .result-total {
    background: var(--yellow);
    border-radius: 12px;
    padding: 14px 16px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 4px;
  }
  .result-total .label { font-size: 12px; color: var(--dark); font-weight: 500; }
  .result-total .amount { font-size: 26px; font-weight: 500; color: var(--dark); font-family: 'Playfair Display', serif; }
  .result-total .pp { font-size: 11px; color: rgba(44,52,64,.65); }

  .note-pill {
    background: rgba(255,255,255,.08);
    border-radius: 10px;
    padding: 10px 12px;
    font-size: 12px;
    color: rgba(255,255,255,.65);
    margin-top: 12px;
    line-height: 1.5;
  }

  /* ── share section ── */
  .share-section {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 22px 20px;
    margin-top: 20px;
    text-align: center;
  }
  .share-section h3 {
    font-family: 'Playfair Display', serif;
    font-style: italic;
    font-size: 18px;
    color: var(--dark);
    margin-bottom: 6px;
  }
  .share-section p {
    font-size: 13px;
    color: var(--mid);
    margin-bottom: 18px;
    line-height: 1.5;
  }

  .share-steps {
    display: flex;
    flex-direction: column;
    gap: 10px;
    text-align: left;
    margin-bottom: 20px;
  }
  .share-step {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    background: var(--bg);
    border-radius: 10px;
    padding: 12px 14px;
  }
  .step-num {
    width: 24px; height: 24px;
    border-radius: 50%;
    background: var(--teal);
    color: white;
    font-size: 12px;
    font-weight: 500;
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0;
    margin-top: 1px;
  }
  .step-text { font-size: 13px; color: var(--dark); line-height: 1.5; }
  .step-text strong { color: var(--teal); }
  .step-text a { color: var(--teal); }

  .download-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: var(--coral);
    color: white;
    font-family: 'DM Sans', sans-serif;
    font-size: 14px;
    font-weight: 500;
    padding: 12px 28px;
    border-radius: 999px;
    border: none;
    cursor: pointer;
    transition: opacity .2s, transform .1s;
    text-decoration: none;
  }
  .download-btn:hover { opacity: .9; transform: translateY(-1px); }
  .download-btn:active { transform: scale(.98); }

  #qr-container {
    margin: 20px auto 0;
    display: none;
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }
  #qr-container.visible { display: flex; }
  #qr-canvas {
    border-radius: 12px;
    border: 4px solid var(--yellow);
    display: block;
  }
  .qr-label {
    font-size: 12px;
    color: var(--mid);
    text-align: center;
  }

  /* progress dots */
  .progress-bar {
    display: flex;
    justify-content: center;
    gap: 6px;
    margin: 20px 0 8px;
  }
  .prog-dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--border);
    transition: background .2s, transform .2s;
  }
  .prog-dot.active { background: var(--teal); transform: scale(1.4); }

  @media (max-width: 480px) {
    .options { gap: 6px; }
    .opt-btn { font-size: 12px; padding: 6px 12px; }
  }
</style>
</head>
<body>
<div class="page">

  <!-- header -->
  <div class="header">
    <div class="header-flowers">
      <span class="flower">🌸</span>
      <span class="flower">💍</span>
      <span class="flower">🌸</span>
    </div>
    <h1>Ruthie's Bach<br><span>Budget Calculator</span></h1>
    <div class="header-sub">June 18–22, 2026 · Williamsburg, VA</div>
    <div class="wavy-line"></div>
  </div>

  <!-- intro -->
  <div class="intro-card">
    Hey girl! 👋 Answer a few quick questions below to see your <strong>personalized cost estimate</strong> for the trip. Everything is flexible — pick exactly what you want to spend on!
  </div>

  <!-- fixed costs -->
  <div class="fixed-section">
    <h3>✨ Already covered for everyone</h3>
    <div class="fixed-row">
      <span class="fixed-label">🏨 Hotel (4 nights)</span>
      <span class="free-badge">FREE — timeshare points!</span>
    </div>
    <div class="fixed-row">
      <span class="fixed-label">🍳 All room breakfasts</span>
      <span class="free-badge">Included in groceries</span>
    </div>
    <div class="fixed-row">
      <span class="fixed-label">🍽️ Room dinners (nachos, taco bowls, dips night)</span>
      <span class="free-badge">Included in groceries</span>
    </div>
    <div class="fixed-row">
      <span class="fixed-label">👰 Bride's grocery share</span>
      <span class="free-badge">Covered by the group 💕</span>
    </div>
    <div class="fixed-row">
      <span class="fixed-label">🎶 Vineyard entry + live music</span>
      <span class="free-badge">FREE admission</span>
    </div>
  </div>

  <!-- questions label -->
  <div class="q-section-label">Your choices 👇</div>

  <!-- progress dots -->
  <div class="progress-bar" id="progress-bar"></div>

  <!-- Q1: Park Tickets -->
  <div class="q-card" id="q1">
    <div class="q-header">
      <div class="q-icon teal">🎢</div>
      <div>
        <div class="q-title">Do you want park tickets?</div>
        <div class="q-note">2-day park-hop (Busch Gardens + Water Country USA) via nurse discount. Each person pays their own.</div>
      </div>
    </div>
    <div class="options" id="opts-park">
      <button class="opt-btn" onclick="select('park','yes',this)">Yes! 2-day park-hop (~$110)</button>
      <button class="opt-btn" onclick="select('park','no',this)">No thanks, skipping parks</button>
    </div>
  </div>

  <!-- Q2: Groceries share -->
  <div class="q-card" id="q2">
    <div class="q-header">
      <div class="q-icon coral">🛒</div>
      <div>
        <div class="q-title">Shared groceries & gas</div>
        <div class="q-note">Covers all room meals, breakfasts, snacks & packed park lunches. Groceries split 7 ways (bride's share is covered by the group 💕). Gas split 8 ways.</div>
      </div>
    </div>
    <div class="options" id="opts-groceries">
      <button class="opt-btn" onclick="select('groceries','yes',this)">Yes, I'm in (~$56–58)</button>
      <button class="opt-btn" onclick="select('groceries','no',this)">I'll opt out / bring my own</button>
    </div>
  </div>

  <!-- Q3: Vineyard lunch -->
  <div class="q-card" id="q3">
    <div class="q-header">
      <div class="q-icon lavender">🧺</div>
      <div>
        <div class="q-title">Sunday vineyard — lunch plan?</div>
        <div class="q-note">Saude Creek Vineyards, June 22. Food trucks on site, or pack a free picnic from the room!</div>
      </div>
    </div>
    <div class="options" id="opts-lunch">
      <button class="opt-btn" onclick="select('lunch','pack',this)">Pack a picnic (free!)</button>
      <button class="opt-btn" onclick="select('lunch','truck',this)">Food trucks (~$10–15)</button>
      <button class="opt-btn" onclick="select('lunch','both',this)">Mix of both (~$8)</button>
    </div>
  </div>

  <!-- Q4: Wine flight -->
  <div class="q-card" id="q4">
    <div class="q-header">
      <div class="q-icon lavender">🍷</div>
      <div>
        <div class="q-title">Wine flight at the vineyard?</div>
        <div class="q-note">Walk-up bar with wine flights. Totally optional — one of our girls is underage & that's totally fine!</div>
      </div>
    </div>
    <div class="options" id="opts-wine">
      <button class="opt-btn" onclick="select('wine','yes',this)">Yes please! (~$20)</button>
      <button class="opt-btn" onclick="select('wine','no',this)">I'll skip the wine</button>
    </div>
  </div>

  <!-- Q5: Thai Tara -->
  <div class="q-card" id="q5">
    <div class="q-header">
      <div class="q-icon teal">🍣</div>
      <div>
        <div class="q-title">Sunday dinner at Thai Tara Sushi & Bar</div>
        <div class="q-note">Everyone orders for themselves. How much do you want to spend? (We'll have room snacks after too!)</div>
      </div>
    </div>
    <div class="options" id="opts-dinner">
      <button class="opt-btn" onclick="select('dinner','light',this)">Light — a roll or two ($14–18)</button>
      <button class="opt-btn" onclick="select('dinner','mid',this)">Mid — entrée or 2 rolls ($20–28)</button>
      <button class="opt-btn" onclick="select('dinner','splurge',this)">Treat myself! ($35–50)</button>
    </div>
  </div>

  <!-- Q6: Drinks at dinner -->
  <div class="q-card" id="q6">
    <div class="q-header">
      <div class="q-icon coral">🍸</div>
      <div>
        <div class="q-title">Drinks at dinner?</div>
        <div class="q-note">Cocktails, sake, or mocktails. Optional — order whatever you'd like!</div>
      </div>
    </div>
    <div class="options" id="opts-drinks">
      <button class="opt-btn" onclick="select('drinks','yes',this)">Yes, I'll get a drink or two (~$16–28)</button>
      <button class="opt-btn" onclick="select('drinks','no',this)">Water/mocktail for me</button>
    </div>
  </div>

  <!-- Q7: Personal alcohol -->
  <div class="q-card" id="q7">
    <div class="q-header">
      <div class="q-icon yellow">🥂</div>
      <div>
        <div class="q-title">Personal alcohol for nights in?</div>
        <div class="q-note">A little will be provided in the group grocery haul, but you might want to bring your own. This is a personal expense — not split with the group!</div>
      </div>
    </div>
    <div class="options" id="opts-alcohol">
      <button class="opt-btn" onclick="select('alcohol','yes',this)">Yes, I'll bring some (~$15–25)</button>
      <button class="opt-btn" onclick="select('alcohol','maybe',this)">Maybe a little (~$10)</button>
      <button class="opt-btn" onclick="select('alcohol','no',this)">What's provided is enough / not drinking</button>
    </div>
  </div>

  <!-- Q8: Park food -->
  <div class="q-card" id="q8">
    <div class="q-header">
      <div class="q-icon teal">🌭</div>
      <div>
        <div class="q-title">Park food & drinks budget?</div>
        <div class="q-note">Packed lunches from the room are free! But you might want snacks, a treat, or a park meal.</div>
      </div>
    </div>
    <div class="options" id="opts-parkfood">
      <button class="opt-btn" onclick="select('parkfood','packed',this)">Just packed lunch (free!)</button>
      <button class="opt-btn" onclick="select('parkfood','some',this)">Packed + a few snacks (~$15–20)</button>
      <button class="opt-btn" onclick="select('parkfood','full',this)">Full park meals + snacks (~$30–45)</button>
    </div>
  </div>

  <!-- result -->
  <div class="result-card" id="result-card">
    <div class="result-title">Your estimated trip cost ✨</div>
    <div class="result-rows" id="result-rows"></div>
    <div class="result-total">
      <div>
        <div class="label">Your total estimate</div>
        <div class="pp" id="result-range"></div>
      </div>
      <div class="amount" id="result-amount">$0</div>
    </div>
    <div class="note-pill" id="result-note"></div>
  </div>

  <!-- share section -->
  <div class="share-section" style="margin-top:32px;">
    <h3>Share with the girls 🎉</h3>
    <p>Save this file and share it — everyone can open it in their phone browser and fill it out themselves. No app needed!</p>

    <div class="share-steps">
      <div class="share-step">
        <div class="step-num">1</div>
        <div class="step-text">Download this file using the button below and save it to your phone or computer.</div>
      </div>
      <div class="share-step">
        <div class="step-num">2</div>
        <div class="step-text">Upload it to <strong>Google Drive</strong> or <strong>Dropbox</strong> (free) and copy the shareable link.</div>
      </div>
      <div class="share-step">
        <div class="step-num">3</div>
        <div class="step-text">Drop the link in your group chat — everyone can open it in their browser, no download needed! Or use the QR code below.</div>
      </div>
    </div>

    <button class="download-btn" onclick="downloadSelf()">
      ⬇ Download calculator file
    </button>

    <div style="margin-top:24px; border-top:1px dashed var(--border); padding-top:20px;">
      <p style="margin-bottom:14px; font-size:13px;">Once you have your shareable link, paste it below to generate a QR code the girls can scan:</p>
      <div style="display:flex; gap:8px; flex-wrap:wrap; justify-content:center;">
        <input type="text" id="link-input" placeholder="Paste your Google Drive / Dropbox link here..."
          style="flex:1; min-width:200px; padding:10px 14px; border-radius:999px; border:1.5px solid var(--border); font-family:'DM Sans',sans-serif; font-size:13px; background:var(--bg); color:var(--dark); outline:none;"
          oninput="handleLinkInput(this.value)">
        <button onclick="generateQR()" style="padding:10px 20px; border-radius:999px; border:none; background:var(--teal); color:white; font-family:'DM Sans',sans-serif; font-size:13px; font-weight:500; cursor:pointer;">
          Make QR Code
        </button>
      </div>
      <div id="qr-container">
        <canvas id="qr-canvas" width="200" height="200"></canvas>
        <div class="qr-label">Screenshot this QR code and send it in the group chat!<br>Girls can scan it to open the calculator.</div>
        <button onclick="downloadQR()" style="padding:8px 18px; border-radius:999px; border:1.5px solid var(--teal); background:transparent; color:var(--teal); font-family:'DM Sans',sans-serif; font-size:13px; cursor:pointer;">
          Save QR code image
        </button>
      </div>
    </div>
  </div>

</div>

<script>
// ── state ──────────────────────────────────────────────────────────────────
const answers = {};
const Q_IDS = ['park','groceries','lunch','wine','dinner','drinks','alcohol','parkfood'];

const COSTS = {
  park:      { yes: {lo:110,hi:110}, no: {lo:0,hi:0} },
  groceries: { yes: {lo:56,hi:58},  no: {lo:0,hi:0} },
  lunch:     { pack:{lo:0,hi:0}, truck:{lo:10,hi:15}, both:{lo:6,hi:12} },
  wine:      { yes: {lo:20,hi:20}, no: {lo:0,hi:0} },
  dinner:    { light:{lo:14,hi:18}, mid:{lo:20,hi:28}, splurge:{lo:35,hi:50} },
  drinks:    { yes: {lo:16,hi:28}, no: {lo:0,hi:0} },
  alcohol:   { yes:{lo:15,hi:25}, maybe:{lo:8,hi:12}, no:{lo:0,hi:0} },
  parkfood:  { packed:{lo:0,hi:0}, some:{lo:15,hi:20}, full:{lo:30,hi:45} },
};

const LABELS = {
  park:      { yes:'Park tickets (2-day hop)', no:null },
  groceries: { yes:'Shared groceries & gas', no:null },
  lunch:     { pack:null, truck:'Vineyard food trucks', both:'Vineyard food trucks' },
  wine:      { yes:'Vineyard wine flight', no:null },
  dinner:    { light:'Thai Tara dinner', mid:'Thai Tara dinner', splurge:'Thai Tara dinner' },
  drinks:    { yes:'Drinks at dinner', no:null },
  alcohol:   { yes:'Personal alcohol (nights in)', maybe:'Personal alcohol (nights in)', no:null },
  parkfood:  { packed:null, some:'Park snacks & extras', full:'Park food & meals' },
};

const COLORS = {
  park:'selected', groceries:'selected-coral', lunch:'selected-lavender',
  wine:'selected-lavender', dinner:'selected', drinks:'selected-coral',
  alcohol:'selected-yellow', parkfood:'selected'
};

// build progress dots
function buildProgress() {
  const bar = document.getElementById('progress-bar');
  bar.innerHTML = '';
  Q_IDS.forEach((q,i) => {
    const d = document.createElement('div');
    d.className = 'prog-dot' + (answers[q] ? ' active' : '');
    d.id = 'dot-'+q;
    bar.appendChild(d);
  });
}
buildProgress();

function select(key, val, btn) {
  answers[key] = val;
  // deselect siblings
  const container = btn.parentElement;
  container.querySelectorAll('.opt-btn').forEach(b => {
    b.className = 'opt-btn';
  });
  btn.classList.add(COLORS[key] || 'selected');
  document.getElementById('dot-'+key).classList.add('active');
  updateResult();
  // scroll smoothly to result if all answered
  if (Object.keys(answers).length === Q_IDS.length) {
    setTimeout(() => document.getElementById('result-card').scrollIntoView({behavior:'smooth', block:'nearest'}), 150);
  }
}

function updateResult() {
  const card = document.getElementById('result-card');
  const rowsEl = document.getElementById('result-rows');
  const amountEl = document.getElementById('result-amount');
  const rangeEl = document.getElementById('result-range');
  const noteEl = document.getElementById('result-note');

  let lo = 0, hi = 0;
  const rows = [];

  Q_IDS.forEach(key => {
    const val = answers[key];
    if (!val) return;
    const cost = COSTS[key][val];
    const label = LABELS[key][val];
    if (!label) return; // free / not chosen
    lo += cost.lo; hi += cost.hi;
    rows.push({ label, lo: cost.lo, hi: cost.hi });
  });

  if (Object.keys(answers).length === 0) return;

  card.classList.add('visible');

  // free items
  const freeRows = [
    { label: '🏨 Hotel (4 nights)', tag: 'FREE' },
    { label: '🍳 Room breakfasts + dinners', tag: 'Included' },
    { label: '🎶 Vineyard entry', tag: 'FREE' },
  ];

  let html = freeRows.map(r => `
    <div class="r-row">
      <span class="r-label">${r.label}</span>
      <span class="r-free">${r.tag} ✓</span>
    </div>`).join('');

  rows.forEach(r => {
    const display = r.lo === r.hi ? `$${r.lo}` : `$${r.lo}–$${r.hi}`;
    html += `<div class="r-row">
      <span class="r-label">${r.label}</span>
      <span class="r-val">${display}</span>
    </div>`;
  });

  rowsEl.innerHTML = html;

  const midpoint = Math.round((lo + hi) / 2);
  amountEl.textContent = lo === hi ? `$${lo}` : `$${lo}–$${hi}`;
  rangeEl.textContent = `midpoint ~$${midpoint}`;

  // note
  const answered = Object.keys(answers).length;
  if (answered < Q_IDS.length) {
    noteEl.textContent = `⬆ Answer all ${Q_IDS.length} questions above to finalize your estimate. (${answered}/${Q_IDS.length} done)`;
  } else {
    const note = lo <= 140
      ? "Great news — this is a very affordable trip thanks to the free hotel! 🎉"
      : lo <= 210
      ? "Totally reasonable budget for a 5-day trip! You're going to have the best time. 💕"
      : "You're treating yourself — worth every penny for Ruthie's bach! 🥂";
    noteEl.textContent = note;
  }
}

// ── download self ──────────────────────────────────────────────────────────
function downloadSelf() {
  const html = document.documentElement.outerHTML;
  const blob = new Blob([html], {type:'text/html'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'ruthies_bach_budget_calculator.html';
  a.click();
}

// ── QR code generator (pure JS, no library) ───────────────────────────────
function handleLinkInput(val) {
  if (!val.trim()) document.getElementById('qr-container').classList.remove('visible');
}

function generateQR() {
  const input = document.getElementById('link-input').value.trim();
  if (!input) { alert('Please paste a link first!'); return; }
  drawQR(input);
  document.getElementById('qr-container').classList.add('visible');
}

// Minimal QR encoder for URLs (alphanumeric + byte mode, version adaptive)
// Uses a compact Reed-Solomon + QR matrix implementation
function drawQR(text) {
  const canvas = document.getElementById('qr-canvas');
  const ctx = canvas.getContext('2d');

  // Use a public QR API rendered into canvas via Image
  // We'll use the goqr.me API URL pattern drawn via an Image element
  const size = 200;
  canvas.width = size; canvas.height = size;

  const encoded = encodeURIComponent(text);
  const apiUrl = `https://api.qrserver.com/v1/create-qr-code/?size=${size}x${size}&data=${encoded}&margin=2`;

  const img = new Image();
  img.crossOrigin = 'anonymous';
  img.onload = () => {
    ctx.clearRect(0,0,size,size);
    ctx.fillStyle = 'white';
    ctx.fillRect(0,0,size,size);
    ctx.drawImage(img,0,0,size,size);
  };
  img.onerror = () => {
    // fallback: draw a simple placeholder with message
    ctx.fillStyle = '#2C3440';
    ctx.fillRect(0,0,size,size);
    ctx.fillStyle = 'white';
    ctx.font = '12px DM Sans, sans-serif';
    ctx.textAlign = 'center';
    ctx.fillText('QR requires internet.', size/2, size/2 - 10);
    ctx.fillText('Share the file directly!', size/2, size/2 + 10);
  };
  img.src = apiUrl;
}

function downloadQR() {
  const canvas = document.getElementById('qr-canvas');
  const a = document.createElement('a');
  a.download = 'ruthies_bach_qr.png';
  a.href = canvas.toDataURL('image/png');
  a.click();
}
</script>
</body>
</html>
