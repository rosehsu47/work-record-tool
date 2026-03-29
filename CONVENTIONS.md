# Work Record — Conventions

This file defines how to maintain `project-index.md`, generate per-project intro files, and
regenerate the personal career summary. Claude Code reads this file automatically via `CLAUDE.md`.

> **Setup note:** After cloning, run the path setup command in README.md § Quick Start step 2
> to replace `{WORK_RECORD_PATH}` with your actual folder path throughout this file.

---

## 1. Directory Structure

```
{WORK_RECORD_PATH}/
├── CONVENTIONS.md           ← this file (rules + templates)
├── CLAUDE.md                ← auto-loaded context for Claude Code sessions
├── project-index.md         ← quick-scan index of all key projects
├── my-summary.md            ← personal career summary (generated, gitignored)
└── resumes/
    └── resume-{role}-{date}.md   ← one file per job application (gitignored)
```

Each project's full intro lives **inside that project's own repo**, not here.

---

## 2. project-index.md — Management Rules

### When to add an entry
Add a new entry whenever:
- A new client/product project has been worked on significantly
- An existing project gains a meaningfully different stack or purpose

### Entry format (copy-paste template)
```markdown
### {Client or Product Name}
- **Path:** `{absolute path to the project's {category}_project_intro_{name}.md}`
- **Stack:** {comma-separated: language, framework, DB, cloud services, CI/CD}
- **Domain:** {one sentence — what the system does and for whom}
- **Highlights:** {3–5 keywords relevant to interviews or technical discussions}
```

### Rules
- Keep each entry to 4 lines — no paragraphs
- Stack line: list only infrastructure-relevant technologies (skip internal libs)
- Highlights: pick terms that map to job description keywords (e.g. RBAC, multi-tenant, event-driven, Kubernetes)
- Sort entries by most recently worked on (newest at top)

---

## 3. {category}_project_intro_{name}.md — Generation Rules

### File naming
Choose a `{category}` prefix that groups projects by client or team.

```
{category}_project_intro_{repo-or-product-name}.md
```

Examples:
- `client-acme_project_intro_crm.md`
- `internal_project_intro_platform.md`
- `freelance_project_intro_ecommerce.md`

### Customize your categories
Edit this table to match your own project groupings:

| Category prefix | Represents |
|---|---|
| `{your-client-or-team}` | {description} |
| `{your-client-or-team}` | {description} |
| `internal` | Internal or personal projects |

### File location
Place the file in the **root of the project repo** it describes.

### How to generate

Use the slash command from the `work-record` folder:
```
/new-project-intro /absolute/path/to/your/repo
```

Or tell Claude Code directly:
> "Explore this repo and generate a project intro file following the conventions in `{WORK_RECORD_PATH}/CONVENTIONS.md`. Then add a new entry in `{WORK_RECORD_PATH}/project-index.md`."

### Required sections (in order)

```markdown
# {Project Name} — Project Introduction (Interview Reference)

> One-line context: prepared for what purpose, e.g. interview for X role.

## Opening Hook
A 2–3 sentence spoken intro. Should cover: what the system does, who uses it, what cloud/tech it runs on.

## Project Overview
Table: Client, Domain, Language, Database, Portals/Services, Environments.

## Cloud Architecture
ASCII diagram showing: CI/CD → registries → compute → database.
List each cloud component with its actual value (e.g. real hostnames from .env files).

## {Cloud Provider A} Deployment Flow
- Trigger (which branch/tag)
- Workflow filename
- Components table (service name + actual endpoint/registry)
- Numbered steps showing exact commands or actions

## {Cloud Provider B} Deployment Flow
(same structure — add one section per cloud provider used)

## Environment Breakdown
Table: Env | Database | Auth | Domains

## Key Architecture Patterns
One subsection per pattern. Each should:
- Name the pattern
- Describe the concrete implementation in this project
- Map to a JD keyword where applicable

## Security & Compliance Highlights
Table: Measure | Implementation

## Key Interview Talking Points
Table: Topic | Evidence | What to Say
Timeless — not tied to any specific JD. Covers the project's strongest angles for interviews.
JD-specific mapping goes in resumes/resume-{role}-{date}.md.

## Closing Statement
A 3–4 sentence spoken closing. Should signal: production maturity, known limitations,
and the next architectural evolution toward the target stack.

## Key Numbers

### Concrete Facts
Table of raw metrics an interviewer might ask about.
Format: | Metric | Value |

### Impressive Outcomes
Table of achievements that signal scale, architectural maturity, rare experience, or domain complexity.
Each entry must answer "why does this impress someone?"
Do NOT include ordinary counts (e.g. "5 workflows", "3 environments").
Format: | Achievement | Why It Impresses |
```

### Content rules
- Use actual values from the codebase (real hostnames, real workflow filenames, real env var names)
- Do not invent or generalize — if something isn't in the code, don't include it
- ASCII diagrams should reflect the real CI/CD flow found in `.github/workflows/`
- Keep the file self-contained — a reader with no prior context should understand the full system
- JD-specific mapping belongs in `resumes/resume-{role}-{date}.md`, not here

---

## 4. my-summary.md — Generation Rules

### File location
`{WORK_RECORD_PATH}/my-summary.md` *(gitignored — regenerate any time)*

A single, self-contained personal introduction document synthesizing all documented projects
into hard skills, soft skills, project highlights, and spoken-ready statements.

### How to generate

Use the slash command:
```
/update-summary
```

Or tell Claude Code:
> "Summarize my working experience and how to explain the projects I've done for my personal
> introduction (including hard and soft skills), based on the project descriptions in
> `project-index.md`. Create `my-summary.md` following the conventions in
> `{WORK_RECORD_PATH}/CONVENTIONS.md`."

### Required sections (in order)

```markdown
# Personal Introduction — Career Summary

> One-line context: source projects and date prepared.

## Opening Statement (Spoken — ~90 seconds)
A memorizable spoken intro: career identity → languages → cloud breadth → project names →
what makes the candidate distinct. Must be deliverable in under 90 seconds.

## Professional Summary
2–3 sentences for written use (resume, LinkedIn, email).

## Hard Skills
Organized by category. Each row: skill name + project evidence (what was actually built).
Categories: Languages, Backend Frameworks, Frontend, Databases, Cloud per-provider,
Containerization & Orchestration, CI/CD, Secrets & Security, Authorization & Identity,
Async & Messaging, Monorepo & Code Quality.

## Soft Skills
One subsection per skill. Each must map to a concrete project behaviour — no generic claims.

## Project Highlights
One paragraph per project: what it is → what you built → key tech → key scale metric.

## Key Numbers

### Concrete Facts
Table of raw metrics. Format: | Metric | Value |

### Impressive Outcomes
Table of achievements that signal scale, maturity, or rare experience.
Each entry must answer "why does this impress someone?"
Format: | Achievement | Why It Impresses |
```

### Content rules
- Source only from documented project intro files — no invented details
- Every soft skill claim must be backed by a named project behaviour
- Spoken sections must be readable aloud in under 90 seconds
- Impressive Outcomes must answer "why does this impress an interviewer?" — not just raw counts

---

## 5. resumes/resume-{role}-{date}.md — Generation Rules

### File location
`{WORK_RECORD_PATH}/resumes/resume-{role-slug}-{YYYY-MM}.md` *(gitignored)*

One file per job application. Keeps all JD-specific mapping out of timeless project intros.

### How to generate

Use the slash command:
```
/new-resume Role: {role title}. Company: {company or 'general'}.
JD:
{paste full JD here}
```

### Required sections (in order)

```markdown
# Resume — {Role Title} ({YYYY-MM})

> Target role: {role}. Company: {company or 'general'}. Date: {YYYY-MM}.

## Role & Focus Areas
- Target role: {role title}
- Key JD requirements: {3–5 bullet points}
- Date prepared: {YYYY-MM}

## Projects to Highlight
Ordered list: which project to lead with and why for this specific role.

## Bridging to JD Requirements

### {Project A Name}
Table: JD Requirement | Evidence | What to Say

### {Project B Name}
Table: JD Requirement | Evidence | What to Say

## Recommended Narrative
2–3 sentences on overall positioning: which strengths to lead with, what story
to tell across projects, and what differentiates you for this specific JD.

## Opening Statement for This Role
A tailored spoken intro (under 90 seconds) tuned to this role's priorities.
```

### Content rules
- Pull evidence only from documented project intro files — no invented details
- **Opening Statement**: never state years of experience — only describe technical background (languages, domains, systems built). Years of experience is not in any project intro and must not be invented.
- Every "What to Say" cell must be a concrete, speakable quote
- One file per application — never overwrite; create a new dated file
- Projects section: explicitly state which project to mention first and why

---

## 6. Key Numbers — Definition

All `Key Numbers` sections (in project intros and my-summary.md) must split into two tables:

**Table 1 — Concrete Facts:** Raw metrics from the codebase.
Format: `| Metric | Value |`

**Table 2 — Impressive Outcomes:** Achievements that signal scale, maturity, or rare experience.
Each entry must answer "why does this impress someone?"
Do NOT include ordinary counts (e.g. "5 workflows", "3 environments").
Format: `| Achievement | Why It Impresses |`

Good Impressive Outcome examples:
- 500+ DB migrations in production → long-lived, production-hardened system
- Zero-downtime rolling deployments across 10 K8s namespaces → real orchestration maturity
- Multi-cloud production (AWS + GCP + Azure) → rare breadth, pragmatic decision-making
- Legally binding digital contract signing (national CA) → compliance gravity

---

## 7. Session Handoff Instructions

Open Claude Code in this folder — `CLAUDE.md` auto-loads context.

To resume from a different folder, share:
1. `{WORK_RECORD_PATH}/CONVENTIONS.md`
2. `{WORK_RECORD_PATH}/project-index.md`

Then state your task, e.g.:
- "Add a new project intro for the repo at /path/to/repo"
- "Create a resume file for this role: ..."
- "Regenerate my-summary.md"
