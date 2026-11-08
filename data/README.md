# The data

ODbL 1.0 (see [`../LICENSE-DATA`](../LICENSE-DATA) and [`../NOTICE`](../NOTICE)).

- `tables/cities.csv`: one row per city: `city` (MEL, SYD, NYC, SFO, PAR, BCN, ROM), `name`, `centre` (the city hall), `study_km2`, `districts`, `fountains` (in the study area), `fountains_per_km2`, `street_km` (street centrelines in the study area), `reached_km` (within a 5-minute walk of a fountain), `streets_5min_pct`, `streets_2min_pct`, `all_ways_km` and `all_ways_5min_pct` (every walkable way counted), `residents`, `residents_reached`, `residents_5min_pct`, `fountains_source` (official or osm), `osm_points` and `osm_5min_pct` (OpenStreetMap's drinking water points instead), `official_matched_in_osm_pct` (official fountains with an OpenStreetMap point within 30 m).
- `tables/districts.csv`: one row per district: `district` (the key), `city`, `name`, `area_km2` (the part in the study area), `fountains`, `street_km`, `reached_km`, `streets_5min_pct`, `residents`, `residents_reached`, `residents_5min_pct`.
- `fountains/fountains.csv`: every fountain used (up to 400 m outside the study area): `fountain` (the key), `city`, `kind` (fountain or refill), `source` (official or osm), `source_id` (the city's own id, or the OpenStreetMap node), `where`, `in_study_area`, `lat`, `lng`.
- `geometry/districts.*`: the districts as exported from Plotlay, keyed by `key` (the `district` code). `geometry/study_areas.geojson`: the seven study areas.
- `streets/<city>_streets.geojson`: two MultiLineStrings: `street` (every street centreline touching the study area) and `reached` (the parts within a 5-minute walk).
