# Datasheet: American Community Survey (ACS) Summary Tables

**One-line summary:** Documentation datasheet for the U.S. Census Bureau's American Community Survey (ACS) *summary tables* (aggregated estimates such as Data Profiles, Subject Tables, and Detailed Tables) — not the PUMS micro-data.

> This datasheet (the documentation in this file) is licensed **CC-BY-4.0**. It describes, but does not contain, host, mirror, or redistribute any ACS data.

---

## Provenance & attribution

| Field | Value |
|---|---|
| Publisher / source | U.S. Census Bureau — American Community Survey (ACS) |
| Source URL | https://www.census.gov/programs-surveys/acs/data.html |
| Data access portal | https://data.census.gov and the Census Data API (https://www.census.gov/data/developers/data-sets/acs-5year.html) |
| Catalog id (candidate) | cat-census-001 |
| Retrieval date | 2026-06-28 |
| Scope documented | ACS **summary tables** (aggregated estimates). The **PUMS** micro-data product is explicitly **out of scope**. |

**Required attribution string (suggested):**

> "Source: U.S. Census Bureau, American Community Survey. This product uses the Census Bureau Data API but is not endorsed or certified by the Census Bureau."

The second sentence is the verbatim attribution the Census Bureau requires of products that use its Data API (see Source licence below).

---

## Source licence

**Licence:** U.S. Government work — **public domain (no copyright)** under **17 U.S.C. § 105**. Works prepared by an officer or employee of the U.S. Government as part of their official duties are not subject to U.S. copyright protection. This permits **reuse and derivative works**.

**Citations confirming derivatives are permitted:**

- USA.gov, "Copyright and other rights pertaining to U.S. Government works" — references **Copyright Law of the United States, Sections 101 and 105**; federal works are in the public domain and may be reused, including derivative works. Retrieved 2026-06-28: https://www.usa.gov/government-copyright
- Census Bureau Data API **Terms of Service** (https://www.census.gov/data/developers/about/terms-of-service.html), retrieved 2026-06-28. The only integrity restriction relevant to derivatives is: *"You may not modify or falsely represent content accessed through the API and still claim the source is the Census Bureau."* This is a **standard misrepresentation/integrity clause** (you may modify the data; you simply may not present a modified version as if it were unmodified official Census data). It does **not** prohibit derivative works. The ToS also prohibits using the data to identify individuals (consistent with 13 U.S.C. §§ 8, 9).

**Verdict:** ✅ Licence permits derivatives. Public domain (17 U.S.C. § 105), with an attribution/integrity requirement when the Census Data API is used.

> Licence-snapshot note: a full hash + archived copy of the verbatim ToS/licence text should be attached as the per-dataset gate artifact at review time. This file records the licence name, the controlling statute, and dated citation URLs; the byte-for-byte archived copy + hash is produced by the gate, not committed here (documentation-only guardrail).

---

## Data dictionary

ACS summary tables are distributed as wide tables keyed by **geography**, where each substantive measure appears as an **estimate** column with a paired **margin of error** column. The structural/column-naming conventions below are standard across ACS summary tables (verified from the Census Data API documentation and data.census.gov table structure). **Per-table variable IDs are illustrative** (drawn from the well-known table B01001) and are marked as such; the exact variable set depends on the specific table requested.

| Field / column | Type | Units | Description | Allowed values / null handling |
|---|---|---|---|---|
| `GEO_ID` | string | — | Full geographic identifier (e.g., `0500000US06075` for a county). | Non-null key. |
| `NAME` | string | — | Human-readable geography name (e.g., "San Francisco County, California"). | Non-null. |
| `<TABLE>_<line>E` (e.g. `B01001_001E`) | integer/float | persons, housing units, dollars, etc. (varies by table) | **Estimate** for a table line item. Verified-convention; specific IDs illustrative. | May carry special annotation values (see below) instead of a count. |
| `<TABLE>_<line>M` (e.g. `B01001_001M`) | integer/float | same as paired estimate | **Margin of error** (90% confidence) for the paired estimate. | `-555555555` (or annotation) where an MOE cannot be computed. |
| `<TABLE>_<line>EA` | string | — | Estimate **annotation** flag. | Null when no annotation. |
| `<TABLE>_<line>MA` | string | — | Margin-of-error **annotation** flag. | Null when no annotation. |
| `for` / `in` (API query params) | string | — | Geography selectors used at request time (not stored columns). | API-only. |

**Special / sentinel values (verified Census convention):** ACS uses jam/sentinel values such as `-666666666` (estimate could not be computed), `-999999999` (estimate not available), `-888888888` (not applicable), and `*` / `**` annotations for statistical suppression or controlled-to-zero cells. Treat these as **nulls / missing**, never as numeric magnitudes.

> ⚠️ **Unverified rows:** the specific variable IDs (`B01001_*`) above are illustrative examples of the naming scheme, not a claim about which variables a given product contains. Confirm the exact variable list against the table's API `variables.json` (e.g., https://api.census.gov/data/2022/acs/acs5/variables.json) before relying on it. No row-level data was sampled to produce this file.

---

## Datasheet for Datasets

**Motivation.** The ACS is the premier source of detailed U.S. demographic, social, economic, and housing statistics, produced by the U.S. Census Bureau to inform the allocation of federal funding, redistricting, planning, and research. Summary tables provide ready-to-use **aggregated** estimates for public use.

**Composition.** Aggregated estimates (counts, percentages, medians, dollar amounts) organized as tables (Detailed Tables, Subject Tables, Data Profiles, Comparison Profiles) across geographies from the nation down to block groups. Each estimate is paired with a 90% margin of error. **No individual records** are present in summary tables (micro-data lives in the separately-published PUMS product, which is excluded here). Documented product is aggregate only — **contains no PII**.

**Collection process.** Continuous household survey conducted by the Census Bureau via mail, internet, telephone, and in-person interview, sampling addresses monthly and pooled into 1-year and 5-year period estimates. Responses are weighted and controlled to independent population estimates.

**Preprocessing / cleaning.** The Bureau performs editing, imputation, weighting, disclosure avoidance (suppression of small/unreliable cells), and computes margins of error before publication. Summary tables are the post-processed, statistically protected product.

**Uses.** Funding allocation, policy and program planning, academic and journalistic research, equity analysis, and as denominators/contextual layers in other datasets. **Appropriate use** requires honoring margins of error and not attempting re-identification. **Inappropriate use:** treating sentinel values as real numbers; using the data to identify individuals (prohibited by 13 U.S.C. §§ 8, 9 and the API ToS).

**Distribution.** Freely available via data.census.gov, the Census Data API, FTP summary files, and bulk downloads. Public domain (17 U.S.C. § 105). No fee, no registration for table access (an API key is recommended for high-volume API use).

**Maintenance.** Maintained by the U.S. Census Bureau; new ACS vintages are released annually (1-year and 5-year). Older vintages remain available. Contact and documentation via census.gov.

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
  "name": "American Community Survey (ACS) Summary Tables",
  "description": "Aggregated demographic, social, economic, and housing estimates from the U.S. Census Bureau's American Community Survey (summary tables: Detailed Tables, Subject Tables, Data Profiles, Comparison Profiles). Aggregate estimates only; excludes PUMS micro-data.",
  "url": "https://www.census.gov/programs-surveys/acs/data.html",
  "license": "https://www.usa.gov/government-copyright",
  "creator": {
    "@type": "GovernmentOrganization",
    "name": "U.S. Census Bureau",
    "url": "https://www.census.gov"
  },
  "datePublished": "2022",
  "isAccessibleForFree": true,
  "citation": "U.S. Census Bureau, American Community Survey. This product uses the Census Bureau Data API but is not endorsed or certified by the Census Bureau.",
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "acs-api",
      "name": "Census Data API (ACS 5-year)",
      "contentUrl": "https://api.census.gov/data/2022/acs/acs5",
      "encodingFormat": "application/json"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "acs_summary_table",
      "field": [
        { "@type": "cr:Field", "name": "GEO_ID", "dataType": "Text", "description": "Full geographic identifier." },
        { "@type": "cr:Field", "name": "NAME", "dataType": "Text", "description": "Human-readable geography name." },
        { "@type": "cr:Field", "name": "estimate", "dataType": "Integer", "description": "Estimate column, e.g. B01001_001E. Variable IDs vary by table." },
        { "@type": "cr:Field", "name": "margin_of_error", "dataType": "Integer", "description": "90% margin of error paired with each estimate, e.g. B01001_001M." }
      ]
    }
  ]
}
```

---

## Validation script

The script below validates the **structure** of an ACS summary-table extract that a user has *already* obtained themselves. It does **not** download, host, or redistribute any data — it only inspects a local file the user provides.

```python
#!/usr/bin/env python3
"""Structural validator for a locally-held ACS summary-table extract.
Documentation only: this script does NOT download, host, or transmit data.
Point it at a CSV/JSON file you already obtained from data.census.gov / the
Census API and it checks expected structure. No network calls are made.
"""
import csv
import re
import sys

SENTINELS = {"-666666666", "-999999999", "-888888888", "-555555555", "-222222222"}
EST_RE = re.compile(r"^[A-Z]+\d+_\d+E$")   # e.g. B01001_001E
MOE_RE = re.compile(r"^[A-Z]+\d+_\d+M$")   # e.g. B01001_001M

def validate(path: str) -> int:
    with open(path, newline="", encoding="utf-8") as fh:
        reader = csv.reader(fh)
        header = next(reader, None)
        if not header:
            print("FAIL: empty file"); return 1
        cols = set(header)
        problems = []
        if "GEO_ID" not in cols:
            problems.append("missing required column GEO_ID")
        if "NAME" not in cols:
            problems.append("missing required column NAME")
        est = [c for c in header if EST_RE.match(c)]
        moe = [c for c in header if MOE_RE.match(c)]
        if not est:
            problems.append("no estimate columns (expected *_E) found")
        # every estimate should have a paired margin of error
        for e in est:
            if e[:-1] + "M" not in cols:
                problems.append(f"estimate {e} has no paired *_M margin of error")
        rows = sum(1 for _ in reader)
        if rows < 1:
            problems.append("no data rows")
        print(f"columns={len(header)} estimates={len(est)} moe={len(moe)} rows={rows}")
        if problems:
            print("FAIL:"); [print("  -", p) for p in problems]; return 1
        print("OK: structure looks like an ACS summary table.")
        print("Reminder: treat sentinel values", sorted(SENTINELS), "as nulls.")
        return 0

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("usage: validate_acs.py <local_acs_extract.csv>"); sys.exit(2)
    sys.exit(validate(sys.argv[1]))
```

**Data-quality checks performed:** presence of `GEO_ID`/`NAME` keys, presence of estimate columns, each estimate paired with a margin-of-error column, non-zero row count, and a reminder to treat sentinel codes as nulls.

---

## Limitations & gaps

- **Field IDs not exhaustively verified.** The specific variable IDs (`B01001_*`) are illustrative of the Census naming convention; the exact variable set is table- and vintage-specific. Confirm against the relevant `variables.json` before relying on any specific field.
- **No data sampled.** Per the documentation-only guardrail, no rows were downloaded, sampled, or inspected; the data dictionary is derived from published Census conventions and documentation, not from a data sample.
- **Vintage-specific.** API endpoints/examples reference an ACS 5-year vintage for concreteness; replace the year for the vintage you need. Geographies, suppression rules, and available tables change between vintages.
- **Licence snapshot.** The verbatim licence/ToS text hash + archived copy is to be attached by the per-dataset gate; this file records the licence name, statute, and dated citation URLs but does not embed the archived copy (documentation-only).
- **Scope.** Only ACS **summary/aggregate** tables are documented. PUMS micro-data is intentionally excluded and would require a separate PII/disclosure assessment.
