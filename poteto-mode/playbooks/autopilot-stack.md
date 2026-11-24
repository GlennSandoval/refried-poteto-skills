### Autopilot-stack

Run the Autopilot-full playbook, but do not merge.

#### Procedure

1. In place of step 5 of Autopilot-full, stop at verified. Stop when each PR is
   verified and green at its current head. Then hand the PRs to the operator.
   After the handoff, nobody pushes without the operator's go. Include this
   no-merge rule in every scheduled audit. If scheduling is unavailable,
   report the limitation.
2. Stack a PR only when it builds on another PR. This is the one exception to
   step 3 of Autopilot-full.
   1. Base the PR on the other PR's branch in place of trunk, per
      `playbooks/opening-a-pr.md`.
   2. In place of the rebase onto trunk in step 2 of Autopilot-full, rebase
      each PR onto its parent PR's branch. Rebase the stack root onto trunk.
   3. When the lower PR gets a new head, restack the PRs above it. If the
      restack leaves the `git patch-id` of a PR unchanged, that PR keeps its
      verdict.

#### Reply

List each PR with its verdict, in place of what merged.
