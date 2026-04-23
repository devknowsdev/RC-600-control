# TRACK Bounce In / Input-Source Slice — Smallest Safe PR Scope

## Inspection result (current repo state)
I inspected the repository tree for existing RC-600 Dev `track` schema/state/UI source files and found no first-party planner source tree in this snapshot (only research artifacts + bundled app assets).

Because of that, the safest next PR scope is a **foundational typed model slice** (schema/state + minimal summary), with UI deferred to a minimal read-only surface only if a UI layer exists.

---

## 1) Smallest safe PR scope
Implement only the TRACK input-source model convergence slice in planner core:

- Add a typed `TrackInputSourceSet` structure with exactly these validated members:
  - `mic1`
  - `mic2`
  - `inst1L`
  - `inst1R`
  - `inst2L`
  - `inst2R`
  - `rhythm`
- Add `bounceInEnabled` and `inputSources` to track state.
- Replace any flattened/grouped source abstraction with the explicit 7-member structure.
- Add summary logic that renders this structure deterministically (for diff/validation/reporting).
- Keep UI changes minimal and only where needed to display/edit the new structure safely.

No ASSIGN/CTL/ROUTING expansion in this PR.

---

## 2) Exact files likely to change
> These are target file groups for the next mergeable increment. If repo paths differ once source tree is present, map to equivalent modules.

### Schema/state
- `src/planner_core/track/schema.py`
- `src/planner_core/track/state.py`
- `src/planner_core/track/actions.py` (or equivalent reducer/update layer)
- `src/planner_core/memory_plan.py` (if TrackPlan shape is declared centrally)

### Summary / projection
- `src/planner_core/summary/track_summary.py`
- `src/planner_core/diff/track_diff.py` (only if existing diff layer already includes track summaries)

### UI (minimal, only if already present)
- `src/ui/planner/editors/TrackInputEditor.*`
- `src/ui/planner/cards/TrackSummaryCard.*`

### Tests/fixtures
- `tests/planner_core/test_track_input_sources.py`
- `tests/planner_core/test_track_summary.py`
- `tests/fixtures/rc600/track_input_sources/*.json`

---

## 3) Schema/state/UI impact
### Schema impact
- Introduces explicit typed source members (7 fixed fields) instead of grouped/flattened abstraction.
- Makes unsupported sources impossible at schema-validation level.

### State impact
- Track state now holds `bounceInEnabled` + explicit source set.
- Existing grouped flags/masks (if any) should be adapted via a compatibility adapter, not preserved as primary state.

### UI impact
- Minimal: show/edit 7 source toggles + bounce-in toggle.
- No large UX redesign; no set-level workflow changes in this slice.

---

## 4) Validation method
Before editing:
1. Re-check `TRACK-APP-002` evidence in `research/rc600_claim_validation.json`.
2. Re-check XML corroboration in `research/sources/rc600_rc0xml_validation_excerpt.xml` for source members.
3. Preserve precedence: official docs > RC0/XML excerpt > repo rules > style.

During/after implementation:
- Unit tests enforce exactly 7 allowed source members.
- Round-trip tests: state -> summary -> state-compatible projection (if applicable).
- Controlled change tests verify deterministic summary/diff output when toggling each source.
- Negative tests reject unknown source keys.

Definition of done:
- Flattened grouped abstraction removed from active track schema/state path.
- 7-member structure is the canonical internal track input-source model.
- Summary logic and tests pass with deterministic output.

---

## 5) Explicit defer list
Do **not** attempt in this PR:
- ASSIGN model changes
- CTL FUNC model changes
- ROUTING model changes
- XML field-address mapping beyond validated member semantics
- Device sync/upload protocol
- broad planner UX workflow changes
- bulk set editing behavior

This keeps the slice mergeable, auditable, and aligned with incremental convergence.
