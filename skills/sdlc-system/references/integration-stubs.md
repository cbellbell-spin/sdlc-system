# Integration Stubs and Manual Fallback Templates

When an integration is not connected, surface the corresponding manual fallback template. Ask the PM to complete it and return with the results. The stub output format matches what the integration would produce — downstream steps work identically whether data came from the integration or the manual template.

---

## CRM / Signal Sources

**Used in:** Phase 1A (signal aggregation), Phase 1B (validation signal)

**Integration stub:** When connected, query CRM for customer quotes, support tickets, and sales notes tagged to the relevant problem area. Return structured signal entries with source, observation, date, and strength rating.

**Manual fallback — Signal Collection Template:**

```
## Signal Collection: [Initiative Name] — [Date]
Completed by: [Name]
Sources reviewed: [list systems checked]

### Customer Signal
| # | Source (name / role / company) | Quote or observation | Date | Strength |
|---|-------------------------------|---------------------|------|----------|
| C1 | | | | Low / Med / High |

Strength guide: Direct quote from target-segment user describing specific workflow problem = High. Secondhand report from sales rep = Low.

### Internal Data Signal
| # | Source | Metric or observation | Date range | Strength |
|---|--------|-----------------------|-----------|----------|
| D1 | | | | Low / Med / High |

### Market Signal
| # | Source | Observation | Date | Strength |
|---|--------|-------------|------|----------|
| M1 | | | | Low / Med / High |

### Anecdotes (label explicitly)
| # | Source | Observation | Date |
|---|--------|-------------|------|
| A1 | | | |
```

---

## Analytics / Telemetry

**Used in:** Phase 5, Phase 6A, Phase 6B

**Integration stub:** When connected, query product analytics for activation, engagement, friction, and retention metrics defined in `_metric_registry.md`. Return structured metric values with prior period and trend.

**Manual fallback — Product Signal Template:**

```
## Product Signal: [Initiative Name] — Report #[N]
Reporting period: [Start] to [End]
Data source: [Analytics system]
Extracted by: [Name] on [Date]

Use metric definitions from _metric_registry.md exactly. Do not substitute.

### Activation Metrics
| Metric name (from registry) | Definition | Current value | Prior period | Trend |
|----------------------------|-----------|---------------|--------------|-------|

### Engagement Metrics
| Metric name (from registry) | Definition | Current value | Prior period | Trend |
|----------------------------|-----------|---------------|--------------|-------|

### Friction and Failure States
| Observation | Frequency | Affected workflow | Trend | Severity |
|-------------|-----------|------------------|-------|----------|

If friction table is empty: explain why. A product in market with no reported friction has either no users or no instrumentation.
```

---

## System / Performance Monitoring

**Used in:** Phase 5, Phase 6A, Phase 6B

**Manual fallback — System Signal Template:**

```
## System Signal: [Initiative Name] — Report #[N]
Reporting period: [Start] to [End]

### Performance
| Metric | SLI threshold (from PRD) | Current value | Trend | Status |
|--------|--------------------------|---------------|-------|--------|
| Latency (p95) | | | | Within / Approaching / Breached |
| Error rate | | | | Within / Approaching / Breached |

### Incidents
| Incident | Date | Duration | User impact | Root cause | Status |
|----------|------|----------|-------------|-----------|--------|

If no incidents: write "None in this period" explicitly.

### System Risk Flags
[Behavior not yet an incident but warranting monitoring. "None" if none — do not leave blank.]
```

---

## Financial Data

**Used in:** Phase 5, Phase 6A, Phase 6B

**Manual fallback — Financial Data Extract Template:**

```
## Financial Data Extract: [Initiative Name] — Report #[N]
Reporting period: [Start] to [End]
Finance partner review: [Name] on [Date] — required before filing

Use metric definitions from _metric_registry.md exactly. A changed definition is a metric continuity violation.

| Metric | Definition (from registry) | Current value | Prior period | Trend | Source |
|--------|---------------------------|---------------|--------------|-------|--------|
| Revenue | | | | | |
| Average deal size | | | | | |
| Margin | | | | | |
| Retention / churn | | | | | |

If financial metrics are not separately tracked: confirm this was documented in the Product Brief Section 5.
```

---

## Support Systems

**Used in:** Phase 1A, Phase 5, Phase 6

**Manual fallback — Support Signal Template:**

```
## Support Signal: [Initiative Name] — [Date range]
Filter applied: [keyword or category used]

| Observation | Ticket count | Affected workflow | Verbatim (if available) | Trend | Strength |
|-------------|-------------|------------------|------------------------|-------|----------|
```

---

## GTM / Sales Signal

**Used in:** Phase 5, Phase 6A, Phase 6B

**Manual fallback — GTM Signal Template:**

```
## GTM Signal: [Initiative Name] — Report #[N]
Reporting period: [Start] to [End]

### Channel Performance
| Channel | Target (from GTM plan) | Actual | Trend | vs. Plan |
|---------|----------------------|--------|-------|----------|

### Conversion
| Stage | Target | Actual | Trend | vs. Plan |
|-------|--------|--------|-------|----------|

### GTM Execution Fidelity
Fidelity assessment: On plan / Minor drift / Significant drift

If drifted — what changed, why, and how it affects interpretation of product signal: [Describe]

### Sales Observations
| Observation | Source | Frequency | Trend | Strength |
|-------------|--------|-----------|-------|----------|
```

---

## Deferral Log

**Used in:** Phase 0, Gate 2A

**Manual fallback — Deferral Log Template:**

```
## Deferral Log: [Problem Area / Initiative Name]

| Date considered | Decision | Decision-maker | Reason | New signal since |
|----------------|----------|---------------|--------|-----------------|

Deferral count: [N]

If considered 3+ times: flag explicitly at Gate 2A. Repeated deferral with no new signal is organizational information, not a neutral state.
```