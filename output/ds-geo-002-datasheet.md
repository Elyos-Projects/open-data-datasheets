# Datasheet — Natural Earth (vector + raster map data)

One-line summary: Natural Earth is a public-domain, cartographer-friendly global map dataset of
cultural and physical features (and raster shaded relief) at 1:10m, 1:50m, and 1:110m scales.

This datasheet is documentation only. It does not host, mirror, transform, or republish the
Natural Earth data. This datasheet is licensed **CC-BY-4.0**. (The underlying dataset has its own,
separate licence — see "Source licence" below.)

---

## Provenance & attribution

- **Publisher / creator:** Natural Earth (a volunteer cartographic project supported by the North
  American Cartographic Information Society, NACIS).
- **Source URL (landing):** https://www.naturalearthdata.com/
- **Theme example used for the data dictionary:** Admin 0 – Countries (Cultural vectors) —
  https://www.naturalearthdata.com/downloads/10m-cultural-vectors/10m-admin-0-countries/
- **Retrieval date:** 2026-06-28
- **Required attribution string:** None required. Natural Earth is public domain; attribution is
  optional. The project *suggests* (but does not require) the courtesy credit:
  `Made with Natural Earth. Free vector and raster map data @ naturalearthdata.com.`

---

## Source licence

- **Licence name:** Public Domain.
- **Verified:** YES — the licence permits modification and redistribution (derivatives).
- **Citation (Terms of Use):** https://www.naturalearthdata.com/about/terms-of-use/
- **Exact clauses (retrieved 2026-06-28):**
  > "All versions of Natural Earth raster + vector map data found on this website are in the
  > public domain."
  > "You may use the maps in any manner, including modifying the content and design, electronic
  > dissemination, and offset printing."
- **Derivatives permitted:** Yes — modification is explicitly allowed.
- **Attribution required:** No (optional courtesy credit only).

Because the source is public domain and explicitly permits modification and redistribution, this
datasheet is published as a normal (non-DRAFT) record.

---

## Data dictionary

Scope note: Natural Earth ships **many** themes (e.g. Admin 0 Countries, Admin 1
states/provinces, Populated Places, Coastline, Rivers/Lakes, Land, Ocean, plus raster shaded
relief). The table below documents attribute fields for the **Admin 0 – Countries** vector theme,
the most common entry point. Per the bounded-access guardrail, no dataset rows were downloaded;
fields are documented from the publisher's documentation and from the dataset's well-known,
publicly documented schema. Rows that could **not** be confirmed on the fetched Natural Earth page
are marked `UNVERIFIED` and should be checked against the actual shapefile/GeoJSON attribute table
before relying on them.

| Field | Type | Units | Description | Allowed values / nulls | Verified? |
|-------|------|-------|-------------|------------------------|-----------|
| (geometry) | Polygon / MultiPolygon | decimal degrees (EPSG:4326) | Country boundary geometry; de-facto boundaries by default | n/a | Confirmed (publisher states de-facto boundaries, lon/lat) |
| ISO_A2 | string | — | ISO 3166-1 alpha-2 country code | 2-letter code; `-99` used for missing/unassigned | Partially — publisher confirms "ISO codes"; exact column name UNVERIFIED |
| ISO_A3 | string | — | ISO 3166-1 alpha-3 country code | 3-letter code; `-99` for missing | Partially — "ISO codes" confirmed; column name UNVERIFIED |
| FIPS_10 / FIPS | string | — | U.S. FIPS country code | FIPS code; nulls possible | Partially — publisher confirms "FIPS codes"; exact name UNVERIFIED |
| INSEE (French code) | string | — | French INSEE country code | code; nulls possible | Partially — publisher confirms "French INSEE codes"; exact name UNVERIFIED |
| NAME | string | — | Common country name | non-null | UNVERIFIED (well-known field, not listed on fetched page) |
| NAME_LONG | string | — | Long/formal country name | non-null | UNVERIFIED |
| ADM0_A3 | string | — | Admin-0 3-letter identifier (sovereignty grouping) | 3-letter code | UNVERIFIED |
| SOVEREIGNT | string | — | Sovereign state name | non-null | UNVERIFIED |
| POP_EST | number (integer/float) | persons | Estimated population | >= 0; sentinel values possible | UNVERIFIED |
| GDP_MD | number | million USD | Estimated GDP | nullable | UNVERIFIED |
| CONTINENT | string | — | Continent name | enumerated continents | UNVERIFIED |
| REGION_UN | string | — | UN region | enumerated | UNVERIFIED |
| SUBREGION | string | — | UN subregion | enumerated | UNVERIFIED |
| ECONOMY | string | — | Economy classification | enumerated | UNVERIFIED |
| INCOME_GRP | string | — | World Bank income group | enumerated | UNVERIFIED |

Confirmed from the publisher page: the Admin 0 Countries theme contains **258 countries**, treats
Greenland as separate from Denmark, distinguishes metropolitan vs. independent/semi-independent
portions of sovereign states, and offers point-of-view boundary variants for disputed areas.

No personal or identifying fields are present or documented (country-level boundaries and
aggregate thematic attributes only). PII pass: clean.

---

## Datasheet for Datasets

**Motivation.** Built by and for cartographers to make small-scale ("zoomed-out") world, regional,
and country mapmaking fast and consistent, removing the need to hand-clean disparate sources.
Maintained by the volunteer Natural Earth project with NACIS support.

**Composition.** Vector themes (Cultural: countries, states/provinces, populated places, roads,
etc.; Physical: coastline, land, ocean, rivers, lakes, glaciated areas, bathymetry) plus Raster
shaded relief / land cover. Each theme is offered at three nested scales: 1:10m (most detailed),
1:50m, and 1:110m (least detailed). Instances are geographic features (e.g. one polygon per
country). Admin 0 Countries holds 258 country records. No personal data.

**Collection process.** Compiled and generalized by cartographers from multiple public sources,
including thematic data from the United Nations, the U.S. CIA, and others, then integrated and
edited for cartographic consistency across scales.

**Preprocessing / cleaning / labeling.** Geometries are generalized per target scale; attribute
tables are harmonized (ISO/FIPS/INSEE codes attached); boundaries default to de-facto control with
optional point-of-view variants. Exact per-field cleaning rules are not fully published.

**Uses.** Base maps, thematic mapping, geospatial joins on country/region codes, teaching, and
visualization. Not intended for high-precision/large-scale (zoomed-in) geodetic or legal boundary
use; boundaries are cartographic, not authoritative for disputes.

**Distribution.** Free download from naturalearthdata.com as Shapefile, file geodatabase (geoDB),
and GeoJSON (vector) and TIFF (raster). Public domain — no usage restrictions. This datasheet does
not redistribute the data; obtain it from the publisher.

**Maintenance.** Maintained by the Natural Earth volunteer project (NACIS). Versioned releases are
published on the site; issues and changes are tracked by the project. Check the site for the
current version before use.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "dct": "http://purl.org/dc/terms/"
  },
  "@type": "Dataset",
  "name": "Natural Earth (vector + raster map data)",
  "description": "Public-domain global cultural and physical vector map data and raster shaded relief, offered at 1:10m, 1:50m, and 1:110m scales for small-scale cartography.",
  "url": "https://www.naturalearthdata.com/",
  "license": "https://creativecommons.org/publicdomain/mark/1.0/",
  "creditText": "Made with Natural Earth.",
  "creator": {
    "@type": "Organization",
    "name": "Natural Earth (supported by NACIS)",
    "url": "https://www.naturalearthdata.com/"
  },
  "dct:rights": "Public Domain — modification and redistribution permitted (see https://www.naturalearthdata.com/about/terms-of-use/).",
  "version": "unspecified — verify current release at source",
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "ne_10m_admin_0_countries.zip",
      "name": "Admin 0 Countries (1:10m) shapefile bundle",
      "description": "Documentation reference only; not hosted by this datasheet.",
      "encodingFormat": "application/zip"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "admin0_countries",
      "name": "admin0_countries",
      "description": "One record per country/territory (Admin 0).",
      "field": [
        { "@type": "cr:Field", "@id": "admin0_countries/NAME", "name": "NAME", "description": "Common country name", "dataType": "sc:Text" },
        { "@type": "cr:Field", "@id": "admin0_countries/ISO_A3", "name": "ISO_A3", "description": "ISO 3166-1 alpha-3 code", "dataType": "sc:Text" },
        { "@type": "cr:Field", "@id": "admin0_countries/CONTINENT", "name": "CONTINENT", "description": "Continent name", "dataType": "sc:Text" },
        { "@type": "cr:Field", "@id": "admin0_countries/geometry", "name": "geometry", "description": "Polygon/MultiPolygon boundary (EPSG:4326)", "dataType": "sc:GeoShape" }
      ]
    }
  ]
}
```

---

## Validation script

This script validates the **structure** of a Natural Earth Admin 0 Countries layer that the user
has already obtained themselves. It does **not** download, host, or republish any data — it only
inspects a local file path supplied by the user.

```python
#!/usr/bin/env python3
"""Validate structure of a locally-obtained Natural Earth Admin 0 Countries layer.

Documentation/validation only. This script does NOT download or host data.
Point it at a file you obtained yourself from naturalearthdata.com.

Usage:
    python validate_ne_admin0.py /path/to/ne_10m_admin_0_countries.shp
Requires: geopandas (or fiona). Reads the header/attribute table only.
"""
import sys

EXPECTED_MIN_ROWS = 200          # 1:10m Admin 0 has ~258 country records
EXPECTED_FIELDS_ANY = {          # at least these identifier-style fields should exist
    "ISO_A2", "ISO_A3", "ADM0_A3", "NAME", "SOVEREIGNT",
}

def main(path: str) -> int:
    try:
        import geopandas as gpd
    except ImportError:
        print("FAIL: geopandas not installed (pip install geopandas)")
        return 2

    gdf = gpd.read_file(path)
    cols = {c.upper() for c in gdf.columns}
    n = len(gdf)

    ok = True
    print(f"rows: {n}")
    if n < EXPECTED_MIN_ROWS:
        print(f"FAIL: expected >= {EXPECTED_MIN_ROWS} rows, got {n}")
        ok = False

    present = EXPECTED_FIELDS_ANY & cols
    print(f"identifier fields present: {sorted(present)}")
    if not present:
        print(f"FAIL: none of the expected fields {sorted(EXPECTED_FIELDS_ANY)} found")
        ok = False

    crs = getattr(gdf, "crs", None)
    print(f"CRS: {crs}")
    if crs is None or "4326" not in str(crs.to_epsg() if hasattr(crs, 'to_epsg') else crs):
        print("WARN: expected EPSG:4326 (WGS84 lon/lat)")

    print("PASS" if ok else "RESULT: FAIL")
    return 0 if ok else 1

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__)
        sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

Data-quality checks performed by the script: minimum row count (≈258 for 1:10m Admin 0), presence
of at least one stable identifier field, and a coordinate reference system sanity check (EPSG:4326).

---

## Limitations & gaps

- **Field names not fully confirmed at source.** The fetched publisher pages confirm the presence
  of ISO, FIPS, and French INSEE codes and high-level dataset facts (258 countries, de-facto
  boundaries, scales, formats), but do **not** publish a complete attribute dictionary. Fields
  marked `UNVERIFIED` above reflect the dataset's widely-documented schema and must be checked
  against the actual attribute table before being relied upon.
- **No data was sampled.** Per the bounded-access guardrail, no rows were downloaded; row counts
  and types are stated from documentation, not measured.
- **Single theme documented in detail.** The data dictionary covers Admin 0 – Countries only;
  other themes (Admin 1, Populated Places, Physical layers, raster) have different schemas.
- **Versioning.** Natural Earth is periodically revised; the current release version was not pinned
  here. Verify the version at the source before use.
- **Boundaries are cartographic.** De-facto boundaries are not authoritative for legal/disputed
  territory questions; point-of-view variants exist for some disputed areas.
- **No PII / no commercial-only restriction found.** The source is public domain and contains
  country-level aggregate data only.
