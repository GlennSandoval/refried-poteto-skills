---
name: principle-migrate-callers-then-delete-legacy-apis
description: "Apply when introducing a new internal API while old callers still exist. Migrate callers and delete the old API in the same wave instead of preserving compatibility layers."
---

# Migrate callers then delete legacy APIs

Apply this skill only when the user requests it or another active skill routes
to it.

## When this applies

Use this principle when all of the following are true:

- No external users depend on backward compatibility.
- The project can absorb coordinated breaking changes.
- The new API is part of a simplification or refactor initiative.

## Procedure

1. Migrate every caller of the old API to the new API.
2. Delete the old API in the same wave. Do not keep a compatibility layer.
3. Update tests to assert the new contract.
4. Delete tests that only protect pre-refactor implementation details.
