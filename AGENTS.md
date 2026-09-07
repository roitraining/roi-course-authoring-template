# Agent instructions — ROI course authoring

## Skills

- **Slide courses:** Always read and follow `.agents/skills/course-generator/SKILL.md` and `.agents/skills/course-generator/examples/layout-templates.md` when creating, outlining, editing, or validating slides.
- **Labs:** When `.agents/skills/lab-generator/` exists, follow it for files under `labs/`. Until then, do not invent a full lab authoring standard; keep lab stubs on slides as links only.

## Repository layout

- `course/` — slide Markdown and `images/`
- `labs/` — lab Markdown
- Stock intro/outro images live in `course/images/`; copy/reuse those filenames; do not regenerate.

## Output expectations

- Prefer multi-file courses (`00-introduction.md`, `01-….md`, …) under `course/`.
- Same `<!-- course-title: … -->` in every chapter file.
- No ampersand (`&`) in slide titles or body text (use “and”).
- Questions and Answers slides: title + `images/qa.png` only (`layout: stacked`).
