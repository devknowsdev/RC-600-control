# RC-600 Implementation-Ready Repo Action Plan

This plan translates the execution strategy into small, mergeable increments Codex can execute safely.

## A. Proposed workstream list
1. **WS1 — Core schema/state convergence (Stage 1)**
   - ROUTING
   - TRACK Bounce In/input-source
   - ASSIGN
   - CTL FUNC
2. **WS2 — Validation confidence (Stage 2)**
   - fixtures
   - diff tooling
   - baseline/default memory comparisons
   - controlled change comparisons
3. **WS3 — Planner-first UX (Stage 3)**
   - memory overview
   - set overview hooks
   - routing/control summaries
   - constrained planner editing flow

## B. Ordered increments
1. INC-001 planner core skeleton
2. INC-002 ROUTING model
3. INC-003 TRACK Bounce In/input-source model
4. INC-004 ASSIGN model
5. INC-005 CTL FUNC model
6. INC-006 baseline/default fixture corpus
7. INC-007 deterministic memory diff tooling
8. INC-008 validation report aggregation
9. INC-009 planner memory overview UI (read-first)
10. INC-010 minimal planner editing vertical slice

## C. Per-increment file impact (high level)
- **INC-001:** `src/planner_core/*`, `docs/rc600/model_boundaries.md`
- **INC-002:** `src/planner_core/routing/*`, `tests/planner_core/test_routing_schema.py`
- **INC-003:** `src/planner_core/track/*`, `tests/planner_core/test_track_input_sources.py`
- **INC-004:** `src/planner_core/assign/*`, `tests/planner_core/test_assign_bank.py`
- **INC-005:** `src/planner_core/ctl/*`, `tests/planner_core/test_ctl_plan.py`
- **INC-006:** `tests/fixtures/rc600/*`, `tests/planner_core/test_fixture_loading.py`
- **INC-007:** `src/planner_core/diff/*`, `tests/planner_core/test_memory_diff.py`
- **INC-008:** `src/planner_core/validation/report.py`, `tests/planner_core/test_validation_report.py`
- **INC-009:** `src/ui/planner/MemoryOverview*`, `src/ui/planner/DomainSummaryCards*`, UI tests
- **INC-010:** `src/ui/planner/MemoryEditorFlow*`, domain editors, integration tests

> If exact paths differ in repo conventions, preserve increment boundaries and map these file groups to the project’s actual structure.

## D. Per-increment validation method
- **Stage 1:** schema/unit tests + invariants only; no broad UI work.
- **Stage 2:** fixture conformance, deterministic diff snapshots, controlled change comparisons.
- **Stage 3:** planner UX integration tests driven by Stage 2 artifacts.

Each increment must include:
1. evidence check references (docs + XML + validated claim file)
2. explicit DoD
3. explicit “not yet” scope

(See machine-readable DoD + defer items per increment in `research/rc600_repo_action_plan.json`.)

## E. Explicit defer list
- pedal upload/sync protocol implementation
- unsupported semantic mapping beyond validated evidence
- RC-505 compatibility-field promotion into RC-600 semantics
- large UI redesign before schema stabilization
- cross-device abstraction framework

## F. Recommended first PR scope
**PR-1 = INC-001 + INC-002 (schema/state/tests only)**
- Include:
  - planner core skeleton
  - ROUTING typed schema/state/actions
  - ROUTING schema tests
- Exclude:
  - editing UI
  - fixture expansion
  - diff tooling
  - assign/ctl/track implementation

This is the smallest high-value merge that moves from research evidence to executable planner-state convergence without a rewrite.
