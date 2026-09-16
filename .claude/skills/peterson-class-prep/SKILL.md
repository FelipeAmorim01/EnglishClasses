---
name: peterson-class-prep
description: Prepare or edit an English lesson page for Peterson, Felipe's beginner student, whose material lives in Peterson/ in the EnglishClasses repo. Use this when the user names Peterson, or points at a file under Peterson/ — including openers like "let's do Peterson's next class" or "what should Peterson cover next". Covers his level, the English-only rule, who says each item out loud, the page template and house style. Do NOT use this for Raffa (Raffaele), who is upper-intermediate on a separate track with its own skill (raffa-class-prep), and do NOT use it for an unnamed student — if the request does not say which student, ask before loading either skill.
---

# Peterson's class prep

## This skill is for Peterson only

Felipe teaches two students, on deliberately different tracks:

| | Peterson | Raffa (Raffaele) |
|---|---|---|
| Level | False beginner — solid basics, thin vocabulary | Upper-intermediate, B2+ |
| Folder | `Peterson/` | `Raffa/` |
| Skill | this one | `raffa-class-prep` |
| The job | the core — grammar and high-frequency language | range — vocabulary he would not reach for |
| Portuguese on the page | forbidden | not needed |

**Do not apply the Raffa skill's content rules here.** Its 60–80 item target, its
vocabulary-over-grammar rule and its "could he already do this in Portuguese?
then cut it" test are calibrated for a fluent adult. On this track they are
actively wrong: Peterson needs fewer items drilled far harder, and grammar *is*
the lesson. That holds even though his own gap is vocabulary — the difference is
that here vocabulary rides in **on the back of a structure** (false-friend fix
cards, sequencing words, collocations hung off the grammar being taught) rather
than arriving as a list.

What the tracks genuinely share is the page template, the design tokens, the
brand, and the shared-screen rules. Copy those across freely.

If a request does not name the student, **ask which one** before building
anything.

## The student

Peterson. Brazilian, first language Portuguese. Classes are one-to-one, 60
minutes, roughly weekly. He wants English for work and for everyday life; not
for an exam, not primarily for travel.

**A false beginner — diagnosed 15 September 2026.** Felipe's read: *"he can
speak the basics well, but doesn't have a very sophisticated vocabulary."* The
core grammar is there and it comes out. The gap is range. So pitch at one level
rather than hedging across three, and do not spend a block re-drilling something
he already says correctly. He reached five toolkit blocks in his first hour —
that is the pace to plan for.

Lesson material lives in `Peterson/lesson_plan_N.html`, one self-contained HTML
page per class, listed on the class library at `Peterson/index.html`.

**Check `references/lesson-log.md` before proposing anything** — it holds what
has been taught, what carried over, and what was cut from each page and why.

## The rules that govern the content

### English-only pages

Felipe's choice: **no Portuguese anywhere on the page.** He translates out loud
when it is needed. This has two consequences worth planning for.

First, Portuguese-speaker errors get taught as **struck-through wrong / right
pairs** (`.fix-card`) rather than translation columns — the error form is shown
and crossed out, so the trap is named without naming the language:

> ✗ I have thirty-four years. → ✓ I'm thirty-four.

Second, an English-only class with a beginner only works if *Sorry, I don't
understand* · *Can you say that again?* · *How do you spell that?* come out
automatically instead of silence. They were taught as a full block in lesson 0
and that is enough — **do not re-teach them as a block on later pages.** Felipe
cut exactly that from lesson 1. They belong in the activity stage's
`.language-sidebar` under *If you get stuck*, where he can reach them
mid-conversation, which is the only moment he actually needs them.

### Say who speaks every single item

This is the rule most easily forgotten, and Felipe asked about it directly. A
beginner cannot decode English spelling, so anything he reads cold comes out in
Portuguese phonetics — and that pronunciation is what sticks. The conventions
are fixed:

| | |
|---|---|
| **Boxed words** (chips) | Felipe says it first, Peterson says it back — twice. The box is to look at while speaking, not to read cold. |
| **Italic sentences** (vocab table column 3, the ladder) | Peterson reads them, after Felipe has read the first one in the table. |
| **Green ✓ lines** (`.fix-card`) | Peterson, twice each. |

**Every block states its own cue, in its own `.panel-note`.** A legend at the
top of the toolkit was built for lessons 0 and 1, and Felipe cut it: once every
block says who speaks, the legend is a second copy of the same instruction —
and the copy that is too far up the page to help mid-class. Cue the block, not
the page.

Irregular verbs and the three `-ed` endings (`worked`/`talked` → /t/, `called`
→ /d/, `wanted` → /ɪd/) are listen-and-repeat *only* — say so on the page.

### No pacing labels

Level and difficulty badges were built into lesson 0 and Felipe cut all of them:
*"I'll manage the time."* Do not reintroduce Start here / Next step / Stretch
tags, time estimates, or anything that paces the hour for him. A genuine
difficulty warning belongs in prose — a `.panel-note` — not a badge.

### No timers

A countdown on a beginner is cruel and it does not teach anything. Use scarcity
instead: a deck that does not repeat until it is exhausted does the same work
without the pressure.

### He can see the screen

Felipe shares his screen during class, so **nothing on the page may refer to
Peterson in the third person.** Address him directly — "You get a minute to
prepare", "Say your name, and spell it". For instructions genuinely aimed at
Felipe, use a neutral passive. `he`/`she` inside grammar examples is fine —
*"He's my manager"* is a sentence, not a reference to the student.

No live assessment widgets. Nothing that reads as a score.

## How a lesson gets made

**1. Check the log, then propose.** Read `references/lesson-log.md` for what has
been taught and what carried over. Blocks routinely carry over: pages are built
with more material than one hour reaches, on purpose. Propose the shape before
building.

**2. Build the page.** Copy the most recent `lesson_plan_N.html` — it carries the
fullest CSS, and the house style is deliberately copy-forwarded rather than
shared between files. See `references/page-anatomy.md`.

**3. Register it** in the `LESSONS` array in `Peterson/index.html`.

**4. Verify it in a browser** before saying it is done. See the checklist below.

## What a lesson page contains

Four stages. The nav sidebar, progress bar and Previous/Next buttons are driven
by a small script — `references/page-anatomy.md` has the contract.

1. **Warm-up** — a `.ladder` of five sentences, easiest first, each one a block
   from the toolkit below it, plus a phrase bank for the conversation the lesson
   exists to make possible. Not discussion questions: a beginner cannot hold a
   discussion yet.
2. **The toolkit** — the lesson. Numbered blocks, easiest first, each carrying
   its own cue saying who speaks, **closing with the Language Tip**.
3. **The activity** — a machine that forces production. The question deck and
   the transformation deck both work; see the anatomy file.
4. **Wrap-up** — recall with the page closed, then homework. **Not the ladder
   again.** Felipe cut that bookend from lesson 1 — *"too repetitive and doesn't
   add anything."* The five sentences appear once, in the warm-up.

### Every lesson closes its toolkit with a Language Tip

Felipe asked for this on every lesson going forward. It is `.rule-box`, the
recurring stage-2 closer from Raffa's pages — same component, same markup, so
copy it from the most recent lesson on either track. It goes **last in the
toolkit stage, after a `.divider`**.

One tip per lesson, holding **the single most important rule of that class** —
not a summary of the page. Lesson 1's is *was / were vs. did / didn't*, the rule
that blocks 1, 4 and 5 all depend on. Pick the thing that, got wrong, makes
everything else on the page come out wrong too.

The shape is fixed and each part does a job:

| Part | What goes in it |
|---|---|
| `.rule-title` | the two things being told apart, as a pair |
| `.rule-lead` | why the choice exists, and what it turns on |
| `.rule-split` | two `.rule-card`s, one per side, each with a `.rule-formula` (the shape, not a sentence) and three example lines |
| `.rule-trap` | the ✗ → ✓ pair he will actually get wrong, then *why* in prose |
| `.rule-say` | four sentences to say out loud, covering both sides |

**Raffa's version names the Portuguese** that causes the confusion — *"Portuguese
covers both directions with emprestar."* That is forbidden here. State the
English rule; Felipe says the Portuguese half out loud.

### A widget has to make him change something

The sentence builder generated a grammatical sentence for Peterson to read out
loud. Felipe cut it from lesson 1: *"too fancy for something that is just for
reading sentences."* However sound the grammar behind it, a machine that hands
him a finished sentence buys one reading rep and costs a screenful. If a widget
is not making him **change** something — a tense, a form, a direction — it is
not earning its place. Its replacement shows a finished sentence plus the job to
do to it, and **states that job on its face**: an instruction styled as a label
gets read as a heading and looked straight past, which is exactly what happened.

### Homework is one item

Felipe cut a three-item list down to one. Keep it to a single thing, with a
**verified** link — check the URL resolves before shipping it, because a
plausible-looking deep link is often a 404.

### Activities carry their own difficulty

An added-on rule strip ("now use a time word") was built and cut. Make the
prompt demanding on its own instead — two-part questions like *"What do you
like about your job, and what do you not like?"* do the same work without a
second mechanism.

## Before you finish

Open the page in a browser and check:

- All four stages navigate; progress bar, step counter and "Last stage" work.
- Every widget does what it claims: decks draw without repeating until
  exhausted, resets clear state, toggles toggle both ways.
- Drill output is not just well-formed but *checked* — read every card, in every
  mode. Hand-written decks beat generated ones for exactly this reason.
- No console errors.
- At 375px: grids collapse to one column, tables stack, no horizontal scroll.
  **A new grid needs its own mobile rule, and it must not be overridden by a
  later top-level declaration** — this bug has already happened once.
- Grep for `\bhe\b`, `\bhim\b`, `\bhis\b` and confirm every hit is a grammar
  example.
- Every block has a cue saying who says it out loud.
- The toolkit closes with a Language Tip, and it is about one rule, not the page.
- No Portuguese anywhere on the page.

## References

- `references/page-anatomy.md` — the HTML template, component class names, the
  navigation script, the widgets, registration, and mobile behaviour.
- `references/lesson-log.md` — what has been taught, what carried over, and what
  was cut from each page and why. Read before proposing a topic.
