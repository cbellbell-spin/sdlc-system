# Phase Behavior Reference

---

## Phase 0: Portfolio Intake & Triage

**Classification:** A/H — agent drafts triage scoring; PM reviews and overrides.

Ask the PM to describe the idea using these fields:
- Idea name (working title)
- Problem description (who has it, what it costs them)
- Source (customer, market, sales, internal)
- Customer segment
- Rough frequency or volume of the signal
- Any prior consideration of this idea

Propose initial triage scores (Low / Med / High) on three dimensions with reasoning:
- Strategic fit
- Estimated size
- Feasibility

PM validates or overrides. Overrides are recorded with PM's rationale.

Ask PM for Product Sponsor assignment. This is a human decision — do not propose one.

Create the initiative entry in `_portfolio_registry.md` and the subfolder structure per `references/file-structure.md`.

---

## Phase 1A: Opportunity Brief

**Classification:** H/a — PM does the thinking; agent provides structure, prompts, and quality checks.
**File:** `01_opportunity_brief.md`

**Cross-Plugin Read:**

Before starting Section 1, check `~/Documents/pm-coach/customer-context/` for an existing profile matching the segment in play:
- If a profile exists: surface it. *"I see you have a customer-context profile for `<segment>` (last updated YYYY-MM-DD). The key signals are: [summary]. Are those still the inputs to this Opportunity Brief, or has the picture changed?"* The profile is reference material, not a substitute for the work in this phase.
- If the segment is named but no profile exists: suggest capturing context first via `product-ic-coach` `customer-understanding` before drafting. *"There's no customer-context profile for `<segment>` yet. Want to capture what we know about them via `product-ic-coach` `customer-understanding` first, or proceed and we'll build it inline here?"*
- Also check `~/Documents/pm-coach/problems/` for any in-flight problem statement this initiative continues. If one matches, link it.

Record any cross-plugin anchors in `_state.md` under "Customer-context anchors" (see `references/file-structure.md`).

Work through each section with the PM. Do not write answers on the PM's behalf for H/a sections.

**Section 1 — Problem Hypothesis:**
- "Who has this problem? Walk me through the user — their role, their daily context relative to this problem."
- "Who would authorize a purchase? How do their priorities differ from the user's?"
- "What is the user trying to accomplish? Frame it as: When [situation], I want to [motivation], so I can [expected outcome]."
- "What is hard, slow, broken, or missing today? How is the user currently working around it?"
- Flag any claim not labeled by source type (data / customer quote / domain inference).

**Section 2 — Signal:**
- If CRM or signal integrations are connected: pull available signal.
- If not: surface the Signal Collection template from `references/integration-stubs.md`.
- After each signal entry: run Evidence Quality Assessment. Anything that sounds like "this suggests" or "this means" belongs in Section 3, not here.

**Section 3 — Interpretation:**
- After signal is logged: "What do these signals tell you, taken together?"
- Verify each interpretation references specific signal IDs. Flag any without a citation.
- "What else could these signals mean? What would be true if your primary interpretation is wrong?"
- One alternative interpretation is the minimum. If PM cannot generate one, prompt again.

**Section 4 — Confidence Levels:**
- Propose confidence ratings (L/M/H) based on signal volume, consistency, and source diversity. PM validates or overrides.

**Section 6 — Validation Plan:**
- "What are the 1-3 most important uncertainties? Not the most convenient ones."
- "What would make you kill this idea?" If PM cannot articulate a kill condition, the validation plan is not ready.

**Pre-gate check:** Run completeness checklist. Prepare Gate 1A brief. Tell PM: "This is ready for Gate 1A. Go have the meeting."

---

## Phase 1B: Validated Opportunity Brief

**Classification:** H/a with A/H for signal synthesis.
**File:** `02_validated_opportunity_brief.md`

The PM runs the validation work outside this tool. When they return with findings, the agent structures them.

**Returning with findings:**
- Ask PM to walk through each finding: what was observed, source type, strength, whether it supports the hypothesis.
- Record each as a V-prefixed signal in Section 2.
- Run Evidence Quality Assessment on every entry.
- Track: interviews conducted, positive signals, neutral signals, negative signals, experiments run.

**Kill condition evaluation:**
- Restate the kill condition from Phase 1A verbatim.
- If triggered: default recommendation is No-Go. Proceeding requires BET framing with named sponsor and explicit risk acceptance. Do not soft-pedal this.

**Disqualifier check — run all four:**
1. Customers cannot clearly articulate the problem
2. Interest without behavior change or willingness to pay
3. Highly inconsistent feedback across similar personas
4. Reliance on anecdotal or internal-only signal after validation

**Pre-gate check:** Run completeness checklist. Prepare Gate 1B brief.

---

## Phase 2A: Product Brief

**Classification:** H/a with A/H for artifact assembly.
**File:** `03_product_brief.md`

**Key rules:**
- Problem statement must be declarative. Flag "we believe" language and ask for a rewrite.
- Value proposition claims must reference validated signal IDs from Phase 1B.
- Every behavioral metric requires four things: name, definition, measurement method, telemetry event. A metric without a telemetry event is incomplete.
- After Section 5 (Success Metrics) is approved: write `_metric_registry.md`. Tell PM: "The metric registry is now locked. Any change to metric names, definitions, or telemetry events from this point forward must be explicitly documented and justified."

**Section 3 — v1 Scope:**
- "What is explicitly in v1? Specific enough that an engineer could estimate against it."
- "What is explicitly out of scope for v1 and why?" If PM cannot write this, scope has not been thought through.
- Future phases: high-level only. Flag any future-phase detail as expectation debt.

**Section 5 — Success Metrics:**
- Require all four fields per behavioral metric before accepting.
- Financial metrics required only for product-level initiatives. PM must explicitly state why they do not apply if this is a feature.
- After metrics confirmed: draft and write `_metric_registry.md`.

**Section 8 — Strategic Fit:**
- Surface deferral history from `_portfolio_registry.md` for the deferral history table.
- If urgency cannot be tied to a specific trigger event, push back.

**Pre-gate check:** Run completeness checklist (26 items). Prepare Gate 2A brief with Portfolio Coherence Assessment and Market & Deferral Reality Check summary.

**Gate 2B:** Agent prepares scope and resource summary. Actual allocation is a human decision. Record named owners and capacity if provided.

**Gate 2C:** Agent prepares timing rationale. Actual placement is a human decision. Record timeline, release strategy, roadmap position.

---

## Phase 3: Design and Launch Planning

**Classification:** Gate check only. No agent drafting of Phase 3 artifacts.

Tell the PM: "Phase 3 covers UX design, architecture assessment, event schema, and GTM planning. These are produced in your preferred tools — not here. When the following are complete and available, bring them back and I will run the Gate 3 readiness check:

- UX flows and design specs (linked or uploaded)
- Architecture assessment (from Engineering)
- Event schema — telemetry instrumentation plan mapping every Phase 2 metric to an event
- GTM plan — positioning, target segment definition, activation model, launch plan

I will verify these are present and run the Metric Alignment Check: every metric in `_metric_registry.md` must be covered by a defined telemetry event. Any gap is a blocking issue."

**Gate 3 Readiness Check when PM returns:**
1. Confirm all four artifact types are present or linked.
2. Run Metric Alignment Check against `_metric_registry.md`. List any metric without a corresponding event.
3. Confirm learning objective is defined.
4. Confirm Directional GA Criteria are defined with specific, observable thresholds.
5. Confirm time-to-learn window is defined (specific duration, not "TBD").
6. Prepare Gate 3 brief.

Record in `_gate_log.md`: decision, learning objective verbatim, Directional GA Criteria, time-to-learn window.

---

## Phase 4: PRD

**Classification:** A/H — agent drafts PRD from Phase 2A and Phase 3 outputs; PM reviews.
**File:** `04_prd.md`

**Section 1 — Scope and Lineage:**
- Pull problem statement verbatim from `03_product_brief.md`. Do not paraphrase.
- Pull v1 scope verbatim. Note any changes in the changes table.
- Pull Gate 3 decision from `_gate_log.md`.

**Section 4 — User Workflows:**
- For each workflow: trigger, preconditions, each step, success state.
- After each workflow: "What happens when this breaks? Define at least one failure state."
- Flag workflows carrying Extended triggers (Multi-actor / Regulated / AI / High-stakes).

**Section 5 — Functional Requirements:**
- Every requirement must link to at least one workflow ID.
- Every workflow must have at least one supporting requirement.
- If everything is Must: "If everything is Must, the label adds no information. What would you defer first under schedule pressure?"

**Section 7 — Instrumentation:**
- Pull all metrics from `_metric_registry.md` into the metric-to-event mapping table.
- Flag any metric without a defined telemetry event.

**Change Impact Detection (ongoing):**
At defined checkpoints, ask: "Have any of the six Protected Impact Zones changed? Core flows, metrics/telemetry, target segment, value proposition, activation path, GTM commitments." Classify each change as Contained or Structural. Log in the PRD change log before continuing.

**Behavioral Format Enforcement:**
Every requirement in Section 5 must be in the behavioral format defined in `references/openspec-handoff.md`: a SHALL/MUST/SHOULD statement followed by at least one Given/When/Then scenario. A requirement expressed only in prose is incomplete. When the PM provides a prose requirement, convert it to behavioral format and confirm: "I've converted this to behavioral format. Does this capture what you mean?" Do not accept requirements that lack scenarios.

**OpenSpec Export (Phase 4 exit deliverable):**
After Section 5 and Section 7 are complete and approved:
1. Run the OpenSpec completeness check from `references/openspec-handoff.md`. All five conditions must be met.
2. Generate the OpenSpec change folder at `initiatives/[slug]/openspec/changes/[slug]-v1/` per the structure in `references/openspec-handoff.md`.
3. Tell the PM: "The OpenSpec package is at `initiatives/[slug]/openspec/changes/[slug]-v1/`. The `specs/` directory is the behavioral contract for engineering. `design.md` is ready for the engineering team to fill in technical decisions. `tasks.md` has the implementation checklist. Review before handing to engineering. The PRD remains your product-layer source of truth; this package is the implementation-layer contract."
4. Update `_state.md` to note: "OpenSpec package generated: [slug]-v1 — [date]"

This package is a Phase 4 exit deliverable. The PM cannot close Phase 4 without it.

---

## Phase 5: Signal Reports and Rollout Decisions

**Classification:** A/H
**Files:** `05_signal_report_[N].md`, `06_phase5_rollout_decision_[N].md`

**Signal Report:**
1. Scan for existing signal reports. Tell PM: "The last signal report filed was #[N]. Are we working on #[N+1]?" Create only after PM confirms.
2. Guide through all six signal categories in order: product, adoption, system, GTM, financial, qualitative.
3. Adoption tracked separately from usage — do not merge.
4. If adoption is weak: populate root cause diagnosis table. All four root cause categories must be assessed — an all-Unknown table means the diagnosis was not done.
5. If no system incidents: PM must state "None in this period" explicitly.
6. Financial metric definitions must match `_metric_registry.md` exactly.
7. Draft interpretation after all six sections. Every interpretation references specific signal rows. Surface contradictory signal explicitly.

**Rollout Decision Brief:**
1. Scan for existing rollout decisions. Confirm number with PM.
2. Pull signal summary from current signal report — do not re-enter data.
3. Assess learning objective status: answered / partially / not at all.
4. Decision options: Expand / Hold / Roll Back. Each has an evidentiary standard.
5. If Expand: PM must name expansion risks being accepted.
6. If Hold: PM must define what converts to Expand and what converts to Roll Back. Specific conditions only.
7. Check time-to-learn window status. If at risk or expired, the window section is required.

---

## Phase 6A: Validation Mode Decision Brief

**Classification:** A/H
**File:** `07_phase6a_decision_brief.md`

1. Reference all signal reports across the full evaluation window — not just the most recent.
2. Assess learning objective first. If unanswered, this leads the brief.
3. Compare all metrics against `_metric_registry.md`. Document any continuity violations.
4. Evaluate each Directional GA Criterion individually from `_gate_log.md`.
5. Adoption evidence assessed separately from usage. Mandated usage does not qualify.
6. Decision options: Scale / Iterate / Reposition / Kill / Pause.
7. Enforce explicitly: "Continue as-is" is not valid in Phase 6A.
8. For Iterate: require a hypothesis and specific re-evaluation criterion and timeline.
9. For Pause: require a specific re-entry trigger. Without one, the recommendation should be Kill.

---

## Phase 6B: Operating Reviews

**Classification:** A/H — lightweight review.
**File:** `08_phase6b_operating_review_[N].md`

1. Scan for existing operating reviews. Confirm number with PM.
2. Pull signal report(s) for the review period. Summarize — do not re-enter data.
3. Evaluate behavioral and financial metrics against Phase 2 success criteria from `_metric_registry.md`.
4. Decision options: Continue as-is / Optimize / Invest / Sunset.
5. If Continue as-is: enforce all five evidentiary standards. PM must populate each one explicitly:
   - Behavioral metrics are meeting expectations (cite specific metrics)
   - Adoption signal shows sustained workflow integration (specific evidence)
   - Financial metrics tracking to plan (if applicable)
   - No significant unresolved risks
   - Continued investment is justified vs. alternatives — must be answered directly
6. If Invest: confirm this triggers a return to Phase 2.