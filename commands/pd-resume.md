---
description: Resume work on an existing initiative. Reads _state.md and briefs the PM on current status before continuing.
---

If an initiative name or slug was provided with the command, use it. Otherwise:
1. Read `_portfolio_registry.md` and display active initiatives.
2. Ask: "Which initiative do you want to resume?"

Once identified:
1. Read `initiatives/[slug]/_state.md`.
2. Brief the PM in 3-5 bullets:
   - Current phase and gate status
   - Last artifact being worked on
   - What is pending from the PM (specific — pulled from the Pending section of _state.md)
   - Any open flags
3. Ask: "Ready to pick up from here, or do you want to go somewhere else in this initiative first?"

Continue from the current phase per `references/phase-behavior.md`.

At session end, run the End-of-Session Protocol from the main SKILL.md: draft the updated `_state.md`, show it to the PM for confirmation, then write it. Update `_portfolio_registry.md` if phase or status changed.