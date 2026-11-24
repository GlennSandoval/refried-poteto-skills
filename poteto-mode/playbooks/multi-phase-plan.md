### Multi-phase or multi-PR plan

You own the plan, not the code. The plan is a checklist that an owner runs box
by box and the operator audits from the evidence. The plan is the deliverable.
Do not implement.

#### Procedure

1. If the change is one or two files with an obvious approach, skip the plan.
   Say so and stop.
2. Settle open questions by prototype before you write, per
   `playbooks/prototype.md`. Ask the operator only about a product or
   preference call that no run can settle.
3. Write the plan file.
   1. Open with what changes, the PR ids in landing order, and the dependency
      graph. The graph says which PRs are independent and branch from trunk,
      which PRs wait for which, and the files that each PR may touch.
   2. Add one section per PR. One PR is one change with its own evidence (the
      **sequence-verifiable-units** principle skill).
   3. In each section, add checkboxes for what the PR depends on, the files it
      edits, the one change it builds, the result you see, and its
      verification.
4. Do not treat tests alone as sufficient verification. A PR is verified only
   when its unit, live, and perf boxes are all checked.
   - Each live box drives the real surface with a concrete scenario and a pass
     predicate.
   - The perf box names the metric, the probe, the trunk baseline measured
     first, and the number that fails.
   - If a PR changes an interaction, it waits for the operator's review before
     merge.
5. Hand back the plan path and stop. Execution starts on the operator's
   explicit go.

#### Reply

Give the plan path, the PR ids with their dependencies and the review-gated
set, and what stays unproven.
