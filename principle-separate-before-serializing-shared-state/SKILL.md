---
name: principle-separate-before-serializing-shared-state
description: "Apply when concurrent actors might write to the same file, branch, key, or state object. Eliminate the sharing first; serialize structurally only when one shared writer is a real invariant."
---

# Separate before serializing shared state

Apply this skill only when the user requests it or another active skill routes
to it.

## Concept

Concurrent actors might write the same file, branch, key, or object. Before you
add any coordination, decide whether they need one shared object or are
publishing independent facts.

Two workers that write their own field into one `state.json` still share
mutation.

Instructions are not concurrency control. Treat "we need a lock" as a smell,
and check the alternative first.

## Procedure

1. Give each actor its own file, key, branch, or state directory. This is the
   default.
2. Merge the separate state only where it is read.
3. If one shared write target is a real invariant, serialize access
   structurally. Use one of these:
   - A lockfile.
   - A single writer.
   - Sequential phases.
   - Compare-and-swap.
