# Datasheet — Our World in Data: Health Datasets

> One-line summary: A documentation datasheet for the health-related datasets compiled and
> distributed by Our World in Data (OWID), covering provenance, licensing, field structure,
> a Datasheet-for-Datasets writeup, Croissant metadata, and a validation script.
>
> **This datasheet is licensed CC-BY-4.0.** (The datasheet document only — not the underlying data.)

Documentation only. This file does **not** host, mirror, transform, or republish any OWID
data. No personal or identifying data is included; OWID health datasets are aggregate
country/region/year time series.

---

## Provenance & attribution

- **Publisher / curator:** Our World in Data (OWID), a project of Global Change Data Lab (a
  UK-registered charity) and affiliated with the University of Oxford.
- **Dataset family documented:** Our World in Data — health datasets (OWID-compiled
  indicators across topics such as life expectancy, mortality, disease burden, vaccination,
  and health-system metrics).
- **Source URL:** https://ourworldindata.org/ (per-indicator pages and CSV/API downloads
  under the same domain; catalog/API at https://docs.owid.io/).
- **Retrieval date:** 2026-06-28
- **Required attribution string (for OWID-compiled data):**
  > "Our World in Data" — and, for each indicator used, credit the underlying third-party
  > source(s) named in that indicator's metadata. Example chart-level citation form:
  > *Author(s) (Year) – "{Title}". Published online at OurWorldInData.org. Retrieved from
  > {page URL}.* Data reuse additionally requires crediting both Our World in Data and the
  > original data provider(s).

---

## Source licence

- **Verified licence (OWID-compiled data & charts):** Creative Commons Attribution 4.0
  International (**CC BY 4.0**).
- **Permits derivatives:** **Yes.** CC BY 4.0 grants rights to "reproduce and Share the
  Licensed Material, in whole or in part" and to "produce, reproduce, and Share Adapted
  Material," subject only to attribution. (CC BY 4.0 legal code, Section 2(a)(1):
  https://creativecommons.org/licenses/by/4.0/legalcode )
- **Citation confirming OWID's licence:** OWID FAQ / "How is our work copyrighted?":
  https://ourworldindata.org/faqs#how-is-our-work-copyrighted — states that OWID data and
  charts are available under CC BY and may be used, reproduced, and distributed, including
  the production of derivative works, with attribution.
- **IMPORTANT caveat (third-party layers):** OWID's *own* compiled layer is CC BY 4.0, but
  **most underlying values originate from third parties** (e.g. WHO, UN, World Bank, IHME).
  Those source layers retain their providers' own licence terms, **which must be checked
  per indicator** before redistribution. Some IHME/GBD data, for example, is published under
  non-commercial / no-derivatives terms. The Grapher visualization *software* is **not**
  freely licensed for reuse without permission (out of scope here — software, not data).
- **Licence snapshot:** This datasheet records the licence name, the legal-code clause URL,
  and the FAQ citation URL above. A hash + archived copy of the licence text should be
  attached as the per-dataset gate artifact at review time (the CC BY 4.0 legal code is
  immutable and versioned by Creative Commons).

Licence status for this datasheet: **VERIFIED — permits derivatives (OWID-compiled layer).**
Reusers MUST still verify the specific source layer of any individual indicator.

---

## Data dictionary

Fields below describe the **standard OWID CSV download** structure for a chart/indicator,
verified from the OWID Chart/Data API documentation (https://docs.owid.io/projects/etl/api/).
Per-indicator value columns vary; the structural columns are consistent.

| Field | Type | Units | Description | Allowed values / nulls |
|-------|------|-------|-------------|------------------------|
| `Entity` | string | — | Name of the entity, typically a country or region (e.g. "United States"). | Free text country/region/aggregate names; non-null. |
| `Code` | string | — | OWID internal entity code; matches ISO alpha-3 for standard countries (e.g. "USA"); custom codes for historical/non-standard entities; may be blank for some aggregates. | ISO alpha-3 or custom code; may be empty/null for certain aggregates. |
| `Year` | integer | calendar year | Present when data is annual; the observation year. | e.g. 1950–present; non-null when used. |
| `Day` | string (date) | YYYY-MM-DD | Present instead of `Year` when data is daily; ISO date string. | ISO `YYYY-MM-DD`; used only for daily series. |
| `<indicator value column(s)>` | numeric (typically float/int); occasionally categorical | per-indicator (e.g. years, %, rate per 100,000, count) | One or more time-series value columns powering the chart; column name(s) describe the indicator and unit. | Numeric range per indicator; **missing observations omitted / left blank (null)** — *exact null encoding not explicitly documented; verify per file.* |

Notes:
- Either `Year` or `Day` is present (not both), depending on the series' temporal resolution.
- Units and allowed numeric ranges are indicator-specific and are carried in the
  accompanying `.metadata.json` (column metadata: units, timespan, data sources).
- **Unverified:** the precise null/missing-value encoding in the CSV (blank vs. omitted row)
  is not explicitly stated in the docs and must be confirmed against an actual sample at
  review time (bounded, header/streamed read, <=1000-row local-only ephemeral sample).

---

## Datasheet for Datasets

**Motivation.** OWID compiles, standardizes, and harmonizes health indicators from many
authoritative international sources into consistent, comparable, long-run time series so that
researchers, journalists, educators, and the public can study global health progress and
inequalities. Created/maintained by Our World in Data (Global Change Data Lab).

**Composition.** Instances are aggregate observations keyed by entity (country/region) and
time (year or day). Each indicator is a time series; there are no individual-person records.
The data is statistical/aggregate; **no PII**. Entities span countries, regions, income
groups, and global aggregates.

**Collection process.** OWID does not (in general) collect primary data; it ingests published
datasets from third parties (e.g. WHO, UN agencies, World Bank, IHME/GBD, national statistics
offices), then cleans, standardizes entity names/codes, and harmonizes units via its ETL
pipeline. Original collection methodology is defined by each upstream source.

**Preprocessing / cleaning / labeling.** Entity standardization to OWID codes (ISO alpha-3
where applicable), unit harmonization, interpolation/derived metrics in some series, and
metadata enrichment (units, sources, timespans). Transformations are documented per indicator
in metadata and in the public ETL repository.

**Uses.** Suitable for descriptive analysis, visualization, education, comparative and
longitudinal health research, and journalism. **Not** a substitute for primary clinical or
official statistics; users should consult upstream sources for authoritative/official figures
and check upstream caveats (definitions, coverage, revisions).

**Distribution.** Distributed by OWID via its website (per-indicator pages with CSV download),
the OWID Charts/Tables/Indicators APIs, and the `owid-catalog` Python library. OWID-compiled
layer under CC BY 4.0; third-party layers under their own terms. This datasheet does not
redistribute the data — only points to OWID's official distribution.

**Maintenance.** Maintained and regularly updated by the OWID data team; indicators are
refreshed as upstream sources release new data. Issues and contributions via OWID's public
GitHub repositories. Versioning is handled through the ETL catalog.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/"
  },
  "@type": "Dataset",
  "name": "Our World in Data — Health Datasets",
  "description": "OWID-compiled, standardized health indicator time series (e.g. life expectancy, mortality, disease burden, vaccination) keyed by entity and year/day. OWID-compiled layer licensed CC BY 4.0; underlying third-party source layers retain their own licences.",
  "url": "https://ourworldindata.org/",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Organization",
    "name": "Our World in Data (Global Change Data Lab)",
    "url": "https://ourworldindata.org/"
  },
  "datePublished": "2026-06-28",
  "version": "retrieved-2026-06-28",
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "owid-chart-csv",
      "name": "OWID chart/indicator CSV download",
      "description": "Standard OWID CSV export for an indicator/chart.",
      "encodingFormat": "text/csv",
      "contentUrl": "https://ourworldindata.org/"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "observations",
      "name": "observations",
      "field": [
        {
          "@type": "cr:Field",
          "@id": "observations/entity",
          "name": "Entity",
          "description": "Country/region/aggregate name.",
          "dataType": "sc:Text"
        },
        {
          "@type": "cr:Field",
          "@id": "observations/code",
          "name": "Code",
          "description": "OWID entity code; ISO alpha-3 for standard countries.",
          "dataType": "sc:Text"
        },
        {
          "@type": "cr:Field",
          "@id": "observations/year",
          "name": "Year",
          "description": "Observation year (annual series).",
          "dataType": "sc:Integer"
        },
        {
          "@type": "cr:Field",
          "@id": "observations/value",
          "name": "Value",
          "description": "Indicator value; units defined per indicator in metadata.json.",
          "dataType": "sc:Float"
        }
      ]
    }
  ]
}
```

---

## Validation script

Documentation only. The script below does **not** download, host, or transform the dataset.
It validates the *structure* of a locally-provided CSV sample (e.g. a bounded <=1000-row
sample a reviewer obtained ephemerally from OWID's official download) against the expected
OWID schema. It reads only from a local path supplied by the operator.

```python
#!/usr/bin/env python3
"""Validate the structure of a locally-supplied OWID health-indicator CSV sample.

Documentation/validation only: does NOT fetch, host, mirror, or transform any data.
Usage: python validate_owid.py /path/to/local_sample.csv
"""
import csv
import sys

# Standard OWID structural columns. Exactly one of Year/Day must be present,
# plus at least one indicator value column.
TEMPORAL = {"Year", "Day"}
REQUIRED_BASE = {"Entity"}  # 'Code' is usually present but may be blank for some aggregates

def validate(path: str) -> int:
    with open(path, newline="", encoding="utf-8") as fh:
        reader = csv.reader(fh)
        try:
            header = next(reader)
        except StopIteration:
            print("FAIL: empty file")
            return 1

        cols = set(header)
        problems = []

        missing_base = REQUIRED_BASE - cols
        if missing_base:
            problems.append(f"missing base column(s): {sorted(missing_base)}")

        temporal_present = TEMPORAL & cols
        if len(temporal_present) != 1:
            problems.append(f"expected exactly one of {sorted(TEMPORAL)}, found {sorted(temporal_present)}")

        structural = REQUIRED_BASE | {"Code"} | TEMPORAL
        value_cols = [c for c in header if c not in structural]
        if not value_cols:
            problems.append("no indicator value column(s) found")

        # Row-level checks (bounded sample; no transformation/storage)
        rows = 0
        ycol = next(iter(temporal_present), None)
        yidx = header.index(ycol) if ycol in header else None
        for row in reader:
            rows += 1
            if len(row) != len(header):
                problems.append(f"row {rows}: column count {len(row)} != header {len(header)}")
                break
            if ycol == "Year" and yidx is not None and row[yidx].strip():
                if not row[yidx].strip().lstrip("-").isdigit():
                    problems.append(f"row {rows}: Year '{row[yidx]}' is not an integer")
                    break

        if rows == 0:
            problems.append("no data rows")

        if problems:
            print("FAIL:")
            for p in problems:
                print("  -", p)
            return 1
        print(f"OK: {rows} data row(s); value column(s): {value_cols}")
        return 0

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("usage: python validate_owid.py /path/to/local_sample.csv")
        sys.exit(2)
    sys.exit(validate(sys.argv[1]))
```

Expected result on a valid OWID CSV: `Entity` present, exactly one of `Year`/`Day`, `Year`
values integer, and at least one indicator value column. Row count should match the indicator's
documented timespan x entity coverage (verify against `.metadata.json`).

---

## Limitations & gaps

- **Indicator-level coverage not enumerated.** OWID's health family contains hundreds of
  indicators; this datasheet documents the **common structure**, not every indicator's units,
  range, or value columns. Each indicator's `.metadata.json` is authoritative for units/sources.
- **Third-party licence layers unverified per-indicator.** Only the OWID-compiled CC BY 4.0
  layer was verified. Individual indicators may draw on upstream sources with stricter terms
  (e.g. some IHME/GBD data is non-commercial/no-derivatives). Verify per indicator before reuse.
- **Null/missing-value encoding unconfirmed.** The exact CSV representation of missing data
  (blank cell vs. omitted row) was not explicitly stated in the docs and should be confirmed
  against a bounded local sample.
- **No sample was downloaded** for this datasheet (documentation-only guardrail); structural
  claims derive from the OWID Charts/Data API documentation, not from inspecting a file.
- **Value-column data types** are indicator-specific (mostly numeric, occasionally categorical)
  and were generalized as float in the Croissant stub.
