# Datasheet: GISTEMP — GISS Surface Temperature Analysis (v4)

**One-line summary:** A documentation datasheet for NASA GISS's GISTEMP, a widely cited
global surface-temperature anomaly index (1880–present) derived from land station and
sea-surface temperature records.

*This datasheet (the document you are reading) is licensed under **CC-BY-4.0**.*
*It is documentation only: it does not host, mirror, or republish any GISTEMP data.*

---

## Provenance & attribution

| Field | Value |
|---|---|
| **Dataset** | GISS Surface Temperature Analysis (GISTEMP), version 4 |
| **Publisher / creator** | NASA Goddard Institute for Space Studies (NASA GISS) |
| **Source URL** | https://data.giss.nasa.gov/gistemp/ |
| **Retrieval date** | 2026-06-28 |
| **Catalog id (candidate)** | cat-climate-003 |
| **Upstream data sources** | Land: NOAA GHCN v4 (meteorological stations); Ocean: NOAA ERSST v5 |
| **Key references** | Hansen et al. (2010); Lenssen et al. (2024), *J. Geophys. Res. Atmos.* 129(17):e2023JD040179 |

**Required attribution string** (as specified on the source page):

> GISTEMP Team, 2026: GISS Surface Temperature Analysis (GISTEMP), version 4. NASA Goddard
> Institute for Space Studies. Dataset accessed 2026-06-28 at https://data.giss.nasa.gov/gistemp/.

Accompanying scholarly citation:

> Lenssen, N., G. Schmidt, M. Hendrickson, P. Jacobs, M. Menne, and R. Ruedy, 2024:
> A NASA GISTEMPv4 global surface temperature uncertainty record. *J. Geophys. Res.
> Atmos.*, 129(17), e2023JD040179.

---

## Source licence

**Licence:** U.S. Government work — **public domain** (not subject to copyright in the
United States).

**Verification — confirmed to permit derivatives:**

- NASA's brand/media guidance states (retrieved 2026-06-28,
  https://www.nasa.gov/nasa-brand-center/images-and-media/):
  > "NASA content – images, audio, video, and media files … generally are not subject to
  > copyright in the United States."
  Content that is "not subject to copyright" is in the public domain, which by definition
  permits reuse **and derivative works** (no copyright exists to restrict transformation).
- This is consistent with U.S. statute **17 U.S.C. § 105**, under which works prepared by
  U.S. Government officers/employees as part of their official duties carry no copyright
  protection in the United States. GISTEMP is produced by NASA GISS staff.

**Conditions / caveats captured:**
- NASA *requests* acknowledgement as the source (see attribution string above) — this is a
  courtesy/citation request, not a copyright restriction.
- The source page asks that the formal citation string be used when the data is referenced.
- Carve-outs noted in NASA guidance that do **not** apply to this numeric dataset:
  identifiable persons in imagery, the NASA logo/insignia, and any third-party copyrighted
  material — none of which are present in GISTEMP tabular/gridded temperature anomalies.

**Conclusion:** The source permits derivatives. `licenseVerified = true`.

> Licence snapshot note: the acceptance criteria call for a hash + archived copy of the
> licence text. This datasheet records the verbatim licence quote, source URLs, and
> retrieval date inline above; a binary archive/hash artifact is **not** included in this
> documentation-only deliverable and is flagged under *Limitations & gaps*.

---

## Data dictionary

GISTEMP is distributed in several products. The most commonly reused product is the
**global / hemispheric / zonal tabular anomaly series** (e.g. `GLB.Ts+dSST.csv`,
Land-Ocean Temperature Index). Gridded products are also offered.

### Global tabular anomaly file (Land-Ocean Temperature Index, e.g. `GLB.Ts+dSST`)

| Field | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| `Year` | integer | calendar year | Observation year | 1880 → present (verified: series runs 1880–present) |
| `Jan` … `Dec` | float | °C anomaly vs 1951–1980 baseline | Monthly mean surface-temperature anomaly | Missing months shown as `***` (unverified glyph — see note) |
| `J-D` | float | °C anomaly vs 1951–1980 | January–December (annual mean) anomaly | null when year incomplete |
| `D-N` | float | °C anomaly vs 1951–1980 | December(prev)–November meteorological-year anomaly | null when incomplete |
| `DJF` | float | °C anomaly vs 1951–1980 | Boreal winter seasonal mean | null when incomplete |
| `MAM` | float | °C anomaly vs 1951–1980 | Boreal spring seasonal mean | null when incomplete |
| `JJA` | float | °C anomaly vs 1951–1980 | Boreal summer seasonal mean | null when incomplete |
| `SON` | float | °C anomaly vs 1951–1980 | Boreal autumn seasonal mean | null when incomplete |

**Verification status of the table above:**
- ✅ **Verified from source docs (FAQ + main page, 2026-06-28):** anomalies are expressed
  relative to the **1951–1980 base period**; coverage is **1880 to present**; products
  include **zonal, hemispheric and global means**; updates occur monthly (~10th).
- ⚠️ **Unverified in this pass (documented from the published file format, not re-read from a
  live header):** the exact column header tokens (`J-D`, `D-N`, `DJF`/`MAM`/`JJA`/`SON`),
  the precise missing-value glyph (`***`), and whether the CSV ships anomalies in whole °C
  vs hundredths in some variants. These rows should be re-confirmed against a header read of
  the live file before relying on exact tokens.

### Gridded products (alternative distribution)

| Product | Format | Resolution | Notes (verified 2026-06-28) |
|---|---|---|---|
| LOTI gridded | netCDF | 2°×2° regular grid | Anomalies vs 1951–1980 baseline |
| LOTI gridded | Zarr v3 (compressed dir) | 2°×2° regular grid | Same content, cloud-native format |
| SBBX | compressed binary | equal-area grid | Subbox time series |
| AIRS | gridded | 2°×2° | Satellite anomalies vs **2007–2016** baseline (different baseline) |

No personal or identifying fields exist in any GISTEMP product — it contains only
geophysical aggregates (temperature anomalies by time/region).

---

## Datasheet for Datasets

**Motivation.** GISTEMP estimates global and regional surface-temperature change over the
instrumental era to support climate monitoring and research. It is one of the principal
global temperature indices and benefits from a formal datasheet for reproducibility.

**Composition.** Time series of temperature *anomalies* (departures from the 1951–1980
mean), available as global/hemispheric/zonal tables and as 2°×2° gridded fields, monthly
from 1880 to present. Instances are spatio-temporal aggregates, not individual observations,
and contain no personal data.

**Collection process.** Derived, not directly collected: land-air temperatures come from
NOAA GHCN v4 station records; ocean temperatures from NOAA ERSST v5. NASA GISS combines and
spatially interpolates these into anomaly fields per the Hansen et al. (2010) and Lenssen et
al. (2024) methodology.

**Preprocessing / cleaning.** Station homogenization (GHCN v4), conversion to anomalies vs
the 1951–1980 base period, spatial interpolation (1200 km influence radius historically),
and land/ocean blending into the Land-Ocean Temperature Index. Full method in the cited
papers.

**Uses.** Climate-change detection and attribution, model evaluation, education, and public
communication. Suitable for derivative analyses (anomaly trends, comparisons). Users should
note baseline conventions differ between LOTI (1951–1980) and AIRS (2007–2016) products.

**Distribution.** Freely downloadable from https://data.giss.nasa.gov/gistemp/ as plain-text
tables, netCDF, Zarr, and SBBX. U.S. Government public-domain status; no licence fee or
access restriction. (This datasheet does not redistribute the data.)

**Maintenance.** Maintained by the GISTEMP Team at NASA GISS; updated monthly (~10th) by an
automated procedure. Versioned (current: v4). Contact and updates via the source site.

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
  "name": "GISTEMP v4 — GISS Surface Temperature Analysis",
  "description": "Global, hemispheric, zonal and 2x2-degree gridded surface-temperature anomalies (relative to the 1951-1980 base period) from 1880 to present, derived from NOAA GHCN v4 land stations and NOAA ERSST v5 sea-surface temperatures.",
  "url": "https://data.giss.nasa.gov/gistemp/",
  "license": "https://www.usa.gov/government-works",
  "creator": {
    "@type": "Organization",
    "name": "NASA Goddard Institute for Space Studies (GISTEMP Team)",
    "url": "https://www.giss.nasa.gov/"
  },
  "citation": "GISTEMP Team, 2026: GISS Surface Temperature Analysis (GISTEMP), version 4. NASA GISS. Accessed 2026-06-28 at https://data.giss.nasa.gov/gistemp/",
  "datePublished": "1999",
  "version": "4",
  "temporalCoverage": "1880/..",
  "variableMeasured": "surface temperature anomaly (degrees Celsius, vs 1951-1980 baseline)",
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "global_monthly_anomalies",
      "description": "Global Land-Ocean Temperature Index, monthly/seasonal/annual anomalies.",
      "field": [
        { "@type": "cr:Field", "name": "Year", "dataType": "sc:Integer", "description": "Calendar year (1880-present)." },
        { "@type": "cr:Field", "name": "month_anomaly", "dataType": "sc:Float", "description": "Monthly mean anomaly in deg C vs 1951-1980." },
        { "@type": "cr:Field", "name": "J-D", "dataType": "sc:Float", "description": "Annual (Jan-Dec) mean anomaly in deg C." }
      ]
    }
  ]
}
```

> Note: field stubs marked above mirror the *unverified* column tokens in the data
> dictionary; confirm exact tokens against a live header read before treating this Croissant
> record as authoritative.

---

## Validation script

This script checks the **expected structure** of a GISTEMP global tabular file that a user
has **already obtained themselves** from the official source. It does **not** download, host,
or transform the dataset — it only validates a local file path the user supplies.

```python
#!/usr/bin/env python3
"""Validate the structure of a GISTEMP global tabular anomaly file (e.g. GLB.Ts+dSST.csv).

Documentation-only: this script does NOT download or host any data. Point it at a file you
downloaded yourself from https://data.giss.nasa.gov/gistemp/ .

Usage: python validate_gistemp.py /path/to/GLB.Ts+dSST.csv
"""
import csv
import sys

EXPECTED_COLUMNS = (
    ["Year"]
    + ["Jan", "Feb", "Mar", "Apr", "May", "Jun",
       "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"]
    + ["J-D", "D-N", "DJF", "MAM", "JJA", "SON"]
)
MISSING_TOKENS = {"***", "****", ""}  # GISTEMP marks missing values with asterisks


def main(path: str) -> int:
    with open(path, newline="", encoding="utf-8") as fh:
        rows = [r for r in csv.reader(fh) if r and any(c.strip() for c in r)]

    # The header row is the line whose first cell is exactly "Year".
    header_idx = next((i for i, r in enumerate(rows) if r and r[0].strip() == "Year"), None)
    if header_idx is None:
        print("FAIL: no 'Year' header row found")
        return 1

    header = [c.strip() for c in rows[header_idx]]
    missing_cols = [c for c in EXPECTED_COLUMNS if c not in header]
    if missing_cols:
        print(f"WARN: expected columns not found (format may differ): {missing_cols}")

    data = rows[header_idx + 1:]
    data = [r for r in data if r and r[0].strip().isdigit()]
    if not data:
        print("FAIL: no data rows parsed")
        return 1

    years = [int(r[0]) for r in data]
    first, last = min(years), max(years)
    print(f"OK: {len(data)} data rows; year range {first}-{last}")

    if first != 1880:
        print(f"WARN: series expected to start at 1880, found {first}")

    # Spot-check that month cells are floats or recognised missing tokens.
    bad = 0
    for r in data:
        for cell in r[1:13]:
            v = cell.strip()
            if v in MISSING_TOKENS:
                continue
            try:
                float(v)
            except ValueError:
                bad += 1
    print(f"{'OK' if bad == 0 else 'WARN'}: {bad} unparseable monthly cells")
    return 0


if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__)
        sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

**Expected data-quality result:** one row per year from 1880 to the current year; 12 monthly
columns plus annual/seasonal aggregates; recent-month cells may be missing (`***`) before the
monthly update; anomalies typically within roughly ±2 °C of the 1951–1980 baseline.

---

## Limitations & gaps

- **Exact column tokens unverified.** The source FAQ/main page confirm coverage (1880–present),
  baseline (1951–1980), units (°C anomalies), and the existence of global/hemispheric/zonal
  means, but did **not** expose the literal CSV header tokens or the missing-value glyph.
  Those rows are documented from the established published file format and are marked ⚠️
  unverified; re-confirm against a live header read.
- **Licence text archive/hash not attached.** Verification is recorded as verbatim quotes +
  source URLs + retrieval date inline, but a binary archived copy of the licence text with a
  content hash (per acceptance criteria) is not bundled in this documentation-only file.
- **No data sampled.** No GISTEMP rows were downloaded, sampled, transformed, hosted, or
  committed. The bounded-access (≤1000-row sample) step in the acceptance criteria was **not**
  performed; field types/values are inferred from documentation, not from a live sample.
- **Multiple products, one focus.** The data dictionary focuses on the global tabular LOTI
  product; netCDF/Zarr/SBBX/AIRS products are summarised but not field-mapped in detail.
  Note the AIRS product uses a different (2007–2016) baseline.
- **PII:** none. GISTEMP contains only geophysical aggregates; no personal or identifying
  fields exist or were documented.
