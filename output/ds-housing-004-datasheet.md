# Datasheet — UK House Price Index (UK HPI)

One-line summary: A monthly aggregated index and average-price series tracking changes in residential property values across the UK (countries, regions, and local authorities), published by HM Land Registry with ONS.

_This datasheet (the document you are reading) is licensed under **CC-BY-4.0**. It is documentation only: it does not host, mirror, transform, or republish any of the underlying dataset._

---

## Provenance & attribution

- **Dataset title:** UK House Price Index (UK HPI)
- **Publisher / producer:** HM Land Registry (in partnership with the Office for National Statistics, Registers of Scotland, and Land & Property Services Northern Ireland)
- **Source / landing page:** https://www.gov.uk/government/collections/uk-house-price-index-reports
- **Methodology page:** https://www.gov.uk/government/publications/about-the-uk-house-price-index/about-the-uk-house-price-index
- **Catalog id (candidate):** cat-housing-004
- **Retrieval date:** 2026-06-28
- **Required attribution string:**
  > Contains HM Land Registry data © Crown copyright and database right 2026. This data is licensed under the Open Government Licence v3.0.

  (The generic OGL fallback attribution, usable where a provider statement is absent, is: "Contains public sector information licensed under the Open Government Licence v3.0.")

## Source licence

- **Licence:** Open Government Licence (OGL) v3.0.
- **Licence URL:** https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/
- **Stated on source page:** The collection page states "All content is available under the Open Government Licence v3.0, except where otherwise stated."
- **Derivatives permitted — verified:** YES. The OGL v3.0 "You are free to" section explicitly grants the right to **"adapt the Information"** and to "copy, publish, distribute and transmit the Information" and "exploit the Information commercially and non-commercially for example, by combining it with other Information, or by including it in your own product or application." Adapting + distributing = derivative works are permitted, subject to the attribution requirement above.
- **Licence text snapshot:** Archive a copy of the licence text from the National Archives URL above at retrieval time and record its hash alongside this datasheet (e.g. `sha256sum ogl-v3.0.txt`). The snapshot/hash is stored as the per-dataset gate artifact; it is not reproduced here to keep this file documentation-only.

> Note: gov.uk also flags that re-publishing the *data* may require agreeing to terms in the "About the UK House Price Index" guidance before download. This datasheet performs no download or republication, so those re-use conditions are satisfied by construction; downstream re-publishers must review them.

## Data dictionary

Fields below are confirmed from the official methodology page, Section 8.2 ("CSV column headers and definitions"). The dataset is wide: most metrics repeat across property-type, buyer-status, funding-status, and property-status breakdowns. Representative core fields and the repeating field families are documented; individual breakdown columns follow the documented `[Prefix]Metric` naming pattern.

| Field | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| `Date` | date (YYYY-MM-DD, first of month) | calendar month | Year and month the monthly statistics apply to | Monthly periods; non-null |
| `RegionName` | string | — | Name of geography (Country, Region, County/Unitary/District Authority, London Borough) | Controlled geography names; non-null |
| `AreaCode` | string (ONS GSS code) | — | Code of geography matching `RegionName` | e.g. `E92000001`; non-null |
| `AveragePrice` | number | GBP (£) | Average house price for the geography in the period | Null where insufficient transactions |
| `Index` | number | index (Jan 2015 = 100) | House price index for the geography in the period | Baseline 100 = Jan 2015 |
| `IndexSA` | number | index (Jan 2015 = 100) | Seasonally adjusted index (published at national/regional level only) | Null where SA not produced |
| `AveragePriceSA` | number | GBP (£) | Seasonally adjusted average price | Null where SA not produced |
| `1m%Change` | number | percent | Month-on-month % change in average price | May be null at series start |
| `12m%Change` | number | percent | % change in average price vs. same month 12 months earlier | Null for first 12 months of a series |
| `SalesVolume` | integer | count of transactions | Number of registered transactions for the geography in the period | Lags ~2 months; null/blank for most recent months pending registration |
| `DetachedPrice`, `SemiDetachedPrice`, `TerracedPrice`, `FlatPrice` | number | GBP (£) | Average price by property type | Null where insufficient data |
| `DetachedIndex`, `SemiDetachedIndex`, `TerracedIndex`, `FlatIndex` | number | index (Jan 2015 = 100) | Index by property type (each also has `1m%Change` / `12m%Change`) | As above |
| `CashPrice`, `MortgagePrice` | number | GBP (£) | Average price by funding status | Null where insufficient data |
| `CashIndex`, `MortgageIndex` | number | index (Jan 2015 = 100) | Index by funding status | As above |
| `CashSalesVolume`, `MortgageSalesVolume` | integer | count | Sales volume by funding status | Null pending registration |
| `FTBPrice`, `FOOPrice` | number | GBP (£) | Average price by buyer status (First-Time Buyer / Former Owner Occupier) | Null where insufficient data |
| `FTBIndex`, `FOOIndex` | number | index (Jan 2015 = 100) | Index by buyer status | As above |
| `NewPrice`, `OldPrice` | number | GBP (£) | Average price by property status (new build / existing resold) | Null where insufficient data |
| `NewIndex`, `OldIndex` | number | index (Jan 2015 = 100) | Index by property status | As above |
| `NewSalesVolume`, `OldSalesVolume` | integer | count | Sales volume by property status | Null pending registration |

Unverified / to confirm against an actual header row:
- **Exact column header spelling/casing** (e.g. `1m%Change` vs `1m%change`, presence of spaces such as `Sales Volume` vs `SalesVolume`) — _UNVERIFIED_: the methodology table uses human-readable labels; confirm against a live CSV header before machine parsing.
- **Full enumerated list of breakdown columns and their ordering** — _UNVERIFIED_: only the repeating field families are documented here; the full wide schema should be enumerated from a header read.

No personal or identifying fields are present or documented: all values are aggregated to geography level. No bounded-access sample was taken (none required to document structure from published methodology).

## Datasheet for Datasets

- **Motivation:** Created to provide an authoritative, official measure of UK residential property price change for policymakers, analysts, lenders, researchers, and the public. Funded and produced by HM Land Registry / ONS as part of UK official statistics.
- **Composition:** Aggregated time series of average prices and indices (no individual transactions or persons). Instances are (geography × month) rows with price/index/volume metrics, broken down by property type, buyer status, funding status, and property status. Coverage: England & Wales from Jan 1995, Scotland from Jan 2004, Northern Ireland from Jan 2005 (quarterly). Geographies: country, region, county/unitary/district authority, and London borough.
- **Collection process:** Built from property transaction data sourced from HM Land Registry / Registers of Scotland / LPS NI and HMRC. Uses a repeat-sales/hedonic regression approach with imputation; revised over a ~13-estimate revision cycle as more registrations arrive. Imputation methods updated (notably Aug 2025) to improve early estimates for new builds.
- **Preprocessing / cleaning:** Transactions are filtered, deduplicated, and modelled; figures are revised as late registrations arrive. Seasonally adjusted series are derived for higher-level geographies. Most-recent-months figures (esp. sales volumes) are provisional.
- **Uses:** Macroeconomic and housing-market analysis, affordability studies, regional comparison, indexation. Not suitable for valuing an individual property or for inferring anything about identifiable persons. Provisional recent months should be used with caution.
- **Distribution:** Published openly on gov.uk as downloadable CSV and online reports under OGL v3.0; free to access. This datasheet does not redistribute the data.
- **Maintenance:** Maintained and updated monthly by HM Land Registry (NI quarterly), typically the second/third Wednesday of the month, with ongoing revisions. Methodology changes are announced on the about/methodology page.

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "dct": "http://purl.org/dc/terms/"
  },
  "@type": "Dataset",
  "name": "UK House Price Index (UK HPI)",
  "description": "Monthly index and average-price series tracking changes in UK residential property values by country, region, and local authority, with breakdowns by property type, buyer status, funding status, and property status. Published by HM Land Registry with ONS.",
  "url": "https://www.gov.uk/government/collections/uk-house-price-index-reports",
  "sameAs": "https://www.gov.uk/government/publications/about-the-uk-house-price-index/about-the-uk-house-price-index",
  "license": "https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/",
  "creator": {
    "@type": "Organization",
    "name": "HM Land Registry",
    "url": "https://www.gov.uk/government/organisations/land-registry"
  },
  "publisher": {
    "@type": "Organization",
    "name": "HM Land Registry"
  },
  "datePublished": "1996-01-01",
  "dateModified": "2026-06-28",
  "creditText": "Contains HM Land Registry data © Crown copyright and database right 2026, licensed under the Open Government Licence v3.0.",
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "uk-hpi-csv",
      "name": "UK HPI full dataset (CSV)",
      "description": "Official downloadable CSV from gov.uk; not mirrored by this datasheet.",
      "encodingFormat": "text/csv",
      "contentUrl": "https://www.gov.uk/government/collections/uk-house-price-index-reports"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "uk-hpi-records",
      "name": "uk-hpi-records",
      "field": [
        {"@type": "cr:Field", "@id": "uk-hpi-records/Date", "name": "Date", "description": "Month the statistics apply to", "dataType": "sc:Date"},
        {"@type": "cr:Field", "@id": "uk-hpi-records/RegionName", "name": "RegionName", "description": "Name of geography", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "uk-hpi-records/AreaCode", "name": "AreaCode", "description": "ONS GSS geography code", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "uk-hpi-records/AveragePrice", "name": "AveragePrice", "description": "Average house price (GBP)", "dataType": "sc:Float"},
        {"@type": "cr:Field", "@id": "uk-hpi-records/Index", "name": "Index", "description": "House price index (Jan 2015 = 100)", "dataType": "sc:Float"},
        {"@type": "cr:Field", "@id": "uk-hpi-records/SalesVolume", "name": "SalesVolume", "description": "Count of registered transactions", "dataType": "sc:Integer"}
      ]
    }
  ]
}
```

## Validation script

This script validates the structure of a UK HPI CSV that the user has already obtained from the official source. It does **not** download, host, or redistribute the data — supply a local path to a file you fetched yourself.

```python
#!/usr/bin/env python3
"""Structure check for a locally-obtained UK House Price Index CSV.
Documentation/validation only. Does NOT download or host any data.
Usage: python validate_uk_hpi.py path/to/uk-hpi-local.csv
"""
import csv
import sys

# Core columns we expect from the methodology (Section 8.2).
# Header spelling/casing is marked UNVERIFIED in the datasheet; compare
# case-insensitively and report rather than hard-fail on naming variants.
EXPECTED_CORE = ["Date", "RegionName", "AreaCode", "AveragePrice", "Index", "SalesVolume"]

def main(path):
    with open(path, newline="", encoding="utf-8-sig") as f:
        reader = csv.reader(f)
        header = next(reader, None)
        if not header:
            print("FAIL: empty file / no header")
            return 1
        norm = {h.strip().lower().replace(" ", "") for h in header}
        missing = [c for c in EXPECTED_CORE if c.lower() not in norm]
        rows = sum(1 for _ in reader)

    print(f"Columns found : {len(header)}")
    print(f"Data rows     : {rows}")
    if missing:
        print(f"WARN: expected core columns not matched: {missing}")
    else:
        print("OK: all expected core columns present")
    # Sanity: national series should have many monthly rows (>300 since 1995).
    if rows < 100:
        print(f"WARN: row count {rows} lower than expected for a full series")
    return 0 if not missing else 2

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__); sys.exit(64)
    sys.exit(main(sys.argv[1]))
```

Expected-structure summary for a data-quality report: a full national-level series should contain hundreds of monthly rows (England & Wales since Jan 1995); `Index` values are anchored at 100 for Jan 2015; `AveragePrice` is positive GBP; recent-month `SalesVolume` may be null/provisional.

## Limitations & gaps

- **Header naming UNVERIFIED:** exact CSV column spelling, casing, spacing, and the complete enumerated set/order of breakdown columns were not confirmed against a live header row — they are documented from the published methodology table (Section 8.2). Confirm before automated parsing.
- **No sample taken:** no rows were downloaded or sampled; field types and null behaviour are inferred from documentation, not observed data.
- **Provisional/revised data:** recent months and sales volumes are provisional and revised over a ~13-estimate cycle; methodology (incl. imputation) changes over time.
- **Coverage variance:** start dates and SA availability differ by nation/geography level; Northern Ireland is quarterly.
- **Re-use terms:** gov.uk references additional data re-publishing terms in the "About" guidance; this datasheet does not republish data, but downstream republishers must review those terms in addition to OGL v3.0.
- **No PII:** the dataset is fully aggregated; no personal/identifying data was documented or sampled.
