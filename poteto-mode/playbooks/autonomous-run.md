### Autonomous run

You own the exit condition. Define done, then drive to it without stopping.

#### Procedure

1. Before the first iteration, state the exit condition as a checkable
   predicate (tests green, repro fixed, all N PRs merged, pixel-diff zero).
2. Wake on CI, merge, or ref changes:
   1. If an event watcher or scheduler is available, use it. Add a timed
      heartbeat when the host supports one.
   2. Otherwise recheck at useful intervals during the current session.
   3. If the host cannot continue after the session ends, checkpoint and
      report that unattended automation is unavailable. Do not promise a
      wake-up.
3. In each iteration, make the smallest change that the evidence justifies.
   Verify the change against the predicate. If the change advanced the
   predicate, commit it. If the change did not help, discard it. Revert a
   belt-and-suspenders change that "might help". Do not leave it in place.
   Sequence the work with the **sequence-verifiable-units** principle skill.
   Verify each unit before the next. Do not batch the checks at the end.
4. Address each discovery that supports the goal, within the user's scope and
   permissions. Put authorised out-of-band fixes in their own PR. Surface
   these items to the user:
   - irreversible actions
   - genuine product or preference calls that no experiment can settle
   - real dead ends

   Keep the predicate as the main drive. Return to it after each side fix.
5. Checkpoint every iteration with the **show-me-your-work** skill. Add a row
   for what changed and whether the predicate moved.
6. Stop when the predicate is met. A plateau is not a stop. Keep going and
   pivot your approach to push past the plateau. If you reach a genuine dead
   end, surface it. Do not spin. Never relax the predicate to declare victory.

#### Reply

Give the exit condition, the iterations run, what landed, what you discarded,
and the final predicate state.
