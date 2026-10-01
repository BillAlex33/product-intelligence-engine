# Progress

## Current state
Repository initialized with:
- project README
- Claude operating instructions
- master context
- architecture prompt
- agent orchestration design
- daily autonomous run prompt
- initial schemas for drones, smartphones, flashlights and cameras

## Decisions made
- Python-first backend
- PostgreSQL as source of truth
- FastAPI service layer
- Node-RED as orchestration/control plane
- Claude Code CLI for engineering jobs
- Grok API for fresh research jobs
- deterministic Python for validation, normalization, metrics and DB writes
- WordPress as initial publishing layer
- Docker deployment target

## Next highest-value task
Implement the universal PostgreSQL data model and migrations, then expose a minimal FastAPI job API.

## First working vertical slice
One real product category should support:

discovery
→ candidate identity
→ manufacturer specs
→ provenance
→ normalization
→ retailer offer
→ derived metric
→ PostgreSQL persistence
→ job status

Use flashlights only as the first validation dataset because the specs are easy to verify. Do not hard-code flashlight logic into the core engine.

## After that
1. category schema loader
2. product/source/offer models
3. manufacturer ingestion interface
4. retailer offer ingestion
5. derived metric engine
6. review queue
7. Node-RED flow
8. Grok research adapter
9. Claude CLI worker
10. scheduled discovery

## Still open
- WordPress integration method
- first retailer/feed integrations
- VPS provider/size
