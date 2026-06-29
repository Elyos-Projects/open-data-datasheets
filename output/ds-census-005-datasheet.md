# Datasheet: WorldPop Gridded Population

**One-line summary:** High-resolution (~100 m) gridded estimates of human population counts per grid cell, modelled globally by WorldPop using a Random Forest dasymetric top-down approach.

*This datasheet is published under the **Creative Commons Attribution 4.0 International License (CC-BY-4.0)**. It is documentation only and does not contain, host, mirror, or republish any portion of the underlying dataset.*

---

## Provenance & attribution

| Field | Value |
|---|---|
| Publisher | WorldPop, University of Southampton |
| Source URL | https://www.worldpop.org/ (data hub: https://hub.worldpop.org/) |
| Catalog id (candidate) | cat-census-005 |
| Retrieval date | 2026-06-28 |
| Funder (acknowledged) | Bill & Melinda Gates Foundation (grant OPP1134076) |
| Data type | Gridded raster (modelled population counts) |

**Required attribution string (use when redistributing derivatives):**

> WorldPop (www.worldpop.org), School of Geography and Environmental Science, University of Southampton. Licensed under CC-BY-4.0. https://creativecommons.org/licenses/by/4.0/

A dataset-specific citation also acknowledges the methods paper: *Lloyd et al., "Global spatio-temporally harmonised datasets for producing high-resolution gridded population distribution datasets."* (referenced on the WorldPop hub dataset listing; full DOI to be confirmed per dataset on the hub).

---

## Source licence

- **Licence name:** Creative Commons Attribution 4.0 International (CC-BY-4.0).
- **Verification:** The WorldPop data hub footer and individual dataset listing pages state: *"WorldPop datasets are licensed under the Creative Commons Attribution 4.0 International License."* (verified 2026-06-28 at https://hub.worldpop.org/ and on the gridded population count listing at https://hub.worldpop.org/geodata/listing?id=29).
- **Derivatives permitted:** YES. CC-BY-4.0 grants the right to "copy and redistribute the material in any medium or format" and to "remix, transform, and build upon the material for any purpose, even commercially," provided attribution is given. See the licence deed clause "Adapt — remix, transform, and build upon the material for any purpose" at https://creativecommons.org/licenses/by/4.0/ and the legal code §2(a)(1) at https://creativecommons.org/licenses/by/4.0/legalcode.
- **Licence snapshot:** The canonical legal text lives at https://creativecommons.org/licenses/by/4.0/legalcode. (Reviewers: attach an archived copy + SHA-256 hash of the retrieved legal-code text as the per-dataset gate artifact. Not embedded here to keep this datasheet documentation-only.)

**Conclusion:** Source licence verified to permit derivatives with citation. No guardrail block; the dataset is CC-BY (open, attribution-only) and is modelled (cell-aggregated) rather than person-level.

---

## Data dictionary

WorldPop gridded population is a **single-band raster**, not a tabular file, so "fields" below describe the raster's properties and per-cell value semantics. Verified items are sourced from the WorldPop hub dataset listing (retrieved 2026-06-28); items not explicitly stated on the docs are marked **UNVERIFIED**.

| Name | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| `pixel_value` (band 1) | Float32 (raster band) | persons per pixel | Estimated number of people residing in the grid cell | Non-negative real numbers; NoData for non-land/unmodelled cells |
| `nodata_value` | raster metadata | n/a | Value marking cells with no estimate | **UNVERIFIED** — commonly `-99999` in WorldPop GeoTIFFs; confirm via raster header per file |
| `spatial_resolution` | raster metadata | arc-seconds / metres | Cell size | 3 arc-second (~100 m at equator). **UNVERIFIED**: a 30 arc-second (~1 km) variant is also published for some products |
| `crs` | raster metadata | n/a | Coordinate reference system | Geographic Coordinate System, WGS84 (EPSG:4326) |
| `temporal_coverage` | dataset attribute | year | Reference year of the estimate | Annual, 2000–2020 (per the listing) |
| `spatial_coverage` | dataset attribute | n/a | Extent | Per-country rasters (global coverage assembled country-by-country) |
| `file_format` | dataset attribute | n/a | Distribution format | GeoTIFF (`.tif`) |

Notes:
- Cell values are continuous (modelled redistribution), so a single cell may carry a fractional person count.
- No person-level, household-level, or otherwise identifying fields exist in this product; values are spatially aggregated model outputs.

---

## Datasheet for Datasets

**Motivation.** Created to provide consistent, open, high-resolution estimates of where people live, supporting public-health, humanitarian response, disaster planning, SDG monitoring, and demographic research where recent or fine-grained census data are unavailable. Produced by WorldPop (University of Southampton); funded in part by the Bill & Melinda Gates Foundation (OPP1134076).

**Composition.** Each instance is a grid cell (~100 m) whose value is the estimated number of people in that cell. Distributed as per-country single-band GeoTIFF rasters, annually for 2000–2020. Contains no individuals or personal records — only modelled aggregate counts. No labels beyond the population estimate; uncertainty is not encoded per cell in the standard count product.

**Collection process.** Outputs are *derived*, not directly observed. A top-down dasymetric method redistributes official census/administrative population totals using a Random Forest weighting surface built from remotely-sensed and geospatial covariates (settlement locations and extents, land cover, roads, building maps, etc.). Census counts act as control totals at the country level.

**Preprocessing / cleaning / labelling.** Census totals are harmonised across space and time; covariate layers are assembled and aligned to the ~100 m grid; the Random Forest model predicts a weighting surface used for dasymetric redistribution. Resulting rasters are clipped to national boundaries.

**Uses.** Suitable for population exposure analysis, accessibility/coverage studies, sampling frames, and resource allocation. Cautions: values are model estimates with spatially varying error; not a substitute for an enumerated census; not appropriate for inferring attributes of specific individuals or small identifiable groups.

**Distribution.** Openly distributed via the WorldPop hub (https://hub.worldpop.org/) under CC-BY-4.0; downloadable GeoTIFFs, some with DOIs. This datasheet does not redistribute the data.

**Maintenance.** Maintained by the WorldPop programme, University of Southampton. Methods and releases are versioned; consult the hub for the authoritative, current version and per-dataset DOIs/changelogs.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "sc": "https://schema.org/"
  },
  "@type": "sc:Dataset",
  "name": "WorldPop Gridded Population",
  "description": "High-resolution (~100 m) gridded estimates of human population counts per grid cell, modelled by WorldPop using a Random Forest dasymetric top-down approach. Distributed as per-country single-band GeoTIFF rasters, annually for 2000-2020.",
  "url": "https://hub.worldpop.org/",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Organization",
    "name": "WorldPop, University of Southampton",
    "url": "https://www.worldpop.org/"
  },
  "datePublished": "2020",
  "keywords": ["population", "demographics", "gridded", "raster", "geospatial", "census"],
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "geotiff",
      "name": "population_count_geotiff",
      "encodingFormat": "image/tiff",
      "description": "Single-band GeoTIFF, ~100 m (3 arc-second), WGS84 (EPSG:4326)."
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "raster_cells",
      "name": "raster_cells",
      "description": "Per-grid-cell population estimates.",
      "field": [
        {
          "@type": "cr:Field",
          "@id": "raster_cells/pixel_value",
          "name": "pixel_value",
          "description": "Estimated number of people per ~100 m grid cell.",
          "dataType": "sc:Float"
        },
        {
          "@type": "cr:Field",
          "@id": "raster_cells/crs",
          "name": "crs",
          "description": "Coordinate reference system: WGS84 / EPSG:4326.",
          "dataType": "sc:Text"
        },
        {
          "@type": "cr:Field",
          "@id": "raster_cells/year",
          "name": "year",
          "description": "Reference year of the estimate (2000-2020).",
          "dataType": "sc:Integer"
        }
      ]
    }
  ]
}
```

---

## Validation script

The script below documents how to validate the **structure** of a WorldPop population GeoTIFF that a user has already obtained themselves. It does **not** download, host, or republish any data; supply your own local file path. It only reads the raster header/metadata (no data redistribution).

```python
#!/usr/bin/env python3
"""Validate the structure of a locally-held WorldPop population GeoTIFF.
Documentation/QA only: reads header + a bounded sample. Does not download or host data.

Usage: python validate_worldpop.py /path/to/your_local_file.tif
Requires: rasterio (pip install rasterio)
"""
import sys
import rasterio

EXPECTED_BANDS = 1
EXPECTED_DTYPE_PREFIX = "float"          # WorldPop counts are floating point
EXPECTED_CRS_EPSG = 4326                 # WGS84
APPROX_RES_DEG = 0.0008333333            # 3 arc-second ~= 0.000833 degrees

def main(path):
    ok = True
    with rasterio.open(path) as ds:
        print(f"driver={ds.driver} size={ds.width}x{ds.height} bands={ds.count}")
        print(f"dtype={ds.dtypes[0]} crs={ds.crs} nodata={ds.nodata}")
        print(f"pixel_size={ds.res}")

        if ds.driver != "GTiff":
            print("WARN: expected a GeoTIFF (GTiff driver)"); ok = False
        if ds.count != EXPECTED_BANDS:
            print(f"WARN: expected {EXPECTED_BANDS} band, got {ds.count}"); ok = False
        if not ds.dtypes[0].startswith(EXPECTED_DTYPE_PREFIX):
            print(f"WARN: expected float dtype, got {ds.dtypes[0]}"); ok = False
        if ds.crs is None or ds.crs.to_epsg() != EXPECTED_CRS_EPSG:
            print(f"WARN: expected EPSG:{EXPECTED_CRS_EPSG}, got {ds.crs}"); ok = False
        if abs(ds.res[0] - APPROX_RES_DEG) > 0.0005:
            print(f"NOTE: pixel size {ds.res[0]} differs from ~100 m (could be the 1 km variant)")

        # Bounded sample: read a single small window only (no full-data export)
        win = rasterio.windows.Window(0, 0, min(256, ds.width), min(256, ds.height))
        sample = ds.read(1, window=win)
        nd = ds.nodata
        valid = sample[(sample != nd)] if nd is not None else sample
        if valid.size and (valid < 0).any():
            print("WARN: negative population values found in sample"); ok = False
        print(f"sample_window_min={valid.min() if valid.size else 'n/a'} "
              f"sample_window_max={valid.max() if valid.size else 'n/a'}")

    print("RESULT:", "PASS" if ok else "CHECK WARNINGS")
    return 0 if ok else 1

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__); sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

Expected-structure summary the script enforces: 1 band, float dtype, CRS EPSG:4326, ~100 m pixel size (flagging the ~1 km variant), and non-negative population values in a bounded 256x256 sample window.

---

## Limitations & gaps

- **Not verified from docs:** the exact NoData sentinel value (commonly `-99999` in WorldPop GeoTIFFs but not confirmed on the pages retrieved), the precise per-dataset DOI/citation string, and the existence/scope of the 30 arc-second (~1 km) variant for this specific product. These are marked UNVERIFIED above and should be confirmed against the per-file raster header and the specific hub dataset page before relying on them.
- **No data was downloaded, sampled, hosted, or transformed** in producing this datasheet; field semantics are taken from WorldPop's published documentation only. The validation script is illustrative and was not executed against a live file here.
- WorldPop counts are **modelled estimates**, not enumerated census figures; they carry spatially varying uncertainty not encoded in the standard count raster. Do not use for individual-level inference.
- Licence verified at the hub/listing level; if a specific sub-product on the hub declares a different licence, that per-product statement governs and this datasheet should be re-checked.
