### Shipping

You own what lands. Verify each PR independently, land only the verified run
from the root, then keep your hands off the stack.

#### Concepts

- A verdict covers a patch. A chain rebase moves every PR above it to a new SHA
  without failing any check, so an old verdict can stop describing the code.
- The verified run is the contiguous set of verified PRs rooted at the bottom
  of the stack. The top PR of the run is the ceiling.
- A verified PR above an unverified one waits, because it cannot land without
  the code below it.

#### Procedure

1. **Resolve the forge, then verify each PR independently before it lands.**
   Use the active host's forge tool or an available CLI for the repository.
   For each PR, an independent verifier runs the change as a user would, on the
   real surface, parent against head. The verifier records `PASS`,
   `PASS+NOTES`, or `FAIL` with evidence. CI and bot approval are not
   substitutes. If no independent verifier or real-surface driver is
   available, perform the available checks sequentially, report the missing
   independence or access, and stop before merging.
2. **Land only the contiguous verified run rooted at the bottom.**
   1. Walk up from the lowest unmerged PR.
   2. Stop at the first PR that does not have `PASS` or `PASS+NOTES`.
   3. The PRs below that PR are the run. The top one is the ceiling.
   4. A verified PR above an unverified one waits. If its branch neither holds
      nor needs the code below it, you can move it onto trunk and land it on
      its own. It needs a fresh verdict first, because its old verdict ran
      with that code beneath it, and trunk does not have that code.
3. **Re-check that the verdicts still describe the code.** Compare
   `git patch-id` at the verdict SHA with the current head before you trust an
   older verdict.
   - If the patches differ only in tests, docs, or lint config, a lane's result
     stands when what it ran builds the same at both SHAs, apart from noise.
     Noise is a difference that also shows up between two builds of the verdict
     SHA, or an embedded commit SHA. Report each kind of noise with its files,
     so that a reader can check the call.
   - The change itself still gets fresh checks and a review, because the old
     verdict never saw it.
   - A lane with no build output, such as a dev server, cannot show this. Rerun
     that lane, and re-verify anything else that drifted.
4. **Land bottom-up, one PR at a time.**
   1. Use the available forge to merge the lowest unmerged PR, subject to
      approval and permissions.
   2. Check the forge-specific stack semantics. On GitHub, a PR that is based
      on its parent's branch merges into that branch, not trunk. Origin's plain
      merge may include lower PRs.
   3. Read back the state and the base, to distinguish a landed merge from a
      queue or auto-merge request.
   4. Enable auto-merge only for a verdict that covers the current head.
   5. After a merge lands, retarget the next PR to trunk. When authorised, move
      its patch onto the merge result. Use a lease for any permitted
      force-push.
   6. Apply the patch-id rule from step 3. Then wait for checks and a surviving
      verdict before you merge the PR.
5. **Leave the stack alone while it lands.** The move of the next PR in step 4
   is the only change to a branch or base.
   - On GitHub, the shipped `scripts/watch-pr/watch-pr --queued-stack` can
     watch the run with Bun and authenticated `gh` access. It bootstraps
     dependencies with `bun install --frozen-lockfile` if needed. Run it only
     when that installation is permitted. Pass the PR numbers bottom-to-top
     with `--stack-prs` and preserve that list on restart.
   - Otherwise use the forge's status and checks views to recheck each PR until
     the ceiling is merged.
   - A scheduler may repeat these checks if the host supports it. Otherwise
     monitor during the session and report that unattended monitoring is
     unavailable.
   - A base that moves to trunk when its parent merges is expected. Investigate
     stalls before you change anything.
6. **Stop at the ceiling.** Extending the run takes new verdicts, so it is a
   new pass through step 1.

#### Reply

Give the verified run and its ceiling, each PR's verdict and who produced it,
what landed and how you confirmed it, and what the next gap needs.
