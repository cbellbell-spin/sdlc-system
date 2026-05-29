---
description: Prepare a gate brief for the current initiative. Runs the artifact completeness check and produces the decision-ready summary for Product Leadership. Also used to record a gate decision when the PM returns from the meeting.
---

Identify the initiative. If in an active session, use the current one. Otherwise read `_portfolio_registry.md` and ask.

Read `initiatives/[slug]/_state.md` to confirm current phase and gate.

Identify the gate this initiative is approaching:
- End of Phase 1A → Gate 1A
- End of Phase 1B → Gate 1B
- End of Phase 2A → Gate 2A
- End of Phase 2B → Gate 2B
- End of Phase 2C → Gate 2C
- End of Phase 3 → Gate 3

Run the completeness check for the relevant artifact. List every incomplete item as a numbered blocking issue. Do not proceed to brief preparation until all issues are addressed or explicitly acknowledged by the PM.

When completeness is confirmed, produce the gate brief per `references/gate-behavior.md`:
- Decision options (exact, for this gate)
- PM recommendation
- 2-3 strongest supporting signals
- 2-3 most significant risks or weaknesses
- Any disqualifiers triggered or BET conditions required

Tell the PM: "This is ready for Gate [X]. The decision options are [list]. Go have the meeting and come back with: (1) the decision, (2) who made it, and (3) any conditions attached."

Update `_portfolio_registry.md` status to "At gate." Update `_state.md`.

**When PM returns with the decision:**
1. Collect: decision, decision-maker name, date, conditions.
2. Record in `_gate_log.md`.
3. Update `_portfolio_registry.md` (Active, or Parked / Killed as appropriate).
4. Update `_state.md` with new phase.
5. Brief PM on what Phase [X+1] involves and the first step.