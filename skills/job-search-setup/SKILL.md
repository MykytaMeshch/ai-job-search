---
name: job-search-setup
description: Onboard or refresh the candidate profile for this job-search workspace. Use when the user wants to set up the repo, import a CV, read the documents folder, answer profile questions, refresh search queries, or update profile sections like skills, experience, or search preferences.
---

# Job Search Setup

Use this skill to populate or refresh the candidate profile in this repository.

## Load these references first

- `.claude/commands/setup.md`
- `CLAUDE.md`
- `documents/README.md`

If the request is a section-only refresh, also load the target files mentioned in `.claude/commands/setup.md`.

## Workflow

1. Follow the three-path setup flow from `.claude/commands/setup.md`:
   - documents-folder ingestion
   - single CV import
   - interview mode
2. Read before writing so repeated setup runs stay idempotent.
3. Surface conflicts explicitly instead of silently choosing between mismatched dates, titles, or degrees.
4. Write only the confirmed profile changes.
5. Finish by confirming which files were populated and what the user should do next.

## OpenClaw-specific rules

- Natural-language requests should trigger this skill, for example: "set up my profile", "read my documents folder", or "update my search queries".
- Use targeted file edits instead of rewriting the whole repo when only one section changes.
- When documents are missing, point the user to `documents/README.md` and stop cleanly instead of guessing.
- Treat `CLAUDE.md` as the canonical candidate profile file for this repository.