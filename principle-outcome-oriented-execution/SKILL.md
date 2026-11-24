---
name: principle-outcome-oriented-execution
description: "Apply during planned rewrites and migrations with explicit phase boundaries. Converge on the target architecture; don't preserve smooth intermediate states with throwaway compatibility code."
---

# Outcome-oriented execution

Apply this skill only when the user requests it or another active skill routes
to it.

## Concept

Optimise for the intended, verifiable end state. Do not preserve smooth
intermediate states.

Keeping every intermediate step fully stable often creates temporary
compatibility code that becomes long-lived debt. Instead, converge on the
target architecture and prove correctness at explicit verification boundaries.

Prioritise end-state integrity over transitional stability. Intermediate
breakage is acceptable when it is planned, scoped, and reversible.

## Guardrails

- Use this principle only for planned rewrites and migrations with explicit
  phase boundaries.
- Declare where temporary breakage is acceptable.
- Keep high-signal checks for the areas you actively touch while you migrate.
- Require full static and runtime verification when the plan completes.
