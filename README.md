<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Business English — Marketing Project Manager</title>
<style>
  :root {
    --page-bg: #ece5d6;
    --card-bg: #faf6ee;
    --ink: #2b2620;
    --muted: #7a7266;
    --accent: #1f4e5f;
    --red: #c0453c;
    --track: #e2d9c6;
    --border-soft: #e2d9c6;
    --border-btn: #ddd2ba;
    --hover-bg: #f4efe2;
    --green-bg: #e6f4e8;
    --green-text: #256a34;
    --green-border: #4c9a5c;
    --red-bg: #fbe9e7;
    --red-text: #a13328;
    --hint-bg: #fff6e0;
    --hint-text: #8a6d1f;
    --hint-border: #e0c869;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: Georgia, "Times New Roman", serif;
    background: var(--page-bg);
    color: var(--ink);
    min-height: 100vh;
    padding: 24px 14px 60px;
  }

  .paper {
    max-width: 760px;
    margin: 0 auto;
    background: var(--card-bg);
    border-left: 5px solid var(--red);
    border-radius: 4px;
    box-shadow: 0 6px 24px rgba(60,50,35,0.18);
    padding: 36px 40px 50px 34px;
  }

  header h1 { font-size: 26px; color: var(--ink); }
  header .subtitle {
    color: var(--muted);
    font-style: italic;
    margin-top: 6px;
    font-size: 15px;
  }

  .progress-track {
    height: 10px;
    background: var(--track);
    border-radius: 6px;
    overflow: hidden;
    margin-top: 22px;
  }
  .progress-fill {
    height: 100%;
    width: 0%;
    background: var(--red);
    border-radius: 6px;
    transition: width 0.35s ease;
  }
  .progress-label {
    font-family: Arial, sans-serif;
    font-size: 11px;
    color: var(--muted);
    margin-top: 5px;
  }

  .step-nav {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin-top: 14px;
    margin-bottom: 8px;
  }
  .step-dot {
    font-family: Arial, sans-serif;
    font-size: 12px;
    width: 32px;
    height: 32px;
    border-radius: 50%;
    border: 1px solid var(--border-btn);
    background: #fff;
    color: var(--muted);
    cursor: pointer;
    transition: all 0.15s ease;
  }
  .step-dot:hover { background: var(--hover-bg); }
  .step-dot.visited {
    border: 1px solid var(--accent);
    color: var(--accent);
    background: #fff;
  }
  .step-dot.current {
    background: var(--accent);
    border-color: var(--accent);
    color: #fff;
    font-weight: bold;
  }

  .stage { display: none; }
  .stage.active { display: block; animation: fadeSlide 0.35s ease; }
  @keyframes fadeSlide {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .stage-tag {
    display: inline-block;
    font-family: Arial, sans-serif;
    font-size: 0.7rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    background: var(--accent);
    color: #fff;
    padding: 4px 12px;
    border-radius: 12px;
    margin-bottom: 14px;
  }
  .stage h2 { font-size: 22px; margin-bottom: 6px; }
  .stage-intro {
    color: var(--muted);
    font-style: italic;
    margin-bottom: 22px;
    font-size: 15px;
  }

  .vocab-card {
    background: #fff;
    border: 1px solid var(--border-soft);
    border-left: 4px solid var(--accent);
    border-radius: 4px;
    padding: 16px 18px;
    margin-bottom: 14px;
  }
  .vocab-card .term {
    font-weight: bold;
    color: var(--accent);
    font-size: 17px;
  }
  .vocab-card .definition { margin-top: 6px; font-size: 15px; }
  .vocab-card .example {
    margin-top: 10px;
    background: #f4efe2;
    border-radius: 4px;
    padding: 8px 12px;
    font-style: italic;
    font-size: 14px;
    color: var(--ink);
  }

  .item {
    padding: 18px 0;
    border-bottom: 1px dashed var(--border-btn);
  }
  .item:last-child { border-bottom: none; }
  .context-line {
    font-size: 13px;
    color: var(--muted);
    font-style: italic;
    margin-bottom: 6px;
  }
  .prompt { margin-bottom: 12px; font-size: 16px; }

  .options { display: flex; flex-direction: column; gap: 8px; }
  .option-btn {
    font-family: Arial, sans-serif;
    font-size: 14px;
    text-align: left;
    padding: 10px 14px;
    background: #fff;
    border: 1px solid var(--border-btn);
    border-radius: 6px;
    cursor: pointer;
    transition: background 0.15s ease;
  }
  .option-btn:hover:not(:disabled) { background: var(--hover-bg); }
  .option-btn:disabled { cursor: default; opacity: 0.85; }
  .option-btn.correct {
    background: var(--green-bg);
    color: var(--green-text);
    border-color: var(--green-border);
    opacity: 1;
  }
  .option-btn.wrong {
    background: var(--red-bg);
    color: var(--red-text);
    border-color: var(--red);
    opacity: 1;
  }

  .feedback-box {
    margin-top: 12px;
    padding: 10px 14px;
    border-radius: 6px;
    font-size: 14px;
  }
  .feedback-box.good {
    background: var(--green-bg);
    color: var(--green-text);
    border: 1px solid var(--green-border);
  }
  .feedback-box.hint {
    background: var(--hint-bg);
    color: var(--hint-text);
    border: 1px solid var(--hint-border);
  }

  .fill-row { display: flex; gap: 10px; flex-wrap: wrap; align-items: center; }
  .text-input, textarea {
    font-family: Georgia, serif;
    font-size: 15px;
    background: #fff;
    border: 1px solid var(--border-btn);
    border-radius: 6px;
    padding: 8px 12px;
    color: var(--ink);
  }
  .text-input { flex: 1; min-width: 180px; }
  textarea { width: 100%; min-height: 80px; resize: vertical; }
  .text-input:disabled, textarea:disabled { background: var(--hover-bg); color: var(--muted); }

  .check-btn {
    font-family: Arial, sans-serif;
    font-size: 13px;
    background: var(--accent);
    color: #fff;
    border: none;
    border-radius: 6px;
    padding: 9px 18px;
    cursor: pointer;
  }
  .check-btn:hover { opacity: 0.9; }
  .check-btn:disabled { opacity: 0.5; cursor: default; }

  .word-bank {
    background: var(--hover-bg);
    border-radius: 8px;
    padding: 12px 16px;
    margin-bottom: 20px;
  }
  .word-bank .wb-title {
    font-family: Arial, sans-serif;
    font-size: 11px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 8px;
  }
  .chips { display: flex; flex-wrap: wrap; gap: 8px; }
  .chip {
    font-family: Arial, sans-serif;
    font-size: 13px;
    background: #fff;
    border: 1px solid var(--accent);
    color: var(--accent);
    padding: 4px 14px;
    border-radius: 14px;
  }

  .bubble {
    background: #fff;
    border: 1px solid var(--border-soft);
    border-radius: 10px;
    padding: 12px 16px;
    margin-bottom: 8px;
    font-size: 15px;
  }
  .bubble .who {
    font-family: Arial, sans-serif;
    font-size: 10px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--muted);
    display: block;
    margin-bottom: 4px;
  }
  .turn-instruction {
    font-size: 14px;
    color: var(--ink);
    margin-bottom: 10px;
  }

  .score-big {
    font-size: 42px;
    color: var(--red);
    font-weight: bold;
    margin: 10px 0 4px;
  }
  .score-caption {
    color: var(--muted);
    font-style: italic;
    margin-bottom: 8px;
  }
  .score-note { color: var(--muted); font-size: 13px; margin-bottom: 18px; }
  .recap-card {
    background: #fff;
    border: 1px solid var(--border-soft);
    border-radius: 4px;
    padding: 10px 14px;
    margin-bottom: 8px;
    font-size: 14px;
  }
  .recap-card .term { font-weight: bold; color: var(--accent); }

  .nav-buttons {
    display: flex;
    justify-content: space-between;
    gap: 12px;
    margin-top: 30px;
    padding-top: 20px;
    border-top: 1px solid var(--border-soft);
  }
  .nav-btn {
    font-family: Arial, sans-serif;
    font-size: 14px;
    padding: 10px 22px;
    border-radius: 6px;
    cursor: pointer;
    border: none;
    background: var(--red);
    color: #fff;
  }
  .nav-btn:hover { opacity: 0.9; }
  .nav-btn.secondary {
    background: transparent;
    border: 1px solid var(--accent);
    color: var(--accent);
  }
  .nav-spacer { width: 1px; }

  @media (max-width: 520px) {
    .paper { padding: 24px 18px 36px 20px; }
    header h1 { font-size: 21px; }
    .nav-buttons { flex-direction: column-reverse; }
    .nav-btn { width: 100%; }
    .nav-spacer { display: none; }
  }
</style>
</head>
<body>
<div class="paper">
  <header>
    <h1>Business English — Marketing Project Manager</h1>
    <div class="subtitle">Lesson 4 · timeline · briefing · milestone · customer acquisition · conduct · creative fatigue · put forward</div>
  </header>

  <div class="progress-track"><div class="progress-fill" id="progressFill"></div></div>
  <div class="progress-label" id="progressLabel">Stage 1 of 5</div>

  <div class="step-nav" id="stepNav"></div>

  <div id="stages"></div>

  <div class="nav-buttons" id="navButtons">
    <button class="nav-btn secondary" id="backBtn">← Back</button>
    <div class="nav-spacer"></div>
    <button class="nav-btn" id="nextBtn">Next →</button>
  </div>
</div>

<script>
/* ================= DATA ================= */

var VOCAB = [
  { term: "timeline",
    definition: "the schedule of a project, from start to finish",
    example: "Let's walk through the timeline — creative concepts are due in two weeks, and the launch is set for mid-March." },
  { term: "briefing",
    definition: "a meeting or document that explains what needs to be done and why",
    example: "I'll send the creative team a briefing today so they have everything they need before the kickoff call." },
  { term: "milestone",
    definition: "a significant checkpoint or achievement within a project",
    example: "Client sign-off on the concept is our next milestone — once that's done, production can start." },
  { term: "customer acquisition",
    definition: "the process of gaining new customers",
    example: "This campaign is focused entirely on customer acquisition — the goal is new sign-ups, not brand awareness." },
  { term: "conduct",
    definition: "to carry out or run something, such as a meeting, a survey, or research",
    example: "We conducted a short workshop with the client's sales team to understand their pain points before writing the brief." },
  { term: "creative fatigue",
    definition: "when an audience gets tired of seeing the same ad or creative too often, so performance drops",
    example: "Click-through rates have been falling for two weeks — it's a classic sign of creative fatigue, so we need fresh assets." },
  { term: "put forward",
    definition: "to propose or suggest an idea for others to consider",
    example: "I'd like to put forward a new concept direction — something a bit bolder than what we've been running." }
];

var MATCH_ITEMS = [
  { context: "You're opening a client call and want to walk through the schedule for the project.",
    sentence: "Let's start with the ___ — here's what's due and when.",
    options: ["timeline", "briefing", "milestone"], answer: "timeline",
    why: "The timeline is the project schedule — what's due and when." },
  { context: "You want the creative team to have everything they need before they start work.",
    sentence: "I'll send over a ___ so the team knows exactly what we need.",
    options: ["briefing", "conduct", "put forward"], answer: "briefing",
    why: "A briefing explains what needs to be done and why." },
  { context: "You're explaining the next important checkpoint in the project.",
    sentence: "Our next ___ is client sign-off on the concept.",
    options: ["milestone", "timeline", "creative fatigue"], answer: "milestone",
    why: "A milestone is a significant checkpoint within a project." },
  { context: "You're describing the goal of a campaign focused on new sign-ups rather than brand awareness.",
    sentence: "This campaign is all about ___ — we need new customers, not just visibility.",
    options: ["customer acquisition", "briefing", "put forward"], answer: "customer acquisition",
    why: "Customer acquisition is the process of gaining new customers." },
  { context: "You're describing a workshop you ran with the client's sales team.",
    sentence: "We ___ a short workshop to understand their pain points before writing the brief.",
    options: ["conduct", "put forward", "milestone"], answer: "conduct",
    why: "To conduct means to carry out or run something like a workshop or research." },
  { context: "Click-through rates have been dropping for two weeks on the same ad.",
    sentence: "This looks like ___ — we need fresh creative.",
    options: ["creative fatigue", "customer acquisition", "timeline"], answer: "creative fatigue",
    why: "Creative fatigue is when the audience gets tired of seeing the same ad." },
  { context: "You want to suggest a bolder new concept direction to the client.",
    sentence: "I'd like to ___ a new idea — something bolder than what we've been running.",
    options: ["put forward", "conduct", "briefing"], answer: "put forward",
    why: "To put forward an idea means to propose or suggest it." }
];

var GAP_ITEMS = [
  { context: "Kickoff email to a new client",
    sentence: "Attached is the project ___ — you'll see all key dates from concept to launch.",
    answer: "timeline", hint: "the schedule of the project" },
  { context: "Message to your creative director",
    sentence: "I'll put together a ___ today so the team has full context before Monday.",
    answer: "briefing", hint: "a document/meeting explaining what's needed" },
  { context: "Status update to your manager",
    sentence: "We just hit a big ___ — the client approved the full concept.",
    answer: "milestone", hint: "a significant checkpoint in a project" },
  { context: "Explaining a campaign's goal to a junior colleague",
    sentence: "The KPI here is ___, not engagement — we're measuring new sign-ups.",
    answer: "customer acquisition", hint: "gaining new customers" },
  { context: "Describing research you ran for a client",
    sentence: "We ___ a short survey with their existing customers before writing the messaging.",
    answer: "conducted", hint: "carried out / ran something — use the past tense of 'conduct'" },
  { context: "Explaining declining ad performance to a client",
    sentence: "The numbers are dropping because of ___ — the audience has seen this ad too many times.",
    answer: "creative fatigue", hint: "audience tired of seeing the same ad" },
  { context: "Proposing a new idea in a meeting",
    sentence: "Can I ___ an alternative approach before we finalize this?",
    answer: "put forward", hint: "propose / suggest an idea" }
];

var PRODUCTION_ITEMS = [
  { context: "A client asks when they'll see the first draft of the campaign.",
    prompt: "Explain the timeline, mentioning at least one date or phase.",
    model: "According to the timeline, you'll see the first concepts next Friday, with final assets ready two weeks before launch." },
  { context: "Your creative team says they don't have enough information to start.",
    prompt: "Tell them you'll send a briefing so they have what they need.",
    model: "I'll put together a proper briefing today so you have all the context and references before you start." },
  { context: "Your manager asks how the project is progressing.",
    prompt: "Mention a milestone you've recently reached.",
    model: "We just hit a key milestone — the client signed off on the full concept yesterday." },
  { context: "A client asks what success looks like for their new campaign.",
    prompt: "Explain that the focus is customer acquisition, not just awareness.",
    model: "This campaign is really about customer acquisition — we're optimizing for new sign-ups, not just visibility." },
  { context: "You're explaining how you gathered insights before writing a client brief.",
    prompt: "Say you conducted some research or interviews first.",
    model: "Before writing the brief, we conducted a few short interviews with their customer support team." },
  { context: "A client's ad performance has dropped after running for a month.",
    prompt: "Explain that it might be creative fatigue.",
    model: "This drop in performance looks like creative fatigue — the audience has probably seen the ad too many times." },
  { context: "You have an idea for a bolder campaign direction.",
    prompt: "Put forward your idea in a meeting.",
    model: "I'd like to put forward a different direction — something a bit bolder than what we've tested so far." }
];

var ROLEPLAY_TURNS = [
  { client: "Great to get started — can you walk me through what the next few weeks look like?",
    instruction: "Explain the timeline and mention the first milestone.",
    keywords: ["timeline", "milestone"],
    model: "Sure — here's the timeline: concepts are due in two weeks, and our first milestone is your sign-off on the direction." },
  { client: "Sounds good. How will your creative team know what to actually make?",
    instruction: "Explain that you'll prepare a briefing for the creative team, and that the focus is customer acquisition.",
    keywords: ["briefing", "customer acquisition"],
    model: "I'll prepare a full briefing for the creative team, and I'll make sure it's clear this campaign is focused on customer acquisition." },
  { client: "Before we finalize the brief, is there anything from the last campaign we should learn from?",
    instruction: "Mention that you conducted some research, and that performance dropped due to creative fatigue.",
    keywords: ["conduct", "creative fatigue"],
    model: "We conducted a quick review of the last campaign, and performance dropped mainly because of creative fatigue — the audience had seen the same ad too many times." },
  { client: "Good to know. So what would you suggest we do differently this time?",
    instruction: "Put forward a bolder new idea.",
    keywords: ["put forward"],
    model: "I'd like to put forward a bolder direction this time, based on what we learned from the last round." }
];

var RECAP = [
  ["timeline", "the schedule of a project"],
  ["briefing", "a meeting/document explaining what's needed"],
  ["milestone", "a significant checkpoint in a project"],
  ["customer acquisition", "gaining new customers"],
  ["conduct", "to carry out / run something"],
  ["creative fatigue", "audience tired of seeing the same ad"],
  ["put forward", "propose / suggest an idea"]
];

var SCREENS = [
  { tag: "Stage 1", label: "1", tooltip: "Meet the words", title: "Meet the words" },
  { tag: "Stage 2", label: "2", tooltip: "Match", title: "Match the meaning" },
  { tag: "Stage 3", label: "3", tooltip: "Fill the gap", title: "Fill the gap" },
  { tag: "Stage 4", label: "4", tooltip: "Own sentences", title: "Build your own sentence" },
  { tag: "Stage 5", label: "5", tooltip: "Role play", title: "Role play" },
  { tag: "Finish", label: "✓", tooltip: "Finish", title: "" }
];

/* ================= STATE ================= */

var currentScreen = 0;
var visited = [false, false, false, false, false, false];

// Stage 2 (match): per item — { answered: bool, correct: bool, chosen: string }
var matchState = MATCH_ITEMS.map(function () { return { answered: false, correct: false, chosen: null }; });
// Stage 3 (gap): { attempted: bool, correct: bool, locked: bool }
var gapState = GAP_ITEMS.map(function () { return { attempted: false, correct: false, locked: false }; });

var score = { correct: 0, attempted: 0 };

/* ================= HELPERS ================= */

function shuffle(arr) {
  var a = arr.slice();
  for (var i = a.length - 1; i > 0; i--) {
    var j = Math.floor(Math.random() * (i + 1));
    var tmp = a[i]; a[i] = a[j]; a[j] = tmp;
  }
  return a;
}

function normalize(s) {
  return s.trim().toLowerCase().replace(/\s+/g, " ");
}

function el(tag, cls, html) {
  var e = document.createElement(tag);
  if (cls) e.className = cls;
  if (html !== undefined) e.innerHTML = html;
  return e;
}

function escapeHtml(s) {
  return s.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
}

/* ================= STAGE BUILDERS (rendered ONCE) ================= */

function buildStageShell(index, tag, title, intro) {
  var stage = el("div", "stage");
  stage.id = "screen" + index;
  stage.appendChild(el("span", "stage-tag", tag));
  stage.appendChild(el("h2", null, title));
  stage.appendChild(el("div", "stage-intro", intro));
  return stage;
}

function buildVocabStage(container) {
  var stage = buildStageShell(0, "Stage 1", "These 7 words, the way you'll actually use them",
    "Read each one in a real PM situation — no exercise here, just get familiar.");
  var list = el("div");
  VOCAB.forEach(function (v) {
    var card = el("div", "vocab-card");
    card.appendChild(el("div", "term", escapeHtml(v.term)));
    card.appendChild(el("div", "definition", escapeHtml(v.definition)));
    card.appendChild(el("div", "example", "\u201C" + escapeHtml(v.example) + "\u201D"));
    list.appendChild(card);
  });
  stage.appendChild(list);
  container.appendChild(stage);
}

function buildMatchStage(container) {
  var stage = buildStageShell(1, "Stage 2", "Match the meaning",
    "Pick the correct word — this only checks understanding, so relax and trust your instinct.");
  MATCH_ITEMS.forEach(function (item, i) {
    var block = el("div", "item");
    block.appendChild(el("div", "context-line", "[" + escapeHtml(item.context) + "]"));
    block.appendChild(el("div", "prompt", "\u201C" + escapeHtml(item.sentence) + "\u201D"));
    var options = el("div", "options");
    shuffle(item.options).forEach(function (opt) {
      var btn = el("button", "option-btn", escapeHtml(opt));
      btn.type = "button";
      btn.addEventListener("click", function () { checkMatch(i, opt, btn); });
      options.appendChild(btn);
    });
    block.appendChild(options);
    var fb = el("div", null);
    fb.id = "matchFb" + i;
    fb.style.display = "none";
    block.appendChild(fb);
    stage.appendChild(block);
  });
  container.appendChild(stage);
}

function checkMatch(i, choice, btn) {
  var st = matchState[i];
  if (st.answered) return; // locked
  var item = MATCH_ITEMS[i];
  st.answered = true;
  st.chosen = choice;
  st.correct = (choice === item.answer);
  score.attempted++;
  if (st.correct) score.correct++;

  var buttons = btn.parentElement.querySelectorAll(".option-btn");
  buttons.forEach(function (b) {
    b.disabled = true;
    var val = b.textContent;
    if (val === item.answer) b.classList.add("correct");
  });
  if (!st.correct) btn.classList.add("wrong");

  var fb = document.getElementById("matchFb" + i);
  fb.className = "feedback-box " + (st.correct ? "good" : "hint");
  fb.innerHTML = (st.correct ? "✓ Correct! " : "Not quite. ") + escapeHtml(item.why);
  fb.style.display = "block";
}

function buildGapStage(container) {
  var stage = buildStageShell(2, "Stage 3", "Fill the gap",
    "Type the correct word or phrase into each gap.");
  var bank = el("div", "word-bank");
  bank.appendChild(el("div", "wb-title", "Word bank"));
  var chips = el("div", "chips");
  VOCAB.forEach(function (v) {
    chips.appendChild(el("span", "chip", escapeHtml(v.term)));
  });
  bank.appendChild(chips);
  stage.appendChild(bank);

  GAP_ITEMS.forEach(function (item, i) {
    var block = el("div", "item");
    block.appendChild(el("div", "context-line", "[" + escapeHtml(item.context) + "]"));
    block.appendChild(el("div", "prompt", "\u201C" + escapeHtml(item.sentence) + "\u201D"));
    var row = el("div", "fill-row");
    var input = el("input", "text-input");
    input.type = "text";
    input.id = "gapInput" + i;
    input.placeholder = "Type your answer…";
    var btn = el("button", "check-btn", "Check");
    btn.type = "button";
    btn.addEventListener("click", function () { checkGap(i); });
    row.appendChild(input);
    row.appendChild(btn);
    block.appendChild(row);
    var fb = el("div", null);
    fb.id = "gapFb" + i;
    fb.style.display = "none";
    block.appendChild(fb);
    stage.appendChild(block);
  });
  container.appendChild(stage);
}

function checkGap(i) {
  var st = gapState[i];
  if (st.locked) return;
  var item = GAP_ITEMS[i];
  var input = document.getElementById("gapInput" + i);
  var fb = document.getElementById("gapFb" + i);
  var val = normalize(input.value);

  if (val === "") {
    fb.className = "feedback-box hint";
    fb.innerHTML = "Type an answer first.";
    fb.style.display = "block";
    return; // does not count as an attempt
  }

  if (!st.attempted) {
    st.attempted = true;
    score.attempted++;
  }

  if (val === normalize(item.answer)) {
    st.correct = true;
    st.locked = true;
    score.correct++;
    input.disabled = true;
    fb.className = "feedback-box good";
    fb.innerHTML = "✓ Correct!";
  } else {
    fb.className = "feedback-box hint";
    fb.innerHTML = "Not quite — hint: " + escapeHtml(item.hint) + ". Try again.";
  }
  fb.style.display = "block";
}

function buildProductionStage(container) {
  var stage = buildStageShell(3, "Stage 4", "Build your own sentence",
    "Build the sentence yourself with the target word — there's no single correct answer. Then compare with the model.");
  PRODUCTION_ITEMS.forEach(function (item, i) {
    var block = el("div", "item");
    block.appendChild(el("div", "context-line", "[" + escapeHtml(item.context) + "]"));
    block.appendChild(el("div", "prompt", escapeHtml(item.prompt)));
    var ta = el("textarea");
    ta.id = "prodTa" + i;
    ta.placeholder = "Write your sentence here…";
    block.appendChild(ta);
    var btn = el("button", "check-btn", "Compare with model answer");
    btn.type = "button";
    btn.style.marginTop = "10px";
    btn.addEventListener("click", function () { showProdModel(i); });
    block.appendChild(btn);
    var fb = el("div", null);
    fb.id = "prodFb" + i;
    fb.style.display = "none";
    block.appendChild(fb);
    stage.appendChild(block);
  });
  container.appendChild(stage);
}

function showProdModel(i) {
  var item = PRODUCTION_ITEMS[i];
  var fb = document.getElementById("prodFb" + i);
  fb.className = "feedback-box good";
  fb.innerHTML = "A natural version: \u201C" + escapeHtml(item.model) + "\u201D" +
    "<div style='font-size:12px;margin-top:6px;color:var(--green-text);'>Compare it to yours — did you use the target word naturally?</div>";
  fb.style.display = "block";
}

function buildRoleplayStage(container) {
  var stage = buildStageShell(4, "Stage 5", "Role play",
    "Client kickoff call for a new campaign.");
  var scenario = el("div", null,
    "You're a Marketing PM at an agency, kicking off a new campaign with a client. " +
    "You need to walk them through the timeline and milestones, explain how you'll brief the creative team, " +
    "clarify that this campaign is about customer acquisition, mention the research you conducted, " +
    "flag creative fatigue on their current ads, and put forward a bolder new idea.");
  scenario.className = "feedback-box hint";
  scenario.style.marginBottom = "18px";
  stage.appendChild(scenario);

  ROLEPLAY_TURNS.forEach(function (turn, i) {
    var block = el("div", "item");
    var bubble = el("div", "bubble");
    bubble.appendChild(el("span", "who", "Client"));
    bubble.appendChild(document.createTextNode(turn.client));
    block.appendChild(bubble);
    block.appendChild(el("div", "turn-instruction", escapeHtml(turn.instruction)));
    var ta = el("textarea");
    ta.id = "roleTa" + i;
    ta.placeholder = "Write your reply as the PM…";
    block.appendChild(ta);
    var btn = el("button", "check-btn", "Check my sentence");
    btn.type = "button";
    btn.style.marginTop = "10px";
    btn.addEventListener("click", function () { checkRoleTurn(i); });
    block.appendChild(btn);
    var fb = el("div", null);
    fb.id = "roleFb" + i;
    fb.style.display = "none";
    block.appendChild(fb);
    stage.appendChild(block);
  });
  container.appendChild(stage);
}

function checkRoleTurn(i) {
  var turn = ROLEPLAY_TURNS[i];
  var ta = document.getElementById("roleTa" + i);
  var fb = document.getElementById("roleFb" + i);
  var text = ta.value.toLowerCase();
  var allFound = turn.keywords.every(function (kw) {
    return text.indexOf(kw.toLowerCase()) !== -1;
  });

  if (allFound) {
    fb.className = "feedback-box good";
    fb.innerHTML = "✓ Great — you used the target language naturally.<br><br>A natural model version: \u201C" +
      escapeHtml(turn.model) + "\u201D";
  } else {
    fb.className = "feedback-box hint";
    fb.innerHTML = "Try to include: " + turn.keywords.map(escapeHtml).join(", ") + ".<br><br>" +
      "Model version for comparison: \u201C" + escapeHtml(turn.model) + "\u201D";
  }
  fb.style.display = "block";
}

function buildFinishStage(container) {
  var stage = el("div", "stage");
  stage.id = "screen5";
  stage.appendChild(el("span", "stage-tag", "Finish"));
  stage.appendChild(el("h2", null, "Nice work, Marta 👏"));
  var scoreBox = el("div");
  scoreBox.id = "finishScore";
  stage.appendChild(scoreBox);
  stage.appendChild(el("div", null,
    "Here are today's 7 words one more time — say each one out loud in a sentence about your own week before next lesson."));
  var list = el("div");
  list.style.marginTop = "16px";
  RECAP.forEach(function (r) {
    var card = el("div", "recap-card");
    card.innerHTML = "<span class='term'>" + escapeHtml(r[0]) + "</span> — " + escapeHtml(r[1]);
    list.appendChild(card);
  });
  stage.appendChild(list);
  container.appendChild(stage);
}

/* ================= NAVIGATION ================= */

function renderScore() {
  var box = document.getElementById("finishScore");
  var notAnswered = 14 - score.attempted;
  var html = "<div class='score-big'>" + score.correct + " / 14</div>" +
    "<div class='score-caption'>correct on Stage 2–3 exercises</div>";
  if (notAnswered > 0) {
    html += "<div class='score-note'>" + notAnswered + (notAnswered === 1 ? " exercise" : " exercises") +
      " not answered yet — jump back to any stage with the step dots above.</div>";
  } else {
    html += "<div class='score-note'>All 14 exercises answered.</div>";
  }
  box.innerHTML = html;
}

function showScreen(index) {
  currentScreen = index;
  visited[index] = true;

  // stages
  for (var i = 0; i < 6; i++) {
    document.getElementById("screen" + i).classList.toggle("active", i === index);
  }

  // progress bar
  var pct = (index / 5) * 100;
  document.getElementById("progressFill").style.width = pct + "%";
  document.getElementById("progressLabel").textContent =
    index === 5 ? "Lesson complete!" : "Stage " + (index + 1) + " of 5";

  // step dots
  var dots = document.querySelectorAll(".step-dot");
  dots.forEach(function (d, i) {
    d.classList.toggle("current", i === index);
    d.classList.toggle("visited", visited[i] && i !== index);
  });

  // nav buttons
  var back = document.getElementById("backBtn");
  var next = document.getElementById("nextBtn");
  back.style.visibility = index === 0 ? "hidden" : "visible";
  next.textContent = index === 4 ? "Finish lesson →" : (index === 5 ? "Start over →" : "Next →");

  if (index === 5) renderScore();

  window.scrollTo({ top: 0, behavior: "auto" });
}

function buildStepNav() {
  var nav = document.getElementById("stepNav");
  SCREENS.forEach(function (s, i) {
    var btn = el("button", "step-dot", s.label);
    btn.type = "button";
    btn.title = s.tooltip;
    btn.addEventListener("click", function () { showScreen(i); });
    nav.appendChild(btn);
  });
}

function init() {
  var container = document.getElementById("stages");
  buildVocabStage(container);
  buildMatchStage(container);
  buildGapStage(container);
  buildProductionStage(container);
  buildRoleplayStage(container);
  buildFinishStage(container);

  buildStepNav();

  document.getElementById("backBtn").addEventListener("click", function () {
    if (currentScreen > 0) showScreen(currentScreen - 1);
  });
  document.getElementById("nextBtn").addEventListener("click", function () {
    if (currentScreen < 4) showScreen(currentScreen + 1);
    else if (currentScreen === 4) showScreen(5);
    else showScreen(0); // "Start over" on finish screen — just returns to stage 1 view
  });

  document.addEventListener("keydown", function (e) {
    if (e.key !== "ArrowLeft" && e.key !== "ArrowRight") return;
    var t = e.target;
    if (t && (t.tagName === "INPUT" || t.tagName === "TEXTAREA")) return;
    if (e.key === "ArrowLeft" && currentScreen > 0) showScreen(currentScreen - 1);
    if (e.key === "ArrowRight" && currentScreen < 5) showScreen(currentScreen + 1);
  });

  showScreen(0);
}

document.addEventListener("DOMContentLoaded", init);
</script>
</body>
</html>
