# Page anatomy — Peterson

How a `Peterson/lesson_plan_N.html` page is built. Read before creating or
editing one.

The skeleton, the design tokens, the navigation script and the mobile behaviour
are **shared with Raffa's pages** and were copied from them. The components in
[Peterson-only components](#peterson-only-components) were built for this track
and do not exist on Raffa's pages.

## Contents

- [Ground rules](#ground-rules)
- [Page skeleton](#page-skeleton)
- [The navigation script](#the-navigation-script)
- [Shared components](#shared-components)
- [Peterson-only components](#peterson-only-components)
- [Widgets](#widgets)
- [Registering the lesson](#registering-the-lesson)
- [Mobile](#mobile)
- [Gotchas](#gotchas)

## Ground rules

Every page is **fully self-contained** — one `<style>` block, one `<script>`
block, fonts from Google Fonts, nothing else. No shared stylesheet, deliberately:
each lesson is copy-forwarded from the last, so an old lesson never breaks when a
new component is added.

**To build lesson N+1: copy `lesson_plan_N.html`.** Strip the widgets that do not
apply, keep the base, add what is new.

Design tokens, identical to Raffa's:

```css
:root {
  --bg: #f5f2ee;        --surface: #ffffff;   --surface2: #ede9e3;
  --border: #d8d2c8;    --accent: #2d5f3f;    --accent-light: #e8f0eb;
  --accent2: #b85c2a;   --text: #1a1a18;      --muted: #7a7368;
  --sidebar-w: 210px;
}
```

Green (`--accent`) is structure and correctness. Orange (`--accent2`) is emphasis
and warning — it is the colour of the struck-through wrong form. Lora serif for
headings and anything meant to be *said*; Inter for everything else.

## Page skeleton

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="robots" content="noindex, nofollow" />
    <title>English Conversation — Lesson 1</title>
    <link href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400;0,600;1,400;1,600&family=Inter:wght@400;500;600&display=swap" rel="stylesheet" />
    <style>/* tokens, base, components */</style>
  </head>
  <body>
    <header>
      <div>
        <h1>English Conversation</h1>
        <div class="subtitle">Getting Started — Lesson 1</div>
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
          <div class="stage-title">Warm-up: <em>hello</em></div>
          <div class="stage-sub">One or two short lines.</div>
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

**Keep the prose short.** Stage subs on Raffa's pages run to three sentences of
atmosphere; here they are one line. Peterson has to be able to read them.

## The navigation script

Copy verbatim. `total` and the `done` array length must equal the stage count.

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

The `shuffle` helper is also worth copying verbatim:

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

## Shared components

Inherited from Raffa's pages; reuse before inventing anything.

**Vocabulary table** — `<table class="vocab-table">` with `thead`/`tbody`, three
columns. Column 2 renders bold green. Column 3 is the sentence to read aloud,
wrapped in `<em>`. Build each column-3 sentence so the target pattern appears
two or three times, so one reading is several reps.

**Cards** — `.idiom-grid` > `.idiom-card` > `.idiom-term` + `.idiom-meaning` +
`.idiom-example`. On this track these are used as **question / how to answer /
example answer** rather than idiom definitions.

**Phrase banks** — `.chip-group` > `.chip-group-label` + `.vocab-chips` >
`span.chip`. The workhorse. Grouped by function, never more than about six per
group.

**Roleplay** — `.scenario-intro` (+ `.intro-label`), optional `.scenario-numbers`
for the situation, then `.scenario-block` > `.scenario-name` + `.position-split`
> `.position-card.mine` / `.position-card.counterpart`, with a
`button.reveal-toggle` calling `toggleReveal('reveal-a', this)`. **Name the roles
in `.position-role`** — "You — the new employee", "Me — a colleague from another
team". A beginner should never have to infer who he is playing.

**Sticky sidebar** — `.language-sidebar` inside `.negotiation-layout` (with
`.negotiation-main`), filled with `.chip-group`s, so the target language stays
visible while he talks.

**Label / content rows** — `.reflection-grid` > `.reflection-row` >
`.reflection-label` + `.reflection-content`. Used for the who-speaks legend and
for the "Next class" note.

**Homework** — `.apply-box` > `.apply-label` + `.apply-lead` + `p.apply-text` +
`a.apply-link`.

**Misc** — `.section-label`, `.divider`, `.panel-note`, `.q-list`.

## Peterson-only components

**The ladder** — `.ladder` > `.ladder-step` > `.ladder-num` + `.ladder-body` >
`.ladder-say` (italic Lora, the sentence) + `.ladder-note` (what it needs). Five
sentences, easiest first. It opens the warm-up as the diagnostic and closes the
wrap-up as the bookend, with the same five sentences both times.

**Fix cards** — `.fix-grid` > `.fix-card` > `.fix-bad` + `.fix-good` +
`.fix-note`. `.fix-bad` is struck through in orange with a `✗` prefix;
`.fix-good` is bold green with a `✓`. This is how Portuguese-speaker errors get
taught without putting Portuguese on the page. Also good for pronunciation
contrasts (*thir-TEEN* vs *THIR-ty*).

**Word bank** — `.word-bank` > `span.chip`. A denser, ungrouped chip layout for
long lists of single words (jobs, verbs). Distinct from `.vocab-chips`, which is
for grouped fixed expressions.

## Widgets

**Question deck** (`.prompt-deck`, `.prompt-card`, `.prompt-text`,
`.deck-controls`, `.deck-count`) — `drawQuestion()` pops from a shuffled array
so nothing repeats until the deck is exhausted; `resetDeck()` reshuffles.
Questions should be two-part so they demand more than one sentence. The rule /
constraint strip that Raffa's decks carry was built here and cut — do not
reintroduce it.

**Sentence builder** (`.builder`, `.builder-card`, `.builder-sentence`,
`.builder-mode` > `.mode-label` + `.mode-chip`, `.builder-controls`,
`.builder-count`) — generates a random grammatical sentence to say out loud, in
positive / negative / question / mix mode. It drills exactly where Portuguese
speakers break: the third-person `-s` and the `do`/`does` auxiliary.

The generator is data-driven — `B_SUBJ` (each with a `third` flag, and `qOk:
false` for subjects that read badly as questions), `B_VERBS` (with `base`, `s`,
a `time` flag and a `comp` list), and `B_TIME`. **Complements must be
subject-neutral**, since any subject can be paired with any complement. Time
phrases only attach to verbs flagged `time: true`, or you get "She lives in São
Paulo every day".

If you change the generator, generate a dozen sentences in every mode and read
them before shipping.

## Registering the lesson

Append one object to the `LESSONS` array in `Peterson/index.html`:

```js
{
  file: "lesson_plan_0.html",
  title: "Getting Started",
  date: "10 September 2026",
  desc: "One line describing what the class covers.",
},
```

Set `soon: true` for a class that is not ready — it renders as a dashed,
unclickable card.

**Numbering:** files are zero-indexed, `<title>` is one-indexed, and the library
labels by array position. So `lesson_plan_0.html` carries
`<title>English Conversation — Lesson 1</title>` and appears as "Lesson 0". This
mismatch is inherited from Raffa's pages — reproduce it, do not correct it.

## Mobile

The `@media (max-width: 720px)` block is inherited: the sidebar becomes a
horizontal scrolling tab strip, `.nav-num` hides, vocab tables stack into cards
with a `→` prefix on column 2, `.reflection-row` stacks, and `.nav-bar` sticks to
the bottom.

**Any new grid needs its own rule collapsing it to one column.**

## Gotchas

- **A mobile rule can be silently overridden.** `.fix-grid` was given
  `grid-template-columns: 1fr` inside the inherited media query, but the
  component's own two-column rule was declared *later* in the stylesheet at the
  same specificity, so it won. Put mobile overrides for new components in a
  media block **after** their base rule, and verify with `getComputedStyle`.
- **`.apply-steps li` is `display: flex`** (number badge + text). An inline
  `<em>`, `<strong>` or `<a>` inside one becomes a separate flex item and breaks
  the sentence into columns. This is why homework uses `p.apply-text` +
  `a.apply-link` instead of a numbered list.
- **`.q-list li` is a normal list item** — inline markup there is fine.
- **`.negotiation-main` needs `min-width: 0`**, or a wide child pushes the whole
  page past the viewport.
- **Verify external links.** A plausible-looking BBC episode URL turned out to be
  a 404; the real one had a different slug pattern. Curl it before shipping.
- Reset functions must restore the *rest* state, not the *finished* state.
