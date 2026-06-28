# Datasheet: TIGER/Line Shapefiles (U.S. Census Bureau)

**One-line summary:** Authoritative, public-domain vector geographic boundary and feature
data (states, counties, tracts, roads, water, etc.) published annually by the U.S. Census
Bureau as ESRI Shapefiles; they carry geographic identifier codes (GEOIDs) but contain no
demographic or personal data.

*This datasheet (the documentation in this file) is licensed **CC-BY-4.0**. It is documentation
only: it does not host, mirror, transform, or republish any TIGER/Line data.*

Task ID: `ds-geo-004` · Catalog candidate: `cat-geo-004`

---

## Provenance & attribution

| Field | Value |
|-------|-------|
| Publisher / creator | U.S. Census Bureau, Geography Division (Geographic Products Branch) |
| Product | TIGER/Line Shapefiles (current vintage; documented against 2024 vintage) |
| Source landing page | https://www.census.gov/geographies/mapping-files.html |
| Technical documentation | https://www.census.gov/programs-surveys/geography/technical-documentation/complete-technical-documentation/tiger-geo-line.html |
| Record layouts (verified source) | https://www2.census.gov/geo/pdfs/maps-data/data/tiger/tgrshp2024/TGRSHP2024_TechDoc_F-S.pdf |
| Legal/citation chapter (verified source) | https://www2.census.gov/geo/pdfs/maps-data/data/tiger/tgrshp2024/TGRSHP2024_TechDoc_Ch1.pdf |
| Retrieval date | 2026-06-28 |
| Trademark notice | "TIGER/Line" is a registered trademark of the U.S. Census Bureau. |

**Required attribution string (per Census Bureau citation guidance):**

> U.S. Census Bureau, TIGER/Line Shapefiles, https://www.census.gov/geographies/mapping-files.html (accessed 2026-06-28).

The Census Bureau also requests that any *repackaging* of the TIGER/Line Shapefiles,
documentation, or accompanying files for distribution include a conspicuously placed statement
to that effect, and that the trademark, when used to refer to the nature of the product, be
accompanied by the ® symbol. (This datasheet does not repackage the data.)

---

## Source licence — VERIFIED (public domain, derivatives permitted)

**Licence:** U.S. Government work — **public domain** under **Title 17 U.S.C. § 105**. No
copyright applies; reuse and derivative works are permitted; attribution is requested (not
legally required).

**Verbatim clause (cited):** From *TIGER/Line Shapefiles Technical Documentation, Chapter 1,
§1.2 Citation Information*
(https://www2.census.gov/geo/pdfs/maps-data/data/tiger/tgrshp2024/TGRSHP2024_TechDoc_Ch1.pdf):

> "Copyright protection is not available for any work of the United States Government (Title 17
> U.S.C., Section 105). Thus, you are free to reproduce census materials as you see fit. We
> would ask, however, that you cite the Census Bureau as the source."

This explicitly permits reproduction and, by extension, derivative works (no restriction on
modification or commercial use is asserted; only attribution is requested and the trademark
constraints in §1.1 apply to product naming, not to data reuse).

**Licence snapshot (archival record):**
- Source: Chapter 1, §1.2, TGRSHP2024_TechDoc_Ch1.pdf
- Retrieved: 2026-06-28
- SHA-256 of the quoted clause text (verbatim string above):
  `70a70741a7e6702bd73715cbf715a23acd7b0cf32c5fb93c535e7e14a3cd7d49`
  (recompute with: `printf '%s' "<clause>" | sha256sum`)

---

## Data dictionary (verified from official record layouts)

TIGER/Line is a *family* of shapefiles; each geography has its own record layout. Below are two
representative, fully verified layouts transcribed from the 2024 record-layout appendix
(`TGRSHP2024_TechDoc_F-S.pdf`). Lengths are the DBF field lengths from the Census layout.
"Type" is the Census-declared type (String / Number); the geometry column (`the_geom` /
shapefile polygon or polyline) is implicit to the shapefile format and not listed in the DBF
table.

### County and Equivalent Entity National Shapefile — `tl_YYYY_us_county.shp` (Appendix I-2, VERIFIED)

| Field | Type | Length | Units | Description | Allowed values / nulls |
|-------|------|--------|-------|-------------|------------------------|
| STATEFP | String | 2 | — | Current state FIPS code | 2-digit FIPS; not null |
| COUNTYFP | String | 3 | — | Current county FIPS code | 3-digit FIPS; not null |
| COUNTYNS | String | 8 | — | ANSI feature code for the county/equivalent | 8-char ANSI code |
| GEOID | String | 5 | — | County identifier = STATEFP + COUNTYFP | not null; unique per county |
| GEOIDFQ | String | 14 | — | Fully qualified GEOID; joins to data.census.gov | not null |
| NAME | String | 100 | — | Current county name | not null |
| NAMELSAD | String | 100 | — | Name + translated LSAD code | not null |
| LSAD | String | 2 | — | Legal/Statistical Area Description code | 2-char code |
| CLASSFP | String | 2 | — | FIPS class code | 2-char code |
| MTFCC | String | 5 | — | MAF/TIGER feature class code | constant `G4020` for counties |
| CSAFP | String | 3 | — | Combined statistical area code | may be blank if none |
| CBSAFP | String | 5 | — | Metro/micropolitan statistical area code | may be blank if none |
| METDIVFP | String | 5 | — | Metropolitan division code | may be blank if none |
| FUNCSTAT | String | 1 | — | Functional status | single-char code (e.g. `A`, `N`) |
| ALAND | Number | 14 | square meters | Current land area | integer ≥ 0 |
| AWATER | Number | 14 | square meters | Current water area | integer ≥ 0 |
| INTPTLAT | String | 11 | decimal degrees | Latitude of internal point | signed string, e.g. `+41.1234567` |
| INTPTLON | String | 12 | decimal degrees | Longitude of internal point | signed string, e.g. `-096.1234567` |

### Census Tract State-based Shapefile — `tl_YYYY_<stateFIPS>_tract.shp` (Appendix G-4, VERIFIED)

| Field | Type | Length | Units | Description | Allowed values / nulls |
|-------|------|--------|-------|-------------|------------------------|
| STATEFP | String | 2 | — | Current state FIPS code | not null |
| COUNTYFP | String | 3 | — | Current county FIPS code | not null |
| TRACTCE | String | 6 | — | Current census tract code | 6-digit; not null |
| GEOID | String | 11 | — | Tract identifier = STATEFP + COUNTYFP + TRACTCE | not null; unique per tract |
| GEOIDFQ | String | 20 | — | Fully qualified GEOID; joins to data.census.gov | not null |
| NAME | String | 7 | — | Tract code as integer (with 2 decimals if suffix non-zero) | not null |
| NAMELSAD | String | 20 | — | Translated LSAD code + tract name | not null |
| MTFCC | String | 5 | — | MAF/TIGER feature class code | constant `G5020` for tracts |
| FUNCSTAT | String | 1 | — | Functional status | single-char code |
| ALAND | Number | 14 | square meters | Current land area | integer ≥ 0 |
| AWATER | Number | 14 | square meters | Current water area | integer ≥ 0 |
| INTPTLAT | String | 11 | decimal degrees | Latitude of internal point | signed string |
| INTPTLON | String | 12 | decimal degrees | Longitude of internal point | signed string |

> **Unverified / out-of-scope rows:** Other TIGER/Line layers (e.g. `edges`, `faces`,
> `addrfeat`, `roads`, `areawater`, `linearwater`, block groups, places, congressional
> districts) have their own distinct field sets documented in the same appendix family
> (F–S). They are **not** transcribed here and should be treated as **unverified** in this
> datasheet until individually documented. `addrfeat`/address-range layers contain street
> address ranges (interpolated, not individual addresses) — see Limitations.

---

## Datasheet for Datasets

**Motivation.** Created by the U.S. Census Bureau to provide a consistent, nationwide spatial
reference frame for collecting, tabulating, and disseminating census and survey statistics, and
to give the public an authoritative open base map of U.S. legal and statistical geographies.

**Composition.** A family of ESRI Shapefiles (plus KML and File Geodatabase distributions),
one set per geographic entity type and vintage. Each record is a geographic feature (polygon
for areas, polyline for linear features) with attribute fields such as FIPS/ANSI identifier
codes, names, LSAD/class codes, MTFCC feature class, functional status, land/water area, and an
internal-point lat/long. The files contain **GEOIDs that can be joined to** demographic data but
contain **no demographic data and no personal/identifying data** themselves.

**Collection process.** Boundaries and features are derived and maintained in the Census
Bureau's MAF/TIGER (Master Address File / Topologically Integrated Geographic Encoding and
Referencing) database, updated continuously through partnership programs with tribal, state,
and local governments and other federal agencies, then extracted annually into the TIGER/Line
products.

**Preprocessing / cleaning.** Data are topologically integrated within MAF/TIGER. Boundary
information is for statistical collection/tabulation purposes only and is **not** a legal land
description or a determination of jurisdictional authority (per the legal disclaimer, §1.1).
Coordinates are in NAD 83 geographic coordinates (decimal degrees) for the standard products.

**Uses.** Base mapping; spatial joins of census/ACS demographic tables via GEOID; geocoding
reference; routing/road network analysis (edges/roads layers); redistricting and boundary
analysis. Not suitable as a legal/cadastral boundary source or for sub-statistical-purpose
jurisdictional determinations.

**Distribution.** Free of charge from the Census Bureau website
(https://www.census.gov/geographies/mapping-files.html and the `www2.census.gov/geo/tiger/`
download tree). Public domain under 17 U.S.C. § 105. Annual vintages (1990–present) are
retained.

**Maintenance.** Maintained by the Geographic Products Branch, Geography Division, U.S. Census
Bureau (geo.geography@census.gov). New vintages are released annually; the MAF/TIGER database
is updated continuously between releases.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/"
  },
  "@type": "Dataset",
  "name": "TIGER/Line Shapefiles",
  "description": "U.S. Census Bureau TIGER/Line Shapefiles: public-domain vector geographic boundary and feature data (states, counties, census tracts, roads, water, etc.) with FIPS/ANSI identifier codes and GEOIDs for joining to census demographic data. Contains no demographic or personal data.",
  "url": "https://www.census.gov/geographies/mapping-files.html",
  "sameAs": "https://www2.census.gov/geo/pdfs/maps-data/data/tiger/tgrshp2024/",
  "license": "https://www.usa.gov/government-works",
  "creditText": "U.S. Census Bureau, TIGER/Line Shapefiles (accessed 2026-06-28).",
  "isAccessibleForFree": true,
  "version": "2024",
  "creator": {
    "@type": "Organization",
    "name": "U.S. Census Bureau, Geography Division",
    "url": "https://www.census.gov/programs-surveys/geography.html"
  },
  "publisher": {
    "@type": "GovernmentOrganization",
    "name": "U.S. Census Bureau"
  },
  "keywords": ["geospatial", "boundaries", "shapefile", "census", "TIGER/Line", "GEOID", "FIPS"],
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "county-shapefile",
      "name": "tl_YYYY_us_county.shp",
      "description": "County and Equivalent Entity National Shapefile (polygon).",
      "encodingFormat": "application/x-shapefile"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "county-attributes",
      "name": "County attributes",
      "field": [
        { "@type": "cr:Field", "@id": "GEOID", "name": "GEOID", "description": "County identifier (STATEFP+COUNTYFP).", "dataType": "Text" },
        { "@type": "cr:Field", "@id": "STATEFP", "name": "STATEFP", "description": "State FIPS code.", "dataType": "Text" },
        { "@type": "cr:Field", "@id": "COUNTYFP", "name": "COUNTYFP", "description": "County FIPS code.", "dataType": "Text" },
        { "@type": "cr:Field", "@id": "NAME", "name": "NAME", "description": "County name.", "dataType": "Text" },
        { "@type": "cr:Field", "@id": "ALAND", "name": "ALAND", "description": "Land area in square meters.", "dataType": "Integer" },
        { "@type": "cr:Field", "@id": "AWATER", "name": "AWATER", "description": "Water area in square meters.", "dataType": "Integer" }
      ]
    }
  ]
}
```

---

## Validation script

Documentation only: this script validates the **structure** of a TIGER/Line county shapefile
that the user has *already obtained themselves* from the Census Bureau. It does **not** download,
host, or republish any data. Point it at a local file path you control.

```python
#!/usr/bin/env python3
"""Validate a local TIGER/Line county shapefile against the documented schema.

Does NOT download or host data. Requires the user to supply their own local file,
obtained directly from the U.S. Census Bureau. Usage:
    python validate_tiger_county.py /path/to/tl_2024_us_county.shp
"""
import sys

EXPECTED_FIELDS = [
    "STATEFP", "COUNTYFP", "COUNTYNS", "GEOID", "GEOIDFQ", "NAME", "NAMELSAD",
    "LSAD", "CLASSFP", "MTFCC", "CSAFP", "CBSAFP", "METDIVFP", "FUNCSTAT",
    "ALAND", "AWATER", "INTPTLAT", "INTPTLON",
]
# As of 2024 there were 3235 county-and-equivalent records (verify per vintage).
EXPECTED_MIN_ROWS, EXPECTED_MAX_ROWS = 3000, 3300

def main(path):
    try:
        import fiona  # reads shapefiles without loading geometry into memory
    except ImportError:
        sys.exit("Please install 'fiona' (pip install fiona) to run this validator.")

    with fiona.open(path) as src:
        props = list(src.schema["properties"].keys())
        missing = [f for f in EXPECTED_FIELDS if f not in props]
        extra = [f for f in props if f not in EXPECTED_FIELDS]
        n = len(src)

    ok = True
    if missing:
        print(f"FAIL: missing expected fields: {missing}"); ok = False
    if extra:
        print(f"WARN: unexpected extra fields (vintage drift?): {extra}")
    if not (EXPECTED_MIN_ROWS <= n <= EXPECTED_MAX_ROWS):
        print(f"WARN: row count {n} outside expected {EXPECTED_MIN_ROWS}-{EXPECTED_MAX_ROWS}")
    else:
        print(f"OK: row count {n} within expected range")
    print("PASS: schema matches documented County layout" if ok else "VALIDATION FAILED")
    sys.exit(0 if ok else 1)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        sys.exit(__doc__)
    main(sys.argv[1])
```

Quick header-only check without Python (requires GDAL `ogrinfo`, reads metadata only):

```bash
# Lists fields and feature count from a LOCAL file you already downloaded yourself.
ogrinfo -so /path/to/tl_2024_us_county.shp tl_2024_us_county
```

---

## Limitations & gaps

- **Vintage coupling:** Field lengths, the `GEOIDFQ` field, and codes are transcribed from the
  **2024** record layouts. Earlier vintages used `AFFGEOID`/different fields; always re-verify
  against the matching year's Appendix F–S record layout.
- **Only two layers verified:** Only the `county` (Appendix I-2) and `tract` (Appendix G-4)
  layouts are fully transcribed and verified here. All other TIGER/Line layers (edges, faces,
  roads, water, places, block groups, legislative districts, `addrfeat`, etc.) are **not**
  documented in this file and are marked unverified.
- **Address-range layers:** `addrfeat`/address-range products contain interpolated street
  address *ranges*, not individual addresses or names — no PII — but were not examined here and
  should be reviewed separately before any address-related use.
- **Row counts approximate:** The 3000–3300 county range in the validator is an expected-range
  heuristic, not transcribed from official docs; confirm the exact count for your vintage.
- **License label in Croissant:** `https://www.usa.gov/government-works` is used as a stable
  machine-readable stand-in for "U.S. Government public-domain work (17 U.S.C. § 105)"; the
  authoritative wording is the cited Chapter 1 §1.2 clause.
- **Not legal boundaries:** Per the Census legal disclaimer, boundaries are for statistical
  purposes only and are not legal land descriptions or jurisdictional determinations.
- **Coordinate system / datum** (NAD 83) was not re-verified field-by-field from the docs in
  this pass and should be confirmed in Chapter 3 / the product metadata for precision work.
