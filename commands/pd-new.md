---
description: Start a new product initiative. Collects initiative name, slug, and named PM. Creates the folder structure, adds to the portfolio registry, and begins Phase 0 or Phase 1A.
---

Ask the PM for:
1. Initiative name (working title)
2. Slug (kebab-case, lowercase — this becomes the folder name under `initiatives/`)
3. Named PM for this initiative

Then ask: "Do you want to start with Phase 0 triage (scoring this idea against the portfolio before investing in a full Opportunity Brief), or go directly to Phase 1A (Opportunity Brief)?"

Create the initiative subfolder:

```
initiatives/[slug]/
  _state.md          — initialize with phase set to the selected starting phase, status: Active, Named PM recorded
  _metric_registry.md — initialize with header only — not populated until Phase 2A
  _gate_log.md       — initialize with header and empty rows for all six gates
```

Add a row to `_portfolio_registry.md`:

```
| [Initiative name] | [slug] | [Named PM] | [Phase 0 or Phase 1A] | Active | [today's date] |
```

Confirm creation with the PM, then proceed with the selected starting phase per `references/phase-behavior.md`.