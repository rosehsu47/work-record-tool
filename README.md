# 🧠 Work Record

An AI-powered developer memory system for documenting, structuring, and reusing your past projects.

Built on Claude Code, it reads your repositories, extracts real implementation details, and turns them into structured interview references, resume content, and a cohesive personal narrative — all as Markdown files you own and version-control.

> Stop guessing how to describe your work. Let your code speak for itself.

---

## ✨ What This Solves

Most engineers don’t struggle with building —  
they struggle with **explaining what they built**.

- You forget implementation details over time  
- You can’t clearly articulate system design in interviews  
- Writing resumes becomes repetitive and inconsistent  

This system fixes that by maintaining a **living, structured record of your work**, extracted directly from your codebase — not written from memory.

---

## 💡 Vision

This project explores a simple idea:

> Your code already contains your experience.
> You just need a system to extract and reuse it.

Work Record turns your repositories into a **developer memory layer** —
so you don’t just build projects, you **retain and leverage them**.

---

## ⚙️ What It Generates

Three types of documents, each with a clear responsibility:

| Document | Purpose | Location |
|--------|--------|--------|
| `{category}_project_intro_{name}.md` | Architecture, CI/CD, security, talking points | Inside each project repo |
| `my-summary.md` | Aggregated skills, experience, personal intro | This folder |
| `resumes/resume-{role}-{date}.md` | Job-specific mapping, narrative, tailored intro | `resumes/` |

---

## 🧠 Core Design Principle

Project documentation and job applications should **never be mixed**.

- **Project intros** = timeless, factual system knowledge  
- **Resumes** = context-specific storytelling for one role  

This separation ensures your source of truth stays clean, reusable, and future-proof.

---

## 🚀 Quick Start

### 1. Create your own copy

Click **Use this template** on GitHub, then:

```bash
git clone https://github.com/{you}/work-record-tool.git
cd work-record-tool
````

---

### 2. Set your path (one-time setup)

Replace `{WORK_RECORD_PATH}` with your local path:

```bash
WORK_RECORD_PATH=$(pwd) && grep -rl '{WORK_RECORD_PATH}' . --include="*.md" | xargs sed -i '' "s|{WORK_RECORD_PATH}|$WORK_RECORD_PATH|g"
```

(Linux: remove `''` after `-i`)

---

### 3. Open Claude Code

```bash
claude .
```

---

### 4. Document your first project

```bash
/new-project-intro /absolute/path/to/your/repo
```

Claude will:

* Explore the repo
* Generate a structured project intro
* Register it in `project-index.md`

---

### 5. Generate your personal summary

```bash
/update-summary
```

---

### 6. Create a resume for a job

```bash
/new-resume Role: Backend Engineer. Company: ABC.
JD:
{paste the full job description here}
```

---

## 🔄 How It Works

```
/new-project-intro {repo-path}
       │
       ▼
project_intro.md         ← timeless system knowledge (per project)
       │
       ├──────────────▶ my-summary.md        (/update-summary)
       │                     aggregated skills & narrative
       │
       └──────────────▶ resume.md            (/new-resume)
                             job-specific mapping & storytelling
```

**Rule:**
Never put JD-specific content into project intros.
Always generate a new resume file instead.

---

## 📂 Project Structure

| File             | Purpose                             |
| ---------------- | ----------------------------------- |
| README.md        | This file                           |
| CONVENTIONS.md   | System rules and templates          |
| CLAUDE.md        | Auto-loaded context for Claude Code |
| project-index.md | All tracked projects                |
| my-summary.md    | Personal summary (gitignored)       |
| resumes/         | One file per application            |
| .claude/skills/  | Command definitions                 |

---

## 🎯 When to Use Each Command

### After finishing a project

```bash
/new-project-intro /path/to/repo
```

→ Generates project intro + updates index
→ Then run `/update-summary`

---

### When applying for a job

```bash
/new-resume Role: {role}. Company: {company}.
JD:
{job description}
```

→ Creates a new resume file

---

### When your experience evolves

```bash
/update-summary
```

→ Rebuilds your personal narrative
(Regenerate `my-summary.md` from all projects listed in `{WORK_RECORD_PATH}/project-index.md`, following the conventions in `{WORK_RECORD_PATH}/CONVENTIONS.md`.)

---

## 🛠 Customization

All generation rules live in `CONVENTIONS.md`.

You can:

* Change section structures
* Redefine what counts as “impact”

---

## 🤖 Using with Other AI Tools

The generated `my-summary.md` is designed to be portable.

You can directly copy its content into other AI tools (e.g. ChatGPT, Gemini) to:
- Refine wording and tone  
- Adapt content for different roles  
- Improve storytelling and flow  

This makes it easy to turn structured facts into polished narratives without rewriting everything from scratch.

---

## 📦 Version

### v0.1.0 — Initial Release

Focused on quickly extracting and structuring key technical details from your projects — making it easier to recall what you built and talk about it with clarity.

---

## 📄 License

MIT — see LICENSE.
