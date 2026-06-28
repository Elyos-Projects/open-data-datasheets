# Datasheet — UK Election Results (UK Electoral Commission)

> One-line summary: A documentation datasheet for the UK Electoral Commission's published
> election results and turnout data (UK-wide constituency- and candidate-level results),
> released under the Open Government Licence v3.0.

*This datasheet (the documentation in this file) is licensed under **CC-BY-4.0**. It documents,
but does not contain, host, mirror, or redistribute, the underlying dataset.*

**Task:** ds-elections-002 · **Catalog id:** cat-elections-002 · **Prepared:** 2026-06-28

---

## Provenance & attribution

| Field | Value |
| --- | --- |
| Publisher / source | UK Electoral Commission |
| Source landing page | https://www.electoralcommission.org.uk/research-reports-and-data |
| Dataset family | Election results and turnout (e.g. 2024 UK Parliamentary general election results by constituency / by candidate) |
| Retrieval date | 2026-06-28 |
| Access note | The Electoral Commission web domain returned HTTP 403 to automated fetch on the retrieval date; structure below was corroborated from secondary public documentation (data.gov.uk "Election results" collection; House of Commons Library general election 2024 results briefing). See **Limitations & gaps**. |

**Required attribution string (per OGL v3.0):**

> "Contains public sector information licensed under the Open Government Licence v3.0."

Where the Information Provider specifies its own wording, the Electoral Commission's
attribution should be used; otherwise the standard OGL statement above applies.

---

## Source licence

| Item | Value |
| --- | --- |
| Licence name | Open Government Licence (OGL) v3.0 |
| Licence URL | https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/ |
| Permits derivatives? | **Yes — confirmed** |
| Confirming clause | The OGL v3.0 "You are free to" section grants the right to *"copy, publish, distribute and transmit the Information; **adapt the Information**; exploit the Information commercially and non-commercially **for example, by combining it with other Information**, or by including it in your own product or application."* The right to *adapt* and *combine* the Information confirms derivative works are permitted. |
| Confirmation that this dataset is OGL v3.0 | The data.gov.uk "Election results" collection (which presents the UK Parliamentary election results) states: *"All content is available under the Open Government Licence v3.0, except where otherwise stated."* (https://www.data.gov.uk/collections/government/election-results) |
| Key condition | Attribution is mandatory; rights terminate automatically on failure to attribute. |

> Note on a related source: The UK Parliament results portal (electionresults.parliament.uk)
> publishes overlapping results under the **Open Parliament Licence**, not OGL. This datasheet
> documents the **Electoral Commission** release under **OGL v3.0**. If a downstream user mixes
> the two, each source's licence and attribution must be honoured separately.

Licence status for this datasheet: **VERIFIED — OGL v3.0 permits derivatives.** (Not a DRAFT.)

---

## Data dictionary

Scope: UK Parliamentary general election results as published by the Electoral Commission,
typically distributed as one or more spreadsheet/CSV files at two grains — **results by
constituency** and **results by candidate**.

Verification legend: **[S]** = field corroborated from secondary public documentation
(data.gov.uk collection, House of Commons Library 2024 results briefing); **[U]** = name/type
**unconfirmed** against the Electoral Commission's own file headers (source page was 403 on the
retrieval date — treat exact column spellings, types and null handling as provisional).

### Grain A — Results by constituency

| Field (provisional) | Type | Units | Description | Allowed values / nulls |
| --- | --- | --- | --- | --- |
| Constituency name | string | — | Name of the Parliamentary constituency. **[S]** | Non-null; one row per constituency. **[U]** |
| Constituency / ONS code | string | — | Standard geographic code (e.g. ONS GSS code) identifying the constituency. **[U]** | Expected non-null; format unconfirmed. **[U]** |
| Country / region | string | — | Country (England/Scotland/Wales/NI) or region of the constituency. **[U]** | Controlled vocabulary; unconfirmed. **[U]** |
| Electorate | integer | persons | Number of registered electors eligible to vote. **[S]** | Non-negative integer. **[U]** |
| Valid votes / total votes | integer | votes | Count of valid votes cast. **[S]** | Non-negative integer. **[U]** |
| Turnout | decimal | percent (or ratio) | Turnout = valid votes / electorate. **[S]** | 0–100 (or 0–1); unit unconfirmed. **[U]** |
| Votes per party (one column per party, e.g. Con/Lab/LD/...) | integer | votes | Votes won by each party in the constituency. **[S]** | Non-negative integer; blank/0 where party did not stand. **[U]** |
| Vote share per party | decimal | percent | Each party's share of valid votes. **[S]** | 0–100; unit unconfirmed. **[U]** |
| Winning party / result | string | — | Party that won the seat. **[S]** | Registered party name; unconfirmed vocabulary. **[U]** |

### Grain B — Results by candidate

| Field (provisional) | Type | Units | Description | Allowed values / nulls |
| --- | --- | --- | --- | --- |
| Constituency name / code | string | — | Constituency the candidacy belongs to. **[S]** | Non-null. **[U]** |
| Candidate name | string | — | Name of the standing candidate (public electoral record). **[S]** | Non-null. **[U]** |
| Party / description | string | — | Registered party (or "Independent") under which the candidate stood. **[S]** | Registered party name or Independent. **[U]** |
| Votes | integer | votes | Votes received by the candidate. **[S]** | Non-negative integer. **[U]** |
| Vote share | decimal | percent | Candidate's share of valid votes in the constituency. **[S]** | 0–100. **[U]** |
| Elected flag | boolean | — | Whether the candidate was elected. **[U]** | true/false (or Y/N); unconfirmed. **[U]** |

PII note: candidate names appearing on a public ballot are part of the **public electoral
record**, not private personal data. No private/identifying voter-level fields exist in or are
documented from this dataset; aggregate results only.

---

## Datasheet for Datasets

**Motivation.** Created by the UK Electoral Commission (the independent elections regulator) to
publish official, authoritative results and turnout for UK elections, supporting transparency,
public accountability, research and democratic scrutiny.

**Composition.** Aggregate electoral outcomes at constituency and candidate grain: electorate,
votes, turnout, per-party and per-candidate vote counts and shares, and the winning result. No
individual voter records; candidate identities are public electoral information.

**Collection process.** Results are the official counts certified by Returning Officers for each
constituency, consolidated and published by the Electoral Commission. The data reflects the
administrative count of cast ballots, not a sample or survey.

**Preprocessing / cleaning.** Counts are consolidated into standardised tabular form (per
constituency / per candidate). Exact transformations (code joins, party-name normalisation)
are not documented here as the source documentation could not be retrieved on 2026-06-28.

**Uses.** Psephological and political-science research; journalism; civic dashboards;
combining with boundary/demographic data (OGL expressly permits combination). Should not be
used to infer individual voter behaviour — the data is aggregate only.

**Distribution.** Published openly by the Electoral Commission (and mirrored via data.gov.uk)
under OGL v3.0, typically as spreadsheet/CSV downloads. This datasheet does not redistribute
the data; consult the source landing page for the authoritative files.

**Maintenance.** Maintained by the UK Electoral Commission; updated as new elections occur and
official results are certified. Refer to the source page for the current authoritative version
and any corrections.

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
  "name": "UK Election Results (Electoral Commission)",
  "description": "Official UK election results and turnout published by the UK Electoral Commission, at constituency and candidate grain (electorate, votes, turnout, per-party/per-candidate vote counts and shares). Documentation datasheet; data not hosted here.",
  "url": "https://www.electoralcommission.org.uk/research-reports-and-data",
  "license": "https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/",
  "creator": {
    "@type": "Organization",
    "name": "UK Electoral Commission",
    "url": "https://www.electoralcommission.org.uk/"
  },
  "datePublished": "2024",
  "dateModified": "2026-06-28",
  "citation": "Contains public sector information licensed under the Open Government Licence v3.0.",
  "recordSet": [
    {
      "@type": "cr:RecordSet",
      "name": "results_by_constituency",
      "description": "One row per Parliamentary constituency (provisional field set; see datasheet).",
      "field": [
        { "@type": "cr:Field", "name": "constituency_name", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "constituency_code", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "electorate", "dataType": "sc:Integer" },
        { "@type": "cr:Field", "name": "valid_votes", "dataType": "sc:Integer" },
        { "@type": "cr:Field", "name": "turnout_pct", "dataType": "sc:Float" }
      ]
    },
    {
      "@type": "cr:RecordSet",
      "name": "results_by_candidate",
      "description": "One row per candidacy (provisional field set; see datasheet).",
      "field": [
        { "@type": "cr:Field", "name": "constituency_name", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "candidate_name", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "party", "dataType": "sc:Text" },
        { "@type": "cr:Field", "name": "votes", "dataType": "sc:Integer" },
        { "@type": "cr:Field", "name": "vote_share_pct", "dataType": "sc:Float" }
      ]
    }
  ]
}
```

---

## Validation script

Documentation only. This script does **not** download, mirror, or host the dataset. Point it at
a locally-obtained copy (CSV) to check that the expected structure is present. Keep any local
copy ephemeral and local-only.

```python
#!/usr/bin/env python3
"""Structural check for a locally-held UK election results CSV (Electoral Commission, OGL v3.0).
Does NOT fetch or host data. Usage: python validate.py results_by_constituency.csv
Field names are PROVISIONAL (source headers unconfirmed on 2026-06-28) -- adjust to match the
actual file before relying on the result."""
import csv, sys

# Provisional expected columns (constituency grain). Edit to match the real header row.
EXPECTED = {"constituency_name", "electorate", "valid_votes", "turnout"}
MIN_ROWS = 600   # UK has ~650 Parliamentary constituencies; sanity floor, not exact.

def main(path):
    with open(path, newline="", encoding="utf-8-sig") as f:
        reader = csv.DictReader(f)
        header = {(h or "").strip().lower().replace(" ", "_") for h in (reader.fieldnames or [])}
        rows = sum(1 for _ in reader)

    missing = EXPECTED - header
    print(f"columns found : {len(header)}")
    print(f"rows (data)   : {rows}")
    if missing:
        print(f"WARN missing expected columns (names provisional): {sorted(missing)}")
    if rows < MIN_ROWS:
        print(f"WARN row count {rows} below sanity floor {MIN_ROWS}")
    ok = not missing and rows >= MIN_ROWS
    print("PASS" if ok else "REVIEW: structure did not match provisional expectations")
    sys.exit(0 if ok else 1)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        sys.exit("usage: python validate.py <local_results.csv>")
    main(sys.argv[1])
```

---

## Limitations & gaps

- **Source page not machine-retrievable on 2026-06-28:** electoralcommission.org.uk returned
  HTTP 403 to automated fetch, so exact file URLs, column headers, data types, units (percent
  vs ratio), null handling, and row counts could **not** be verified against the source files.
  All data-dictionary rows are marked **[U]** (unconfirmed) accordingly and should be reconciled
  against the actual published file headers before downstream use.
- **Field set is provisional and corroborated from secondary documentation** (data.gov.uk
  "Election results" collection and the House of Commons Library 2024 general election results
  briefing), not from the Electoral Commission's own file headers.
- **Licence is verified** (OGL v3.0 permits adaptation/derivatives — National Archives clause
  cited; data.gov.uk confirms the collection is OGL v3.0). A licence-text hash/archived snapshot
  was not captured here because the live OGL page was the only authoritative copy fetched;
  recommend archiving the licence text at gate time per acceptance criteria.
- **Related but distinct source:** electionresults.parliament.uk publishes overlapping data
  under the **Open Parliament Licence**; do not conflate its terms with OGL v3.0.
- **No PII / no data hosted:** only aggregate results and public-record candidate names are
  documented; no actual dataset rows are included or redistributed.
