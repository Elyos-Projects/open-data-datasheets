# Datasheet: Spending over £25,000 (UK departmental transparency)

One-line summary: Monthly line-item records of UK central-government departmental
expenditure where the transaction value exceeds £25,000, published as open data under
the UK transparency programme.

_This datasheet is documentation only. It does not host, mirror, transform, or
republish the underlying dataset. This datasheet (the document you are reading) is
licensed under **CC-BY-4.0**._

---

## Provenance & attribution

- **Publisher:** HM Revenue & Customs (HMRC), a UK central-government department,
  publishing via the UK Government transparency programme (data.gov.uk / GOV.UK).
  From 1 April 2026 the collection also integrates Valuation Office Agency (VOA) data.
- **Source URL (documentation/collection page):**
  https://www.gov.uk/government/collections/spending-over-25-000
- **Retrieval date:** 2026-06-28
- **Catalog id (candidate):** cat-budget-001
- **Required attribution string (per OGL v3.0):**
  > Contains public sector information licensed under the Open Government Licence v3.0.

  Where a more specific provider statement is available, attribute as: "Source: HM
  Revenue & Customs, licensed under the Open Government Licence v3.0."

---

## Source licence

- **Licence:** Open Government Licence v3.0 (OGL v3.0).
- **Licence URL:** https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/
- **Statement on the source page (retrieved 2026-06-28):** "All content is available
  under the Open Government Licence v3.0".
- **Derivatives permitted — VERIFIED.** OGL v3.0 grants the licensee the rights to:
  - "copy, publish, distribute and transmit the Information";
  - "**adapt the Information**"; and
  - "exploit the Information commercially and non-commercially for example, by
    combining it with other Information, or by including it in your own product or
    application".

  The explicit "adapt the Information" right plus the "combining / including in your
  own product" right confirm that derivative works are permitted. The only mandatory
  condition is attribution (see above).
- **Licence snapshot note:** The canonical, archivable licence text is hosted at The
  National Archives URL above. This datasheet records the licence identity, the
  governing URL, and the verified clause text in lieu of committing a copy of the
  licence body (to keep this deliverable documentation-only). Reviewers archiving a
  hash should snapshot the National Archives OGL v3.0 page.

---

## Data dictionary

Fields below are derived from the HMRC collection/documentation page (the canonical
UK transparency spending schema). Individual monthly CSVs may vary slightly in column
naming and may include additional administrative columns; rows marked **UNVERIFIED**
were not confirmed against a specific file's header during this documentation pass
(per the bounded-access / no-sampling guardrail).

| Field | Type | Units | Description | Allowed values / null handling |
|-------|------|-------|-------------|-------------------------------|
| Payment Date | date | calendar date | Date the expense posting cleared to the Trade Creditor account | Date (typically DD/MM/YYYY). Nulls not expected for posted lines. |
| Supplier / Recipient | string | n/a | Name of the vendor or body receiving payment | Free text organisation/recipient name. May be redacted/blank where withheld. |
| Amount | decimal | GBP (£), VAT-inclusive | Invoice amount; positive for invoices, negative for credit notes; inclusive of VAT | Signed decimal. Line value may fall below £25,000 when one invoice is split across multiple expense types. |
| Expense Type | string | n/a | Material Group description from HMRC's ERP system — the finest level at which a commercial purchase is described | Controlled ERP material-group descriptions (free-text label). |
| Expense Area | string | n/a | Categorisation for transactions split across multiple codes / business area | Departmental expense-area label. |
| Transaction Number / Reference | string | n/a | Identifier for the payment/transaction line | **UNVERIFIED** — common in the standard transparency schema but not explicitly confirmed on the source page. |
| VAT Registration Number | string | n/a | Supplier VAT number (standard transparency field) | **UNVERIFIED** — part of the Cabinet Office standard but not confirmed on this page; may be absent. |
| Department / Entity | string | n/a | Reporting body (HMRC; VOA from Apr 2026) | **UNVERIFIED** — may be implicit in file scope rather than a column. |

PII note: documented fields describe organisational suppliers and accounting
categories. No personal/identifying individual-level fields are documented or sampled.
Supplier names occasionally relate to sole traders; consumers should treat the
"Supplier / Recipient" column with care but no personal data is reproduced here.

---

## Datasheet for Datasets

**Motivation.** Created to meet the UK Government's transparency commitment to publish
all central-government spending transactions over £25,000, enabling public scrutiny of
how public money is spent. Maintained by the publishing department (HMRC).

**Composition.** Each record is a line item of departmental expenditure above the
£25,000 threshold (split lines may individually fall below it). Instances describe a
payment: date, supplier/recipient, amount (VAT-inclusive), and expense
type/area. Files are monthly. The collection spans September 2013 through April 2026
(and ongoing), one CSV per reporting month.

**Collection process.** Data is extracted from the department's Enterprise Resource
Planning (ERP)/finance system. "Payment Date" reflects when a posting cleared to the
Trade Creditor account. Amounts are taken as recorded in the accounting system,
inclusive of VAT, with credit notes as negative values.

**Preprocessing / cleaning.** Lines are filtered/aggregated to the transparency
threshold and coded to ERP material groups (Expense Type) and expense areas. Single
invoices may be split across multiple expense-type codes, producing sub-threshold line
amounts. No further cleaning is documented; consumers should expect raw accounting
categorisations.

**Uses.** Public accountability, spend analysis, supplier/market analysis, journalism,
and academic research. Suitable for derivative analytical products under OGL v3.0.
Not an authoritative audited financial statement; figures are operational accounting
extracts and should not be treated as final accounts.

**Distribution.** Published openly on GOV.UK / data.gov.uk as downloadable monthly CSV
files, free of charge, under OGL v3.0. No login or fee required.

**Maintenance.** Maintained by HMRC; new monthly files are published roughly 28-31 days
after the reporting month. From 1 April 2026 VOA data is integrated into the same
collection. Corrections are issued via re-publication of monthly files.

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
  "name": "Spending over £25,000 (UK departmental transparency) — HMRC",
  "description": "Monthly line-item records of HM Revenue & Customs departmental spending where the transaction value exceeds £25,000, published under the UK Government transparency programme. Documentation datasheet only; data not hosted here.",
  "url": "https://www.gov.uk/government/collections/spending-over-25-000",
  "sameAs": "https://www.gov.uk/government/collections/spending-over-25-000",
  "license": "https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/",
  "creator": {
    "@type": "GovernmentOrganization",
    "name": "HM Revenue & Customs",
    "url": "https://www.gov.uk/government/organisations/hm-revenue-customs"
  },
  "publisher": {
    "@type": "Organization",
    "name": "GOV.UK / data.gov.uk"
  },
  "datePublished": "2013-09-01",
  "isAccessibleForFree": true,
  "keywords": ["public spending", "government transparency", "open data", "OGL", "HMRC"],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "spending_line_items",
      "field": [
        { "@type": "cr:Field", "name": "payment_date", "description": "Date the posting cleared to the Trade Creditor account", "dataType": "sc:Date" },
        { "@type": "cr:Field", "name": "supplier", "description": "Vendor or recipient receiving payment", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "amount_gbp", "description": "Invoice amount in GBP, VAT-inclusive; negative for credit notes", "dataType": "sc:Float" },
        { "@type": "cr:Field", "name": "expense_type", "description": "ERP material-group description", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "expense_area", "description": "Expense-area categorisation", "dataType": "sc:Text" }
      ]
    }
  ]
}
```

---

## Validation script

This script validates the structure of a monthly CSV that a user has **already
obtained themselves** from the official source. It does **not** download, host, or
republish any data — it only inspects a local file the user supplies.

```python
#!/usr/bin/env python3
"""Validate a locally-obtained 'Spending over £25,000' monthly CSV.

Documentation aid only. This script does NOT download or host any data.
Point it at a CSV you have already downloaded from:
  https://www.gov.uk/government/collections/spending-over-25-000
Usage: python validate.py path/to/monthly_spend.csv
"""
import csv
import sys

# Core expected columns (names vary by file; matched case-insensitively, substring).
EXPECTED = ["date", "amount", "expense type", "expense area"]
SUPPLIER_HINTS = ["supplier", "recipient", "vendor"]

def norm(s: str) -> str:
    return s.strip().lower()

def main(path: str) -> int:
    with open(path, newline="", encoding="utf-8-sig") as fh:
        reader = csv.reader(fh)
        try:
            header = [norm(h) for h in next(reader)]
        except StopIteration:
            print("FAIL: file is empty"); return 1

        missing = [c for c in EXPECTED if not any(c in h for h in header)]
        has_supplier = any(any(s in h for s in SUPPLIER_HINTS) for h in header)
        if not has_supplier:
            missing.append("supplier/recipient")

        rows = sum(1 for _ in reader)

    print(f"Columns found ({len(header)}): {header}")
    print(f"Data rows: {rows}")
    if missing:
        print(f"FAIL: missing expected column(s): {missing}")
        return 1
    if rows < 1:
        print("FAIL: no data rows")
        return 1
    print("OK: structure looks consistent with the transparency spending schema")
    return 0

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__); sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

Expected quick checks: a valid monthly file has at minimum a date column, an
amount column, a supplier/recipient column, and expense type/area columns, and at
least one data row. Amounts should parse as signed decimals (negatives are credit
notes).

---

## Limitations & gaps

- **Field list is partially unverified.** The data dictionary fields confirmed from the
  collection page are Payment Date, Supplier/Recipient, Amount, Expense Type, and
  Expense Area. Common standard-schema fields (Transaction Number, VAT Registration
  Number, Department/Entity) are marked **UNVERIFIED** — they appear in the wider
  Cabinet Office transparency standard but were not confirmed against a specific file
  header here, in keeping with the no-sampling / bounded-access guardrail.
- **No data was sampled, downloaded, or inspected** to produce this datasheet; column
  types/units are inferred from the documentation page, not measured from a file.
- **Per-department variation.** Column names, ordering, and date formats differ between
  months and (post-April 2026) between HMRC and integrated VOA data. Validate each file
  individually.
- **Threshold nuance.** Individual line amounts can be below £25,000 where one invoice
  is split across multiple expense codes; do not filter on amount >= 25000 to reconstruct
  the dataset.
- **Not audited accounts.** Figures are operational accounting extracts (VAT-inclusive)
  and are not a substitute for the department's audited financial statements.
- **Licence archival.** This deliverable records the OGL v3.0 identity, URL, and verified
  clause text but intentionally does not commit a copy/hash of the licence body; a
  reviewer wanting a snapshot should archive the National Archives OGL v3.0 page.
