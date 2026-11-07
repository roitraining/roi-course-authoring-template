# Course Outline Template

Copy this structure into `plan/course-outline.md`. Keep the headings exactly as
shown; Course Generator and Lab Generator read them. Replace the example
content (a 1-day Terraform course) with your own.

---

````markdown
# Course Outline: 815: Hands-On Terraform

## Course Header

| Field | Value |
| :--- | :--- |
| Code and title | 815: Hands-On Terraform |
| Subtitle | Infrastructure as Code for Cloud Teams |
| Audience | Cloud engineers and developers who deploy infrastructure |
| Level | Intermediate |
| Duration | 1 day (about 6 hours of instruction) |
| Delivery | Instructor-led, in person or virtual |
| Lab environment | Google Cloud project per student, Cloud Shell, Terraform 1.x |
| Status | Draft for review |

### Prerequisites
- Comfortable with the Linux command line
- Familiar with one major cloud console
- Basic Git workflows (clone, commit, push)

## Course Objectives

- **Overall:** Build and operate team Terraform workflows with remote state, modules, and safe applies.
- **Chapter 1:** Write, plan, and apply Terraform configurations with providers and variables.
- **Chapter 2:** Move state to a shared remote backend with locking.
- **Chapter 3:** Package infrastructure as reusable modules.

## Chapters

### Chapter 1: Terraform Fundamentals

**File:** `01-terraform-fundamentals.md`
**Time:** 120 minutes (75 lecture, 30 lab, 15 quiz and discussion)

**Chapter objectives**
- Explain the write, plan, apply loop and what each step changes.
- Configure a provider and authenticate it safely.
- Use variables and outputs to parameterize a configuration.

#### Section 1.1: The Terraform Workflow
- **Teaching point:** Terraform compares desired state in code to real infrastructure and plans the difference.
- **Key concepts:** declarative configuration, plan as a diff, apply, state as the record of what exists
- **Examples and demos:** live `terraform plan` that adds one bucket; reading the plan symbols (+, ~, -)
- **Misconceptions:** “apply runs my file top to bottom like a script”
- **Proves:** the write, plan, apply objective; Lab 1 applies a real plan

#### Section 1.2: Providers and Authentication
- **Teaching point:** …
- **Key concepts:** …
- **Examples and demos:** …
- **Misconceptions:** …
- **Proves:** …

#### Section 1.3: Variables and Outputs
- …

**Lab 1: Deploy Your First Terraform Configuration** (30 minutes)
- **Folder:** `labs/lab-01-first-terraform-config/`
- **Outcome:** Student has applied a configuration that creates a bucket and a service account, parameterized by variables, with outputs printed.
- **Starting state:** Empty Cloud Shell in a fresh project.
- **Finished solution:** `main.tf`, `variables.tf`, `outputs.tf`, `terraform.tfvars`; `terraform apply` succeeds; `terraform output` shows the bucket URL.
- **Tools:** Cloud Shell, Terraform 1.x, `gcloud`
- **Tasks:**
  1. Set up the project and Terraform working directory
  2. Write and apply a bucket resource
  3. Add variables and outputs
  4. Bonus: add a second resource that depends on the first

### Chapter 2: State and Remote Backends
…

### Chapter 3: Modules
…

## Schedule

### Day 1

| Time | Block | Minutes |
| :--- | :--- | :--- |
| 9:00 | Introduction | 15 |
| 9:15 | Chapter 1 lecture | 75 |
| 10:30 | Break | 15 |
| 10:45 | Lab 1 | 30 |
| 11:15 | Chapter 1 quiz | 15 |
| … | … | … |

**Totals:** lecture X min, labs Y min, quizzes Z min, breaks W min.

## Facts to Verify

| Claim the course depends on | Where | Why it may change |
| :--- | :--- | :--- |
| `gcs` backend arguments (`bucket`, `prefix`) | Ch 2, Lab 2 | Provider and backend releases |
| Current Terraform minor version | Ch 1 | Frequent releases |

## Risks and Open Questions

- Do students get a pre-provisioned project, or create their own?
- Is Terraform pinned to a specific version in the lab image?
````

---

## Notes

- Keep one `#` heading for the outline title, and the `##` / `###` / `####` levels shown. Downstream skills rely on them.
- Do not put a slide count on a section. Course Generator writes as many slides as the teaching point needs. It must not invent a budget.
- Chapter **Time** and the schedule are an estimate you write after the teaching is listed. Do not add or cut sections to make them match the requested duration. Report the difference in the handoff and stop.
- When an existing outline was assessed, add a `## Changes from the Source Outline` section listing what you added or changed.
