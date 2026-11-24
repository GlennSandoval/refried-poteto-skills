### Hillclimb

You own the metric and the experiment's integrity. Supervise and review.
Delegate the attempts.

#### When to use this playbook

Use this playbook for sustained, iterative improvement of one measurable thing
against a target. A one-off fix is Bug fix or Perf issue. This playbook is the
loop.

#### Core discipline

Make one change, take one measurement, then keep or revert. Never stack
untested changes. Never claim a win from code inspection (the
**prove-it-works** principle skill).

#### Procedure

1. Ground the workload and architecture before you choose the metric.
   1. Trace the target.
   2. Name the realistic workload dimensions that can move the result (data
      size, history, state, concurrency).
   3. Select a case that reproduces the user's complaint. If no case
      reproduces it, fix the repro instead of hillclimbing.
   4. Fix one metric, the direction that counts as better, and a checkable stop
      predicate. The predicate pairs a target with a floor on attempts, so that
      a lucky early win cannot end the run. For example: "at least 50% better
      than baseline and at least 10 iterations".
   5. Use the user's numbers when given. Otherwise agree the numbers with the
      user.
2. Build the measurement harness, prove its sensitivity, then freeze it (the
   **build-the-lever** principle skill).
   1. Run contrasting realistic workloads. Confirm that the target case
      reproduces the symptom and that easier cases separate as expected. If the
      harness cannot distinguish them, revise the workload or metric.
   2. Vet the harness with the **benchmark-checklist** skill before you freeze
      it. Make it print its error count and a count of the work done.
   3. After the freeze, make one repeatable command emit the metric. Sample
      enough to clear the noise (median of N, not a single run).
   4. Before any change, record the baseline metric and a green run of the
      regression gate (the tests that must keep passing).
3. Open the decision log with the **show-me-your-work** skill. Use a
   `decision.tsv` with one row per attempt: id, hypothesis, change, before,
   after, delta, tests, verdict (kept or reverted), note. Read it before each
   attempt. Keep it out of the tree (gitignored).
4. Ground each hypothesis in the architecture model from step 1, so that it
   names a specific mechanism ("defer X off the boot path because it blocks
   first paint"), not "try memoizing something". For a perf metric, order the
   hypotheses by the "Performance mantras" section of the Perf issue playbook
   (`playbooks/perf-issue.md`). Borrow only their order, not the stop rule of
   that section.
5. Loop with one hypothesis per iteration:
   1. If delegation is supported, delegate the tightly scoped change and
      follow the Subagents section for the optional `hillclimb` model entry.
      Review the diff. When independent hypotheses are live, use separate
      worktrees and parallel agents if available. Otherwise run the attempts
      sequentially and disclose the lack of independent review.
   2. Measure before and after with the frozen harness, and run the regression
      gate.
   3. Accept the change only when the metric moves past noise and the gate
      stays green. Otherwise revert the change in full. Do not keep a tweak
      that "might help".
   4. Make one commit per accepted fix. Stage only the files that you changed
      (`git add <files>`, never `-A`).
   5. Log the row either way, kept or reverted.

   End each iteration with a check before the next begins (the
   **sequence-verifiable-units** principle skill). If the run is unattended,
   borrow only the wake mechanism from the Autonomous run playbook
   (`playbooks/autonomous-run.md`), not its stop rule.
6. Push past the first plateau. After a stall (several rejects in a row), do
   one of these before you conclude that the hill is climbed: pivot category,
   combine near-misses, re-read the source, or try something more radical.
   Correctness and simplicity outrank the number. Revert a win that breaks
   behaviour. Keep a simplification that holds the number (the
   **laziness-protocol** principle skill).
7. Stop when the predicate is met, or when the remaining ideas are marginal and
   not worth their cost. Do not relax the predicate to meet it. Do not quit
   while cheap untried hypotheses remain. If you are stuck, surface it. Do not
   spin.
8. Run **Opening a PR** with the accepted commits stacked in the order they
   landed.

#### Reply

Give the metric and target, the baseline to final with the percent delta, the
iterations run (kept and reverted), each accepted fix on one line, the
`decision.tsv` path, and the best idea you would try next if pushed further.
