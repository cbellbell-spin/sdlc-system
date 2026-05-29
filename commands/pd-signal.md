---
description: File a new signal report for an initiative in Phase 5, 6A, or 6B. Scans for existing reports, confirms the report number with the PM, and guides through all six signal categories.
---

Identify the initiative. If in an active session, use the current one. Otherwise read `_portfolio_registry.md` and ask.

Scan `initiatives/[slug]/` for existing signal reports (files matching `05_signal_report_*.md`).

If no prior reports: "No signal reports filed yet for this initiative. We are starting with Report #1. Ready to proceed?"

If prior reports exist: "The last signal report filed was #[N]. Are we working on #[N+1]?"

Wait for PM confirmation before creating the file.

Create `05_signal_report_[N+1].md` and guide the PM through each section in order:

1. Product signal — surface Product Signal template from `references/integration-stubs.md` if no integration connected
2. Adoption signal — track separately from usage; if adoption is weak, populate the root cause diagnosis table (all four categories assessed — an all-Unknown table means the diagnosis was not done)
3. System signal — surface System Signal template if needed; require explicit "None" for incidents if there are none
4. GTM signal — surface GTM Signal template; assess fidelity explicitly; document drift if it exists
5. Financial signal — surface Financial Data Extract template if applicable; verify all metric definitions against `_metric_registry.md`
6. Qualitative signal — ask for customer feedback, support observations, sales insights; require strength ratings

After all six sections: draft interpretation. Every interpretation must reference specific signal rows. Surface contradictory signal explicitly — do not omit it.

Run completeness check before finalizing.

Ask: "Do you also need to prepare a Rollout Decision Brief (Phase 5) or Decision Brief (Phase 6A) based on this signal report?"

Update `_state.md` with the filed report number and any flags.