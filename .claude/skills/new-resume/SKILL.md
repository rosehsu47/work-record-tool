---
name: new-resume
description: Create a resume file for a specific role by mapping JD requirements to project evidence. Usage: /new-resume Role: {title}. Company: {name}. JD: {paste JD}
---

Create a resume file following the conventions in `{WORK_RECORD_PATH}/CONVENTIONS.md`.

Read all project intros listed in `{WORK_RECORD_PATH}/project-index.md` for evidence.

Save the result to `{WORK_RECORD_PATH}/resumes/`.

## Input collection

Arguments provided: $ARGUMENTS

If Role, Company, or JD are missing from the arguments above, collect them interactively **before** doing any file reads or generation:

1. If Role is missing → ask: "What is the role title? (e.g. Cloud Engineer)"
2. Wait for the user's reply, then if Company is missing → ask: "Which company is this for? (or type 'general')"
3. Wait for the user's reply, then if JD is missing → ask: "Please paste the job description."
4. Wait for the user's reply.

Once all three are confirmed, proceed with reading the project intros and generating the resume.
