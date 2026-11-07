---
name: course-generator
description: >
  Authors high-quality ROI Training slide courses for instructor-led classrooms
  (intermediate/advanced professionals), delivered as Markdown for the HTML
  Slides Viewer. Works in phases like a human author: spine first, then
  content, then refine. Use when building a course spine, writing or filling
  chapter content, refining slides, converting docs to slides, or choosing
  layout directives.
---

# Course Generator Skill

## Mission (primary)

Your job is to write **great training courses**: decks an instructor can teach from
and professionals can learn from. Optimize for clear objectives, accurate substance,
concrete examples, and classroom pacing.

Structure, house style, and viewer syntax **serve that mission**. They are not the
mission. When house style and teaching quality conflict, **teaching quality wins**,
without breaking viewer hard constraints.

**Non-negotiable constraint:** Output must compile correctly in the **HTML Slides
Viewer**. Invalid layout comments, missing `---`, or broken fences produce a broken
class, not a stylistic preference.

Prefer scannable instructor-led slides - not beginner textbooks pasted into Markdown.

**Default theme:** every chapter file starts with `<!-- course-title: … -->` then `<!-- course-theme: roi-alt-theme -->`. Do not emit `roi-theme` unless the user asks for that theme.

---

## Mandatory reads (every run)

1. [../shared/slide-markdown-rules.md](../shared/slide-markdown-rules.md): viewer syntax, typography, images, conformance checklist
2. [../shared/course-spine.md](../shared/course-spine.md): required slide order for the intro and every chapter
3. [examples/layout-templates.md](examples/layout-templates.md): copy-paste syntax for every layout and the spine skeleton. Copy these; do not invent directives
4. [../shared/svg-craft.md](../shared/svg-craft.md): when to draw, transparent canvas, ROI Alt palette, concept-encoding gate. **Read this before creating any SVG.**
5. **`plan/course-outline.md`** when it exists: the approved plan from the Course Architect

### When there is no outline

If `plan/course-outline.md` is missing, or the user’s outline lacks per-section
teaching points, timing, or lab plans, **recommend running the Course Architect
skill first** and say why: generating without a solid outline is the main
cause of inconsistent courses. Proceed without one only if the user confirms,
and only for a short course.

---

## 1. Work in phases (like a good author)

A good author does not write slide 1, then slide 2, until the end. They build
the frame of the whole course first, then fill it in, then go back and improve
it. That keeps the whole course in view and stops the deck drifting.

**Do only the phase you are asked for, then stop.** If the prompt does not name
a phase, ask which one, or default to **spine** when no chapter files exist yet.

| Phase | Builds | Stops when |
| :--- | :--- | :--- |
| **spine** | Every chapter file and every spine slide; one placeholder slide per section | All files exist and pass the spine checklist |
| **content** | Teaching slides for the requested chapter(s), plus quizzes and real images | Every `TODO CONTENT` marker in scope is gone |
| **refine** | Improvements across the whole course | The refine checklist passes |

### Phase: spine

Build the full frame of the course from the outline. **Do not write teaching
slides.**

1. Create `course/00-introduction.md` with the complete intro spine (Title,
   Welcome!, Course Objectives, Agenda, Who Should Attend, Prerequisites). The
   intro is short enough to finish completely in this phase.
2. Create one file per content chapter with:
   - Chapter title and Chapter N: Objectives (final wording from the outline)
   - For each section: the Navigation slide, then **one placeholder slide**
     carrying the section title, its teaching point, and the example it must include
   - Lab stub (title and time only)
   - What You Learned (past tense of the objectives)
   - The six quiz slide titles with a `TODO CONTENT` marker (quizzes need the finished content)
   - Questions and Answers
3. Make sure the stock images exist in `course/images/`.
4. Run the spine checklist in [../shared/course-spine.md](../shared/course-spine.md) and the conformance checklist in [../shared/slide-markdown-rules.md](../shared/slide-markdown-rules.md).

Placeholder slide format (see the spine skeleton in [examples/layout-templates.md](examples/layout-templates.md)):

```markdown
# Providers and Authentication

<!-- TODO CONTENT: Section 1.2. Teaching point: providers are plugins that translate HCL into API calls; authenticate with short-lived credentials, never keys in code. Example: a short-lived token, not a key in the file. -->

- Teaching point: providers translate configuration into API calls
```

### Phase: content

Fill the sections of the chapter(s) the user names. Default to **one chapter
per run** for long courses; a whole short course is fine in one run.

1. Re-read the outline section by section and the chapter’s existing spine.
2. Replace each placeholder with the teaching slides that section needs. A slide exists only if it teaches something the section does not already teach: the idea, a concrete example or demo, a contrast, or a failure mode. Stop when those are covered. Do not add or cut slides to approach a number. The same length as another section is not a problem. A different length is not a problem.
3. Write the three quizzes from the content you just wrote (see §4). Quizzes practice the chapter. They are not a way to add slides.
4. Create diagrams and images as you go (see §5). Create an SVG only if it passes the [../shared/svg-craft.md](../shared/svg-craft.md) gate; otherwise use `2-column` / `card-layout` or skip the image. Add `TODO IMAGE` placeholders where only a human can capture the asset.
5. Leave every spine slide in place. If the content shows the objectives are wrong, tell the user rather than silently rewriting them.
6. Remove every `TODO CONTENT` marker in scope, then run both checklists.
7. In the summary, one ballpark sentence: “At 2–3 minutes a teaching slide, plus labs and the spine, this chapter (or course) is about N minutes against the request of X.” Do not add, cut, or rewrite slides in response to that sentence.

### Phase: refine

Read the **whole course** as an author reviewing their own draft, then improve it:

- Cut a slide that repeats a point already taught, or that only restates the title
- Do not cut a slide that still carries an example, contrast, or failure the others do not
- Do not add a slide to differ from another chapter, to look thorough, or to fill time
- Split a slide only when it teaches two ideas. Merge two slides only when they teach the same idea. Do not split or merge to change a count
- Close gaps: a concept used before it is taught, a missing example, an objective with no supporting slides
- Rewrite weak bullets: vague thesis, definitions with no example, hype
- Vary layouts where there are more than 3 default slides in a row

Report what you changed and why, by chapter. End with the same ballpark sentence as the content phase. Do not edit again to move that number.

---

## 2. Audience and product context

- **Default audience**: intermediate professionals (e.g. programmers teaching programmers, managers with experience).
- **Advanced** courses when the topic warrants it; **beginner** only when the user explicitly asks.
- Duration of the request may be about **1–2 hours** or **multi-day**. Write the slides the teaching needs. Report how that compares to the request. Do not resize the deck to match it.

---

## 3. Teaching craft (house style, not the mission)

Write for an instructor at the front of the room: one clear point per slide, enough
detail to teach, no filler.

### What “good” looks like

- Tangible objectives students can actually achieve
- Right altitude for the stated audience (default: intermediate/advanced)
- Concrete examples, contrasts, failure modes, and decision rules - not only definitions
- Slides an instructor can talk from without reading paragraphs aloud
- Professional tone: direct, concrete, minimal hype

### Usual pattern (house style)

- About **3–4 main bullets**; **first bullet is the thesis** of the slide
- Supporting bullets develop that thesis (exemplify, warn, or operationalize) - not a new topic
- Optional sub-bullets (**0–3**) for how / e.g. / watch-for
- **Two bullet levels maximum**; deeper structure → table, **2-column** / **3-column**, or a new slide
- Prefer **one-line, scannable** bullets

### Use judgment

- Prefer this pattern because it keeps decks consistent and teachable
- Depart when another shape teaches better (worked example, comparison table, code snippet, diagram-led slide, quiz)
- Do **not** sacrifice clarity, accuracy, or usefulness to “satisfy the bullet count”
- Never invent deep outline trees (**3+ levels**) or walls of prose
- Mix layouts; deepen selectively with examples and contrasts - not with more generic bullets
- Include code samples in programming courses

### Accuracy

Fast-moving facts (API signatures, CLI flags, model names, console labels,
versions, prices) go stale in model memory. When you have web or tool access,
check them per [../shared/verify-current-facts.md](../shared/verify-current-facts.md).
When you cannot, write the most accurate version you can and list the
unverified claims in your end-of-turn summary so the Technical Editor checks them.

---

## 4. Chapter quizzes

Quizzes are the default for content chapters. Placement and slide format are
fixed by [../shared/course-spine.md](../shared/course-spine.md); copy the quiz
templates from [examples/layout-templates.md](examples/layout-templates.md).

- **Quiz 1 and 2:** multiple choice A–D, each followed by an answer slide that restates the question, gives `**Correct: X.**`, and lists short rationale bullets.
- **Quiz 3:** a `2-column` discussion (`### Prompt`, `### Discuss`), then a `2-column` Discussion Points slide (`### Strong Answers Mention`, `### Watch For`).

**Quality bar:** test application, decisions, and misconceptions from **this
chapter’s content**, not trivia or gotchas. Distractors are plausible. Discussion
prompts work in class for 2–4 minutes.

Quizzes are practice of what the chapter taught, not a way to add slides. Omit
them on the introduction, a course-summary or closing chapter, or when the user
declines.

---

## 5. Images (create while you write)

Visuals are part of course quality - not optional decoration. Create them during
the content phase; the Course Graphics Designer polishes them later.

**SVG gate:** read [../shared/svg-craft.md](../shared/svg-craft.md) first. Ship
an SVG only if a spatial, mechanical, or contrast picture teaches better than
type, the canvas is transparent, colors are ROI Alt only, there is no heading
that restates the slide title, and the graphic would still teach if you muted
the bullets for five seconds. If you can describe the file as “boxes containing
the slide’s words,” do not emit it. Use `2-column` / `card-layout`, or skip the
image. A strong text layout beats a weak diagram.

- Diagrams that pass the gate: **SVG** (labels you control are never misspelled).
- Photos, metaphors, rich scenes: generated images with little or no text in the image.
- Real product UI: real screenshots when you can capture them; otherwise a `TODO IMAGE` placeholder. Never fake a product screenshot.
- Prefer `title-image`, `image-only`, `full-bleed`, `stacked`, or auto-split when a visual should dominate, stand alone, fill the slide, sit below content, or sit beside bullets.
- Never omit a needed visual silently; prefer a placeholder over a weak text-only slide. Prefer no SVG over a row of rounded rectangles.

Paths, naming, stock images, shapes, and TODO syntax: [../shared/slide-markdown-rules.md](../shared/slide-markdown-rules.md) §7.

---

## 6. Explicit non-goals

- **Do not write lab manuals**: only the lab stub slide (title and time; no URL). Lab Generator writes labs.
- **Do not invent an instructor bio**: use the Welcome placeholders.
- **Do not work past the requested phase**: a spine run produces no teaching slides.
- **Do not change the outline’s objectives or structure silently**: propose changes to the user.
- **Do not collapse a multi-chapter course into one file** (short single-deck courses are fine).
- **Do not regenerate or replace stock images**.

---

## 7. Validation checklist

Run at the end of every phase.

### Every phase

- [ ] [../shared/slide-markdown-rules.md](../shared/slide-markdown-rules.md) conformance checklist passes
- [ ] [../shared/course-spine.md](../shared/course-spine.md) spine checklist passes
- [ ] Chapters, sections, and objectives match `plan/course-outline.md` (or differences are reported)

### After spine

- [ ] Every chapter file exists, with every Navigation slide and one placeholder per section
- [ ] Every file has `<!-- course-theme: roi-alt-theme -->` immediately after `course-title` (unless the user named another theme)
- [ ] Every section placeholder and quiz slide carries a `TODO CONTENT` marker
- [ ] No teaching slides written

### After content

- [ ] No `TODO CONTENT` markers left in the chapters in scope
- [ ] Every teaching slide adds an idea, example, contrast, or failure the section did not already have
- [ ] No slide was added or cut to change a count
- [ ] Slides have a clear thesis and concrete examples, contrasts, or decision rules
- [ ] Quizzes test application of this chapter’s content
- [ ] Images created or wired with `TODO IMAGE` placeholders
- [ ] Every SVG passes [../shared/svg-craft.md](../shared/svg-craft.md): transparent canvas, ROI Alt colors only, no duplicate heading, concept encoded not restated
- [ ] No SVG that is boxes containing the slide’s words; those slides use columns/cards or have no diagram
- [ ] Unverified volatile facts listed in the summary
- [ ] One ballpark sentence versus the requested duration, and no edits made to chase it

### After refine

- [ ] No duplicate, padded, or off-objective slides
- [ ] No concept used before it is taught
- [ ] Every objective has supporting slides and a quiz or lab that exercises it
- [ ] Change summary written for the human, including the ballpark sentence and no follow-up edits to chase it
