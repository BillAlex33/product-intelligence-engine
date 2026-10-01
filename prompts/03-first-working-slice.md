# First Working Vertical Slice

Implement a real end-to-end slice before adding more architecture.

## Goal
Prove that one category can flow from raw source to structured comparable data while keeping the core generic.

Use flashlights as the initial validation dataset only because attributes such as lumens, candela, throw and weight are easy to verify.

Do NOT hard-code flashlight fields into core product tables or service logic.

## Implement

### 1. PostgreSQL data model
At minimum:
- categories
- category_schema_versions
- products
- product_variants
- sources
- attribute_definitions
- product_attribute_observations
- canonical_product_attributes
- retailers
- offers
- price_observations
- derived_metric_definitions
- derived_metric_values
- review_items
- jobs
- agent_runs

### 2. FastAPI service
Endpoints:
- POST /jobs
- GET /jobs/{job_id}
- POST /products/candidates
- GET /products/{product_id}
- POST /products/{product_id}/observations
- POST /products/{product_id}/recalculate

### 3. Category schema loader
Load versioned JSON schemas from /schemas.
Validate schema structure with Pydantic.

### 4. Provenance
Every observation must retain:
- raw value
- normalized value
- unit
- source URL
- source type
- retrieval timestamp
- confidence

### 5. Derived metrics
Implement formula evaluation safely.
For flashlights support initial metrics such as:
- candela_per_gram
- lumens_per_gram
- throw_per_gram

The formula engine must remain generic.

### 6. Tests
Add tests proving:
- category schemas load
- observations preserve provenance
- unit normalization works
- derived metric calculations work
- invalid/missing required values are flagged
- idempotent reprocessing does not duplicate observations

### 7. Local development
Add Docker Compose for:
- PostgreSQL
- FastAPI service

Do not add Node-RED to Docker Compose until the API slice works.

### 8. Documentation
Update docs/progress.md with:
- what was implemented
- commands to run locally
- tests
- known gaps
- next task

## Acceptance criteria
A test fixture representing a real flashlight can be inserted with sourced observations, normalized, persisted, and have derived metrics calculated without any flashlight-specific database columns.
