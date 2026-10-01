# Daily Autonomous Run

Inspect the repository and `docs/progress.md`.

Continue the highest-value unfinished work without rebuilding systems that already exist.

For each active category:

1. discover newly released products,
2. compare against existing identities,
3. deduplicate models and regional variants,
4. fetch authoritative manufacturer specs,
5. fetch retailer offers/prices,
6. store raw values + normalized values + source + timestamp,
7. validate required fields,
8. recalculate derived metrics,
9. identify affected comparison pages,
10. update structured page data,
11. flag conflicts for review,
12. log what changed.

## Rules
- Never fabricate missing values.
- Prefer structured sources over scraping.
- Do not silently resolve conflicts.
- Do not publish uncertain product identities.
- Make every job retry-safe and idempotent.
- Update `docs/progress.md` after work.

## Priority order when nothing is queued
1. correctness/provenance bugs
2. product identity & deduplication
3. ingestion reliability
4. price freshness
5. derived metrics
6. comparison page generation
7. SEO/publishing improvements
8. new categories
