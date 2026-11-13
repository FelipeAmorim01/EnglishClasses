---
name: antonio-class-prep
description: Prepare or edit a Duolingo English Test (DET) prep lesson page for Antonio, Felipe's exam-prep student, whose material lives in Antonio/ in the EnglishClasses repo. Use this when the user names Antonio, mentions the Duolingo English Test or DET prep, or points at a file under Antonio/ — including openers like "let's do Antonio's next class" or "what's next for the Duolingo prep". Covers his score target, the course outline's class order, the task-based page shape, the timed drills and their answer keys, and house style. Do NOT use this for Peterson (beginner, peterson-class-prep) or Raffa (upper-intermediate conversation, raffa-class-prep), and do NOT use it for an unnamed student — if the request does not say which student, ask first.
---

# Antonio's class prep

## This skill is for Antonio only

Felipe teaches three students, on deliberately different tracks:

| | Antonio | Raffa (Raffaele) | Peterson |
|---|---|---|---|
| Goal | Pass the Duolingo English Test | Range in conversation | Core grammar and everyday English |
| Folder | `Antonio/` | `Raffa/` | `Peterson/` |
| Skill | this one | `raffa-class-prep` | `peterson-class-prep` |
| A lesson is built around | **exam task types** | a topic carrying vocabulary | a grammar structure |
| Timers | yes, the real exam time limits | sparingly | never |

**Do not carry the other skills' content rules over.** Raffa's 60–80 item
target, Peterson's four-block limit, no-timer rule and Language Tip box are
calibrated for their tracks. On this one the unit of a lesson is a DET task
(Read and Select, Interactive Writing, …): a strategy for it, then timed
practice of it. What the tracks share is the page template, the design tokens
and the shared-screen rules.

If a request does not name the student, **ask which one** before building.

## The student and the goal

Antonio started in October 2026. He is preparing for the **Duolingo English
Test**, set for **Friday 27 November 2026** (moved from 1 December; it may still move). Classes are
**every Tuesday and Thursday**. Antonio cancelled 29 October, so Class 2 moved
to 3 November and **only 9 classes fit** before the exam. Following the
outline's "exam moves earlier" plan, **Classes 7 and 8 are merged** into one
(Interactive Speaking & Writing Sample, 19 November). The table below shows the
current plan; the outline file still shows the original 10.

`Antonio/index.html` shows a calendar of this ("Your road to the exam"). It
reads `EXAM`, `SCHEDULE` and `CANCELLED` in its script: if the date or a
class day moves, update those, and the countdown and done marks update themselves. Each
class links to its lesson once the lesson is in `LESSONS` (`Antonio/lessons.js`).

- His college needs **110** overall.
- He scored **110–120** on the free official practice test and has never taken
  the real exam.
- The course aims for **120+**, so a bad day on the real exam still clears 110.

Still unknown, worth asking about when relevant: subscore minimums and the
college's deadline.

His English is already around the target level, so the job is not general
English. It is **exam technique, accuracy and speed**: knowing every task type,
using all the time, spelling exactly, and having ready-made frames so he never
freezes.

## The course outline is the plan

`Antonio/course_outline.html` holds a 10-class, 5-week plan (Tuesdays and Thursdays).
It is **git-ignored and stays local** — never commit it, and read it from disk
before planning. **Follow its class order**; don't propose topics the way the
Raffa skill does. Check `references/lesson-log.md` for which class is next and
what was actually covered, since a lesson can run short or change.

| Class | Date | Focus | Tasks |
|---|---|---|---|
| 1 | Oct 27 | Diagnostic & test tour | all task types |
| — | Oct 29 | *cancelled* | |
| 2 | Nov 3 | Real words & missing letters | Read and Select, Read and Complete |
| 3 | Nov 5 | Reading strategies | Fill in the Blanks, Interactive Reading |
| 4 | Nov 10 | Listening accuracy | Listen and Type, Interactive Listening |
| 5 | Nov 12 | Speaking: photos & prompts | Speak About the Photo, Read/Listen Then Speak |
| 6 | Nov 17 | Writing: sentences that score | Write About the Photo, Interactive Writing |
| 7 | Nov 19 | Interactive Speaking & Writing Sample (outline 7 + 8) | Interactive Speaking, Speaking Sample, Writing Sample, summaries |
| 8 | Nov 24 | Full mock, exam conditions (outline 9) | full test |
| 9 | Nov 26 | Weak spots & test day (outline 10) | weakest tasks, rules & setup |
| Exam | Nov 27 (Fri) | Duolingo English Test | |

The outline also has a plan for the exam moving earlier or later (section 4)
and the **toolkit frames** (section 5: photo frame, opinion frame, phrases to
buy time, linking words). Reuse the toolkit wording exactly on lesson pages,
so Antonio sees the same frames every time.

If the date or the plan changes, update the outline and say so, not only the
lesson page.

## Rules that govern the content

### No full practice tests in class

Felipe doesn't want class time spent watching Antonio take full practice tests.
Those are **homework**, taken like the real thing, with the score sent to
Felipe. Class time is for strategy and **short timed samples** of the real
tasks. (Class 9's mock is the exception the outline already plans.)

### Use the real time limits

The exam is timed per task, so drills use the **real limits** from the outline's
task table (Read and Select 1:00, Read and Complete 3:00, speaking 20 s prep +
up to 1:30, Interactive Speaking 35 s per answer, and so on). Every practice
stage has the shared clock in its sidebar with presets for that stage's tasks.

### Make the drills look like the real task

Antonio types on the real test, so typed tasks are typed on the page too: he
opens it on his own computer for those parts. Mirror the real format: a word
grid for Read and Select, half-words with letter-sized boxes for Read and
Complete, hidden questions for Interactive Speaking (they are only heard on the
test). Turn off autocorrect and spellcheck on every input
(`spellcheck="false"`, `autocomplete="off"`, `autocapitalize="off"`). There is
no autocorrect on test day.

### Answer keys must be right

A drill with a wrong key teaches the wrong thing, and on an exam-prep page it
also damages trust. Before shipping:

- **Fake words must be fake.** Check that each one is not a real word, including
  rare or archaic ones (*mundify* and *obtention* are real, so they were avoided).
  If in doubt, swap it for a clearer fake.
- **Real words must not have common variant spellings** in typed answers
  (*center/centre*, *color/colour*). Pick a word without one, or accept both.
- **Read and Complete gaps must have one answer** given the visible letters, the
  box length and the sentence. The C-test convention: show the first
  `floor(n/2)` letters, hide the rest; keep the first and last sentences whole;
  cut roughly every other word.
- Fill every set with its own answers in the browser and confirm it scores full
  marks (see the checklist below).

### Strategy is short; practice is most of the class

Each task stage opens with a compact strategy block (idiom cards, a three-step
`.apply-box`, a clue table) and then gives most of its space to timed practice.
Strategy that doesn't change how he answers the task is not worth a slot.

### He can see the screen

Felipe shares his screen, and Antonio also opens the page himself. **Address him
directly** ("You get one minute", "Click every real word"). Nothing on the page
refers to Antonio in the third person; for instructions aimed at Felipe, use a
neutral passive. Don't add pacing badges or score-report widgets that grade him
live. A drill's own `Check` result (*12 / 16 correct*) is fine, since that is how
he practises.

### State facts about the exam carefully

The DET format changes (Interactive Speaking was added in mid-2025, Read Aloud
was reportedly removed). Don't state a format detail, rule or score fact as
certain unless it is in the outline or checked against the official DET site.
Hedge where needed ("These are the usual rules. Check the official page before
you book."). If a lesson turns up a difference, update the outline's task table.

## How a lesson gets made

1. **Read the outline and the log.** Find the next class number and its focus,
   tasks and homework. Check the log for anything carried over or changed.
2. **Build the page.** Copy the most recent `Antonio/lesson_plan_N.html`: it
   carries the fullest CSS, and the house style is copied forward rather than
   shared between files. Update the `<title>` (`DET Prep — Class N`) and the
   header subtitle (`<Class title> — Class N`). See
   `references/page-anatomy.md`.
3. **Register it** in the `LESSONS` array in `Antonio/lessons.js` (not in `index.html`): file, title,
   date (the class day, e.g. "29 October 2026"), one-line desc.
4. **Verify it in a browser** (the `lessons` launch config serves the repo on
   port 8765). See the checklist below.
5. **Update `references/lesson-log.md`** with the new lesson.

## What a lesson page contains

Five or six stages:

1. **Warm-up.** A `.q-list` of about four questions, always covering the
   homework: the latest practice-test score and hardest tasks, the word list,
   the writing sprints or recordings.
2. **One stage per task (or pair of tasks)** from the outline. Each has a short
   strategy block, then `.task-block` drills inside a `.negotiation-layout`
   with the clock and chip banks in the `.language-sidebar`. Drills are lettered
   A, B, C… across the whole page.
3. **(Optional) a supporting stage** for the skill behind the task, e.g. Class
   2's spelling traps.
4. **Extra practice (reserve).** Felipe found that a page's drills don't fill
   60 minutes (29 October 2026), so every lesson has a reserve stage just
   before the wrap-up: more timed rounds of the day's tasks, one task where
   Antonio produces something (e.g. invents fake words for Felipe to spot), and
   a live 5-minute writing sprint. It's used only if there's time, so the
   homework never depends on it.
5. **Wrap-up.** Only "Before next class" in a `.reflection-grid`: the
   outline's homework for that class, plus the ongoing routines (word list,
   5-minute writing sprints with autocorrect off, recordings), each with a new
   twist or new prompts so it isn't the same list every class. **No "Out loud,
   now" recall questions:** Lesson 1 had them and Felipe cut them from Lesson 2
   on 29 October 2026 ("I don't like them").

## Before you finish

Open the page in a browser and check:

- Every stage navigates; progress bar, step counter and "Last stage" work.
- The clock appears in each practice stage's sidebar, with that stage's presets.
- Every drill's Check, Show answers and Reset work. **Fill each answer set with
  its own key via JS and confirm full marks.** Read every fake word and gap
  answer once more.
- No console errors.
- At 375px wide: grids collapse, tables stack, no horizontal scroll.
- Grep for `\bhe\b`, `\bhim\b`, `\bhis\b`, `Antonio`: every hit is inside an
  example sentence, not about him.
- The new lesson shows on `Antonio/index.html`.
- `course_outline.html` is not staged if you commit.

## References

- `references/page-anatomy.md`: page skeleton, component classes, the drill
  widgets and their JS, the shared clock, registration.
- `references/lesson-log.md`: what each class covered, homework set, and
  anything carried over. Read before building the next one.
