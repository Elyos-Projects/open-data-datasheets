# Datasheet: USDA FoodData Central

**One-line summary:** A documentation datasheet for FoodData Central (FDC), the USDA's authoritative integrated food-composition database, widely reused in nutrition apps and research.

*This datasheet (the document you are reading) is licensed under **CC-BY-4.0**. It is documentation only: it does not host, mirror, transform, or republish any FoodData Central data.*

---

## Provenance & attribution

| Field | Value |
|---|---|
| Dataset name | FoodData Central (FDC) |
| Publisher | U.S. Department of Agriculture (USDA), Agricultural Research Service (ARS) |
| Source URL | https://fdc.nal.usda.gov/ |
| Downloads page | https://fdc.nal.usda.gov/download-datasets/ |
| Catalog id (candidate) | cat-agri-003 |
| Retrieval date | 2026-06-28 |
| Required attribution | Not legally required (public domain). Requested citation: *U.S. Department of Agriculture, Agricultural Research Service. FoodData Central, [year]. fdc.nal.usda.gov.* |

---

## Source licence

**Verified licence: CC0 1.0 Universal (Public Domain Dedication).**

The source page states verbatim:

> "USDA FoodData Central data are in the public domain and they are not copyrighted."

It further indicates the data permit unrestricted use, **including derivatives and reuse**, with no permission required, though users are *requested* (not required) to cite FoodData Central as the source.

- Licence reference URL: https://creativecommons.org/publicdomain/zero/1.0/
- Confirming source: https://fdc.nal.usda.gov/ (FoodData Central home / usage statement), retrieved 2026-06-28
- US-government works are additionally not subject to domestic copyright (17 U.S.C. § 105).

**Derivatives permitted: YES (verified).** CC0 / US-gov public domain places no restriction on creating derivative works. This datasheet is therefore not marked DRAFT.

**Licence snapshot note:** Per acceptance criteria, a hash + archived copy of the licence text should be attached as a per-dataset gate artifact at the governance gate. The canonical CC0 legal text is at the URL above; this datasheet records the licence determination but does not embed the data or a binary archive.

---

## Data dictionary

FoodData Central is distributed as a set of relational CSV/JSON tables (CSV = comma-delimited ASCII; JSON also offered. MS Access discontinued Oct 2021). Field-level definitions are published by USDA in the **"Download Field Descriptions"** document (cited below), which is included inside each download bundle.

- Authoritative field reference: `https://www.usda.gov/docs/Download_Field_Descriptions_Oct2020.pdf` (referenced from the FDC Downloads page, retrieved 2026-06-28).

**Verification status:** The *table-category structure* below was confirmed from the FDC documentation pages (home, Data Documentation, Foundation Foods Documentation, Downloads). Individual column names/types marked **(unverified — field-level)** are drawn from the table categories the docs describe but could not be confirmed line-by-line because the official Field Descriptions PDF did not render during retrieval; they must be reconciled against that PDF at the gate before being treated as authoritative.

### Confirmed table categories (from FDC documentation)

| Category | Confirmed contents (verbatim/paraphrased from docs) | Verified |
|---|---|---|
| Food Descriptions | food name, brand, characteristics (e.g. raw/cooked), scientific/common names, food groups, refuse amounts, conversion factors, FDC_ID | Yes (category-level) |
| Nutrient Data | nutrient values organized as proximates, energy, minerals, vitamins, lipid components; analytical source details; per-100g basis; LOQ (Limit of Quantification) field | Yes (category-level) |
| Weights / Portions | portion sizes in grams for edible material | Yes (category-level) |

### Field-level dictionary (to be reconciled with the official PDF)

| Table | Field | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|---|
| food | fdc_id | integer | — | Unique identifier for a food item (confirmed: docs reference "FDC_ID numbers") | Verified key; not null |
| food | description | string | — | Name/description of the food | (unverified — field-level) |
| food | data_type | string | — | Source data type (foundation_food, sr_legacy_food, survey_fndds_food, branded_food, experimental_food) | enum confirmed at dataset level |
| food | food_category_id | integer | — | FK to food_category | (unverified — field-level) |
| food | publication_date | date | — | Date the record was published | (unverified — field-level) |
| nutrient | id | integer | — | Unique nutrient identifier | (unverified — field-level) |
| nutrient | name | string | — | Nutrient name (e.g. Protein, Energy) | (unverified — field-level) |
| nutrient | unit_name | string | g, mg, µg, kcal, kJ | Measurement unit for the nutrient | (unverified — field-level) |
| food_nutrient | fdc_id | integer | — | FK to food | (unverified — field-level) |
| food_nutrient | nutrient_id | integer | — | FK to nutrient | (unverified — field-level) |
| food_nutrient | amount | number | per 100 g | Nutrient amount per 100 g of food (per-100g basis confirmed in docs) | nullable when not analyzed |
| food_nutrient | loq | number | per 100 g | Limit of Quantification — lowest quantifiable measure (field addition confirmed in docs) | nullable |
| food_category | id / code / description | int/string | — | Food grouping categories (food groups confirmed in docs) | (unverified — field-level) |
| measure_unit | id / name | int/string | — | Portion measurement units; portions given in grams (confirmed in docs) | (unverified — field-level) |
| branded_food | brand_owner, gtin_upc, ingredients, serving_size, serving_size_unit | string/number | g, ml | Commercial label data from public-private partnership (branded set confirmed in docs) | (unverified — field-level) |

No personal or identifying fields are present or documented (FDC describes foods and their nutrient composition, not individuals).

---

## Datasheet for Datasets

**Motivation.** Created and maintained by USDA ARS to provide an authoritative, integrated source of food and nutrient composition data for research, nutrition policy, food labeling, and public/commercial applications. It consolidates multiple legacy USDA datasets into one platform.

**Composition.** Multiple data types: Foundation Foods (analytical data on commodity/minimally processed samples), SR Legacy (historical analyses and literature, final update 2018), Survey Foods / FNDDS (for What We Eat in America, NHANES), Experimental Foods (peer-reviewed collaborative studies), and Branded Foods (commercial label data via public-private partnership). Instances are foods, each linked to nutrient values (per 100 g) and portion weights. No human-subject records.

**Collection process.** Foundation/Experimental data come from laboratory analytical measurement of food samples; SR Legacy from historical analyses and published literature; Branded Foods from manufacturer/retailer label data submitted through a partnership; Survey foods from dietary-survey nutrient databases. Update cadences differ (Foundation/Experimental twice-yearly, Branded monthly, FNDDS every ~2 years, SR Legacy frozen at 2018).

**Preprocessing / cleaning / labeling.** USDA harmonizes records into a relational schema (food, nutrient, food_nutrient, weights, categories). Nutrient amounts are normalized to a per-100-g basis; an LOQ field indicates the lowest quantifiable measurement. Analytical source/provenance details are retained per record.

**Uses.** Nutrition research, dietary assessment, food labeling, app/product development, public-health policy. Caution: data types differ in method and recency (e.g. Branded label data is self-reported by manufacturers; SR Legacy is no longer updated), so cross-type comparisons should account for source.

**Distribution.** Public, free, no registration for bulk downloads (CSV and JSON) at the Downloads page; an API is also available (key signup). Public domain (CC0). This datasheet does not redistribute the data.

**Maintenance.** Maintained by USDA ARS. Updated on the per-data-type cadences above; the FDC platform and API are the canonical access points. Versioning is by publication date / data-type release.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/"
  },
  "@type": "Dataset",
  "name": "FoodData Central",
  "description": "USDA's integrated food-composition database (Foundation Foods, SR Legacy, Survey/FNDDS, Experimental, and Branded Foods) providing food descriptions, nutrient values per 100 g, and portion weights.",
  "url": "https://fdc.nal.usda.gov/",
  "sameAs": "https://fdc.nal.usda.gov/download-datasets/",
  "license": "https://creativecommons.org/publicdomain/zero/1.0/",
  "creator": {
    "@type": "Organization",
    "name": "U.S. Department of Agriculture, Agricultural Research Service",
    "url": "https://www.ars.usda.gov/"
  },
  "datePublished": "2019",
  "version": "rolling (per data-type release)",
  "citation": "U.S. Department of Agriculture, Agricultural Research Service. FoodData Central. fdc.nal.usda.gov.",
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "food.csv",
      "name": "food.csv",
      "encodingFormat": "text/csv",
      "description": "Core food records (one row per food)."
    },
    {
      "@type": "cr:FileObject",
      "@id": "food_nutrient.csv",
      "name": "food_nutrient.csv",
      "encodingFormat": "text/csv",
      "description": "Nutrient amounts per food (per 100 g)."
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "food",
      "name": "food",
      "field": [
        { "@type": "cr:Field", "@id": "food/fdc_id", "name": "fdc_id", "dataType": "sc:Integer", "description": "Unique food identifier." },
        { "@type": "cr:Field", "@id": "food/description", "name": "description", "dataType": "sc:Text", "description": "Food name/description." },
        { "@type": "cr:Field", "@id": "food/data_type", "name": "data_type", "dataType": "sc:Text", "description": "Source data type (foundation_food, sr_legacy_food, survey_fndds_food, branded_food, experimental_food)." }
      ]
    },
    {
      "@type": "cr:RecordSet",
      "@id": "food_nutrient",
      "name": "food_nutrient",
      "field": [
        { "@type": "cr:Field", "@id": "food_nutrient/fdc_id", "name": "fdc_id", "dataType": "sc:Integer", "description": "Foreign key to food." },
        { "@type": "cr:Field", "@id": "food_nutrient/nutrient_id", "name": "nutrient_id", "dataType": "sc:Integer", "description": "Foreign key to nutrient." },
        { "@type": "cr:Field", "@id": "food_nutrient/amount", "name": "amount", "dataType": "sc:Float", "description": "Nutrient amount per 100 g." }
      ]
    }
  ]
}
```

---

## Validation script

The script below validates the **structure** of a FoodData Central CSV export the user has already obtained and stored **locally**. It does **not** download, host, or republish any data — it only checks headers and row counts on a local file.

```python
#!/usr/bin/env python3
"""Validate the structure of a locally-obtained FoodData Central food.csv.

Documentation-only: this script does NOT download or host data. Point it at a
file you have already downloaded yourself from https://fdc.nal.usda.gov/download-datasets/.

Usage: python validate_fdc.py /path/to/food.csv
"""
import csv
import sys

# Expected core columns for the FDC `food` table.
# NOTE: 'fdc_id' and 'data_type' are verified from FDC docs; reconcile the full
# header against the official "Download Field Descriptions" PDF before treating
# the rest as authoritative.
EXPECTED_MIN_COLUMNS = {"fdc_id", "data_type", "description"}

def main(path: str) -> int:
    with open(path, newline="", encoding="utf-8") as f:
        reader = csv.reader(f)
        try:
            header = next(reader)
        except StopIteration:
            print("FAIL: file is empty")
            return 1
        cols = {c.strip().lower() for c in header}
        missing = EXPECTED_MIN_COLUMNS - cols
        if missing:
            print(f"FAIL: missing expected columns: {sorted(missing)}")
            return 1
        rows = sum(1 for _ in reader)
        if rows == 0:
            print("FAIL: header present but zero data rows")
            return 1
        print(f"OK: {len(header)} columns, {rows} data rows")
        print(f"OK: required columns present: {sorted(EXPECTED_MIN_COLUMNS)}")
    return 0

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__)
        sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

**Data-quality checks suggested (manual / extendable):** non-null `fdc_id` uniqueness; `data_type` ∈ the documented enum; `food_nutrient.amount` ≥ 0; nutrient amounts on a per-100-g basis; LOQ present where reported.

---

## Limitations & gaps

- **Field-level schema not fully verified.** The license, dataset composition, and table-*category* structure were confirmed from FDC documentation pages, but the official **"Download Field Descriptions" PDF did not render during retrieval (timeout)**. Individual column names/types marked *(unverified — field-level)* are inferred from the documented table categories and must be reconciled against that PDF (cited above) at the governance gate before being treated as authoritative.
- **No data was sampled or downloaded.** Per guardrails, this datasheet is documentation only; no <=1000-row sample was taken and no data-quality report was run against live data.
- **Heterogeneous data types.** Foundation, SR Legacy, Survey, Experimental, and Branded subsets differ in method, recency, and reliability; Branded data is manufacturer-reported and SR Legacy is frozen at 2018.
- **Licence snapshot artifact.** The hash + archived copy of the CC0 licence text named in the acceptance criteria is a gate artifact and is not embedded in this document.
- **No PII.** The dataset describes foods/nutrients, not people; no personal or identifying fields were found or documented.
