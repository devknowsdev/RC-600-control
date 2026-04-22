# RC-600 Crosswalk Candidate (Inference-Only, Review Artifact)

## Method and source-order guardrail
This artifact preserves the required source hierarchy:
1. official docs
2. uploaded RC0/XML
3. repo schema/frontmatter
4. style refs (formatting only)

Current workspace status: official docs and uploaded RC0/XML were **not present** in this repository snapshot, so this crosswalk is necessarily **app-bundle-supported only** and unresolved for canonical mapping.

Companion structured file: `research/rc600_crosswalk_candidate.json`

---

## ROUTING
### Candidate structure (not final mapping)
- `Routing:Track` appears to use bitwise track membership (`Track 1..Track 6`) across output bus groups:
  - Main Left/Right
  - Sub1 Left/Right
  - Sub2 Left/Right
  - Phones (conditional visibility)
- `Routing:Input/Rhythm` appears to use bitwise input/rhythm membership:
  - Mic 1, Mic 2, Inst 1 Left/Right, Inst 2 Left/Right, Rhythm
- Additional routing controls observed:
  - Rhythm Out
  - Phones Monitor
  - Phones Rhythm
  - Phones Out
  - Input Thru

**Evidence split**
- Official docs: unavailable here (unresolved)
- Uploaded RC0/XML: unavailable here (unresolved)
- App bundle: supported (compiled XML-like strings + prior index)

---

## TRACK (focus: input-source bitwise)
### Candidate structure (not final mapping)
- Track sections (`Track 1..Track 6`) expose copy/paste metadata at `track:section` scope.
- Track field labels include loop/playback controls plus a `Bounce In` source set.
- `Bounce In` appears to be bitwise over:
  - Mic 1, Mic 2, Inst 1 (Left), Inst 1 (Right), Inst 2 (Left), Inst 2 (Right), Rhythm.

**Evidence split**
- Official docs: unavailable here (unresolved)
- Uploaded RC0/XML: unavailable here (unresolved)
- App bundle: supported (compiled XML-like strings + `RC600ParameterHelp.json` for some labels)

---

## ASSIGN
### Candidate structure (not final mapping)
- Assign blocks observed: `Assign 1..Assign 16`.
- Copy/paste metadata observed: `copyPasteScope="assign"`, section-level.
- Repeating field structure candidate:
  - Switch
  - Action.Source
  - Mode
  - Act.Low
  - Act.High
  - Target.Source
  - Target.Low
  - Target.High

**Evidence split**
- Official docs: unavailable here (unresolved)
- Uploaded RC0/XML: unavailable here (unresolved)
- App bundle: supported (compiled XML-like strings)

---

## CTL FUNC / pedal / expression
### Candidate structure (not final mapping)
- Internal pedal modes appear as:
  - `Pedals: Mode 1`
  - `Pedals: Mode 2`
  - `Pedals: Mode 3`
- Each mode appears to contain `Pedal 1..9`, with `Min`/`Max` dynamic range fields.
- External controls appear as:
  - `ECTL_CTL1..4` with `CtrlFunc` + `Min`/`Max`
  - `ECTL_EXP1..2` with `ExpFunc` + `Min`/`Max`
- Guardrail note:
  - A hidden B-field label references RC-505mk2 (`"ignore used by RC-505mk2"`), which is treated as shared-infrastructure artifact only, **not** as RC-600 semantic inheritance.

**Evidence split**
- Official docs: unavailable here (unresolved)
- Uploaded RC0/XML: unavailable here (unresolved)
- App bundle: supported (compiled XML-like strings)

---

## Confidence rubric used
- **High**: direct section/value label and value-type strings extracted from RC-600 database-scoped compiled XML-like resources.
- **Medium**: structure inferred from repeated patterns in app strings and prior index normalization.
- **Low**: would require canonical corroboration but canonical source files are absent in this workspace.

## Explicit non-claims
- No final field mapping is asserted.
- No RC-505 semantics are inherited silently.
- No hidden/internal BOSS architecture is claimed.
