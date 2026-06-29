# Datasheet — Crime & Criminal Justice Statistics (Eurostat)

One-line summary: A documentation datasheet for Eurostat's comparable EU crime and criminal
justice statistics (police-recorded offences, offenders, victims, and justice-system personnel
across EU members, EFTA, and candidate countries).

**Datasheet licence:** This datasheet (the document you are reading) is published under
**CC-BY-4.0**. It is documentation only and contains no copy of the underlying dataset.

---

## Provenance & attribution

- **Publisher / source:** Eurostat — the statistical office of the European Union.
- **Source URL:** https://ec.europa.eu/eurostat/web/crime
- **Catalog id (candidate):** cat-justice-004
- **Retrieval date:** 2026-06-28
- **Required attribution string:**
  `Source: Eurostat — Crime and criminal justice statistics, © European Union, retrieved 2026-06-28.
  Reused under CC BY 4.0; changes (extraction/summarisation) indicated.`

The actual data is distributed through the Eurostat online database/dissemination API and is **not**
mirrored, hosted, or transformed by this datasheet.

---

## Source licence

- **Licence:** Creative Commons Attribution 4.0 International (**CC BY 4.0**).
- **Legal basis:** Commission Decision 2011/833/EU on the reuse of Commission documents; the
  European Commission legal notice applies the CC BY 4.0 licence to its documents and data.
- **Citation / confirming clause:** European Commission legal notice
  (https://commission.europa.eu/legal-notice_en):
  > "This means that reuse is allowed, provided appropriate credit is given and changes are
  > indicated."
  CC BY 4.0 expressly permits derivative works and commercial reuse (see
  https://creativecommons.org/licenses/by/4.0/ — "Adapt — remix, transform, and build upon the
  material for any purpose, even commercially").
- **Derivatives permitted:** **YES.** CC BY 4.0 permits adaptation/derivatives provided attribution
  is given and changes are indicated. A datasheet (documentation about the data) is therefore
  permitted.
- **Caveat captured from the source legal notice:** additional rights clearance may be required
  where content involves identifiable individuals or third-party works; EU industrial-property
  rights (logos, trademarks) are excluded from the reuse licence. None of these affect this
  documentation-only datasheet.

> Licence snapshot note: per acceptance criteria, an archived copy + hash of the CC BY 4.0 licence
> text should be attached to the per-dataset gate artifact at review time. This datasheet cites the
> canonical licence URL rather than embedding the text.

---

## Data dictionary

Eurostat publishes this domain as a **collection of related tables** (a data cube per indicator)
rather than a single flat file, so fields below are the **common dimensions** shared across the
crime/justice tables, verified from the dataset overview page. Specific code-list values (e.g. the
full ICCS offence categories) live in Eurostat's dimension code lists and are marked **UNVERIFIED**
where the exact enumeration was not inspected in this pass.

| Field (dimension) | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| `geo` | categorical | — | Reporting geography | EU member states, EFTA, candidate/potential-candidate countries; NUTS 3 regions for some tables. Exact code list **UNVERIFIED** |
| `time` (`TIME_PERIOD`) | temporal | year | Reference year | Recent years incl. 2024; "last 10 years" coverage noted on overview. Missing years = null |
| `iccs` / offence type | categorical | — | Type of offence | intentional homicide, sexual violence, human trafficking, migrant smuggling, bribery/corruption (verified categories listed on overview); full ICCS list **UNVERIFIED** |
| `unit` | categorical | varies | Measurement unit | e.g. number, per hundred thousand inhabitants — exact enumeration **UNVERIFIED** |
| `sex` | categorical | — | Sex breakdown (victims/perpetrators) | typically M / F / T(total); nulls where not applicable. Codes **UNVERIFIED** |
| `age` | categorical | — | Age group breakdown | age bands; exact bands **UNVERIFIED** |
| `citizen` | categorical | — | Citizenship breakdown of victim/offender | code list **UNVERIFIED** |
| `leg_stat` / justice stage | categorical | — | Stage in justice process for offenders | suspected, prosecuted, convicted (verified concept); exact codes **UNVERIFIED** |
| `OBS_VALUE` | numeric | per `unit` | Observed statistical value | non-negative; null/`:` = not available/confidential |
| `OBS_FLAG` | categorical | — | Observation status flag | Eurostat flags (e.g. `b`, `e`, `p`, `c`, `:`); exact set **UNVERIFIED** |

Additional thematic tables in this domain cover **justice-system personnel** (police, courts,
prison staff) and **prison data** (prisoners by demographics, prison capacity/occupancy) — these
share the `geo`/`time`/`unit` dimensions above. Their specific measure fields are **UNVERIFIED** in
this pass.

> PII note: all documented fields are **aggregate counts / rates by category**. No
> personal/identifying records are documented or sampled. No micro-data is exposed by these tables.

---

## Datasheet for Datasets

**Motivation.** Created so that crime and criminal-justice phenomena can be compared across EU and
associated countries on a harmonised basis, supporting policy, research, and public transparency.
Produced by Eurostat in cooperation with national statistical authorities and ministries.

**Composition.** Aggregate statistics (counts and rates) on police-recorded offences, offenders by
justice stage, victims, justice-system personnel, and prison populations, broken down by geography,
year, offence type, and demographic dimensions (sex, age, citizenship). Instances are
aggregate cells, **not** individuals — no personal records.

**Collection process.** Data are compiled from national administrative sources (police, prosecution,
courts, prison services) and reported to Eurostat by member/associated countries, then harmonised
toward comparable definitions (the International Classification of Crime for Statistical Purposes,
ICCS). Exact per-table methodology is documented in Eurostat's metadata/"information on data"
sections (**UNVERIFIED** in detail here).

**Preprocessing / cleaning.** Eurostat harmonises national figures to common classifications and
applies observation flags (provisional, estimated, break-in-series, confidential). Confidential or
unavailable cells are suppressed (`:`).

**Uses.** Cross-country comparison, trend analysis, policy evaluation, academic research,
journalism. **Not** suitable for identifying individuals or for operational/law-enforcement
targeting. Comparability caveats apply because national legal definitions and recording practices
differ despite ICCS harmonisation.

**Distribution.** Disseminated openly via the Eurostat database and dissemination API under CC BY
4.0. This datasheet does not redistribute the data.

**Maintenance.** Maintained and periodically updated by Eurostat; users should re-fetch from the
source for current vintages and consult the source metadata for revisions.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/"
  },
  "@type": "Dataset",
  "name": "Eurostat — Crime and Criminal Justice Statistics",
  "description": "Comparable EU statistics on police-recorded offences, offenders, victims, justice-system personnel, and prison populations across EU member states, EFTA, and candidate countries, broken down by geography, year, offence type, and demographics.",
  "url": "https://ec.europa.eu/eurostat/web/crime",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Organization",
    "name": "Eurostat",
    "url": "https://ec.europa.eu/eurostat"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Statistical Office of the European Union (Eurostat)"
  },
  "datePublished": "2026-06-28",
  "keywords": ["crime", "criminal justice", "European Union", "Eurostat", "ICCS", "public-data"],
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "crime_justice_observations",
      "description": "Aggregate observation cells (counts/rates) by geography, year, offence type, and demographic breakdown.",
      "field": [
        { "@type": "cr:Field", "name": "geo", "description": "Reporting geography (country / NUTS region)", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "time", "description": "Reference year", "dataType": "sc:Date" },
        { "@type": "cr:Field", "name": "iccs", "description": "Offence type (ICCS-aligned)", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "unit", "description": "Measurement unit (number, per 100k)", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "OBS_VALUE", "description": "Observed value", "dataType": "sc:Float" },
        { "@type": "cr:Field", "name": "OBS_FLAG", "description": "Eurostat observation status flag", "dataType": "sc:Text" }
      ]
    }
  ]
}
```

---

## Validation script

Documentation only — this script does **not** download, mirror, or host the dataset. Point it at a
locally obtained, ephemeral sample (header/streamed read, <= 1000 rows) that you fetched yourself
from the source under its licence; it checks structure and basic quality.

```python
#!/usr/bin/env python3
"""Validate the structure of a local Eurostat crime/justice sample (TSV/CSV).
Does NOT download or host data. Usage: python validate.py path/to/local_sample.tsv"""
import sys, csv

# Common Eurostat dimensions expected across crime/justice tables.
# Exact set varies by table; treat absence of all as a hard failure.
EXPECTED_DIMS = {"geo", "TIME_PERIOD", "OBS_VALUE"}
# 'time' may appear as wide year columns in classic Eurostat TSV; accept either layout.
MAX_SAMPLE_ROWS = 1000

def main(path):
    with open(path, newline="", encoding="utf-8") as f:
        # Eurostat dissemination TSV is tab-separated; SDMX-CSV is comma-separated.
        sniff = f.read(4096); f.seek(0)
        delim = "\t" if "\t" in sniff else ","
        reader = csv.reader(f, delimiter=delim)
        header = next(reader, None)
        assert header, "empty file"
        cols = {c.strip().split("\\")[0] for c in header}  # strip 'dim\time' artefacts
        wide_years = any(c.strip().isdigit() and len(c.strip()) == 4 for c in header)
        ok_dims = ("geo" in " ".join(header).lower()) and ("OBS_VALUE" in cols or wide_years)
        assert ok_dims, f"missing expected geo/value structure; got {header[:6]}"

        rows = 0
        for row in reader:
            rows += 1
            if rows > MAX_SAMPLE_ROWS:
                print(f"NOTE: sample exceeds {MAX_SAMPLE_ROWS} rows; truncating check.")
                break
        assert rows > 0, "no data rows"
    print(f"OK: structure looks valid (delimiter={delim!r}, "
          f"wide_year_layout={wide_years}, rows_checked={rows}).")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        sys.exit("usage: python validate.py path/to/local_sample.tsv")
    main(sys.argv[1])
```

Expected result: the script confirms a `geo` dimension and either an `OBS_VALUE` column (SDMX-CSV)
or wide 4-digit year columns (classic Eurostat TSV), and that at least one data row is present.

---

## Limitations & gaps

- **Field enumerations are partially unverified.** The overview page confirms the dimensions and
  several offence categories, but the exact code lists (full ICCS offence list, `unit`, `sex`,
  `age`, `citizen`, `OBS_FLAG` values) were **not** inspected against Eurostat's dimension code
  lists in this pass; those rows are marked **UNVERIFIED**. Do not treat unverified field values as
  authoritative — confirm against the source metadata before relying on them.
- **Multi-table domain.** "Crime and criminal justice statistics" is a *collection* of tables, not
  one file; the data dictionary documents shared dimensions, not every per-table measure.
- **Licence snapshot.** The licence (CC BY 4.0) and its derivative permission are verified via the
  EC legal notice and the canonical CC URL, but an archived hash/copy of the licence text (an
  acceptance-criteria artifact) is to be attached at the gate, not embedded here.
- **No data inspected at row level.** Per guardrails, no dataset was hosted, downloaded into this
  repo, transformed, or sampled here; structural expectations are derived from the documented
  Eurostat dissemination formats.
- **Comparability.** Despite ICCS harmonisation, national recording/legal differences limit strict
  cross-country comparison.
