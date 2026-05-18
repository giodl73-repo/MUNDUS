# MUNDUS Foundation Wave

## Objective

Create MUNDUS as the neutral known-asset catalog: searchable URL pointers,
source-family metadata, rights posture, and promotion routes without source-byte
mirroring.

## Pulses

| Pulse | Title | Status |
|---:|---|---|
| 1 | Repo foundation and intake | Done |
| 2 | Knowledge Systems registry bridge | Done |
| 3 | Registry conventions | Planned |
| 4 | Known-asset expansion | Planned |
| 5 | FONTES promotion bridge | Planned |
| 6 | Search validation contract | Planned |

## Acceptance

- MUNDUS owns catalog registry data; FLETCH owns generic tooling.
- The seed registry validates with FLETCH.
- FLETCH can build a derived registry index and search metadata-only rows.
- Docs clearly separate MUNDUS cataloging from FONTES custody.

## Validation commands

```powershell
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry validate --file .fletch\registries\mundus-known-assets-seed.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry validate --file .fletch\registries\mundus-knowledge-systems-registries.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry index --file .fletch\registries\mundus-known-assets-seed.json --file .fletch\registries\mundus-knowledge-systems-registries.json --output .fletch\indexes\mundus-all.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry search --index .fletch\indexes\mundus-all.json --tag known-asset --metadata fetch_policy=metadata_only --limit 5
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry search --index .fletch\indexes\mundus-all.json --tag repo-registry --metadata fetch_policy=metadata_only --limit 12
git diff --check
```
