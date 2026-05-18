# MUNDUS Product Plan

## One-line product

MUNDUS is the neutral catalog of known important knowledge assets for the
portfolio.

## Problem

FONTES can do authentic source custody, but not every important source should
immediately become a custody project. FLETCH can validate, index, search, fetch,
and cache registries, but it should not carry domain data. Agents need a curated
middle layer that says which assets matter, how to find them, and what rights
posture applies before any fetch or extraction happens.

## Product promise

MUNDUS makes the knowledge world searchable without prematurely copying it. It
records important asset URLs, owners, domains, rights posture, tags, and
promotion routes so agents can discover sources and then hand selected assets to
FONTES/PROOF for authentic custody.

## Core objects

| Object | Meaning |
|---|---|
| Asset | A known URL-addressable source, book, course, standard, dataset, archive, repository, or collection. |
| Family | A stable owner or collection such as MIT OCW, NIST CSRC, OpenStax, NASA, NOAA, or USGS. |
| Registry | A `fletch.registry.v1` file with searchable asset rows. |
| Registry bridge | A MUNDUS row that points to another repo's `.fletch\registries\` entry point without taking ownership of that repo's asset rows. |
| Rights posture | `metadata_only`, `license_review`, `derived_text_allowed`, or `local_cache_allowed`. |
| Promotion route | The repo/process that can turn a catalog row into custody, packs, views, or downstream evidence. |
| Search index | A derived `fletch.registry-index.v1` report built by FLETCH from MUNDUS registries. |

## First wave

**Wave:** MUNDUS Foundation

Goal: establish MUNDUS as the neutral known-asset registry home and prove that
FLETCH can search metadata-only URL pointers without taking a dependency on
MUNDUS.

Pulses:

1. **Repo foundation and intake** - scaffold docs, wave records, skills, and
   TRACKER integration.
2. **Registry conventions** - standardize tags, metadata keys, and rights posture
   values.
3. **Known-asset seed** - add first authoritative source-family and asset rows.
4. **Knowledge Systems registry bridge** - point to repo-owned FLETCH registries
   for FONTES, MAXIM, LUCIA, CANON, PORTO, CERES, FAUNA, FLORA, RITE, GENES, and
   STORM.
5. **FONTES promotion bridge** - document how a MUNDUS asset becomes a PROOF-backed
   FONTES source map.
6. **Search validation contract** - keep FLETCH registry index/search commands as
   the generic validation gate.

## Dependency placement

MUNDUS is a Knowledge Systems catalog repo. It owns registry data and curation
policy, not runtime code. It depends on FLETCH as a CLI/tool for validation and
search; PROOF/CROP/PEBBLE are planned publisher layers after promotion flows
stabilize.

| System | Initial status | Reason |
|---|---|---|
| FLETCH | Required CLI/tool | Validate registries and build/search derived registry indexes. |
| FONTES | Planned bridge | Promote selected assets into source custody and PROOF ledgers. |
| PROOF | Planned | Render catalog/custody status and validate source records. |
| CROP | Planned | Index catalog slices and promoted source corpora. |
| PEBBLE | Planned | Package portable catalog/source context after custody. |
| ROLES | Planned | Review source-family curation, rights posture, and promotion decisions. |

## Non-goals

- No raw source asset mirroring in the foundation wave.
- No source extraction without FONTES/PROOF custody.
- No FLETCH dependency on MUNDUS registry content.
- No domain-specific simulation or product behavior.
- No claim-ranking, search-result scoring, or web crawling beyond curated rows.

## Validation commands

```powershell
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry validate --file .fletch\registries\mundus-known-assets-seed.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry validate --file .fletch\registries\mundus-knowledge-systems-registries.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry index --file .fletch\registries\mundus-known-assets-seed.json --file .fletch\registries\mundus-knowledge-systems-registries.json --output .fletch\indexes\mundus-all.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry search --index .fletch\indexes\mundus-all.json --tag known-asset --metadata fetch_policy=metadata_only --limit 5
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry search --index .fletch\indexes\mundus-all.json --tag repo-registry --metadata fetch_policy=metadata_only --limit 12
git diff --check
```
