### Session pickup

You own the resume point. Read the prior trail. Do not redo it.

#### Concepts

The prior trail is authoritative input. Resist the bias to re-derive it. A "let
me verify from scratch" pass treats the trail as untrustworthy, when it is
authoritative.

#### Procedure

1. Locate a prior trail that the active host exposes, a checkpoint, or a pushed
   branch.
   - Read the overview and the last messages first. Then scan back for
     decisions.
   - Access transcripts only with permission and only within this run or
     workspace.
   - Delegate long transcripts when supported. Otherwise reduce them
     sequentially.
   - If the trail is unavailable, report the gap. Do not assume a path. Do not
     claim what the trail says.
2. Reconstruct the operational state: the branch and worktree, what already
   landed (`git log`, `git diff` against the base), the open todos, and the
   decisions made.
3. Diff done against pending. Compare what shipped against what was planned.
   Name the resume point. Do not re-run the prior repro. Do not redo completed
   work.
4. Route the remaining work to the matching playbook and pick the verdict:
   continue the execution, ship a finished recommendation, ratify or override a
   prior conclusion, or postmortem a failed run. The pickup playbook ends here.
   The routed playbook owns the rest.
5. Verify the inherited claims against the original goal on the real artifact
   (the **principle-prove-it-works** skill). A passing prior self-report is not
   the proof.

#### Reply

Give where the prior agent stopped, what you inherited and what you redid
(ideally nothing redone), the resume point, and the outcome.
