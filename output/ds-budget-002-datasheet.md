# Datasheet: USAspending.gov Federal Award & Spending Data

**One-line summary:** Documentation datasheet for the U.S. federal government's
authoritative, machine-readable record of federal awards (contracts, grants, loans, direct
payments, and other financial assistance) published via USAspending.gov.

*This datasheet (the document you are reading) is licensed under **CC-BY-4.0**. It is
documentation only — it does not host, mirror, transform, or republish any of the underlying
dataset.*

---

## Provenance & attribution

| Field | Value |
|---|---|
| **Publisher / source authority** | U.S. Department of the Treasury, Bureau of the Fiscal Service (operator of USAspending.gov) |
| **Dataset** | USAspending.gov federal award & spending data |
| **Source URL (download center)** | https://www.usaspending.gov/download_center/custom_award_data |
| **Data dictionary (authoritative)** | https://api.usaspending.gov/api/v2/references/data_dictionary/ ("Rosetta Crosswalk" Data Dictionary) |
| **Catalog id (candidate)** | cat-budget-002 |
| **Retrieval date** | 2026-06-28 |
| **Required attribution string** | "Source: USAspending.gov, U.S. Department of the Treasury (Bureau of the Fiscal Service). Retrieved 2026-06-28. Public domain (CC0 1.0)." |

Mandated by the DATA Act of 2014 (Digital Accountability and Transparency Act); USAspending.gov
is the official public source for federal spending transparency data.

---

## Source licence

**Verified licence: CC0 1.0 Universal (Public Domain Dedication).**

- **Cited source:** The official USAspending repository (org `fedspendingtransparency`,
  maintained by the Bureau of the Fiscal Service) publishes its code and data under CC0 1.0.
  LICENSE file: https://github.com/fedspendingtransparency/usaspending-api/blob/master/LICENSE
- **Clause confirming derivatives are permitted (CC0 1.0):** the affirmer waives all rights so
  that the public may *"reliably and without fear of later claims of infringement build upon,
  modify, incorporate in other works, reuse and redistribute as freely as possible in any form
  whatsoever and for any purposes, including without limitation commercial purposes."*
- **Reinforcing legal basis:** Works prepared by U.S. federal government employees as part of
  their official duties are not subject to copyright protection (17 U.S.C. § 105); USA.gov
  confirms federal government works are in the public domain
  (https://www.usa.gov/government-copyright).

**Conclusion: the source licence permits reuse, redistribution, and derivative works.**
LicenseVerified = true.

> Note on permitted-use caveats (not licence restrictions, but good practice): do not use the
> data in a way that implies U.S. government endorsement, and do not reuse federal logos/
> trademarks without permission (per USA.gov government-works guidance).

### Licence snapshot
- Licence text canonical URL: https://creativecommons.org/publicdomain/zero/1.0/legalcode
- Source LICENSE file URL (archived reference): https://github.com/fedspendingtransparency/usaspending-api/blob/master/LICENSE
- Snapshot method: SHA-256 of the retrieved CC0 1.0 legalcode text should be recorded by the
  maintainer at archival time (not embedded here to avoid republishing third-party text in this
  documentation-only deliverable).

---

## Data dictionary

Fields below are verified against the authoritative USAspending "Rosetta Crosswalk" Data
Dictionary endpoint (retrieved 2026-06-28). The full dictionary contains several hundred
elements across procurement (FPDS) and financial-assistance (FABS) award types; the table is a
representative, verified core subset. Types/units are inferred from the element definitions and
are marked where not explicitly typed by the source.

| Field name | Type | Units | Description | Allowed values / null handling |
|---|---|---|---|---|
| `ActionDate` | date | YYYY-MM-DD | Date the reported action was issued/signed by the Government or a binding agreement reached. | Valid date; required on transactions. |
| `ActionDateFiscalYear` | integer | fiscal year | Federal fiscal year (Oct 1 – Sep 30) of the action. | e.g. 2026. |
| `ActionType` | string (code) | — | Code describing the modification type. | Assistance: New, Continuation, Revision; Contracts: Supplemental Agreement, Change Order, Termination (etc.). |
| `AssistanceType` | string (code) | — | Category of financial assistance provided. | Block grants, project grants, cooperative agreements, direct loans, guaranteed/insured loans, etc. |
| `AssistanceListingNumber` | string (code) | — | CFDA/Assistance Listing number from SAM.gov (financial assistance only). | Pattern `NN.NNN`; null for contracts. |
| `AwardingAgencyCode` | string (code) | — | Department/establishment responsible for the award. | Controlled agency code list. |
| `AwardingSubTierAgencyCode` | string (code) | — | Level-2 organization that awarded/executed the transaction. | Controlled sub-tier code list. |
| `AwardingOfficeCode` | string (code) | — | Office that awarded/executed or is responsible for the transaction. | Controlled office code list; may be null. |
| `AwardModificationAmendmentNumber` | string | — | Identifier of a subsequent change to the initial award. | Null/0 for the base action. |
| `AwardDescription` | string (free text) | — | Plain-English description/purpose of the award or modification. | May be null; truncated for long descriptions. |
| `AwardLatestActionDate` | date | YYYY-MM-DD | Most recent action date associated with the award. | Valid date. |
| `AssistanceListingNumber` is financial-assistance only — see above. | — | — | — | — |
| `AwardeeOrRecipientLegalEntityName` | string | — | Legal name of the awardee/recipient tied to the unique identifier. | For individual recipients, USAspending redacts personal data ("REDACTED DUE TO PII"). |
| `AwardeeOrRecipientUEI` | string (code) | — | Unique Entity Identifier (UEI) for the awardee/recipient. | 12-char SAM.gov UEI; may be null for legacy records. |
| `CAGECode` | string (code) | — | CAGE Code of the entity; key into SAM, maps to UEI. | May be null. |
| `BaseAndAllOptionsValue` | number (decimal) | USD | Mutually agreed total contract value including all options. | Contracts only; null for assistance. |
| `BusinessTypes` | string (code list) | — | Recipient organization classification. | e.g. state government, nonprofit, small business, individual. |
| `AccountTitle` | string | — | Descriptive name of the Treasury Account Symbol (TAS). | May be null. |

**Unverified / requires confirmation (do NOT treat as authoritative):**
- *Exact CSV column header strings* in the Custom Award Data download bundle were **not
  confirmed** here — the download_center page is a client-rendered SPA and did not expose column
  text to retrieval. The names above are the canonical dictionary element names; download files
  may use slightly different header labels. **Mark as unverified until validated against an
  actual header row.**
- *Precise numeric scale/precision* and *enumerated full code lists* (agency, action-type,
  assistance-type) are governed by external reference lists (FPDS/FABS) and were not enumerated
  in full here.

---

## Datasheet for Datasets

**Motivation.** Created to satisfy the Federal Funding Accountability and Transparency Act and
the DATA Act of 2014: provide a single authoritative public record of how federal money is
awarded and spent, enabling oversight, journalism, research, and civic accountability. Funded
and maintained by the U.S. Treasury (Bureau of the Fiscal Service).

**Composition.** Records represent federal award transactions and award summaries across award
types: contracts (procurement, from FPDS-NG), financial assistance (grants, loans, direct
payments, insurance — from the FABS/Broker pipeline), and IDV/contract vehicles. Each record
links agency, recipient, amounts, dates, geography, and program (CFDA/Assistance Listing) data.
The full population is the universe of reported federal awards; it is not a sample. For
*individual* (natural-person) recipients, personal data is redacted by the publisher.

**Collection process.** Data is submitted by federal agencies through statutory reporting
systems (FPDS-NG for contracts; agency financial systems via the DATA Act Broker / FABS for
assistance), validated, and aggregated by Treasury. Cadence is continuous with periodic agency
certification; values can be revised by later modifications.

**Preprocessing / cleaning.** Treasury's Broker validates and standardizes submissions, links
transactions to award summaries (Rosetta crosswalk), and redacts PII for individual recipients.
Derived/rolled-up fields (e.g., award totals, latest action date) are computed downstream.

**Uses.** Spending analysis, oversight and audit, grant/contract research, recipient due
diligence, economic and policy research, journalism. Suitable for derivative datasets and
dashboards. **Not** suitable as a system of record for legal/financial determinations without
agency verification, and not suitable for re-identifying redacted individuals.

**Distribution.** Publicly distributed via USAspending.gov (bulk Custom Award Data downloads,
Award Data Archive, and a public REST API at api.usaspending.gov). Free, no authentication, no
licence fee. CC0 1.0 / public domain.

**Maintenance.** Maintained by the Bureau of the Fiscal Service. Continuously updated; schema
governed by the published Data Dictionary and DATA Act Information Model Schema (DAIMS).
Corrections occur via agency resubmission and award modifications.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "dataType": "cr:dataType",
    "Field": "cr:Field",
    "RecordSet": "cr:RecordSet"
  },
  "@type": "Dataset",
  "name": "USAspending.gov Federal Award & Spending Data",
  "description": "Authoritative, machine-readable record of U.S. federal awards (contracts, grants, loans, direct payments, and other financial assistance), published under the DATA Act by the U.S. Department of the Treasury, Bureau of the Fiscal Service.",
  "url": "https://www.usaspending.gov/download_center/custom_award_data",
  "sameAs": "https://api.usaspending.gov/api/v2/references/data_dictionary/",
  "license": "https://creativecommons.org/publicdomain/zero/1.0/",
  "creator": {
    "@type": "GovernmentOrganization",
    "name": "U.S. Department of the Treasury, Bureau of the Fiscal Service",
    "url": "https://www.usaspending.gov"
  },
  "datePublished": "2014",
  "dateModified": "2026-06-28",
  "keywords": ["federal spending", "awards", "contracts", "grants", "DATA Act", "public finance"],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "award_transactions",
      "description": "One row per reported federal award action/transaction.",
      "field": [
        { "@type": "cr:Field", "name": "ActionDate", "description": "Date the action was issued/signed.", "dataType": "sc:Date" },
        { "@type": "cr:Field", "name": "AwardingAgencyCode", "description": "Department responsible for the award.", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "AwardeeOrRecipientUEI", "description": "Unique Entity Identifier of the recipient.", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "AwardeeOrRecipientLegalEntityName", "description": "Recipient legal name (PII redacted for individuals).", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "BaseAndAllOptionsValue", "description": "Total contract value incl. options (USD).", "dataType": "sc:Number" },
        { "@type": "cr:Field", "name": "AssistanceType", "description": "Category of financial assistance.", "dataType": "sc:Text" }
      ]
    }
  ]
}
```

---

## Validation script

Documentation only. The script below validates the **structure** of a USAspending Custom Award
Data CSV that a user has *already* downloaded themselves to a local path. It does **not**
download, fetch, mirror, or host any data.

```python
#!/usr/bin/env python3
"""Validate the structure of a locally-held USAspending award-data CSV.
Documentation-only: does NOT download or host the dataset. Provide your own
locally downloaded file path. PII-safe: reads headers + a bounded sample only.
"""
import csv
import sys

# Canonical dictionary element names (see datasheet "Data dictionary").
# NOTE: actual download header labels may differ; treat mismatches as warnings,
# not hard failures, until confirmed against a real header row.
EXPECTED_CORE = {
    "ActionDate",
    "AwardingAgencyCode",
    "AwardeeOrRecipientUEI",
    "AwardeeOrRecipientLegalEntityName",
    "AssistanceType",
}
MAX_SAMPLE_ROWS = 1000  # bounded read; never load the full file into memory

def validate(path: str) -> int:
    with open(path, newline="", encoding="utf-8-sig") as fh:
        reader = csv.reader(fh)
        try:
            header = next(reader)
        except StopIteration:
            print("FAIL: file is empty")
            return 1
        cols = {c.strip() for c in header}
        missing = EXPECTED_CORE - cols
        if missing:
            print(f"WARN: expected core columns not found (header labels may differ): {sorted(missing)}")
        else:
            print("OK: all expected core columns present")

        rows = 0
        for _ in reader:
            rows += 1
            if rows >= MAX_SAMPLE_ROWS:
                print(f"INFO: stopped after bounded sample of {MAX_SAMPLE_ROWS} rows")
                break
        print(f"INFO: counted {rows} data row(s) in bounded sample; {len(cols)} columns total")
    return 0

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("usage: validate.py <path-to-locally-downloaded.csv>")
        sys.exit(2)
    sys.exit(validate(sys.argv[1]))
```

Run: `python validate.py ./my_local_usaspending_download.csv`

---

## Limitations & gaps

- **Download column headers unverified.** The exact CSV header strings in the Custom Award Data
  bundle were not confirmed (source page is a JavaScript SPA not retrievable as text). The data
  dictionary element names are authoritative, but download header labels may differ; the
  validation script therefore treats column mismatches as warnings.
- **Field table is a representative subset**, not the full several-hundred-element schema.
  Complete enumerations (agency codes, action/assistance-type code lists, exact numeric
  precision) live in external FPDS/FABS reference lists and the DAIMS and were not exhaustively
  reproduced.
- **No row counts or data-quality metrics** were computed: per guardrails, no data was
  downloaded, sampled, or hosted for this deliverable.
- **PII:** No personal/identifying data is documented or sampled here. The publisher redacts PII
  for individual (natural-person) recipients; downstream users must not attempt re-identification.
- **Licence snapshot hash** is described as a maintainer step rather than embedded, to avoid
  reproducing third-party licence text inside this documentation-only file.
- **Catalog id `cat-budget-002`** is a candidate and should be confirmed at the catalog gate.
