---
name: raffa-class-prep
description: Prepare or edit an English lesson page for Raffa (Raffaele), Felipe's upper-intermediate (B2+) student, whose material lives in Raffa/ in the EnglishClasses repo. Use this when the user names Raffa or Raffaele, or points at a file under Raffa/ — including openers like "let's do Raffa's class six" or "what should Raffa cover next". Covers picking a topic, the vocabulary-first rule, the page template and house style, and the shared-screen language rules. Do NOT use this for Peterson, who is a beginner on a separate track with its own skill (peterson-class-prep), and do NOT use it for an unnamed student — if the request does not say which student, ask before loading either skill.
---

# Raffa's class prep

## This skill is for Raffa only

Felipe teaches two students, on deliberately different tracks:

| | Raffa (Raffaele) | Peterson |
|---|---|---|
| Level | Upper-intermediate, B2+ | Beginner, level still being diagnosed |
| Folder | `Raffa/` | `Peterson/` |
| Skill | this one | `peterson-class-prep` |
| The job | range — vocabulary he would not reach for | the core — grammar and high-frequency language |
| Items per lesson | 60–80 | far fewer, drilled far harder |
| Portuguese on the page | not needed | forbidden; Felipe translates out loud |

**Everything below applies to Raffa and misleads on Peterson.** The
vocabulary-first rule, the 60–80 item target and "could he already do this in
Portuguese? then cut it" are all calibrated for a fluent adult who needs range.
A beginner needs the opposite, and grammar *is* his lesson.

What the two tracks genuinely share is the page template, the design tokens, the
brand and the shared-screen rules. Those are worth copying across. The pedagogy
is not.

If a request does not name the student — "let's do the next class", "add a
lesson" — **ask which one** rather than guessing. The two pages look alike and
the mistake is not obvious until the class is underway.

## The student

Raffaele — "Raffa". Brazilian, first language Portuguese. Upper-intermediate,
roughly B2+: fluent, confident, makes himself understood easily. A working
business professional who deals with clients, vendors and a team, and travels
for work a few times a year. Classes are one-to-one, conversational, roughly
weekly.

His problem is not grammar and it is not confidence. It is **range**. He can say
almost anything with the English he already has, which means he never has to
reach for anything new. Every lesson exists to put words in front of him that he
would not have reached for on his own, and then force him to say them out loud.

Lesson material lives in `Raffa/lesson_plan_N.html`, one self-contained HTML page
per class, listed on the class library at `Raffa/index.html`.

## What this class is — and what it is not

**Felipe is Raffa's English teacher.** He is not a public-speaking coach, a
storytelling coach, a negotiation trainer or a presentation consultant. This is
the single most important thing to get right, and it is the mistake that keeps
recurring, because lesson topics like "Presentations" or "Storytelling" pull hard
toward teaching the *skill* instead of the *language*.

The test, applied to every block on the page:

> **Could Raffa already do this in Portuguese?**
> If yes, it is not your lesson. Cut it.

He is a fluent adult. He already knows that a story needs a turn, that a pitch
needs an ask, that you should not explain why a joke was funny. Teaching him that
is condescending and it burns class time he needs for English. What he lacks is
the *English* to execute what he already knows how to do.

| Craft — cut it | English — teach it |
|---|---|
| "Set the scene in one sentence" | `this` + noun to introduce someone: *"there's this guy who…"* |
| "Switch to the present tense at the peak for drama" | `goes` / `is like` as informal reported speech, which happens to stay present |
| "Land the punchline and stop" | *long story short* · *and that was that* as fixed expressions |
| "Three concrete details beat one adjective" | ungradable adjectives: *absolutely freezing*, *completely exhausted* |
| "Signpost the turn so the listener leans in" | *out of the blue* · *next thing I know* · *and then it got weird* |
| A scorecard ticking "signalled the turn ✓" | a table of expressions with a sentence to read aloud |

Same content area, completely different lesson. The right-hand column is the job.

**The topic is a container, not the subject.** "Storytelling" is a good topic
because anecdotes are stuffed with phrasal verbs, informal reported speech and
reaction language — not because Raffa needs to become a better storyteller. Pick
topics for the vocabulary they carry.

**Activities are machines for producing speech, not lessons in themselves.** A
prompt deck, a timer, a set of interruptions — these are good because they force
him to talk under mild pressure. They are not good because they teach technique.
Every activity should have target language attached to it.

Aim for **60–80 discrete language items** per lesson: expressions, idioms,
phrasal verbs, collocations, fixed chunks. That is the deliverable.

## He can see the screen

Felipe shares his screen with Raffa during class. **Nothing on the page may refer
to him in the third person.** Reading "he'll recognise all of them and use about
three" while sitting next to the person who wrote it is a bad experience, and it
turns the page into something done *to* him rather than *with* him.

- Address him directly: "You get 90 seconds", "What got thrown at you".
- For instructions genuinely aimed at Felipe, use a neutral passive: "Each
  reaction gets clicked the moment it's used" — not "click it when he says it".
- `he`/`him` inside example sentences is fine — *"And he goes, 'I'm not doing
  that'"* is about a character in a story, not about Raffa.

Same reasoning applies to anything that reads as scoring him. Avoid live
assessment widgets — a grid of checkboxes ticked while he talks reads as a report
card, and in practice nobody can operate one mid-activity anyway.

## How a lesson gets made

**1. Propose topics before building anything.** Felipe chooses the topic; do not
assume one. Offer three or four options with genuinely different vocabulary
payloads, and say what language each one would carry. Check
`references/lesson-log.md` first so you do not repeat a topic or re-teach the same
expressions. Note whether he wants business or non-business — the early lessons
were all work-shaped and he has since asked for material outside the office.

**2. Confirm the shape.** Ask what the main activity should be if it is not
obvious. Roleplays with hidden briefs and custom interactive widgets have both
worked; a plain vocabulary lesson with a timer is also fine.

**3. Build the page.** Copy the most recent `lesson_plan_N.html` — it carries the
fullest CSS, and the house style is deliberately copy-forwarded rather than shared
between files. Replace the content. See `references/page-anatomy.md` for the
template, the component class names and the JavaScript contract.

**4. Register it** in the `LESSONS` array in `Raffa/index.html`.

**5. Verify it in a browser** before saying it is done. See the checklist below.

## What a lesson page contains

Four stages, in this order. The nav sidebar, progress bar and Previous/Next
buttons are driven by a small script — `references/page-anatomy.md` has the
details.

1. **Warm-up** — four or five discussion questions in a `.q-list`. No teaching
   yet; this is where he talks and you hear what is missing.
2. **The toolkit** — the actual lesson. Vocabulary tables, idiom/phrasal-verb
   grids, chip banks of fixed expressions. This is the biggest stage and should
   carry most of the 60–80 items.
3. **The activity** — the machine that forces production. Prompts, a clock,
   interruptions, roleplays. Points back at the stage 2 language.
4. **Wrap-up** — recall, not reflection. "Close the page, how many can you say
   from memory?" beats "what did you learn today?". Plus homework: a voice note,
   and something to listen to.

### Vocabulary tables

Three columns, and the third one matters:

| Correct, but textbook | What's actually said | Read it out loud |
|---|---|---|
| "He asked me many times." | He kept asking me. | *She kept looking at her phone while I was talking, and the waiter kept walking past without stopping.* |

Column three is **a sentence for Raffa to say**, not an explanation of why the
phrase works. A rule he reads is inert; a sentence he says is a rep. Build each
one so the target pattern appears two or three times, so one reading gets him
several reps. Set them in `<em>` so they read as speech.

## House rules, learned the hard way

- **`.apply-steps li` is a flex container.** An inline `<em>`, `<strong>` or `<a>`
  inside one becomes its own flex item and shreds the sentence into columns. Keep
  those list items plain text. `.q-list li` is a normal list item and is fine.
- **Time the right interval.** A drill that starts a 3-second clock on a button
  click fails, because reading the prompt aloud eats the three seconds. If a
  constraint can be enforced socially ("don't take too long"), prefer that over a
  timer. Scarcity — "you can't use the same reaction twice" — is usually a better
  constraint than a clock anyway.
- **Numbering matches the file name.** `lesson_plan_4.html` is titled "Lesson 4",
  in both the `<title>` and the header subtitle, and shows as "Lesson 4" on the
  library, where cards are labelled by array index. The two used to be off by one;
  that was corrected on 12 September 2026. So `lesson_plan_N.html` is "Lesson N"
  — the only exception is `lesson_plan_0.html`, whose header still reads
  "Experimental Lesson" rather than carrying a number at all.
- **Felipe edits these files directly between sessions.** If a count or a phrase
  does not match what was last written, that is him, not corruption. Read the
  current file and build on it. Never restore something back to a previous version
  without asking.
- **Homework alternates** speaking (a voice note sent to Felipe) and listening (a
  talk or podcast episode). Keep it to two or three items.

## Before you finish

Open the page in a browser and check:

- All four stages navigate; progress bar, step counter and "Last stage" label work.
- Every interactive control does what it claims: decks draw without repeating
  until exhausted, resets actually clear state, toggles toggle both ways.
- No console errors.
- At 375px wide: grids collapse to one column, tables stack into cards, and there
  is no horizontal scroll.
- Grep the page for `\bhe\b`, `\bhim\b`, `\bhis\b` and confirm every hit is inside
  an example sentence.
- Count the language items. If it is under about 50, the lesson is thin — add
  vocabulary before shipping it.

## References

- `references/page-anatomy.md` — the HTML template, component class names, the
  navigation script contract, registration in the library, and mobile behaviour.
  Read this before building or editing a page.
- `references/lesson-log.md` — what has already been taught, lesson by lesson,
  with the specific expressions. Read this before proposing a topic, both to avoid
  repeats and to recycle a few old items into the new warm-up.
