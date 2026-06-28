# Datasheet — NHS England Published Statistics

One-line summary: A documentation datasheet for the NHS England official statistics
collection — a portal of 200+ aggregated health- and care-service statistical series
published under the Open Government Licence v3.0.

> This datasheet (the document you are reading) is licensed under **CC-BY-4.0**.
> It is documentation only: it does **not** host, mirror, transform, or republish any
> NHS England data.

---

## Scope note

The cited source (`https://www.england.nhs.uk/statistics/`) is a **collection / portal**,
not a single tabular dataset. It indexes 200+ distinct statistical series (e.g. A&E
waiting times, Referral to Treatment, cancer waiting times, diagnostics, vaccinations),
each with its own files, columns, and definitions. This datasheet documents the
collection at portal level and anchors concrete structure to one representative,
verified series (**A&E Attendances and Emergency Admissions**). Field-level details that
vary by series, or that require opening a specific data file, are marked **UNVERIFIED**.

---

## Provenance & attribution

| Item | Value |
|---|---|
| Publisher / source | NHS England |
| Source URL | https://www.england.nhs.uk/statistics/ |
| Series index | https://www.england.nhs.uk/statistics/statistical-work-areas/ |
| Representative series | https://www.england.nhs.uk/statistics/statistical-work-areas/ae-waiting-times-and-activity/ |
| Retrieval date | 2026-06-28 |
| Catalog id | cat-health-003 |

**Required attribution string** (per OGL v3.0, source-specified form preferred):

> Contains public sector information published by NHS England and licensed under the
> Open Government Licence v3.0. Source: NHS England Statistics
> (https://www.england.nhs.uk/statistics/), retrieved 2026-06-28.

---

## Source licence

- **Licence:** Open Government Licence for public sector information **version 3.0 (OGL v3.0)**.
- **Citation / clause confirming derivatives are permitted:**
  https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/
  Under "You are free to: ... **adapt the Information**" and "**exploit the Information
  commercially and non-commercially**, for example, by combining it with other
  Information, or by including it in your own product or application."
- **Verdict:** OGL v3.0 explicitly permits adaptation and derivative works (with
  attribution). **Derivatives are permitted — licence VERIFIED.**
- Confirmed on the source: the `england.nhs.uk` footer links to OGL v3.0 as the licence
  governing site content (verified 2026-06-28).

### Licence snapshot

A point-in-time snapshot of the licence text should be archived alongside the per-dataset
gate artifact. To produce a hash of the licence text locally (documentation only — does
not redistribute the licence within this repo):

```bash
# Fetch licence text to a LOCAL, ephemeral file and hash it; do not commit the text.
curl -sL https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/ \
  -o /tmp/ogl-v3.html
sha256sum /tmp/ogl-v3.html   # record this digest in the gate artifact
rm -f /tmp/ogl-v3.html
```

---

## Data dictionary

The collection has no single global schema. The fields below are **verified from the
published series documentation** (metric/dimension level). Exact CSV/Excel column header
strings vary by series and release and are **UNVERIFIED** here because, per guardrails, no
data file was downloaded; consult each series' "definitions" document for canonical names.

Representative series: **A&E Attendances and Emergency Admissions** (monthly, Excel
`.xls`/`.xlsx`; provider-level aggregates).

| Field (logical) | Type | Units | Description | Allowed values / nulls | Status |
|---|---|---|---|---|---|
| Reporting period | string/date | month | Calendar month the figures cover | YYYY-MM; not null | Verified (monthly publication) |
| Organisation code | string | — | NHS provider (Trust / FT / ISO) identifier | ODS org code; not null | UNVERIFIED column name |
| Organisation name | string | — | Provider name | text; not null | UNVERIFIED column name |
| A&E attendances (Type 1) | integer | count | Major / consultant-led A&E attendances | >=0; may be blank if not applicable | Verified (metric) |
| A&E attendances (Type 2) | integer | count | Single-specialty A&E attendances | >=0; nullable | Verified (metric) |
| A&E attendances (Type 3) | integer | count | Other A&E / UTC / MIU / Walk-in attendances | >=0; nullable | Verified (metric) |
| Total attendances | integer | count | Sum across A&E types | >=0; not null | Verified (metric) |
| Attendances > 4 hours | integer | count | Attendances breaching the 4-hour standard | >=0; nullable | Verified (metric) |
| Emergency admissions | integer | count | Emergency admissions via A&E | >=0; nullable | Verified (metric) |
| Waits > 4h from decision to admit | integer | count | Trolley waits after admission decision | >=0; nullable | Verified (metric) |
| 12-hour performance | integer | count | ECDS-based 12-hour metric (from Apr 2023) | >=0; nullable | Verified (metric) |
| Demographic breakdowns (age, gender, ethnic category) | integer | count | **Aggregated counts only** in ECDS supplementary outputs | >=0; nullable | Verified (aggregated; no row-level PII) |

Note on PII: these are **aggregated, provider-level counts**. Demographic dimensions
(age band, gender, ethnic category) appear only as aggregate breakdowns, not as
individual records. No personal/identifying fields are documented or sampled.

---

## Datasheet for Datasets

**Motivation.** Published by NHS England to provide transparent, official statistics on
the performance and activity of health and care services in England, supporting
accountability, planning, research, and public information.

**Composition.** A collection of 200+ statistical series. Instances are typically
**aggregated counts/rates** at provider, ICB, regional, or national level, by reporting
period. No individual patient records; demographic detail is aggregated. Representative
series (A&E) covers NHS Trusts, Foundation Trusts, and Independent Sector Organisations.

**Collection process.** Data are returned by NHS organisations through standard NHS
data collections (e.g. ECDS for emergency care from April 2023) and compiled/validated
by NHS England analytical teams. A&E figures are published monthly (2nd Thursday),
covering the prior month, with time series back to 2011-12.

**Preprocessing / cleaning.** NHS England applies validation, aggregation, and (where
relevant) statistical disclosure control to aggregate outputs. Definitions and revisions
are documented per series in accompanying "definitions" and methodology notes.

**Uses.** Performance monitoring, capacity/demand planning, academic and policy research,
journalism, and public transparency. Suitable for derivative analyses under OGL v3.0 with
attribution. Not suitable for re-identification (and the data is not designed to allow it).

**Distribution.** Publicly downloadable from england.nhs.uk (and data.england.nhs.uk for
some acute provider statistics), primarily as Excel files, under OGL v3.0. This datasheet
does not redistribute the data.

**Maintenance.** Maintained by NHS England; series are updated on published schedules
(monthly/quarterly/annual depending on series). Revisions and discontinuations are
announced on the respective series pages.

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
  "name": "NHS England Published Statistics",
  "description": "Collection of 200+ aggregated health and care service statistical series published by NHS England under the Open Government Licence v3.0. Documentation-only datasheet; data is not hosted here.",
  "url": "https://www.england.nhs.uk/statistics/",
  "license": "https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/",
  "creator": {
    "@type": "sc:Organization",
    "name": "NHS England",
    "url": "https://www.england.nhs.uk/"
  },
  "datePublished": "2026-06-28",
  "version": "portal-snapshot-2026-06-28",
  "keywords": ["public health", "NHS", "England", "official statistics", "open data", "OGL"],
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "ae-attendances-monthly",
      "name": "A&E Attendances and Emergency Admissions (representative series)",
      "encodingFormat": "application/vnd.ms-excel",
      "contentUrl": "https://www.england.nhs.uk/statistics/statistical-work-areas/ae-waiting-times-and-activity/"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "ae-records",
      "name": "A&E provider-month aggregates",
      "field": [
        {"@type": "cr:Field", "@id": "ae-records/period", "name": "reporting_period", "dataType": "sc:Text", "description": "Reporting month (YYYY-MM)"},
        {"@type": "cr:Field", "@id": "ae-records/org_code", "name": "organisation_code", "dataType": "sc:Text", "description": "ODS provider code (column name unverified)"},
        {"@type": "cr:Field", "@id": "ae-records/total_att", "name": "total_attendances", "dataType": "sc:Integer", "description": "Total A&E attendances (all types)"},
        {"@type": "cr:Field", "@id": "ae-records/over_4h", "name": "attendances_over_4h", "dataType": "sc:Integer", "description": "Attendances breaching 4-hour standard"},
        {"@type": "cr:Field", "@id": "ae-records/emerg_adm", "name": "emergency_admissions", "dataType": "sc:Integer", "description": "Emergency admissions via A&E"}
      ]
    }
  ]
}
```

---

## Validation script

Documentation only: this script validates the **structure** of a locally-held A&E series
file that the user has already obtained from NHS England. It does **not** download, host,
or redistribute any data.

```python
#!/usr/bin/env python3
"""Validate the structure of a locally-held NHS England A&E series file.

Usage: python validate_ae.py path/to/ae_series.csv
Does NOT fetch, host, or redistribute data. Expected logical columns are matched
case-insensitively and by substring because exact header strings vary by release.
"""
import sys, csv

# Logical metrics expected (substrings); exact headers vary by release/series.
EXPECTED = [
    "period",          # reporting period
    "org",             # organisation code/name
    "total",           # total attendances
    "4",               # 4-hour related metric
    "admission",       # emergency admissions
]
MIN_ROWS = 1  # at least one provider-period row

def main(path: str) -> int:
    with open(path, newline="", encoding="utf-8-sig") as f:
        reader = csv.reader(f)
        try:
            header = [h.strip().lower() for h in next(reader)]
        except StopIteration:
            print("FAIL: file is empty"); return 1
        missing = [tok for tok in EXPECTED
                   if not any(tok in col for col in header)]
        rows = sum(1 for _ in reader)
    ok = not missing and rows >= MIN_ROWS
    print(f"columns_found={len(header)} data_rows={rows}")
    if missing:
        print(f"WARN: no column matched these logical tokens: {missing}")
    print("PASS" if ok else "FAIL")
    return 0 if ok else 1

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("usage: python validate_ae.py path/to/ae_series.csv"); sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

---

## Limitations & gaps

- **Portal, not one dataset:** exact schemas differ across the 200+ series. Only the A&E
  series structure was inspected, at metric level, from its documentation page.
- **No data file opened:** per guardrails, no dataset file was downloaded. Exact CSV/Excel
  **column header strings, data types, units, and null conventions are UNVERIFIED** and
  should be confirmed against each series' official "definitions" document.
- **Row counts / quality metrics not measured:** the validation script is provided for the
  user to run against their own local copy; no data-quality report was generated here
  because the data was deliberately not accessed.
- **Licence form:** OGL v3.0 derivatives permission is verified from the National Archives
  canonical text and the england.nhs.uk footer link; if a specific series page specifies a
  bespoke attribution string, that series-specific form takes precedence.
- **Croissant record stubs** for fields are illustrative for the A&E series and reuse the
  unverified column-name caveat above.
