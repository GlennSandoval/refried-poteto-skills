### Worktree and simulator cleanup

1. Snapshot and audit. Record `df -h /`. The shipped `scripts/worktree-audit.sh [-b <pr-base-ref>] [repo-path]` inventories worktrees and suggests review buckets. It fetches the base ref and queries the forge, so run it only when those accesses are permitted and prerequisites are available; pass `-b` for a non-default PR base. Forge lookup can be unavailable, and the script cannot know which worktrees are in use. Otherwise use `git worktree list --porcelain`, `git status`, merge checks, and disk usage to assemble the inventory.
2. Treat buckets as advice, not permission. Cross-check active or pinned sessions and their worktrees using the host's available session information and the user where needed. If usage cannot be established, hold the candidate.
3. Inspect uncertain usage with delegated agents when supported, or sequentially otherwise. Read only authorised, relevant transcripts. Consider sibling worktrees used by delegated jobs; do not assume an absent chat record means unused.
4. Before deletion, inspect tracked, untracked, and ignored files and obtain any required approval. Hold active worktrees and any work with unknown ownership or potentially valuable uncommitted data. Never assume untracked or ignored files are disposable.
5. Remove only confirmed, authorised candidates with `git worktree remove`; use force or remove leftover files only with explicit permission for the data at risk. Prune stale metadata, then re-list and compare disk usage.
6. If simulator or cache cleanup is requested, inspect the platform's available tools and candidates first. On macOS, `xcrun simctl` can list simulators and runtimes. Remove only explicitly authorised items; report anything held or inaccessible.

This is the one playbook that deletes user state with no code review to catch a slip, so the gates above are the review.

**Reply:** `df -h /` before and after with space reclaimed, the worktrees pruned, and a one-line reason for each held back (in-use by which chat, or uncommitted work).
