# MUNDUS

World catalog for known important knowledge assets.

MUNDUS is a Knowledge Systems repo for curated asset discovery: canonical URLs,
owners, domains, tags, rights posture, and routing hints. It does not fetch,
mirror, or redistribute source bytes by default. It tells the portfolio what
exists and why it matters; source-custody repos such as FONTES decide what can be
promoted into PROOF-backed extraction, PEBBLE packs, and CROP views.

## Product thesis

Agents need a map of the world before they fetch the world. MUNDUS records the
important source families, references, standards, courses, datasets, books, and
archives that the portfolio should know about, even when the correct treatment is
`metadata_only`.

## First consumers

| Consumer | Use |
|---|---|
| FONTES | Promote selected known assets into rights-reviewed source custody. |
| FLETCH | Validate, index, and search MUNDUS registries without depending on MUNDUS data. |
| PROOF | Later render catalog/custody status and enforce rights-boundary linting. |
| PEBBLE/CROP | Later consume promoted source packs and catalog slices. |
| MAXIM/LUCIA/CANON/PORTO/etc. | Discover authoritative source candidates and repo-owned FLETCH registry entry points before local backfill. |

## Initial scope

1. Maintain curated `fletch.registry.v1` files for known assets and source
   families.
2. Use `metadata_only` for important URL pointers that should be searchable but
   not fetched.
3. Use `license_review` for assets that may become extractable after child
   resource review.
4. Add registry tags and metadata conventions so FLETCH search works across
   families.
5. Hand off selected assets to FONTES when full custody and PROOF evidence are
   needed.
6. Point to repo-owned Knowledge Systems registries so MUNDUS remains the
   one-stop discovery catalog without absorbing domain repo assets.

## Knowledge Systems registry bridge

MUNDUS publishes `.fletch\registries\mundus-knowledge-systems-registries.json`
as a top-level map to repo-owned FLETCH registries. Use this when the question is
"which repo has the searchable catalog for this domain?" and then follow the
`promotion_route` or `repo_url` metadata into that repo for deeper rows. The
bridge uses raw GitHub file URLs and GitHub contents API directory URLs so
`fletch registry index --follow` can resolve the deeper registry rows without a
local clone of every Knowledge Systems repo.

## Non-goals

- MUNDUS is not a fetch/cache engine; FLETCH owns that.
- MUNDUS is not the rights/custody ledger; FONTES and PROOF own promoted source
  custody.
- MUNDUS does not commit raw books, PDFs, media, datasets, notebooks, or code
  archives.
- MUNDUS does not replace domain repos such as PORTO, STORM, FAUNA, or FLORA.
- MUNDUS does not rank truth claims; it catalogs source assets and routing
  posture.

## First validation

```powershell
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry validate --file .fletch\registries\mundus-known-assets-seed.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry validate --file .fletch\registries\mundus-knowledge-systems-registries.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry index --follow --file .fletch\registries\mundus-known-assets-seed.json --file .fletch\registries\mundus-knowledge-systems-registries.json --output .fletch\indexes\mundus-all.json
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry search --index .fletch\indexes\mundus-all.json --tag known-asset --metadata fetch_policy=metadata_only --limit 5
..\..\tools-infra\fletch\target\debug\fletch-cli.exe registry search --index .fletch\indexes\mundus-all.json --tag repo-registry --metadata fetch_policy=metadata_only --limit 12
git diff --check
```
