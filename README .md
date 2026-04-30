# ZopaAI Case Study — Data Foundation

Public German geographic datasets gathered for the ZopaAI case study
(Saarland University, Phase 1 — data foundation).

## Datasets

All public datasets below are sourced from
[suche-postleitzahl.org](https://www.suche-postleitzahl.org/downloads),
which derives them from OpenStreetMap and the German Federal Statistical Office
(Destatis).

### `plz-5stellig.geojson` (9.0 MB)
Polygon boundaries for all ~8,173 German 5-digit postal codes.
- **Format:** GeoJSON FeatureCollection (Polygon / MultiPolygon)
- **Properties per feature:** `plz`, `note`, `einwohner`, `qkm`
- **Use:** main map layer for the application

### `plz_einwohner.csv` (8,170 rows)
Population, area, and centroid per PLZ.
- **Columns:** `plz`, `note`, `einwohner`, `qkm`, `lat`, `lon`
- **Use:** population and density calculations

### `zuordnung_plz_ort.csv` (12,871 rows)
Mapping between PLZ, municipality (Ort), official municipality key (AGS),
district (Landkreis), and federal state (Bundesland).
- **Columns:** `osm_id`, `ags`, `ort`, `plz`, `landkreis`, `bundesland`
- **Use:** bridge table to join municipality-level data (e.g. Destatis / Zensus)
  with PLZ-level data. Note: the relationship is many-to-many.

## Important technical notes

- **PLZ codes must be read as strings, not integers** — leading zeros
  (e.g. `01067`) get stripped if loaded as numbers.
- **PLZ ↔ Municipality is many-to-many** — one PLZ can span multiple
  municipalities and vice versa. Joins must handle this carefully.
- **PLZ count differs slightly between files** (8,170 in CSV vs. 8,173 in
  GeoJSON) — use `LEFT JOIN` semantics on the GeoJSON side so no polygons
  are dropped.

## Data attribution

Data from suche-postleitzahl.org is based on
[OpenStreetMap](https://www.openstreetmap.org) © OpenStreetMap contributors,
licensed under the [Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/).
