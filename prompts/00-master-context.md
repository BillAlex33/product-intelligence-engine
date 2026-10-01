# Master Context

We are building a **general product intelligence and comparison engine**, not a single-category review blog.

The engine should support unrelated categories such as drones, smartphones, cameras, flashlights, laptops, power stations, microphones, headphones, AR glasses and more.

## Core pipeline

category enabled
→ discover products
→ detect new/changed products
→ resolve identity/variants
→ ingest manufacturer specs
→ ingest retailer offers
→ normalize attributes/units
→ validate
→ calculate derived metrics
→ detect interesting comparisons
→ update structured comparison data
→ publish/update pages
→ repeat on schedule

## Data principles

### Product facts
Every spec value needs:
- canonical attribute
- normalized value
- original raw value
- unit
- source URL
- source type
- retrieved_at
- confidence
- source priority

### Prices
Prices are not product specs. Store as offers/time-series:
- retailer
- price
- currency
- availability
- affiliate URL
- region
- checked_at

### Product lifecycle
candidate → verified → published → updated → discontinued

### Category lifecycle
draft schema → reviewed → active → versioned

## Category examples

### Drones
weight, flight time, sensor size, video modes, obstacle sensing, transmission range, wind resistance, storage.

Possible metrics:
- flight_time_per_gram
- sensor_area_per_euro
- range_per_euro
- camera_value_index

### Smartphones
weight, battery, SoC, benchmark, display, storage, RAM, sensor size, zoom, charging.

Possible metrics:
- battery_per_gram
- benchmark_per_euro
- storage_per_euro
- sensor_area_per_euro

### Cameras
sensor area, MP, body weight, IBIS, video modes, dynamic range, weather sealing.

Possible metrics:
- sensor_area_per_gram
- MP_per_euro
- video_capability_per_gram

### Flashlights
lumens, candela, throw, weight, battery, dimensions.

Possible metrics:
- candela_per_gram
- candela_per_euro
- lumens_per_gram
- throw_per_gram

## Automation requirement

Once a category is approved, the system should discover and ingest future products automatically.

Suggested cadence:
- product discovery: daily
- high-value offer refresh: several times/day
- ordinary price refresh: daily
- spec revalidation: weekly or on source change
- comparison regeneration: on meaningful changes
- stale-source audit: weekly

## Publishing philosophy
Do not blindly rewrite full articles every day.
Prefer structured page blocks:
- intro
- live comparison table
- derived rankings
- methodology
- generated commentary
- source freshness

Update only affected blocks when data changes.

## Business model
Potential revenue:
- affiliate links
- display ads
- sponsored placements later
- price alerts
- API/data access
- premium comparison tools

The durable asset is the structured product database and comparison engine.