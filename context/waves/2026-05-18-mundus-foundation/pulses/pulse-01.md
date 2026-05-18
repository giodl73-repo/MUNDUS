# Pulse 01 - Repo foundation and intake

## Objective

Scaffold MUNDUS as the neutral known-asset catalog and prove that metadata-only
URL pointers can be validated, indexed, and searched with FLETCH.

## Work

| Item | Status | Notes |
|---|---|---|
| README and product plan | Done | Defines MUNDUS as catalog, not custody or fetch engine. |
| Wave docs and skills | Done | Adds foundation wave and repo-local skills. |
| Seed registry | Done | Adds `.fletch\registries\mundus-known-assets-seed.json`. |
| Validation contract | Done | Uses FLETCH validate/index/search and `git diff --check`. |
| TRACKER intake | Pending | Commit repo first, then add submodule and intake records. |

## Boundary notes

- MUNDUS rows can be `metadata_only` and still be searchable.
- FLETCH does not depend on MUNDUS data.
- FONTES remains the promotion target for PROOF-backed source custody.

## Validation commands

```powershell
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry validate --file .fletch\registries\mundus-known-assets-seed.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry index --file .fletch\registries\mundus-known-assets-seed.json --output .fletch\indexes\mundus-known-assets.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry search --index .fletch\indexes\mundus-known-assets.json --tag known-asset --metadata fetch_policy=metadata_only --limit 5
git diff --check
```
