---
name: content-brief
description: Plan or improve content for one page with SEOcc evidence (page details, queries, competitors, article ideas, overlap) and read or save SEOcc content briefs. Use when the user asks for a content brief, a writing plan, how to improve a page's content, or to check a brief's claims.
argument-hint: "[page URL or main search]"
---

# Content brief

Follow the `seocc-guide` ground rules. Input: $ARGUMENTS (an existing page URL, or the main search for a new page).

## Gather evidence

1. `projects_list`. For an existing page, `pages_list` to confirm the exact URL, then `page_details`: queries, `click_potential`, `competitor_gap`, `improvements`, cannibalisation, internal-link suggestions and recent change notes.
2. For a new page, `article_ideas` and `keyword_research` for the search, its volume, related searches and competitor pages.
3. `content_briefs_list`: a brief for this URL or search may already exist. If so, `content_brief_details` and build on it.
4. `overlap_review`: make sure the new or updated page won't compete with another page of the site. `content_inventory` with `q` finds drafts or planned pages on the same subject.
5. `internal_links` without `url`, filtered with `q`: pages that should link to this one.

## Write the brief

- Working title and meta description (about 60 and 155 characters).
- Main search and the related searches it should answer, with volumes.
- Outline: H2/H3s covering what competitors cover, plus what they miss. Use the idea's `outline` subtopics and questions when present.
- Internal links in and out, with anchor text.
- Facts that need a source. Never invent figures, prices or claims.

Mark what comes from SEOcc evidence and what's your suggestion. The brief's evidence is a dated snapshot; suggestions aren't measured facts. For an existing brief, `brief_claims` lists claims with missing, own-site or competitor sources: point those out.

## Save (with `briefs:write` and a yes)

- New: `content_brief_create` with `title`, `keyword`, `url` (blank for a new page), `status` `draft`, and `keyword_id` or `opportunity_id` when you have one, so SEOcc captures the evidence.
- Existing: `content_brief_update` with only the changed fields and `expected_version` from `content_brief_details`.

Show the fields first and wait for a yes. Without the scope, give the user the text to paste on the **Content briefs** page. When the content is published, the next step is a timeline note (`change-timeline` skill).
