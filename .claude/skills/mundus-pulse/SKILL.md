# MUNDUS Pulse

Use this skill to execute one MUNDUS catalog pulse.

## Required output

- Update the active wave record.
- Add or update only the registry/docs in scope.
- Run FLETCH registry validation and any index/search checks named by the pulse.
- Commit MUNDUS first, then update the TRACKER submodule pointer.

## Guardrails

- Metadata-only URL pointers are allowed and encouraged for important assets.
- `license_review` means known asset, not cleared corpus.
- PROOF-backed extraction belongs in FONTES after promotion.
