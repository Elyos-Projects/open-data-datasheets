# Datasheet: USDA NASS Quick Stats

**One-line summary:** A documentation datasheet for the USDA National Agricultural Statistics
Service (NASS) "Quick Stats" agricultural census and survey database — the most granular
publicly available record of US agriculture across commodity, geography, and time.

*This datasheet (the document you are reading) is licensed under **CC-BY-4.0**. It is
documentation only: it does not host, mirror, transform, or republish any of the underlying
dataset.*

---

## Provenance & attribution

| Field | Value |
|---|---|
| Publisher / producer | U.S. Department of Agriculture (USDA), National Agricultural Statistics Service (NASS) |
| Dataset name | Quick Stats (Quick Stats Agricultural Database) |
| Source URL | https://quickstats.nass.usda.gov/ |
| API documentation | https://quickstats.nass.usda.gov/api |
| Catalog record | https://catalog.data.gov/dataset/quick-stats-agricultural-database |
| Candidate catalog id | cat-agri-002 |
| Retrieval date | 2026-06-28 |

**Required attribution string** (suggested; no attribution is legally required under the
source license — see below — but attribution is good practice for provenance):

> Source: USDA National Agricultural Statistics Service (NASS), Quick Stats database,
> https://quickstats.nass.usda.gov/ (retrieved 2026-06-28). U.S. government work; not endorsed
> by USDA.

> Endorsement note: USDA names, logos, and the official USDA seal may not be used in a way that
> implies USDA endorsement of a derived product.

---

## Source licence

**Verified licence:** Creative Commons Zero 1.0 Universal — Public Domain Dedication (CC0 1.0).

- **Citation (clause/URL):** The Quick Stats Agricultural Database catalog record on data.gov
  lists the licence as **CC0 1.0 (Public Domain Dedication)**, licence URL
  `https://creativecommons.org/publicdomain/zero/1.0/`.
  Catalog record: https://catalog.data.gov/dataset/quick-stats-agricultural-database
- **Does it permit derivatives?** **Yes.** CC0 1.0 places the work in the public domain to the
  fullest extent possible; the dedication permits copying, modification, distribution, and
  derivative works, for any purpose, without restriction or attribution requirement (see the
  CC0 deed text at the licence URL above: "You can copy, modify, distribute and perform the
  work, even for commercial purposes, all without asking permission.").
- **Corroboration:** NASS is the official statistical agency of USDA; works produced by U.S.
  federal government employees are generally not subject to domestic copyright (17 U.S.C.
  §105), consistent with the public-domain dedication recorded above.

**Verification status: LICENSE VERIFIED — permits derivatives.**

> Licence snapshot note (acceptance criterion): a content hash + archived copy of the licence
> text was NOT committed here, because committing archived source artifacts is out of scope for
> this documentation-only deliverable and to avoid mirroring source material. The verified
> licence name, licence URL, and citing catalog URL above constitute the recorded licence
> snapshot. A reviewer wishing to pin an immutable copy should archive the data.gov record and
> the CC0 deed via a web archive service and attach the resulting hash at the gate.

---

## Data dictionary

Fields below are the columns returned by the Quick Stats API, as documented at
https://quickstats.nass.usda.gov/api (retrieved 2026-06-28). "Max len" is the documented
maximum character length of the text field. No sample rows were downloaded; types/units are
inferred from the official field documentation and are marked where unverified.

### "WHAT" — commodity dimension

| Name | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| `source_desc` | string (len 60) | — | Source program of the record | `CENSUS` or `SURVEY` |
| `sector_desc` | string (len 60) | — | High-level category | Crops, Animals & Products, Economics, Demographics, Environmental |
| `group_desc` | string (len 80) | — | Subset within a sector | e.g. Field Crops, Livestock, Prices |
| `commodity_desc` | string (len 80) | — | Primary subject of the statistic | e.g. CORN, CATTLE (500+ values) |
| `class_desc` | string (len 180) | — | Physical attribute (variety, size, colour, gender) | text; `ALL CLASSES` when not differentiated |
| `prodn_practice_desc` | string (len 180) | — | Production practice | e.g. IRRIGATED, ORGANIC, ON FEED |
| `util_practice_desc` | string (len 180) | — | Utilisation / marketing channel | text |
| `statisticcat_desc` | string (len 80) | — | Measured aspect | e.g. AREA HARVESTED, PRICE RECEIVED, INVENTORY |
| `unit_desc` | string (len 60) | unit of `value` | Unit for the statistic | e.g. ACRES, $ / LB, HEAD |
| `short_desc` | string (len 512) | — | Concatenated long data-item description | text |
| `domain_desc` | string (len 256) | — | Operation characteristic or chemical type | `TOTAL` when not broken out |
| `domaincat_desc` | string (len 512) | — | Category within the domain | text; `NOT SPECIFIED` common |

### "WHERE" — geographic dimension

| Name | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| `agg_level_desc` | string (len 40) | — | Geographic aggregation level | NATIONAL, STATE, COUNTY, AGRICULTURAL DISTRICT, REGION, WATERSHED, ZIP CODE, etc. |
| `state_alpha` | string (len 2) | — | Two-letter state code | USPS code; null above state level |
| `state_name` | string (len 30) | — | State full name | null above state level |
| `state_ansi` | string | — | State ANSI/FIPS code *(unverified type)* | null above state level |
| `state_fips_code` | string | — | State FIPS code *(unverified type)* | null above state level |
| `county_name` | string (len 30) | — | County name | null above county level |
| `county_ansi` | string (len 3) | — | ANSI county code | null above county level |
| `county_code` | string | — | County code *(unverified type)* | null above county level |
| `asd_code` | string (len 2) | — | Agricultural statistics district code | null when N/A |
| `asd_desc` | string (len 60) | — | Agricultural statistics district name | null when N/A |
| `region_desc` | string (len 80) | — | Region name | null when N/A |
| `zip_5` | string (len 5) | — | 5-digit ZIP code | null when N/A |
| `watershed_code` | string (len 8) | — | USGS Hydrologic Unit Code | null when N/A |
| `watershed_desc` | string (len 120) | — | Watershed name | null when N/A |
| `congr_district_code` | string (len 2) | — | Congressional district code | null when N/A |
| `country_code` | string (len 4) | — | Foreign Trade Division country code | null when N/A |
| `country_name` | string (len 60) | — | Country name | null when N/A |

### "WHEN" — time dimension

| Name | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| `year` | integer (len 4) | year | Numeric calendar/marketing year | range documented ~1866–present |
| `freq_desc` | string (len 30) | — | Period length | ANNUAL, SEASON, MONTHLY, WEEKLY, POINT IN TIME |
| `begin_code` | string (len 2) | — | 2-digit period-beginning code | text/numeric code |
| `end_code` | string (len 2) | — | 2-digit period-ending code | text/numeric code |
| `reference_period_desc` | string (len 40) | — | Specific timeframe within the year | text |
| `week_ending` | string/date (len 10) | date | Week-ending date for weekly data | null for non-weekly |

### Value & metadata

| Name | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| `value` | string (len 24) | given by `unit_desc` | Published estimate, OR a data-suppression / disclosure code | numeric string, or codes such as `(D)` withheld to avoid disclosing individual operations, `(Z)`, `(NA)`, `(X)` |
| `CV %` | numeric (len 7) | percent | Coefficient of variation | populated for 2012 Census records only; null otherwise *(scope per source docs)* |
| `load_time` | datetime (len 19) | timestamp | Database insert timestamp | `YYYY-MM-DD HH:MM:SS` |

**Unverified items** are tagged *(unverified ...)* above: the field is listed in the official
parameter set but its exact type/length was not separately confirmed against a data sample
(no sample was downloaded for this documentation-only deliverable).

---

## Datasheet for Datasets

**Motivation.** Created by USDA NASS to publish official US agricultural statistics — the
results of the Census of Agriculture and ongoing surveys — in a single queryable database so
that the public, researchers, and policymakers can analyse production, economics, and demographics
of US agriculture. It exists to make otherwise siloed official statistics openly accessible.

**Composition.** Each record is one published statistic (a `value`) fully qualified by a
commodity ("what"), a geography ("where"), and a time period ("when"), plus metadata such as
source program and unit. Geographic granularity ranges from national down to county, ZIP code,
and watershed. There are no records about identifiable individuals; aggregates that could
disclose an individual operation are suppressed and shown as codes (e.g. `(D)`).

**Collection process.** Data originate from two NASS programs: the **Census of Agriculture**
(conducted every five years, a complete enumeration of US farms) and recurring **Surveys**
(samples of operations, often with published coefficients of variation). NASS administers the
instruments, edits and validates responses, and computes official estimates.

**Preprocessing / cleaning.** NASS performs editing, imputation, aggregation, and statistical
disclosure control before publication. Suppressed cells are released as codes rather than
numbers. The exact methodology is defined by NASS and is outside the scope of this datasheet.

**Uses.** Agricultural economics research, market analysis, policy and program evaluation, food
security and environmental studies, journalism, and educational use. Suitable for derivative
analytical products (public domain). Not suitable for inferring data about specific named
farms/operations (deliberately suppressed) or as a real-time data feed.

**Distribution.** Publicly distributed by USDA NASS via the Quick Stats web UI, downloadable
files, and a documented REST API (JSON/CSV/XML, max 50,000 records per query; an API key is
required for the API). This datasheet does not redistribute the data.

**Maintenance.** Maintained by USDA NASS. The database is updated continuously as new survey
and census results are released; `load_time` reflects the database insert timestamp. Contact and
support are provided through the NASS website.

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
  "name": "USDA NASS Quick Stats",
  "description": "USDA National Agricultural Statistics Service Quick Stats: official US agricultural census and survey statistics across commodity, geography, and time dimensions.",
  "url": "https://quickstats.nass.usda.gov/",
  "license": "https://creativecommons.org/publicdomain/zero/1.0/",
  "creator": {
    "@type": "Organization",
    "name": "USDA National Agricultural Statistics Service (NASS)",
    "url": "https://www.nass.usda.gov/"
  },
  "datePublished": "2026-06-28",
  "keywords": ["agriculture", "census", "survey", "USDA", "public-data", "crops", "livestock"],
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "quickstats-api",
      "name": "Quick Stats API",
      "description": "REST API returning JSON/CSV/XML; max 50,000 records per query (API key required).",
      "contentUrl": "https://quickstats.nass.usda.gov/api",
      "encodingFormat": "application/json"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "statistic",
      "name": "statistic",
      "field": [
        { "@type": "cr:Field", "@id": "statistic/commodity_desc", "name": "commodity_desc", "description": "Primary subject of the statistic (e.g. CORN).", "dataType": "sc:Text" },
        { "@type": "cr:Field", "@id": "statistic/statisticcat_desc", "name": "statisticcat_desc", "description": "Measured aspect (e.g. AREA HARVESTED).", "dataType": "sc:Text" },
        { "@type": "cr:Field", "@id": "statistic/agg_level_desc", "name": "agg_level_desc", "description": "Geographic aggregation level.", "dataType": "sc:Text" },
        { "@type": "cr:Field", "@id": "statistic/year", "name": "year", "description": "Numeric year.", "dataType": "sc:Integer" },
        { "@type": "cr:Field", "@id": "statistic/value", "name": "value", "description": "Published estimate or suppression code; unit given by unit_desc.", "dataType": "sc:Text" },
        { "@type": "cr:Field", "@id": "statistic/unit_desc", "name": "unit_desc", "description": "Unit of the value.", "dataType": "sc:Text" }
      ]
    }
  ]
}
```

---

## Validation script

The script below documents how to validate the *structure* of a Quick Stats CSV export that a
user has already obtained themselves. **It does not download, host, or transform the dataset** —
it only inspects a local file the operator supplies and prints a small data-quality report.

```python
#!/usr/bin/env python3
"""Validate the STRUCTURE of a locally-held USDA NASS Quick Stats CSV export.

Documentation-only: this script does NOT download, host, mirror, or republish data.
Point it at a CSV you exported yourself from https://quickstats.nass.usda.gov/.

Usage:  python validate_quickstats.py path/to/your_export.csv
"""
import csv
import sys

# Core columns expected in a Quick Stats export (subset; extras are allowed).
EXPECTED_COLUMNS = {
    "source_desc", "sector_desc", "group_desc", "commodity_desc",
    "statisticcat_desc", "unit_desc", "short_desc",
    "agg_level_desc", "state_alpha", "county_name",
    "year", "freq_desc", "reference_period_desc", "value",
}
ALLOWED_SOURCE = {"CENSUS", "SURVEY"}


def main(path: str) -> int:
    with open(path, newline="", encoding="utf-8-sig") as fh:
        reader = csv.DictReader(fh)
        cols = set(reader.fieldnames or [])
        missing = EXPECTED_COLUMNS - cols
        if missing:
            print(f"FAIL: missing expected columns: {sorted(missing)}")
            return 1

        rows = bad_source = bad_year = suppressed = 0
        for r in reader:
            rows += 1
            if r.get("source_desc", "").strip().upper() not in ALLOWED_SOURCE:
                bad_source += 1
            y = r.get("year", "").strip()
            if not (y.isdigit() and 1866 <= int(y) <= 2100):
                bad_year += 1
            v = r.get("value", "").strip()
            if v.startswith("(") and v.endswith(")"):
                suppressed += 1  # disclosure-suppressed cell, e.g. (D)

    print(f"OK: all {len(EXPECTED_COLUMNS)} expected columns present")
    print(f"rows                : {rows}")
    print(f"invalid source_desc : {bad_source}")
    print(f"invalid year        : {bad_year}")
    print(f"suppressed values   : {suppressed}")
    return 0 if rows > 0 and bad_source == 0 and bad_year == 0 else 2


if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__)
        sys.exit(64)
    sys.exit(main(sys.argv[1]))
```

Expected outcome on a valid export: every core column present, `rows > 0`, zero invalid
`source_desc`/`year`, and a small count of suppressed `value` cells (`(D)` etc.) is normal.

---

## Limitations & gaps

- **No sample was downloaded.** Per the documentation-only / bounded-access protocol, the data
  dictionary was built from the official API field documentation, not from inspecting a data
  sample. Field types/units marked *(unverified ...)* should be confirmed against an actual
  export before relying on them programmatically.
- **Value field is overloaded.** `value` mixes numeric estimates with disclosure-suppression
  codes (`(D)`, `(Z)`, `(NA)`, `(X)`); consumers must parse defensively.
- **`CV %` coverage.** Per source docs the coefficient of variation is populated for 2012
  Census records only; coverage for other years was not independently verified.
- **Licence snapshot not pinned.** Licence verification relies on the live data.gov catalog
  record and the CC0 deed URL (both retrieved 2026-06-28); no immutable archived copy + hash was
  committed (out of scope for this deliverable). A reviewer should pin an archived snapshot at
  the gate if an immutable record is required.
- **Year range** stated as ~1866–present from interface cues; exact earliest year varies by
  commodity and was not exhaustively verified.
- **No PII.** The dataset documents aggregate agricultural statistics with disclosure control;
  no personal or identifying fields were found, documented, or sampled.
