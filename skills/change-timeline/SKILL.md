---
name: change-timeline
description: Record SEO changes on SEOcc's change timeline and judge whether past changes worked (before/after impact, measurement plans, what-worked ledger). Use when the user made or plans a site change, asks "did my change work?", wants a timeline of improvements, or asks what has worked so far.
argument-hint: "[page URL or change]"
---

# Change timeline and impact

Follow the `seocc-guide` ground rules. Input: $ARGUMENTS.

The timeline is the project's memory: what changed on the site and when. Every later review depends on it.

## Read the timeline

- `annotations_list` with `from`/`to` or an exact `url` (also returns site-wide notes). Check it before recommending anything, so you don't redo a change or credit the wrong edit.
- `page_changes`: changes SEOcc's page monitoring detected on watched pages (field-by-field before and after). A detected change without a note is a reason to suggest one.

## Record a change (with `annotations:write` and a yes)

Record only changes that are **live**, never planned ones. One note per logical change.

| Field | Rule |
|---|---|
| `date` | The real go-live date, YYYY-MM-DD in UTC. Not today by default, never in the future. |
| `type` | `title` (title/snippet), `content`, `links` (internal links), `technical` (canonical, robots, redirects, schema), `release` (deploy), `other`. |
| `title` | ≤120 characters and specific, such as "Rewrote title and description of /tomato-seeds for 'buy tomato seeds'". Not "SEO update". |
| `url` | The exact page on the project domain; blank for a site-wide change. |
| `note` | ≤2,000 characters: old → new, why, and when to review. No secrets or private data. |

Call `annotation_create` with a fresh `client_request_id`. With a `url`, SEOcc also drafts a measurement plan and freezes its baseline (pass `measure: false` to skip). Fix a mistake with `annotation_update` and `expected_version`; don't add a duplicate. Without the scope, give the user the values for the **Change timeline** page.

For a batch of fixes, prepare a table of all notes, get approval, then create them one by one and check each result.

Habits that keep results readable: space related changes on one URL at least one window (14 or 28 days) apart; record site-wide changes (theme, robots, sitemap, migration) as site-wide notes; put the hypothesis and review date in the note.

## Judge a change

1. Find the note's `annotation_id` with `annotations_list`.
2. `seo_change_impact` with `days` 28 (14 for quick checks, 90 for slow pages).
3. Report the observed direction (improved, declined, mixed, unchanged, insufficient data), the coverage and quality flags, the other notes in the windows, and the `measurement_plan` result if there is one (`attribution` says controlled or association).
4. If the after-window hasn't fully passed: "too early, check again on <date>".

It's not a significance test. Without a control group it's association, not proof.

## What worked so far

`what_worked` summarises measured changes by kind and plan (improved, declined, unchanged, insufficient, median effect) and lists reminders: plans without a frozen baseline, and page changes without a plan. Use it for "what kind of changes work on our site?", and say how many changes each conclusion rests on.
