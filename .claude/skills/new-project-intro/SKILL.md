---
name: new-project-intro
description: Explore a project repo, generate a project intro file, and add an entry to project-index.md. Usage: /new-project-intro {absolute-repo-path}
---

Explore the repo at the path provided and generate a project intro file following the conventions in `{WORK_RECORD_PATH}/CONVENTIONS.md`.

Then add a new entry for it in `{WORK_RECORD_PATH}/project-index.md`.

## Input collection

Arguments provided: $ARGUMENTS

If a repo path is missing from the arguments above, ask the user before doing anything else:

1. Ask: "Which repo should I document? Please provide the absolute path (e.g. /absolute/path/to/your/repo)"
2. Wait for the user's reply, then proceed.
