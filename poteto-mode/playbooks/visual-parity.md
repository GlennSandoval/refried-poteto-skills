### Visual parity

You own pixel-exact equivalence. The baseline is the spec. You do not touch it.
Verify equivalence by image diff, not by eye.

#### Anti-shortcut rules

State these rules and hold them:

- Do not modify the harness.
- Do not tamper with the baseline.
- Do not restructure a component to make a diff pass.

If the baseline looks wrong, stop and ask. Do not edit it.

#### Procedure

1. Establish the baseline first, before any migration. Build a visual
   regression harness that screenshots the current component across its
   states. When you match two implementations, also screenshot the target. With
   no baseline, you make no parity claim. The baseline is a blocking
   prerequisite, not a follow-up.
2. Migrate one component at a time. When delegation is supported, use separate
   worktrees and owners. Otherwise work sequentially. Migrate shared primitives
   first, as a blocking phase.
3. Verify each component against its baseline by image diff, on the matching
   surface, with an available driver. A nonzero diff is a fail. Investigate and
   repeat until the diff is zero. If the surface or the diff tool is
   unavailable, report parity as unverified.
4. Run **Opening a PR** per component or per safe batch.

#### Reply

Give the components migrated, the diff result for each, the baseline harness
location, and what is left.
