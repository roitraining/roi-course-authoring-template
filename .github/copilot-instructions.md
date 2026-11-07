# Course and lab authoring guidelines (GitHub Copilot)

Follow **PIPELINE.md**. One fresh session per pipeline step.

When **planning** a course, follow:

- [.agents/skills/course-architect/SKILL.md](.agents/skills/course-architect/SKILL.md)
- [.agents/skills/course-architect/examples/outline-template.md](.agents/skills/course-architect/examples/outline-template.md)

When drafting or modifying **presentation slides** in this repository, follow:

- [.agents/skills/course-generator/SKILL.md](.agents/skills/course-generator/SKILL.md)
- [.agents/skills/course-generator/examples/layout-templates.md](.agents/skills/course-generator/examples/layout-templates.md)
- [.agents/skills/shared/slide-markdown-rules.md](.agents/skills/shared/slide-markdown-rules.md)
- [.agents/skills/shared/course-spine.md](.agents/skills/shared/course-spine.md)
- [.agents/skills/shared/svg-craft.md](.agents/skills/shared/svg-craft.md)

When polishing **course visuals** (layouts, SVG diagrams, generated images, screenshot placeholders), follow:

- [.agents/skills/course-graphics-designer/SKILL.md](.agents/skills/course-graphics-designer/SKILL.md)
- [.agents/skills/course-graphics-designer/examples/visual-patterns.md](.agents/skills/course-graphics-designer/examples/visual-patterns.md)
- [.agents/skills/shared/svg-craft.md](.agents/skills/shared/svg-craft.md)

When reviewing for **accuracy, currency, and teachability**, follow:

- [.agents/skills/technical-editor/SKILL.md](.agents/skills/technical-editor/SKILL.md)
- [.agents/skills/shared/verify-current-facts.md](.agents/skills/shared/verify-current-facts.md)

When **proofreading** for spelling, grammar, typography, and consistency, follow:

- [.agents/skills/copy-editor/SKILL.md](.agents/skills/copy-editor/SKILL.md)
- [.agents/skills/copy-editor/examples/editing-patterns.md](.agents/skills/copy-editor/examples/editing-patterns.md)

When drafting or modifying **labs**, follow:

- [.agents/skills/lab-generator/SKILL.md](.agents/skills/lab-generator/SKILL.md)
- [.agents/skills/lab-generator/examples/lab-template.md](.agents/skills/lab-generator/examples/lab-template.md)
- [.agents/skills/shared/lab-markdown-rules.md](.agents/skills/shared/lab-markdown-rules.md)

When **testing** a lab, follow:

- [.agents/skills/lab-tester/SKILL.md](.agents/skills/lab-tester/SKILL.md)

Place slide chapters under `course/` with shared assets in `course/images/`. Place each lab under `labs/lab-NN-slug/` (`lab.md` + `images/` + `solution/`). Write the outline to `plan/course-outline.md`.

Reuse stock slide images in `course/images/`. Default theme is `roi-alt-theme` (`<!-- course-theme: roi-alt-theme -->` after `course-title` in every chapter file). Do not use the ampersand character in titles or body text; write “and” instead.

Content chapters default to quizzes after What You Learned. Lab stubs use title and time only (no lab URL). Questions and Answers may use `Questions?` or stacked + `qa.png`.

Preview labs at https://labv.roitraining.com/ by pasting the lab folder URL.
