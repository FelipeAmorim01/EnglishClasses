# Page anatomy

How a `lesson_plan_N.html` page is built. Read before creating or editing one.

## Contents

- [Ground rules](#ground-rules)
- [Page skeleton](#page-skeleton)
- [The navigation script](#the-navigation-script)
- [Component vocabulary](#component-vocabulary)
- [Interactive widgets](#interactive-widgets)
- [Registering the lesson](#registering-the-lesson)
- [Mobile](#mobile)
- [Gotchas](#gotchas)

## Ground rules

Every page is **fully self-contained** — one `<style>` block, one `<script>`
block, fonts from Google Fonts, nothing else. There is no shared stylesheet and
this is deliberate: each lesson is copy-forwarded from the last, so an old lesson
never breaks when a new component is added.

**To build lesson N+1: copy `lesson_plan_N.html`.** It has the most complete CSS.
Strip the widgets that do not apply, keep the base, add what is new.

The design tokens, unchanged since lesson 0:

```css
:root {
  --bg: #f5f2ee;        --surface: #ffffff;   --surface2: #ede9e3;
  --border: #d8d2c8;    --accent: #2d5f3f;    --accent-light: #e8f0eb;
  --accent2: #b85c2a;   --text: #1a1a18;      --muted: #7a7368;
  --sidebar-w: 210px;
}
```

Green (`--accent`) is structure and state. Orange (`--accent2`) is emphasis and
warning. Lora serif for headings and anything meant to be *said*; Inter for
everything else.

## Page skeleton

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="robots" content="noindex, nofollow" />
    <title>English Conversation — Lesson 5</title>
    <link href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400;0,600;1,400;1,600&family=Inter:wght@400;500;600&display=swap" rel="stylesheet" />
    <style>/* tokens, base, components */</style>
  </head>
  <body>
    <header>
      <div>
        <h1>English Conversation</h1>
        <div class="subtitle">Storytelling — Lesson 5</div>
      </div>
      <a class="back-link" href="index.html">&larr; All classes</a>
    </header>

    <div class="progress-wrap"><div class="progress-fill" id="progress-fill"></div></div>

    <main>
      <aside>
        <div class="nav-item active" onclick="goTo(0)">
          <div class="nav-num">01</div><div class="nav-label">Warm-up</div>
        </div>
        <!-- one .nav-item per stage -->
      </aside>

      <div class="content">
        <div class="stage active" id="stage-0">
          <div class="stage-eyebrow">Stage 01 of 04</div>
          <div class="stage-title">Warm-up: <em>the accent half</em></div>
          <div class="stage-sub">One or two lines setting up the stage.</div>
          <div class="section-label">Let's talk</div>
          <ul class="q-list"><li>…</li></ul>
        </div>
        <!-- .stage blocks, ids stage-1 … stage-N -->
      </div>
    </main>

    <div class="nav-bar">
      <button class="btn" id="btn-prev" onclick="prev()" disabled>Previous</button>
      <span class="step-counter" id="step-counter">Step 1 of 4</span>
      <button class="btn primary" id="btn-next" onclick="next()">Next</button>
    </div>

    <script>/* nav + widgets */</script>
  </body>
</html>
```

`.stage-title` puts the second half in `<em>` — it renders italic green. The
`.stage-eyebrow` reads `Stage 0K of 0T` and must match the real stage count.

## The navigation script

Copy verbatim. `total` and the `done` array length must equal the number of stages.

```js
let current = 0;
const total = 4;
const done = [false, false, false, false];

function goTo(idx) {
  if (idx < 0 || idx >= total) return;
  if (idx > current) done[current] = true;
  document.querySelectorAll(".stage").forEach((el, i) =>
    el.classList.toggle("active", i === idx));
  document.querySelectorAll(".nav-item").forEach((el, i) => {
    el.classList.toggle("active", i === idx);
    el.classList.toggle("done", done[i] && i !== idx);
  });
  current = idx;
  document.getElementById("btn-prev").disabled = current === 0;
  document.getElementById("btn-next").disabled = current === total - 1;
  document.getElementById("btn-next").textContent =
    current === total - 2 ? "Last stage" : "Next";
  document.getElementById("step-counter").textContent =
    "Step " + (current + 1) + " of " + total;
  document.getElementById("progress-fill").style.width =
    (current / (total - 1)) * 100 + "%";
  document.querySelector(".content").scrollTo({ top: 0, behavior: "smooth" });
  window.scrollTo({ top: 0, behavior: "smooth" }); // mobile scrolls the page
}
function next() { goTo(current + 1); }
function prev() { goTo(current - 1); }
```

## Component vocabulary

Reuse these before inventing anything.

**Discussion questions** — `<ul class="q-list"><li>` — italic Lora on a tinted
ground with a left rule. Four or five per warm-up.

**Vocabulary table** — `<table class="vocab-table">` with `thead`/`tbody`, three
columns. Column 2 renders bold green. Column 3 is the sentence to read aloud,
wrapped in `<em>`.

**Idioms and phrasal verbs** — `.idiom-grid` > `.idiom-card` > `.idiom-term` +
`.idiom-meaning` + `.idiom-example`. Six per grid reads well; twelve is fine.

**Phrase banks** — `.chip-group` > `.chip-group-label` + `.vocab-chips` >
`span.chip`. The workhorse for fixed expressions grouped by function.

**Two-column contrast** — `.topic-split` > `.topic-card.safe` /
`.topic-card.risky` > `.topic-head` + `ul` + optional `.topic-note`.

**Roleplay** — `.scenario-intro` (+ `.intro-label`), then `.negotiation-layout` >
`.negotiation-main` + `.language-sidebar`. Inside main: `.scenario-block` >
`.scenario-name` + `.position-split` > `.position-card.mine` /
`.position-card.counterpart`, with a `button.reveal-toggle` calling
`toggleReveal('reveal-a', this)` to flip `.revealed`. Hidden briefs are what make
these work — he cannot prepare for what he cannot see.

**Sticky sidebar** — `.language-sidebar` inside `.negotiation-layout`, filled with
`.chip-group`s. Use it on any stage where he needs the target language visible
while talking.

**Homework / applied task** — `.apply-box` > `.apply-label` + `.apply-lead` +
`<ol class="apply-steps">`, or `.reflection-grid` > `.reflection-row` >
`.reflection-label` + `.reflection-content`.

**Misc** — `.section-label` (small caps section heading), `.divider`,
`.panel-note` (small muted explanatory text), `.reset-row`.

## Interactive widgets

Built per-lesson; keep whichever ones the new lesson uses and delete the rest.

- **Prompt deck** (`.prompt-deck`, `.prompt-card`, `.prompt-text`,
  `.prompt-constraint`, `.deck-controls`) — draws from a shuffled array so nothing
  repeats until the deck is exhausted, then reshuffles.
- **Clock** (`.timer-panel`, `.timer-display`, `.timer-bar`, `.timer-bar-fill`,
  `.timer-controls`, `.mute-btn`) — countdown with a warning state at 20%
  remaining, a `beep()` built on `AudioContext` wrapped in try/catch, and a mute
  toggle. Drive the duration from a state object, not a hard-coded constant.
- **Derailer** (`.react-grid`, `.react-btn`, `.react-btn.fired`, `.derail-log`,
  `.derail-entry`, `.derail-time`) — buttons Felipe fires mid-activity, each
  labelled with the grammar it forces ("forces a scene: past continuous"), logged
  with a timestamp.
- **No-repeat chip drill** (`.drill-panel`, `.drill-line`, `.drill-chips`,
  `.drill-chip.used`, `.drill-status`) — a line is read out, he responds, the
  expression he used is clicked and struck through. Scarcity does the work.

The shuffle helper worth copying:

```js
function shuffle(arr) {
  const out = arr.slice();
  for (let i = out.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [out[i], out[j]] = [out[j], out[i]];
  }
  return out;
}
```

## Registering the lesson

Append one object to the `LESSONS` array in `Raffa/index.html` (there is a comment
block above it explaining the fields). The card label and the count both derive
from the array, so nothing else needs editing.

```js
{
  file: "lesson_plan_4.html",
  title: "Storytelling & Anecdotes",
  date: "5 September 2026",
  desc: "One line describing what the class covers.",
},
```

Set `soon: true` for a class that is not ready — it renders as a dashed,
unclickable card.

**Numbering:** files are zero-indexed, `<title>` is one-indexed, and the library
labels by array position. So `lesson_plan_4.html` carries
`<title>English Conversation — Lesson 5</title>` and appears as "Lesson 4". This
mismatch is the established convention — reproduce it, do not correct it.

## Mobile

The `@media (max-width: 720px)` block is inherited and mostly handles itself: the
sidebar becomes a horizontal scrolling tab strip, `.nav-num` hides, vocab tables
stack into cards with a `→` prefix on column 2, and `.nav-bar` sticks to the
bottom. **Any new grid needs its own rule collapsing it to one column**, or it
will push the page wider than the viewport.

## Gotchas

- **`.apply-steps li` is `display: flex`** (number badge + text). Inline `<em>`,
  `<strong>` or `<a>` inside one becomes a separate flex item and breaks the
  sentence into columns. Keep those items plain text.
- **`.q-list li` is a normal list item** — inline markup there is fine.
- **`.negotiation-main` needs `min-width: 0`**, or a wide child will push the
  whole page past the viewport.
- Widgets sharing state (two mute buttons, say) must keep their labels in sync, or
  drop the duplicate control.
- Reset functions need to restore the *rest* state, not the *finished* state — a
  countdown bar should read empty after a reset, not full.
