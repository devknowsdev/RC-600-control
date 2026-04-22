# RC-600 App-Bundle Schema Clue Index (Research Artifact, Non-Canonical)

## Scope & guardrails
- This is an **inference artifact** extracted from shipped app-bundle resources (`RC600 Editor.dll` strings + `RC600ParameterHelp.json`), not a canonical RC-600 spec.
- RC-505/RC-600 shared editor infrastructure is present in the binary; this extract was constrained to `database name="RC-600"` scoped records when possible.
- No hidden internal BOSS architecture is asserted.
- No speculative RC0 field mapping was attempted (A/B/C leaf keys remain unresolved unless labels were directly present).

## Canonical source coverage check (in this workspace)
1. Official RC-600 docs: **not found** here.
2. Uploaded RC0/XML files: **not found** here.
3. Repo schema/frontmatter rules: **not found** here.
4. Style refs: not used for semantic extraction.

Because #1-#3 were unavailable in this repository snapshot, all extracted rows are marked as app-bundle evidence only.

## What was extracted
- Structured index JSON: `research/rc600_app_bundle_schema_index.json`
- Categories included per task: `TRACK`, `ROUTING`, `ASSIGN`, `CTL FUNC`, `INPUT`, `OUTPUT`, `MIXER`, `FX`, `MEMORY`.
- For each row, the JSON includes:
  - section name
  - field/group labels
  - apparent value type
  - bus/track/system keys (if detectable)
  - copy/paste scope (if present)
  - evidence class + confidence
  - direct field entries (`DisplayName` + `ValueDef`) when available

## Quick high-signal observations (app-bundle evidence only)
- Track sections expose copy/paste metadata (`copyPasteScope="track"`, `copyPasteLevel="section"`) and field labels such as `Reverse`, `1 Shot`, `Pan`, `Play Level`, `Start Mode`, `Stop Mode`, `Dub Mode`, `Fx`, `Play Mode`, `Measure`.
- Assign sections appear as `ASSIGN1..ASSIGN16`, each with field labels like `Switch`, `Source`, `Mode`, `Target`, `Target Min`, `Target Max`, `Act Range Lo`, `Act Range Hi`.
- CTL FUNC clues appear under `ICTL*` and `ECTL_*` sections, with labels such as `Track Fx`, `Track`, `Target`, `Reverse`, and external control labels.
- Input/Output/Routing/Mixer sections are present as top-level XML tags with direct defaults and, in schema-like blocks, field labels/value defs.
- FX clues are split between `MASTER_FX` XML section labels and `RC600ParameterHelp.json` effect parameter help rows.

## Unknowns / review queue
- Exact canonical mapping of `A/B/C...` node keys to official parameter IDs.
- Whether all extracted `ValueDef` enumerations exactly match official RC-600 manuals.
- Whether any labels are stale/editor-specific placeholders (e.g., one track field label appears as `investigating!!!!` in bundle strings).

