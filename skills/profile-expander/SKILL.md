---
name: profile-expander
description: Enrich the candidate profile from public sources already linked in the workspace, such as GitHub, portfolio sites, Kaggle, Google Scholar, course pages, or certifications. Use when the user asks to expand the profile, surface hidden skills, scan linked public work, or enrich setup after the base profile is in place.
---

# Profile Expander

Use this skill after the base profile exists and the user wants deeper skill extraction from public sources.

## Load these references first

- `.claude/commands/expand.md`
- `CLAUDE.md`
- `.claude/skills/job-application-assistant/01-candidate-profile.md`
- `.claude/skills/job-application-assistant/02-behavioral-profile.md`

## Workflow

1. Identify which public sources are already linked in the profile.
2. Fetch or search only those public sources.
3. Extract concrete competencies, tools, domains, certifications, or public outputs that are supported by evidence.
4. Propose additive changes before writing them.
5. Label inferred items clearly when they are synthesized rather than explicitly stated.

## OpenClaw-specific rules

- Use `web_fetch` and `web_search` for public-source collection.
- Never invent skills or credentials from vague signals.
- Prefer additive edits over broad rewrites.
- Stop cleanly if the profile does not yet contain public links worth expanding.