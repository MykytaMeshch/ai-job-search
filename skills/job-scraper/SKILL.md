---
name: job-scraper
description: Search for jobs that match this repo's candidate profile, deduplicate results, and present ranked matches. Use when the user asks to find jobs, scrape job boards, check for new roles, or search openings based on the stored profile and query set.
---

# Job Scraper

Use this skill to find new roles for the candidate described in this repository.

## Load these references first

- `.claude/skills/job-scraper/search-queries.md`
- `job_search_tracker.csv`
- `job_scraper/seen_jobs.json` if it exists, otherwise create it with `{ "seen": {} }`
- `.claude/skills/job-application-assistant/01-candidate-profile.md` when you need a quick fit signal

## Workflow

1. Read the query priorities from `.claude/skills/job-scraper/search-queries.md`.
2. Run `web_search` queries against the configured boards and locations.
3. Pre-filter using result titles and snippets before spending `web_fetch` calls.
4. Fetch only promising postings, then extract title, company, location, posting date, deadline, URL, and key requirements.
5. Deduplicate against both `job_scraper/seen_jobs.json` and `job_search_tracker.csv`.
6. Rank new roles as high, medium, or low match.
7. Persist seen jobs back to `job_scraper/seen_jobs.json`.
8. Present only genuinely new roles and ask which ones should be evaluated in depth.

## OpenClaw-specific rules

- Prefer `web_search` and `web_fetch` over any browser-only or Claude-specific tooling.
- If the search is broad or slow, parallelize with multiple tool calls or a spawned helper session, but keep one owner session for the final deduped result.
- Never fabricate postings. Every presented role must come from an actual fetched or searched result.
- Skip expired or obviously closed roles.
- Keep the final answer concise and sorted by fit.

## Data files

- Seen-job state: `job_scraper/seen_jobs.json`
- Manual tracker: `job_search_tracker.csv`
- Query config: `.claude/skills/job-scraper/search-queries.md`