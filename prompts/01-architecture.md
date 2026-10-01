# Architecture Prompt

Design and implement one category-agnostic engine.

## Required entities
- Product
- ProductVariant
- Category
- CategorySchemaVersion
- AttributeDefinition
- ProductAttributeObservation
- CanonicalProductAttribute
- Source
- Retailer
- Offer
- PriceObservation
- DerivedMetricDefinition
- DerivedMetricValue
- ComparisonPage
- ReviewItem
- DiscoveryRun
- IngestionRun

## Requirements
1. PostgreSQL as source of truth.
2. Flexible attributes without turning everything into unvalidated JSON.
3. Keep raw observations and canonical resolved values separately.
4. Preserve provenance.
5. Support units and normalization.
6. Support product variants and regional SKUs.
7. Support time-series prices.
8. Support category-specific formulas.
9. Support idempotent ingestion.
10. Support review queues for ambiguity/conflicts.
11. Support scheduled discovery and refresh jobs.
12. Support WordPress output later without coupling core domain logic to WordPress.

## Deliverables
- architecture diagram
- schema/migrations
- source-trust model
- attribute resolution rules
- formula engine
- ingestion interfaces
- discovery interfaces
- publishing interface
- tests
- docs/progress.md

Keep V1 simple enough to build in about a week.