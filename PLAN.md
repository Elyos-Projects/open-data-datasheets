# PLAN — open-data-datasheets

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## Executive summary

High-value public open datasets are frequently published with little to no usable documentation:
no data dictionary, no provenance trail, ambiguous licensing, and no machine-readable metadata.
The data is technically "open" but practically unusable — reusers cannot tell what a column means,
whether the license permits derivatives, how current the data is, or whether it contains personal
information. This project produces standardized, source-verified **documentation and metadata** for
such datasets — data dictionaries, "Datasheets for Datasets", Croissant ML metadata, provenance and
license records, and small validation scripts — and contributes them back to the dataset's portal
or repository.

The **deliverable is documentation, not the data**. We never republish, mirror, or transform the
underlying data; we describe it. Each dataset is a self-contained unit of work suitable for a single
donated AI session plus human review. The hard constraint and central design principle is the
**license gate**: every dataset is verified to permit reuse and derivative metadata (OGL, CC-BY,
CC0, or equivalent) before any documentation work begins, and any dataset with unclear terms or
unanonymized personal/identifying data is flagged and excluded rather than guessed at.

Risk tier is **low–medium**. The primary risks are not technical but factual and legal: misstating
what a dataset contains, mischaracterizing a license, or documenting a dataset that should never
have been in scope (PII). The plan front-loads license/provenance/PII review as a hard gate.

## Problem & beneficiaries

**Who is helped.** Researchers, data journalists, civic-tech groups, students, and downstream data
portals — anyone who wants to reuse a public dataset but is blocked by missing documentation.
Improving documentation also helps the original publishing body (often a government or public
institution) by increasing the verifiable, attributed reuse of data they already paid to collect.

**The verified need.** Poor documentation is widely cited as the single largest barrier to reuse of
open data. The proposal asserts this need as verified. We treat the *general* need as well
established, but the **per-dataset, per-partner need is TO BE SECURED**: we have not yet confirmed a
named portal or publisher who has agreed to accept contributed documentation. Until a specific
portal/maintainer confirms they will review and accept contributions, individual tasks carry
`verifiedNeed: false`. This honesty matters because "delivered, not merged" requires the output to
actually be accepted by a beneficiary, not merely produced.

**Partner org.** TO BE SECURED. Candidate channels include CKAN-based national/municipal portals,
Socrata-based city portals, data.gov dataset maintainers, and dataset repositories on GitHub/Hugging
Face/Zenodo. M0 includes explicit partner-outreach work; no partner is assumed.

## Goals and non-goals

**Goals**
- Produce a reusable, standards-aligned documentation template and toolkit (data dictionary,
  provenance record, license record, known-issues, examples, Datasheet, Croissant metadata).
- For each in-scope dataset, deliver complete, source-verified documentation + machine-readable
  metadata that measurably improves reuse.
- Make license and provenance verification a non-skippable, auditable gate.
- Provide small, dependency-light validation scripts that let any reuser re-check the dataset
  against its documented schema.
- Provide portal-contribution adapters (CKAN/Socrata/data.gov) so metadata lands in the right
  format on the right portal.

**Non-goals**
- We do **not** host, mirror, clean, transform, or republish the underlying data.
- We do **not** create datasets, scrape data, or generate synthetic data.
- We do **not** document datasets with unclear licenses or unanonymized PII — these are flagged and
  excluded, not "best-guessed."
- We do **not** provide analytical conclusions, rankings, or interpretation of the data's meaning.
- We do **not** auto-publish to portals; a human submits/contributes after review.

## Success metrics (outcomes)

Outcome-based, beneficiary-centric. Vanity metrics (e.g., "docs written") are explicitly excluded.

| Metric | Baseline | Target (first 6 months) |
| --- | --- | --- |
| Datasets with documentation **accepted onto the source portal/repo** (last-mile delivered) | 0 | 8 accepted |
| Datasets passing the license+provenance+PII gate / total triaged | n/a | ≥ 95% of *triaged-in* datasets have a recorded, verifiable license |
| Reuse signal: documented datasets cited/forked/referenced by a third party | 0 | ≥ 3 with a verifiable external reuse event |
| Confirmed contribution partners (portals/maintainers accepting contributions) | 0 | ≥ 2 secured |
| Documentation defects found in human/expert review (factual or license errors) | n/a | < 1 license/PII error per 10 delivered (target: 0 PII/license errors) |
| Reusable template + Croissant validator adopted across tasks | n/a | 100% of delivered datasets use the standard template |

Note on attribution of outcomes: a "reuse event" must be externally verifiable (a citation, a
portal acceptance record, an issue/PR referencing the docs). Self-reported reuse does not count.

## Scope

**In scope**
- Documentation artifacts: data dictionary, provenance record, license record, known-issues,
  worked examples, Datasheet-for-Datasets, Croissant ML metadata (JSON-LD).
- Small validation scripts (schema/type/row-count/null checks) emitting a data-quality report.
- Portal-contribution adapters that emit portal-native metadata (CKAN package, Socrata dataset
  metadata, data.gov / DCAT-US fields) from our canonical metadata.
- License, provenance, and PII triage and recording for each candidate dataset.

**Out of scope**
- The data itself (no hosting/mirroring/transformation/cleaning/republishing).
- Datasets with unclear/unverifiable licenses or with personal/identifying data not properly
  anonymized.
- Interpretation, analysis, modeling, or ranking of the data.
- Automated, unattended publishing to any portal.
- Any task that primarily serves a for-profit entity's private data.

## Solution approach & architecture

This is a **content/data-documentation project with light software** (templates + validators +
adapters). It is not a data pipeline that moves data.

**Pipeline (per dataset)**
1. **Triage & gate** — identify the dataset, its publisher, its license, and presence of PII.
   PASS only if license permits reuse + derivatives and no unanonymized PII. Record decision.
2. **Provenance capture** — source URL, publisher, retrieval date, version/edition, update cadence,
   license URL + license text snapshot reference, attribution string.
3. **Schema documentation** — data dictionary: field name, type, units, allowed values, nullability,
   description, caveats. Derived by *inspecting* the data, never by republishing it.
4. **Datasheet** — Datasheets-for-Datasets questionnaire: motivation, composition, collection,
   preprocessing, uses, distribution, maintenance.
5. **Croissant metadata** — machine-readable JSON-LD (Croissant ML format) describing the dataset.
6. **Validation script** — small, dependency-light script that checks the live/source data against
   the documented schema and emits a quality report.
7. **Portal adapter** — transform canonical metadata into the target portal's format.
8. **Review & contribute** — human review (license/PII reviewer + technical reviewer), then a human
   submits the contribution to the portal/repo.

**Canonical metadata model.** A single internal metadata object per dataset is the source of truth;
all outputs (Datasheet, Croissant, portal-specific) are *projections* of it. Fields include:
`id`, `title`, `publisher`, `sourceUrl`, `license {id, url, permitsDerivatives:boolean, snapshotRef}`,
`provenance {retrievedAt, version, updateCadence, attribution}`, `pii {present:boolean,
anonymized:boolean, notes}`, `fields[] {name, type, units, allowedValues, nullable, description,
caveats}`, `knownIssues[]`, `examples[]`.

**Tech stack.** TypeScript, ESM, pnpm workspaces (per Elyos conventions). Validators and adapters
are small Node packages with minimal dependencies. Croissant output validated against the published
Croissant JSON-LD spec; portal adapters emit CKAN/Socrata/DCAT-US JSON. Documentation authored in
Markdown + JSON/JSON-LD. No runtime services; everything runs locally or in CI.

**Key decisions.**
- Canonical-model-first so we never hand-maintain three parallel metadata formats.
- License/PII gate is a *blocking* step encoded as a checklist artifact committed with the work,
  not an informal judgement.
- Adapters are output-only (we generate metadata files); a human performs the actual portal upload.

## Data, licensing & compliance

**This is the critical section.** The project's deliverable is metadata *about* data; we still must
treat licensing and privacy conservatively because we describe and link to others' data.

**Source licenses we accept (must permit reuse AND derivative works):**
- **Open Government Licence (OGL)** v2.0/v3.0 — accepted; attribution required.
- **CC0 1.0** — accepted; no attribution required (we still record provenance).
- **CC-BY 4.0** (and compatible CC-BY versions) — accepted; attribution required.
- Other licenses (CC-BY-SA, CC-BY-NC, ODbL, bespoke government terms) → **case-by-case**, recorded,
  and only accepted if they clearly permit derivative documentation/metadata. NC terms require care:
  our docs are non-commercial public-commons artifacts, but we still flag for human decision.

**Excluded:**
- Datasets with **no clear license**, "all rights reserved," or terms that forbid derivatives →
  **flagged and excluded**, never guessed.
- Datasets containing **personal or identifying data** unless they are **properly anonymized** by
  the publisher and that anonymization is documented → excluded otherwise.

**Provenance model.** Every documented dataset records: source URL, publisher, retrieval timestamp,
dataset version/edition, license identifier + license URL + a captured reference to the license text
as it stood at retrieval, update cadence, and the required attribution string. Provenance is part of
the committed deliverable.

**Privacy/PII stance.** PII triage is mandatory and happens *before* documentation. If a dataset
contains direct identifiers (names, addresses, emails, precise geolocation tied to individuals,
government IDs) or plausibly re-identifiable quasi-identifiers, and the publisher has not documented
proper anonymization, the dataset is excluded and the concern is surfaced. We never anonymize data
ourselves (that would be transforming the data, which is out of scope).

**Attribution requirements.** All produced documentation attributes the original publisher per the
source license, links to the original source, and clearly states that the documentation — not the
data — is our contribution. Our documentation/metadata output is licensed **CC-BY-4.0**; validator
and adapter **code is MIT**.

## Quality, review & risk gates

**Risk tier: low–medium** (per proposal). Most documentation is low risk; medium applies where
factual accuracy about sensitive context, license interpretation, or PII judgement is involved.

**Required review before a deed is "done":**
- **License + PII reviewer** (mandatory, every dataset): confirms the recorded license permits
  reuse/derivatives and that no unanonymized PII is present. This is the hard gate.
- **Technical reviewer**: confirms the data dictionary, Datasheet, Croissant metadata, and
  validation script are accurate and run cleanly (CI green).
- **Expert/domain reviewer** (for any dataset touching health/legal/safety context, or any
  ambiguous license): required sign-off, escalating the task to `riskTier: medium` (or `high` if
  the underlying domain is high-stakes — such datasets are out of scope unless an expert signs off).

**Definition of Shipped.** Documentation + machine-readable metadata **accepted onto the dataset's
portal or repository**, with a verified license and recorded provenance, demonstrably improving
reuse (e.g., merged contribution, portal acceptance record, or a maintainer's confirmation).
Producing the docs is *not* shipped; acceptance by the beneficiary is.

## Roadmap & milestones

**M0 — Foundation & cold-start (thin)**
- Goal: build the reusable toolkit and prove the end-to-end flow on one dataset; begin partner
  outreach.
- Exit criteria: (1) documentation template + canonical metadata model published; (2) Croissant
  validator + one validation script working in CI; (3) the license/PII gate checklist exists and is
  applied to one dataset; (4) one dataset fully documented end-to-end and **submitted** to its
  source (acceptance may still be pending); (5) at least one partner-outreach thread opened.

**M1 — License/provenance gate hardened + first acceptances**
- Goal: make the gate rigorous and get real deliveries accepted.
- Exit criteria: (1) license/PII gate codified as a reviewable artifact and applied to ≥ 3 datasets;
  (2) ≥ 2 datasets **accepted** onto their portal/repo; (3) ≥ 1 confirmed contribution partner;
  (4) provenance model captures license snapshots automatically where feasible.

**M2 — Portal adapters & scale**
- Goal: reduce per-dataset effort via CKAN/Socrata/data.gov(DCAT-US) adapters.
- Exit criteria: (1) at least two portal adapters emit valid portal-native metadata, verified
  against a real portal's import format; (2) ≥ 5 datasets delivered+accepted cumulatively;
  (3) per-dataset effort measurably reduced vs. M0/M1 baseline.

**M3 — Reuse outcomes & sustainability**
- Goal: demonstrate real downstream reuse and a maintenance model.
- Exit criteria: (1) ≥ 3 verifiable external reuse events; (2) ≥ 8 datasets accepted cumulatively;
  (3) documented maintenance/refresh process and a steward identified for ongoing portal liaison.

Dependencies: M1 depends on M0 toolkit; M2 adapters depend on M1's canonical metadata; M3 depends on
a body of accepted deliveries from M1–M2.

## Work breakdown

The itemized, schema-mapped backlog lives in `TASKS.md`. It is organized by the milestones above,
each with a task table (`ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer`),
acceptance criteria for the most important tasks, and a milestone Definition of Done. A backlog of
sized-but-unscheduled tasks and one complete example Task JSON are included there.

## Governance, roles & stakeholders

- **Maintainer (Owner):** TBD — owns the toolkit, triage, and backlog.
- **License + PII reviewer:** TBD — mandatory gatekeeper; may rotate but must be qualified to read
  open-data licenses and spot PII. No deed ships without this sign-off.
- **Technical reviewer(s):** rotation of contributors who verify dictionaries, Croissant metadata,
  and validators (CI green).
- **Expert/domain reviewer(s):** engaged per-dataset for sensitive domains or ambiguous licenses
  (medium/high risk tier).
- **Steward (last-mile owner):** TBD — owns the relationship with portals/maintainers and confirms
  acceptance (the "delivered" signal). Critical because Definition of Shipped is acceptance, not
  production.
- **Partner / requestor:** TO BE SECURED — named portal(s) or dataset maintainer(s).

## Dependencies & integrations

- **External standards/specs:** Datasheets for Datasets (Gebru et al.), Croissant ML metadata spec,
  DCAT / DCAT-US, schema.org Dataset, SPDX license identifiers.
- **External services/portals:** CKAN, Socrata, data.gov; dataset repos (GitHub, Hugging Face,
  Zenodo). Integration is *output-only* metadata; no automated upload.
- **Datasets:** specific public datasets — TO BE SELECTED via triage; none assumed in scope yet.
- **Elyos pieces:** Task JSON schema (`packages/schema`), the donated-lane CLI workspace/PR flow
  (`packages/cli`), good-deed definition + refusal guardrails. No funded-lane/runner dependency
  (this project is donated lane).

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| Misclassifying a license (treating non-reusable data as reusable) | Medium | High | Mandatory license reviewer; record license URL + text snapshot; exclude on any doubt | License+PII reviewer |
| Documenting a dataset that contains unanonymized PII | Low | High | PII triage as a blocking pre-step; exclude unless publisher-documented anonymization; never anonymize ourselves | License+PII reviewer |
| Factual errors in data dictionary / Datasheet | Medium | Medium | Technical review; validation script must run; source-verified statements only | Technical reviewer |
| No portal partner secured → docs produced but never accepted (fails "delivered") | Medium | High | M0 partner outreach; steward role; mark `verifiedNeed:false` until secured | Steward |
| Source data changes/disappears, making docs stale | Medium | Medium | Record version + retrieval date; validation script detects drift; maintenance milestone | Maintainer |
| Croissant/portal format drift (spec or portal API changes) | Medium | Low | Canonical-model-first; validators pinned to spec versions; adapters isolated | Maintainer |
| Scope creep into cleaning/transforming data | Medium | Medium | Explicit non-goal; reviewers reject any data-transformation work | Maintainer |
| NC / share-alike license ambiguity blocks contribution | Medium | Low | Case-by-case human decision; default exclude; record rationale | License+PII reviewer |

## Security & privacy

- **Threat surface is small** (no runtime service, no data hosting). Main surfaces are CI and the
  metadata files we publish.
- **Secrets handling:** validators/adapters require no credentials by default. If a portal API
  token is ever needed for a contribution, it is supplied by the human submitting and must never be
  written into logs, receipts, or committed files (per Elyos rules).
- **PII:** the dominant privacy concern is *upstream* PII in candidate datasets. Handled by the
  mandatory exclusion gate above. We do not download, store, or process personal data; we inspect
  schema/sample only enough to document, and exclude on any PII signal.
- **Abuse/misuse prevention:** refuse and flag any task steering documentation toward surveillance,
  de-anonymization, targeting individuals, or laundering a non-open dataset as open. Documentation
  must remain descriptive and source-verified.

## Sustainability & maintenance

- **Post-delivery ownership:** the steward maintains portal relationships; the maintainer keeps the
  toolkit (validators, adapters, template) current with spec/portal changes.
- **Refresh:** validation scripts let anyone re-check a dataset against its documented schema;
  recorded version + cadence flags when a refresh is due. Stale docs are tracked as maintenance
  tasks (`type: maintenance`).
- **Outcome tracking:** the steward records acceptance events and external reuse signals against the
  success metrics; these are reviewed each milestone.

## Open questions

- Which specific portal(s)/maintainer(s) will be the first confirmed contribution partner(s)?
- How do we accept NC and share-alike licenses for *derivative metadata* — blanket policy or
  per-dataset? (Default: exclude/escalate.)
- Where is the canonical license-text snapshot stored (and is linking the license URL sufficient, or
  must we archive the text)?
- What counts as a sufficiently "verifiable external reuse event" for the outcome metric?
- For datasets on Hugging Face/Zenodo, do we contribute via PR or via their metadata APIs?

## References

- Elyos work rules — `C:\code\elyos\CLAUDE.md`
- Good Deed Definition + risk tiers — `C:\code\elyos\docs\good-deed-definition.md`
- Task JSON schema — `C:\code\elyos\packages\schema\src\schemas.ts`
- Proposal — `C:\code\elyos\governance\proposals\open-data-datasheets.md`
- Datasheets for Datasets (Gebru et al., 2018/2021)
- Croissant ML metadata format specification
- DCAT / DCAT-US, schema.org/Dataset, SPDX license list
- Open Government Licence (OGL); Creative Commons CC0 / CC-BY 4.0
