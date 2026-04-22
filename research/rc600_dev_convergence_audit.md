# RC-600 Dev Convergence Audit (Staged, Reviewable)

## Bottom line
The current RC-600 Dev repository is **not yet converged** to a reliable planner/editor implementation. It has strong validated structural evidence, but that evidence is still mostly represented as research artifacts rather than explicit planner-state schemas and workflows.

## Domain audit

### 1) ROUTING
- **Already correct:** split between `Routing:Track` and `Routing:Input/Rhythm`; bus families and member sets are validated.
- **Missing/flat:** no explicit editable routing-matrix state model per memory.
- **Smallest next step:** add `MemoryRouting` schema with typed destination groups and member enums.

### 2) TRACK input-source / Bounce In
- **Already correct:** Bounce In source members (Mic/Inst/Rhythm set) are validated.
- **Missing/flat:** no typed per-track input-source set in planner state.
- **Smallest next step:** add `TrackInputSourceSet` to each track plan entry; keep serialization encoding explicit-but-pending.

### 3) ASSIGN
- **Already correct:** `ASSIGN1..16` and core field-family shape are validated.
- **Missing/flat:** no assign-bank typed slots and no invariant checks in visible app-state artifacts.
- **Smallest next step:** introduce `AssignSlot x16` typed schema + low-cost range/mode checks.

### 4) CTL FUNC
- **Already correct:** pedal mode 1/2/3 + pedal 1..9 and ext/exp control structure are validated.
- **Missing/flat:** no mode-indexed control plan object separating pedal/external/expression concerns.
- **Smallest next step:** add `ControlPlan` object with `pedal_modes`, `ext_ctrl`, `expression`, plus separate compatibility metadata.

### 5) Set/memory planning suitability
- **Already correct:** evidence is memory-oriented and suitable to seed planning aggregates.
- **Missing/flat:** no `MemoryPlan` aggregate workflow (draft/validate/export-ready) is represented in current source artifacts.
- **Smallest next step:** define `MemoryPlan` schema + fixture pack (3-5 realistic memories) + diff/validation pass.

## Practical staged path (no monolithic rewrite)
1. Add typed schemas (Routing, TrackInputSourceSet, AssignSlot, ControlPlan).
2. Add fixture-driven validation + MemoryPlan diff output.
3. Wire UI/editing incrementally per domain.

See machine-readable audit: `research/rc600_dev_convergence_audit.json`.
