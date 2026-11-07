# Technical Review Report Template

Write this file as `reviews/technical-review.md`. If a report already exists,
add a new dated `## Pass` section instead of overwriting.

Replace the example rows with real findings.

---

````markdown
# Technical Review: 815: Hands-On Terraform

## Pass: 2026-11-07

| Field | Value |
| :--- | :--- |
| Reviewer model | (model name) |
| Session | Fresh (yes / no) |
| Web / CLI verification | Available / not available |
| Outline | `plan/course-outline.md` present / missing |
| Lab tester reports | `labs/lab-01-…/test-report.md` (list) |
| Scope | Slides, labs, or both |

### Summary

- **Readiness:** (ready for human technical review / not ready: list blockers)
- **Top risks:**
  1. …
  2. …
  3. …

### Findings

| ID | Severity | Location | Problem | Evidence | Recommended fix | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| T-1 | Must fix | `01-….md` / Why Local State Fails | `terraform force-unlock` flag is wrong | Official docs, YYYY-MM-DD | Change to `…` | Open |
| T-2 | Should fix | `02-….md` / Remote Backends | Objective 2 has no quiz or lab | Outline vs slides | Add a quiz item or lab task | Open |
| T-3 | Consider | Lab 1 / Task 3 | Bonus is easier than Task 3 | Walkthrough | Swap or drop | Open |

### Verification log

| Location | Claim | Result | Source | Date |
| :--- | :--- | :--- | :--- | :--- |
| `02-….md` / Remote Backends | `gcs` backend takes `bucket` and `prefix` | Confirmed | https://developer.hashicorp.com/terraform/language/backend/gcs | YYYY-MM-DD |
| Lab 2 / Task 2 | Console label “Create bucket” | Unverified | No console access | YYYY-MM-DD |

### Fixes applied

| ID | File | Change |
| :--- | :--- | :--- |
| T-1 | `02-….md` | Corrected `terraform init` migrate flag |

### Not in scope (handed off)

- Spelling and typography → Copy Editor
- Layout variety → Course Graphics Designer
- End-to-end lab execution → Lab Tester
````
