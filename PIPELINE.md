# Course Factory pipeline

How to create an ROI Training course with this template and an AI coding agent.
Each step is a **new agent session** that reads and writes **files on disk**,
not chat history. That keeps the work portable across Cursor, VS Code + Copilot,
Claude Code, and Antigravity.

**Goal, not replacement:** for each day of training, plan on about one day of
human technical verification and one to two hours of human copy editing. The
pipeline should get the draft close enough that those humans are reviewing,
not rebuilding.

If a skill seems unaware of the rules, tell it to read the skill file listed
in that step before doing any work.

---

## Model tiers

| Tier | Use for |
| :--- | :--- |
| **Best available** | Architecture, spine, content, labs |
| **Different model** from the one that wrote the course | Technical review |
| **Cheaper** | Copy editing |

“Best available” means the strongest model you can give a long, careful task.
Architecture should run in a **planning mode** if the tool has one (for example Cursor Plan mode).

---

## Step 0: New course repo

**Purpose:** copy this template into a new git repo, disconnected from the template’s history.

**Model:** any. **Fresh session:** not required.

**Who runs it:** ask an agent to run the script, or run it yourself. The script is
deterministic; the agent helps with naming, `git`, and `gh` authentication.

```bash
# From a clone of this template (Git Bash or WSL on Windows):
scripts/new-course.sh ../my-course-folder
scripts/new-course.sh ../my-course-folder --github owner/repo --private
```

The script copies the template **without** `.git`, `course/sample-course.md`,
`introducing-the-roi-course-factory/`, sample course images, and the sample lab.
It runs `git init`, makes the first commit, and optionally creates a GitHub repo.

**Human checkpoint:** open the new folder in your editor. Confirm you are not
still inside the template repo.

**Copy-paste prompt**

```text
Run scripts/new-course.sh to create a new course repo at ../COURSE-FOLDER-NAME.
Use --github owner/repo if I should create a GitHub repo, and --private if it
should be private. If git or gh is missing or I am not signed in, tell me
exactly what to install or run. Do not create the GitHub repo unless I named it.
```

---

## Step 1: Course architecture

**Purpose:** a detailed outline good enough that later steps do not guess.

**Skill:** `.agents/skills/course-architect/SKILL.md`

**Model:** best available, in planning mode. **Fresh session:** yes (first session in the new repo).

**Input:** your request, or an existing outline.
**Output:** `plan/course-outline.md`

If you already have a detailed outline, say so. The skill **assesses** it, fills
gaps, and stops if it already passes. Do not skip this step when there is no
outline or only a thin bullet list.

**Human checkpoint (required):** read the outline. Fix audience, duration, labs,
and anything it invented. Downstream steps treat this file as the contract.

**Copy-paste prompt**

```text
Read .agents/skills/course-architect/SKILL.md and follow it.
Create a course outline for: AUDIENCE, DURATION, TOPIC, OUTCOMES, LAB ENVIRONMENT.
Write plan/course-outline.md. Sections follow teaching points, not a slide count.
Ask me only what you cannot infer. End with one duration estimate and do not
resize the outline to match it. Stop for my approval. Do not write slides or labs.
```

Assess an existing outline:

```text
Read .agents/skills/course-architect/SKILL.md and follow it in Assess mode.
The outline is at PATH (or pasted below). Grade it, fill gaps, write
plan/course-outline.md, and list every change. If it already passes, say so
and stop.
```

---

## Step 2: Course spine

**Purpose:** every chapter file and every boiler slide, with one placeholder per section. No teaching slides yet.

**Skill:** `.agents/skills/course-generator/SKILL.md` (phase: **spine**)

**Model:** best available. **Fresh session:** yes.

**Input:** approved `plan/course-outline.md`
**Output:** `course/00-introduction.md`, `course/01-….md`, …, stock images in `course/images/`

**Human checkpoint:** skim the files. Confirm chapters, section names, lab titles, and times. Search for `TODO CONTENT` to see placeholders.

**Copy-paste prompt**

```text
Read .agents/skills/course-generator/SKILL.md and follow the spine phase only.
Use the approved outline in plan/course-outline.md. Write the chapter files
under course/. Do not write teaching slides. Stop when the spine checklist passes.
```

---

## Step 3: Course content

**Purpose:** fill the placeholders with teaching slides, quizzes, and graphics.

**Skill:** `.agents/skills/course-generator/SKILL.md` (phase: **content**, then optional **refine**)

**Model:** best available. **Fresh session:** yes (one chapter per session on long courses).

**Input:** spine files + outline
**Output:** filled chapter Markdown and images; no `TODO CONTENT` left in scope

Default to **one chapter per run** on a multi-day course.

**Human checkpoint:** preview the chapter at https://slidesv.roitraining.com/. Note gaps; the refine phase or Technical Editor will take a full pass.

**Copy-paste prompt**

```text
Read .agents/skills/course-generator/SKILL.md and
.agents/skills/shared/svg-craft.md and follow the content phase.
Fill chapter N (file course/0N-….md) from plan/course-outline.md. Replace every
TODO CONTENT placeholder in that file, write the quizzes, and create or TODO
the images. A slide exists only when it teaches something the section does not
already teach. Do not add or cut slides to change a count. Create an SVG only
if it passes the svg-craft gate; otherwise use columns or skip the diagram.
End with one ballpark sentence and do not edit to chase it. Do not start
another chapter. Stop when the content checklist passes.
```

Optional refine, after all chapters are filled:

```text
Read .agents/skills/course-generator/SKILL.md and follow the refine phase on
the whole course. Cut a slide that repeats a point already taught. Do not cut a
needed example, and do not add or merge slides to change a count. Close gaps
and vary layouts. Do not change the outline’s objectives silently. Report what
you changed by chapter, then one ballpark sentence. Do not edit again to move
that number.
```

---

## Step 3b: Graphics polish

**Purpose:** see the whole deck and improve layouts and visuals. Course Generator already created graphics while writing; this is the polish pass.

**Skill:** `.agents/skills/course-graphics-designer/SKILL.md`

**Model:** best available or a capable vision-capable model. **Fresh session:** yes.

**Input:** filled course (no `TODO CONTENT`)
**Output:** updated layouts and `course/images/` assets

Skip this step if chapters still contain `TODO CONTENT`.

**Human checkpoint:** spot-check diagrams for accuracy; Technical Editor will also check them.

**Copy-paste prompt**

```text
Read .agents/skills/course-graphics-designer/SKILL.md and
.agents/skills/shared/svg-craft.md and follow them.
Polish the course under course/ after the content phase. Do not rewrite
objectives or quizzes. Do not regenerate stock intro images. Redraw or delete
SVGs that fail the svg-craft gate. Stop if TODO CONTENT markers are still present.
```

---

## Step 4: Technical review

**Purpose:** accuracy, currency, and teachability. Verify facts that change; do not trust model memory for APIs, CLIs, model names, or console labels.

**Skill:** `.agents/skills/technical-editor/SKILL.md`

**Model:** a **different** model from the one that generated the course. **Fresh session:** required.

**Input:** `course/`, `plan/course-outline.md`, any `labs/*/test-report.md`
**Output:** `reviews/technical-review.md`; only clear, low-risk verified fixes in the Markdown

**Human checkpoint (the main human day):** work the must-fix and should-fix list. This is the one-day-per-training-day review.

**Copy-paste prompt**

```text
Read .agents/skills/technical-editor/SKILL.md and follow it in this fresh session.
Review the course under course/ against plan/course-outline.md. Verify volatile
facts from current docs or --help; do not trust memory. Check for missing
teaching (an objective with no example, a concept used before it is taught).
Do not score chapter length or sameness, and do not add or cut slides to change
a count. Write reviews/technical-review.md. Apply only clear, verified,
low-risk fixes. Do not copy-edit and do not rewrite the curriculum.
```

---

## Step 5: Copy editing

**Purpose:** spelling, grammar, typography, and consistency.

**Skill:** `.agents/skills/copy-editor/SKILL.md`

**Model:** cheaper. **Fresh session:** required.

**Input:** reviewed course
**Output:** in-place language fixes + `reviews/copy-edit-report.md`

**Human checkpoint:** one to two hours confirming the report and skimming the deck.

**Copy-paste prompt**

```text
Read .agents/skills/copy-editor/SKILL.md and follow it in this fresh session.
Copy-edit the course under course/ (and labs/ if they exist). Fix spelling,
grammar, smart quotes, em-dashes, ampersands, and consistency. Do not change
meaning, code, or layout directives. Write reviews/copy-edit-report.md.
```

---

## Step 6: Lab creation

**Purpose:** build the finished solution first, then write the steps that get a student there.

**Skill:** `.agents/skills/lab-generator/SKILL.md`

**Model:** best available. **Fresh session:** yes. Can start after the outline is approved; does not have to wait for copy editing.

**Input:** lab plan in `plan/course-outline.md`
**Output:** `labs/lab-NN-slug/lab.md`, `images/`, `solution/` (and `starter/` if needed)

**Human checkpoint:** skim the solution and the task list before testing.

**Copy-paste prompt**

```text
Read .agents/skills/lab-generator/SKILL.md and follow it.
Build Lab N from the lab plan in plan/course-outline.md. Create the finished
solution under labs/lab-NN-slug/solution/ first, then write lab.md as the path
to that solution. Do not mark the lab as tested.
```

---

## Step 7: Lab testing

**Purpose:** run the lab as a student and report what fails.

**Skill:** `.agents/skills/lab-tester/SKILL.md`

**Model:** capable; a different model from the author is a plus. **Fresh session:** required.

**Input:** one named lab folder
**Output:** `labs/lab-NN-slug/test-report.md` (does **not** rewrite the lab)

Feed the report back to Lab Generator or to the Technical Editor. Then a human
walks the lab once.

**Copy-paste prompt**

```text
Read .agents/skills/lab-tester/SKILL.md and follow it in this fresh session.
Test labs/lab-NN-slug/ as a student. Do not edit lab.md. Write
labs/lab-NN-slug/test-report.md. If a step fails or looks out of date, verify
against current docs or --help and record the source.
```

---

## Suggested order

```text
0 Setup → 1 Architect (approve) → 2 Spine → 3 Content → 3b Graphics
                                         → 6 Labs → 7 Lab tests
Then: 4 Technical review (reads lab test reports) → 5 Copy edit → human sign-off
```

Labs (6–7) can run in parallel with content (3–3b) once the outline is approved.

---

## Shared rules

Every skill that edits content must follow:

- `.agents/skills/shared/slide-markdown-rules.md`
- `.agents/skills/shared/lab-markdown-rules.md`
- `.agents/skills/shared/course-spine.md`
- `.agents/skills/shared/verify-current-facts.md`

---

## Preview

- Slides: https://slidesv.roitraining.com/ (paste the GitHub URL of `course/`)
- Labs: https://labv.roitraining.com/ (paste the GitHub URL of the lab folder)
