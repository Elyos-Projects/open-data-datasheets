# Datasheet: CO2 & Greenhouse Gas Emissions (Our World in Data)

One-line summary: A tidy, citable, country-year panel of CO2 and greenhouse-gas
emissions compiled by Our World in Data (OWID) from authoritative scientific sources,
covering fossil/industrial CO2 by source, land-use change, other GHGs, and emissions
intensity indicators.

*This datasheet (the documentation in this file) is licensed under **CC-BY-4.0**.*
It is documentation only: it does **not** host, mirror, transform, or republish the
underlying dataset.

---

## Provenance & attribution

- **Publisher / compiler:** Our World in Data (OWID)
- **Dataset:** CO2 and Greenhouse Gas Emissions
- **Source URL (canonical):** https://github.com/owid/co2-data
- **Codebook referenced:** `owid-co2-codebook.csv` (in the same repository)
- **Retrieval date:** 2026-06-28
- **Catalog id (candidate):** cat-climate-004 / task ds-climate-004
- **File formats offered by source:** CSV, XLSX (codebook as an extra sheet), JSON

**Required attribution string (suggested):**

> Our World in Data — "CO2 and Greenhouse Gas Emissions" (https://github.com/owid/co2-data).
> Compiled by Our World in Data from the Global Carbon Budget (Global Carbon Project),
> Jones et al. "National Contributions to Climate Change", the Energy Institute Statistical
> Review of World Energy, U.S. EIA, the Maddison Project Database, and OWID population data.
> Licensed under CC-BY-4.0. Retrieved 2026-06-28.

Note: per OWID's terms, when reusing you should credit **both** Our World in Data and the
**underlying source(s)** for any specific indicator, as third-party source data remains
subject to its original licensing.

---

## Source licence (VERIFIED — permits derivatives)

- **Licence:** Creative Commons Attribution 4.0 International (**CC-BY-4.0**)
- **Where stated:** OWID README at https://github.com/owid/co2-data (License section)
- **Verbatim clause confirming derivatives/redistribution are permitted:**

  > "All visualizations, data, and code produced by *Our World in Data* are completely
  > open access under the Creative Commons BY license. You have the permission to use,
  > distribute, and reproduce these in any medium, provided the source and authors are
  > credited."

- **Canonical licence text:** https://creativecommons.org/licenses/by/4.0/
  CC-BY-4.0 grants the right to "Adapt — remix, transform, and build upon the material
  for any purpose, even commercially," subject to the Attribution condition. This
  explicitly permits derivatives.

**Caveat (recorded, not a blocker):** OWID-produced data and code are CC-BY-4.0, but the
*third-party source data* it aggregates (e.g. Global Carbon Budget, Energy Institute)
remains under each provider's own terms. This datasheet documents the OWID-compiled
product; downstream users must honour upstream source terms for individual indicators.

Conclusion: derivatives are permitted → `licenseVerified = true`. Not flagged.

---

## Data dictionary

Structure: one row per **(country, year)** in the CSV/XLSX; the JSON is keyed by country
with yearly arrays. Field names, units, and sources below are taken verbatim from
`owid-co2-codebook.csv` (retrieved 2026-06-28). Numeric emission columns are nullable —
missing where a country/year has no reported value. The codebook contains roughly 70+
columns; the table documents the core/representative verified fields. Remaining columns
follow the same naming families (`*_co2`, `*_co2_per_capita`, `cumulative_*`, `share_*`,
`*_per_gdp`) and are documented in the source codebook.

| Field | Type | Units | Description | Allowed values / nulls |
|-------|------|-------|-------------|--------------------------|
| `country` | string | — | Geographic location (country/region name). | Non-null key. |
| `year` | integer | calendar year | Year of observation. | Non-null key; historical through latest year. |
| `iso_code` | string | — | ISO 3166-1 alpha-3 three-letter country code. | Null for aggregates/regions (e.g. "World"). |
| `population` | number | people | Population estimate (spans 10,000 BCE–2100 in source population data). | Nullable. |
| `gdp` | number | international-$ (2011 prices) | Inflation-adjusted total economic output per year. | Nullable. |
| `co2` | number | million tonnes (Mt) | Annual total CO2 emissions, excluding land-use change. | Nullable. |
| `co2_growth_abs` | number | million tonnes (Mt) | Annual absolute growth in total CO2 emissions. | Nullable; may be negative. |
| `co2_growth_prct` | number | % | Annual percentage growth in total CO2 emissions. | Nullable; may be negative. |
| `co2_including_luc` | number | million tonnes (Mt) | Total CO2 emissions including land-use change. | Nullable. |
| `co2_per_capita` | number | tonnes per person | Fossil-fuel & industrial CO2 per person. | Nullable. |
| `co2_per_gdp` | number | kg per international-$ | Emissions intensity relative to economic output. | Nullable. |
| `cumulative_co2` | number | million tonnes (Mt) | Total cumulative CO2 emissions, excluding land-use change. | Nullable. |
| `cement_co2` | number | million tonnes (Mt) | Annual CO2 emissions from cement. | Nullable. |
| `cement_co2_per_capita` | number | tonnes per person | Cement CO2 emissions per person. | Nullable. |
| `coal_co2` | number | million tonnes (Mt) | Annual CO2 emissions from coal. | Nullable. |
| `coal_co2_per_capita` | number | tonnes per person | Coal CO2 emissions per person. | Nullable. |
| `cumulative_coal_co2` | number | million tonnes (Mt) | Cumulative coal CO2 emissions since first available year. | Nullable. |
| `oil_co2` | number | million tonnes (Mt) | Annual CO2 emissions from oil. | Nullable. |
| `gas_co2` | number | million tonnes (Mt) | Annual CO2 emissions from gas. | Nullable. |
| `gas_co2_per_capita` | number | tonnes per person | Gas CO2 emissions per person. | Nullable. |
| `methane` | number | million tonnes (Mt) | Annual methane emissions, including land use. | Nullable. |
| `methane_per_capita` | number | tonnes of CO2-equivalent per person | Per-person methane emissions. | Nullable. |
| `nitrous_oxide` | number | million tonnes (Mt) | Annual nitrous oxide emissions, including land use. | Nullable. |
| `nitrous_oxide_per_capita` | number | tonnes of CO2-equivalent per person | Per-person nitrous oxide emissions. | Nullable. |
| `total_ghg` | number | million tonnes (Mt) | Annual greenhouse-gas emissions, including land use. | Nullable. |

> Unverified beyond the rows above: the remaining `*_co2`, `share_global_*`, `*_per_gdp`,
> `consumption_co2*`, `flaring_co2*`, `trade_co2*`, and `energy_per_*` columns exist in the
> codebook but were not individually transcribed here — consult `owid-co2-codebook.csv` for
> authoritative definitions of each. Treat their exact units as **unconfirmed** in this file.

---

## Datasheet for Datasets

**Motivation.** Created by Our World in Data to provide a single, regularly updated,
research-grade, openly licensed dataset on CO2 and greenhouse-gas emissions, so journalists,
researchers, educators, and policymakers can analyse emissions without stitching together
disparate primary sources.

**Composition.** Country/region-year observations of emissions (total and by fuel/source:
coal, oil, gas, cement, flaring), land-use-change CO2, other greenhouse gases (methane,
nitrous oxide, total GHG), plus contextual variables (population, GDP) and derived
indicators (per capita, per GDP, cumulative, growth, global shares). Units are consistent
(Mt for emissions, tonnes per person for per-capita, CO2-equivalents for non-CO2 gases).
No personal or identifying data — observations are at country/region aggregate level only.

**Collection process.** OWID does not collect raw observations; it ingests and harmonises
published datasets: the Global Carbon Budget (Global Carbon Project), Jones et al. "National
Contributions to Climate Change", the Energy Institute Statistical Review of World Energy,
U.S. EIA international energy data, the Maddison Project Database (GDP), and OWID population
data.

**Preprocessing / cleaning.** Country-name standardisation; carbon-to-CO2 conversion using
the 3.664 factor; computation of per-capita and per-GDP intensities; regional/World
aggregation; alignment to a common country-year grid. Aggregates (e.g. "World", continents)
carry a null `iso_code`.

**Uses.** Emissions trend analysis, country comparisons, climate reporting, education,
teaching reproducible data workflows. Caution: cross-source indicators have differing
coverage and vintages; per-capita/per-GDP values depend on the population/GDP series and
should not be over-interpreted at fine resolution. Not suitable for sub-national or
facility-level analysis.

**Distribution.** Publicly distributed via the GitHub repository (CSV/XLSX/JSON) under
CC-BY-4.0. This datasheet does not redistribute the data; it links to the canonical source.

**Maintenance.** Maintained by Our World in Data; updated as upstream sources release new
vintages (the codebook references 2024/2025 source vintages). Issues and updates are tracked
in the GitHub repository.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "data": "https://schema.org/"
  },
  "@type": "Dataset",
  "name": "CO2 and Greenhouse Gas Emissions",
  "description": "Country-year panel of CO2 and greenhouse-gas emissions compiled by Our World in Data from the Global Carbon Budget, Jones et al. National Contributions to Climate Change, the Energy Institute Statistical Review of World Energy, U.S. EIA, the Maddison Project Database, and OWID population data.",
  "url": "https://github.com/owid/co2-data",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Organization",
    "name": "Our World in Data",
    "url": "https://ourworldindata.org"
  },
  "datePublished": "2026-06-28",
  "keywords": ["climate", "CO2", "greenhouse gas emissions", "open data", "country-year"],
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "owid-co2-data.csv",
      "name": "owid-co2-data.csv",
      "encodingFormat": "text/csv",
      "contentUrl": "https://github.com/owid/co2-data"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "emissions",
      "name": "emissions",
      "field": [
        { "@type": "cr:Field", "@id": "emissions/country", "name": "country", "dataType": "sc:Text", "description": "Geographic location." },
        { "@type": "cr:Field", "@id": "emissions/year", "name": "year", "dataType": "sc:Integer", "description": "Year of observation." },
        { "@type": "cr:Field", "@id": "emissions/iso_code", "name": "iso_code", "dataType": "sc:Text", "description": "ISO 3166-1 alpha-3 code; null for aggregates." },
        { "@type": "cr:Field", "@id": "emissions/co2", "name": "co2", "dataType": "sc:Float", "description": "Annual total CO2 emissions excluding land-use change (Mt)." },
        { "@type": "cr:Field", "@id": "emissions/co2_per_capita", "name": "co2_per_capita", "dataType": "sc:Float", "description": "Fossil & industrial CO2 per person (tonnes)." },
        { "@type": "cr:Field", "@id": "emissions/total_ghg", "name": "total_ghg", "dataType": "sc:Float", "description": "Annual GHG emissions including land use (Mt)." }
      ]
    }
  ]
}
```

---

## Validation script

Documentation only. This script does **not** download or host the data. Point it at a
locally obtained copy of `owid-co2-data.csv` (obtained by the user directly from the source
under CC-BY-4.0) to check that the structure matches what this datasheet documents.

```python
#!/usr/bin/env python3
"""Validate the structure of a locally-held owid-co2-data.csv against this datasheet.
Usage: python validate.py /path/to/owid-co2-data.csv
Does NOT download, mirror, or republish data. Local-only, read-only, ephemeral.
"""
import csv
import sys

EXPECTED_KEYS = {"country", "year", "iso_code"}
EXPECTED_NUMERIC = {
    "population", "gdp", "co2", "co2_growth_abs", "co2_growth_prct",
    "co2_including_luc", "co2_per_capita", "co2_per_gdp", "cumulative_co2",
    "cement_co2", "coal_co2", "oil_co2", "gas_co2",
    "methane", "nitrous_oxide", "total_ghg",
}

def main(path):
    with open(path, newline="", encoding="utf-8") as f:
        reader = csv.DictReader(f)
        cols = set(reader.fieldnames or [])
        rows = 0
        bad_year = 0
        for r in reader:
            rows += 1
            y = r.get("year", "")
            if y and not y.lstrip("-").isdigit():
                bad_year += 1

    missing_keys = EXPECTED_KEYS - cols
    missing_num = EXPECTED_NUMERIC - cols

    print(f"rows (excl. header): {rows}")
    print(f"columns: {len(cols)}")
    print(f"missing key columns: {sorted(missing_keys) or 'none'}")
    print(f"missing expected numeric columns: {sorted(missing_num) or 'none'}")
    print(f"non-integer 'year' values: {bad_year}")

    ok = not missing_keys and not missing_num and bad_year == 0 and rows > 0
    print("RESULT:", "PASS" if ok else "FAIL")
    sys.exit(0 if ok else 1)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__)
        sys.exit(2)
    main(sys.argv[1])
```

---

## Limitations & gaps

- Only the core/representative columns above were transcribed verbatim from
  `owid-co2-codebook.csv`. The full file has ~70+ columns; the remaining `share_global_*`,
  `consumption_co2*`, `trade_co2*`, `flaring_co2*`, `*_per_gdp`, and `energy_*` families were
  **not** individually verified here — consult the source codebook for their exact units and
  definitions. Rows are marked accordingly.
- Exact current **row count** and the latest covered **year** were not asserted (they change
  with each upstream vintage); the validation script checks structure, not a fixed row count.
- The licence applies to OWID-produced data/code; **upstream third-party source licences**
  for individual indicators were not each independently audited — only the OWID-compiled
  product's CC-BY-4.0 status was verified.
- No data was downloaded, sampled in bulk, hosted, or transformed in producing this
  datasheet; field metadata was read from the published codebook page only.
- The Croissant block is a minimal, hand-authored record (field stubs only) and was not run
  through an automated Croissant validator.
