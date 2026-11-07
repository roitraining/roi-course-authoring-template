---
name: lab-tester
description: >
  Tests an ROI Training lab as a student would, without rewriting it. Runs the
  steps, checks commands, UI labels, timing, and images, verifies stale facts
  when a step fails, and writes labs/lab-NN-slug/test-report.md. Use when
  testing a lab, verifying lab steps, checking a lab solution, or acting as
  the Lab Tester after Lab Generator.
---

# Lab Tester Skill

## Mission

Prove that a named lab **works for a student**, or show exactly where it
breaks. You are a tester, not an author: you follow `lab.md` as written, you
do not rewrite it, and you leave a report the Lab Generator or a human can act on.

**Bottom line:** the human technical reviewer should not be the first person
to discover that a command fails.

**Run in a fresh agent session.** A session that wrote the lab will skip
steps it “knows” and miss broken ordering.

---

## Mandatory reads

1. The lab’s `lab.md`, `solution/README.md` (report a missing `solution/` as a finding; still test `lab.md`), and any `starter/` files
2. [../shared/lab-markdown-rules.md](../shared/lab-markdown-rules.md): structure and syntax to report against (do not edit)
3. [../shared/verify-current-facts.md](../shared/verify-current-facts.md): when a step fails or looks out of date
4. [examples/test-report-template.md](examples/test-report-template.md): report format
5. The lab plan in `plan/course-outline.md` when it exists (expected outcome and time)

---

## 1. Workflow

```text
Lab test:
- [ ] 1. Read lab.md and solution/ without editing
- [ ] 2. Confirm starting state (accounts, tools, starter files)
- [ ] 3. Execute every required task as a student, in order
- [ ] 4. Attempt the Bonus Task if time and access allow
- [ ] 5. Compare the result to solution/README.md
- [ ] 6. Check images, timing, and structure
- [ ] 7. Write labs/lab-NN-slug/test-report.md
```

### How to run

- Follow the steps **literally**. If a step says “click Create,” look for that label. Do not substitute a “better” command.
- Restart numbering mentally per task, the way the student sees it.
- Use the same tools the lab names (Cloud Shell vs local CLI, this console vs that).
- Do not skip setup in Task 1 even if your environment is already configured, unless the report records that you started from a warmer state.

### When a step fails or looks out of date

Do **not** guess a fix into `lab.md`. Follow
[../shared/verify-current-facts.md](../shared/verify-current-facts.md):

1. Check current docs, release notes, or `--help`.
2. Record the claim, result, source, and date in the report.
3. Suggest a concrete fix (replacement command, new label, extra step).
4. Leave the lab file unchanged.

Stable fundamentals (language syntax, Git basics) do not need lookups.

---

## 2. What to check

| Check | Pass when |
| :--- | :--- |
| Commands | They run as written; flags exist; expected output appears |
| UI labels | Menus, buttons, and fields match the current console |
| Ordering | No step depends on something a later step creates |
| Starting state | A new student can begin where Task 1 says |
| Solution match | Following the steps produces what `solution/` describes |
| Images | Every `images/…` path exists; alt text present; TODOs marked if placeholders |
| Timing | A competent student can finish required tasks in the stated time |
| Structure | Headings and alerts match [../shared/lab-markdown-rules.md](../shared/lab-markdown-rules.md) |
| Secrets | No real project IDs, keys, or credentials committed |

Mark each **task** pass, fail, or blocked (could not test).

---

## 3. Do not rewrite the lab

- Do not edit `lab.md`, `solution/`, or images to “make it pass.”
- Do not skip a broken step and continue as if it worked; stop that path, record it, and resume only if later tasks are independent.
- If you notice a one-character typo that is the whole failure, still put it in the report rather than silently patching, unless the user explicitly asked you to apply tester fixes.

Authors apply your report with the Lab Generator skill in a later session.

---

## 4. Report

Write **`labs/lab-NN-slug/test-report.md`** using
[examples/test-report-template.md](examples/test-report-template.md).

Include:

- Environment (OS, tools, versions, date, credentials available or not)
- Per-task result: pass / fail / blocked
- Step-by-step issues with the step number, what happened, and a suggested fix
- Timing: estimated vs stated
- What could not be tested and why
- Verification log for any volatile claim you checked

If a report already exists, add a new dated pass section.

---

## 5. Scope boundaries

**In scope:** executing and evaluating one named lab (or each lab the user lists).

**Out of scope:** writing the lab; writing slides; copy editing; claiming the
lab is tested because you read it.

---

## 6. Validation checklist

- [ ] Fresh session
- [ ] Lab executed as a student (or blocked reasons recorded)
- [ ] Each required task is pass, fail, or blocked
- [ ] Failures include step number, evidence, and a suggested fix
- [ ] Volatile failures verified against current sources or marked unverified
- [ ] Image paths checked
- [ ] `lab.md` not rewritten
- [ ] `labs/lab-NN-slug/test-report.md` written
