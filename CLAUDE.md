# Claude Operating Instructions

You are the implementation agent for **Product Intelligence Engine**.

Read `prompts/00-master-context.md` before substantial work.

## Mission
Build a category-agnostic product intelligence platform that can move from one category to another without rewriting the core application.

The system must continuously:
1. discover new products,
2. identify/deduplicate models and regional variants,
3. ingest authoritative specs,
4. ingest current retail offers/prices,
5. preserve provenance and timestamps,
6. normalize units,
7. calculate category-specific derived metrics,
8. update comparisons and ranking pages,
9. surface conflicts for review,
10. publish/update content safely.

## Non-negotiable rules
- Never invent a product specification.
- Every factual value must retain source URL, timestamp and raw value.
- Prefer manufacturer sources for technical specs.
- Keep retail offers/prices separate from canonical specs.
- Store conflicting values; do not silently overwrite.
- Treat prices as time-series data.
- Core engine must remain category-independent.
- Category-specific logic belongs in schemas/config/metric definitions.
- New products in an approved category should be ingestible with minimal human intervention.
- Major ambiguity, identity conflict, or unsupported claims go to a review queue.
- Prefer APIs, feeds, JSON-LD and structured data before browser automation.
- Use Playwright only when necessary.

## Preferred stack
- PostgreSQL
- Python
- FastAPI
- Node-RED for orchestration
- Claude Code CLI for engineering tasks
- xAI/Grok API for fresh research tasks
- Playwright when required
- Docker
- GitHub
- WordPress initially

## Agent orchestration
The human should not need to manually move information between Claude and Grok.

- Node-RED is the control plane.
- Claude Code CLI runs against the local checkout for engineering work.
- Grok is called via API for live research and returns structured JSON.
- Python performs deterministic validation, normalization, scoring and DB writes.
- PostgreSQL stores runtime state.
- GitHub stores code, prompts, schemas and documentation.

Claude should operate from the repository and job payloads, not pasted chat context.

## Implementation style
- Do not over-engineer V1.
- Build small, testable modules.
- Preserve source provenance everywhere.
- Add migrations and tests as the schema evolves.
- Keep category schemas versioned.
- Make ingestion idempotent.
- Make scheduled refresh jobs retry-safe.
- Keep business logic out of Node-RED.
- Treat Node-RED as an orchestrator, not the intelligence layer.

## Initial categories
- drones
- smartphones
- flashlights
- cameras

## First implementation milestone
Create:
1. universal database schema,
2. category schema loader,
3. product/source/offer models,
4. first manufacturer ingestion path,
5. first retailer offer path,
6. derived metric engine,
7. candidate/review workflow,
8. Node-RED-triggerable job API.

After each meaningful change, update `docs/progress.md` with:
- what changed
- what works
- what is blocked
- next highest-value task
