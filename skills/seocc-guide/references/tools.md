# SEOcc MCP tools and scopes

A token only lists and allows the tools its scopes cover. Read scopes cover stored data. Write scopes are opt-in and never delete or spend money. Every project tool takes `project_id`.

If a tool is missing, ask the user to create a new token with the scope (SEOcc: **Integrations → AI access → New token**). Existing tokens never gain scopes.

## Read scopes

### `projects:read`
| Tool | Use it for |
|---|---|
| `projects_list` | Always first: project IDs and domains. |
| `project_overview` | Headline numbers for every section the token can read. |
| `project_monitoring` | Alerts, report schedule, integration health, IndexNow state (alerts need `opportunities:read`). |
| `data_quality` | Which datasets are available, stale, partial or missing, and import coverage. Check it before comparing periods. |
| `annotations_list` | The SEO change timeline (25 per page; optional `from`/`to`, exact `url`). |
| `seo_report` | The weekly or monthly report; each section needs its own scope. |
| `guide_list`, `guide_search`, `guide_read` | The official SEOcc user guide. |

### `search:read`
| Tool | Use it for |
|---|---|
| `search_performance_summary` | Clicks, impressions, CTR, position vs the previous period. `days` 7–486 or `from`/`to`; `source` `combined` (default), `google`, `bing`; `include_daily` opt-in. |
| `search_queries_list`, `search_pages_list` | Top queries and pages. Combined lists are bounded at 5,000 rows per engine: a sample, never everything. |
| `search_segments` | Search performance split into segments. |
| `forecasts` | 7/14/28-day forecasts with intervals, or the reason there is none. |

### `keywords:read`
| Tool | Use it for |
|---|---|
| `keywords_list` | Tracked keywords with volume, CPC and competition. |
| `keyword_research` | Stored research: what you and competitors rank for, gaps, ideas, relevance. |
| `research_on_file` | Which lookups and analyses exist and how fresh they are. |
| `article_ideas` | Up to 50 article ideas (new or update), predictions, outlines, markets, and published-article tracking. |
| `topic_plans` | Pillar/cluster plans with planned internal links and backlinks. |
| `clusters_list`, `cluster_get` | Topics and which page owns each. |
| `investigations_list`, `investigation_get` | Saved research notebooks. |

### `rankings:read`
| Tool | Use it for |
|---|---|
| `rankings_summary` | Visibility, average position, top 3/top 10, winners and losers. |
| `keyword_history` | One keyword's position history. |
| `serp_changes` | Stored results-page changes: new competitors, features, your URLs. |
| `ai_visibility` | AI Overview citations, ChatGPT/Gemini/Perplexity mentions, crawler access, citation readiness. Name and domain counts overlap: never add them. |
| `local_rankings` | Google Maps positions, grid, branches, profile checks; review texts opt-in. |

### `competitors:read`
| Tool | Use it for |
|---|---|
| `competitors_list`, `competitor_compare` | Competitor visibility and where they lead. |
| `backlinks` | Link profile, new and lost links, link gap (1,000-link sample). |

### `opportunities:read`
| Tool | Use it for |
|---|---|
| `opportunities_list` | Prioritised findings with score breakdown and action plan. Filters: `status`, `type`, `page_url`, `effort`, `verdict`, `zero_click`; `opportunity_id` for one finding's detail. |
| `opportunity_outcomes` | Checkpoints of completed findings: predicted vs observed. |
| `seo_tasks_list` | The team's tasks: assignee, due date, progress, overdue. |
| `site_audit` | Latest crawl: health score and issues; with `issue_type`, the affected pages with status, title, description, H1, canonical, noindex and word count as crawled. `audit_id` picks an older run. |
| `browser_audit` | Saved rendered/Lighthouse findings. |

### `pages:read`
| Tool | Use it for |
|---|---|
| `pages_list` | Known URLs. Get the exact URL here first. |
| `page_details` | Everything about one URL, including an ordered `improvements` list, click potential, competitor gap, indexing and change results. |
| `indexing_status` | Saved Google URL inspection for one exact URL. |
| `internal_links` | Links in/out of a page, or link suggestions. |
| `content_inventory` | One row per page address across CMS, crawl, sitemap and Search Console. |
| `overlap_review` | Near-duplicates and pages competing for the same searches. |
| `content_briefs_list`, `content_brief_details` | Saved writing plans with their dated evidence. |
| `brief_claims` | Factual claims on briefs with source checks. |
| `analytics_summary` | GA4 organic landing-page outcomes and AI-assistant referrals. |
| `business_measurement` | Whether business events are measured. |
| `web_vitals`, `lab_tests` | CrUX field data and saved lab (Lighthouse) tests, kept apart. |
| `page_changes` | Watched pages and detected field changes. |
| `change_bundles` | Planned and deployed change bundles with verification. |
| `seo_change_impact` | Before/after for one change note (`days` 14, 28 or 90). Site-wide results also need `search:read`. |
| `what_worked` | Results ledger of measured changes. |

## Write scopes (opt-in)

| Scope | Tools | Notes |
|---|---|---|
| `annotations:write` | `annotation_create`, `annotation_update` | Fields: `date` (YYYY-MM-DD UTC, not future), `type` (`title`, `content`, `links`, `technical`, `release`, `other`), `title` ≤120, `url` (blank = site-wide), `note` ≤2,000. With a `url`, create also drafts a measurement plan unless `measure: false`. |
| `tasks:write` | `seo_task_save` | `opportunity_id`, `status` (`todo`, `in_progress`, `done`), `assignee_id`, `due_date`, `url`, `notes`, `brief_id`, `annotation_id`; `expected_version` 0 creates. |
| `briefs:write` | `content_brief_create`, `content_brief_update` | `title`, `keyword`, `url` (blank = new page), `status` (`draft`, `in_progress`, `published`), optional `keyword_id`, `opportunity_id`. |
| `opportunities:write` | `opportunity_set_status`, `opportunity_outcome_confirm` | Status `open`, `done`, `dismissed`, `snoozed` (+ `snooze_until`); guarded by `expected_status`. |
| `watches:write` | `page_watch_set` | 1–50 `urls`, `enabled` true/false; workspace limit applies. |
| `keywords:write` | `keyword_set_relevance` | Up to 50 keywords: relevant, not relevant or auto. |
| `clusters:write` | `cluster_set_owner` | Set or clear the page that owns a topic. |
| `investigations:write` | `investigation_save`, `investigation_add` | Research notebooks. |

All writes accept `client_request_id` for safe retries and take the version from your latest read.

Tool details change between SEOcc versions. When in doubt, trust the tool's own description and input schema over this file.
