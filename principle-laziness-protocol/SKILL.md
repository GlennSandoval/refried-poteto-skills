---
name: principle-laziness-protocol
description: "Apply when refactoring, evaluating diff size, or tempted to add abstractions, layers, or signal threading. Bias toward deletion and the smallest change that solves the problem."
---

# Laziness Protocol

Apply this skill only when the user requests it or another active skill routes
to it.

## Rules

- **Consolidate decisions.** Do not repeat the same choice in several places.
  Put the choice behind one source of truth. Pass the result as a simple flag.
- **Minimise the diff.** Make the smallest change that solves the problem.
  Fewer lines are better than "elegant" boilerplate.
