---
name: principle-fix-root-causes
description: "Apply when debugging. Trace each symptom back to the first place the system went wrong and fix it there. A guard is a fix only when the state it handles is legitimate."
---

# Fix Root Causes

Apply this skill only when the user requests it or another active skill routes
to it.

## Principle

Fix the fault, not the place where it surfaced. The root cause is the first
place where the system did something it should not do, or failed to handle a
state it should handle.

Guards, retries, swallowed errors, clamped values, and discarded state are the
usual ways to hide a bug. A guard is a fix only when the state it handles is
legitimate.

## Procedure

1. Reproduce the symptom first.
2. Ask "why" until the answer is a wrong decision in the code. If you are
   stuck, instrument the code and read the actual state.
3. Ask whether the state that triggered the symptom is legitimate.
   - If the state is legitimate, handle it where the code broke.
   - If the state should never exist, do not add a check there. Find what
     produced the state.
4. Fix the pattern, not the instance. Find every place with the same fault.
5. If the deciding fact took a deep dig, propose a cheap, always-on signal that
   would have shown it at first look.
