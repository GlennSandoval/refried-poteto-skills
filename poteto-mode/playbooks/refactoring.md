### Refactoring

You own the contract. The structure changes. The behaviour does not.

#### Scope

Refactoring is distinct from Feature, which adds behaviour, and from Bug fix,
which corrects it. This playbook is for the focused-to-medium change. Large or
cross-cutting structural work belongs to the **figure-it-out** skill.

If the cleanup reveals a missing feature or a real bug, split it out. Ship the
structural change first, against the pinned contract. A redesign is allowed,
but name it and route it to Feature.

#### Procedure

1. Pin the behaviour contract first.
   1. Trace the affected subsystem to learn the contract.
   2. Write a characterisation test, snapshot, or equivalence harness that
      captures current behaviour before any structure moves.
   3. If the area has no coverage, write the pin before you touch structure.
      Type check and lint are not a pin.
2. Name the structure that the code is missing, per
   **principle-model-the-domain**. Boring code stays when the shape is already
   clear and local. The reshape must delete branches or invalid states. It must
   not add indirection.
3. Name the target shape. State what the module layout, types, and call graph
   should be if built today (**principle-foundational-thinking**,
   **principle-redesign-from-first-principles**). If the target crosses a
   function boundary, run the **architect** skill for the shape before the
   move.
4. Subtract before you add. Delete dead code, collapse one-caller wrappers,
   drop redundant validators, and remove orphan references before you
   introduce the new shape (**principle-subtract-before-you-add**). Ship the
   smallest change that reaches the target shape
   (**principle-laziness-protocol**). Revert a speculative cleanup that "might
   help".
5. Move in small behaviour-preserving steps. Keep the pin green after each
   step.
   - For API reshapes, migrate every caller and delete the old API in the same
     wave (**principle-migrate-callers-then-delete-legacy-apis**). Add no
     compatibility shims or parallel paths.
   - Check every rename against actual files, including strings, prose, and
     back-references.
   - If delegation is supported, delegate mechanical edits with a specific
     scope and follow the Subagents section for the optional
     `feature, refactoring` model entry. Otherwise make and review them
     sequentially, and disclose the loss of independence.
6. Prove that behaviour is unchanged on the real artifact, not merely that the
   code compiles (**principle-prove-it-works**). For larger reshapes, use an
   equivalence check, a baseline replay, or a smoke run with an available
   driver on the matching surface. Report unavailable verification.
7. Confirm that the change is worth keeping. The success measure is reduced
   reader load (**principle-minimize-reader-load**). If the diff does not lower
   reader load somewhere, revert it.
8. Rebase into small ordered commits: a subtraction commit, then the reshape,
   then any follow-on cleanup. Shape them with the
   **sequence-verifiable-units** principle skill, so that each
   behaviour-preserving slice stays green before the next. Run
   **Opening a PR**.

#### Reply

Give the structure that changed, the pin you held it against, the equivalence
proof, the reader-load delta, and what shipped and what you reverted. Add no
new behaviour.
