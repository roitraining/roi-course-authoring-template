# Course Spine (Required Slide Order)

The spine is the set of slides every ROI course has, in a fixed order. It is
the frame the content hangs on. Course Architect plans it, Course Generator
builds it first, and every later skill must leave it intact.

Syntax for each slide: [../course-generator/examples/layout-templates.md](../course-generator/examples/layout-templates.md).
Formatting gates: [slide-markdown-rules.md](slide-markdown-rules.md).

---

## 1. Files

```text
course/
  00-introduction.md        # intro spine only
  01-short-chapter-slug.md  # one file per content chapter
  02-…
  images/
```

- Zero-padded index plus a short kebab-case slug.
- A short single-sitting course (about 1–2 hours) may be one file, such as `course.md`, holding the intro spine followed by one chapter.

---

## 2. Introduction (`00-introduction.md`)

| # | Slide | Layout | Notes |
| :--- | :--- | :--- | :--- |
| 1 | Title | `title` | ROI logo, course code and name, subtitle |
| 2 | Welcome! | `panel-right` | ROI positioning; instructor Name / Background / Contact info placeholders (never invent a bio); `images/welcome.png` |
| 3 | Course Objectives | default | 1 overall objective, then 1 per content chapter |
| 4 | Agenda | `panel-left` | Chapter list; `images/agenda.png` |
| 5 | Who Should Attend | `panel-right` | `images/who-should-attend.png` |
| 6 | Prerequisites | `panel-left` | `images/prerequisites.png` |

No quizzes, no lab stub, no Questions and Answers in the introduction.

---

## 3. Each content chapter (`0N-….md`)

| # | Slide | Layout | Notes |
| :--- | :--- | :--- | :--- |
| 1 | Chapter title | `title` | `# Chapter N: Name` |
| 2 | Chapter N: Objectives | default | Tangible objectives from the outline |
| 3 | For each section: Navigation | `navigation` | All sections listed; exactly one **bold** (the current one) |
| 4 | For each section: teaching slides | varies | As many as the teaching point needs. Not a target count |
| 5 | Lab stub | default | `# Lab N: Title` and `**Time:** 30 minutes` only. No steps, no URL |
| 6 | What You Learned | default | Past tense of the Chapter Objectives, same ideas, same order |
| 7 | Quiz 1 of 3 / Quiz 1: Answer | default | Multiple choice A–D, then `**Correct: X.**` with rationale |
| 8 | Quiz 2 of 3 / Quiz 2: Answer | default | Same pattern |
| 9 | Quiz 3 of 3: Discussion / Quiz 3: Discussion Points | `2-column` | `### Prompt` + `### Discuss`; then `### Strong Answers Mention` + `### Watch For` |
| 10 | Questions and Answers | default or `stacked` | `Questions?` **or** stacked with `images/qa.png`; one pattern per course |

Quizzes are the default for content chapters because they practice what the
chapter taught, not because they add slides. Omit them only for a course-summary
or closing chapter, or when the user says so.

A chapter with no lab omits the lab stub. A chapter with more than one lab may
place a lab stub after the section it supports.

---

## 4. Spine checklist

- [ ] Introduction order: Title, Welcome!, Course Objectives, Agenda, Who Should Attend, Prerequisites
- [ ] Welcome and Who Should Attend use `panel-right`; Agenda and Prerequisites use `panel-left`; stock images wired
- [ ] Course Objectives = 1 overall + 1 per content chapter; Agenda lists every chapter
- [ ] Every content chapter: Title, Objectives, (Navigation, sections)…, Lab stub, What You Learned, Quizzes, Questions and Answers last
- [ ] Every Navigation slide lists all sections of that chapter with exactly one bold item, matching the section order
- [ ] What You Learned mirrors Chapter Objectives in past tense
- [ ] Lab stubs have title and time only
- [ ] One Questions and Answers pattern used across the course
