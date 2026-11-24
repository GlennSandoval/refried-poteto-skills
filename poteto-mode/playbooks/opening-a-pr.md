### Opening a PR

Use this playbook when a PR is requested or authorised. Do not use it for
read-only work.

#### Format

- Title: `type(scope): subject`. Name a real symbol when one carries the
  change.
- Body: a one-minute briefing under 40 lines. Use these `##` headings in this
  order and drop the empty ones:
  1. `## Why`
  2. `## What changed`
  3. `## Scope`
  4. `## Tradeoffs` (only rejected alternatives that a reviewer would otherwise
     ask about)
  5. `## Blast Radius`
  6. `## Verification`

#### Procedure

1. Work from an appropriate branch or worktree. Keep unrelated work out of it.
2. Shape small, landable commits.
3. Before you commit, inspect the diff and remove unnecessary code and prose.
4. Stack follow-ups by base branch.
5. Open the PR ready for review with an available forge tool. On GitHub,
   `gh pr create` opens a ready PR unless you pass `--draft`.
6. If no forge access is available, provide the branch and the PR description,
   and report the limitation.

Opening a PR does not start a babysit.
