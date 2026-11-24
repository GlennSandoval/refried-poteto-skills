### Autopilot-full

You own the verdicts, never the PRs. One owner carries each PR from build to
merge. Nothing merges until your swarm, which never wrote the code, has proven
the code that lands.

#### Concepts

A verdict covers one patch. Green CI covers one head. Step 4 runs a full swarm
once, and runs it again only for a major change. The patch-id rule in
`playbooks/shipping.md` can carry a lane's result. Every new head needs its own
green CI.

#### Procedure

1. **Apply the operator's gates first.** The grant covers only the queue's
   items. Items that the operator names as theirs, and PRs outside the queue,
   stop at merge-ready. A request to state the plan is not a go.
2. **Assign one owner per PR and keep its work recoverable.** Use an available
   forge tool for the repository. Each owner does these things:
   - Builds the change.
   - Opens its PR per `playbooks/opening-a-pr.md`.
   - Proves the change on the real artifact.
   - Babysits the PR to green per `playbooks/babysit.md`.

   Merge only after steps 4 and 5 and the required approvals. When agents are
   unavailable, work through the owners sequentially and disclose the loss of
   independent verification. Do not merge without an independent verdict.

   For each owner:

   1. When authorised, open the PR early so that CI and bots run alongside the
      work.
   2. Inspect the diff for unnecessary code and prose, and apply
      **no-comments**, before independent verification.
   3. When permitted, rebase onto current trunk.
   4. Report the code-ready head before self-proof. Report every later head
      and the merge-ready state.
   5. Run the relevant checks on each head that needs a verifier.
   6. Keep a durable decision trail with **show-me-your-work**. When
      authorised, push finished units.
   7. Where the host exposes them, record the agent IDs, the states, and a
      reasonable stuck-after time.
   8. Force-push only your own branch, and only when authorised. Use a lease
      pinned to the SHA that you last pushed or took over.
   9. If an unexpected external push occurs, stop and report it.
3. **Run owners off trunk, never stacked,** so that each PR lands on its own.
   Run independent owners in parallel when supported. Otherwise run them
   sequentially.
4. **Swarm-verify once.** Use **swarm** to run independent verifiers at the
   code-ready SHA.
   - For new behaviour, a redesign, or a large new diff, repeat the full swarm.
   - For a rebase, conflict resolution, or minor fix, use a single verifier.
   - Each verifier reruns the gates, exercises load-bearing behaviour on the
     real surface with an available driver, and audits the diff.
   - Audit the receipts.
   - If independent agents or the real surface are unavailable, report the
     gap. Do not claim a clean verdict. Do not merge.

   Block a PR only for a problem that you can show: a failing run at the head
   or a doc line that the PR made wrong. A problem that the PR's base already
   has does not block, unless the PR copies it or newly reaches it. The base is
   trunk, or the PR below it in a stack. Only a bug a user would hit, a failed
   gate, or a wrong shipped doc blocks. Put everything else in a follow-up.
5. **Let the owner merge only what you verified, tested on the trunk it lands
   on.** Green CI alone never authorises a merge. After the swarm's lanes have
   started, merge prep rebases onto current trunk, reports the new head, and
   waits for green CI.

   Right before the merge, fetch trunk and ask whether its changes can affect
   the patch. Do not rebase for every trunk move, because that never ends.
   - If the code that would land was never tested, rebase and wait for CI.
     Examples are a conflict, a file that both sides changed, or a change to
     which checks run for the PR.
   - If a lockfile changed on both sides, do not rebase when both of these are
     true: a frozen install passes on the merge result, and the packages that
     the PR changes resolve there as on the head. That install tests the
     lockfile that would land. If the install fails, the rebase must repair
     it.
   - If trunk changed a caller of the patch, or something the patch depends on
     (code it calls, or a dependency version), run the patch's checks on the
     merge result. Merge on a pass.
   - Otherwise, merge.
   - If trunk would force a third rebase past merge prep, hold and report to
     the root. The root sequences the colliding work.
6. **Run the root layer.** Anything that loosens a gate, such as a raised
   budget or an allowlist entry, needs a verifier's proof and then your fresh
   countersign, because the owner is the one who wants green. Under a grant
   that covers approvals, that countersign is the approval. The owner's record
   of it points at your countersign for a lane to check. Always remove a
   disabled or soft-failed check, because it stops guarding every case. Never
   give or bypass an approval that the forge enforces, because no countersign
   covers it.

   On the operator's go, audit until no delegated work remains:
   1. Use an available scheduler or watcher.
   2. Re-read this playbook.
   3. Check agent progress and side effects.
   4. Record drift.
   5. Answer agents that wait on you.
   6. Replace stuck agents when supported.
   7. Use **ketchup** for material updates.

   Without a scheduler, audit during the active session, checkpoint, and
   report that unattended monitoring cannot continue after the session ends.
7. **Stand down at once on the operator's stop.** A hold reaches every owner as
   a zero-writes order. Each owner reports where it stands and keeps its brief
   until the operator releases it.

#### Reply

Catch the operator up per the **ketchup** skill. Cover each PR's state and
verdict, what merged, the countersigns and why, the open operator gates, and
the parked follow-ups. Link to each PR and to the trails.
