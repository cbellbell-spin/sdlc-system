# OpenSpec Handoff Reference

## Purpose

This reference defines how the SDLC system generates an OpenSpec change folder from a completed PRD. The OpenSpec package is the engineering-layer behavioral contract — what human developers and coding agents execute against. The PRD remains the product-layer source of truth.

The SDLC enforces what to build (gates, evidence quality, metric continuity). OpenSpec defines the behavioral contract that expresses how it must behave, in terms testable by engineering.

---

## When to Generate

Generate the OpenSpec package:
1. Automatically at the end of Phase 4, after PRD Sections 5 and 7 are complete and approved by the PM.
2. On demand, when the PM runs `/pd-openspec-export`.

Regenerate (increment version, preserve prior version) when:
- A structural PRD change modifies a SHALL/MUST statement in Section 5
- A new requirement is added to Section 5
- A requirement is removed from Section 5

Do not regenerate for prose-only edits, rationale updates, or changes to sections other than 5 and 7.

---

## Output Structure

Generate at `initiatives/[slug]/openspec/`:

```
openspec/
├── changes/
│   └── [slug]-v[N]/
│       ├── proposal.md
│       ├── design.md
│       ├── tasks.md
│       └── specs/
│           └── [domain]/
│               └── spec.md
└── archive/
    └── [slug]-v[N-1]/    ← prior versions preserved here on regeneration
```

**Version numbering:** Start at v1. On regeneration, move the current version to `archive/` and create `v[N+1]` as the new active version. Never overwrite a version that may be in active use by engineering.

---

## Artifact Mapping: PRD → OpenSpec

| OpenSpec artifact | Source in PRD |
|---|---|
| `proposal.md` | Section 1 (scope and lineage) + Section 2 (problem statement) + Section 3 (target users) |
| `specs/[domain]/spec.md` | Section 5 (functional requirements), grouped by the workflow they govern from Section 4 |
| `design.md` | Section 6 (dependencies and constraints) + Section 7 (instrumentation / telemetry) |
| `tasks.md` | Derived from Section 5 requirements — one task group per spec domain, one task per requirement |

---

## Behavioral Requirement Format

Every functional requirement in PRD Section 5 must be expressed in this format before the OpenSpec package can be generated. A requirement that does not have at least one scenario is incomplete.

```markdown
### Requirement: [Short name — 3-6 words, sentence case]
The system SHALL/MUST/SHOULD [observable behavior, stated without implementation detail].

#### Scenario: [Descriptive name]
- GIVEN [precondition — system or user state]
- WHEN [action or triggering event]
- THEN [expected system response, observable from outside]
- AND [additional assertion, if needed]

#### Scenario: [Edge case or failure name]
- GIVEN [precondition]
- WHEN [edge condition or failure trigger]
- THEN [expected system response]
```

**RFC 2119 keyword mapping to SDLC priority tiers:**
- `SHALL` → Must (blocking to launch — required for GA)
- `MUST` → Must (safety, security, or compliance constraint — non-negotiable)
- `SHOULD` → Should (important but deferrable under schedule pressure)
- `MAY` → Nice to have (optional capability)

**Requirement names** must match the names used in PRD Section 5 exactly. If a requirement name changes, the OpenSpec package must be regenerated.

---

## Spec Domain Organization

Specs are organized by workflow domain. One domain = one major user workflow from PRD Section 4.

Rules:
- Use the workflow name from PRD Section 4 as the domain name, converted to kebab-case
- A PRD with N core workflows produces N spec files
- Requirements that span multiple workflows go in the domain of the primary workflow they serve
- Infrastructure requirements (auth, rate limiting, logging) that do not belong to a user workflow go in a `system/` domain

Example: A PRD with workflows "User Onboarding," "Data Import," and "Report Generation" produces:
```
specs/
├── user-onboarding/
│   └── spec.md
├── data-import/
│   └── spec.md
└── report-generation/
    └── spec.md
```

---

## `proposal.md` Format

```markdown
# Proposal: [Initiative name]

## Intent
[Problem statement verbatim from PRD Section 2. Do not paraphrase.]

## Scope

### In scope
[v1 scope verbatim from PRD Section 1. Do not paraphrase.]

### Out of scope
[Explicit out-of-scope items from PRD Section 1.]

## Target Users
[Target segment and primary user from PRD Section 3.]

## Gate Lineage
[Gate 3 decision and date from _gate_log.md. Format: "Gate 3: [Decision] — [Date] — [Decision-maker]"]
```

---

## `design.md` Format

```markdown
# Design: [Initiative name]

## Technical Constraints
[Dependencies and constraints from PRD Section 6.]

## Instrumentation
[Metric-to-event mapping table from PRD Section 7. Every row from the PRD table is included here.]

## Architecture Decisions
[Placeholder section. Engineering fills this in. Do not generate content for this section.]

## Open Technical Questions
[Placeholder section. Engineering fills this in. Do not generate content for this section.]
```

---

## `tasks.md` Format

Generate one task group per spec domain. Within each group, generate one task per SHALL/MUST requirement (implementation task) plus one task for instrumentation coverage (verify telemetry events for that domain).

```markdown
# Tasks: [Initiative name]

## [Domain Name] (from specs/[domain]/spec.md)
- [ ] Implement: [Requirement name]
- [ ] Implement: [Requirement name]
- [ ] Verify instrumentation: confirm telemetry events defined in design.md cover all [domain] metrics

[Repeat for each domain]

## Pre-Launch Checks
- [ ] All SHALL requirements have passing acceptance tests
- [ ] All MUST requirements verified by engineering lead
- [ ] Instrumentation verified: every metric in _metric_registry.md has a confirmed telemetry event
- [ ] OpenSpec package version matches PRD version in _state.md
```

---

## Completeness Standard

The OpenSpec package is complete when:

1. `proposal.md` contains a verbatim problem statement and v1 scope from the PRD — no paraphrase
2. Every SHALL/MUST/SHOULD requirement in PRD Section 5 has a corresponding entry in a spec file
3. Every spec requirement has at least one Given/When/Then scenario
4. Every metric in `_metric_registry.md` appears in `design.md`'s instrumentation table
5. `tasks.md` has one task per SHALL/MUST requirement plus the pre-launch checklist

If any of these conditions is not met, the package is not complete. Do not tell the PM the handoff is ready until all five conditions are satisfied. List any gaps as numbered blocking items.

---

## Stale Package Detection

The OpenSpec package becomes stale when:

- A SHALL or MUST statement in PRD Section 5 is modified
- A requirement is added to or removed from PRD Section 5
- A metric is added to `_metric_registry.md` (metric continuity exception process)

When a staleness condition is detected, flag it: "The OpenSpec package may be stale. Run `/pd-openspec-export` to regenerate." Do not silently let the package drift from the PRD.

---

## What Belongs in Specs vs. Design

**In `specs/` (behavioral contract):**
- Observable system behavior
- Inputs, outputs, and error conditions
- External constraints (security, privacy, compatibility, regulatory)
- Scenarios that can be tested by engineering or QA

**In `design.md` (technical approach):**
- Class, function, or component names
- Library or framework choices
- Database schema decisions
- Internal system interactions not visible externally
- Step-by-step implementation details

If a requirement describes *how* the system achieves something rather than *what* it does, it belongs in `design.md`, not `specs/`. Push back on implementation-heavy requirements and restate them in behavioral terms before including in specs.