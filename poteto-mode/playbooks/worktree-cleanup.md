### Worktree and simulator cleanup

This is the one playbook that deletes user state with no code review to catch a
slip. The gates in the procedure are the review.

#### Procedure

1. Snapshot and audit.
   1. Record `df -h /`.
   2. Inventory the worktrees. The shipped
      `scripts/worktree-audit.sh [-b <pr-base-ref>] [repo-path]` inventories
      worktrees and suggests review buckets. It fetches the base ref and
      queries the forge. Run it only when those accesses are permitted and the
      prerequisites are available. Pass `-b` for a non-default PR base. The
      forge lookup can be unavailable, and the script cannot know which
      worktrees are in use.
   3. Otherwise use `git worktree list --porcelain`, `git status`, merge
      checks, and disk usage to assemble the inventory.
2. Treat buckets as advice, not permission. Cross-check active or pinned
   sessions and their worktrees. Use the host's available session information
   and ask the user where needed. If you cannot establish usage, hold the
   candidate.
3. Inspect uncertain usage with delegated agents when supported, or
   sequentially otherwise. Read only authorised, relevant transcripts. Consider
   sibling worktrees that delegated jobs use. Do not assume that an absent chat
   record means unused.
4. Before deletion, inspect tracked, untracked, and ignored files, and get any
   required approval. Hold active worktrees and any work with unknown ownership
   or potentially valuable uncommitted data. Never assume that untracked or
   ignored files are disposable.
5. Remove only confirmed, authorised candidates with `git worktree remove`.
   Force a removal, or remove leftover files, only with explicit permission for
   the data at risk. Prune stale metadata. Then re-list and compare disk usage.
6. If simulator or cache cleanup is requested, inspect the platform's available
   tools and candidates first. On macOS, `xcrun simctl` can list simulators and
   runtimes. Remove only explicitly authorised items. Report anything held or
   inaccessible.

#### Reply

Give `df -h /` before and after with the space reclaimed, the worktrees pruned,
and a one-line reason for each worktree held back (in use by which chat, or
uncommitted work).
