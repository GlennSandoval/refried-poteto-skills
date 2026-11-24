### Feature

You own the design. Plan, review, and verify. If delegation is supported,
delegate the implementation. Otherwise implement and review sequentially, and
disclose the loss of independence.

#### Ownership of code-coupled work

Send code-coupled work (one feature, one migration) to a single owner with the
checkpoint inline. That owner fans out internally after the blocking phase.
Parent-level fan-out is for slices that produce independent artifacts (audits,
cross-subsystem investigations, competing experiments). Rewrite the checkpoint
at phase boundaries. Spawn a fresh owner rather than chain interrupts.

#### Procedure

1. Trace the affected subsystem.
2. Use `architect` for the shape.
3. Write the throughput checkpoint as four todo items. If a dimension does not
   apply (single file, no fan-out), keep its item with `n/a: <reason>`. Do not
   drop it.
   - **Blocking first steps.** Gates run before fan-out.
   - **Independent workstreams.** Disjoint files, services, or layers
     parallelise. Shared writes serialise.
   - **Shared mutable state.** Default to splitting the target (the
     **separate-before-serializing-shared-state** principle skill). Serialise
     only for real invariants.
   - **Smallest safe decomposition.** If one worker is best, name why.
4. Give the implementer a specific scope: file paths, the named data shape and
   organising structure per **principle-model-the-domain**, and success
   criteria. Follow the Subagents section for the optional `feature,
   refactoring` model entry.
   - When multiple valid shapes exist, use **arena** to compare the
     alternatives and cross-judge them.
   - If delegation is unavailable, compare them sequentially yourself and
     disclose that the review was not independent.
   - Re-ground upstream-derived files against their source.
   - Port shared-primitive improvements to all consumers and verify each.
5. Verify on the matching surface. "Inconclusive" or wrong-surface is not a
   pass. Flag it.
6. Rebase into small, ordered commits. Stack follow-ups. Use the
   **sequence-verifiable-units** principle skill: build, verify, and commit
   each small unit before the next.
7. If the design is contested, run `interrogate` before shipping.
8. Run **Opening a PR**.

#### Reply

Give what you built, what you chose and why, the throughput checkpoint, and the
open decisions. Use tables for design alternatives.
