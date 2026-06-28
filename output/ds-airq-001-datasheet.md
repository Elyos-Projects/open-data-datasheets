# DRAFT — licence unverified

> **Why DRAFT:** OpenAQ is a **data aggregator**, not a single-licence publisher. Its Terms of
> Use state explicitly that OpenAQ does **not** impose one unified licence (e.g. it is *not*
> blanket CC-BY-4.0). Each underlying source carries its own licence — "Creative Commons
> licences or open government licences, and sometimes under bespoke terms" — surfaced per
> location via the API `licenses[]` array. Because some Creative Commons variants are
> **No-Derivatives (ND)** or **Non-Commercial (NC)**, derivative reuse **cannot be confirmed for
> the dataset as a whole**. The task's first-pass assumption ("CC-BY-4.0 — permits derivatives")
> did **not** survive verification. This datasheet is therefore released as a DRAFT for human
> review at the licence gate. See **Source licence** and **Limitations & gaps** below.

---

# Datasheet — OpenAQ global air-quality measurements

One-line summary: A documentation datasheet for OpenAQ's aggregated global air-quality station
measurements (PM2.5, PM10, NO2, O3, SO2, CO, BC and related parameters) accessed via the OpenAQ
open API — **documentation only; no data is hosted, mirrored, or transformed here.**

**Datasheet licence:** This datasheet (the document you are reading) is released under
**CC-BY-4.0**. This says nothing about the underlying data licence, which is addressed below.

---

## Provenance & attribution

| Field | Value |
|---|---|
| Publisher / aggregator | OpenAQ (OpenAQ Inc., a US 501(c)(3) non-profit) |
| Source URL | https://openaq.org/ |
| API documentation | https://docs.openaq.org/ |
| Terms of Use | https://docs.openaq.org/about/terms |
| Catalog id (candidate) | cat-airq-001 |
| Retrieval date | 2026-06-28 |
| Data nature | Aggregated readings from many third-party station networks worldwide |

**Required attribution (platform level):** OpenAQ's Terms require attribution to OpenAQ when its
services are used to access the data — e.g. *"Air-quality data accessed via OpenAQ
(https://openaq.org)."*

**Required attribution (source level):** In addition, each location/source carries its **own**
attribution string in the API response field `licenses[].attribution` and must be credited per
that source's licence. There is no single global attribution string that satisfies all sources.

---

## Source licence

**Verified finding (NOT a confirmation of derivative rights):**

- OpenAQ does **not** publish the aggregated dataset under one named licence. Per the Terms of
  Use (https://docs.openaq.org/about/terms), OpenAQ aggregates data that "to the best of our
  knowledge, has been made available for redistribution and use throughout the world," while
  **individual data providers retain their own licensing terms** ("Creative Commons licences or
  open government licences, and sometimes under bespoke terms").
- Users are "solely responsible for their use of the data and for compliance with any applicable
  laws and third-party terms."
- The machine-readable licence for any given series is exposed per location through the API in
  `location.licenses[]` with sub-fields `id`, `name`, `attribution`, `dateFrom`, `dateTo`.

**Derivatives permitted?** **UNCONFIRMED for the dataset as a whole.** Redistribution is broadly
asserted, but *derivative* rights and *commercial* rights vary by source and may be restricted
(ND/NC variants exist among the source licences). A blanket "permits derivatives" claim cannot be
cited to a single clause. Derivative reuse must be confirmed **per location** by reading that
location's `licenses[].name` and resolving it to its canonical licence deed before reuse.

**Licence snapshot (acceptance criterion):** A hash + archived copy of the *applicable* licence
text could not be produced because there is no single applicable licence text at the dataset
level; the correct artifact is a per-location capture of `licenses[]`. This is flagged for the
gate reviewer.

---

## Data dictionary

Fields below are verified from the OpenAQ API documentation
(https://docs.openaq.org/ — quick-start and locations resource). Rows describe the **locations**
resource and the per-measurement shape. Rows that could not be fully verified from the docs are
marked **(unverified)**.

### Location object

| Field | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| `id` | integer | — | Unique OpenAQ location id | positive int; not null |
| `name` | string | — | Station/location name | free text; may be null |
| `locality` | string | — | Locality/city label | free text; nullable |
| `timezone` | string | — | IANA timezone of the station | e.g. `America/New_York` |
| `country` | object | — | `{ id, code, name }` | ISO country code in `code` |
| `owner` | object | — | `{ id, name }` data owner | nullable |
| `provider` | object | — | `{ id, name }` upstream provider | not null |
| `isMobile` | boolean | — | Whether the sensor platform is mobile | true / false |
| `isMonitor` | boolean | — | True = reference monitor; false = low-cost sensor | true / false |
| `coordinates` | object | degrees | `{ latitude, longitude }` (WGS84) | numeric; lat [-90,90], lon [-180,180] |
| `bounds` | array | degrees | Bounding box coordinate array | numeric array; nullable |
| `distance` | number | metres | Distance from query point (only on radius queries) | nullable |
| `instruments` | array | — | `[{ id, name }]` measuring instruments | possibly empty |
| `sensors` | array | — | `[{ id, name, parameter }]` sensors at location | possibly empty |
| `sensors[].parameter` | object | varies | `{ id, name, units, displayName }` | see parameters table |
| `licenses` | array | — | `[{ id, name, attribution, dateFrom, dateTo }]` per-source licence | may be null/empty |
| `datetimeFirst` | object | — | `{ utc, local }` first observation (ISO 8601) | nullable |
| `datetimeLast` | object | — | `{ utc, local }` last observation (ISO 8601) | nullable |

### Measurement / sensor reading (shape per docs)

| Field | Type | Units | Description | Allowed values / nulls |
|---|---|---|---|---|
| `value` | number | parameter units | Measured concentration | numeric; provider may emit sentinel/negative QA values **(unverified handling)** |
| `parameter` | object | varies | `{ id, name, units, displayName }` | see parameters table |
| `datetime` / `period` | object | — | Observation time `{ utc, local }` and aggregation period **(unverified exact key names for /measurements vs /sensors)** | ISO 8601 |
| `coordinates` | object | degrees | `{ latitude, longitude }` for the reading | nullable for mobile |
| `coverage` | object | — | Aggregation coverage `{ expectedCount, observedCount, ... }` **(unverified field set)** | nullable |

### Parameters (pollutants) — verified from openaq.org station example

| Parameter (`name`) | Typical `units` | Description |
|---|---|---|
| `pm25` | µg/m³ | Fine particulate matter ≤2.5µm |
| `pm10` | µg/m³ | Particulate matter ≤10µm |
| `so2` | ppb | Sulfur dioxide |
| `o3` | ppb | Ozone |
| `co` | ppb | Carbon monoxide |
| `no2` | ppb | Nitrogen dioxide |
| `bc` | µg/m³ | Black carbon |

> Units shown are those displayed by OpenAQ for the example station; OpenAQ may also serve some
> parameters in alternative units (e.g. ppm, particle counts). Always read `parameter.units` from
> the response rather than assuming. The full parameter catalogue is larger than the seven above
> **(remaining parameters unverified here)**.

---

## Datasheet for Datasets

**Motivation.** Created so that anyone can access comparable air-quality measurements worldwide
from a single open API, supporting public-health research, civic tech, journalism, and policy.
OpenAQ aggregates rather than originates the measurements.

**Composition.** Instances are time-stamped pollutant concentration readings tied to a
geolocated station (reference monitor or low-cost sensor) with parameter, value, units, and
coordinates. No human-subject or personal data is intended; instances describe environmental
sensors, not people. Station metadata coverage is **uneven** across providers.

**Collection process.** Measurements are produced by third-party networks (government reference
monitors, research deployments, low-cost sensor fleets) and ingested by OpenAQ via provider
feeds. OpenAQ standardises structure but data quality/cadence varies by source. Sensors are
flagged `isMonitor` (reference) vs low-cost; treat them differently in analysis.

**Preprocessing / cleaning.** OpenAQ normalises parameters, units, timestamps (UTC + local), and
geolocation into a common schema, and attaches source licence metadata. It does not guarantee
correction of provider-side errors; QA/sentinel/negative values can appear and should be filtered
by the user **(exact null/QA convention unverified)**.

**Uses.** Air-quality monitoring, exposure and epidemiology research, model training/validation,
public dashboards, and journalism. Not suitable as a regulatory system of record; not a
substitute for official agency data where legally required.

**Distribution.** Distributed by OpenAQ via its open REST API (https://docs.openaq.org/) and an
"Open data on AWS" bucket. **This datasheet does not redistribute any data.** Reuse is subject to
each source's licence (see Source licence).

**Maintenance.** Maintained by OpenAQ Inc. The dataset is continuously updated as providers feed
new readings; historical series carry `datetimeFirst`/`datetimeLast`. Per-source `licenses[]`
entries carry `dateFrom`/`dateTo` validity windows.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "data": "cr:data",
    "dataType": "cr:dataType",
    "field": "cr:field",
    "recordSet": "cr:recordSet"
  },
  "@type": "Dataset",
  "name": "OpenAQ global air-quality measurements",
  "description": "Aggregated global air-quality station measurements (PM2.5, PM10, NO2, O3, SO2, CO, BC and related parameters) collected by third-party networks and served via the OpenAQ open API. Licensing is per-source and heterogeneous; derivative rights are not guaranteed dataset-wide.",
  "url": "https://openaq.org/",
  "sameAs": "https://docs.openaq.org/",
  "license": "https://docs.openaq.org/about/terms",
  "creator": {
    "@type": "Organization",
    "name": "OpenAQ Inc.",
    "url": "https://openaq.org/"
  },
  "datePublished": "2026-06-28",
  "version": "draft-2026-06-28",
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "measurement",
      "description": "A single pollutant reading at a station.",
      "field": [
        { "@type": "cr:Field", "name": "parameter", "description": "Pollutant code, e.g. pm25", "dataType": "Text" },
        { "@type": "cr:Field", "name": "value", "description": "Measured concentration", "dataType": "Float" },
        { "@type": "cr:Field", "name": "units", "description": "Units of value, e.g. ug/m3 or ppb", "dataType": "Text" },
        { "@type": "cr:Field", "name": "datetimeUtc", "description": "Observation timestamp (UTC, ISO 8601)", "dataType": "DateTime" },
        { "@type": "cr:Field", "name": "latitude", "description": "WGS84 latitude", "dataType": "Float" },
        { "@type": "cr:Field", "name": "longitude", "description": "WGS84 longitude", "dataType": "Float" }
      ]
    }
  ]
}
```

> Note: `license` here points to OpenAQ's Terms of Use rather than a single SPDX licence
> identifier, because no single dataset-wide licence exists. A schema-valid record can be
> produced, but it should not assert a derivative-permitting SPDX id (e.g. `CC-BY-4.0`) that the
> sources do not uniformly grant.

---

## Validation script

This script validates the **structure** of a user-provided sample that the user has already
obtained themselves under the applicable licence. It does **not** download, host, or mirror any
OpenAQ data.

```python
#!/usr/bin/env python3
"""
Validate the STRUCTURE of an OpenAQ measurements sample (JSON the user fetched themselves).
Documentation/validation only: this script never downloads or republishes data.
Usage: python validate_openaq.py sample.json
"""
import json
import sys

# Fields we expect to verify against the datasheet's data dictionary.
EXPECTED_LOCATION_KEYS = {
    "id", "name", "coordinates", "sensors", "licenses",
    "datetimeFirst", "datetimeLast", "country", "provider",
}
EXPECTED_PARAM_KEYS = {"id", "name", "units"}
KNOWN_PARAMS = {"pm25", "pm10", "so2", "o3", "co", "no2", "bc"}
MAX_SAMPLE_ROWS = 1000  # bounded-access protocol: refuse oversized samples

def fail(msg):
    print(f"FAIL: {msg}")
    sys.exit(1)

def main(path):
    with open(path, "r", encoding="utf-8") as fh:
        doc = json.load(fh)

    results = doc.get("results", doc if isinstance(doc, list) else [])
    if not isinstance(results, list):
        fail("expected a list of results (or a {'results': [...]} envelope)")
    if len(results) > MAX_SAMPLE_ROWS:
        fail(f"sample has {len(results)} rows; exceeds {MAX_SAMPLE_ROWS}-row bound")

    for i, loc in enumerate(results):
        missing = EXPECTED_LOCATION_KEYS - set(loc)
        if missing:
            print(f"WARN row {i}: missing location keys {sorted(missing)}")
        coords = loc.get("coordinates") or {}
        lat, lon = coords.get("latitude"), coords.get("longitude")
        if lat is not None and not (-90 <= lat <= 90):
            fail(f"row {i}: latitude {lat} out of range")
        if lon is not None and not (-180 <= lon <= 180):
            fail(f"row {i}: longitude {lon} out of range")
        for s in loc.get("sensors", []) or []:
            p = s.get("parameter") or {}
            if EXPECTED_PARAM_KEYS - set(p):
                print(f"WARN row {i}: sensor parameter missing keys")
            if p.get("name") and p["name"] not in KNOWN_PARAMS:
                print(f"INFO row {i}: parameter '{p['name']}' not in known-7 set")
        if not loc.get("licenses"):
            print(f"WARN row {i}: no per-source licence metadata present")

    print(f"OK: structure validated for {len(results)} record(s).")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        fail("usage: python validate_openaq.py sample.json")
    main(sys.argv[1])
```

To validate row counts / coverage you can additionally check `meta.found` against
`len(results)` in the API envelope — again on a sample you fetched yourself.

---

## Limitations & gaps

- **Licence not verified for derivatives (primary gap).** OpenAQ imposes no single dataset-wide
  licence; rights are per-source and include potentially ND/NC terms. The first-pass CC-BY-4.0
  assumption was **not confirmed**. Derivative/commercial reuse must be checked per location via
  `licenses[]`. This file is consequently a DRAFT for gate review.
- **Licence snapshot artifact incomplete.** A single hash/archived licence text could not be
  produced (no single applicable licence); the correct artifact is a per-location `licenses[]`
  capture, which requires querying specific locations.
- **Field schema partially unverified.** The exact key names and field sets for the
  `/measurements`, `/sensors`, `coverage`, and `period` objects were not fully confirmed from the
  docs excerpt and are marked **(unverified)** above. The locations object is well verified.
- **Parameter list incomplete.** Only the seven parameters from the public station example are
  listed; OpenAQ serves more, and units can differ per series — always read `parameter.units`.
- **Null / QA conventions unverified.** Handling of sentinel, negative, or missing values is
  provider-dependent and was not confirmed.
- **No data accessed.** No sample rows were fetched, hosted, mirrored, or transformed in
  producing this datasheet (documentation-only guardrail honoured). No personal/identifying data
  is present in this dataset by design.
