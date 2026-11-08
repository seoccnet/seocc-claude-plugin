---
name: article-ideas
description: Pick what to write next from SEOcc's article ideas (new articles and updates, with predicted traffic, difficulty, competitor coverage, outlines and markets), topic plans and published-article tracking. Use when the user asks what to write, for content ideas, a content plan, or whether published articles met their predictions.
argument-hint: "[topic or market]"
---

# Article ideas

Follow the `seocc-guide` ground rules. Input: $ARGUMENTS.

## Steps

1. `projects_list`, then `article_ideas` (paged with `offset`/`limit`). Note `built_at`, `last_lookup` and `markets`. If there are no ideas, the competitor lookup hasn't run: it's a paid lookup the user starts on the **Article ideas** page, which shows `estimated_cost` first. Don't start or promise it.
2. For each idea read `kind` (`new` or `update`), `main_keyword`, `volume`, `prediction` (traffic low/expected/high, difficulty with reasons, backlinks, months), `score`, `reasons`, `competitors` and `your_page`.
3. `inventory` on an idea means a draft or page already covers its search: suggest updating that instead of writing a duplicate. Check `overlap_review` with `kind=synonym_ideas` for ideas on the same subject in other words.
4. `content_briefs_list`: is a brief already planned?
5. `topic_plans`: does the idea belong to a pillar plan? Prefer ideas that complete a plan.
6. `published`: how earlier articles from ideas did against their predictions. Use that to say how far to trust the new predictions.

## Markets

An idea in several markets is the same search in the same language, so its volume and traffic add the markets up; `markets[]` gives the split. Ideas in different languages are never joined. Mention `skipped_markets` when they matter.

## Output

Recommend five ideas at most, best first:

| Idea | New/update | Main search (volume) | Expected traffic (range) | Difficulty | Why now | Already covered? |
|---|---|---|---|---|---|---|

Predictions are ranges with stated bases, not promises. Give the low/high, not just the expected value. Keep competitor URLs as evidence; don't copy their content.

## Next step

Offer to turn the chosen idea into a brief with the `content-brief` skill. The detailed outline (subtopics, questions, competitor headings) is `outline` on the idea; it's null until the user opens it in the dashboard.
