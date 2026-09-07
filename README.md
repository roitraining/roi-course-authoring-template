# ROI Course Authoring Template

Template repository for ROI Training **slide courses** and (soon) **labs**.  
It does **not** include the slide or lab viewer apps—only what instructors need to author content with an AI coding agent.

## What’s in this repo

| Path | Purpose |
| :--- | :--- |
| `course/` | Slide Markdown + shared `images/` (stock graphics + sample) |
| `labs/` | Lab Markdown (Lab Generator skill coming later) |
| `.agents/skills/course-generator/` | Rules and layout templates for slide courses |
| `.cursorrules`, `CLAUDE.md`, `AGENTS.md`, `.github/copilot-instructions.md` | Point every common coding agent at the skill |

## Quick start

1. **Create your course repo** from this template (GitHub → *Use this template*), or clone/copy it.
2. **Open the repo** in Cursor, VS Code (Copilot), Claude Code, Antigravity, or another agent-capable editor.
3. **Ask the agent** to create a course, for example:
   - *“Using the Course Generator skill, outline a 1-day intermediate course on … then write the chapter files under `course/`.”*
4. **Put slides under `course/`** (multi-file: `00-introduction.md`, `01-….md`, …) and keep shared graphics in `course/images/`.
5. **Preview slides** in the hosted HTML Slides Viewer (paste your GitHub course folder URL):
   - https://roitraining.github.io/md-to-html-slides-viewer/
6. **Labs** go under `labs/` when you are ready (see `labs/README.md`). Preview with the [lab viewer](https://github.com/roitraining/md-to-html-lab-viewer).

Full workflow: **[AUTHORING.md](AUTHORING.md)**.

## Sample

Open `course/sample-course.md` in the slides viewer to see layouts and stock intro/outro images.

## Related products

- Slides viewer: https://github.com/roitraining/md-to-html-slides-viewer  
- Lab viewer: https://github.com/roitraining/md-to-html-lab-viewer  
