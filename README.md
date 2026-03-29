# Work Record

**An AI-powered career documentation system built on [Claude Code](https://claude.ai/code).**

You point it at your project repos. It reads the code, writes structured interview references,
maps your experience to job descriptions, and generates a personal introduction — all as
plain Markdown files you own and version-control.

---

## What Is This?

Most engineers struggle to articulate their work in interviews. This system solves that by
maintaining a living, structured record of every project you've shipped — extracted directly
from your codebase, not written by hand.

**Three types of documents, generated automatically:**

| Document | What it contains | Lives in |
|---|---|---|
| `{category}_project_intro_{name}.md` | Cloud architecture, CI/CD, security, talking points | Inside each project repo |
| `my-summary.md` | Hard skills, soft skills, spoken intro across all projects | This folder |
| `resumes/resume-{role}-{date}.md` | JD mapping, narrative, tailored opening for one application | `resumes/` |

**The key insight:** project intros are timeless facts about the system. JD mapping is
application-specific. Keeping them separate means you never corrupt your source-of-truth
when applying for a new role.

---

## Prerequisites

- **[Claude Code](https://claude.ai/code)** — the CLI or desktop app (required)
- Git (to version-control your documentation)

---

## Quick Start

**1. Create your own copy**

On GitHub, click **Use this template → Create a new repository**, then clone your copy:
```bash
git clone https://github.com/{you}/work-record-tool.git
cd work-record-tool
```

**2. Set your path** (one-time setup)

Several skill files reference `{WORK_RECORD_PATH}` as a placeholder for this folder's absolute path.
Run this to replace it everywhere:
```bash
WORK_RECORD_PATH=$(pwd) && grep -rl '{WORK_RECORD_PATH}' . --include="*.md" | xargs sed -i '' "s|{WORK_RECORD_PATH}|$WORK_RECORD_PATH|g"
```

> On Linux, remove the `''` after `-i`: `xargs sed -i "s|..."`

**3. Open Claude Code in this folder**
```bash
claude .
```

**4. Document your first project**
```
/new-project-intro /absolute/path/to/your/repo
```

Claude explores the repo, writes a project intro inside it, and registers it in `project-index.md`.

**5. Generate your personal summary**
```
/update-summary
```

**6. When applying for a job, create a resume file**
```
/new-resume Role: Backend Engineer. Company: ABC.
JD:
{paste the full job description here}
```

---

## How It Works

```
/new-project-intro {repo-path}
       │
       ▼
{category}_project_intro_{name}.md     ← timeless per-project detail (lives in each repo)
       │                                  cloud architecture · CI/CD · security · talking points
       │                                  NO JD-specific content
       │
       ├──────────────────────────────▶ my-summary.md          (/update-summary)
       │                                  hard skills · soft skills · spoken intro
       │
       └──────────────────────────────▶ resumes/resume-{role}-{date}.md    (/new-resume)
                                          JD mapping · narrative · tailored opening
                                          one file per application, never overwritten
```

**Rule:** Never put JD-specific content in project intros. Create a new resume file instead.
This keeps your project documentation clean and reusable across every future application.

---

## Files in This Folder

| File | Purpose |
|---|---|
| `README.md` | This file |
| `CONVENTIONS.md` | Full rules and section templates — the system's source of truth |
| `CLAUDE.md` | Auto-loaded by Claude Code when you open this folder — no manual setup needed |
| `project-index.md` | Index of all your documented projects *(auto-updated by `/new-project-intro`)* |
| `my-summary.md` | Your personal career summary *(gitignored — regenerate any time)* |
| `resumes/` | One file per job application *(gitignored)* |
| `.claude/skills/` | Slash command definitions |

---

## When to Use Each Command

### After finishing a new project
```
/new-project-intro /absolute/path/to/your/repo
```
Claude explores the repo, generates a project intro inside it, and adds an entry to `project-index.md`.
Then run `/update-summary` to refresh your personal summary.

### When applying for a new role
```
/new-resume Role: {role title}. Company: {company}.
JD:
{paste full JD here}
```
Creates a new file in `resumes/`. Project intros are never touched.

### When your skills or stack changed significantly
```
/update-summary
```
Re-reads all project intros and overwrites `my-summary.md`.

### After a major architecture change in a project

Open Claude Code in the project repo and ask:
```
Re-explore this repo and update the existing project intro file following the
conventions in {WORK_RECORD_PATH}/CONVENTIONS.md.
Focus on what has changed — cloud architecture, CI/CD, security, or key patterns.
```

---

## Customizing the System

All rules, section templates, and content guidelines live in `CONVENTIONS.md`. Edit it to:
- Add your own project category prefixes
- Change the sections generated in project intros
- Adjust what counts as an "Impressive Outcome" in Key Numbers

---

## License

MIT — see `LICENSE`.
