# Datasheet: Price Paid Data (property transactions) — HM Land Registry

**One-line summary:** A datasheet documenting HM Land Registry's *Price Paid Data* — the public register of residential and commercial property sales in England and Wales (from 1 January 1995 onwards), lodged for registration and sold for value.

*This datasheet (the document you are reading) is licensed under **CC-BY-4.0**. It documents the dataset only; it does not host, mirror, transform, or republish any of the underlying data.*

---

## Provenance & attribution

| Item | Value |
|------|-------|
| **Publisher / creator** | HM Land Registry (UK government) |
| **Dataset title** | Price Paid Data (property transactions) |
| **Source (documentation) URL** | https://www.gov.uk/government/statistical-data-sets/price-paid-data-downloads |
| **About / field-spec page** | https://www.gov.uk/guidance/about-the-price-paid-data |
| **Catalog id (candidate)** | cat-housing-001 |
| **Coverage** | All property sales in England & Wales "sold for value and lodged with us for registration", from 1 January 1995 onwards |
| **Update frequency** | Updated on the 20th working day of each month |
| **Retrieval date** | 2026-06-28 |

**Required attribution string** (per HM Land Registry, to be reproduced by any reuser; update the year to match the data vintage you use):

> Contains HM Land Registry data © Crown copyright and database right 2026. This data is licensed under the Open Government Licence v3.0.

---

## Source licence

- **Licence name:** Open Government Licence v3.0 (OGL v3.0)
- **Licence URL (citation):** http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/
- **Permits derivatives? YES — verified.** OGL v3.0 grants the right to "copy, publish, distribute and transmit the Information; **adapt** the Information; and exploit the Information **commercially and non-commercially** for example, by combining it with other Information, or by including it in your own product or application." The explicit grant to *adapt* and to combine/include in your own product confirms that derivative works are permitted (cited clause: "Using Information under this licence" / "You are free to" section of the OGL v3.0 text at the URL above).
- **Licence snapshot:** The authoritative licence text is the version hosted at the National Archives URL above. Reusers should archive a copy of that page text alongside their data vintage and record its retrieval date/hash for provenance. (This datasheet intentionally does not embed the full third-party licence text; it cites the canonical source.)

### Third-party rights caveat (important, not a blocker on the OGL grant)
The HM Land Registry download page notes that **OGL does not cover third-party rights it is not authorised to license**. The **address components** (Postcode, PAON, SAON, Street, Locality, Town/City) derive in part from Royal Mail / Ordnance Survey data, whose reuse for purposes beyond "providing residential property price information services" / personal/non-commercial use may require separate permission (contact Royal Mail: address.management@royalmail.com). The dataset *as a whole* is released under OGL v3.0 and permits derivatives; reusers building products on the **address fields** must check this carve-out independently. This caveat does not change the verified OGL derivative grant for the transaction data.

---

## Data dictionary

Fields below are **verified** from the official HM Land Registry "About the Price Paid Data" guidance page (retrieved 2026-06-28). The CSV is supplied **without a header row**; columns appear in the order shown. There are 16 columns.

| # | Field | Type | Units | Description | Allowed values / null handling |
|---|-------|------|-------|-------------|--------------------------------|
| 1 | Transaction unique identifier | String (GUID-style) | — | Reference generated automatically, recording each published sale | Unique alphanumeric (often a brace-wrapped GUID). Not a stable property key — changes if a record is updated. Not null |
| 2 | Price | Integer | GBP (£) | Sale price stated on the transfer deed | Positive integer. Not null |
| 3 | Date of Transfer | DateTime | — | Date the sale was completed, as stated on the transfer deed | Format `YYYY-MM-DD HH:MM`; time component typically `00:00`. Not null |
| 4 | Postcode | String | — | Postcode used at the time of the original transaction | UK postcode format; **may be blank** if not recorded |
| 5 | Property Type | Character (enum) | — | Built form of the property | `D`=Detached, `S`=Semi-detached, `T`=Terraced, `F`=Flats/Maisonettes, `O`=Other |
| 6 | Old/New | Character (enum) | — | Whether newly built or established | `Y`=newly built, `N`=established residential building |
| 7 | Duration | Character (enum) | — | Tenure | `F`=Freehold, `L`=Leasehold. (Note: HMLR does not record leases of 7 years or less) |
| 8 | PAON | String | — | Primary Addressable Object Name — typically the house number or name | Alphanumeric; may be blank |
| 9 | SAON | String | — | Secondary Addressable Object Name — identifies a unit/flat within a PAON | Alphanumeric; may be blank |
| 10 | Street | String | — | Street name | Text; may be blank |
| 11 | Locality | String | — | Smaller place identifier within a town/area | Text; may be blank |
| 12 | Town/City | String | — | Primary location identifier | Text; may be blank |
| 13 | District | String | — | Local administrative district | Text; may be blank |
| 14 | County | String | — | County | Text; may be blank |
| 15 | PPD Category Type | Character (enum) | — | Type of Price Paid transaction | `A`=Standard price-paid entry (single residential sold for value at full market value); `B`=Additional price-paid entry (e.g. repossessions, buy-to-lets, transfers under power of sale) |
| 16 | Record Status — monthly file only | Character (enum) | — | Indicates the change type in monthly update files | `A`=Addition, `C`=Change, `D`=Delete. Present in monthly-update files; the full single-file dataset is all additions |

> Verification note: all 16 rows above are verified from the official field-specification guidance. The exact internal format of field #1 (GUID braces) and the always-`00:00` time component of field #3 are conventions observed in HMLR's published examples; treat those formatting sub-details as **indicative**, not contractually guaranteed.

---

## Datasheet for Datasets

**Motivation.** Created by HM Land Registry to provide an authoritative, transparent public record of property sale prices in England & Wales. It supports market transparency, research, valuation, policy analysis, and consumer information services. It is open government data, not produced for a single for-profit beneficiary.

**Composition.** Each record represents a single property sale transaction lodged for registration. Instances include the sale price, completion date, address components, property type, tenure, new/old status, and transaction category. The dataset covers all qualifying sales "sold for value" from 1995-01-01 onward. It does **not** include: sales not lodged for registration, transfers not for value (e.g. gifts), "right to buy" at a discount, compulsory purchases, or leases of 7 years or less. Addresses are public-register data; there are no explicit personal-identity fields (no buyer/seller names, no demographics), though an address can in principle be linked to occupants by third parties — handle with the PII caveat below.

**Collection process.** Data originates from property transfer deeds lodged with HM Land Registry for registration. It is a byproduct of the statutory land-registration process (administrative/registry data), not a survey or sample — it is intended to be a near-complete population of qualifying transactions.

**Preprocessing / cleaning.** HM Land Registry assembles records from registration data. Monthly files carry Record Status flags (A/C/D) reflecting corrections/deletions over time; consumers should apply changes to keep a synchronized copy. Some address components may be blank. The Transaction unique identifier is regenerated when a record changes, so it is not a durable join key.

**Uses.** Property market analysis, house-price indices, academic and policy research, valuation tooling, and residential property price information services. **Out of scope / requires care:** using the address fields commercially beyond price-information services (Royal Mail/OS third-party rights), and any attempt to re-identify individuals at an address.

**Distribution.** Published openly by HM Land Registry on gov.uk as downloadable CSV files (full file and monthly updates), plus a SPARQL/Linked-Data endpoint. Released under OGL v3.0. This datasheet does not redistribute the data — only its documentation.

**Maintenance.** Maintained by HM Land Registry; refreshed on the 20th working day each month. Errors/queries are handled through HM Land Registry's published channels. The schema has been stable, with PPD Category Type added in earlier revisions.

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
  "name": "HM Land Registry Price Paid Data",
  "description": "Public register of property sales in England and Wales sold for value and lodged for registration, from 1 January 1995 onwards. Published by HM Land Registry under the Open Government Licence v3.0.",
  "url": "https://www.gov.uk/government/statistical-data-sets/price-paid-data-downloads",
  "sameAs": "https://www.gov.uk/guidance/about-the-price-paid-data",
  "license": "http://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/",
  "creator": {
    "@type": "Organization",
    "name": "HM Land Registry",
    "url": "https://www.gov.uk/government/organisations/land-registry"
  },
  "datePublished": "1995-01-01",
  "creditText": "Contains HM Land Registry data © Crown copyright and database right 2026. Licensed under the Open Government Licence v3.0.",
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "ppd-csv",
      "name": "price-paid-data.csv",
      "description": "Headerless CSV, 16 columns, one row per transaction.",
      "encodingFormat": "text/csv"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "transactions",
      "name": "transactions",
      "field": [
        { "@type": "cr:Field", "@id": "transactions/price", "name": "Price", "dataType": "sc:Integer", "description": "Sale price in GBP from the transfer deed." },
        { "@type": "cr:Field", "@id": "transactions/date_of_transfer", "name": "Date of Transfer", "dataType": "sc:Date", "description": "Completion date of the sale." },
        { "@type": "cr:Field", "@id": "transactions/postcode", "name": "Postcode", "dataType": "sc:Text", "description": "Postcode at time of transaction; may be blank." },
        { "@type": "cr:Field", "@id": "transactions/property_type", "name": "Property Type", "dataType": "sc:Text", "description": "Enum: D, S, T, F, O." },
        { "@type": "cr:Field", "@id": "transactions/duration", "name": "Duration", "dataType": "sc:Text", "description": "Tenure enum: F (Freehold), L (Leasehold)." }
      ]
    }
  ]
}
```

---

## Validation script

The script below validates the **structure** of a Price Paid Data CSV file that the user already has locally. It does **not** download, host, or transmit the dataset; it only inspects a file path the user supplies, and it streams (does not load the whole file into memory). Documentation only.

```python
#!/usr/bin/env python3
"""Validate the STRUCTURE of an HM Land Registry Price Paid Data CSV.

This script does NOT download, host, mirror, or republish any data.
Point it at a file you already obtained from gov.uk under OGL v3.0.

Usage: python validate_ppd.py /path/to/pp-complete.csv
"""
import csv
import sys

EXPECTED_COLS = 16  # PPD CSV is headerless, 16 columns
PROPERTY_TYPE = {"D", "S", "T", "F", "O"}
OLD_NEW = {"Y", "N"}
DURATION = {"F", "L"}
PPD_CATEGORY = {"A", "B"}
RECORD_STATUS = {"A", "C", "D"}  # monthly files only


def validate(path: str) -> int:
    errors = 0
    rows = 0
    with open(path, newline="", encoding="utf-8") as fh:
        reader = csv.reader(fh)
        for i, row in enumerate(reader, start=1):
            rows += 1
            if len(row) != EXPECTED_COLS:
                print(f"row {i}: expected {EXPECTED_COLS} cols, got {len(row)}")
                errors += 1
                continue
            (_id, price, _date, _pc, ptype, oldnew, dur,
             _paon, _saon, _st, _loc, _town, _dist, _cnty, ppd, status) = row
            if not price.isdigit():
                print(f"row {i}: price not an integer: {price!r}"); errors += 1
            if ptype and ptype not in PROPERTY_TYPE:
                print(f"row {i}: bad Property Type {ptype!r}"); errors += 1
            if oldnew and oldnew not in OLD_NEW:
                print(f"row {i}: bad Old/New {oldnew!r}"); errors += 1
            if dur and dur not in DURATION:
                print(f"row {i}: bad Duration {dur!r}"); errors += 1
            if ppd and ppd not in PPD_CATEGORY:
                print(f"row {i}: bad PPD Category {ppd!r}"); errors += 1
            if status and status not in RECORD_STATUS:
                print(f"row {i}: bad Record Status {status!r}"); errors += 1
            if i >= 1000:  # bounded sample: inspect at most 1000 rows
                break
    print(f"checked {min(rows, 1000)} rows; {errors} structural issue(s)")
    return 1 if errors else 0


if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__); sys.exit(2)
    sys.exit(validate(sys.argv[1]))
```

**Data-quality checks performed by the script:** column count == 16, `Price` is a positive integer, and enumerated fields (Property Type, Old/New, Duration, PPD Category Type, Record Status) contain only documented codes. Blank address fields are tolerated as valid nulls. The check is bounded to the first 1000 rows (local-only, ephemeral) per the bounded-access protocol.

---

## Limitations & gaps

- **Documentation only:** no actual data was downloaded, sampled, mirrored, or committed as part of this deed. The data dictionary and codes were verified from HM Land Registry's official guidance pages, **not** from a data sample.
- **Third-party address rights (unresolved here):** the OGL v3.0 derivative grant is confirmed for the dataset, but the Royal Mail / Ordnance Survey carve-out on address components is a real constraint for downstream commercial address use and was **not** independently cleared in this datasheet.
- **PII context:** the dataset has no explicit personal-identity fields, but address + price are public-register data that a third party could link to occupants. Treat re-identification as out of scope and a misuse.
- **Formatting sub-details indicative:** the GUID-brace format of the Transaction unique identifier and the always-`00:00` time component of Date of Transfer are observed conventions, not guaranteed by the spec.
- **Croissant record is minimal:** it includes a representative subset of field stubs, not all 16 columns, and has not been run through a Croissant validator in this environment.
- **Licence text not embedded/hashed here:** this datasheet cites the canonical OGL v3.0 URL rather than embedding a hashed snapshot; a reuser should archive and hash the licence text against their specific data vintage.
- **No live row-count verification:** the validation script documents expected structure but was not executed against real data (by design).
