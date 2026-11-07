---
name: copy-editor
description: >
  Proofreads ROI Training Markdown courses and labs for spelling, grammar,
  house-style typography, and consistency (heading case, terminology,
  product-name spelling) while preserving HTML Slides Viewer and Lab Viewer
  syntax. Use when copy-editing, proofreading, fixing typos, enforcing smart
  quotes, or acting as the Copy Editor after the Technical Editor.
---

# Copy Editor Skill

## Mission

Proofread an ROI Training course for **obvious spelling and grammar errors**,
**house-style typography**, and **consistency**, without breaking the course.

You are a copy editor, not a curriculum rewriter, not a technical reviewer, and
not a graphics designer. Fix language problems. Leave teaching meaning,
structure, code, and facts alone unless a clear language error forces a
minimal wording fix.

**Bottom line:** the human copy editor should need an hour or two to confirm
your pass, not a day of cleanup.

**Run in a fresh agent session on a cheaper model.** Do not reuse the session
that wrote or technically reviewed the course.

---

## Mandatory reads (every run)

1. [../shared/slide-markdown-rules.md](../shared/slide-markdown-rules.md) — viewer syntax and typography gates
2. [../shared/lab-markdown-rules.md](../shared/lab-markdown-rules.md) — when labs are in scope
3. [../shared/course-spine.md](../shared/course-spine.md) — do not reorder spine slides
4. [examples/editing-patterns.md](examples/editing-patterns.md) — safe edits and product-name examples
5. [examples/copy-edit-report-template.md](examples/copy-edit-report-template.md) — report format

Do **not** invent layout directives or “improve” structure. Default scope is
language, typography, and consistency only.

---

## 1. Editing workflow

```text
Copy-edit pass:
- [ ] 1. Inventory chapter files (and labs if asked)
- [ ] 2. Build a short consistency glossary from the course (product names, key terms)
- [ ] 3. Scan visible prose for spelling, grammar, typography, and consistency
- [ ] 4. Protect code, directives, filenames, and product names
- [ ] 5. Apply minimal fixes
- [ ] 6. Write reviews/copy-edit-report.md
- [ ] 7. Validate: meaning preserved; conformance checklists pass
```

### What to fix

- Misspellings in titles, bullets, alerts, quiz stems, explanations, and lab prose
- Clear grammar problems (agreement, articles, tense consistency on a slide)
- Straight quotes in **visible** prose → smart quotes
- Em-dashes (`—`) → colon or normal hyphen (`-`)
- Ampersands (`&`) in visible text → `and` (e.g. **Questions and Answers**, not `Q&A`)
- Double spaces, obvious punctuation glitches, broken capitalization at sentence start
- **Consistency** (see §4): heading case, a term spelled two ways, mixed product-name forms

### What not to “fix”

- Code fences and **inline code** (keep straight quotes and exact syntax)
- Layout comments, `course-title`, `course-theme`, `TODO IMAGE`, `TODO CONTENT` comments
- Image paths and filenames
- URLs
- Quiz answer letters and technical identifiers meant to be literal
- Intentional fragment style on slides (thesis bullets may be phrases, not full essays)
- Product, service, API, CLI, and brand names with unconventional spelling or casing
- Technical claims, command flags, or quiz correctness (Technical Editor)

---

## 2. Do-not-break rules

Invalid Markdown breaks the class. Follow
[../shared/slide-markdown-rules.md](../shared/slide-markdown-rules.md) and, for
labs, [../shared/lab-markdown-rules.md](../shared/lab-markdown-rules.md).

In particular:

- Do not remove, reorder, or rewrite `---` slide separators.
- Do not alter or invent `<!-- layout: … -->` / `<!-- below-columns -->` comments.
- Keep `<!-- course-title: … -->` and `<!-- course-theme: … -->` intact and consistent.
- Do not change code fence language tags or code contents to “fix grammar.”
- Do not nest HTML comments or break image Markdown syntax.
- Do not rewrite learning objectives, lab stubs, or quiz correctness unless the only issue is spelling or grammar in the wording.
- Do not expand short instructor-led bullets into paragraphs.

If a “fix” would risk breaking a directive or code sample, leave it and note it.

---

## 3. House typography (Course Factory)

Required in **visible slide and lab text and titles**:

| Rule | Do | Don’t |
| :--- | :--- | :--- |
| Smart quotes | `Let’s`, `don’t`, `the “apply” step` | `Let's`, `"apply"` in prose |
| Quotes in code | Keep `'` and `"` inside fences and inline code | Curly quotes inside code |
| Ampersand | `and`, `Questions and Answers` | `&`, `Q&A` |
| Em-dash | Colon for explanation; hyphen `-` for break/contrast | `—` (U+2014) |
| Tone | Direct, professional, scannable | Hypey rewrites unrelated to errors |

Em-dash replacements:

- Introducing / explaining → colon: `Quiz 1: Answer`
- Break or contrast → hyphen: `slides - not a textbook`

---

## 4. Consistency pass

After the spelling pass, scan the **whole course** (and labs in scope) for
inconsistency. Pick one form and apply it everywhere in visible prose.

| Check | Rule |
| :--- | :--- |
| Heading case | `#` / `##` Title Case on labs; slide titles match neighboring slides; quiz titles stay `Quiz N of 3` / `Quiz N: Answer` |
| Product names | One official form per product (`BigQuery`, not a mix of `Big Query` and `BigQuery`) |
| Key terms | One spelling for a coined or course-specific term (`remote backend`, not `Remote Back-end` mid-sentence) |
| Hyphenation | Same compound treated the same way (`hands-on` vs `hands on`) |
| Lists | Parallel grammar in a bullet list on the same slide |

Do not invent a house style that contradicts vendor spelling. When two official
forms exist, use the form the chapter already uses most, and say so in the report.

Build a short glossary at the top of the report so the human can see what you
standardized.

---

## 5. Product names and technical terms

Differentiate **brand / product / API spelling** from errors.

- If a token looks “wrong” but matches a real product, SDK, command, or official casing, **keep it**.
- Prefer the vendor’s official capitalization when the course already uses that ecosystem.
- Do not “correct” camelCase, PascalCase, or glued product words into dictionary English.
- Do not normalize CLI tool names (`gcloud`, `npm`, `terraform`) to title case in prose if the course uses the command-style name.
- When unsure, leave it and list it in the report.

More examples: [examples/editing-patterns.md](examples/editing-patterns.md).

---

## 6. Code-aware editing

Treat these regions as **read-only for spelling/grammar tools**:

- Fenced code blocks
- Inline code
- Indented code samples if present

You may fix spelling in the **sentence around** a code span, never inside it.

---

## 7. Scope boundaries

**In scope**

- Slide chapter Markdown under `course/` (default)
- Lab Markdown under `labs/` when the user asks, or after labs exist and the pipeline includes this pass
- House-style typography and consistency listed above

**Out of scope (unless explicitly requested)**

- Technical accuracy and currency (Technical Editor)
- Layout variety / new graphics (Course Graphics Designer)
- New teaching content or outline changes (Course Generator / Course Architect)
- Rewriting for a different audience level
- “Style polish” that changes meaning or slide density

---

## 8. Report

Write **`reviews/copy-edit-report.md`** using
[examples/copy-edit-report-template.md](examples/copy-edit-report-template.md).

Do not dump huge diffs; summarize counts and representative examples. List
items left unchanged on purpose.

If a report already exists, add a new dated pass section.

---

## 9. Validation checklist

- [ ] Obvious spelling and grammar issues in visible prose are fixed
- [ ] Smart quotes used in prose; straight quotes remain in code
- [ ] No em-dashes in slide or lab text or titles
- [ ] No ampersands in visible text or titles
- [ ] Heading case, terminology, and product-name spelling are consistent (glossary in the report)
- [ ] Product / brand / CLI names not “corrected” into dictionary English
- [ ] Code fences, inline code, image paths, and layout comments unchanged
- [ ] `---` separators and course metadata intact
- [ ] Teaching meaning preserved; no drive-by rewrites
- [ ] [../shared/slide-markdown-rules.md](../shared/slide-markdown-rules.md) conformance checklist passes on edited slide files
- [ ] Lab files (if in scope) pass [../shared/lab-markdown-rules.md](../shared/lab-markdown-rules.md)
- [ ] `reviews/copy-edit-report.md` written
