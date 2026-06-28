# TASKS — open-data-datasheets

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## How these tasks map to Elyos

Each task below becomes an Elyos **Task JSON** validated against
`packages/schema/src/schemas.ts`. Mapping of fields:

- `id` — stable slug ID from the tables (e.g. `open-data-datasheets-template-001`).
- `title` — the table's Title.
- `project` — `open-data-datasheets`.
- `type` — one of `code | research | writing | data | design-spec | maintenance` (see each table).
- `lane` — `donated` for all tasks here (no funded escrow). Funded tasks would add `fundedBudgetUsd`.
- `priority` — `high | medium | low`.
- `domain` — array, e.g. `["public-data","open-science","civic"]`.
- `riskTier` — `low | medium | high`. License/PII-judgement and sensitive-domain tasks are `medium`.
- `urgent` — boolean; `false` for all current tasks.
- `deliverable` — `pr | dataset | document | translation`. We never deliver `dataset` (data is out of
  scope); code → `pr`, docs/metadata → `document`.
- `tokenEstimate` — `small | medium | large` (Size column).
- `status` — `open | in-progress | review | delivered | done`; all start `open`.
- `context`, `objective`, `acceptanceCriteria[]`, `resources[]`, `output` — per task.
- `requestor` — TO BE SECURED until a partner is confirmed.
- `verifiedNeed` — **`false`** until a named portal/maintainer agrees to accept contributions
  (general need is real, but per-task delivery need is unproven).
- `outputLicense` — `CC-BY-4.0` for documentation/metadata; `MIT` for code (validators/adapters).

---

## Milestone M0 — Foundation & cold-start

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| open-data-datasheets-template-001 | Documentation template + canonical metadata model | writing | small | low | document | — | Technical |
| open-data-datasheets-gate-002 | License + PII triage checklist (blocking gate) | design-spec | small | medium | document | — | License+PII |
| open-data-datasheets-croissant-003 | Croissant ML metadata generator + spec validator | code | medium | low | pr | template-001 | Technical |
| open-data-datasheets-validator-004 | Reusable dataset validation script + quality report | code | small | low | pr | template-001 | Technical |
| open-data-datasheets-pilot-005 | End-to-end documentation for one pilot dataset | data | medium | medium | document | template-001, gate-002, croissant-003, validator-004 | License+PII, Technical |
| open-data-datasheets-outreach-006 | Partner/portal outreach + candidate dataset shortlist | research | small | low | document | — | Maintainer |

**Acceptance criteria — key tasks**

- **template-001 (template + canonical model)**
  - [ ] Canonical metadata model documented with every field from PLAN (license, provenance, pii,
        fields[], knownIssues, examples).
  - [ ] Markdown template covers data dictionary, provenance, license record, known-issues, examples,
        and the Datasheets-for-Datasets questionnaire.
  - [ ] Explicitly states deliverable is documentation, not data; output licensed CC-BY-4.0.
  - [ ] At least one filled-in worked example skeleton included.

- **gate-002 (license + PII gate)**
  - [ ] Checklist enumerates accepted licenses (OGL, CC0, CC-BY) and case-by-case/excluded ones.
  - [ ] Requires recording license id + URL + text snapshot reference and an explicit
        permits-derivatives boolean.
  - [ ] PII triage section: direct identifiers + quasi-identifiers; exclude unless publisher-documented
        anonymization; never anonymize ourselves.
  - [ ] Produces a committed, reviewable PASS/FLAG/EXCLUDE artifact per dataset.

- **pilot-005 (pilot dataset, end-to-end)**
  - [ ] Dataset passed gate-002 (license permits reuse+derivatives; no unanonymized PII) with the
        artifact committed.
  - [ ] Complete data dictionary, Datasheet, and valid Croissant metadata produced.
  - [ ] Validation script runs clean in CI and emits a quality report.
  - [ ] Provenance recorded (source URL, publisher, retrieval date, version, attribution).
  - [ ] Documentation **submitted** to the dataset's portal/repo (acceptance may be pending).

**M0 Definition of Done:** template + canonical model + license/PII gate published; Croissant
generator and one validation script green in CI; one pilot dataset documented end-to-end and
submitted upstream; ≥ 1 partner-outreach thread opened.

---

## Milestone M1 — License/provenance gate hardened + first acceptances

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| open-data-datasheets-snapshot-007 | License-text snapshot capture in provenance flow | code | small | low | pr | template-001, gate-002 | Technical |
| open-data-datasheets-triage-008 | Triage 5 candidate datasets through the gate | research | medium | medium | document | gate-002, outreach-006 | License+PII |
| open-data-datasheets-doc-009 | Full documentation for accepted dataset #2 | data | medium | medium | document | pilot-005, triage-008 | License+PII, Technical |
| open-data-datasheets-doc-010 | Full documentation for accepted dataset #3 | data | medium | medium | document | pilot-005, triage-008 | License+PII, Technical |
| open-data-datasheets-partner-011 | Secure first confirmed contribution partner | research | small | low | document | outreach-006 | Steward |

**Acceptance criteria — key tasks**

- **triage-008 (triage 5 candidates)**
  - [ ] Five datasets evaluated with a committed gate artifact each (PASS/FLAG/EXCLUDE + rationale).
  - [ ] Each PASS records license id/URL/snapshot and permits-derivatives = true.
  - [ ] Any PII or unclear-license datasets are FLAGGED/EXCLUDED with the concern surfaced.

- **partner-011 (first confirmed partner)**
  - [ ] A named portal/maintainer confirms they will review and accept contributed documentation.
  - [ ] Contribution mechanism documented (PR vs. portal API vs. email).
  - [ ] Tasks for that partner updated to `verifiedNeed: true` with `requestor` set.

**M1 Definition of Done:** gate applied to ≥ 3 datasets with committed artifacts; ≥ 2 datasets
accepted onto a portal/repo; ≥ 1 confirmed partner; license-snapshot capture working.

---

## Milestone M2 — Portal adapters & scale

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| open-data-datasheets-ckan-012 | CKAN package metadata adapter | code | medium | low | pr | croissant-003 | Technical |
| open-data-datasheets-socrata-013 | Socrata dataset metadata adapter | code | medium | low | pr | croissant-003 | Technical |
| open-data-datasheets-dcat-014 | data.gov / DCAT-US metadata adapter | code | medium | low | pr | croissant-003 | Technical |
| open-data-datasheets-doc-015 | Documentation for datasets #4 and #5 via adapters | data | large | medium | document | ckan-012, socrata-013, partner-011 | License+PII, Technical |

**Acceptance criteria — key tasks**

- **ckan-012 (CKAN adapter)**
  - [ ] Transforms canonical metadata into a valid CKAN package payload.
  - [ ] Output verified against a real CKAN portal's import schema (or documented sample).
  - [ ] Code MIT-licensed; unit tests + CI green; no credentials embedded.

- **doc-015 (datasets #4 and #5)**
  - [ ] Both datasets pass the gate with committed artifacts.
  - [ ] Metadata emitted via the relevant portal adapter and accepted upstream.
  - [ ] Per-dataset effort recorded to show reduction vs. M0/M1 baseline.

**M2 Definition of Done:** ≥ 2 portal adapters emitting valid portal-native metadata; ≥ 5 datasets
accepted cumulatively; measurable per-dataset effort reduction.

---

## Milestone M3 — Reuse outcomes & sustainability

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| open-data-datasheets-reuse-016 | Track and verify external reuse events | research | small | low | document | doc-009, doc-010, doc-015 | Steward |
| open-data-datasheets-refresh-017 | Staleness/refresh process + drift detection | maintenance | small | low | document | validator-004 | Maintainer |
| open-data-datasheets-scale-018 | Documentation for datasets #6–#8 | data | large | medium | document | doc-015, refresh-017 | License+PII, Technical |

**Acceptance criteria — key tasks**

- **reuse-016 (reuse tracking)**
  - [ ] ≥ 3 verifiable external reuse events recorded (citation/portal acceptance/PR reference).
  - [ ] Each event links to externally verifiable evidence (no self-reported reuse).

- **refresh-017 (staleness/refresh)**
  - [ ] Documented process to detect when a documented dataset has drifted from its recorded version.
  - [ ] Validation script flags schema drift; stale docs become `maintenance` tasks.

**M3 Definition of Done:** ≥ 3 verifiable reuse events; ≥ 8 datasets accepted cumulatively;
maintenance/refresh process documented and steward identified.

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| open-data-datasheets-hf-019 | Hugging Face dataset-card / metadata adapter | code | medium | low | pr | If HF datasets enter scope |
| open-data-datasheets-zenodo-020 | Zenodo metadata adapter + DOI provenance | code | medium | low | pr | For archived/citable datasets |
| open-data-datasheets-i18n-021 | Translate a delivered Datasheet (domain reviewer) | translation | small | medium | translation | Widens reuse; needs language reviewer |
| open-data-datasheets-policy-022 | NC / share-alike acceptance policy for derivative metadata | design-spec | small | medium | document | Resolves an open question; License+PII review |
| open-data-datasheets-dash-023 | Outcome dashboard for accepted docs + reuse events | code | medium | low | pr | Supports success-metric tracking |

---

## Example task JSON

```json
{
  "id": "open-data-datasheets-template-001",
  "title": "Documentation template + canonical metadata model",
  "project": "open-data-datasheets",
  "type": "writing",
  "lane": "donated",
  "priority": "high",
  "domain": ["public-data", "open-science", "civic"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "small",
  "status": "open",
  "context": "Public open datasets are often unusable because they lack data dictionaries, provenance, clear licensing, and machine-readable metadata. Before documenting any specific dataset, the project needs one reusable template and a canonical metadata model that all other outputs (Datasheet, Croissant ML metadata, portal-specific metadata) are projections of. Deliverable is documentation, never the data.",
  "objective": "Create the reusable documentation template and the canonical metadata model that every per-dataset task will use.",
  "acceptanceCriteria": [
    "Canonical metadata model documents all fields: title, publisher, sourceUrl, license {id, url, permitsDerivatives, snapshotRef}, provenance {retrievedAt, version, updateCadence, attribution}, pii {present, anonymized, notes}, fields[] {name, type, units, allowedValues, nullable, description, caveats}, knownIssues[], examples[].",
    "Markdown template covers data dictionary, provenance record, license record, known-issues, worked examples, and the full Datasheets-for-Datasets questionnaire.",
    "Template explicitly states the deliverable is documentation, not data, and that documentation output is licensed CC-BY-4.0.",
    "At least one filled-in worked example skeleton is included to guide contributors.",
    "pnpm build && pnpm test && pnpm lint pass for any committed tooling; commit is DCO signed-off."
  ],
  "resources": [
    "C:\\code\\elyos\\planning\\projects\\open-data-datasheets\\PLAN.md",
    "C:\\code\\elyos\\governance\\proposals\\open-data-datasheets.md",
    "Datasheets for Datasets (Gebru et al.)",
    "Croissant ML metadata specification"
  ],
  "output": "A documentation template plus a canonical metadata model definition, committed to the project repo and ready for reuse by per-dataset documentation tasks.",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "CC-BY-4.0"
}
```
