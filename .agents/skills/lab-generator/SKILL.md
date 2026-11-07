---
name: lab-generator
description: >
  Designs and writes ROI Training hands-on lab manuals as Markdown for the HTML
  Lab Viewer, one folder per lab with lab.md, images, and a solution. Works
  solution-first: build the finished result, then write the steps that get
  students there. Use when creating labs, lab guides, lab manuals, challenge
  steps, or pairing labs with course slide stubs.
---

# Lab Generator Skill

Write **clear, procedural lab manuals** for intermediate professionals. Output
compiles in the [HTML Lab Viewer](https://labv.roitraining.com/) as a single
Markdown document (not slide decks).

Labs are **simpler than slide courses**: one story, numbered tasks, copyable
commands, screenshots where useful. Prefer doing over lecturing.

---

## Mandatory reads (every run)

1. [../shared/lab-markdown-rules.md](../shared/lab-markdown-rules.md): required structure, syntax, typography, images, conformance checklist
2. [examples/lab-template.md](examples/lab-template.md): copy-paste skeleton
3. `labs/lab-01-sample-lab-viewer-format/lab.md`: reference sample
4. **`plan/course-outline.md`** when it exists: the lab plan (outcome, starting state, finished solution, tools, tasks)
5. [../shared/verify-current-facts.md](../shared/verify-current-facts.md): commands, flags, and UI labels change; verify them while you build

If there is no lab plan for the lab you are asked to write, ask for the
outcome, time, and environment, or recommend running the Course Architect first.

---

## 1. Audience and tone

- Default: intermediate practitioners (same audience as the paired slide course unless the user says otherwise).
- Voice: **second person** (*you*), **simple present**, conversational but professional.
- Steps begin with an **imperative** (Click, Run, Create, Configure…).

---

## 2. Workflow: solution first, then steps

A good lab author builds the finished result first, then writes the path to it.
Writing steps before the solution exists produces labs that do not work.

### Step 1: Build the finished solution

- Build the end state the lab plan describes, for real, when you have the tools and access.
- Save solution files under `labs/lab-NN-slug/solution/` (code, config, SQL, notebooks, prompt text, whatever the student produces).
- Write `solution/README.md` with:
  - What the finished state is
  - How to verify it (commands to run, what the console should show, expected output)
  - Versions and tools used, with the date
- For console-only labs with no files, `solution/README.md` describes the end state and how to check it.
- If you cannot build it (no credentials, no product access), say so, and write the most accurate solution you can with every unverified part marked.

### Step 2: Define the starting state

- What the student has at the start: an empty project, a starter repo, a dataset, a previous lab’s result.
- If students need starter files, put them in `labs/lab-NN-slug/starter/`.

### Step 3: Write the steps

- Work out the shortest sensible path from the starting state to the solution.
- Group it into **Tasks** (usually 3–6) that each produce a visible result. Setup goes in Task 1.
- Add a **Bonus Task** with fewer hints unless it truly does not fit.
- Every command and code block in `lab.md` must match the solution files.
- When a step copies a starter file, give the **exact relative path** from the lab folder (for example `starter/README.md`) and the destination. Do not say “copy the starter file” without a path.

### Step 4: Images

- Capture real screenshots for non-obvious UI steps when you can.
- Generate diagrams when they teach better than a screenshot.
- Otherwise: image reference + `<!-- TODO IMAGE: … -->` + a labeled placeholder file (see [../shared/lab-markdown-rules.md](../shared/lab-markdown-rules.md) §6).

### Step 5: Self-check, then hand off

- Run the conformance checklist in [../shared/lab-markdown-rules.md](../shared/lab-markdown-rules.md) and the checklist in §6 below.
- Check that the course lab stub (if any) has this lab’s title and time only.
- **Do not grade your own lab as tested.** Full verification belongs to the **Lab Tester** skill in a fresh session. End your turn by listing what you could and could not run.

---

## 3. Folder layout

```text
labs/
  lab-01-getting-started/
    lab.md             # the manual (preferred filename)
    images/
    solution/          # finished result + README.md (how to verify)
    starter/           # optional: files students start from
```

- Folder: `lab-NN-short-kebab-slug`, aligned with the course chapter and lab numbers.
- Preview by pasting the GitHub URL of the **lab folder** into the [Lab Viewer](https://labv.roitraining.com/).

---

## 4. Writing guidance

Structure, headings, syntax, and typography are fixed by
[../shared/lab-markdown-rules.md](../shared/lab-markdown-rules.md). Within
that structure:

### Overview and learning objectives

```markdown
## Overview

In this lab, you will configure a remote backend and migrate Terraform state for team use.

### You learn how to:
- Create a remote state bucket with versioning enabled.
- Configure a Terraform backend and migrate state.
- Verify that state locking prevents concurrent applies.
```

- One learning bullet per primary task (Bonus may share themes rather than adding a new bullet).
- Congratulations mirrors these bullets in past tense.

### Scenario (optional, but preferred)

A short business problem or use case. Omit when the Overview already gives enough context.

### Task body pattern

1. One or two sentences on what this task achieves.
2. Numbered steps, one primary action each, blank line between steps.
3. Commands introduced by their purpose (“To list regions, run:”), in fenced blocks with a language tag.
4. Screenshots for non-obvious UI; never screenshot text that belongs in a code block.
5. Callouts where they help (below).
6. Optional short **Success criteria** list when verification matters.

### Callouts

| Alert | Use when |
| :--- | :--- |
| `> [!NOTE]` | Helpful context, expected results, “you should see…” |
| `> [!IMPORTANT]` | Must-follow constraints and required settings |
| `> [!WARNING]` | Mistakes, destructive actions, easy-to-miss failures |
| `> [!TIP]` | Optional shortcut (sparingly) |
| `> [!CAUTION]` | Stronger than WARNING when the risk is high |

Place callouts after the step they apply to. Not on every step.

### Teaching quality bar

- One clear **story**: problem → approach → tasks → accomplishment.
- Prefer **transferable skills** over click-only tourism.
- Keep conceptual asides short; link out for deep docs.
- Fit the stated time. If the solution takes longer than the budget to reach, cut scope or move work to the Bonus Task, and say so.

---

## 5. Relationship to other skills

- **Course Architect** plans the lab (outcome, starting state, solution sketch).
- **Course Generator** writes the slide lab stub: title and time only. Humans add the lab URL later.
- **Lab Generator** (this skill) builds the solution and writes `lab.md`.
- **Lab Tester** runs the lab as a student in a fresh session and writes `test-report.md`. Use its report to fix the lab.

---

## 6. Explicit non-goals

- Do **not** write slide decks (Course Generator).
- Do **not** author Qwiklabs YAML, assessments, or `ql-*` markup unless the user explicitly asks for that platform.
- Do **not** invent credentials, project IDs, or secret values; use placeholders like `YOUR_PROJECT_ID`.
- Do **not** invent fake product screenshots when accuracy matters.
- Do **not** add a separate top-level Setup or Prerequisites section; setup goes in Task 1.
- Do **not** put a lab URL on the course stub.
- Do **not** mark a lab as tested; that is the Lab Tester’s job.

---

## 7. Validation checklist

- [ ] [../shared/lab-markdown-rules.md](../shared/lab-markdown-rules.md) conformance checklist passes
- [ ] `solution/` exists with `README.md` describing the end state and how to verify it
- [ ] Every command and code block in `lab.md` matches the solution files
- [ ] Starting state is clear; `starter/` exists if students need files
- [ ] Every “copy this file” step names the exact source path and destination
- [ ] Lab matches its plan in `plan/course-outline.md` (or differences are reported)
- [ ] Bonus Task included unless it clearly does not fit
- [ ] Steps fit the stated time
- [ ] Volatile facts (commands, flags, UI labels, versions) verified or listed as unverified
- [ ] Screenshots captured or generated when possible; otherwise placeholder file + TODO + alt text
- [ ] Course stub (if any) has title and time only
- [ ] End-of-turn summary lists what was run and what still needs the Lab Tester
