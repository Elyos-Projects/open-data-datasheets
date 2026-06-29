# Datasheet: geoBoundaries Global Administrative Boundaries

**One-line summary:** An open, attribution-only global database of political administrative
boundaries (ADM0-ADM5) for 200+ entities, built for redistribution as a CC-BY alternative to GADM.

*This datasheet is documentation only. It does not host, mirror, transform, or republish any
geoBoundaries data. This datasheet's own content is licensed **CC-BY-4.0**.*

---

## Provenance & attribution

| Item | Value |
|------|-------|
| **Publisher / creator** | William & Mary geoLab (Runfola, D. et al.) and the geoBoundaries community |
| **Source URL** | https://www.geoboundaries.org/ |
| **API / docs URL** | https://www.geoboundaries.org/api.html |
| **Catalog id** | cat-geo-005 |
| **Retrieval date** | 2026-06-28 |
| **Datasheet task id** | ds-geo-005 |

**Required attribution string** (from geoboundaries.org usage terms):

> "geoBoundaries" — www.geoboundaries.org

For written/academic works the publisher requests the PLoS ONE citation:

> Runfola D, et al. (2020) geoBoundaries: A global database of political administrative boundaries.
> PLoS ONE 15(4): e0231866. https://doi.org/10.1371/journal.pone.0231866

---

## Source licence

**Verified licence:** Creative Commons Attribution 4.0 International (**CC-BY-4.0**).

**Permits derivatives / redistribution:** **Yes.** This was confirmed at the source on 2026-06-28.
geoBoundaries states the licence "allows for most commercial, noncommercial, and academic uses"
and that "the only requirement for use is acknowledgement."

- Citation (publisher terms): https://www.geoboundaries.org/ (usage / "How do I cite or use this?" section).
- Citation (licence text, derivatives clause): CC-BY-4.0 §2(a)(1) grants the right to
  "reproduce and Share the Licensed Material" and "produce, reproduce, and Share Adapted Material."
  Full text: https://creativecommons.org/licenses/by/4.0/legalcode

**Important scope note (verified):** Only the **gbOpen** product line is uniformly CC-BY-4.0. The
`gbHumanitarian` (UN OCHA mirror) line has variable per-source licensing, and `gbAuthoritative`
(UN SALB mirror) is **non-commercial use only**. This datasheet documents the CC-BY-4.0 `gbOpen`
line. Each layer additionally records its upstream `boundaryLicense`/`licenseSource`, which should
be checked per-country for the humanitarian/authoritative lines.

A licence snapshot (hash + archived copy of the licence text) should be attached as the per-dataset
gate artifact; it is not embedded here to keep this file documentation-only.

---

## Data dictionary

geoBoundaries exposes two layers of fields: (A) per-layer **metadata** returned by the API and
metadata CSV, and (B) per-feature **geometry attributes** carried inside each GeoJSON/shapefile.

### A. Per-layer metadata (verified from https://www.geoboundaries.org/api.html, 2026-06-28)

| Field | Type | Units | Description | Allowed values / nulls |
|-------|------|-------|-------------|------------------------|
| boundaryID | string | — | Unique id = ISO code + boundary type + hash | Guaranteed non-null |
| boundaryName | string | — | Country/entity name for the layer | Guaranteed non-null |
| boundaryISO | string | — | ISO 3166-1 alpha-3 country code | Guaranteed non-null |
| boundaryYearRepresented | string/number | year | Year or year range the boundaries represent | Guaranteed non-null |
| boundaryType | string | — | Administrative level | ADM0..ADM5 |
| boundaryCanonical | string | — | Official regional/local name | May be null |
| boundarySource | string | — | Comma-separated primary data sources | Guaranteed non-null |
| boundaryLicense | string | — | Original licence from primary source | Guaranteed non-null |
| licenseDetail | string | — | Licence notes / verification info | May be null |
| licenseSource | string (URL) | — | URL of the primary source | Guaranteed non-null |
| sourceDataUpdateDate | date | — | Integration date into repository | Guaranteed non-null |
| buildDate | date | — | Standardization/release build date | Guaranteed non-null |
| Continent | string | — | Continental classification | Guaranteed non-null |
| UNSDG-region | string | — | UN SDG region | Guaranteed non-null |
| UNSDG-subregion | string | — | UN SDG subregion | Guaranteed non-null |
| worldBankIncomeGroup | string | — | World Bank income category | Guaranteed non-null |
| admUnitCount | integer | count | Number of administrative units in the layer | Guaranteed non-null |
| meanVertices | number | count | Mean vertices per unit | Guaranteed non-null |
| minVertices | integer | count | Minimum vertices in layer | Guaranteed non-null |
| maxVertices | integer | count | Maximum vertices in layer | Guaranteed non-null |
| minPerimeterLengthKM | number | km | Min perimeter (World Equidistant Cylindrical) | Guaranteed non-null |
| meanPerimeterLengthKM | number | km | Mean perimeter | Guaranteed non-null |
| maxPerimeterLengthKM | number | km | Max perimeter | Guaranteed non-null |
| minAreaSqKM | number | km^2 | Min area (EASE-GRID 2 projection) | Guaranteed non-null |
| meanAreaSqKM | number | km^2 | Mean area | Guaranteed non-null |
| maxAreaSqKM | number | km^2 | Max area | Guaranteed non-null |
| staticDownloadLink | string (URL) | — | Aggregate ZIP download URL | Guaranteed non-null |
| gjDownloadURL | string (URL) | — | GeoJSON download link | Guaranteed non-null |
| tjDownloadURL | string (URL) | — | TopoJSON download link | Guaranteed non-null |
| simplifiedGeometryGeoJSON | string (URL) | — | Simplified GeoJSON link | Guaranteed non-null |
| imagePreview | string (URL) | — | Auto-rendered PNG preview link | Guaranteed non-null |

### B. Per-feature geometry attributes (GeoJSON/shapefile properties)

> **Partially verified.** These are the standard geoBoundaries per-feature property names as
> documented by the project. They were **not** re-verified field-by-field against a downloaded
> sample during this pass (the guardrail forbids downloading/sampling the data here). Treat the
> rows below as documented-but-unconfirmed and verify with the validation script before relying
> on them.

| Field | Type | Units | Description | Allowed values / nulls | Status |
|-------|------|-------|-------------|------------------------|--------|
| shapeName | string | — | Name of the administrative unit | May be empty for unnamed units | Unverified (documented) |
| shapeISO | string | — | ISO code for the unit where available | Often empty below ADM0 | Unverified (documented) |
| shapeID | string | — | Unique per-feature identifier | Non-null | Unverified (documented) |
| shapeGroup | string | — | ISO3 code of the parent country/entity | Non-null | Unverified (documented) |
| shapeType | string | — | Administrative level of the feature | ADM0..ADM5 | Unverified (documented) |
| geometry | GeoJSON geometry | WGS84 (EPSG:4326) deg | Polygon / MultiPolygon boundary | Non-null | Unverified (documented) |

---

## Datasheet for Datasets

**Motivation.** Created to provide an openly licensed, redistributable global set of administrative
boundaries, addressing the redistribution restrictions of common alternatives (e.g., GADM).
Built since 2016 by the William & Mary geoLab and a contributor community.

**Composition.** Political/administrative boundary polygons for 200+ entities including all UN
member states, organized into hierarchical levels ADM0 (country) through ADM5. Each instance is an
administrative unit polygon with the per-feature attributes above; layers carry rich metadata
(area, perimeter, vertex statistics, source, licence). The project reports tracking ~1 million
boundaries. **No personal or identifying data** — units are geographic/administrative entities,
not individuals.

**Collection process.** Boundaries are sourced from upstream providers (national agencies, UN
mirrors, OpenStreetMap, and others recorded per-layer in `boundarySource`/`licenseSource`),
then standardized, quality-checked, and built into harmonized releases. Provenance and original
licence are retained per layer.

**Preprocessing / cleaning.** geoBoundaries standardizes naming and structure, computes geometry
statistics, and produces both full-resolution and **simplified** geometries plus multiple formats
(GeoJSON, TopoJSON, shapefile). Geometries are distributed in WGS84 (EPSG:4326); area/perimeter
statistics are computed in equal-area / equidistant projections (EASE-GRID 2, World Equidistant
Cylindrical).

**Uses.** Mapping, spatial joins, choropleths, humanitarian and development analytics, research.
Suitable for commercial, non-commercial, and academic use under CC-BY (gbOpen line). Not a
legal/authoritative source for disputed borders — boundary depictions do not imply endorsement.

**Distribution.** Publicly downloadable from geoboundaries.org and its API in GeoJSON, TopoJSON,
and shapefile; per-layer static ZIP links. Released under CC-BY-4.0 for the gbOpen line.

**Maintenance.** Maintained by the William & Mary geoLab; versioned releases (v2.0, v4.0, and
later) with `buildDate`/`sourceDataUpdateDate` tracking. Contact and contribution channels are on
geoboundaries.org.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/"
  },
  "@type": "Dataset",
  "name": "geoBoundaries Global Administrative Boundaries (gbOpen)",
  "description": "Open, attribution-only global database of political administrative boundaries (ADM0-ADM5) for 200+ entities, built for redistribution. Published by the William & Mary geoLab.",
  "url": "https://www.geoboundaries.org/",
  "sameAs": "https://www.geoboundaries.org/api.html",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Organization",
    "name": "William & Mary geoLab",
    "url": "https://www.geoboundaries.org/"
  },
  "citation": "Runfola D, et al. (2020) geoBoundaries: A global database of political administrative boundaries. PLoS ONE 15(4): e0231866.",
  "keywords": ["administrative boundaries", "geospatial", "GIS", "open data", "GeoJSON"],
  "datePublished": "2020-04-15",
  "version": "gbOpen",
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "geojson",
      "name": "boundary-geojson",
      "encodingFormat": "application/geo+json",
      "contentUrl": "https://www.geoboundaries.org/api.html"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "boundaries",
      "name": "boundaries",
      "field": [
        {"@type": "cr:Field", "@id": "shapeName", "name": "shapeName", "description": "Name of the administrative unit", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "shapeISO", "name": "shapeISO", "description": "ISO code for the unit where available", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "shapeID", "name": "shapeID", "description": "Unique per-feature identifier", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "shapeGroup", "name": "shapeGroup", "description": "ISO3 of the parent country/entity", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "shapeType", "name": "shapeType", "description": "Administrative level (ADM0..ADM5)", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "geometry", "name": "geometry", "description": "Polygon/MultiPolygon boundary in WGS84 (EPSG:4326)", "dataType": "sc:GeoShape"}
      ]
    }
  ]
}
```

---

## Validation script

The script below validates the **structure** of a locally-obtained geoBoundaries GeoJSON layer.
It does **not** download, host, or republish data — the user supplies a path to a file they have
already obtained from geoboundaries.org under its CC-BY licence.

```python
#!/usr/bin/env python3
"""Validate the structure of a local geoBoundaries GeoJSON layer.
Documentation-only: this script does NOT download or host any data.
Usage: python validate_geoboundaries.py path/to/geoBoundaries-XXX-ADMn.geojson
"""
import json, sys

EXPECTED_PROPS = {"shapeName", "shapeISO", "shapeID", "shapeGroup", "shapeType"}
VALID_ADM = {"ADM0", "ADM1", "ADM2", "ADM3", "ADM4", "ADM5"}

def main(path):
    with open(path, "r", encoding="utf-8") as f:
        gj = json.load(f)

    assert gj.get("type") == "FeatureCollection", "Top-level type must be FeatureCollection"
    feats = gj.get("features", [])
    assert len(feats) > 0, "Expected at least one feature"
    print(f"features: {len(feats)}")

    for i, feat in enumerate(feats):
        props = set((feat.get("properties") or {}).keys())
        missing = EXPECTED_PROPS - props
        assert not missing, f"feature {i}: missing properties {missing}"
        st = feat["properties"].get("shapeType")
        assert st in VALID_ADM, f"feature {i}: unexpected shapeType {st!r}"
        geom = feat.get("geometry") or {}
        assert geom.get("type") in {"Polygon", "MultiPolygon"}, \
            f"feature {i}: geometry must be Polygon/MultiPolygon"

    print("OK: structure validated")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        sys.exit("usage: validate_geoboundaries.py <path.geojson>")
    main(sys.argv[1])
```

---

## Limitations & gaps

- **Per-feature attributes are documented-but-unconfirmed.** The `shape*` property names were not
  re-verified against a downloaded sample in this pass (the guardrail forbids downloading/sampling
  data here). Run the validation script against a locally obtained file before relying on them.
- **Licence scope varies by product line.** Only `gbOpen` is uniformly CC-BY-4.0. `gbHumanitarian`
  has variable upstream licences and `gbAuthoritative` is non-commercial; always check the per-layer
  `boundaryLicense`/`licenseSource`.
- **Exact field types/nullability** for some metadata fields are inferred from descriptions, not a
  formal schema; year fields may be a single year or a range string.
- **Disputed borders.** Boundary depictions are not authoritative and do not imply political
  endorsement; treat contested regions with care.
- **No licence snapshot embedded.** The hash + archived licence text gate artifact must be attached
  separately; it is not committed here to keep this deliverable documentation-only.
- The publisher landing page did not list field/format details directly; field-level facts were
  drawn from the API documentation page (api.html) retrieved 2026-06-28.
