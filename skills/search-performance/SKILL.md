---
name: search-performance
description: Explain the user's search performance from SEOcc (Google Search Console, Bing, GA4 and rankings), including weekly or monthly reviews and diagnosing traffic drops. Use when the user asks how their site is doing, about clicks, impressions, CTR, positions, rankings, or why traffic fell or rose.
argument-hint: "[period, e.g. 28 days | last month | 'why did traffic drop']"
---

# Search performance

Follow the `seocc-guide` ground rules. Input: $ARGUMENTS.

## Review ("how are we doing?")

1. `projects_list`, then `project_overview` for the headline picture and what's connected.
2. `data_quality`: imported-day coverage for Search Console, Bing and GA4. Bing ends about three days before today; a partial last week isn't a drop.
3. `search_performance_summary` for 28 days (default `source=combined`), then 90 days for the trend.
4. `rankings_summary`: winners and losers.
5. `search_queries_list` and `search_pages_list` with small limits: what moved.
6. `project_monitoring`: open alerts.
7. Optionally `analytics_summary` for GA4 organic sessions and key events (check its coverage, currency and timezone), and `forecasts` for what to expect.

Report: what changed, what's a data gap, and three next actions. For a ready-made period report, `seo_report` returns the same weekly or monthly report as the dashboard.

## Diagnose a drop

1. `search_performance_summary` for the period vs the previous one; `include_daily=true` only to see the shape.
2. `search_pages_list` and `search_queries_list`: which pages and queries lost.
3. `annotations_list` for the same dates: was something changed on the site?
4. `page_details` for the biggest loser: traffic comparison, indexing evidence, audit issues, recent notes.
5. Rule out technical causes: `indexing_status` for that URL, and `site_audit` with `issue_type` `noindex`, `canonical_elsewhere`, `blocked_by_robots` or `server_error`.
6. `serp_changes` and `ai_visibility`: did a competitor, a results-page feature or an AI Overview take the clicks?
7. `analytics_summary`: does GA4 agree?

Answer with ranked hypotheses, each with evidence for and against. Name a single cause only when the data supports it, and say what can't be concluded.

## Caveats to repeat

- Combined = Google + Bing clicks and impressions added; position comes from Google.
- Anonymised queries are hidden, so query sums are lower than totals.
- Query and page lists are samples (5,000 rows per engine), not everything.
- GA4 sessions and Search Console clicks aren't the same thing; never subtract one from the other.
