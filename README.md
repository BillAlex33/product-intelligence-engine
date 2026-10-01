# Product Intelligence Engine

Automated, multi-category product intelligence, comparison, pricing and publishing engine.

## Goal
Build one category-agnostic engine that can continuously discover products, ingest authoritative specs, track current prices, calculate useful category-specific metrics, and publish/update comparison content.

Examples of supported categories:
- drones
- smartphones
- cameras
- lenses
- flashlights
- power stations
- laptops
- AR glasses
- audio gear

## Core rule
This is **not** a collection of hard-coded niche sites. The core engine stays generic; category-specific behavior lives in schemas, metric definitions, validation rules and prompts.

## Start here
Claude Code should read:
1. `CLAUDE.md`
2. `prompts/00-master-context.md`
3. `prompts/01-architecture.md`
4. `prompts/12-daily-autonomous-run.md`

## MVP target
- 3+ categories from day one
- 30–50 products/category
- manufacturer specs with provenance
- multiple retail offers where possible
- automatic product discovery
- price refresh
- derived metrics
- comparison pages
- WordPress-ready publishing pipeline

## Status
Initial architecture/prompts seeded. Next step: implement data model + first ingestion pipeline.