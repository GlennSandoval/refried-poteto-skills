---
name: principle-boundary-discipline
description: "Apply when wiring validation, error handling, or framework adapters. Concentrate guards at system boundaries (CLI, config, network, external APIs); trust internal types and keep business logic in pure functions."
---

# Boundary Discipline

Apply this skill only when the user requests it or another active skill routes
to it.

## Principle

Validation, type narrowing, and error handling belong where data crosses a
system boundary, such as CLI arguments, config files, external APIs, and the
network. Inside the boundary, the code trusts its types. It does not
re-validate and does not add redundant nil checks.

Business logic lives in pure functions with no framework dependencies. The
shell that calls those functions stays thin.

## Procedure

1. Validate, narrow types, and handle errors at the boundary.
2. Parse raw data into domain types at the boundary.
3. Keep transport and framework types out of the public surface.
4. Put business logic in pure functions. Call them from the thin shell.

## Tests

- Is this data crossing a boundary right now? If not, the validation is
  redundant. Remove it.
- Can this be a pure function that the shell calls? If yes, extract it.
