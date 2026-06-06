# AGENTS.md - AI Job Search Workspace

This repo is a candidate-centric job search workspace.
Use it to profile the candidate, evaluate postings, tailor CVs and cover letters, search for jobs, and track skill gaps.

## Session startup

1. If candidate-specific OpenClaw files exist (`USER.md`, `MEMORY.md`, `memory/YYYY-MM-DD.md`, etc.), use that startup context first.
2. Read `CLAUDE.md` for the candidate profile and the verification checklist.
3. Load only the task-specific references you need:
   - Profile setup or refresh: `.claude/commands/setup.md`
   - Profile expansion from public sources: `.claude/commands/expand.md`
   - Job evaluation and application drafting: `.claude/commands/apply.md`
   - Search workflow: `.claude/skills/job-scraper/SKILL.md` and `.claude/skills/job-scraper/search-queries.md`
   - Upskilling workflow: `.claude/skills/upskill/SKILL.md`
   - Dangerous cleanup/reset work: `.claude/commands/reset.md`

## OpenClaw-first guidance

- Prefer the repo-local `skills/` directory when a matching skill exists. Those skills are OpenClaw-native wrappers around this repo's existing reference files.
- OpenClaw does not need Claude slash commands. Natural requests like "evaluate this posting", "search for new jobs", or "build an upskilling plan" should trigger the same workflows.
- Use `sessions_spawn` for fresh-context reviewer passes instead of Claude's Agent tool.
- Use `web_fetch` and `web_search` for company and posting research.
- Use `exec` for deterministic local steps like salary lookup and LaTeX compilation.

## Non-negotiables

- Never fabricate skills, experience, dates, education, or achievements.
- Verify every company-specific claim before adding it to a cover letter.
- Evaluate fit before drafting unless the user explicitly asks to skip that step.
- Compile generated LaTeX and inspect the PDFs before presenting final application files.
- Keep personal outputs uncommitted by default (`cv/main_*.tex`, `cover_letters/cover_*.tex`, tracker data, reports, documents/ contents).
- Ask before destructive resets or deleting user data.

## Key files

- `CLAUDE.md` - canonical candidate profile and verification checklist
- `.claude/commands/apply.md` - full drafter-reviewer application workflow
- `.claude/commands/setup.md` - onboarding and profile population flow
- `.claude/commands/expand.md` - profile enrichment from linked public sources
- `.claude/skills/job-application-assistant/` - evaluation, writing, CV, cover letter, and interview references
- `.claude/skills/job-scraper/` - search workflow and query configuration
- `.claude/skills/upskill/` - gap analysis and learning-plan workflow
- `cv/` and `cover_letters/` - generated LaTeX output
- `documents/` - user-provided source material
- `job_scraper/` and `upskill/` - generated search/upskilling state

## Commit hygiene

When changing the framework itself, commit docs, prompts, skills, and tooling changes together.
Do not commit personal candidate data or generated application artifacts unless the user explicitly asks for that.