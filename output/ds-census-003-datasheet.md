# Datasheet — Eurostat Population & Demography Statistics

**One-line summary:** Documentation datasheet for Eurostat's pan-EU population and demography
statistics (population stock, vital events, demographic indicators, censuses, and projections),
provided as comparable aggregate statistics across EU/EFTA countries and regions.

*This datasheet (the documentation in this file) is licensed under **CC-BY-4.0**.*

> **Documentation only.** This file describes an external open dataset. It does not host, mirror,
> transform, sample, or republish any of the underlying data, and contains no personal or
> identifying information. Eurostat publishes only aggregate statistics.

---

## Provenance & attribution

| Field | Value |
|---|---|
| **Publisher / creator** | Eurostat — Statistical Office of the European Union |
| **Dataset / topic** | Population and demography statistics |
| **Source URL** | https://ec.europa.eu/eurostat/web/population-demography |
| **Catalog id (candidate)** | cat-census-003 |
| **Retrieval date** | 2026-06-28 |
| **Required attribution string** | "Source: Eurostat" (acknowledge the source and indicate if changes were made), per the Eurostat copyright notice. |

Eurostat aggregates and harmonises data supplied by the national statistical institutes (NSIs)
of EU Member States and EFTA countries to produce comparable, EU-wide demographic statistics.

---

## Source licence

- **Verified licence:** Creative Commons Attribution 4.0 International (**CC BY 4.0**).
- **Citation / clause (Eurostat copyright notice,
  https://ec.europa.eu/eurostat/web/main/help/copyright-notice, retrieved 2026-06-28):**
  > "The copyright for the editorial content of this website, which is owned by the EU, is
  > licensed under the Creative Commons Attribution 4.0 International licence."
  Reuse (including of statistical data) is authorised, including commercial reuse and derivatives,
  provided the source is acknowledged and any changes are indicated. This implements the
  Commission's reuse policy (Commission Decision of 12 December 2011 on the reuse of Commission
  documents, 2011/833/EU).
- **Derivatives permitted:** YES — CC BY 4.0 expressly permits adaptation/derivatives with
  attribution. The legal text is at https://creativecommons.org/licenses/by/4.0/.
- **Known exceptions (do not affect this datasheet, recorded for completeness):** certain trade
  data and some third-party / non-EU-EFTA content carry reuse restrictions, and additional rights
  clearance may apply where identifiable private individuals or third-party works appear. The
  population & demography statistics documented here are aggregate EU/EFTA statistics.

Licence status: **VERIFIED — permits derivatives.**

---

## Data dictionary

Eurostat demography is published as multiple multidimensional datasets (data cubes) rather than a
single flat table. The fields below are the **common dimensions** observed across Eurostat
demography data cubes (e.g. `demo_pjan`, `demo_gind`, `demo_r_pjangrp3`). Field *codes* follow
Eurostat's standard SDMX-style dimension naming; exact code lists vary per cube and per release.
Rows marked **(unverified)** were not confirmed field-by-field against a specific downloaded cube
(no data was downloaded — documentation only) and should be checked against the cube's metadata
(DSD) before use.

| Field (dimension) | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| `geo` | code (string) | — | Geographic area: country / NUTS region / EU aggregate | NUTS / country codes (e.g. `DE`, `FR`, `EU27_2020`); not null |
| `time` (`TIME_PERIOD`) | year (integer) | calendar year | Reference period | e.g. `2024`; not null |
| `sex` | code (string) | — | Sex breakdown | `T` (total), `M` (male), `F` (female) |
| `age` | code (string) | — | Age class | e.g. `TOTAL`, `Y_LT1`, `Y1`…`Y_OPEN`, `Y_GE65` *(unverified exact list per cube)* |
| `unit` | code (string) | persons / rate / years | Measure unit | e.g. `NR` (number), `RT` (rate), `YR` (years) *(unverified per cube)* |
| `OBS_VALUE` (value) | numeric (float/int) | per `unit` | The observed statistic | may be null/missing when not available |
| `OBS_FLAG` | code (string) | — | Observation status flag | e.g. `p` provisional, `e` estimated, `b` break, `:` not available *(unverified per cube)* |
| `indic_de` | code (string) | — | Demographic indicator (in indicator cubes such as `demo_gind`) | e.g. crude birth/death rate, natural change *(unverified exact list)* |
| `freq` | code (string) | — | Frequency | typically `A` (annual) *(unverified)* |

**Confirmed from the source overview page:** the topic provides population stock and balance,
vital events (births, deaths, marriages, divorces), demographic indicators (population change,
structure, density, fertility, mortality), census characteristics, and population projections,
broken down at national, regional and local levels and on a harmonised 1 km² grid.

---

## Datasheet for Datasets

**Motivation.** Created to provide comparable, harmonised demographic statistics across the EU and
EFTA to support EU and national policymaking, research, and public information. Produced by
Eurostat as part of the European Statistical System.

**Composition.** Aggregate statistics (counts, rates, indicators) on population stock, vital
events, demographic indicators, censuses, and long-range projections. Instances are
statistical observations indexed by geography, time, and demographic breakdowns (sex, age, etc.).
No individual-level records — there is no microdata or PII in these published aggregates.

**Collection process.** Compiled by Eurostat from data transmitted by national statistical
institutes under EU regulations and harmonised methodologies; censuses follow EU census
legislation. Projections are modelled by Eurostat.

**Preprocessing / cleaning / labelling.** Eurostat harmonises national inputs to common
classifications (NUTS regions, standard age/sex breakdowns), applies validation, and annotates
observations with status flags (provisional, estimated, break in series, not available).

**Uses.** Demographic research, policy analysis, regional development, comparative EU statistics,
education, journalism. Not suitable for inferring information about identifiable individuals
(aggregates only). Users must respect the per-dataset exceptions noted under Source licence.

**Distribution.** Published openly via the Eurostat website and dissemination API / bulk download
under CC BY 4.0. This datasheet does not redistribute the data; consult the source URL.

**Maintenance.** Maintained and regularly updated by Eurostat; datasets carry release/update
metadata and version identifiers per data cube.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/"
  },
  "@type": "Dataset",
  "name": "Eurostat Population & Demography Statistics",
  "description": "Comparable pan-EU/EFTA aggregate statistics on population stock, vital events, demographic indicators, censuses, and projections, harmonised by Eurostat from national statistical institutes.",
  "url": "https://ec.europa.eu/eurostat/web/population-demography",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Organization",
    "name": "Eurostat — Statistical Office of the European Union",
    "url": "https://ec.europa.eu/eurostat"
  },
  "datePublished": "2026-06-28",
  "citation": "Source: Eurostat",
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "demography_observations",
      "field": [
        { "@type": "cr:Field", "name": "geo", "dataType": "sc:Text", "description": "Geographic area (country / NUTS region / EU aggregate)" },
        { "@type": "cr:Field", "name": "time", "dataType": "sc:Integer", "description": "Reference year (TIME_PERIOD)" },
        { "@type": "cr:Field", "name": "sex", "dataType": "sc:Text", "description": "Sex: T/M/F" },
        { "@type": "cr:Field", "name": "age", "dataType": "sc:Text", "description": "Age class code" },
        { "@type": "cr:Field", "name": "OBS_VALUE", "dataType": "sc:Float", "description": "Observed statistic value" },
        { "@type": "cr:Field", "name": "OBS_FLAG", "dataType": "sc:Text", "description": "Observation status flag" }
      ]
    }
  ]
}
```

---

## Validation script

The following script documents how to validate the **structure** of a Eurostat demography cube
that a user has obtained themselves (e.g. a TSV from the Eurostat bulk-download / API). It does
**not** download, host, or transform the dataset — it only checks a file the user already has.

```python
#!/usr/bin/env python3
"""Validate the structure of a Eurostat demography data cube (TSV) the user already downloaded.
Documentation-only: this script does NOT fetch, host, or republish any data."""
import csv
import sys

# Expected dimension columns commonly present in Eurostat demography cubes.
# Adjust to the specific cube's Data Structure Definition (DSD) before relying on it.
EXPECTED_DIMENSIONS = {"geo", "time", "sex", "age", "unit"}
MIN_ROWS = 1  # sanity floor; set to a cube-specific expected count if known

def validate(path: str) -> int:
    with open(path, newline="", encoding="utf-8") as fh:
        # Eurostat bulk TSV uses tab separation; the first column header often packs
        # several dimensions as "unit,sex,age,geo\\TIME_PERIOD". This check is heuristic.
        reader = csv.reader(fh, delimiter="\t")
        header = next(reader, None)
        if not header:
            print("FAIL: empty file")
            return 1
        flat = ",".join(header).lower()
        missing = [d for d in EXPECTED_DIMENSIONS if d not in flat]
        rows = sum(1 for _ in reader)
        print(f"rows (excl. header): {rows}")
        if missing:
            print(f"WARN: expected dimensions not found in header: {sorted(missing)}")
        if rows < MIN_ROWS:
            print(f"FAIL: row count {rows} < expected minimum {MIN_ROWS}")
            return 1
        print("OK: structural checks passed (verify dimension codes against the cube DSD).")
        return 0

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("usage: validate.py <path-to-eurostat-cube.tsv>")
        sys.exit(2)
    sys.exit(validate(sys.argv[1]))
```

---

## Limitations & gaps

- **Field codes are common-dimension level, not cube-exact.** Eurostat publishes many demography
  cubes, each with its own dimensions and code lists. Rows marked *(unverified)* and the exact
  allowed-value lists were **not** confirmed against a specific downloaded cube, because no data
  was downloaded (documentation only). Validate field codes against each cube's metadata (DSD).
- **No data inspection / no sample.** No header read, no row sample, and no row-count baseline were
  taken; `MIN_ROWS` in the validation script is a placeholder.
- **Licence exceptions exist.** Certain trade data and some third-party / non-EU-EFTA content carry
  reuse restrictions; the population & demography aggregates documented here are not believed to be
  affected, but users handling adjacent Eurostat datasets should re-check.
- **Source pages may evolve.** The overview and copyright-notice pages were retrieved 2026-06-28;
  Eurostat may revise content or methodology. Re-verify the licence clause and field structure at
  time of use.
- **Croissant record is minimal.** It provides valid schema.org/Dataset JSON-LD with field stubs;
  it is not an exhaustive description of every cube or distribution.
