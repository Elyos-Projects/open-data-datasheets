# Datasheet: Air Quality System (AQS)

**One-line summary:** The U.S. EPA's authoritative repository of ambient air-pollution
measurements and monitoring metadata, distributed as pre-generated CSV summary files and
via a public API.

*This datasheet is licensed under **CC-BY-4.0**. It is documentation only and contains no
dataset records.*

---

## Provenance & attribution

| Field | Value |
|---|---|
| Dataset | Air Quality System (AQS) |
| Publisher | U.S. Environmental Protection Agency (EPA) — Office of Air Quality Planning and Standards (OAQPS), Office of Air and Radiation (OAR) |
| Source URL (landing) | https://www.epa.gov/aqs |
| Pre-generated data files | https://aqs.epa.gov/aqsweb/airdata/download_files.html |
| File format docs | https://aqs.epa.gov/aqsweb/airdata/FileFormats.html |
| Data dictionary | https://aqs.epa.gov/aqsweb/documents/AQS_Data_Dictionary.html |
| Catalog entry | https://catalog.data.gov/dataset/air-quality-system-aqs (catalog id: cat-airq-002) |
| Retrieval date | 2026-06-28 |

**Required attribution string (recommended; not mandated by the licence):**

> Source: U.S. Environmental Protection Agency, Air Quality System (AQS),
> https://www.epa.gov/aqs (retrieved 2026-06-28). Data is in the U.S. public domain.

---

## Source licence

**Licence: U.S. Public Domain (work of the U.S. federal government).**

Verified from the **EPA Data License** referenced by the data.gov catalog entry:
https://edg.epa.gov/EPA_Data_License.htm

Cited clause (verbatim):

> "all data produced by the U.S EPA is by default in the public domain and is not subject
> to domestic copyright protection under 17 U.S.C. § 105."

**Derivatives permitted:** Yes. Public-domain status (17 U.S.C. § 105) imposes no copyright
restriction on use, redistribution, or the creation of derivative works. The licence adds
no mandatory attribution requirement. Standard EPA disclaimer applies:

> "no warranty expressed or implied is made regarding the accuracy or utility of the data
> on any other system or for general or scientific purposes ... The U.S. EPA shall not be
> held liable for improper or incorrect use of the data."

*Licence-text snapshot:* archive the canonical text and record a hash for provenance, e.g.:
`curl -s https://edg.epa.gov/EPA_Data_License.htm | sha256sum > EPA_Data_License.sha256`
(run by the maintainer at gate time; the archived copy and hash are stored as the
per-dataset gate artifact, not in this repository).

---

## Data dictionary

Fields below are verified from the AQS **pre-generated file format documentation**
(FileFormats.html), for the two most-used products: **Daily Summary** and **Hourly** files.
Both are headered CSV. Parameter codes are 5-digit AQS codes (e.g. `44201` = Ozone). The
full enumerated parameter/qualifier/method code lists are not reproduced here; consult the
AQS Coding Manual and Data Dictionary.

### Daily Summary files

| # | Field | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|---|
| 1 | State Code | string | — | FIPS code of the state of the monitor | 2-digit FIPS; not null |
| 2 | County Code | string | — | FIPS code of the county | 3-digit FIPS; not null |
| 3 | Site Num | string | — | Site number, unique within county | not null |
| 4 | Parameter Code | string | — | AQS code for the measured parameter | 5-digit code; not null |
| 5 | POC | integer | — | Parameter Occurrence Code (distinguishes co-located instruments) | ≥1 |
| 6 | Latitude | decimal | degrees | Angular distance north of equator | decimal degrees |
| 7 | Longitude | decimal | degrees | Angular distance east of prime meridian | decimal degrees |
| 8 | Datum | string | — | Coordinate reference system | e.g. WGS84, NAD83 |
| 9 | Parameter Name | string | — | Human-readable parameter description | not null |
| 10 | Sample Duration | string | — | Length of time air passes through the device | e.g. "1 HOUR", "24 HOUR" |
| 11 | Pollutant Standard | string | — | Standard used to aggregate statistics | may be blank if N/A |
| 12 | Date Local | date (YYYY-MM-DD) | — | Calendar date for the summary (local) | not null |
| 13 | Units of Measure | string | varies | Standard units for the parameter | parameter-dependent |
| 14 | Event Type | string | — | Exceptional-event handling | "No Events", "Events Included", "Events Excluded", "Concurred Events Excluded" |
| 15 | Observation Count | integer | count | Number of samples that day | ≥0 |
| 16 | Observation Percent | decimal | percent | Percent of scheduled observations collected | 0–100 |
| 17 | Arithmetic Mean | decimal | (units col 13) | Daily arithmetic mean value | may be null |
| 18 | 1st Max Value | decimal | (units col 13) | Highest value for the day | may be null |
| 19 | 1st Max Hour | integer | hour | Hour the max occurred | 0–23 |
| 20 | AQI | integer | index | Air Quality Index, if applicable | blank when not computed |
| 21 | Method Code | string | — | Internal method identifier | may be blank |
| 22 | Method Name | string | — | Short method/equipment description | may be blank |
| 23–29 | Local Site Name, Address, State Name, County Name, City Name, CBSA Name, Date of Last Change | string / date | — | Geographic & administrative attributes | some may be blank |

### Hourly files

| # | Field | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|---|
| 1–9 | State Code, County Code, Site Num, Parameter Code, POC, Latitude, Longitude, Datum, Parameter Name | as above | — | Site/monitor identifiers | as above |
| 10 | Date Local | date | — | Sample date, Local Standard Time | not null |
| 11 | Time Local | time (HH:MM) | — | Start time of sampling, 24-hour clock, local | not null |
| 12 | Date GMT | date | — | Sample date in GMT | not null |
| 13 | Time GMT | time (HH:MM) | — | Sample time in GMT | not null |
| 14 | Sample Measurement | decimal | (units col 15) | Measured value | may be null (missing) |
| 15 | Units of Measure | string | varies | Standard units | parameter-dependent |
| 16 | MDL | decimal | (units col 15) | Method Detection Limit | may be blank |
| 17 | Uncertainty | decimal | (units col 15) | Total measurement uncertainty | often blank |
| 18 | Qualifier | string | — | Missing/exceptional/QA indicators | code list; may be blank |
| 19 | Method Type | string | — | FRM / equivalent-to-FRM / approved regional / non-federal reference | — |
| 20 | Method Code | string | — | Internal method identifier | may be blank |
| 21 | Method Name | string | — | Method description | may be blank |
| 22–24 | State Name, County Name, Date of Last Change | string / date | — | Administrative attributes | — |

**Unverified / not enumerated here:** exact Qualifier code list, full Parameter Code
catalogue, Method Code values, and Datum enumerations (these live in the AQS Coding Manual
and Data Dictionary and were not exhaustively transcribed). Column ordering/types were
verified against FileFormats.html but exact null-vs-blank conventions per column should be
confirmed against a sample header before automated parsing.

---

## Datasheet for Datasets

**Motivation.** Created so EPA, state, local, and tribal agencies can store, share, and
report regulatory ambient air-quality measurements (criteria pollutants, air toxics, and
meteorological parameters) used for NAAQS compliance, public AQI reporting, and research.

**Composition.** Time-series measurements from thousands of fixed monitoring stations
across the U.S. and territories, plus monitor/site metadata (location, method, operating
agency) and QA information. Pre-generated products aggregate raw submissions into hourly,
daily, annual, and other summaries. Records describe **environmental monitors and physical
measurements**, not people; no personal/identifying data is present.

**Collection process.** Measurements are taken by regulatory-grade monitoring instruments
operated by reporting agencies, submitted to AQS, and subjected to QA/QC. EPA derives the
aggregate summary files from those submissions.

**Preprocessing / cleaning.** Pre-generated files are EPA-calculated aggregates, not raw
feeds. Values below the MDL may be substituted with half the MDL in some calculations;
exceptional events are flagged via the Event Type / Qualifier fields.

**Uses.** Regulatory compliance analysis, AQI/public-health reporting, exposure and
epidemiological research, model validation. **Not** suitable as raw instrument data and
not a substitute for real-time alerting.

**Distribution.** Free public download via the AQS airdata pre-generated files and the AQS
Data API; also catalogued on data.gov. Public domain — redistributable.

**Maintenance.** Maintained by EPA OAQPS/OAR. Each record carries a "Date of Last Change";
files are regenerated as agencies submit and certify data.

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
  "name": "Air Quality System (AQS)",
  "description": "U.S. EPA repository of ambient air-pollution measurements and monitoring metadata, distributed as pre-generated CSV summary files (hourly, daily, annual) and via a public API.",
  "url": "https://www.epa.gov/aqs",
  "sameAs": "https://aqs.epa.gov/aqsweb/airdata/download_files.html",
  "license": "https://edg.epa.gov/EPA_Data_License.htm",
  "creator": {
    "@type": "Organization",
    "name": "U.S. Environmental Protection Agency, Office of Air Quality Planning and Standards (OAQPS)",
    "url": "https://www.epa.gov/aqs"
  },
  "datePublished": "2026-06-28",
  "version": "airdata-pregenerated",
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "daily_summary",
      "description": "One row per monitor/parameter/day daily summary.",
      "field": [
        { "@type": "cr:Field", "name": "State Code", "dataType": "Text" },
        { "@type": "cr:Field", "name": "Parameter Code", "dataType": "Text" },
        { "@type": "cr:Field", "name": "Date Local", "dataType": "Date" },
        { "@type": "cr:Field", "name": "Arithmetic Mean", "dataType": "Float" },
        { "@type": "cr:Field", "name": "Units of Measure", "dataType": "Text" },
        { "@type": "cr:Field", "name": "AQI", "dataType": "Integer" }
      ]
    }
  ]
}
```

---

## Validation script

Documentation only — this script validates the **structure** of a file the user has already
obtained themselves. It does **not** download, host, or redistribute any data.

```python
#!/usr/bin/env python3
"""Validate the structure of an AQS daily-summary CSV the user already has locally.
Reads only the header + a bounded sample. Does NOT download or republish data."""
import csv, sys

EXPECTED = [
    "State Code", "County Code", "Site Num", "Parameter Code", "POC",
    "Latitude", "Longitude", "Datum", "Parameter Name", "Sample Duration",
    "Pollutant Standard", "Date Local", "Units of Measure", "Event Type",
    "Observation Count", "Observation Percent", "Arithmetic Mean",
    "1st Max Value", "1st Max Hour", "AQI", "Method Code", "Method Name",
    "Local Site Name", "Address", "State Name", "County Name", "City Name",
    "CBSA Name", "Date of Last Change",
]
SAMPLE_CAP = 1000  # bounded read; never load the whole file

def main(path):
    with open(path, newline="", encoding="utf-8") as f:
        reader = csv.reader(f)
        header = next(reader)
        missing = [c for c in EXPECTED if c not in header]
        if missing:
            print("FAIL: missing columns:", missing); return 1
        rows = 0
        for i, row in enumerate(reader):
            if i >= SAMPLE_CAP:
                break
            if len(row) != len(header):
                print(f"FAIL: row {i} has {len(row)} cols, expected {len(header)}")
                return 1
            rows += 1
        print(f"OK: header valid; checked {rows} sample rows (cap {SAMPLE_CAP}).")
        return 0

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("usage: validate_aqs.py <local_daily_summary.csv>"); sys.exit(2)
    sys.exit(main(sys.argv[1]))
```

---

## Limitations & gaps

- **Field list verified from documentation, not from a live data sample.** Column order and
  types were taken from EPA's FileFormats.html; exact per-column null/blank conventions and
  the trailing geographic columns (positions 23–29 daily) should be reconfirmed against a
  real header before production parsing.
- **Code lists not enumerated:** Parameter Codes, Qualifier codes, Method Codes, Datum, and
  Event/Pollutant Standard vocabularies are large and live in the AQS Coding Manual / Data
  Dictionary; only representative values are noted here.
- **Multiple products exist** (hourly, daily, annual, 8-hour, blanks, etc.); only Daily
  Summary and Hourly schemas are documented above.
- **Licence:** confirmed public domain via the EPA Data License (17 U.S.C. § 105); the
  data.gov catalog metadata itself did not restate a licence name, so the EPA Data License
  page is the authoritative citation used here.
- **No PII:** the documented schema describes monitors and measurements only; no personal
  or identifying fields are present. No dataset records were hosted, mirrored, or committed.
```
