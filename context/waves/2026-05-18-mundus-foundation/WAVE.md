# MUNDUS Foundation Wave

## Objective

Create MUNDUS as the neutral known-asset catalog: searchable URL pointers,
source-family metadata, rights posture, and promotion routes without source-byte
mirroring.

## Pulses

| Pulse | Title | Status |
|---:|---|---|
| 1 | Repo foundation and intake | In progress |
| 2 | Registry conventions | Planned |
| 3 | Known-asset seed | Planned |
| 4 | FONTES promotion bridge | Planned |
| 5 | Search validation contract | Planned |

## Acceptance

- MUNDUS owns catalog registry data; FLETCH owns generic tooling.
- The seed registry validates with FLETCH.
- FLETCH can build a derived registry index and search metadata-only rows.
- Docs clearly separate MUNDUS cataloging from FONTES custody.

## Validation commands

```powershell
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry validate --file .fletch\registries\mundus-known-assets-seed.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry index --file .fletch\registries\mundus-known-assets-seed.json --output .fletch\indexes\mundus-known-assets.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry search --index .fletch\indexes\mundus-known-assets.json --tag known-asset --metadata fetch_policy=metadata_only --limit 5
git diff --check
```
