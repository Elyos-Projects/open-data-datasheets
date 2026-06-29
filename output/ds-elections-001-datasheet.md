# Datasheet: US Election Returns (precinct / county / state)

> One-line summary: Cleaned, citable U.S. election returns published by the MIT Election Data
> and Science Lab (MEDSL), documented here as a standalone, reusable datasheet.

**This datasheet's own licence:** CC-BY-4.0. (It documents, but does not contain or
redistribute, the underlying data.)

---

## Provenance & attribution

- **Publisher / creator:** MIT Election Data and Science Lab (MEDSL), Massachusetts Institute
  of Technology.
- **Catalog landing page (source URL):** https://electionlab.mit.edu/data
- **Canonical dataset used to verify schema & licence:** "County Presidential Election Returns
  2000-2024", Harvard Dataverse, DOI `10.7910/DVN/VOQCHQ`
  (https://doi.org/10.7910/DVN/VOQCHQ).
- **Retrieval date:** 2026-06-28
- **Required attribution string (recommended):**

  > MIT Election Data and Science Lab, "County Presidential Election Returns 2000-2024",
  > https://doi.org/10.7910/DVN/VOQCHQ, Harvard Dataverse. Released under CC0 1.0.

  Note: under CC0 the publisher waives the *requirement* to attribute, but MEDSL and
  scholarly norms request the citation above. Always cite.

---

## Source licence

- **Verified licence:** **CC0 1.0 Universal (Public Domain Dedication)**.
- **Licence URI:** http://creativecommons.org/publicdomain/zero/1.0
- **How verified:** Retrieved the dataset metadata directly from the Harvard Dataverse API on
  2026-06-28:
  `https://dataverse.harvard.edu/api/datasets/:persistentId/?persistentId=doi:10.7910/DVN/VOQCHQ`
  The metadata `license` block returns `name: "CC0 1.0"` and
  `uri: "http://creativecommons.org/publicdomain/zero/1.0"`.
- **Does it permit derivatives / redistribution?** **Yes.** CC0 1.0 is a public-domain
  dedication: the rights holder waives all copyright and related rights "to the extent
  permitted by law", placing the work in the public domain worldwide. This explicitly permits
  copying, modification, distribution, and derivative works, for any purpose, without
  permission (see the CC0 deed: https://creativecommons.org/publicdomain/zero/1.0/ —
  "You can copy, modify, distribute and perform the work, even for commercial purposes, all
  without asking permission.").

> Caveat on the broader catalog: the MEDSL catalog page lists many datasets across geographic
> levels and years. Licences are assigned *per dataset* on Harvard Dataverse and are mostly
> CC0, but a small number may differ. The CC0 verification above is confirmed for the County
> Presidential returns dataset specifically. **Re-verify the licence for each individual
> dataset before reuse.**

---

## Data dictionary

Fields below reflect MEDSL's published schema for the County Presidential Election Returns
dataset (the canonical wide format also mirrored across MEDSL's other county/state returns).
The licence was verified against the live Dataverse API; the per-field descriptions reflect
MEDSL's documented codebook and the long-standing public schema of this dataset. Rows that
could not be confirmed against a live codebook on the retrieval date are marked
*unverified*.

| Field            | Type    | Units        | Description                                                        | Allowed values / nulls |
|------------------|---------|--------------|-------------------------------------------------------------------|------------------------|
| `year`           | integer | calendar year| Election year.                                                    | 2000, 2004, … 2024; not null |
| `state`          | string  | -            | Full state name.                                                  | e.g. "ALABAMA"; not null |
| `state_po`       | string  | -            | Two-letter USPS state abbreviation.                              | e.g. "AL"; not null |
| `state_fips`     | integer | FIPS code    | Numeric ANSI/FIPS state code.                                     | 1–56; not null *(unverified for this revision)* |
| `state_cen`      | integer | Census code  | Census Bureau state code.                                         | *(unverified)* |
| `state_ic`       | integer | ICPSR code   | ICPSR state code.                                                 | *(unverified)* |
| `county_name`    | string  | -            | County (or county-equivalent) name.                              | e.g. "AUTAUGA"; may be null/"" for non-county units |
| `county_fips`    | integer/string | FIPS code | 5-digit county FIPS (state+county). May be zero-padded string.   | nullable where county unknown |
| `office`         | string  | -            | Contest/office.                                                  | "US PRESIDENT" for this dataset; not null |
| `candidate`      | string  | -            | Candidate name as standardized by MEDSL.                        | uppercase; "OTHER" used for aggregated minor candidates |
| `party`          | string  | -            | Standardized party label.                                       | e.g. "DEMOCRAT", "REPUBLICAN", "OTHER", "GREEN", "LIBERTARIAN"; nullable |
| `candidatevotes` | integer | vote count   | Votes for that candidate in that county/year/mode.              | >= 0; not null |
| `totalvotes`     | integer | vote count   | Total votes cast for the office in that county/year.            | >= 0; not null |
| `mode`           | string  | -            | Vote mode (where reported).                                     | "TOTAL" common; may include "ELECTION DAY", "ABSENTEE", etc. *(values vary by year)* |
| `version`        | integer | date stamp   | Dataset version/build date (e.g. YYYYMMDD).                     | not null |

No personal or identifying fields are present: rows are aggregate vote counts at the
county/precinct/state level, not individual ballots or voters. (See PII note under
Limitations.)

---

## Datasheet for Datasets

**Motivation.** Created to provide cleaned, standardized, citable U.S. election returns so
researchers, journalists, and the public can analyze results without scraping and
reconciling inconsistent official sources. Funded/maintained by the MIT Election Data and
Science Lab.

**Composition.** Each record is an aggregate count: votes for a candidate (or aggregated
"OTHER") within a geographic unit (county/precinct/state) for a given office and year, plus a
`totalvotes` denominator. Instances are vote tallies, **not** individuals. The County
Presidential file spans 2000–2024 across all U.S. states and county-equivalents.

**Collection process.** Compiled from official certified state/county election returns,
standardized by MEDSL into a uniform schema (consistent state/party/candidate labels, FIPS
codes). For some products (e.g., cast-vote-record work) MEDSL notes data were "created by
downloading publicly available unstandardized cast vote records, standardizing them into a
multi-state database, and extensively comparing their totals to certified election results."

**Preprocessing / cleaning / labeling.** Names normalized to uppercase; parties and candidate
names standardized; FIPS/ANSI geographic codes attached; totals reconciled against certified
results. Minor candidates may be collapsed into "OTHER". Exact cleaning rules vary by year;
consult the per-file README/codebook on Dataverse.

**Uses.** Academic research, journalism, civic education, turnout/competitiveness analysis,
joining to Census/ACS data via FIPS. Suitable for derivative datasets and visualizations
(CC0). Not a source of individual-level or ballot-level voter data.

**Distribution.** Distributed via Harvard Dataverse (DOI-stamped, versioned) and linked from
https://electionlab.mit.edu/data. Released under CC0 1.0. **This datasheet does not host,
mirror, or redistribute the data** — obtain it from the official DOI.

**Maintenance.** Maintained by MEDSL; updated after major election cycles (the presidential
file now extends through 2024). Versions are tracked via the `version` field and Dataverse
version history; contact MEDSL / dataset depositor (Samuel Baltz, MIT) for issues.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "dataType": "cr:dataType",
    "field": "cr:field",
    "recordSet": "cr:recordSet"
  },
  "@type": "Dataset",
  "name": "County Presidential Election Returns 2000-2024",
  "description": "Cleaned, standardized county-level U.S. presidential election returns (2000-2024) published by the MIT Election Data and Science Lab. Aggregate vote counts by county, candidate, and party; no individual-level data.",
  "url": "https://doi.org/10.7910/DVN/VOQCHQ",
  "sameAs": "https://electionlab.mit.edu/data",
  "license": "http://creativecommons.org/publicdomain/zero/1.0",
  "creator": {
    "@type": "Organization",
    "name": "MIT Election Data and Science Lab",
    "url": "https://electionlab.mit.edu"
  },
  "datePublished": "2026-06-28",
  "version": "2000-2024",
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "county_returns",
      "field": [
        { "@type": "cr:Field", "name": "year", "dataType": "sc:Integer", "description": "Election year." },
        { "@type": "cr:Field", "name": "state_po", "dataType": "sc:Text", "description": "Two-letter USPS state abbreviation." },
        { "@type": "cr:Field", "name": "county_fips", "dataType": "sc:Text", "description": "5-digit county FIPS code." },
        { "@type": "cr:Field", "name": "candidate", "dataType": "sc:Text", "description": "Standardized candidate name." },
        { "@type": "cr:Field", "name": "party", "dataType": "sc:Text", "description": "Standardized party label." },
        { "@type": "cr:Field", "name": "candidatevotes", "dataType": "sc:Integer", "description": "Votes for the candidate in the county/year." },
        { "@type": "cr:Field", "name": "totalvotes", "dataType": "sc:Integer", "description": "Total votes cast for the office in the county/year." }
      ]
    }
  ]
}
```

---

## Validation script

This script validates the **structure** of a locally-obtained copy of the dataset. It does
**not** download, host, or redistribute any data — you must supply your own local file that
you obtained from the official DOI.

```python
#!/usr/bin/env python3
"""Validate the structure of a local MEDSL county presidential returns CSV.

Documentation-only: this does NOT download or host the dataset. Point it at a CSV
you have already obtained from https://doi.org/10.7910/DVN/VOQCHQ.

Usage: python validate_medsl.py countypres_2000-2024.csv
"""
import csv
import sys

EXPECTED_COLUMNS = {
    "year", "state", "state_po", "county_name", "county_fips",
    "office", "candidate", "party", "candidatevotes", "totalvotes",
    "version", "mode",
}

def main(path: str) -> int:
    with open(path, newline="", encoding="utf-8") as fh:
        reader = csv.DictReader(fh)
        cols = set(reader.fieldnames or [])
        missing = EXPECTED_COLUMNS - cols
        if missing:
            print(f"FAIL: missing expected columns: {sorted(missing)}")
            return 1
        rows = 0
        bad = 0
        for r in reader:
            rows += 1
            try:
                cv = int(r["candidatevotes"])
                tv = int(r["totalvotes"])
                int(r["year"])
                if cv < 0 or tv < 0 or cv > tv:
                    bad += 1
            except (ValueError, TypeError):
                bad += 1
        print(f"OK: found columns {sorted(cols & EXPECTED_COLUMNS)}")
        print(f"rows={rows}, rows_failing_numeric_checks={bad}")
        if rows == 0:
            print("WARN: zero data rows")
            return 1
        return 0 if bad == 0 else 2

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__)
        sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

Expected: a non-zero row count, all `EXPECTED_COLUMNS` present, and
`0 <= candidatevotes <= totalvotes` for every row.

---

## Limitations & gaps

- **Licence scope:** CC0 1.0 was verified via the live Dataverse API **for the County
  Presidential Election Returns dataset only** (DOI 10.7910/DVN/VOQCHQ). Other MEDSL catalog
  datasets (Senate, House, state/local precinct returns) are individually licensed on
  Dataverse and should be re-checked before reuse; the catalog landing page itself did not
  expose machine-readable licence terms.
- **Field verification:** The CC0 licence, dataset title, publisher, and depositor were
  confirmed from the live API. Per-field descriptions follow MEDSL's long-standing published
  schema/codebook for this dataset; rows marked *(unverified)* could not be confirmed against
  a live codebook on the retrieval date and may vary by dataset revision. Validate column
  names against your actual downloaded file (the script above does this).
- **Schema drift:** Column sets and `mode`/`party`/candidate value vocabularies vary across
  years and across the precinct vs county vs state products. Always consult the per-file
  README on Dataverse.
- **No data included:** No data rows were sampled, transformed, hosted, or committed. No
  personal or identifying information is present in this datasheet; the dataset itself is
  aggregate-only and contains no individual voter records.
- **License snapshot:** A hashed/archived copy of the full CC0 legal text was not attached to
  this file; the canonical text lives at https://creativecommons.org/publicdomain/zero/1.0/legalcode
  and should be archived alongside any production gate artifact.
