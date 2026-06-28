# Datasheet: U.S. College Scorecard

**One-line summary:** Institution-level data on cost, enrollment, financial aid, and student
outcomes for U.S. postsecondary institutions, published by the U.S. Department of Education.

*This datasheet (the documentation in this file) is licensed under **CC-BY-4.0**. It is
documentation only: it does not host, mirror, transform, or republish any of the underlying
dataset.*

---

## Provenance & attribution

| Field | Value |
|---|---|
| **Publisher** | U.S. Department of Education — Office of Planning, Evaluation and Policy Development (OPEPD) |
| **Dataset name** | College Scorecard |
| **Source / landing URL** | https://collegescorecard.ed.gov/data/ |
| **Documentation URL** | https://collegescorecard.ed.gov/data/data-documentation/ |
| **Catalog (data.gov)** | https://catalog.data.gov/dataset/college-scorecard |
| **Catalog id (internal)** | cat-edu-001 |
| **Retrieval date** | 2026-06-28 |
| **Source last updated** | 2026-06-10 (per landing page) |
| **Contact** | odp@ed.gov |

**Required attribution string:**

> Source: U.S. Department of Education, College Scorecard (https://collegescorecard.ed.gov/data/),
> retrieved 2026-06-28. Licensed under Creative Commons Attribution (CC-BY).

---

## Source licence

**Verified licence: Creative Commons Attribution (CC-BY).**

- The data.gov catalog entry for this dataset records the licence as
  `http://www.opendefinition.org/licenses/cc-by` — "Creative Commons Attribution"
  (verified at https://catalog.data.gov/dataset/college-scorecard, retrieved 2026-06-28).
- CC-BY explicitly permits the creation and distribution of **derivative works** provided
  attribution is given (see the CC-BY deed,
  https://creativecommons.org/licenses/by/4.0/ — "You are free to ... Adapt — remix, transform,
  and build upon the material for any purpose, even commercially").
- Additionally, as a work of the U.S. federal government, the underlying data is generally a
  **U.S. Government Work** in the public domain in the United States
  (17 U.S.C. § 105), which independently permits reuse and derivatives.

**Conclusion:** Derivatives are permitted. Attribution is the only material obligation.
Licence verification: **PASS**.

> Note: The College Scorecard landing and documentation pages do not themselves print explicit
> licence text; the authoritative licence record is the federal data.gov catalog entry cited
> above. A licence snapshot (hash + archived copy of the catalog licence statement) should be
> captured as the per-dataset gate artifact at ingest time; this datasheet records the verified
> licence name and citation but does not embed the archived copy.

---

## Data dictionary

The College Scorecard institution-level file is wide (1,000+ columns across cohorts). The
authoritative, field-by-field dictionary is the publisher's spreadsheet
`CollegeScorecardDataDictionary.xlsx`
(https://collegescorecard.ed.gov/files/CollegeScorecardDataDictionary.xlsx) and the
`InstitutionDataDocumentation.pdf`. The table below documents core, high-use fields.

**Verification key:**
- **[confirmed-api]** — field/path confirmed directly from the fetched API documentation
  (https://collegescorecard.ed.gov/data/api-documentation/, 2026-06-28).
- **[dict]** — raw CSV column name from the official Data Dictionary spreadsheet (referenced,
  not re-parsed cell-by-cell in this pass); name and meaning are standard but the specific
  row was not individually re-verified here.

| Field (raw CSV) | API path | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|---|
| `UNITID` [dict] | `id` | integer | — | IPEDS unit ID (primary institution key) | positive integer; not null |
| `OPEID` [dict] | `ope8_id` | string | — | 8-digit Office of Postsecondary Education ID | zero-padded string |
| `OPEID6` [dict] | `ope6_id` | string | — | 6-digit OPE ID | zero-padded string |
| `INSTNM` [dict] | `school.name` [confirmed-api] | string | — | Institution name | non-null |
| `CITY` [dict] | `school.city` [confirmed-api] | string | — | City | non-null |
| `STABBR` [dict] | `school.state` [confirmed-api] | string | — | State/territory postal abbreviation | 2-letter code |
| `ZIP` [dict] | `school.zip` | string | — | ZIP code | 5- or 9-digit |
| `CONTROL` [dict] | `school.ownership` | integer (categorical) | — | Governance/control | 1=Public, 2=Private nonprofit, 3=Private for-profit |
| `UGDS` [dict] | `latest.student.size` [confirmed-api] | integer | students | Undergraduate enrollment (degree-seeking) | >=0; may be null |
| `ADM_RATE` [dict] | `latest.admissions.admission_rate.overall` [confirmed-api] | float | proportion (0-1) | Overall admission rate | 0.0-1.0; null/suppressed for non-selective or small n |
| `SAT_AVG` [dict] | `latest.admissions.sat_scores.average.overall` | integer | SAT points | Average SAT equivalent of admitted students | typ. 400-1600; nullable |
| `COSTT4_A` [dict] | `latest.cost.attendance.academic_year` | integer | USD/year | Average annual total cost of attendance (academic-year institutions) | >=0; nullable |
| `TUITIONFEE_IN` [dict] | `latest.cost.tuition.in_state` [confirmed-api] | integer | USD/year | In-state tuition and fees | >=0; nullable |
| `TUITIONFEE_OUT` [dict] | `latest.cost.tuition.out_of_state` | integer | USD/year | Out-of-state tuition and fees | >=0; nullable |
| `C150_4` [dict] | `latest.completion.rate` [confirmed-api, related] | float | proportion (0-1) | Completion rate, first-time full-time, 150% of normal time (4-yr) | 0.0-1.0; nullable |
| `MD_EARN_WNE_P10` [dict] | `latest.earnings...` | integer | USD/year | Median earnings of students working & not enrolled, 10 years after entry | >=0; null or `PrivacySuppressed` |

**Null / suppression handling:** Missing values appear as empty/`NULL`. Cells derived from
small populations are released as the literal string **`PrivacySuppressed`** to protect
individual privacy — these must be treated as nulls, not numbers, in any analysis.

---

## Datasheet for Datasets

**Motivation.** Created by the U.S. Department of Education to give students, families, and
researchers transparent, comparable information on the cost and outcomes of postsecondary
institutions (enrollment, price, financial aid, completion, debt, and post-enrollment
earnings), supporting informed college choice and public accountability.

**Composition.** Each institution-level row represents one postsecondary institution (keyed by
`UNITID`/`OPEID`) for a given data release/cohort. Instances are **institutions and aggregate
statistics about their student bodies**, not individual people. Field-of-study files add
program-level rows (debt and earnings by credential and CIP code). Crosswalk files link
`OPEID` to IPEDS `UNITID`. Coverage spans 1996-97 through 2025-26 (institution level).

**Collection process.** Compiled by the Department from administrative sources, primarily IPEDS
(institutional reporting), Federal Student Aid (Title IV aid/loan records), and matched
tax/earnings data via federal administrative records. Data are released as periodic cohort
files.

**Preprocessing / cleaning / labeling.** The Department aggregates underlying records to the
institution (and program) level, derives rates and medians, and applies **privacy
suppression** (`PrivacySuppressed`) to small cells. The published files are already aggregated;
no raw individual records are distributed.

**Uses.** College search/comparison tools, education-policy and economics research,
accountability reporting, journalism. Documentation-only reuse (like this datasheet) and
analytical derivatives are permitted under CC-BY. *Not* suitable for re-identifying individuals
(it is aggregate by design) or for high-stakes individual advice without expert review.

**Distribution.** Publicly distributed by the U.S. Department of Education via
collegescorecard.ed.gov and cataloged on data.gov; downloadable as ZIP/CSV and via a public
API. Licensed CC-BY (plus U.S. Government Work). **This datasheet does not redistribute the
data** — consult the official source for the files.

**Maintenance.** Maintained by the U.S. Department of Education (OPEPD); contact `odp@ed.gov`.
Updated on a recurring cadence (most recent source update 2026-06-10); a public change log is
published at https://collegescorecard.ed.gov/data/changelog/.

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
  "name": "College Scorecard",
  "description": "Institution-level data on cost, enrollment, financial aid, and student outcomes for U.S. postsecondary institutions, published by the U.S. Department of Education.",
  "url": "https://collegescorecard.ed.gov/data/",
  "sameAs": "https://catalog.data.gov/dataset/college-scorecard",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "GovernmentOrganization",
    "name": "U.S. Department of Education, Office of Planning, Evaluation and Policy Development",
    "url": "https://www.ed.gov/"
  },
  "datePublished": "2026-06-10",
  "version": "most-recent-cohorts-institution",
  "keywords": ["education", "higher education", "college", "earnings", "tuition", "public-data"],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "institution-level",
      "description": "One record per postsecondary institution per cohort.",
      "field": [
        { "@type": "cr:Field", "name": "UNITID", "description": "IPEDS unit ID (primary key)", "dataType": "sc:Integer" },
        { "@type": "cr:Field", "name": "INSTNM", "description": "Institution name", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "STABBR", "description": "State postal abbreviation", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "CONTROL", "description": "Ownership: 1=Public, 2=Private nonprofit, 3=Private for-profit", "dataType": "sc:Integer" },
        { "@type": "cr:Field", "name": "TUITIONFEE_IN", "description": "In-state tuition and fees (USD/year)", "dataType": "sc:Integer" },
        { "@type": "cr:Field", "name": "MD_EARN_WNE_P10", "description": "Median earnings 10 years after entry (USD/year); may be PrivacySuppressed", "dataType": "sc:Text" }
      ]
    }
  ]
}
```

---

## Validation script

This script validates the **structure** of a locally obtained College Scorecard institution CSV.
It does **not** download, host, or republish the data — point it at a file you have already
obtained from the official source. It reads only the header and a bounded sample.

```python
#!/usr/bin/env python3
"""Validate the structure of a College Scorecard institution-level CSV.

Documentation-only: this script does NOT download or host data. Provide a path
to a file you obtained yourself from https://collegescorecard.ed.gov/data/.

Usage:
    python validate_scorecard.py path/to/Most-Recent-Cohorts-Institution.csv
"""
import csv
import sys

# Core columns expected in the institution-level file (subset; the full file is wider).
EXPECTED = ["UNITID", "OPEID", "INSTNM", "CITY", "STABBR", "CONTROL",
            "TUITIONFEE_IN", "TUITIONFEE_OUT"]
SAMPLE_LIMIT = 1000  # bounded read; never load the whole file for validation


def main(path: str) -> int:
    with open(path, newline="", encoding="utf-8") as fh:
        reader = csv.DictReader(fh)
        header = reader.fieldnames or []
        missing = [c for c in EXPECTED if c not in header]
        if missing:
            print(f"FAIL: missing expected columns: {missing}")
            return 1
        rows = suppressed = 0
        for row in reader:
            rows += 1
            if any(v == "PrivacySuppressed" for v in row.values()):
                suppressed += 1
            if rows >= SAMPLE_LIMIT:
                break
        print(f"OK: header has {len(header)} columns; all {len(EXPECTED)} core columns present.")
        print(f"Sampled {rows} rows (<= {SAMPLE_LIMIT}); {suppressed} contained PrivacySuppressed cells.")
        if rows == 0:
            print("WARN: no data rows found in sample.")
            return 1
    return 0


if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__)
        sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

---

## Limitations & gaps

- **Field coverage:** Only core, high-use fields are tabulated above. The full file contains
  1,000+ columns; the authoritative per-field reference is the publisher's
  `CollegeScorecardDataDictionary.xlsx`. Rows marked **[dict]** were taken from the official
  data dictionary by name/meaning but were **not** re-parsed cell-by-cell in this pass; rows
  marked **[confirmed-api]** were verified directly against the live API documentation.
- **Licence text not embedded:** The landing/documentation pages do not print licence text;
  the CC-BY licence was verified via the data.gov catalog entry. A hashed, archived snapshot of
  that licence statement (the gate artifact) was **not** produced in this documentation pass and
  should be captured at ingest.
- **No data inspected:** Per guardrails, no actual data file was downloaded, sampled, or
  hosted. Row counts, exact null rates, and value ranges were therefore **not** empirically
  measured; the validation script is provided for the maintainer to run locally.
- **Types/units** for `[dict]` fields reflect documented conventions and may vary by cohort
  year; confirm against the dictionary for a specific release.
- **No PII:** The dataset is institution-level aggregate by design, with small-cell
  `PrivacySuppressed` redaction; no personal/identifying fields are documented here.
