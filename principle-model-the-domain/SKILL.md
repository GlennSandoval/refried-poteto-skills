---
name: principle-model-the-domain
description: "Apply when writing stateful logic, or when code branches a lot or repeats a shape assumption across files."
---

# Model the domain

Apply this skill only when the user requests it or another active skill routes
to it.

## Concept

Encode the domain in a data structure instead of scattering it across
conditionals. The right structure makes invalid states unrepresentable and
deletes branches.

Signs that you skipped this: a feature grows an if/else chain by one more
branch, or a second boolean must stay in sync with the first.

## Procedure

Choose the structure that matches the problem:

- Use a state machine instead of scattered booleans or phase checks.
- Use a typed model instead of loose parameters.
- Use a map, registry, or discriminated union instead of branching spread
  across files.
- Use a reducer instead of ad hoc mutations.
- Use an index, queue, or normalised collection where the access pattern calls
  for it.

## Limits

Do not force this principle. Keep boring code when the shape is clear, local,
and unlikely to grow. Distrust an abstraction that adds indirection without
removing branches or invalid states.
