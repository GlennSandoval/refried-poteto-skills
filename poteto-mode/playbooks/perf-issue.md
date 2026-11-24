### Perf issue

You own the measurement story. Plan, review, and verify the numbers. Tie every
fix to a measurement. Do not read source instead of measuring.

#### Performance mantras

Try the mantras in this order, cheapest first:

1. Don't do it. Stop work whose result nothing uses, rather than cheapening
   it.
2. Do it, but don't do it again.
3. Do it less.
4. Do it later.
5. Do it when they're not looking.
6. Do it concurrently.
7. Do it cheaper.

When an earlier mantra meets the target, stop.

#### Procedure

1. Capture a baseline trace on the matching surface with an available profiler
   or driver. Vet the baseline, and each later number, with
   **benchmark-checklist**. If capture is unavailable, report the missing
   measurement. Do not claim a result.
2. Trace the code to ground hypotheses. Do not claim a perf ceiling without
   running it first. Order the hypotheses by the performance mantras.
3. Plan the fix from the trace.
   1. If the fix crosses a function boundary, use **architect** first.
   2. If delegation is supported, delegate the implementation and follow the
      Subagents section for the optional `perf-issue` model entry. Otherwise
      implement and review sequentially, and disclose the loss of
      independence.
   3. Capture a post-fix trace.
   4. Apply the **sequence-verifiable-units** principle skill. Verify each
      attempt before you try the next.
4. Parse and compare the artifacts (JSON to sqlite, diff). "Inconclusive" or
   wrong-surface is not a pass. Flag it.
5. Cite the measurement in the PR.
6. Run **Opening a PR**.

For sustained improvement against a metric, rather than a one-off fix, use the
Hillclimb playbook (`playbooks/hillclimb.md`).

#### Reply

Give the baseline number, the post-fix number, the delta, and the artifact
path.
