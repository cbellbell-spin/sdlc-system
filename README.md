# Product Development Coach

Guides PMs through a structured Stage-Gate product development system — from idea intake through post-launch operating decisions. Drafts artifacts, enforces system rules, tracks initiative state across sessions, and prepares gate-ready outputs.

## Commands

| Command | What it does |
|---------|-------------|
| `/pd-portfolio` | Show full portfolio status |
| `/pd-new` | Start a new initiative |
| `/pd-resume [initiative]` | Resume work on an existing initiative |
| `/pd-gate` | Prepare gate brief / record gate decision |
| `/pd-signal` | File a new signal report |
| `/pd-openspec-export` | Generate or regenerate the OpenSpec engineering handoff package |

## File Structure

```
[shared folder root]
  _portfolio_registry.md

  initiatives/
    [initiative-slug]/
      _state.md
      _metric_registry.md
      _gate_log.md
      01_opportunity_brief.md
      02_validated_opportunity_brief.md
      03_product_brief.md
      04_prd.md
      05_signal_report_01.md  (numbered sequentially)
      06_phase5_rollout_decision_01.md  (numbered sequentially)
      07_phase6a_decision_brief.md
      08_phase6b_operating_review_01.md  (numbered sequentially)
      openspec/
        changes/[slug]-v[N]/  (OpenSpec engineering handoff package)
        archive/[slug]-v[N-1]/  (prior versions preserved)
```

## Phase Coverage

| Phase | What it covers | Gate |
|-------|---------------|------|
| 0 | Portfolio intake and triage | — |
| 1A | Opportunity Brief | Gate 1A |
| 1B | Validated Opportunity Brief | Gate 1B |
| 2A | Product Brief + metric registry lock | Gate 2A |
| 2B/2C | Scope, resource, roadmap | Gates 2B, 2C |
| 3 | Gate check only — PM produces artifacts in own tools | Gate 3 |
| 4 | PRD | — |
| 5 | Signal Reports + Rollout Decision Briefs | — |
| 6A | Validation Mode Decision Brief | — |
| 6B | Operating Reviews | — |

## Integration Points

Works without any integrations. Manual fallback templates in `skills/sdlc-system/references/integration-stubs.md` produce the same structured output. Priority order for connecting integrations:

1. Analytics / telemetry (Phases 5/6 signal reports)
2. CRM / signal sources (Phases 1A/1B signal aggregation)
3. Financial data (product-level initiative tracking)
4. Support systems (qualitative signal)