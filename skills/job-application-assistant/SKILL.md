---
name: job-application-assistant
description: Evaluate job postings, tailor CVs, draft cover letters, and prepare interview material for this repo's candidate profile. Use when the user asks to assess a role, apply to a job, rewrite a resume/CV, write a cover letter, or prepare for an interview in this workspace.
---

# Job Application Assistant

Use this skill for role evaluation, application drafting, and interview prep inside this repository.

## Load these references first

- `CLAUDE.md`
- `.claude/skills/job-application-assistant/01-candidate-profile.md`
- `.claude/skills/job-application-assistant/02-behavioral-profile.md`
- `.claude/skills/job-application-assistant/03-writing-style.md`
- `.claude/skills/job-application-assistant/04-job-evaluation.md`
- `.claude/skills/job-application-assistant/05-cv-templates.md`
- `.claude/skills/job-application-assistant/06-cover-letter-templates.md`
- `.claude/skills/job-application-assistant/07-interview-prep.md`

For the full end-to-end drafter-reviewer flow, also read `.claude/commands/apply.md`.

## Core workflow

1. Fetch the job posting with `web_fetch` if the user gives a URL. If the fetch is blocked, ask for pasted text.
2. Evaluate fit before drafting. Cover skills match, experience match, behavioral match, optional salary benchmark, and an overall recommendation.
3. If the user wants documents, write a tailored CV in `cv/` and a tailored cover letter in `cover_letters/`.
4. Run a fresh-context review pass with `sessions_spawn` and pass the drafts inline. Keep the reviewer focused on content critique, not LaTeX structure.
5. Apply revisions without inventing facts.
6. Compile the CV with `lualatex` and the cover letter with `xelatex` via `exec`, then inspect the resulting PDFs before presenting them.

## OpenClaw-specific rules

- Use `sessions_spawn` instead of Claude's Agent tool for the reviewer step.
- Use `web_search` and `web_fetch` to verify company-specific claims before they land in the letter.
- Use `exec` for salary lookup when `salary_data.json` exists:

```bash
python salary_lookup.py "<Company Name>" --json
```

Add `--city "<City>"` when the posting makes city-specific salary filtering useful.

## Quality bar

- Never fabricate skills, education, achievements, dates, or company details.
- Keep the CV in English unless the user explicitly wants otherwise.
- Match the cover letter language to the posting.
- Mention **Claude Code** by name only when the application itself references agentic coding or AI tooling.
- Re-run LaTeX until the CV is exactly 2 pages and the cover letter is exactly 1 page.
- Trust the PDF, not the `.tex` source.

## Output paths

- CV: `cv/main_<company>.tex`
- Cover letter: `cover_letters/cover_<company>_<role>.tex`
- Interview prep can be returned in chat unless the user asks for a saved file.