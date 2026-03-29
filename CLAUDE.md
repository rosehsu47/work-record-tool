# Work Record — Claude Code Context

This workspace manages career documentation: project interview references, a personal summary,
and per-application resume files. Full conventions are in `CONVENTIONS.md`.

## Key Rules (always apply)

- **Project intros** (`{category}_project_intro_{name}.md`) are timeless — no JD-specific content
- **JD mapping** lives in `resumes/resume-{role}-{date}.md` only — one file per application
- **Evidence** in project intros uses a `Key Interview Talking Points` table (Topic | Evidence | What to Say)
- **Key Numbers** split into two tables: Concrete Facts + Impressive Outcomes (must answer "why does this impress?")
- Source only from documented project intro files — never invent details

## Files

| File | Purpose |
|---|---|
| `CONVENTIONS.md` | Full rules and section templates for all file types |
| `project-index.md` | Index of all documented projects with paths |
| `my-summary.md` | Personal career summary (hard skills, soft skills, spoken intro) |
| `resumes/` | One resume file per job application |

## Slash Commands (available in this folder)

| Command | What it does |
|---|---|
| `/new-project-intro` | Explore a repo + generate project intro + update project-index |
| `/new-resume` | Create a resume file for a specific role |
| `/update-summary` | Regenerate my-summary.md from all project intros |

### Usage examples

```
/new-project-intro /absolute/path/to/your/repo
```

```
/new-resume Role: Cloud Engineer. Company: Stripe.
JD:
{paste JD here}
```

```
/update-summary
```
