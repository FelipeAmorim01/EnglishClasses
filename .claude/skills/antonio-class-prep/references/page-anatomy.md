# Page anatomy — Antonio's DET lessons

Each lesson is one self-contained HTML file, `Antonio/lesson_plan_N.html`, with
all CSS and JS inline. Copy the latest one and replace the content. Lesson 1
was copied from Raffa's template, so the design tokens, fonts (Lora + Inter)
and base components match the other tracks.

## Skeleton

```
<head>  <title>DET Prep — Class N</title>  …inline <style>…
<body>
  <header>  h1 "Duolingo English Test Prep" · .subtitle "<Title> — Class N" · .back-link → index.html
  .progress-wrap > #progress-fill
  <main>
    <aside>  .nav-item × stages (onclick="goTo(i)"), .nav-num "01", .nav-label
    .content
      .stage#stage-0.active … .stage#stage-K
        .stage-eyebrow "Stage 0X of 0K" · .stage-title (with <em>) · .stage-sub
  </main>
  #timer-home[hidden] > #timer-panel        (Lesson 2 on: one clock, moved by JS)
  .nav-bar  #btn-prev · #step-counter · #btn-next
  <script>
```

Navigation: `total` and `done[]` must match the number of stages, and the
`#step-counter` default text must say "Step 1 of K". `goTo()` also moves
`#timer-panel` into the active stage's `.timer-slot`, if it has one.

## Content components

| Class | Use |
|---|---|
| `.section-label` | small uppercase heading inside a stage |
| `.q-list` | warm-up questions (normal `li`, inline markup OK) |
| `.idiom-grid > .idiom-card` (`.idiom-term`, `.idiom-meaning`, `.idiom-example`) | 4 strategy or rule cards |
| `.apply-box` (`.apply-label`, `.apply-lead`, `ol.apply-steps`) | numbered steps. `li` is flex: inline tags become columns, so use only one leading `<strong>` per item, or keep it plain |
| `table.det-table` | task or clue tables, stacks on mobile |
| `.score-grid > .score-card(.target)` (`.score-big`, `.score-cap`) | big numbers |
| `.panel-note` | short muted note |
| `.negotiation-layout > .negotiation-main + .language-sidebar` | practice stage with sticky sidebar |
| `.chip-group > .chip-group-label + .vocab-chips > .chip` | frames and reminders in the sidebar |
| `.reflection-grid > .reflection-row` (`.reflection-label`, `.reflection-content`) | homework; `ol.hw-steps`, `.hw-prompts-label`, `ol.hw-prompts` inside |
| `.divider` | separator |

## Drill widgets

All drills live in a `.task-block`:
`.task-head > .task-name (<span>A</span>Name) + .task-time "1:00"`, then
`.task-how` (the instruction, in second person), the widget, and
`.task-actions` with `.mini-btn` buttons and a `.task-result` span.

**Read and Select** — `#word-grid` of `.word-btn`, built by `buildWords()` from
`[word, isReal]` pairs (8 real + 8 fake, shuffled). Click toggles `.picked`;
`checkWords()` marks `.ok` / `.bad` (struck through) / `.missed` (dashed).
Lesson 2 has `ROUNDS` (name, note, words) with tabs in `#round-tabs`.

**Read and Complete / typed answers** — inputs with `data-a="<answer>"`:
- In a C-test paragraph (`.ctest#id`): `<span class="gap">peo<input data-a="ple" /></span>`.
  JS sets `maxLength` and a width of `len + 1` ch.
- Whole-word answers (`ol.fam-list`, Lesson 2): bare `<input data-a="decision" />`,
  wrapped in `.gap` by JS for styling.
- Generic `checkSet(id, resultId)`, `showSet(id)`, `resetSet(id, resultId)`
  (Lesson 2). Comparison is trimmed and case-insensitive. `showSet` **keeps
  what was typed** (struck through) and puts the right answer beside it in a
  `.fix-ans` tag, so Felipe can see why it was wrong. Never overwrite the
  student's answer. Lesson 1 used
  single-set `checkGaps()` and the rest; prefer the generic ones.

**Spelling pairs** — `PAIRS = [[right, wrong], …]` → `.pair-row`s of two
`.word-btn`s (`data-ok`), one pick per row; `checkPairs()`; tips toggle in
`ul.why-list` (`.shown`).

**Listen and Type** (Lesson 1) — `SENTENCES` → `.type-item` with a
`textarea.type-box` and a "Show the sentence" toggle on `.answer-line`. Felipe
reads the sentence aloud; there is no audio file.

**Write About the Photo** (Lesson 1) — `.photo-frame` holding an inline SVG
scene (no external images), `textarea#photo-text` with a live `.word-count`.

**Speaking prompts** — `.speak-prompt` (Lora, accent border, bullet list).

**Interactive Speaking** — `.hidden-qs#iq > ol` blurred until
`toggleQs()` adds `.revealed`. The questions are only heard on the test, so they
stay hidden while he answers.

**Recorder** (Lesson 5) — `<div class="rec" id="…"></div>`, built by
`buildRec()`. `data-prep` (default 20, `0` = no prep) and `data-talk`
(default 90). Start → prep countdown → beep → MediaRecorder + analyser
(RMS every 100 ms) → time up or Stop (unlocks after 30 s). `addTake()` adds
audio, Save link, `.take-map` canvas (voice green, pauses of 2+ s orange,
click seeks) and stats. One recording at a time (`recNow`). Test it with a
fake `getUserMedia` returning an oscillator stream with gated gain.

**Choice drills** (Lesson 5) — `CH[id]` with `kind` `wide` (shared `labels`,
items `[text, answerIndex]`), `stack` (items `{q, opts: [[text, why]], a}`) or
`three` (`opts` plain strings). `buildCH`, `pickCH`, `checkCH`, `showCH`,
`resetCH`; result in `#<id>-result`.

**Model answers** — `.type-row > button[onclick=toggleNext(this)]` followed by
`.il-model[hidden]` holding `.play-row[data-say]` and `.model-text`; the play
button has `plays = 0` (no limit, toggles stop).

## The clock

One timer panel per page. `PRESETS = [[label, seconds, name], …]`, built into
`#timer-presets` as `.preset-btn`. `toggleTimer()` handles start, pause, resume
and again; `resetTimer()`; it shows a warning colour in the last 20%, "Time" at
zero, and plays a WebAudio beep (`#mute-btn` toggles it). Keep presets to the
real limits for the tasks on that page.

- Lesson 1: the panel sits directly in stage 3's sidebar.
- Lesson 2 on: the panel lives in `#timer-home[hidden]`, and each practice
  stage's sidebar has an empty `<div class="timer-slot"></div>`. `goTo()` moves
  the panel there, so it keeps running across stages.

## Adding CSS

Put new rules in a `/* ---- Class N additions ---- */` block at the end of the
`<style>`, with their own `@media (max-width: 720px)` rule for any new grid.
Use the existing tokens (`--accent`, `--accent2`, `--bg`, `--surface`,
`--border`, `--muted`, `--accent-light`).

## Registering

`Antonio/lessons.js` → append to the `LESSONS` array (`window.LESSONS_BY_STUDENT.Antonio`). `index.html` and the teacher home page both load this file, so the list lives only here:

```js
{
  file: "lesson_plan_N.html",
  title: "Real Words & Missing Letters",
  date: "29 October 2026",
  desc: "One line on what the class covers.",
},
```

Cards are numbered by position. `soon: true` shows a card without a link;
`paid: true` adds the green corner.

### Exam calendar on the index

Above the lesson cards: `.cal` (7-column grid, Monday to Sunday) built by
`buildCalendar()` from `EXAM` and `SCHEDULE = [[date, title], …]`. Class days
are `.cal-day.class` (`.done` once past, `<a>` when the lesson exists), the exam
is `.cal-day.exam`, today has `.today`. `#cal-countdown` shows the days and
classes left. Titles hide below 720px.
