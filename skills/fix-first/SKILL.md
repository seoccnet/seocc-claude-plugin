---
name: fix-first
description: Build a prioritised, per-URL fix list for the user's website from SEOcc data (site audit, opportunities, page improvements and existing team tasks). Use when the user asks what to fix on their site, what to do first, or for an SEO to-do list.
argument-hint: "[project name or page URL]"
---

# What should I fix first?

Follow the `seocc-guide` ground rules. Input: $ARGUMENTS (a project, a page URL, or nothing).

## Steps

1. `projects_list`, then confirm the project.
2. `data_quality`: note stale or missing datasets so you don't present gaps as health.
3. `site_audit` without `issue_type`: health score, crawl date, issues by severity and page count. If the crawl is old, say so.
4. For the two or three most severe issue types: `site_audit` with `issue_type` and `limit` ≤ 50 to get exact URLs and their current title, description, H1, canonical, status and noindex.
5. `opportunities_list` with `status=open`, `limit=15`: read each finding's score breakdown and action plan. Quick wins (`quick_win`, `low_ctr`) often beat bigger projects.
6. `seo_tasks_list`: skip anything the team already planned, and mention it as "already assigned to …".
7. If one page dominates, run `page_details` on it and use its ordered `improvements`.
8. `annotations_list` for the last 60 days, so you don't propose undoing a recent change.

## Output

Lead with the top three actions. Then one table, at most 15 rows, most important first:

| # | URL | Problem (evidence) | Current value | Proposed change | Effort |
|---|---|---|---|---|---|

Rules for proposals:

- Titles about 60 characters or fewer, descriptions about 155. These are guidance; the audit's own rules decide what's flagged.
- Stay faithful to the page. Don't keyword-stuff, and don't invent claims, prices or stock.
- `noindex`, `blocked_by_robots` and `canonical_elsewhere` can be deliberate. Ask before proposing removal, and check `indexing_status`.
- Mark each row as evidence-backed or your judgment.

End with the follow-up loop: after a fix is live, record it on the timeline (`change-timeline` skill), re-run the site audit in the dashboard, and review impact after 28 days.

## Optional writes (ask first)

With `tasks:write`, offer to create tasks for the unassigned rows with `seo_task_save`, one per finding. Show assignee, due date, URL and notes first, and wait for a yes. Mark a finding `done` with `opportunity_set_status` only after the fix is live and the user agrees: "done" doesn't prove it's fixed.
