# Copy Edit Report Template

Write this file as `reviews/copy-edit-report.md`. If a report already exists,
add a new dated `## Pass` section instead of overwriting.

---

````markdown
# Copy Edit Report: 815: Hands-On Terraform

## Pass: 2026-11-07

| Field | Value |
| :--- | :--- |
| Editor model | (cheaper model name) |
| Session | Fresh (yes / no) |
| Scope | Slides / slides and labs |

### Glossary (forms standardized this pass)

| Term | Form used | Notes |
| :--- | :--- | :--- |
| BigQuery | `BigQuery` | Not “Big Query” |
| hands-on | `hands-on` | Hyphenated in titles and prose |

### Fix counts

| Type | Count |
| :--- | :--- |
| Spelling | |
| Grammar | |
| Smart quotes | |
| Em-dashes / ampersands | |
| Consistency | |

### Representative fixes

- `01-….md` / Why Local State Fails: “corupt” → “corrupt”
- `02-….md` / Questions and Answers: `Q&A` → `Questions and Answers`

### Left unchanged on purpose

- `gcloud`, `kubectl` kept as command-style names
- Inline code and fenced samples untouched
- “BigQuery” in code comments left as written inside fences

### Residual risk for the human

- (Anything you were unsure about; keep this short)
````
