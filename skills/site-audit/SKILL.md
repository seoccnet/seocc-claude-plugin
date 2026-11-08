---
name: site-audit
description: Read SEOcc's latest site audit (crawl health score, issues by type and severity, affected pages with their crawled title, description, H1, canonical and status) and turn it into exact fixes, plus internal-link, speed and indexing checks. Use when the user asks about the site audit, technical SEO, broken pages, redirects, duplicate titles, noindex, speed or internal links.
argument-hint: "[issue type, e.g. missing_description | redirect_chain]"
---

# Site audit

Follow the `seocc-guide` ground rules. Input: $ARGUMENTS.

The MCP tools never start a crawl. A new audit is started by the user in the dashboard (**Site audit → Start**). It crawls their own site in the background, costs nothing, but does load the site.

## Steps

1. `projects_list`, then `site_audit` without `issue_type`: health score, crawl date, pages checked, issues by type with severity and advice.
2. For each issue type the user cares about: `site_audit` with `issue_type`, `limit` ≤ 50, paging with `offset`. You get each affected URL with status code, redirect target, title, meta description, H1, canonical, noindex and word count as crawled.
3. To compare with an earlier crawl, pass `audit_id` (up to 10 saved runs).
4. Related evidence when it helps:
   - `internal_links` with `url` for links in and out of a page; without `url` for link suggestions.
   - `web_vitals` (field) and `lab_tests` (lab) for `slow_page`. Keep field and lab apart.
   - `browser_audit` for rendered/Lighthouse findings.
   - `indexing_status` for pages that should rank but may not be indexed.

## Fix patterns

| Issue | Fix |
|---|---|
| `missing_title`, `title_too_long`, `title_too_short`, `duplicate_title` | A unique, specific title per URL matching the page and its top query (`page_details`). |
| `missing_description`, `description_too_long`, `duplicate_description` | A unique description that reflects the page and gives a reason to click. |
| `broken_page`, `server_error` | Restore the page or 301 it to the closest live page, then fix internal links pointing to it. |
| `redirect`, `redirect_chain` | Point internal links at the final URL; collapse chains to one 301. |
| `http_url`, `mixed_content` | Force HTTPS; update hard-coded `http://` links and assets. |
| `noindex`, `blocked_by_robots`, `canonical_elsewhere` | Confirm intent first: many are deliberate. |
| `thin_content` | Plan real content with a brief; never pad. |
| `missing_image_alt` | Descriptive alt text; decorative images stay empty. |
| `slow_page`, `large_page` | Compress images, defer scripts; check `web_vitals`. |
| `broken_external_link`, `broken_asset` | Update or remove. |

## Output

One table per issue type: `URL | current value | proposed value | note`. Start with a few high-impact URLs; never propose mass edits. SEOcc never edits the website: the user (or you, if they ask and sign in to their CMS) applies the changes. After they're live, record them with the `change-timeline` skill and ask the user to re-run the audit to confirm.

## Optional write

With `watches:write`, offer `page_watch_set` to watch fixed URLs weekly (title, description, H1, canonical, noindex, status), so regressions raise an alert. Ask first.
