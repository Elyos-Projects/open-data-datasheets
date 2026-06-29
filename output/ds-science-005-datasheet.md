# Datasheet: GenBank Sequence Database

**One-line summary:** GenBank is the US NIH/NCBI annotated public collection of nucleotide
sequences and their protein translations, distributed as structured flatfile records.

*This datasheet is licensed under **CC-BY-4.0**. It is documentation only and contains no
GenBank sequence data.*

---

## Provenance & attribution

| Field | Value |
|---|---|
| Publisher | US National Center for Biotechnology Information (NCBI), National Library of Medicine (NLM), National Institutes of Health (NIH) |
| Source URL | https://www.ncbi.nlm.nih.gov/genbank/ |
| Catalog id | cat-science-005 |
| Retrieval date | 2026-06-28 |
| Required attribution | None legally required for public-domain US-government content; NLM *requests* acknowledgment. Suggested string: "Data from the GenBank sequence database, NCBI/NLM/NIH (https://www.ncbi.nlm.nih.gov/genbank/), retrieved 2026-06-28." Citation of record: Benson DA, et al. "GenBank." *Nucleic Acids Research*. 2013 Jan;41(D1):D36-42. |

---

## Source licence

**Verified licence:** US Government public domain / no-restriction data usage policy.

**Cited confirming clauses (verified 2026-06-28):**

- From the GenBank overview page (https://www.ncbi.nlm.nih.gov/genbank/):
  > "NCBI places no restrictions on the use or distribution of the GenBank data."
- From the NCBI/NLM policies page (https://www.ncbi.nlm.nih.gov/home/about/policies/):
  > "Information that is created by or for the US government on this site is within the public domain."
  and:
  > "NCBI itself places no restrictions on the use or distribution of the data contained therein."

**Does it permit derivatives?** Yes. Public-domain status plus the explicit "no restrictions on
use or distribution" statement permit reuse, transformation, and derivative works.

**Important caveat (not a blocker, but recorded):** NCBI notes that individual submitters or
their country of origin *may* assert patent, copyright, or other IP claims over portions of
deposited data, and NCBI cannot grant or deny permission for those portions. The database as a
whole is open; users of specific records should respect any submitter-asserted third-party
rights. This does not change the public-domain status of the collection or this datasheet.

---

## Data dictionary

Fields below are the top-level sections of a GenBank flatfile record, verified from the NCBI
annotated sample record (https://www.ncbi.nlm.nih.gov/genbank/samplerecord/). GenBank flatfiles
are semi-structured text, not a flat columnar table; "type" describes the value encoding.

| Field (key) | Type | Units / format | Description | Allowed values / null handling |
|---|---|---|---|---|
| LOCUS | string (composite) | length in bp | Locus name, sequence length, molecule type, GenBank division, modification date | Always present; molecule type DNA/RNA; division is a 3-letter code |
| DEFINITION | free text | n/a | Human-readable description: organism, gene/protein names, completeness (e.g. "complete cds") | Always present |
| ACCESSION | string | n/a | Stable unique identifier (e.g. U12345, AF123456) | Always present; never reused |
| VERSION | string | accession.version | Accession plus version integer; version increments when sequence changes | Always present; accession stays stable |
| KEYWORDS | string | n/a | Word/phrase describing the sequence (historical field) | A single period (".") when no keywords |
| SOURCE | free text | n/a | Abbreviated organism name; sometimes molecule type | Present |
| ORGANISM | string + lineage | n/a | Formal scientific name (genus/species) and full NCBI Taxonomy lineage | Present |
| REFERENCE | structured block | n/a | Publication citation(s) about the sequence, ordered oldest-first | Zero or more blocks |
| AUTHORS | list | n/a | Author names in article order | Subfield of REFERENCE |
| TITLE | string | n/a | Title of the work, or "Direct Submission" | Subfield of REFERENCE |
| JOURNAL | string | n/a | MEDLINE-abbreviated journal name, or submitter address | Subfield of REFERENCE |
| PUBMED | integer | PMID | PubMed identifier linking to the literature record | Optional; absent if unpublished |
| FEATURES | structured block | base coordinates | Annotated biological regions: feature keys, location spans, qualifiers | Present |
| source (feature) | feature | bp span | Mandatory feature: sequence length, organism, taxon id (/db_xref) | Always present |
| gene (feature) | feature | bp span | Named gene region with base-span coordinates | Zero or more |
| CDS (feature) | feature | bp span + aa | Coding sequence; start/stop codons and amino-acid translation | Zero or more |
| ORIGIN | sequence block | nucleotides | Sequence start note (often blank) followed by the nucleotide sequence | Present in sequence records |

*All rows above are verified from the NCBI sample-record documentation. Exact column widths and
the full INSDC qualifier vocabulary are defined in the INSDC Feature Table specification
(http://www.insdc.org/documents/feature_table.html) and the GenBank release notes
(https://www.ncbi.nlm.nih.gov/genbank/release/current) — those finer details were not
exhaustively re-verified here and should be treated as unconfirmed beyond the fields listed.*

---

## Datasheet for Datasets

**Motivation.** GenBank exists to provide open, comprehensive access to publicly available
annotated nucleotide sequences, supporting reproducible biological and biomedical research. It
is funded and maintained by the US government (NCBI/NLM/NIH).

**Composition.** Records are nucleotide sequences with rich annotation (organism, taxonomy,
literature references, gene/CDS features, translations). Instances are individual sequence
records identified by stable accessions. GenBank is part of the International Nucleotide Sequence
Database Collaboration (INSDC, with ENA and DDBJ). Reference sequences are public domain. This
datasheet intentionally scopes to public reference sequences and **excludes any consented
human-subject genomic micro-data** (e.g. controlled-access dbGaP data), which is out of scope.

**Collection process.** Sequences are submitted by researchers and sequencing centers
worldwide, plus bulk submissions and exchange with ENA/DDBJ. Submitters provide annotation;
NCBI applies format and consistency checks.

**Preprocessing / cleaning.** Records are normalized into the GenBank flatfile format and the
INSDC Feature Table vocabulary; organism lineage is mapped to NCBI Taxonomy. Versions increment
when sequence data changes; accessions are stable and never reused.

**Uses.** Sequence similarity search (BLAST), comparative genomics, primer/probe design,
phylogenetics, annotation pipelines, teaching. **Misuse caution:** do not treat submitter-
asserted IP-claimed portions as freely licensed, and do not infer identity of any individual.

**Distribution.** Freely distributed by NCBI via web, E-utilities/APIs, FTP releases, and BLAST.
Released under no-restriction public-domain terms (see Source licence). **This datasheet does not
redistribute, mirror, or host any GenBank data.**

**Maintenance.** Maintained by NCBI/NLM/NIH. Full releases are published regularly with release
notes; records are continuously updated and versioned. Contact and documentation are at
https://www.ncbi.nlm.nih.gov/genbank/.

---

## Croissant metadata

```json
{
  "@context": {
    "@vocab": "https://schema.org/",
    "cr": "http://mlcommons.org/croissant/",
    "field": "cr:field",
    "dataType": "cr:dataType",
    "recordSet": "cr:recordSet"
  },
  "@type": "Dataset",
  "name": "GenBank sequence database",
  "description": "NCBI/NLM/NIH annotated public collection of nucleotide sequences and their protein translations, distributed as GenBank flatfile records.",
  "url": "https://www.ncbi.nlm.nih.gov/genbank/",
  "license": "https://www.ncbi.nlm.nih.gov/home/about/policies/",
  "creator": {
    "@type": "Organization",
    "name": "National Center for Biotechnology Information (NCBI), NLM, NIH",
    "url": "https://www.ncbi.nlm.nih.gov/"
  },
  "datePublished": "1982",
  "version": "current-release",
  "recordSet": [
    {
      "@type": "cr:recordSet",
      "name": "genbank_record",
      "description": "A single GenBank flatfile sequence record.",
      "field": [
        { "@type": "cr:field", "name": "accession", "description": "Stable unique record identifier", "dataType": "Text" },
        { "@type": "cr:field", "name": "version", "description": "Accession.version identifier", "dataType": "Text" },
        { "@type": "cr:field", "name": "definition", "description": "Free-text record description", "dataType": "Text" },
        { "@type": "cr:field", "name": "organism", "description": "Scientific name and NCBI Taxonomy lineage", "dataType": "Text" },
        { "@type": "cr:field", "name": "length_bp", "description": "Sequence length in base pairs", "dataType": "Integer" }
      ]
    }
  ]
}
```

---

## Validation script

The script below validates the **structure** of a locally-held GenBank flatfile that the user
already possesses. It does **not** download, host, mirror, or republish any data — it only reads
a path the operator supplies and reports on structural conformance.

```python
#!/usr/bin/env python3
"""Validate the structure of a local GenBank flatfile. Documentation/QA only.
Does NOT download, host, or redistribute any data. Reads a local path only."""
import sys

# Top-level keys expected at the start of a record line in a GenBank flatfile.
REQUIRED = ["LOCUS", "DEFINITION", "ACCESSION", "VERSION", "SOURCE", "ORGANISM", "FEATURES", "ORIGIN"]

def validate(path, max_records=1000):
    seen, records, errors = set(), 0, []
    in_record = set()
    with open(path, "r", encoding="utf-8", errors="replace") as fh:
        for line in fh:
            key = line[:12].strip()
            if line.startswith("LOCUS"):
                in_record = {"LOCUS"}
            elif line.startswith("//"):
                missing = [k for k in REQUIRED if k not in in_record]
                if missing:
                    errors.append(f"record {records+1} missing: {missing}")
                records += 1
                in_record = set()
                if records >= max_records:  # bounded sample, ephemeral, local-only
                    break
            elif key in REQUIRED:
                in_record.add(key)
                seen.add(key)
    print(f"records checked: {records}")
    print(f"top-level keys observed: {sorted(seen)}")
    if errors:
        print("STRUCTURE ISSUES:")
        for e in errors[:20]:
            print("  -", e)
        return 1
    print("OK: all sampled records contain required top-level sections.")
    return 0

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("usage: validate_genbank.py <local_path_to.gb>")
        sys.exit(2)
    sys.exit(validate(sys.argv[1]))
```

---

## Limitations & gaps

- Field structure was verified from the NCBI annotated **sample** record, not from a full
  release. Exact flatfile column widths, the complete INSDC qualifier vocabulary, and every
  optional field (e.g. DBLINK, COMMENT, PRIMARY, CONTIG) were **not** exhaustively confirmed.
- No actual GenBank data was downloaded, sampled, or inspected for this datasheet; the
  validation script was written against documented structure, not executed against live data.
- The licence is public-domain/no-restriction at the collection level, but **individual records
  may carry submitter-asserted IP claims** that NCBI neither grants nor denies. Verify per-record
  before downstream redistribution.
- Consented human-subject genomic micro-data (controlled-access, e.g. dbGaP) is explicitly out
  of scope and must not be treated as covered by this datasheet.
- Croissant record is a minimal valid stub; field coverage is illustrative, not exhaustive.
