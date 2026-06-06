---
name: upskill
description: Analyze tracked jobs against the candidate profile and produce a prioritized skill-gap report with learning resources. Use when the user asks what to learn next, wants an upskilling plan, or wants a gap analysis for tracked jobs or a specific posting.
---

# Upskill

Use this skill to turn tracked jobs or a single posting into a practical learning plan.

## Load these references first

- `.claude/skills/job-application-assistant/01-candidate-profile.md`
- `.claude/skills/upskill/SKILL.md`
- `job_search_tracker.csv` for aggregate mode
- The most recent file in `upskill/` when you need a diff against the last report

## Modes

- **Aggregate mode**: no URL provided. Analyze tracked jobs from `job_search_tracker.csv`.
- **Targeted mode**: the user provides a single job URL. Fetch it and analyze only that role.

## Workflow

1. Extract required and preferred skills from the posting data you have.
2. Remove anything already covered by the candidate profile, using generous matching.
3. Add synthesized gaps for domain knowledge, tooling, process, soft skills, and credentials when the hard-skill diff misses them.
4. Build a heatmap ranked by priority.
5. For each critical or high-priority gap, use `web_search` with the current year to find 2-3 good learning resources.
6. Write the report to `upskill/` and summarize the study order in chat.

## OpenClaw-specific rules

- Use `web_fetch` for targeted-mode postings.
- Use `web_search` for current resources. Never invent course names, URLs, books, or providers.
- Save every report, even when the summary is also returned in chat.
- In aggregate mode, include a diff from the previous report only when a prior report actually exists.

## Output paths

- Aggregate: `upskill/report-YYYY-MM-DD.md`
- Targeted: `upskill/report-YYYY-MM-DD-<company-slug>-<role-slug>.md`