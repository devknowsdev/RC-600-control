# RC-600 Prioritized Execution Plan (Post-Convergence Audit)

## What should change first (foundational prerequisites)
1. **ROUTING state schema** (`MemoryRouting`) with Track/Input-Rhythm matrices.
2. **TRACK Bounce In state schema** (`TrackInputSourceSet`) attached per track.
3. **ASSIGN bank model** (`AssignSlot x16`) with lightweight invariants.
4. **CTL FUNC model** (`ControlPlan`) with pedal modes + ext/exp separation.

These are prerequisites because planner UX cannot be reliable until these domains are represented as typed, validated state rather than claim artifacts.

## What follows after foundations
5. **MemoryPlan aggregate workflow** (draft → validate → diff).
6. Incremental domain UI editors over validated state.
7. Set-building UX refinements and sync-readiness gating.

## Preserve vs correct abstractions
### Preserve
- Evidence-tier discipline and provenance-first validation.
- Benchmark-based coverage checks against the working editor.
- Incremental rollout (no monolithic rewrite).

### Correct / tighten
- Replace claim-only representations with typed domain schemas.
- Separate compatibility/guardrail metadata from primary semantics.
- Move from field fragments to memory-level aggregate planning objects.

## Domain-by-domain staged actions
### ROUTING
- **Current:** validated conceptually; not yet typed as editable planner matrix.
- **Target:** per-memory Track + Input/Rhythm routing model with destination groups.
- **Smallest step:** add `MemoryRouting` schema + reducers/selectors.
- **Areas:** schema/state first, UI matrix view second.
- **Validation:** fixture round-trip + completeness checks.
- **Class:** prerequisite.

### TRACK Bounce In / input-source
- **Current:** source set validated, not operationalized in track state.
- **Target:** typed per-track source-set and bounce intent.
- **Smallest step:** add `TrackInputSourceSet` to each `TrackPlan`.
- **Areas:** schema/state first, source picker UI second.
- **Validation:** fixture persistence + conflict warnings.
- **Class:** prerequisite.

### ASSIGN
- **Current:** field-family validated; no enforceable x16 slot model.
- **Target:** typed assign-bank with required fields/invariants.
- **Smallest step:** implement `AssignSlot` and `AssignBank` schemas.
- **Areas:** schema/state first, slot editor UI second.
- **Validation:** x16 slot fixture coverage + range/mode checks.
- **Class:** prerequisite.

### CTL FUNC
- **Current:** validated structure, but flattened in abstraction.
- **Target:** mode-indexed `ControlPlan` with pedal/ext/exp separation.
- **Smallest step:** add `ControlPlan` schema with dedicated sub-objects.
- **Areas:** schema/state first, mode-tab UI second.
- **Validation:** mode coverage fixtures + ext/exp min/max checks.
- **Class:** prerequisite.

### Memory/set planning UX
- **Current:** research artifacts exist; planner workflow not yet modeled.
- **Target:** memory aggregate workflow with validation and diff confidence.
- **Smallest step:** add `MemoryPlan` + minimal draft/validate/diff flow.
- **Areas:** workflow state machine + planner workspace UI.
- **Validation:** 3–5 memory scenario fixtures with deterministic diffs.
- **Class:** follow-on.

## Recommended implementation order
1. ROUTING schema/state
2. TRACK Bounce In schema/state
3. ASSIGN schema/state
4. CTL FUNC schema/state
5. MemoryPlan aggregate + validation/diff
6. Planner-first UX layering

## Stop / Keep / Start
### Stop doing
- Using evidence documents as a substitute for runtime planner state.
- Flattening RC-600 domains into generic key/value blocks.

### Keep doing
- Provenance-first validation (docs > RC0/XML > benchmark artifacts).
- Fixture-first confidence building before broad UI growth.

### Start doing
- Vertical slices per domain (state + validation + minimal UI).
- Memory-level diff tooling as a core planner capability.

## Milestones
- **M1 Structural convergence:** implement typed core schemas (Routing/Track/Assign/Ctl).
- **M2 Validation + diff confidence:** fixture packs and deterministic memory diffs.
- **M3 Planner-first UX:** draft/validate/diff set-building workflow.

## Risks
- **Semantic risk:** overfitting benchmark quirks where canonical semantics are silent.
- **UX risk:** exposing depth without progressive disclosure.
- **Architecture risk:** UI-first growth before state convergence, causing rework.

See machine-readable plan: `research/rc600_execution_plan.json`.
