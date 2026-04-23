# TRACK Bounce In / input-source support (for RC-600_Dev)

## Validated source members (use exactly this set)
- Mic 1
- Mic 2
- Inst 1 Left
- Inst 1 Right
- Inst 2 Left
- Inst 2 Right
- Rhythm

## Confirmed by app-bundle evidence (secondary tier)
- TRACK field entries include `Bounce In` plus the same 7 source members with Bitwise1..Bitwise64 labels.

## Corroborated by XML excerpt (higher tier than app-bundle)
- `Bounce In` appears as `Switch`.
- Input-source collection repeats the same 7 members with Bitwise1/2/4/8/16/32/64 mapping.

## Unresolved (keep explicit)
- `TRACK-APP-002` remains `partially_confirmed`: docs confirm behavior/control names, but do not explicitly guarantee bitwise encoding as canonical persisted wire format.

## Implementation boundary for next RC-600_Dev slice
- Model as: `bounceInEnabled` + explicit 7-member `inputSources` structure.
- Do not widen scope to ASSIGN / CTL FUNC / sync-upload work in this slice.
