---
name: principle-subtract-before-you-add
description: "Apply when sequencing an addition, refactor, or rewrite. Remove dead code, redundant validators, and stub references first, then build on the simpler base."
---

# Subtract before you add

Apply this skill only when the user requests it or another active skill routes
to it.

## Concept

When you evolve a system, remove complexity first, then build. Default to
subtraction.

Make simplification a continual investment. Leave the design slightly simpler
and more capable, behind the same or a smaller surface than you found it.

## Procedure

- Sequence removal before construction.
- Cut before you polish. Get to the minimum before you invest in quality.
- Design for observed usage, not speculative edge cases.
- Do not add speculative validators, parsers, or guards beyond what the spec
  demands.
- Simplify prompts. Remove redundant instructions and excessive templates.
- When a reference has no novel content, delete it. Do not leave a stub.
