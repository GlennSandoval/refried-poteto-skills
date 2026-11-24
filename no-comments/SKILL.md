---
name: no-comments
description: "Review comments and suppressions, fix accepted findings, and offer encodings for claimed constraints."
---

# No comments

Apply this skill only when the user requests it or another active skill routes
to it.

Review comments and suppressions in the requested scope. Use a fresh read-only
subagent for an independent review when one is available. Otherwise, review
directly and say that the review was not independent.

## Scope

Use the files or diff of the caller. Otherwise, use the current diff against
the base branch, including the working tree. The default base branch is `main`.

## Steps

1. Inspect the comments and the lint or type-checking suppressions in scope.
   - Flag comments that restate the code, describe obsolete behaviour,
     preserve dead code, or explain a workaround that can be removed.
   - Check suppressions for correctness and safety consequences.
   - Include the file, the line, and the evidence for each finding.
   - Keep API contracts, necessary rationale, and constraints on systems
     outside our control, unless evidence shows that they are obsolete.
2. Verify each finding against the surrounding code and history. Trace the
   symbol, or use the **why** skill, when a warning or constraint is unclear.
   Reject unsupported findings and anything outside the requested scope.
3. Fix trivial accepted findings directly. Delete a dead path, drop a
   parameter, or use the real API. If a fix needs a new shape, use the
   **architect** skill once for the accepted set and the surrounding code.
4. Implement the smallest root-cause fix in scope. If the root cause is outside
   scope, report it. Do not widen the change or add a symptom guard.
5. When a comment states a constraint, offer an in-scope type, runtime, test,
   or CI check that can enforce it. Obtain approval before you add that work.
   Delete the comment only when the constraint is obsolete or the replacement
   adequately preserves it. Otherwise, retain the comment and report the
   limitation.
6. Report the deletions, the accepted fixes, the proposed or added enforcement,
   and the open findings. Include any review that could not be independent.
