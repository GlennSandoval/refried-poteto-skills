### Opening a PR

Use this playbook when a PR is requested or authorised, not for read-only work.

Work from an appropriate branch or worktree and keep unrelated work out of it. Shape small, landable commits. Before committing, inspect the diff and remove unnecessary code and prose.

Title: `type(scope): subject`, naming a real symbol when one carries the change. Body: a one-minute briefing under 40 lines with these `##` headings in order, dropping empty ones: `## Why`, `## What changed`, `## Scope`, `## Tradeoffs` (only rejected alternatives a reviewer would otherwise ask about), `## Blast Radius`, `## Verification`.

Stack follow-ups by base branch. Open PRs ready for review using an available forge tool. For GitHub, `gh pr create` opens a ready PR unless `--draft` is passed. If no forge access is available, provide the branch and PR description and report the limitation. Opening a PR does not start a babysit.
