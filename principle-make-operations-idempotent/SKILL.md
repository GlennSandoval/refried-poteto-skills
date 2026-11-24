---
name: principle-make-operations-idempotent
description: "Apply when designing commands, lifecycle steps, or processing loops that run amid crashes, restarts, and retries. Converge to the same end state regardless of partial prior runs."
---

# Make Operations Idempotent

Apply this skill only when the user requests it or another active skill routes
to it.

## Principle

Every state-changing operation must converge to the correct state, however many
times it runs and wherever the previous run stopped.

A run can leave a lock, a temporary file, a half-written record, or a claimed
job behind. The next run must recognise each of these as stale, by evidence
that holds wherever the previous run could have stopped.

## Procedure

1. Derive each step from the state that exists, not from what the previous run
   meant to do.
2. Read the current state. Compare it to the goal. Apply only the difference.
3. Write to a temporary path. Rename it into place.
4. Make sure the next run can recognise anything the run leaves behind as
   stale.

## Tests

- What happens if this runs twice?
- What happens if the previous run crashed at every possible point?

If the answer depends on what the previous run left behind, add a
reconciliation step.
