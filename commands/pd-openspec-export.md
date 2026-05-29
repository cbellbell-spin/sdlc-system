---
description: Generate or regenerate the OpenSpec engineering handoff package from the current PRD. Safe to run multiple times — prior versions are preserved in openspec/archive/. Use after any structural change to PRD Section 5 requirements.
---

Identify the initiative. If in an active session, use the current one. Otherwise read `_portfolio_registry.md` and ask.

Read `initiatives/[slug]/_state.md`. If Phase 4 has not started, tell the PM: "The OpenSpec package requires a completed PRD. Phase 4 has not started for this initiative. Run this command again once Section 5 of the PRD is complete."

Read `initiatives/[slug]/04_prd.md`. If the PRD does not exist or Section 5 is empty, stop and tell the PM what is needed before the export can run.

Read `initiatives/[slug]/_metric_registry.md`.

**Determine version number:**
Check whether `openspec/changes/` already contains a versioned folder for this slug.
- If no prior version exists: this is v1. Create `openspec/changes/[slug]-v1/`.
- If a prior version exists (e.g., v1): move the existing folder to `openspec/archive/[slug]-v[N]/` and create `openspec/changes/[slug]-v[N+1]/` as the new active version. Tell the PM: "Prior version v[N] preserved in `openspec/archive/`. Generating v[N+1]."

**Run the OpenSpec completeness check** from `references/openspec-handoff.md`. List any gaps as numbered blocking items. Do not generate the package until all five completeness conditions are met, or the PM explicitly acknowledges gaps and accepts an incomplete package.

**Generate the package** per `references/openspec-handoff.md`:
1. Generate `proposal.md` from PRD Sections 1, 2, and 3 plus Gate 3 lineage from `_gate_log.md`.
2. Group Section 5 requirements by their governing workflow (from PRD Section 4). Create one domain per workflow.
3. For each domain, generate `specs/[domain]/spec.md` with all requirements for that domain in behavioral format.
4. Generate `design.md` from PRD Sections 6 and 7.
5. Generate `tasks.md` with one task group per domain plus the pre-launch checklist.

**Verify completeness** after generation. Confirm all five completeness conditions are met. If any fail, list them and ask the PM how to proceed.

Update `_state.md` to note: "OpenSpec package generated: [slug]-v[N] — [today's date]"

Tell the PM: "OpenSpec package v[N] generated at `initiatives/[slug]/openspec/changes/[slug]-v[N]/`. Contents:
- `proposal.md` — intent, scope, and gate lineage
- `specs/` — behavioral contract ([N] domains, [M] requirements)
- `design.md` — constraints and instrumentation (engineering fills in technical decisions)
- `tasks.md` — [M] implementation tasks + pre-launch checklist

Review before handing to engineering. Any future changes to PRD Section 5 requirements will require regeneration."