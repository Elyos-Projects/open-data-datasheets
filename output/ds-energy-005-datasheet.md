# Datasheet — Ember Electricity & Power-Sector Data

One-line summary: A documentation datasheet for Ember's open global electricity dataset (yearly/monthly generation, capacity, demand, imports and power-sector emissions for 200+ geographies), distributed in long-format CSV.

*This datasheet (the document you are reading) is licensed under **CC-BY-4.0**. It documents the dataset only; it does not host, mirror, or republish any of the underlying data.*

---

## Provenance & attribution

- **Publisher / creator:** Ember (Ember Climate / Ember Energy Research CIC), London, UK.
- **Dataset:** Ember Electricity & Power-Sector Data (Yearly Electricity Data; companion Monthly Electricity Data and Electricity Data Explorer).
- **Source URL (documentation landing page):** https://ember-energy.org/data/ and https://ember-energy.org/data/yearly-electricity-data/
- **Public download (long-format CSV, as referenced by Ember's public download bucket):** `https://storage.googleapis.com/emb-prod-bkt-publicdata/public-downloads/` (e.g. `monthly_full_release_long_format.csv`)
- **Methodology reference:** Ember "Data Methodology" PDF — `https://storage.googleapis.com/emb-prod-bkt-publicdata/public-downloads/ember_electricity_data_methodology.pdf`
- **Retrieval date:** 2026-06-28
- **Required attribution string (recommended):**
  > "Source: Ember — Yearly Electricity Data (CC BY 4.0)."
  >
  > Full citation: Ember (2026). *Global Electricity Review 2026* and underlying Yearly Electricity Data. Published by Ember, London. Licensed under CC BY 4.0.

---

## Source licence

- **Licence:** Creative Commons Attribution 4.0 International — **CC-BY-4.0** (SPDX: `CC-BY-4.0`).
- **Verified:** Ember states its electricity data and Data Explorer are "fully open and available for free under a CC BY 4.0 license." Ember maintains a dedicated Creative Commons statement page: https://ember-energy.org/creative-commons/
- **Does it permit derivatives?** **Yes.** CC-BY-4.0 explicitly grants the right to "Adapt — remix, transform, and build upon the material for any purpose, even commercially," subject only to the Attribution condition. See the canonical licence deed and legal code:
  - Deed: https://creativecommons.org/licenses/by/4.0/
  - Legal code (clause **§2(a)(1)(B)** — licence grant to "produce, reproduce, and Share Adapted Material"; **§3(a)** — attribution requirement): https://creativecommons.org/licenses/by/4.0/legalcode
- **Licence snapshot / archival note:** The canonical, immutable licence text is the Creative Commons CC BY 4.0 legal code at the URL above (Creative Commons publishes licence text as a versioned, frozen 4.0 document). For an integrity anchor, hash the retrieved `legalcode` HTML/plaintext at audit time, e.g. `sha256sum cc-by-4.0-legalcode.txt`. *No hash is asserted inline here to avoid recording an unverified digest; the validator section documents how to generate and pin one.*
- **Conclusion:** Licence permits reuse, redistribution, and derivatives (incl. commercial) with attribution. Derivative-permission requirement **met**.

---

## Data dictionary

Fields below describe the Ember **long-format** electricity CSV (yearly and monthly releases share this schema). Verified from Ember's published data pages and the public long-format CSV header referenced by Ember's download bucket. Rows marked *(unverified)* could not be confirmed exactly from the documentation at retrieval time and should be checked against a freshly downloaded header.

| Field | Type | Units | Description | Allowed values / null handling |
|---|---|---|---|---|
| Area | string | — | Geography name (country or aggregate region) | e.g. "United Kingdom", "World", "EU"; not null |
| ISO 3 code | string | — | ISO 3166-1 alpha-3 country code | 3-letter code; may be empty for non-country aggregates |
| Date | integer (yearly) / date (monthly) | year / YYYY-MM | Reporting period | Yearly: 4-digit year. Monthly: month start date. Not null |
| Area type | string (categorical) | — | Whether the row is a country or an aggregate | e.g. "Country", "Region" *(exact label set unverified)* |
| Continent | string (categorical) | — | Continent of the area | e.g. "Europe", "Asia"; empty for global aggregates |
| Ember region | string (categorical) | — | Ember's regional grouping | Ember-defined regions; may be empty |
| EU | boolean | — | EU membership flag | typically 0/1 or true/false *(encoding unverified)* |
| OECD | boolean | — | OECD membership flag | 0/1 or true/false *(encoding unverified)* |
| G20 | boolean | — | G20 membership flag | 0/1 or true/false *(encoding unverified)* |
| G7 | boolean | — | G7 membership flag | 0/1 or true/false *(encoding unverified)* |
| ASEAN | boolean | — | ASEAN membership flag | 0/1 or true/false *(encoding unverified)* |
| Category | string (categorical) | — | Top-level metric class | e.g. "Capacity", "Electricity demand", "Electricity generation", "Electricity imports", "Power sector emissions" |
| Subcategory | string (categorical) | — | Further classification within category | e.g. fuel/aggregate type, "Total", "Fossil", "Renewables" *(full set unverified)* |
| Variable | string (categorical) | — | Specific metric / fuel | e.g. "Coal", "Gas", "Wind", "Solar", "Hydro", "Nuclear", "Total Generation", "Demand", "CO2 intensity" |
| Unit | string (categorical) | depends on row | Measurement unit | e.g. "TWh", "%", "MW"/"GW", "mtCO2", "gCO2/kWh" |
| Value | float | per Unit | Numeric measurement | May be null/empty where data unavailable; modelled estimates used for unreported recent months |
| YoY absolute change | float | per Unit | Year-on-year absolute change | Nullable (no value for first year / new series) |
| YoY % change | float | % | Year-on-year percentage change | Nullable; may be empty where prior-year value is 0 or missing |

Notes on nulls/estimates: Ember produces **modelled estimates** to complete a data year where the most recent months are not yet officially reported; some small territories may carry an older Ember vintage. Coverage: 200+ geographies (215 countries reported); recent-year early releases cover ~90+ countries representing ~93% of global demand.

---

## Datasheet for Datasets

**Motivation.** Created by Ember, an independent energy think tank, to provide a transparent, comparable, openly licensed picture of the global power sector (generation mix, capacity, demand, imports, emissions) to inform the clean-energy transition. It is widely reused by researchers, journalists, NGOs, and aggregators such as Our World in Data.

**Composition.** Country- and region-level annual (and monthly) time series of electricity generation by fuel, installed capacity, demand, imports, and power-sector CO2 emissions/intensity. Instances are (Area × Date × Variable) observations in long format. **No personal or individual-level data** — all observations are national/regional aggregates. No PII present.

**Collection process.** Compiled by Ember from official national and multinational statistical sources (e.g. national statistics offices, ENTSO-E, EIA, Eurostat, IEA-type sources) and harmonised; gaps in the most recent period filled with documented modelled estimates. See Ember's Data Methodology PDF (linked above).

**Preprocessing / cleaning / labeling.** Source series are standardised to common units (TWh, MW/GW, %, mtCO2, gCO2/kWh), mapped to consistent Area/ISO codes and Category/Subcategory/Variable taxonomies, and reshaped to long format. Derived fields (YoY absolute and % change) are computed by Ember.

**Uses.** Energy-transition tracking, country/region benchmarking, emissions analysis, journalism, academic research, and as an upstream source for derived datasets. Not intended for sub-national/grid-operational use or for the most-recent unreported months without noting modelled estimates.

**Distribution.** Published openly by Ember on ember-energy.org and via a public download bucket as CSV (long format), under CC-BY-4.0. Free to share and adapt with attribution.

**Maintenance.** Maintained and updated periodically by Ember (annual full releases plus monthly updates; vintage years are versioned, e.g. data year 2025 released 2026). Contact and updates via ember-energy.org.

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
  "name": "Ember Electricity & Power-Sector Data (Yearly Electricity Data)",
  "description": "Open global electricity dataset: yearly (and monthly) electricity generation by fuel, installed capacity, demand, imports and power-sector emissions for 200+ geographies, in long format. Published by Ember under CC-BY-4.0.",
  "url": "https://ember-energy.org/data/yearly-electricity-data/",
  "sameAs": "https://ember-energy.org/data/",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Organization",
    "name": "Ember",
    "url": "https://ember-energy.org/"
  },
  "datePublished": "2026",
  "version": "data-year-2025",
  "keywords": ["electricity", "energy", "power sector", "emissions", "generation", "capacity", "open data"],
  "distribution": [
    {
      "@type": "cr:FileObject",
      "@id": "yearly_electricity_long_format.csv",
      "name": "yearly_electricity_long_format.csv",
      "encodingFormat": "text/csv",
      "contentUrl": "https://ember-energy.org/data/yearly-electricity-data/"
    }
  ],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "@id": "observations",
      "name": "observations",
      "field": [
        {"@type": "cr:Field", "@id": "observations/area", "name": "Area", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "observations/iso3", "name": "ISO 3 code", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "observations/date", "name": "Date", "dataType": "sc:Integer"},
        {"@type": "cr:Field", "@id": "observations/category", "name": "Category", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "observations/subcategory", "name": "Subcategory", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "observations/variable", "name": "Variable", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "observations/unit", "name": "Unit", "dataType": "sc:Text"},
        {"@type": "cr:Field", "@id": "observations/value", "name": "Value", "dataType": "sc:Float"}
      ]
    }
  ]
}
```

---

## Validation script

The script below validates the **structure** of a locally-obtained Ember long-format CSV. It does **not** download, host, or redistribute any data — the operator supplies a local file path that they obtained themselves from Ember under the dataset's licence. It only reads the header and a bounded sample.

```python
#!/usr/bin/env python3
"""Validate the structure of a LOCAL Ember long-format electricity CSV.
Documentation-only: this script does NOT download or host any data.
Usage: python validate_ember.py /path/to/your_local_ember_long_format.csv
"""
import csv
import sys

EXPECTED_COLUMNS = [
    "Area", "ISO 3 code", "Date", "Area type", "Continent", "Ember region",
    "EU", "OECD", "G20", "G7", "ASEAN",
    "Category", "Subcategory", "Variable", "Unit", "Value",
    "YoY absolute change", "YoY % change",
]
# Core columns that must be present regardless of release flavour:
REQUIRED_CORE = {"Area", "Date", "Category", "Variable", "Unit", "Value"}
SAMPLE_LIMIT = 1000  # bounded read; never load the whole file

def main(path):
    with open(path, newline="", encoding="utf-8-sig") as f:
        reader = csv.reader(f)
        header = next(reader)
        cols = set(h.strip() for h in header)

        missing_core = REQUIRED_CORE - cols
        if missing_core:
            print(f"FAIL: missing required core columns: {sorted(missing_core)}")
            return 1
        unexpected = cols - set(EXPECTED_COLUMNS)
        if unexpected:
            print(f"WARN: columns not in expected schema (review): {sorted(unexpected)}")

        rows = 0
        bad_value = 0
        for row in reader:
            rows += 1
            rec = dict(zip(header, row))
            v = (rec.get("Value") or "").strip()
            if v not in ("", "NA", "NaN"):
                try:
                    float(v)
                except ValueError:
                    bad_value += 1
            if rows >= SAMPLE_LIMIT:
                break

        print(f"OK: header valid. Sampled {rows} rows (cap {SAMPLE_LIMIT}).")
        print(f"Non-numeric Value cells in sample: {bad_value}")
        return 0

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__); sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

To pin a licence-text integrity hash for the audit trail (documentation only):

```bash
# Fetch the canonical CC BY 4.0 legal code once, locally, and record its digest.
curl -s https://creativecommons.org/licenses/by/4.0/legalcode.txt -o cc-by-4.0-legalcode.txt
sha256sum cc-by-4.0-legalcode.txt   # record this digest in the gate artifact
```

---

## Limitations & gaps

- **Field encodings partly unverified.** The boolean membership flags (EU/OECD/G20/G7/ASEAN) and the exact label sets for `Area type`, `Subcategory`, and the full `Variable`/`Unit` enumerations could not be confirmed cell-by-cell from the documentation at retrieval time (Ember's site returned HTTP 403 to automated fetches). Column **names** were verified from Ember's data pages and the public long-format CSV reference; **value enumerations** should be re-checked against a freshly downloaded header. Such rows are marked *(unverified)* in the data dictionary.
- **No data sampled.** Per the documentation-only guardrail, no rows of the actual dataset were downloaded, hosted, transformed, or committed; the data dictionary reflects documented schema, not a fetched sample.
- **Licence hash not asserted.** The CC-BY-4.0 text is referenced by its canonical, versioned URL; no digest is hard-coded here to avoid recording an unverified value. The validation section documents how to generate and pin one.
- **Vintage/coverage caveats.** Recent-year values may be modelled estimates; coverage and exact geography counts vary by release vintage. Confirm against the specific release used.
- **Source page access.** Ember pages blocked automated retrieval (403); verification relied on Ember's own statements surfaced via search plus the canonical Creative Commons licence text. License determination (CC-BY-4.0, derivatives permitted) is considered confirmed; field-level details are confirmed only to the extent noted above.
