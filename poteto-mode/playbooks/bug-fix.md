### Bug fix

You own this task. Plan, review, and verify. If delegation is supported,
delegate the investigation and the fix. Otherwise do them sequentially and
disclose the loss of independent review.

#### Principles

Be scientific. Every shipped line traces to runtime evidence. A
belt-and-suspenders change that "might help" is a hypothesis, not a fix, and it
does not ship. When evidence refutes a hypothesis, revert what the hypothesis
motivated. Ship the smallest change that the evidence justifies, and nothing
more.

#### Procedure

1. Reproduce the bug on the matching surface with an available driver or by
   direct interaction. If the surface is unavailable, use the closest
   permitted repro or instrumentation. Report what remains unproven. Ask for
   help only after you explain the access limitation.
2. Form hypotheses from a trace of the affected subsystem and from the **why**
   skill for regression history. Eliminate the hypotheses with runtime
   evidence, instrumentation, or logging. Continue until the mechanism survives
   a direct check. For a long hunt, use the available wake mechanism in the
   Autonomous run playbook. If none exists, continue in the session and report
   the limitation.
3. Plan the fix. If the fix crosses a function boundary, use **architect**
   first. If delegation is supported, delegate the implementation with a
   specific scope and follow the Subagents section for the optional `bug-fix`
   model configuration. Otherwise implement the fix yourself.
4. Verify on the same surface. Confirm that the original repro now passes.
   "Inconclusive" or wrong-surface is not a pass. Flag it. Unit tests show
   branch behaviour, not bug absence.
5. Stage the commits so that the failing repro lands before the fix in git
   history. When the bug has a cheap local test path, see the **tdd** skill for
   the failing-test-first cadence. Skip it when the test is expensive,
   integration-heavy, or unclear. This is the canonical case of the
   **sequence-verifiable-units** principle skill: the failing test first and
   the fix on top.
6. Run **Opening a PR**.

#### Reply

Give what was broken, the root cause, the fix, and how you verified it. Paste
the failing-then-passing repro output verbatim.
