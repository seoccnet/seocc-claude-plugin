---
name: opportunities
description: Review SEOcc's prioritised SEO opportunities and the team's tasks, explain why each finding scores as it does, and (with permission) assign tasks or change finding status. Use when the user asks about opportunities, quick wins, priorities, a team to-do list, or whether completed work paid off.
argument-hint: "[type, e.g. quick_win | content_gap | page URL]"
---

# Opportunities and team tasks

Follow the `seocc-guide` ground rules. Input: $ARGUMENTS.

## Read

1. `projects_list`, then `opportunities_list` with `status=open` and `limit=15`. Filter with `type` (such as `quick_win`, `low_ctr`, `ranking_decline`, `content_gap`, `keyword_gap`, `competitor_gap`, `link_building`, `not_linked`, `content_refresh`), `page_url`, `effort` or `verdict` when the user narrows it.
2. For the findings you recommend, call `opportunities_list` with `opportunity_id` to get the calculation, coverage, supporting signals and action plan. Each has a `score_breakdown` (demand, relevance, impact, confidence, effort, risk, evidence). Explain the score from those factors, not from intuition.
3. `seo_tasks_list` (optionally `overdue`): who already owns what.
4. `opportunity_outcomes`: how earlier completed findings turned out, predicted vs observed. Use it to calibrate how much to trust similar findings.

`priority` means "review earlier", not "bigger ranking impact". An action plan's `tested` label says how well tested that kind of change is; repeat it.

## Present

Group as **do now** (high score, low effort, not assigned), **plan** (bigger work, suggest a brief or task), and **skip or snooze** (low relevance, high zero-click risk, `reconsider` verdict). One line of evidence each.

## Write (only with the scope and a yes)

- **Assign a task** (`tasks:write`): `seo_task_save` with `opportunity_id`, `status` (`todo`, `in_progress`, `done`), `assignee_id` (a member with edit access, from `seo_tasks_list`), `due_date` (project timezone), `url` and `notes`; `expected_version` 0 creates. One finding = one task.
- **Change finding status** (`opportunities:write`): `opportunity_set_status` with `open`, `done`, `dismissed` or `snoozed` plus `snooze_until`, and `expected_status` from your read. Task status and finding status are separate: don't mix them. "Resolved" is set by SEOcc when the rule no longer fires.
- **Confirm an outcome** (`opportunities:write`): `opportunity_outcome_confirm` with `implemented` true or false, only when the user knows.

Show the exact values and wait for a yes before each write. Use a fresh `client_request_id`. Never bulk-close findings to "clear the list".
