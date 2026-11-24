---
name: principle-type-system-discipline
description: "Apply when designing types, reviewing a function signature, or writing code in any statically-typed language. Make illegal states unrepresentable, brand semantic primitives, parse external data at boundaries, exhaust variants, derive from authoritative schemas."
---

# Type system discipline

Apply this skill only when the user requests it or another active skill routes
to it.

## Concept

Make the compiler reject impossible states, mismatched primitives, and
unhandled variants.

## Procedure

- **Brand semantic primitives.** If two arguments share a primitive type but
  mean different things, give each argument its own type. Validate once, at
  creation.
- **Parse external data at boundaries.** External data is untyped until parsed.
  Pass JSON, RPC payloads, CLI args, config, environment variables, and
  database rows through a parse function at the boundary. The function returns
  the typed model.
- **Derive types from authoritative schemas.** When a schema file owns a
  shape, derive the type from it. Do not hand-roll a parallel type.

For TypeScript syntax, see the **typescript-best-practices** skill.
