# Datasheet — Global Carbon Budget (GCB 2024)

> One-line summary: An authoritative annual accounting of the global CO₂ budget — anthropogenic
> sources (fossil + land-use change) and the partitioning of CO₂ among the atmosphere, ocean, and
> land sinks — published by the Global Carbon Project.

*This datasheet (the documentation in this file) is licensed under **CC-BY-4.0**. It documents an
external dataset; it does not contain, host, mirror, or republish the dataset itself.*

- **Task ID:** ds-climate-005
- **Catalog id (candidate):** cat-climate-005
- **Retrieval / review date:** 2026-06-28
- **Datasheet status:** Final — source licence verified to permit derivatives (see *Source licence*).

---

## Provenance & attribution

| Field | Value |
|---|---|
| **Dataset** | Global Carbon Budget 2024 (data product, Version 1.x) |
| **Publisher / creator** | Global Carbon Project (GCP); lead author Prof. Pierre Friedlingstein, University of Exeter, Global Systems Institute |
| **Documentation / landing pages** | https://globalcarbonbudget.org/ and (legacy) https://www.globalcarbonproject.org/carbonbudget/ |
| **Data product DOI (source of record)** | https://doi.org/10.18160/GCP-2024 (resolves to ICOS Carbon Portal: https://www.icos-cp.eu/GCP/2024) |
| **Companion peer-reviewed paper** | Friedlingstein, P., O'Sullivan, M., Jones, M. W., et al. (2025). *Global Carbon Budget 2024.* Earth System Science Data, 17, 965–1039. https://doi.org/10.5194/essd-17-965-2025 |
| **Associated gridded inversion product** | https://doi.org/10.18160/4R5W-VNBV (netCDF; not the subject of this datasheet) |
| **Retrieval date** | 2026-06-28 |

**Required attribution string** (as requested on the ICOS data DOI landing page):

> Global Carbon Project. (2024). *Supplemental data of Global Carbon Budget 2024 (Version 1.0)*
> [Data set]. Global Carbon Project. https://doi.org/10.18160/gcp-2024

When using the analysis/methods, also cite the companion paper: Friedlingstein et al. (2025),
Earth System Science Data, https://doi.org/10.5194/essd-17-965-2025. The ICOS landing page also
notes: *"The use of data is conditional on citing the original data sources."*

---

## Source licence

- **Licence (data product, ICOS Carbon Portal):** Creative Commons Attribution 4.0 International
  (**CC BY 4.0**). Verified on the ICOS Carbon Portal landing page for the product
  (https://www.icos-cp.eu/GCP/2024), retrieved 2026-06-28.
- **Licence (companion paper, ESSD):** Creative Commons Attribution 4.0 License. The article page
  states verbatim: *"© Author(s) 2025. This work is distributed under the Creative Commons
  Attribution 4.0 License."* (https://doi.org/10.5194/essd-17-965-2025).
- **Does it permit derivatives? YES.** CC BY 4.0 explicitly grants the right to *"Adapt — remix,
  transform, and build upon the material for any purpose, even commercially"* subject only to
  attribution. Licence deed: https://creativecommons.org/licenses/by/4.0/ ; legal code:
  https://creativecommons.org/licenses/by/4.0/legalcode.
- **Attribution obligation:** retain attribution as above and indicate if changes were made.
- **Note on derived sources:** the budget is itself a synthesis of many upstream datasets/models;
  the ICOS condition *"citing the original data sources"* applies when reproducing component inputs.

A licence snapshot (the CC BY 4.0 deed/legalcode text) should be archived alongside this datasheet
in the repository's provenance store and hashed; archiving binary/license-text copies is out of
scope for this documentation-only deed and is noted in *Limitations & gaps*.

---

## Data dictionary

The Global Carbon Budget is distributed as Excel workbooks (`.xlsx`). The primary workbook is the
**"Global Carbon Budget"** product; companion workbooks cover **National Fossil Carbon Emissions**
and **National Land-Use Change Carbon Emissions**. The fields below are the canonical global-budget
budget terms, with names, units, and definitions **verified from the companion ESSD paper and the
ICOS landing page**. The **exact spreadsheet column-header strings, tab/sheet names, and per-cell
null encodings were NOT opened/read** for this documentation-only deed and are marked *unverified*.

Global annual budget terms (one row per year; flux terms in **GtC yr⁻¹**, i.e. PgC yr⁻¹):

| Field (canonical) | Symbol | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|---|
| Year | — | integer | calendar year | Year of the annual estimate (series historically begins 1959). | Positive 4-digit year; no nulls expected *(unverified header text)* |
| Fossil CO₂ emissions | E_FOS | float | GtC yr⁻¹ | Emissions from fossil fuel combustion and industry (incl. cement), net of the cement carbonation sink. | ≥ 0; *(unverified)* |
| Land-use change emissions | E_LUC | float | GtC yr⁻¹ | Net CO₂ emissions from land-use, land-use change and forestry. | Can be small/negative in principle; *(unverified)* |
| Atmospheric growth rate | G_ATM | float | GtC yr⁻¹ | Annual increase of CO₂ in the atmosphere. | typically > 0; *(unverified)* |
| Ocean sink | S_OCEAN | float | GtC yr⁻¹ | Net CO₂ uptake by the ocean. | ≥ 0; *(unverified)* |
| Land sink | S_LAND | float | GtC yr⁻¹ | Net CO₂ uptake by the terrestrial biosphere (excl. land-use change). | ≥ 0; *(unverified)* |
| Cement carbonation sink | S_CEMENT | float | GtC yr⁻¹ | CO₂ re-absorbed by cement materials over time. | ≥ 0; sometimes folded into E_FOS; *(unverified)* |
| Budget imbalance | B_IM | float | GtC yr⁻¹ | Residual: E_FOS + E_LUC − (G_ATM + S_OCEAN + S_LAND). Diagnostic of mismatch. | can be ±, near 0; *(unverified)* |

Reservoir/stock quantities, where present, are in **GtC** (not per year). National workbooks are
indexed by **country/territory** and **year**; their exact column layout is *unverified* here.

*Verification basis:* term definitions, symbols and units (GtC yr⁻¹ for fluxes; GtC for reservoirs)
are taken from Friedlingstein et al. (2025) and the ICOS landing page. Representative 2023 values
reported in the paper: E_FOS 10.1±0.5, E_LUC 1.0±0.7, G_ATM 5.9±0.2, S_OCEAN 2.9±0.4,
S_LAND 2.3±1.0, B_IM ≈ −0.02 (all GtC yr⁻¹).

---

## Datasheet for Datasets

**Motivation.** Created to provide a single, peer-reviewed, annually updated, authoritative estimate
of the global carbon budget — quantifying anthropogenic CO₂ emissions and how they are partitioned
among atmosphere, ocean, and land — to support climate science, policy (e.g. Global Stocktake), and
public understanding. Produced by the Global Carbon Project (international research consortium).

**Composition.** Time series (annual, historically from 1959, with longer reconstructions for some
terms) of global CO₂ budget components plus national-level fossil and land-use-change emissions. It
is a synthesis/aggregate of many upstream observational datasets and process/inversion models — not
a record of individuals. **No personal or identifying data.**

**Collection process.** Each budget term is estimated by established, documented methods: fossil
emissions from energy-statistics inventories; land-use change from bookkeeping models; atmospheric
growth from the global CO₂ observation network; ocean sink from observation-based products and global
ocean biogeochemistry models; land sink from dynamic global vegetation models; with a residual
budget imbalance. Methods and uncertainties are documented in the annual ESSD paper.

**Preprocessing / cleaning / labeling.** Component estimates are harmonized to common units (GtC),
combined into the global budget, and quality-controlled against the multi-method ensemble; the
budget imbalance term explicitly surfaces residual inconsistency. Full methodology in the paper.

**Uses.** Climate trend/attribution analysis, carbon-cycle research, emissions tracking, integrated
assessment, education, and policy reporting. **Not** suitable as sub-annual, facility-level, or
real-time emissions data; uncertainty ranges must be carried through any derived analysis.

**Distribution.** Publicly distributed as Excel workbooks (and a separate netCDF gridded inversion
product) via the ICOS Carbon Portal under DOI https://doi.org/10.18160/GCP-2024, under CC BY 4.0.

**Maintenance.** Updated annually by the Global Carbon Project (each release versioned, e.g. 2024
v1.x); the companion ESSD paper is reissued each cycle. Contact via https://globalcarbonbudget.org/.

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
  "name": "Global Carbon Budget 2024",
  "description": "Annual authoritative accounting of the global CO2 budget by the Global Carbon Project: anthropogenic fossil and land-use-change emissions and their partitioning among atmospheric growth, ocean sink, and land sink, with a budget imbalance term. Flux terms in GtC/yr.",
  "url": "https://globalcarbonbudget.org/",
  "sameAs": "https://www.icos-cp.eu/GCP/2024",
  "identifier": "https://doi.org/10.18160/GCP-2024",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Organization",
    "name": "Global Carbon Project",
    "url": "https://globalcarbonbudget.org/"
  },
  "datePublished": "2024",
  "version": "2024 v1.x",
  "citation": "Friedlingstein, P., O'Sullivan, M., Jones, M. W., et al. (2025). Global Carbon Budget 2024. Earth System Science Data, 17, 965-1039. https://doi.org/10.5194/essd-17-965-2025",
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "global-carbon-budget-xlsx",
      "name": "Global Carbon Budget 2024 (Excel workbook)",
      "encodingFormat": "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
      "description": "Documentation-only stub; file not hosted or mirrored here."
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "global-annual-budget",
      "name": "Global annual carbon budget",
      "field": [
        {"@type": "cr:Field", "@id": "year", "name": "Year", "dataType": "sc:Integer", "description": "Calendar year of the annual estimate."},
        {"@type": "cr:Field", "@id": "e_fos", "name": "Fossil CO2 emissions (E_FOS)", "dataType": "sc:Float", "description": "Fossil fuel and industry emissions, GtC/yr."},
        {"@type": "cr:Field", "@id": "e_luc", "name": "Land-use change emissions (E_LUC)", "dataType": "sc:Float", "description": "Net land-use change CO2 emissions, GtC/yr."},
        {"@type": "cr:Field", "@id": "g_atm", "name": "Atmospheric growth (G_ATM)", "dataType": "sc:Float", "description": "Atmospheric CO2 growth rate, GtC/yr."},
        {"@type": "cr:Field", "@id": "s_ocean", "name": "Ocean sink (S_OCEAN)", "dataType": "sc:Float", "description": "Ocean CO2 uptake, GtC/yr."},
        {"@type": "cr:Field", "@id": "s_land", "name": "Land sink (S_LAND)", "dataType": "sc:Float", "description": "Terrestrial CO2 uptake, GtC/yr."},
        {"@type": "cr:Field", "@id": "b_im", "name": "Budget imbalance (B_IM)", "dataType": "sc:Float", "description": "Residual budget imbalance, GtC/yr."}
      ]
    }
  ]
}
```

> Note: field `@id`s above are canonical stubs (verified term definitions/units); exact spreadsheet
> source column names are not bound (`source`/`extract` omitted) because the workbook was not opened.

---

## Validation script

This script checks the *structure* of a Global Carbon Budget global-budget table that a user has
**already obtained themselves** from the official DOI. It does **not** download, host, or fetch the
data — it operates on a local file path the user supplies, and only inspects shape/columns/ranges.

```python
#!/usr/bin/env python3
"""Validate the structure of a locally-obtained Global Carbon Budget global-budget table.

Documentation-only: this script does NOT download, mirror, or host the dataset.
Obtain the data yourself from https://doi.org/10.18160/GCP-2024 (CC BY 4.0) and
pass the local path. Example:
    python validate_gcb.py ./Global_Carbon_Budget_2024.csv
"""
import sys
import csv

# Canonical budget terms (units GtC/yr). Header text in the official workbook may
# differ; treat this as a soft check and adjust EXPECTED to your exported columns.
EXPECTED = ["year", "fossil", "land", "atmospheric", "ocean", "land sink", "imbalance"]
MIN_ROWS = 50           # annual series since ~1959 -> dozens of rows expected
SENTINELS = {"", "na", "nan", "null", "n/a"}

def main(path: str) -> int:
    with open(path, newline="", encoding="utf-8-sig") as f:
        reader = csv.reader(f)
        rows = [r for r in reader if any(c.strip() for c in r)]
    if not rows:
        print("FAIL: file is empty"); return 1

    header = [h.strip().lower() for h in rows[0]]
    data = rows[1:]

    # 1) row-count sanity (annual time series)
    if len(data) < MIN_ROWS:
        print(f"WARN: only {len(data)} data rows (<{MIN_ROWS}); confirm this is the full series")

    # 2) soft column presence check (substring match, case-insensitive)
    missing = [kw for kw in EXPECTED if not any(kw in h for h in header)]
    if missing:
        print(f"WARN: expected budget terms not obviously present: {missing}")
        print(f"      actual header: {header}")

    # 3) basic value/null sanity on numeric columns
    bad = 0
    for i, row in enumerate(data, start=2):
        for cell in row[1:]:                       # skip the year column
            v = cell.strip().lower()
            if v in SENTINELS:
                continue                           # documented null/sentinel
            try:
                float(v)
            except ValueError:
                bad += 1
                if bad <= 5:
                    print(f"WARN: non-numeric value {cell!r} at row {i}")
    print(f"Checked {len(data)} rows, {len(header)} columns; {bad} non-numeric non-null cells.")
    print("PASS (structural)" if not missing and bad == 0 else "REVIEW (see warnings)")
    return 0

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__); sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

To validate the Excel workbook directly, export the relevant sheet to CSV first (e.g. with
`libreoffice --headless --convert-to csv`) and run the script on the CSV — still entirely local.

---

## Limitations & gaps

- **Spreadsheet internals not opened.** Per the documentation-only / bounded-access guardrail, the
  actual `.xlsx` workbooks were not downloaded or parsed. Exact sheet/tab names, verbatim column
  headers, per-column null encodings, and the precise national-workbook layout are therefore
  **unverified** and are marked as such in the data dictionary.
- **Field set is the canonical global budget.** Names/units/definitions are verified from the ESSD
  paper and ICOS landing page, not from the binary file; some releases fold the cement carbonation
  sink into E_FOS or add ancillary columns (per-capita, cumulative) not enumerated here.
- **Version drift.** Documentation reflects the GCB 2024 release reviewed on 2026-06-28; the GCP
  updates annually (newer releases and a 2025 cycle exist) — re-verify the DOI, version, and any
  changed columns against the latest release before use.
- **Licence snapshot/hash not embedded.** The CC BY 4.0 deed/legalcode text was cited and verified
  but not archived as a hashed copy inside this documentation-only deliverable; the provenance
  store should capture that artifact.
- **No data included.** No dataset rows, samples, or files are hosted, mirrored, or committed here,
  and no personal/identifying data exists in this aggregate product.
