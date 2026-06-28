# Datasheet: CAMS Atmosphere Monitoring (Reanalysis / Forecast)

**One-line summary:** Documentation datasheet for the Copernicus Atmosphere Monitoring Service (CAMS) global atmospheric-composition data, exemplified by the CAMS Global Reanalysis (EAC4) product — modelled global fields of reactive gases, aerosols, particulates and meteorology.

*This datasheet (the document you are reading) is licensed under **CC-BY-4.0**. It is documentation only: it does not host, mirror, transform, or republish any CAMS data.*

> Task: `ds-airq-005` · Catalog candidate: `cat-airq-005` · Deliverable: documentation datasheet · Risk tier: low

---

## Provenance & attribution

| Field | Value |
|---|---|
| **Publisher / data provider** | Copernicus Atmosphere Monitoring Service (CAMS), implemented by ECMWF (European Centre for Medium-Range Weather Forecasts) on behalf of the European Commission / Copernicus Programme |
| **Source landing page** | https://atmosphere.copernicus.eu/data |
| **Access portal (Atmosphere Data Store, ADS)** | https://ads.atmosphere.copernicus.eu/ |
| **Representative dataset (used for field verification)** | CAMS global reanalysis (EAC4) — https://ads.atmosphere.copernicus.eu/datasets/cams-global-reanalysis-eac4 |
| **Dataset DOI** | 10.24381/d58bbf47 |
| **Retrieval date** | 2026-06-28 |

**Required attribution string** (CAMS/Copernicus standard wording):

> "Generated using Copernicus Atmosphere Monitoring Service Information [2026]" — or, where the data has been modified — "Contains modified Copernicus Atmosphere Monitoring Service Information [2026]".

For the EAC4 product specifically, the publisher requests citation via its DOI: **https://doi.org/10.24381/d58bbf47** (Copernicus Atmosphere Monitoring Service (CAMS), ECMWF).

---

## Source licence

**Licence name:** Creative Commons Attribution 4.0 International (**CC-BY-4.0**), shown on the ADS dataset page as the "CC-BY licence" that must be accepted before download. CAMS products are additionally governed historically by the *Licence to use Copernicus Products*; both are attribution licences that permit derivative works.

**Does it permit derivatives?** **Yes.** CC-BY-4.0 explicitly grants the right to "reproduce and Share the Licensed Material, in whole or in part" and to "produce, reproduce, and Share Adapted Material" provided attribution is given.

**Citation / clause confirming derivatives:**
- CC-BY-4.0 legal code, Section 2(a)(1): "the Licensor hereby grants You a worldwide, royalty-free, non-sublicensable, non-exclusive, irrevocable license to exercise the Licensed Rights ... to: (A) reproduce and Share the Licensed Material ...; and (B) produce, reproduce, and Share Adapted Material." — https://creativecommons.org/licenses/by/4.0/legalcode
- Human-readable summary ("You are free to ... Adapt — remix, transform, and build upon the material for any purpose, even commercially."): https://creativecommons.org/licenses/by/4.0/
- Verified on the ADS dataset download page for EAC4 (retrieved 2026-06-28): licence listed as "CC-BY licence", required to be accepted prior to download.

> Licence status: **VERIFIED — permits derivatives** (CC-BY-4.0). No non-commercial or no-derivatives restriction was found.

---

## Data dictionary

Fields below are verified from the CAMS Global Reanalysis (EAC4) ADS dataset documentation (retrieved 2026-06-28). EAC4 distributes 200+ variables; the table lists representative, verified variable groups plus the structural/coordinate fields. Rows that could not be individually confirmed are marked **[unverified]**.

| Field / variable | Type | Units | Description | Allowed values / null handling |
|---|---|---|---|---|
| `time` | datetime (coordinate) | UTC timestamp | Analysis valid time | 2003–2025, 3-hourly steps; no nulls in coordinate |
| `latitude` | float (coordinate) | degrees_north | Grid latitude | -90 to 90 at 0.75° spacing |
| `longitude` | float (coordinate) | degrees_east | Grid longitude | 0 to 360 (or -180 to 180) at 0.75° spacing |
| `level` (model level) | int (coordinate) | model level number | Vertical model level | 60 model levels |
| `level` (pressure level) | int (coordinate) | hPa | Vertical pressure level | 25 levels, 1000–1 hPa |
| Carbon monoxide (`co`) | float | kg kg⁻¹ (mass mixing ratio) | Reactive gas concentration | non-negative; fill/missing via GRIB/NetCDF `_FillValue` |
| Ozone (`go3`) | float | kg kg⁻¹ | Reactive gas concentration | non-negative; `_FillValue` for missing |
| Nitrogen dioxide (`no2`) | float | kg kg⁻¹ | Reactive gas concentration | non-negative; `_FillValue` for missing |
| Sulphur dioxide (`so2`) | float | kg kg⁻¹ | Reactive gas concentration | non-negative; `_FillValue` for missing |
| Methane (`ch4`) | float | kg kg⁻¹ | Greenhouse gas concentration | non-negative; `_FillValue` for missing |
| Ammonia (`nh3`) | float | kg kg⁻¹ | Reactive gas concentration | non-negative; `_FillValue` for missing |
| Aerosol species (black carbon, dust, sea salt, organic matter, sulphate) | float | mass mixing ratio (kg kg⁻¹) | Aerosol composition fields | non-negative; `_FillValue` for missing |
| Aerosol optical depths (e.g. `aod550`) | float | dimensionless | Column-integrated optical depth | non-negative; `_FillValue` for missing |
| Particulate matter `pm1`, `pm2p5`, `pm10` | float | kg m⁻³ | Particulate mass concentration | non-negative; `_FillValue` for missing |
| Temperature (`t`) | float | K | Meteorological field | physical range; `_FillValue` for missing |
| Relative humidity (`r`) | float | % | Meteorological field | 0–100 (approx); `_FillValue` for missing |
| Wind components (`u`, `v`) | float | m s⁻¹ | Horizontal wind | `_FillValue` for missing |
| Pressure / surface pressure (`sp`) | float | Pa | Meteorological field | non-negative; `_FillValue` for missing |
| Geopotential (`z`) | float | m² s⁻² | Meteorological field | `_FillValue` for missing |
| Total-column species (e.g. `tcco`, `tc_*`) | float | kg m⁻² | Vertically integrated column mass | non-negative; `_FillValue` for missing |
| Individual short-names for all 200+ variables | mixed | per-variable | Full variable inventory | **[unverified]** — consult ADS variable listing / GRIB parameter database |

**Notes:** Native distribution format is **GRIB** (with optional NetCDF conversion). In GRIB/NetCDF, missing data is encoded via a `_FillValue` / bitmap rather than an explicit null. Exact short-names and per-variable scaling/offset should be read from the GRIB parameter table at download time.

---

## Datasheet for Datasets

**Motivation.** CAMS provides continuous, consistent global information on atmospheric composition — air pollutants, greenhouse gases, aerosols, ozone, and solar radiation — to support air-quality monitoring, health and climate research, policy, and downstream services. The reanalysis (EAC4) gives a long, internally consistent record; forecasts support near-real-time decision making. Created by CAMS/ECMWF as a public service of the EU Copernicus Programme.

**Composition.** Modelled (not raw observational) gridded fields produced by data assimilation combining a forecast model with satellite and in-situ observations. Each "instance" is a gridded field at a given time, level, latitude and longitude. EAC4 covers 2003–2025, 3-hourly, at 0.75°×0.75°, with 60 model levels and 25 pressure levels, and 200+ composition and meteorological variables. No personal or identifying data — fields are geophysical quantities over a global grid.

**Collection process.** Observations from satellites and ground networks are assimilated into ECMWF's Integrated Forecasting System (IFS) with atmospheric-composition modules. The product is the model analysis/forecast, so values are model estimates constrained by observations, not direct measurements.

**Preprocessing / cleaning.** Quality control and bias correction are applied to assimilated observations within the assimilation system; outputs are post-processed onto regular grids and pressure levels. Users typically convert GRIB to NetCDF and apply scaling/offset and unit conversions.

**Uses.** Air-quality assessment and forecasting, health-exposure and epidemiological studies, climate and greenhouse-gas research, renewable-energy (solar) planning, and education. Caution: reanalysis/forecast values are model estimates with spatial/temporal smoothing — not a substitute for local measurement stations for point-accurate readings.

**Distribution.** Free and open via the Atmosphere Data Store (ADS) at https://ads.atmosphere.copernicus.eu/ after accepting the licence; programmatic access via the ADS API/CDS-style client. Governed by CC-BY-4.0.

**Maintenance.** Maintained by CAMS/ECMWF on behalf of the European Commission. Reanalysis is extended/reprocessed periodically; forecasts are produced operationally on a daily cycle. Versioning and DOIs are published per dataset (EAC4 DOI: 10.24381/d58bbf47).

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
  "name": "CAMS Global Reanalysis (EAC4)",
  "description": "Copernicus Atmosphere Monitoring Service global reanalysis of atmospheric composition (reactive gases, aerosols, particulates, greenhouse gases) and meteorology, 2003-2025, 3-hourly, 0.75-degree global grid. Modelled fields from data assimilation. Documentation datasheet only; no data is hosted here.",
  "url": "https://ads.atmosphere.copernicus.eu/datasets/cams-global-reanalysis-eac4",
  "sameAs": "https://doi.org/10.24381/d58bbf47",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Organization",
    "name": "Copernicus Atmosphere Monitoring Service (CAMS) / ECMWF",
    "url": "https://atmosphere.copernicus.eu/"
  },
  "publisher": {
    "@type": "Organization",
    "name": "ECMWF on behalf of the European Commission (Copernicus Programme)"
  },
  "datePublished": "2026-06-28",
  "citation": "Copernicus Atmosphere Monitoring Service (CAMS), ECMWF. CAMS global reanalysis (EAC4). DOI: 10.24381/d58bbf47.",
  "keywords": ["air quality", "atmospheric composition", "reanalysis", "aerosols", "greenhouse gases", "Copernicus", "CAMS"],
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "eac4-grib",
      "name": "EAC4 GRIB distribution (via ADS, not hosted here)",
      "encodingFormat": "application/x-grib",
      "contentUrl": "https://ads.atmosphere.copernicus.eu/datasets/cams-global-reanalysis-eac4"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "fields",
      "name": "fields",
      "field": [
        {"@type": "cr:Field", "@id": "fields/time", "name": "time", "dataType": "sc:DateTime", "description": "Analysis valid time (UTC), 3-hourly"},
        {"@type": "cr:Field", "@id": "fields/latitude", "name": "latitude", "dataType": "sc:Float", "description": "degrees_north, 0.75-degree spacing"},
        {"@type": "cr:Field", "@id": "fields/longitude", "name": "longitude", "dataType": "sc:Float", "description": "degrees_east, 0.75-degree spacing"},
        {"@type": "cr:Field", "@id": "fields/go3", "name": "ozone", "dataType": "sc:Float", "description": "Ozone mass mixing ratio (kg kg-1)"},
        {"@type": "cr:Field", "@id": "fields/no2", "name": "nitrogen_dioxide", "dataType": "sc:Float", "description": "NO2 mass mixing ratio (kg kg-1)"},
        {"@type": "cr:Field", "@id": "fields/pm2p5", "name": "pm2p5", "dataType": "sc:Float", "description": "Particulate matter < 2.5um (kg m-3)"}
      ]
    }
  ]
}
```

---

## Validation script

Documentation only. The script below validates the **structure** of a CAMS/EAC4 NetCDF file that a user has already downloaded themselves under the licence. It does **not** download, host, or republish any data.

```python
#!/usr/bin/env python3
"""Validate the structure of a locally-held CAMS EAC4 NetCDF file.
Does NOT download or host data. Run against a file you obtained yourself
from the Atmosphere Data Store under the CC-BY-4.0 licence.

Usage: python validate_eac4.py path/to/eac4.nc
"""
import sys

EXPECTED_COORDS = {"time", "latitude", "longitude"}
# A few representative composition variables (short-names vary by request):
EXPECTED_SAMPLE_VARS = {"go3", "no2", "co"}  # adjust to your variable request
EXPECTED_LAT_RES = 0.75
EXPECTED_LON_RES = 0.75


def main(path: str) -> int:
    try:
        import xarray as xr  # netCDF4/xarray must be installed locally
    except ImportError:
        print("FAIL: install xarray + netCDF4 to validate (pip install xarray netCDF4)")
        return 2

    ds = xr.open_dataset(path)
    ok = True

    missing_coords = EXPECTED_COORDS - set(ds.coords) - set(ds.variables)
    if missing_coords:
        print(f"FAIL: missing coordinates: {sorted(missing_coords)}")
        ok = False
    else:
        print("PASS: required coordinates present")

    present_vars = set(ds.data_vars)
    found = EXPECTED_SAMPLE_VARS & present_vars
    if not found:
        print(f"WARN: none of the sample vars {sorted(EXPECTED_SAMPLE_VARS)} found; "
              f"available: {sorted(present_vars)[:10]}...")
    else:
        print(f"PASS: found composition vars: {sorted(found)}")

    # Spatial resolution check (best-effort)
    if "latitude" in ds.coords and ds["latitude"].size > 1:
        res = abs(float(ds["latitude"][1] - ds["latitude"][0]))
        if abs(res - EXPECTED_LAT_RES) > 0.01:
            print(f"WARN: latitude resolution {res} != expected {EXPECTED_LAT_RES}")
        else:
            print(f"PASS: latitude resolution ~{EXPECTED_LAT_RES} deg")

    # Row/cell count sanity (no value inspection, structure only)
    print(f"INFO: dims = {dict(ds.sizes)}")

    return 0 if ok else 1


if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__)
        sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

---

## Limitations & gaps

- **Field-level completeness not exhaustively verified.** EAC4 distributes 200+ variables; this datasheet verifies the structural coordinates and representative composition/meteorology variable groups from the ADS documentation, not every individual short-name. Rows marked **[unverified]** require the live ADS variable listing / GRIB parameter table.
- **Licence verification** is based on the ADS EAC4 dataset page (which lists the "CC-BY licence", retrieved 2026-06-28) plus the published CC-BY-4.0 legal text. A byte-level hash/archived snapshot of the exact accepted licence text was **not** captured in this pass — the acceptance-time licence on ADS should be archived alongside any operational reuse.
- **No data was downloaded, sampled, mirrored, transformed, or committed.** Units, fill-value conventions, and scaling/offset descriptions are drawn from documentation and standard GRIB/NetCDF conventions; confirm exact encodings from the file metadata at use time.
- **Modelled, not measured.** Values are model analyses/forecasts constrained by observations; treat as estimates, not point measurements.
- **Forecast vs reanalysis.** This datasheet centers EAC4 (reanalysis) as the representative product; CAMS forecast products share the access portal and licence but have different temporal cadence and variable subsets not individually documented here.
- **No PII.** The dataset contains geophysical gridded fields only; no personal or identifying data was found or documented.
