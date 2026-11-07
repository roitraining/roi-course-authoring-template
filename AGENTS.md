# Agent instructions — ROI course authoring

## Skills

- **Course architecture:** Always read and follow `.agents/skills/course-architect/SKILL.md` when planning a course or writing `plan/course-outline.md`.
- **Slide courses:** Always read and follow `.agents/skills/course-generator/SKILL.md`, `.agents/skills/course-generator/examples/layout-templates.md`, `.agents/skills/shared/slide-markdown-rules.md`, `.agents/skills/shared/course-spine.md`, and `.agents/skills/shared/svg-craft.md` when creating, outlining, editing, or validating slides. Work in phases: spine, then content, then refine. Create an SVG only if it passes the svg-craft gate.
- **Course graphics:** After content exists, read and follow `.agents/skills/course-graphics-designer/SKILL.md`, `.agents/skills/course-graphics-designer/examples/visual-patterns.md`, and `.agents/skills/shared/svg-craft.md`. Improve layouts and graphics without breaking viewer rules. Redraw or delete SVGs that fail the quality bar.
- **Technical editing:** For accuracy, currency, and teachability, read and follow `.agents/skills/technical-editor/SKILL.md` and `.agents/skills/shared/verify-current-facts.md`. Fresh session; do not trust model memory for APIs, CLIs, model names, or console labels.
- **Copy editing:** For spelling, grammar, house-style typography, and consistency, read and follow `.agents/skills/copy-editor/SKILL.md` and `.agents/skills/copy-editor/examples/editing-patterns.md`. Do not break code, directives, or product names.
- **Labs:** Always read and follow `.agents/skills/lab-generator/SKILL.md`, `.agents/skills/lab-generator/examples/lab-template.md`, and `.agents/skills/shared/lab-markdown-rules.md` when creating or editing files under `labs/`. Build the solution first, then the steps.
- **Lab testing:** Read and follow `.agents/skills/lab-tester/SKILL.md`. Do not rewrite the lab; write `test-report.md`.

Pipeline: see `PIPELINE.md`. One fresh session per step.

## Repository layout

- `course/` — slide Markdown and `images/`
- `labs/lab-NN-slug/` — each lab’s `lab.md`, `images/`, and `solution/`
- `plan/` — `course-outline.md` from Course Architect
- `reviews/` — technical-review.md and copy-edit-report.md
- Stock intro/outro slide images live in `course/images/`; copy/reuse those filenames; do not regenerate.

## Output expectations

- Prefer multi-file courses (`00-introduction.md`, `01-….md`, …) under `course/`; short single-deck courses may use one file.
- Same `<!-- course-title: … -->` in every chapter file.
- Same `<!-- course-theme: roi-alt-theme -->` in every chapter file (unless the user names another theme).
- No ampersand (`&`) in slide or lab titles/body text (use “and”).
- Content chapters: Lab stub → What You Learned → Quizzes (default) → Questions and Answers.
- Lab stub on slides: **title and time only** (no lab URL—humans add the link later).
- Questions and Answers: `Questions?` body **or** stacked + `images/qa.png`—pick one pattern per course.
- Labs: Title → Time Required → Overview (You learn how to) → optional Scenario → Lab Instructions (Task / Bonus Task) → Congratulations!; preferred file `lab.md`; no Qwiklabs `ql-*` tags.
- Preview labs at https://labv.roitraining.com/ (paste the lab folder URL).
