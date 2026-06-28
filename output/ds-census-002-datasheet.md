# Datasheet: Census 2021 (England & Wales)

One-line summary: Aggregated 2021 Census tables for England & Wales, published by the UK
Office for National Statistics (ONS), covering population, household and demographic topics
across multiple geographic levels.

*This datasheet (the documentation in this file) is licensed under **CC-BY-4.0**. It is
documentation only and contains none of the underlying dataset.*

---

## Provenance & attribution

| Field | Value |
|---|---|
| Publisher / source | UK Office for National Statistics (ONS) |
| Dataset | Census 2021, England & Wales |
| Source URL | https://www.ons.gov.uk/census |
| Custom-dataset / table builder | https://www.ons.gov.uk/datasets/create |
| Retrieval date | 2026-06-28 |
| Catalog id (candidate) | cat-census-002 |

**Required attribution string** (per OGL v3.0):

> Contains public sector information licensed under the Open Government Licence v3.0.
> Source: Office for National Statistics, Census 2021. https://www.ons.gov.uk/census

---

## Source licence

- **Licence name:** Open Government Licence v3.0 (OGL v3.0).
- **Verified:** YES — the source page states: *"All content is available under the Open
  Government Licence v3.0, except where otherwise stated."*
  (https://www.ons.gov.uk/census)
- **Citation that it permits derivatives:** The OGL v3.0 text
  (https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/) grants the
  rights to *"copy, publish, distribute and transmit the Information"*, to *"adapt the
  Information"*, and to *"exploit the Information commercially and non-commercially for
  example, by combining it with other Information, or by including it in your own product or
  application."* The "adapt" clause explicitly permits derivative works.
- **Attribution required by licence:** *"Contains public sector information licensed under the
  Open Government Licence v3.0."* (or the provider-specified attribution statement, given
  above).

> Licence snapshot note: this deed records the licence name, the verbatim adaptation/derivative
> clauses above, and the two citation URLs. A separate hashed/archived copy of the full licence
> text (an acceptance-criteria artifact) is NOT embedded here to keep this file documentation-
> only; it should be attached at the per-dataset gate.

---

## Data dictionary

Census 2021 aggregated outputs are distributed as **custom datasets / flat tables**, not a
single fixed file. Each downloaded table combines one or more **classification variables** with
a **geography** and a single **observation (count)** column.

The topic/variable list below is **verified** from the source page. The exact column layout is
documented from ONS's published custom-dataset format and is **NOT verified against a live data
sample in this deed** (the interactive table builder did not expose a static schema; rows are
marked accordingly).

### Verified topics/variables covered (from source page)

Ageing; Demography; Education; Ethnic group, national identity, language and religion; Health,
disability and unpaid care; Housing; International migration; Labour market; Sexual orientation
and gender identity; Travel to work; UK armed forces veterans.

### Table column structure

| Field (column) | Type | Units | Description | Allowed values / null handling | Verified? |
|---|---|---|---|---|---|
| `<Geography> Code` | string | n/a | ONS geography code for the area (e.g. an output-area or local-authority GSS code such as `E92000001`) | Non-null; one row per area × category combination | Documented format — UNVERIFIED against live sample |
| `<Geography>` (label) | string | n/a | Human-readable area name corresponding to the code | Non-null | Documented format — UNVERIFIED against live sample |
| `<Variable> (N categories) Code` | integer | n/a | Numeric code for the category of the classification variable | Domain depends on the chosen classification | Documented format — UNVERIFIED against live sample |
| `<Variable> (N categories)` (label) | string | n/a | Human-readable category label (e.g. an age band, ethnic group, tenure type) | Includes a "Does not apply" / aggregate category in many variables | Documented format — UNVERIFIED against live sample |
| `Observation` | integer | persons / households | The count for that area × category combination | Non-negative integer; ONS applies statistical disclosure control, so small counts may be rounded/perturbed | Documented format — UNVERIFIED against live sample |

### Geography levels (documented; UNVERIFIED row-by-row in this deed)

Country, Region, Upper-tier and Lower-tier local authority, Middle layer Super Output Area
(MSOA), Lower layer Super Output Area (LSOA), Output Area (OA), and electoral wards are
commonly available. Availability of finer levels varies by variable due to disclosure control.
Treat the precise level list as **unverified** here.

---

## Datasheet for Datasets

**Motivation.** Created to deliver the decennial statutory census of population and households
for England & Wales (Census Day: 21 March 2021), informing public-service planning, funding
allocation and research. Produced by ONS.

**Composition.** Aggregated counts of persons and households cross-tabulated by demographic,
social and economic classification variables, by geography. Instances are area × category
counts, not individual records. No microdata / individual-level records are included in the
public aggregated tables documented here.

**Collection process.** Self-completed census questionnaires (online and paper) returned by
households and individuals across England & Wales for Census Day 2021, processed and aggregated
by ONS, with statistical disclosure control applied to protect confidentiality.

**Preprocessing / cleaning.** ONS edits, imputes for non-response, classifies free-text
responses into standard categories, and applies disclosure control (e.g. rounding/perturbation
and suppression at small geographies). Exact methods are documented in ONS methodology pages
(not re-stated here).

**Uses.** Demographic analysis, public-service and infrastructure planning, equality
monitoring, academic research, combining with other open data. Suitable for aggregate analysis;
NOT suitable for re-identifying individuals.

**Distribution.** Published openly by ONS on ons.gov.uk and via NOMIS / the custom dataset
builder under OGL v3.0. This datasheet does not redistribute any data.

**Maintenance.** Maintained by ONS; Census 2021 is a fixed historical reference point (next
census expected ~2031), though ONS may release additional/updated tables. Contact via
ons.gov.uk.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/"
  },
  "@type": "Dataset",
  "name": "Census 2021 (England and Wales)",
  "description": "Aggregated 2021 Census tables for England and Wales (Census Day 21 March 2021), published by the UK Office for National Statistics. Counts of persons and households by demographic, social and economic classification variables across multiple geographic levels.",
  "url": "https://www.ons.gov.uk/census",
  "license": "https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/",
  "creator": {
    "@type": "Organization",
    "name": "Office for National Statistics",
    "url": "https://www.ons.gov.uk"
  },
  "datePublished": "2022",
  "keywords": ["census", "demographics", "population", "England", "Wales", "ONS", "open-data"],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "census_table",
      "description": "A custom Census 2021 table: one row per geography x category combination.",
      "field": [
        {"@type": "cr:Field", "name": "geography_code", "dataType": "Text", "description": "ONS GSS geography code for the area."},
        {"@type": "cr:Field", "name": "geography_label", "dataType": "Text", "description": "Human-readable area name."},
        {"@type": "cr:Field", "name": "category_code", "dataType": "Integer", "description": "Numeric code of the classification category."},
        {"@type": "cr:Field", "name": "category_label", "dataType": "Text", "description": "Human-readable classification category label."},
        {"@type": "cr:Field", "name": "observation", "dataType": "Integer", "description": "Count for the geography x category combination (subject to disclosure control)."}
      ]
    }
  ]
}
```

---

## Validation script

This script checks the **structure** of a Census 2021 custom-dataset CSV that a user has
already downloaded themselves from ONS. It does **not** download, host, mirror or transform any
data — it only inspects a local file the user supplies.

```python
#!/usr/bin/env python3
"""Validate the structure of a locally-downloaded ONS Census 2021 custom-dataset CSV.

Usage: python validate_census.py path/to/your_downloaded_table.csv
This script does NOT fetch, host, or redistribute any data. Bring your own file.
"""
import csv
import sys


def validate(path: str) -> int:
    with open(path, newline="", encoding="utf-8-sig") as f:
        reader = csv.reader(f)
        header = next(reader, None)
        if not header:
            print("FAIL: empty file / no header")
            return 1

        # Expected shape: pairs of (<dim> Code, <dim> label) ... then an Observation column.
        if not any(h.strip().lower() == "observation" for h in header):
            print("FAIL: no 'Observation' column found")
            return 1

        code_cols = [h for h in header if h.strip().lower().endswith("code")]
        if not code_cols:
            print("FAIL: expected at least one '... Code' column (geography/category)")
            return 1

        obs_idx = [i for i, h in enumerate(header) if h.strip().lower() == "observation"][0]

        rows = 0
        for row in reader:
            if not row:
                continue
            rows += 1
            val = row[obs_idx].strip()
            if val and not val.lstrip("-").isdigit():
                print(f"FAIL: non-integer Observation on row {rows}: {val!r}")
                return 1

        print(f"OK: {len(header)} columns, {len(code_cols)} code column(s), {rows} data rows")
        print(f"    columns: {header}")
        return 0


if __name__ == "__main__":
    if len(sys.argv) != 2:
        print(__doc__)
        sys.exit(2)
    sys.exit(validate(sys.argv[1]))
```

Expected result on a well-formed ONS custom-dataset CSV: at least one `... Code` column, one
`Observation` column, all observation values non-negative integers, and a row count > 0.

---

## Limitations & gaps

- **Field layout is unverified against a live sample.** The ONS census data is served through
  interactive tools (custom dataset builder, maps, NOMIS) that did not expose a static schema
  to fetch within this documentation-only deed. The data-dictionary column layout and geography
  level list reflect ONS's publicly documented custom-dataset format, NOT a downloaded sample;
  rows are marked UNVERIFIED accordingly. A reuser should confirm exact column headers against
  their own downloaded table.
- **Verified:** the topic/variable list and the OGL v3.0 licence (including the adaptation /
  derivative-works clauses) were verified directly from ONS and The National Archives pages on
  2026-06-28.
- **Disclosure control:** small counts may be rounded, perturbed, or suppressed; do not treat
  low observations as exact. Tables are aggregate only and contain no personal/identifying data.
- **Licence snapshot artifact** (hash + archived full licence text) and the per-dataset gate
  artifact are referenced but not embedded here, to keep this file documentation-only.
- No actual census data was downloaded, sampled, hosted, transformed, or committed in producing
  this datasheet.
