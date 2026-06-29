# Datasheet: UK Energy Statistics (DUKES — Digest of UK Energy Statistics)

> One-line summary: A documentation datasheet for the UK's national energy balances and
> commodity statistics (coal, petroleum, natural gas, electricity, renewables, CHP) published
> by DESNZ, covering production and use over the last 5 years with key series back to 1970.

**This datasheet's own licence:** Creative Commons Attribution 4.0 International (CC-BY-4.0).
The datasheet documents — but does not contain, mirror, or republish — any of the underlying
DUKES data.

---

## Provenance & attribution

| Field | Value |
|---|---|
| **Dataset title** | Digest of UK Energy Statistics (DUKES) |
| **Publisher** | Department for Energy Security and Net Zero (DESNZ); historically the Department for Business, Energy & Industrial Strategy (BEIS) |
| **Distribution channel** | GOV.UK collection page (referenced from data.gov.uk catalogue) |
| **Source URL** | https://www.gov.uk/government/collections/digest-of-uk-energy-statistics-dukes |
| **Catalogue id (candidate)** | cat-energy-004 |
| **Retrieval date** | 2026-06-28 |

**Required attribution string** (per OGL v3.0; provider attribution + licence link):

> Contains public sector information from the Department for Energy Security and Net Zero (DUKES,
> Digest of UK Energy Statistics) licensed under the Open Government Licence v3.0
> (https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/).

---

## Source licence

**Licence:** Open Government Licence for public sector information, version 3.0 (OGL v3.0).

**Confirmed to permit derivatives — citation:**
The GOV.UK collection page states: *"All content is available under the Open Government Licence
v3.0, except where otherwise stated."* The OGL v3.0 text itself
(https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/), under **"You are
free to"**, explicitly grants the right to:

- *"copy, publish, distribute and transmit the Information"*
- *"adapt the Information"*  ← derivatives/adaptation expressly permitted
- *"exploit the Information commercially and non-commercially for example, by combining it with
  other Information, or by including it in your own product or application"*

The licence's only material condition (under **"You must (where you do any of the above)"**) is
attribution: *"acknowledge the source of the Information in your product or application by
including or linking to any attribution statement specified by the Information Provider(s) and,
where possible, provide a link to this licence."*

Conclusion: derivatives are permitted, subject to attribution. **licenseVerified = true.**

> Licence snapshot note: this datasheet records the licence name, version, the canonical licence
> URL, and the verbatim clauses above as the archived licence evidence. A binary hash of the
> archived licence text is not embedded here to avoid committing third-party text into the repo;
> reviewers can reproduce it from the cited URL.

---

## Data dictionary

DUKES is published as a large set of Excel/ODS tables and a long-form PDF/commentary rather than
a single flat CSV with a fixed schema. The GOV.UK collection page does **not** publish a
machine-readable column-level schema, so the per-column field list below is documented at the
**conceptual/dimensional level** verified from the published chapter structure, and individual
column names are marked **UNVERIFIED** because they vary table-by-table and were not confirmed
against a downloaded file (documentation-only, no bounded-access sample was taken in this pass).

| Field (conceptual) | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| Year | integer | calendar year | Reference period for the observation | 1970–latest; key long series back to 1970 (VERIFIED from page: "last 5 years, with key series taken back to 1970") |
| Energy commodity / chapter | categorical | n/a | Top-level commodity grouping | VERIFIED set: Solid fuels and derived gases; Petroleum; Natural gas; Electricity; Renewable sources of energy; Combined heat and power |
| Flow / balance line | categorical | n/a | Energy-balance row (e.g. production, imports, exports, transformation, final consumption) | UNVERIFIED — exact category labels not confirmed from a table file |
| Sector / end-use | categorical | n/a | Consuming sector (e.g. industry, transport, domestic, services) | UNVERIFIED — taxonomy varies by table |
| Quantity (energy) | numeric (float) | Commonly ktoe / Mtoe (thousand/million tonnes of oil equivalent) for balances; GWh/TWh for electricity; therms/GWh for gas | The measured value | UNVERIFIED per-column; units differ per table — confirm in each table header/footnotes |
| Quantity (physical) | numeric (float) | e.g. thousand tonnes (solid/petroleum), million cubic metres (gas) | Physical-unit measure where applicable | UNVERIFIED per-column |
| Footnote / flag | string | n/a | Provisional/revised/estimate markers common in ONS/DESNZ tables | UNVERIFIED; nulls/blank cells typical for not-applicable cells |

> To produce a fully VERIFIED column-level dictionary, a follow-up bounded-access pass (header +
> <=1000-row streamed sample, local-only, ephemeral) on a specific DUKES table file is required.
> No such sample was taken here, so per-column rows are conservatively marked UNVERIFIED.

---

## Datasheet for Datasets

**Motivation.** DUKES provides the authoritative national picture of UK energy production,
transformation and consumption. Reusers frequently struggle with unit conventions (e.g. ktoe vs
GWh) and category definitions across chapters; this datasheet aims to make provenance, licensing,
and structure legible.

**Composition.** Aggregate national statistics (not individual records). Instances are
time-series observations indexed by year, commodity/chapter, balance line, and where applicable
sector. Covers solid fuels & derived gases, petroleum, natural gas, electricity, renewables, and
combined heat and power. No personal or identifying data — these are macro energy balances.

**Collection process.** Compiled by DESNZ from returns, surveys, and administrative/industry
sources across the UK energy sector and harmonised into national energy balances. Exact
collection instruments are documented in DUKES methodology/"Table of tables" guidance referenced
from the collection page (not enumerated here).

**Preprocessing / cleaning.** Source data are aggregated, converted to common energy units
(tonnes of oil equivalent and electricity units), and presented with provisional/revised flags.
Specific transformation rules are in the per-chapter methodology notes.

**Uses.** Energy policy analysis, decarbonisation/net-zero tracking, academic research, and
derivative datasets/dashboards. OGL v3.0 permits commercial and non-commercial reuse with
attribution.

**Distribution.** Published openly on GOV.UK as downloadable Excel/ODS tables plus PDF
commentary; discoverable via data.gov.uk. This datasheet does not redistribute the data.

**Maintenance.** Updated by DESNZ on an annual cycle (with periodic revisions). Authoritative,
current versions should always be retrieved from the source URL above.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/"
  },
  "@type": "Dataset",
  "name": "Digest of UK Energy Statistics (DUKES)",
  "description": "UK national energy statistics and balances covering solid fuels, petroleum, natural gas, electricity, renewables and combined heat and power; last 5 years with key series back to 1970. Published by DESNZ.",
  "url": "https://www.gov.uk/government/collections/digest-of-uk-energy-statistics-dukes",
  "license": "https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/",
  "creator": {
    "@type": "GovernmentOrganization",
    "name": "Department for Energy Security and Net Zero",
    "url": "https://www.gov.uk/government/organisations/department-for-energy-security-and-net-zero"
  },
  "datePublished": "2026",
  "isAccessibleForFree": true,
  "keywords": ["energy", "United Kingdom", "energy balance", "DUKES", "renewables", "electricity", "natural gas", "petroleum"],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "energy_balance_observations",
      "description": "Conceptual schema (column names UNVERIFIED — vary per table).",
      "field": [
        { "@type": "cr:Field", "name": "year", "dataType": "Integer", "description": "Calendar year (1970–latest)." },
        { "@type": "cr:Field", "name": "commodity", "dataType": "Text", "description": "Energy commodity / chapter." },
        { "@type": "cr:Field", "name": "flow", "dataType": "Text", "description": "Energy-balance line (UNVERIFIED)." },
        { "@type": "cr:Field", "name": "value", "dataType": "Float", "description": "Quantity; units vary (ktoe/GWh) per table." }
      ]
    }
  ]
}
```

---

## Validation script

The script below documents how a reviewer would validate the structure of a single DUKES table
**after they themselves obtain it from the source**. It does **not** download, host, or embed any
data — it operates on a local file path the user supplies.

```python
#!/usr/bin/env python3
"""Validate the structure of a locally-obtained DUKES table (documentation only).

This script NEVER downloads, hosts, or republishes DUKES data. The user must
provide a path to a file they retrieved from the official source URL.
"""
import sys

EXPECTED_MIN_COLUMNS = 3          # at least: year + a category + a value column
EXPECTED_MIN_ROWS = 1
# 'year' is the one column concept we VERIFIED is present across DUKES series.
EXPECTED_CONCEPTS = {"year"}      # case-insensitive substring match against headers

def validate(path: str) -> int:
    try:
        import pandas as pd
    except ImportError:
        print("Install pandas+openpyxl to run this check: pip install pandas openpyxl")
        return 2
    # Read header + a bounded sample only (bounded-access protocol; <=1000 rows).
    df = pd.read_excel(path, nrows=1000) if path.lower().endswith((".xls", ".xlsx", ".ods")) \
        else pd.read_csv(path, nrows=1000)
    headers = [str(c).lower() for c in df.columns]
    ok = True
    if len(df.columns) < EXPECTED_MIN_COLUMNS:
        print(f"FAIL: expected >= {EXPECTED_MIN_COLUMNS} columns, got {len(df.columns)}"); ok = False
    if len(df) < EXPECTED_MIN_ROWS:
        print(f"FAIL: expected >= {EXPECTED_MIN_ROWS} rows, got {len(df)}"); ok = False
    for concept in EXPECTED_CONCEPTS:
        if not any(concept in h for h in headers):
            print(f"WARN: no header matched expected concept '{concept}' (DUKES headers vary).")
    print(f"Checked {len(df)} sampled rows, {len(df.columns)} columns.")
    print("PASS" if ok else "FAIL")
    return 0 if ok else 1

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python validate_dukes.py <path-to-local-DUKES-table>"); sys.exit(2)
    sys.exit(validate(sys.argv[1]))
```

---

## Limitations & gaps

- **Column-level schema is UNVERIFIED.** DUKES is distributed as many heterogeneous Excel/ODS
  tables without a single published machine-readable column schema. No bounded-access data sample
  was taken in this documentation-only pass, so per-column names, exact units per column, and the
  full set of balance-line/sector category labels are marked UNVERIFIED.
- **Units vary per table** (ktoe/Mtoe for balances; GWh/TWh for electricity; physical units such
  as thousand tonnes or million cubic metres elsewhere). Always read each table's header and
  footnotes for the authoritative unit.
- **Verified items:** licence (OGL v3.0, derivatives permitted, with cited clause), publisher
  (DESNZ), top-level chapter/commodity set, and the temporal coverage statement ("last 5 years,
  key series back to 1970").
- **No PII:** DUKES contains aggregate national statistics only; no personal/identifying fields
  were documented or sampled.
- **Licence snapshot hash** was intentionally not embedded to avoid committing third-party
  licence text into the repository; the citation URL is provided for reproducibility.
- This datasheet reflects the source as retrieved on 2026-06-28; consult the source URL for the
  current authoritative release and methodology notes.
