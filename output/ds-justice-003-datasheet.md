# Datasheet — Bureau of Justice Statistics (BJS) Data

**One-line summary:** A documentation datasheet for the U.S. Bureau of Justice Statistics
(BJS) statistical data portal — aggregated criminal-justice statistics (corrections, courts,
victimization, law enforcement, recidivism, and more) published as a U.S. Government work in
the public domain.

*This datasheet (the documentation in this file) is licensed **CC-BY-4.0**. It does not host,
mirror, or republish any BJS dataset — it documents one.*

> **Scope note (read first):** `https://bjs.ojp.gov/` is a *portal* that fronts many distinct
> data products (e.g., the National Crime Victimization Survey, National Prisoner Statistics,
> NIBRS-derived tables, Federal Justice Statistics). No single canonical tabular file/schema
> exists for "BJS data" as a whole. This datasheet documents the **portal-level provenance and
> licence** with confidence, and provides a **representative, clearly-marked-unverified** data
> dictionary because individual product schemas vary per release. Field-level rows below are
> marked *(unverified — representative)* unless confirmed against a specific download.

---

## Provenance & attribution

| Item | Value |
|---|---|
| **Publisher / creator** | U.S. Bureau of Justice Statistics (BJS), Office of Justice Programs, U.S. Department of Justice |
| **Source URL** | https://bjs.ojp.gov/ |
| **Catalog id (candidate)** | cat-justice-003 |
| **Retrieval date** | 2026-06-28 |
| **Content type** | Aggregated/statistical criminal-justice data and statistical tables (public, non-individual) |

**Required attribution string (recommended):**

> Bureau of Justice Statistics, Office of Justice Programs, U.S. Department of Justice.
> Retrieved 2026-06-28 from https://bjs.ojp.gov/. Public-domain U.S. Government work
> (17 U.S.C. § 105). For a specific data product, cite that product's title, series, and
> release year as listed on its BJS page.

BJS directs users to its **Data Release Policy** for product-specific citation expectations.
Attribution is a courtesy/scholarly norm here, **not** a copyright condition (see licence).

---

## Source licence

**Licence:** **U.S. Government Work — Public Domain (not subject to copyright)**, per
**17 U.S.C. § 105**. Works prepared by U.S. Government officers/employees as part of official
duties are not eligible for copyright protection, so they may be freely reproduced, reused, and
adapted (derivative works permitted) without permission or fee.

**Verification — does it permit derivatives? YES.** Because no copyright subsists, derivative
works are unrestricted. Cited authority:

- **17 U.S.C. § 105 (statutory text, quoted):** *"Copyright protection under this title is not
  available for any work of the United States Government..."* —
  https://www.copyright.gov/title17/92chap1.html
- **17 U.S.C. § 101 definition (quoted):** a *"work of the United States Government"* is *"a
  work prepared by an officer or employee of the United States Government as part of that
  person's official duties."* — https://www.copyright.gov/title17/92chap1.html
- **USA.gov, government works guidance:** points to Copyright Law §§ 101 and 105 for the public
  status of U.S. Government works — https://www.usa.gov/government-copyright

**Caveats captured during verification (do not change the derivatives conclusion, but apply
when reusing):**
- Do not use the material in a way that **implies government endorsement**.
- Do not reuse **federal trademarks or agency logos** without permission.
- A specific BJS product *could* embed third-party or restricted-access microdata governed by
  separate terms (e.g., restricted-use NCVS microdata via ICPSR). The **public statistical
  tables/aggregates** documented here are public domain; confirm per product before reusing raw
  microdata.

### Licence snapshot (archived text + hash)

Archived licence text (the controlling clause), recorded for integrity:

```
Copyright protection under this title is not available for any work of the United States Government, but the United States Government is not precluded from receiving and holding copyrights transferred to it by assignment, bequest, or otherwise. (17 U.S.C. Sec. 105)
```

- **SHA-256 of the snapshot text above:** `49ab33d22b45dbc7761b40800e579b9ece031c2e5a1f86f18b32a439c187d185`
- **Snapshot source:** https://www.copyright.gov/title17/92chap1.html (retrieved 2026-06-28)

---

## Data dictionary

BJS statistical tables are typically published as wide aggregate tables (CSV/XLSX/PDF) keyed by
geography, time, and demographic/offense categories, with numeric estimate columns. The schema
below is a **representative** structure common across BJS aggregate releases. **Every row is
marked unverified** because no single product file was downloaded (documentation-only deed; see
guardrails). Confirm against a specific product's codebook before relying on it.

| Field (representative) | Type | Units | Description | Allowed values / null handling | Status |
|---|---|---|---|---|---|
| `year` | integer | calendar year | Reference year / survey year of the estimate | 4-digit year; non-null | *(unverified — representative)* |
| `jurisdiction` / `state` | string | — | Geographic unit (national, state, or federal jurisdiction) | "U.S. total", state names, or "Federal"; non-null | *(unverified — representative)* |
| `category` / `offense_type` | string | — | Offense, status, or program category the estimate covers | Controlled vocabulary per product codebook | *(unverified — representative)* |
| `demographic` (sex/race/age) | string | — | Demographic breakdown dimension (aggregated groups only) | Aggregated bands; "All" for totals | *(unverified — representative)* |
| `estimate` / `count` | number | persons / events / rate | The aggregate statistic (count, percent, or rate) | >= 0; nulls/suppression flags common | *(unverified — representative)* |
| `rate` | number | per 100,000 (typical) | Population-normalized rate where applicable | >= 0; may be null when N too small | *(unverified — representative)* |
| `standard_error` / `CV` | number | same as estimate / % | Sampling error for survey-based products (e.g., NCVS) | >= 0; null for census-based products | *(unverified — representative)* |
| suppression flag | string/char | — | Indicates withheld/unreliable cells | e.g., `~`, `:`, `NA`, `*` per product legend | *(unverified — representative)* |

**Note:** No personal/identifying fields are documented or sampled. BJS public products are
aggregate statistics; individual-level restricted-use microdata (if any) is out of scope and
must not be documented or sampled here.

---

## Datasheet for Datasets

**Motivation.** Created by BJS to collect, analyze, and disseminate objective statistics on
crime and the administration of justice in the United States, informing policymakers,
researchers, and the public. Funded and produced by the U.S. Department of Justice.

**Composition.** Aggregated statistical estimates and tables spanning corrections, courts,
crime/victimization, federal justice, forensic sciences, law enforcement, recidivism/reentry,
tribal crime, and victims of crime. Instances are typically aggregate cells (by year,
geography, category, demographic), not individuals. Public products contain **no direct
personal identifiers**; some series carry small-cell suppression to protect confidentiality.

**Collection process.** Data are gathered through national programs and surveys, including the
National Crime Victimization Survey (NCVS), National Prisoner Statistics (NPS), the National
Incident-Based Reporting System (NIBRS), and the Federal Justice Statistics Program, among
others. Methods include sample surveys, administrative-record censuses, and agency reporting.
Methodology is documented per product.

**Preprocessing / cleaning.** BJS performs weighting, estimation, disclosure-avoidance
suppression, and quality review per its **Data Quality Guidelines** and **Statistical
Principles and Practices**. Specific transformations are described in each product's
methodology/codebook.

**Uses.** Policy analysis, academic research, journalism, public accountability, and
derivative statistical work. Suitable for derivative works (public domain). **Not** suitable
for re-identification attempts; **not** to imply government endorsement of derived products.

**Distribution.** Distributed publicly via https://bjs.ojp.gov/ as statistical tables and
downloadable files, plus analysis tools. Restricted-use microdata (where it exists) is
distributed separately under access controls (e.g., via ICPSR) and is out of scope here.

**Maintenance.** Maintained by BJS, which issues periodic updates and new releases by series.
Errata and revisions are published with products. Contact and FOIA channels are available via
the BJS/OJP site.

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
  "name": "Bureau of Justice Statistics (BJS) Data",
  "description": "Aggregated U.S. criminal-justice statistics (corrections, courts, victimization, law enforcement, recidivism, and related domains) published by the U.S. Bureau of Justice Statistics. Public-domain U.S. Government work. This is a documentation record only; it does not host or mirror the data.",
  "url": "https://bjs.ojp.gov/",
  "license": "https://www.usa.gov/government-copyright",
  "creator": {
    "@type": "GovernmentOrganization",
    "name": "U.S. Bureau of Justice Statistics, Office of Justice Programs, U.S. Department of Justice",
    "url": "https://bjs.ojp.gov/"
  },
  "datePublished": "2026-06-28",
  "isAccessibleForFree": true,
  "creditText": "Bureau of Justice Statistics, U.S. Department of Justice. Public domain (17 U.S.C. 105).",
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "bjs_aggregate_table_representative",
      "description": "Representative (unverified) schema for a BJS aggregate statistical table; confirm against the specific product codebook.",
      "field": [
        { "@type": "cr:Field", "name": "year", "dataType": "sc:Integer", "description": "Reference/survey year (unverified — representative)." },
        { "@type": "cr:Field", "name": "jurisdiction", "dataType": "sc:Text", "description": "Geographic unit: national/state/federal (unverified — representative)." },
        { "@type": "cr:Field", "name": "category", "dataType": "sc:Text", "description": "Offense/status/program category (unverified — representative)." },
        { "@type": "cr:Field", "name": "estimate", "dataType": "sc:Float", "description": "Aggregate count/percent/rate estimate (unverified — representative)." },
        { "@type": "cr:Field", "name": "standard_error", "dataType": "sc:Float", "description": "Sampling error for survey-based estimates; null for census products (unverified — representative)." }
      ]
    }
  ]
}
```

---

## Validation script

Documentation only. This script **does not download, host, or transform** any BJS data. Point
it at a CSV file you have *already* obtained yourself from BJS, in your own local/ephemeral
environment, to check that its structure matches expectations. Adjust `EXPECTED` to the actual
product codebook before use.

```python
#!/usr/bin/env python3
"""Validate the STRUCTURE of a locally-obtained BJS aggregate CSV.

Does NOT fetch, host, mirror, or republish data. It only inspects a file the
operator already has, reading at most a small header sample. Configure EXPECTED
to match the specific BJS product's codebook (the columns below are
representative and UNVERIFIED).
"""
import csv
import sys

# Representative expectations — REPLACE per the specific product codebook.
EXPECTED_COLUMNS = {"year", "jurisdiction", "category", "estimate"}
MAX_SAMPLE_ROWS = 1000          # bounded read; never load the whole file blindly
MIN_ROWS_EXPECTED = 1           # set to the codebook's documented row count if known

def validate(path: str) -> int:
    with open(path, newline="", encoding="utf-8-sig") as fh:
        reader = csv.reader(fh)
        try:
            header = next(reader)
        except StopIteration:
            print("FAIL: file is empty")
            return 1

        cols = {c.strip() for c in header}
        missing = EXPECTED_COLUMNS - cols
        if missing:
            print(f"FAIL: missing expected columns: {sorted(missing)}")
            print(f"      found columns: {sorted(cols)}")
            return 1

        rows = 0
        for _ in reader:
            rows += 1
            if rows >= MAX_SAMPLE_ROWS:
                break

        if rows < MIN_ROWS_EXPECTED:
            print(f"FAIL: fewer rows than expected (sampled {rows})")
            return 1

    print(f"OK: header has expected columns; sampled {rows} data row(s) "
          f"(capped at {MAX_SAMPLE_ROWS}).")
    return 0

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("usage: validate_bjs.py <local_bjs_export.csv>")
        sys.exit(2)
    sys.exit(validate(sys.argv[1]))
```

---

## Limitations & gaps

- **Portal, not one dataset.** `bjs.ojp.gov` aggregates many distinct products with differing
  schemas, release cadences, and codebooks. The data dictionary and Croissant `recordSet` here
  are **representative and explicitly unverified** — no specific product file was downloaded
  (documentation-only deed; bounded-access guardrail respected).
- **No homepage licence string.** The homepage carries no explicit licence text; the
  public-domain conclusion rests on **17 U.S.C. § 105** (the governing statute for U.S.
  Government works) plus USA.gov guidance, not on a per-page licence notice. This is
  authoritative for federal works but should be re-confirmed for any product that may embed
  third-party or restricted-use microdata.
- **Restricted-use microdata out of scope.** Some BJS series have access-controlled
  individual-level files (e.g., via ICPSR) under separate terms; those were neither documented
  nor sampled and would require their own datasheet and licence review.
- **Attribution norms unconfirmed per product.** The exact citation format BJS prefers lives in
  its Data Release Policy PDF, which was not parsed field-by-field here; the attribution string
  above is a best-practice composite.
- **No data was hosted, mirrored, transformed, or sampled** in producing this datasheet. No
  personal/identifying data is included.
