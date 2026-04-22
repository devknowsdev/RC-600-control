# RC-600 Claim Validation (Prioritized Claims, XML-Corroborated)

Validation used required tiers:
1. official docs (primary)
2. RC0/XML excerpt (secondary)
3. app bundle (secondary support only)

## Claim statuses
- **ROUTING-APP-001**: confirmed
- **ROUTING-APP-002**: partially_confirmed
- **ROUTING-APP-003**: confirmed
- **TRACK-APP-002**: partially_confirmed
- **ASSIGN-APP-001**: partially_confirmed
- **ASSIGN-APP-002**: confirmed
- **CTL-APP-001**: confirmed
- **CTL-APP-002**: confirmed

## Why some remain partial
- `ROUTING-APP-002` and `TRACK-APP-002` are strongly corroborated by XML bitwise structure, but official docs describe behavior rather than explicit bitwise encoding.
- `ASSIGN-APP-001` is doc-confirmed for ASSIGN1-16 existence, while copy/paste-scope semantics are XML/schema corroborated (not explicitly described in docs).

## Guardrail retained
- `CTL-APP-003` remains a guardrail-only note (`still_inferred`) pending stronger authoritative evidence.

See detailed source-tier evidence in `research/rc600_claim_validation.json`.
