# ZopaAI Case Study Data Foundation

Public German geographic datasets gathered for the ZopaAI case study at Saarland University. This is Phase 1, the data foundation.

## Datasets

All public datasets below are sourced from suche-postleitzahl.org, which derives them from OpenStreetMap and the German Federal Statistical Office (Destatis).

### `plz-5stellig.geojson` (9.0 MB)

Polygon boundaries for all roughly 8,173 German 5-digit postal codes. The file is a GeoJSON FeatureCollection with Polygon and MultiPolygon geometries, and each feature carries the properties `plz`, `note`, `einwohner`, and `qkm`. This will serve as the main map layer for the application.

### `plz_einwohner.csv` (8,170 rows)

Population, area, and centroid per PLZ. The columns are `plz`, `note`, `einwohner`, `qkm`, `lat`, and `lon`. This is used for population and density calculations.

### `zuordnung_plz_ort.csv` (12,871 rows)

Mapping between PLZ, municipality (Ort), official municipality key (AGS), district (Landkreis), and federal state (Bundesland). The columns are `osm_id`, `ags`, `ort`, `plz`, `landkreis`, and `bundesland`. It serves as a bridge table to join municipality-level data such as Destatis or Zensus with PLZ-level data. The relationship is many-to-many.

## Data attribution

Data from suche-postleitzahl.org is based on OpenStreetMap (© OpenStreetMap contributors), licensed under the Open Database License (ODbL).
