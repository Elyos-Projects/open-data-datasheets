# Proposal: open-data-datasheets

**Proposer:** jdev1977 (drafted by Claude Code)
**Date:** 2026-06-28
**Domain(s):** public-data, open-science, civic
**Lane:** donated
**Requestor / beneficiary:** researchers, journalists, civic-tech groups, data portals  ·  **Verified need:** yes (poor documentation is the #1 barrier to dataset reuse)

## Summary
For high-value public open datasets, produce standardized documentation — data dictionaries,
provenance and license records, "Datasheets for Datasets" / Croissant ML-metadata, and small
validation scripts — so the data is actually discoverable and reusable. Documentation, not the
data itself, is the deliverable.

## Why it qualifies as a good deed
- **Tangible public benefit:** unlocks already-public data that is currently unusable in practice.
- **Freely available:** all docs/metadata open, contributed to the dataset's portal.
- **Not primarily for-profit:** improves the public data commons.
- **No harm/misinformation:** documentation is descriptive and source-verified.
- **Executable by AI sessions:** one dataset = one self-contained documentation task.

## Scope / first tasks
- (small) Documentation template (schema dictionary, provenance, license, known-issues, examples).
- (medium) Full datasheet + Croissant metadata for one public dataset; license verified.
- (small) Validation script (schema/row checks) emitting a data-quality report.
- (small) Portal-contribution adapter (CKAN/Socrata/data.gov metadata).

## Definition of shipped
Documentation + machine-readable metadata accepted onto the dataset's portal or repo, with a
verified license and provenance, demonstrably improving reuse.

## Risks / review needs
**Risk tier: low–medium.** **License gate:** verify each source permits reuse/derivatives and
record it (e.g., Open Government Licence, CC-BY, CC0); flag datasets whose terms are unclear rather
than guessing. Exclude any dataset containing personal/identifying data unless properly anonymized.
