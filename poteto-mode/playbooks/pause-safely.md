### Pause safely

**You own a clean stop. Leave a checkpoint a cold-start agent can resume from.** This is explicit only. On "keep going", "going to bed, keep going", or "don't stop", do not pause.

1. Stop at a safe boundary. Finish the current atomic step or back out of it. Start nothing new, and cancel any nested subagents.
2. Take no irreversible action to pause. No PR and no push unless you already had one out.
3. Make your work durable when permitted. Commit only your own edits as a clear `wip:` commit if the operator authorises commits; leave unrelated work untouched. If a commit is unavailable or not authorised, preserve the work in place and report its state. If the tree is broken, record that in the checkpoint.
4. Write a resume note in a permitted durable location. Capture intent, progress, verification, current state, next steps, key files, and gotchas. If a **show-me-your-work** trail exists, point at it instead of duplicating it. If no writable location is available, include the checkpoint in the reply.

**Reply:** where you are in the loop, what's on disk versus still in your head (paths, no diff dumps), the commits you made and whether the tree is clean, and the first action on resume. This is a pause, not a final report.
