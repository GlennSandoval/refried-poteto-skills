### Feature

**You own the design. Plan, review, verify.** Delegate implementation when supported; otherwise implement and review sequentially, disclosing the loss of independence.

1. Trace the affected subsystem.
2. `architect` for the shape.
3. Write the throughput checkpoint as four todo items. A dimension that genuinely does not apply (single file, no fan-out) keeps its item with `n/a: <reason>` rather than being dropped:
   - **Blocking first steps.** Gates run before fan-out.
   - **Independent workstreams.** Disjoint files, services, or layers parallelize. Shared writes serialize.
   - **Shared mutable state.** Default to splitting the target (the **separate-before-serializing-shared-state** principle skill). Serialize only for real invariants.
   - **Smallest safe decomposition.** If one worker is best, name why.
4. Give the implementer a specific scope: file paths, named data shape and organising structure per **principle-model-the-domain**, and success criteria. Follow the Subagents section for the optional `feature, refactoring` model entry. When multiple valid shapes exist, use **arena** to compare alternatives and cross-judge them. If delegation is unavailable, compare them sequentially yourself and disclose that the review was not independent. Re-ground upstream-derived files against their source. Port shared-primitive improvements to all consumers and verify each.
5. Verify on the matching surface. "Inconclusive" or wrong-surface is not a pass. Flag it.
6. Rebase into small, ordered commits. Stack follow-ups.
   Use the **sequence-verifiable-units** principle skill, building, verifying, and committing each small unit before the next.
7. If the design is contested, `interrogate` before shipping.
8. Run **Opening a PR**.

Code-coupled work (one feature, one migration) goes to a single owner with the checkpoint inline. That owner fans out internally after the blocking phase. Parent-level fan-out is for slices that produce independent artifacts (audits, cross-subsystem investigations, competing experiments). Rewrite the checkpoint at phase boundaries. Spawn a fresh owner rather than chaining interrupts.

**Reply:** what you built, what you chose and why, the throughput checkpoint, open decisions. Tables for design alternatives.
