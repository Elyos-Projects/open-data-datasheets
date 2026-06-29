# Datasheet — FBI Crime Data Explorer (UCR / NIBRS)

**One-line summary:** Documentation datasheet for the U.S. FBI *Crime Data Explorer* (CDE),
the public interface to national Uniform Crime Reporting (UCR) and National Incident-Based
Reporting System (NIBRS) crime statistics, published as aggregated counts by agency, year, and
offense category.

> **This datasheet** (the document you are reading) is licensed **CC-BY-4.0**.
> It is documentation only. It does **not** host, mirror, transform, or republish any portion
> of the underlying dataset.

---

## Provenance & attribution

| Field | Value |
|---|---|
| **Dataset** | Crime Data Explorer (UCR / NIBRS) |
| **Publisher** | U.S. Federal Bureau of Investigation (FBI). NIBRS is jointly managed with the Bureau of Justice Statistics (BJS). |
| **Source URL** | https://cde.ucr.cjis.gov/ |
| **Catalog id (candidate)** | cat-justice-002 |
| **Retrieval date** | 2026-06-28 |
| **Coverage (as published)** | All 50 states + D.C. certified to NIBRS as of May 2024; ~82% of the U.S. population covered by NIBRS-reporting agencies. NIBRS became the national standard for U.S. crime reporting in January 2021. |

**Required attribution string** (use when redistributing derivatives of the source data):

> Source: Federal Bureau of Investigation (FBI), *Crime Data Explorer* (Uniform Crime
> Reporting / National Incident-Based Reporting System), https://cde.ucr.cjis.gov/, retrieved
> 2026-06-28. Work of the U.S. Government, public domain (17 U.S.C. § 105).

Although U.S. Government works carry no copyright and attribution is not legally required,
attribution is recommended as a matter of provenance and good practice.

---

## Source licence

**Determination: PUBLIC DOMAIN — derivatives permitted. (Verified.)**

- The Crime Data Explorer dataset is produced by FBI employees as part of their official
  duties, making it a **"work of the U.S. Government."**
- Under **17 U.S.C. § 105**, copyright protection "is not available for any work of the United
  States Government." Such works are in the **public domain**, which permits reproduction,
  redistribution, and the creation of **derivative works** without restriction.
  - Statute: Copyright Law of the United States, Title 17, §§ 101 & 105 —
    https://www.copyright.gov/title17/92chap1.html#105
  - Plain-language confirmation (U.S. government policy): "Government work is something created
    by a U.S. government officer or employee as part of their official duties" and copyright
    protections do not apply — https://www.usa.gov/government-copyright (retrieved 2026-06-28).

**Caveat noted (and why it does not change the determination):** usa.gov cautions that "not
everything that appears on a federal government website is a government work" — third-party
content (e.g., logos, licensed images, externally supplied material) can carry separate rights.
The UCR/NIBRS **statistical aggregates** that the CDE publishes are core FBI-authored government
works and are public domain. Re-users incorporating any third-party material surfaced through
the CDE should verify that material separately.

*Licence snapshot:* The CDE web application loads its terms via client-side JavaScript and did
not render to the fetch tool on 2026-06-28; the public-domain status is therefore established
from the controlling statute (17 U.S.C. § 105) and U.S. government policy rather than an
on-page CDE licence string. A reviewer completing the per-dataset gate should archive a copy of
the CDE terms-of-use text and record its hash. **This is the one unverified item; it does not
affect the derivatives determination, which rests on statute.**

---

## Data dictionary

The CDE publishes **aggregated** crime statistics (counts), not raw incident records, through
its web app, downloadable CSV "datasets/documents," and a public API. The **conceptual data
elements** below are verified against published NIBRS/UCR documentation. The **exact column
names, types, and encodings** of any specific CSV/API export are marked *Unverified* because the
live CDE app/API schema did not render to the fetch tool on 2026-06-28; confirm them against the
actual downloaded file header (bounded, local-only, ephemeral read per the PII protocol).

| Field (conceptual) | Type | Units | Description | Allowed values / null handling | Status |
|---|---|---|---|---|---|
| Reporting agency identifier (ORI) | string | — | FBI Originating Agency Identifier for the law-enforcement agency | 9-char ORI code; non-null for agency-level rows | Verified (UCR/NIBRS concept); exact column name **Unverified** |
| Agency name | string | — | Name of the reporting law-enforcement agency | text; non-null for agency-level rows | Verified concept; column name **Unverified** |
| State | string | — | U.S. state / territory of the agency | 2-letter USPS abbreviation | Verified concept; column name **Unverified** |
| Year | integer | calendar year | Reporting year of the aggregate | e.g., 1985–present; non-null | Verified concept; column name **Unverified** |
| Offense category / type | string | — | Crime classification (see Group A / Group B and UCR violent/property categories) | controlled vocabulary (e.g., aggravated assault, burglary, motor vehicle theft, simple assault, intimidation, destruction of property, animal cruelty, identity theft) | Verified (NIBRS offense taxonomy); exact codes **Unverified** |
| Offense group | string | — | NIBRS grouping of offenses | `Group A` or `Group B` | Verified |
| Actual / reported count | integer | count of offenses or incidents | Number of offenses (or incidents/victims, depending on table) for the agency-year-category | integer ≥ 0; nulls possible where agency did not report | Verified concept; exact metric & nulls **Unverified** |
| Cleared count | integer | count | Offenses cleared (by arrest or exceptional means) | integer ≥ 0; may be null | Verified concept; column name **Unverified** |
| Population covered | integer | persons | Population of the jurisdiction (used as denominator for rates) | integer ≥ 0; may be null | Verified concept; column name **Unverified** |
| Weapon type | string | — | Weapon involved in incident (NIBRS) | controlled vocabulary; may be `None`/null | Verified (NIBRS element); appears in incident-level/aggregated weapon tables |
| Victim / offender / arrestee demographics | aggregated counts | count | Counts by demographic attribute (age band, sex, race) — **aggregated only** | controlled bins; no individual records | Verified (NIBRS element); **only aggregated bins documented — no PII** |

> **PII note:** Only **aggregated** fields are documented. NIBRS *incident-level micro-data*
> exists in the broader UCR program but is **not** documented or sampled here, to avoid any
> personal/identifying content. No individual-level fields are listed above.

---

## Datasheet for Datasets

**Motivation.** Created so the public, researchers, journalists, and policymakers can access
national U.S. crime statistics. NIBRS became the national reporting standard in January 2021,
replacing summary-only UCR reporting with richer incident-based categories (e.g., simple
assault, intimidation, identity theft, animal cruelty) for more accurate measurement.

**Composition.** Aggregated counts of offenses/incidents/arrests by reporting agency, state,
year, and offense category, plus weapon and aggregated demographic breakdowns. The CDE exposes
these via an interactive web app, downloadable summary files, and a public API. Underlying
reports are submitted by law-enforcement agencies; the CDE products are statistical aggregates,
not raw incident records.

**Collection process.** State, local, tribal, and federal law-enforcement agencies certified to
report submit incident/summary data through state UCR programs to the FBI. As of May 2024 all
50 states + D.C. were certified and ~82% of the U.S. population was covered. Coverage varies by
year and agency; non-reporting agencies create gaps.

**Preprocessing / cleaning.** The FBI validates, standardizes (UCR/NIBRS offense taxonomy), and
aggregates submissions. Estimation/imputation may be applied in some published series for
non-reporting agencies; methodology is documented by the FBI and BJS. Re-users should consult
the FBI methodology notes for the specific table/year.

**Uses.** Crime trend analysis, public transparency, research, journalism, resource allocation.
*Not suitable* for: identifying individuals; precise small-area inference where coverage is
incomplete; or cross-year comparisons that ignore the UCR→NIBRS transition and changing agency
participation.

**Distribution.** Published openly by the FBI at https://cde.ucr.cjis.gov/ (web app, file
downloads, public API). Public domain; freely redistributable. **This deed does not
redistribute it.**

**Maintenance.** Maintained by the FBI (UCR Program), with NIBRS jointly managed with BJS.
Updated on the FBI's release schedule (typically annual national releases plus periodic
updates). The CDE is the authoritative public access point.

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
  "name": "FBI Crime Data Explorer (UCR/NIBRS)",
  "description": "Aggregated U.S. national crime statistics (Uniform Crime Reporting and National Incident-Based Reporting System), published by the FBI as offense/incident counts by reporting agency, state, year, and offense category.",
  "url": "https://cde.ucr.cjis.gov/",
  "sameAs": "https://cde.ucr.cjis.gov/",
  "license": "https://www.copyright.gov/title17/92chap1.html#105",
  "creditText": "Federal Bureau of Investigation (FBI), Crime Data Explorer (UCR/NIBRS). Public domain (17 U.S.C. § 105).",
  "isAccessibleForFree": true,
  "creator": {
    "@type": "GovernmentOrganization",
    "name": "U.S. Federal Bureau of Investigation",
    "url": "https://www.fbi.gov/"
  },
  "publisher": {
    "@type": "GovernmentOrganization",
    "name": "U.S. Federal Bureau of Investigation"
  },
  "datePublished": "2021-01-01",
  "dateModified": "2026-06-28",
  "keywords": ["crime", "UCR", "NIBRS", "justice", "public-data", "United States"],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "agency_offense_counts",
      "description": "One aggregated row per agency, year, and offense category (field names UNVERIFIED — confirm against the actual export header).",
      "field": [
        { "@type": "cr:Field", "name": "ori", "description": "FBI Originating Agency Identifier (9-char).", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "state", "description": "USPS 2-letter state/territory abbreviation.", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "year", "description": "Reporting calendar year.", "dataType": "sc:Integer" },
        { "@type": "cr:Field", "name": "offense_category", "description": "NIBRS/UCR offense classification.", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "offense_group", "description": "NIBRS Group A or Group B.", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "actual_count", "description": "Count of offenses/incidents (>= 0).", "dataType": "sc:Integer" }
      ]
    }
  ]
}
```

---

## Validation script

Documentation only — this script **does not download, mirror, or host** the dataset. Point it at
a file you have **already** obtained locally and ephemerally per the bounded-access PII protocol.
It checks structure (expected columns, non-empty, non-negative counts) without inspecting
individual-level data.

```python
#!/usr/bin/env python3
"""Validate the STRUCTURE of a locally-held CDE aggregated export.
Usage: python validate_cde.py path/to/local_export.csv
Does NOT fetch, host, or republish data. Inspects header + bounded rows only.
NOTE: expected column names are UNVERIFIED stubs — edit EXPECTED to match the
real header you observe in your local file before relying on the result.
"""
import csv, sys

EXPECTED = ["ori", "state", "year", "offense_category", "actual_count"]  # UNVERIFIED stubs
MAX_ROWS_SAMPLE = 1000  # bounded, local-only, ephemeral

def main(path):
    with open(path, newline="", encoding="utf-8") as f:
        reader = csv.DictReader(f)
        cols = reader.fieldnames or []
        missing = [c for c in EXPECTED if c not in cols]
        if missing:
            print(f"WARN: expected columns not found (update EXPECTED?): {missing}")
        else:
            print("OK: all expected columns present.")
        n, bad = 0, 0
        for row in reader:
            n += 1
            v = (row.get("actual_count") or "").strip()
            if v and (not v.lstrip("-").isdigit() or int(v) < 0):
                bad += 1
            if n >= MAX_ROWS_SAMPLE:
                break
        print(f"Checked {n} rows (cap {MAX_ROWS_SAMPLE}); {bad} rows with invalid/negative counts.")
        print("PASS" if not missing and bad == 0 else "REVIEW NEEDED")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        sys.exit("Usage: python validate_cde.py path/to/local_export.csv")
    main(sys.argv[1])
```

---

## Limitations & gaps

- **Live schema not captured.** The CDE web app and API render via client-side JavaScript and
  did not return content to the fetch tool on 2026-06-28. Exact column names, data types, the
  precise count metric (offenses vs. incidents vs. victims), and null encodings are therefore
  marked **Unverified** in the data dictionary and Croissant stubs. They must be confirmed
  against an actual local export header before the dictionary is treated as authoritative.
- **Licence text snapshot pending.** Public-domain status is established from statute
  (17 U.S.C. § 105) and U.S. government policy, not from an on-page CDE licence string. A
  reviewer should archive the CDE terms-of-use text and record its hash for the per-dataset
  gate artifact. The derivatives determination itself is solid (statutory).
- **Coverage / comparability.** Agency participation is incomplete and varies by year; the
  UCR→NIBRS transition (national standard from Jan 2021) breaks naive year-over-year
  comparisons. Some series use estimation/imputation.
- **PII boundary.** Only aggregated fields are documented. NIBRS incident-level micro-data was
  deliberately not documented or sampled. No personal/identifying data appears in this datasheet.
