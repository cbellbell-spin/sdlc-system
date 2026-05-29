# Gate Behavior Reference

## Universal Gate Sequence

Every gate follows this sequence without exception:

1. **Completeness check.** Run the artifact's completeness checklist in full. Every unchecked item is a blocking issue. List them numbered. Do not mark the artifact gate-ready until all items are addressed.

2. **Gate brief preparation.** Produce a brief covering:
   - What decision is being made (the exact options available)
   - PM recommendation — one of the valid outcomes, not a hedge
   - 2-3 strongest signals supporting the recommendation
   - 2-3 most significant risks or weaknesses in the evidence
   - Any disqualifiers triggered, kill conditions met, or BET conditions required

3. **Hand-off.** Tell the PM: "This is ready for Gate [X]. The decision options are [list]. Go have the meeting and come back with: (1) the decision, (2) who made it, and (3) any conditions attached."

4. **Decision recording.** Collect: decision, decision-maker name, date, conditions. Record in `_gate_log.md`. Update `_portfolio_registry.md` status.

5. **Phase advance.** Update `_state.md`. Brief PM on what Phase [X+1] involves and the first step.

---

## Gate 1A: Opportunity Validation

**Decision options:** Fund Validation / Kill

If Kill: ask PM for documented rationale before closing. A well-documented kill prevents the same conversation from resurfacing unchanged. Record in `_gate_log.md`.

**Surface in the brief:**
- Validation plan and its cost (time, resources, customer exposure)
- Kill condition defined in Section 6
- Problem and demand confidence ratings with justifications

---

## Gate 1B: Validated Opportunity

**Decision options:** GO / CONDITIONAL GO / NO-GO / BET

- If BET: require named sponsor name and explicit risk acceptance statement before recording. "BET" without a named sponsor is not a BET.
- If CONDITIONAL GO: define specifically what additional validation is required and what outcome converts it to GO or NO-GO.
- If NO-GO: record the evidence that led to the conclusion.

**Surface in the brief:**
- Validation summary counts
- Kill condition evaluation result
- Disqualifiers triggered (if any)
- Confidence direction: did confidence increase, hold, or decrease?

---

## Gate 2A: Prioritization

**Decision options:** Prioritize / Park / Kill

Required beyond standard completeness:

1. **Portfolio Coherence Assessment:** Does this initiative compound existing investments or is it a standalone bet? Prepare from Product Brief Section 8 and `_portfolio_registry.md`.

2. **Market and Deferral Reality Check:** Pull deferral history. If considered and deferred 3+ times, flag explicitly. Surface: cost of not acting, what changes if deferred again, what the re-entry trigger is.

---

## Gate 2B: Resource Commitment

**Decision options:** Fund / Park / Kill

Agent prepares scope and resource summary only. Actual allocation is a human decision.

Available moves if resources are constrained: reduce scope, extend timeline, or increase resources. No other moves are valid. Record named owners and capacity if provided.

---

## Gate 2C: Roadmap Placement

**Decision:** Timeline and release strategy — must produce a specific outcome.

Record in `_gate_log.md`: timeline, release strategy, roadmap position.

---

## Gate 3: Release Readiness

**Decision options:** Launch (Full) / Launch (Conditional) / Delay

Required beyond standard completeness:

1. **Artifact presence check:** All four Phase 3 artifacts present or linked: UX specs, architecture assessment, event schema, GTM plan.

2. **Metric Alignment Check:** Every metric in `_metric_registry.md` must be covered by a defined telemetry event. Gaps are blocking issues.

3. **Learning objective:** Defined and specific. "See how it goes" is not a learning objective.

4. **Directional GA Criteria:** Specific, observable thresholds. Vague criteria cannot be evaluated.

5. **Time-to-learn window:** Specific duration. "TBD" is not acceptable.

Record verbatim in `_gate_log.md`: learning objective, all Directional GA Criteria, time-to-learn window, any conditions on a conditional launch.