# Pulse 02 - Knowledge Systems registry bridge

## Objective

Make MUNDUS the first stop for finding repo-owned Knowledge Systems FLETCH
registries while keeping the registries themselves in the repos that produce or
custody the assets.

## Work

| Item | Status | Notes |
|---|---|---|
| Registry bridge | Done | Added `.fletch\registries\mundus-knowledge-systems-registries.json`. |
| Repo-owned boundaries | Done | Rows point to FONTES, MAXIM, LUCIA, CANON, PORTO, CERES, FAUNA, FLORA, RITE, GENES, and STORM registry homes or seed files. |
| Search tags | Done | Rows use `repo-registry`, `knowledge-systems`, domain tags, and `promotion_route` metadata. |

## Boundary notes

- MUNDUS owns the searchable map to each repo registry, not the repo's local
  artifact rows.
- Domain repos continue to own their `.fletch\registries\` files and validation
  history.
- FLETCH remains the generic validate/index/search tool.

## Validation commands

```powershell
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry validate --file .fletch\registries\mundus-knowledge-systems-registries.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry index --file .fletch\registries\mundus-known-assets-seed.json --file .fletch\registries\mundus-knowledge-systems-registries.json --output .fletch\indexes\mundus-all.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry search --index .fletch\indexes\mundus-all.json --tag repo-registry --metadata fetch_policy=metadata_only --limit 12
git diff --check
```
