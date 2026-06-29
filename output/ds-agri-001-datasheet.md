# Datasheet: FAOSTAT (FAO Corporate Statistical Database)

**One-line summary:** FAOSTAT is the FAO's open global database of food and agriculture
statistics covering ~245 countries/territories and 200+ commodities, spanning production,
trade, food balances, prices, land use, emissions, population and more, from 1961 onward.

*This datasheet (the documentation in this file) is licensed under **CC-BY-4.0**.*
*The underlying FAOSTAT data is documentation-only here; it is not hosted, mirrored, or
republished by this datasheet.*

---

## Provenance & attribution

| Field | Value |
|---|---|
| **Publisher** | FAO — Food and Agriculture Organization of the United Nations |
| **Dataset** | FAOSTAT (FAO corporate statistical database) |
| **Source URL** | https://www.fao.org/faostat/ |
| **Terms / licence page** | https://www.fao.org/contact-us/terms/db-terms-of-use/en |
| **Catalog id (candidate)** | cat-agri-001 |
| **Retrieval date** | 2026-06-28 |

**Required attribution string** (per FAO database terms of use):

> FAO. [YYYY (year of last update)]. [Name of database: Name of dataset OR Name of
> database]. [Accessed on DD Month YYYY]. [URL]. Licence: CC-BY-4.0.

Example (this retrieval):

> FAO. 2026. FAOSTAT. Accessed on 28 June 2026. https://www.fao.org/faostat/. Licence: CC-BY-4.0.

---

## Source licence

**Verified licence:** Creative Commons Attribution 4.0 International (**CC BY 4.0**).

**Permits derivatives:** **Yes.** CC BY 4.0 grants the right to "Adapt — remix, transform,
and build upon the material for any purpose, even commercially," provided you give appropriate
credit, link the licence, and indicate if changes were made
(https://creativecommons.org/licenses/by/4.0/). The FAO database terms of use state that all
datasets disseminated through FAO corporate statistical databases are licensed under CC BY 4.0
and that users may "access, download, create copies, adapt and re-disseminate datasets,"
subject to attribution and to not implying FAO endorsement.

**Citation for the licence determination:**
- FAO database terms of use: https://www.fao.org/contact-us/terms/db-terms-of-use/en
  (verified 2026-06-28; states CC BY 4.0 applies and that adaptation/re-dissemination is permitted).
- Licence deed: https://creativecommons.org/licenses/by/4.0/ (Adapt clause).

> Note on the IGO variant: the original task context referenced "CC-BY-4.0 IGO". The current
> FAO database terms-of-use page reviewed on 2026-06-28 states standard **CC BY 4.0**. Both
> variants permit derivatives; the IGO variant additionally channels dispute mediation through
> WIPO/UNCITRAL. Implementers should re-check the per-dataset licence label on download, as FAO
> has used both labels across its history (the 2020 relicensing moved FAOSTAT to open CC BY).

Conditions to honour when redistributing adaptations: attribute FAO as source, indicate
changes, do not imply FAO endorsement, and do not misrepresent the data.

---

## Data dictionary

FAOSTAT distributes per-domain bulk files (e.g. QCL = Crops and livestock products, TCL =
Crops and livestock trade, GT = emissions, etc.) in two CSV shapes: a **normalized** ("long")
format and a **wide** (year-as-columns) format. The fields below describe the **normalized
bulk-download format**, which is consistent across FAOSTAT domains.

> Verification status: the live FAOSTAT bulk-download README PDFs and the JS-rendered FAOSTAT
> portal could not be fetched in this session (HTTP 403 / client-side rendering). The fields
> below reflect the documented FAOSTAT standard normalized schema and should be **re-confirmed
> against the specific domain's `*_README` and the CSV header** before automated use. Rows that
> could not be re-verified from a fetched docs page in this session are marked *(unconfirmed)*.

| Field | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| Area Code | integer | — | FAO internal numeric code for the country/region/territory | FAO area code list *(unconfirmed)* |
| Area Code (M49) | string | — | UN M49 standard country/area code | e.g. `'004'`; not-null *(unconfirmed)* |
| Area | string | — | Country/region/territory name | e.g. "Afghanistan", "World" *(unconfirmed)* |
| Item Code | integer | — | FAO internal numeric code for the item/commodity | FAO item code list *(unconfirmed)* |
| Item Code (CPC) | string | — | Central Product Classification code for the item | e.g. `'01211'` *(unconfirmed)* |
| Item | string | — | Commodity / item name | e.g. "Wheat", "Cattle" *(unconfirmed)* |
| Element Code | integer | — | FAO numeric code for the measured element | FAO element code list *(unconfirmed)* |
| Element | string | — | Measured variable | e.g. "Area harvested", "Yield", "Production" *(unconfirmed)* |
| Year Code | integer | — | Year identifier (usually equals Year) | e.g. 2022 *(unconfirmed)* |
| Year | integer | calendar year | Reference year of the observation | 1961–present *(unconfirmed)* |
| Unit | string | varies | Unit of the value | e.g. "t", "ha", "hg/ha", "1000 No" *(unconfirmed)* |
| Value | number | per Unit | The statistical observation | nullable when data unavailable *(unconfirmed)* |
| Flag | string | — | Data-status / methodology flag | coded; see below *(unconfirmed)* |
| Note | string | — | Free-text annotation (when present) | nullable *(unconfirmed)* |

**Flag codes (FAOSTAT methodology flags — illustrative, re-confirm against current legend):**
typical values include `A` (official figure), `E` (estimated), `I` (imputed),
`X` (figure from international organizations), `M` (missing — data cannot exist / not
collected). The exact active legend is published with each release and must be re-verified.
*(unconfirmed)*

No personal or identifying fields are present: FAOSTAT records are country/region-level
aggregate statistics. **No PII.**

---

## Datasheet for Datasets

**Motivation.** Created by FAO to provide free access to harmonized food and agriculture
statistics for member countries, enabling policy analysis, food-security monitoring, research,
and progress tracking on the SDGs (notably SDG 2, Zero Hunger).

**Composition.** Time-series of aggregate statistics by country/region, commodity/item, and
element (e.g. production, area harvested, yield, trade quantity/value, food balances, prices,
land use, GHG emissions, population). Instances are (area, item, element, year) observations.
Coverage typically 1961–present for core domains. Country-level aggregates only; no individuals.

**Collection process.** Compiled by FAO primarily from official national reporting
(questionnaires to national statistical offices and ministries), supplemented by estimates,
imputations, and figures from partner international organizations where official data are
missing. The methodology and data status are encoded per observation via flags.

**Preprocessing / cleaning.** FAO harmonizes country names/codes (FAO + UN M49), commodity
classifications (FAO item codes + CPC), and units; performs validation, estimation and
imputation for gaps; and labels each value with a methodology flag. Aggregates ("World",
regional groupings) are computed by FAO.

**Uses.** Food-security and nutrition analysis, agricultural economics, trade analysis,
climate/emissions accounting, academic research, journalism, and SDG monitoring. Suitable for
derivative analytical products under CC BY 4.0 with attribution. Not a substitute for
sub-national or farm-level data; aggregates can mask within-country variation.

**Distribution.** Publicly distributed via the FAOSTAT web portal (interactive query, API, and
per-domain bulk CSV/ZIP downloads). Open access, no registration required. Licence CC BY 4.0.

**Maintenance.** Maintained and regularly updated by FAO's Statistics Division; domains are
revised on rolling release schedules. Each release carries an update year used in the citation.

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
  "name": "FAOSTAT",
  "description": "FAO corporate statistical database of global food and agriculture statistics (production, trade, food balances, prices, land use, emissions, population), by country/region, item and element, from 1961 onward.",
  "url": "https://www.fao.org/faostat/",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Organization",
    "name": "Food and Agriculture Organization of the United Nations (FAO)",
    "url": "https://www.fao.org/"
  },
  "datePublished": "1996",
  "version": "2026-update",
  "keywords": ["agriculture", "food security", "FAOSTAT", "open data", "statistics"],
  "creditText": "FAO. 2026. FAOSTAT. Accessed on 28 June 2026. https://www.fao.org/faostat/. Licence: CC-BY-4.0.",
  "cr:recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "observations",
      "description": "Normalized (long) FAOSTAT bulk-download rows; fields below are stubs pending per-domain README confirmation.",
      "cr:field": [
        { "@type": "cr:Field", "name": "Area", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "Item", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "Element", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "Year", "dataType": "sc:Integer" },
        { "@type": "cr:Field", "name": "Unit", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "Value", "dataType": "sc:Float" },
        { "@type": "cr:Field", "name": "Flag", "dataType": "sc:Text" }
      ]
    }
  ]
}
```

---

## Validation script

Documentation-only: this script validates the **structure** of a FAOSTAT normalized bulk CSV
that the user has already downloaded themselves from FAOSTAT. It does **not** download, host,
mirror, or transform the dataset. Point it at a local file you obtained under CC BY 4.0.

```python
#!/usr/bin/env python3
"""Validate the structure of a locally-downloaded FAOSTAT normalized bulk CSV.

Does NOT download or host any data. Usage:
    python validate_faostat.py path/to/Production_Crops_Livestock_E_All_Data_(Normalized).csv
"""
import csv
import sys

# Standard FAOSTAT normalized-format columns. Re-confirm against the domain README:
# some domains include "Area Code (M49)", "Item Code (CPC)", and/or "Note".
EXPECTED_CORE = ["Area", "Item", "Element", "Year", "Unit", "Value", "Flag"]


def main(path: str) -> int:
    with open(path, newline="", encoding="utf-8-sig") as fh:
        reader = csv.reader(fh)
        header = next(reader, None)
        if header is None:
            print("FAIL: file is empty")
            return 1

        missing = [c for c in EXPECTED_CORE if c not in header]
        if missing:
            print(f"FAIL: missing expected columns: {missing}")
            print(f"      found header: {header}")
            return 1

        rows = sum(1 for _ in reader)
        print(f"OK: header contains all core columns ({len(header)} columns total)")
        print(f"OK: {rows} data rows")
        if rows == 0:
            print("WARN: zero data rows")
        return 0


if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("usage: python validate_faostat.py <local_faostat_normalized.csv>")
        raise SystemExit(2)
    raise SystemExit(main(sys.argv[1]))
```

---

## Limitations & gaps

- **Field schema not re-fetched live.** The FAOSTAT portal is client-side rendered and the
  bulk-download README PDFs returned HTTP 403 in this session, so the data dictionary reflects
  the documented FAOSTAT standard normalized schema rather than a freshly-fetched docs page.
  Rows are marked *(unconfirmed)* and should be re-validated against the specific domain's
  `*_README` file and the actual CSV header before automated use.
- **Licence label variant.** Licence (CC BY 4.0, permits derivatives) is verified from the FAO
  database terms-of-use page. The task context mentioned "CC-BY-4.0 IGO"; the current terms
  page states standard CC BY 4.0. Both permit derivatives, but the precise label should be
  re-checked per dataset at download time.
- **Flag legend.** Flag codes evolve between releases; the legend listed is illustrative and
  must be confirmed against the current release legend.
- **No data sampled.** Per guardrails, no dataset rows were downloaded, hosted, transformed, or
  committed. Row counts and value ranges are therefore not characterized here.
- **Coverage caveats.** FAOSTAT mixes official, estimated, and imputed values; aggregates can
  mask sub-national variation and revisions occur across releases.
