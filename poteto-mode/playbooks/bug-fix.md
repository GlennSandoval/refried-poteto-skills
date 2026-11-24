### Bug fix

**You own this task. Plan, review, verify.** Delegate investigation and the fix when supported; otherwise do them sequentially and disclose the loss of independent review.

Be scientific. Every shipped line traces to runtime evidence. Belt-and-suspenders that "might help" is a hypothesis, not a fix. It does not ship. When evidence refutes a hypothesis, revert what it motivated. The smallest change the evidence justifies ships, nothing more.

1. Reproduce on the matching surface using an available driver or direct interaction. If the surface is unavailable, use the closest permitted repro or instrumentation, report what remains unproven, and ask for help only after explaining the access limitation.
2. Form hypotheses from a trace of the affected subsystem and the **why** skill for regression history. Eliminate them with runtime evidence, instrumentation, or logging until the mechanism survives a direct check. For a long hunt use the available wake mechanism in the Autonomous run playbook; if none exists, continue in-session and report the limitation.
3. Plan the fix. If it crosses a function boundary, use **architect** first. Delegate implementation with a specific scope when supported; follow the Subagents section for optional `bug-fix` model configuration. Otherwise implement it yourself.
4. Verify on the same surface. The original repro now passes. "Inconclusive" or wrong-surface is not a pass. Flag it. Unit tests show branch behavior, not bug absence.
5. Stage the commits so the failing repro lands before the fix in git history. See the **tdd** skill for the failing-test-first cadence when the bug has a cheap local test path. Skip it when the test would be expensive, integration-heavy, or unclear.
   This is the canonical **sequence-verifiable-units** principle skill, the failing test first and the fix on top.
6. Run **Opening a PR**.

**Reply:** what was broken, root cause, fix, how you verified. Paste failing-then-passing repro output verbatim.
