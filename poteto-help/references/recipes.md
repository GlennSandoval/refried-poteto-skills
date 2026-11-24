# Prompts worth copying

Swap in the real paths, skills and done checks. Informal wording works. Ask for
skills by name; use the host's invocation syntax if it has one, or read the
installed skill file directly. Unattended and independent work depend on the
host's capabilities and permissions.

## Understand

- `Use poteto-mode to read <thread>. Restate the underlying issue in your own words, in plain English.`
- `Use in-your-own-words on <long or messy ask>.`
- `Use sharpen on <the prompt you're about to send>.`
- `Use poteto-mode to investigate why <symptom>. Give me what we know, the data used and your best hypotheses. Don't change code yet.`
- `Use how to understand <subsystem>, then why to find out why it broke recently.`
- `Use recall for my work on <topic> from last week, then read <issue>.`
- `Use teach to explain why you implemented it this way rather than <other way>. What did you trade off?`
- `Use poteto-mode to take over this branch. Read the decision log, find what's done and continue. Don't redo finished work.`

## Build

- Bug: `Use poteto-mode on <symptom>. Repro first, then fix and verify.`
- Bug in an app: `Use poteto-mode and verify-<app> to repro this. If it repros on main, fix it and show me a video as proof.`
- Bug with a cheap test: `Use poteto-mode to repro <bug> first. If there's a cheap test path, use tdd. Then fix and rerun.`
- Feature: `Use poteto-mode to add <behaviour>. <current output> stays byte-identical. Verify both.`
- Refactor: `Use poteto-mode to move <code> into one module, with zero behaviour change. Record the current output first and prove it's unchanged after.`
- Perf: `Use poteto-mode. <operation> takes <time> on <fixture>. Trace it, fix the measured cause, and show me before and after.`

## Design and plan

- `Use poteto-mode to prototype a few options for <feature>. Take screenshots or videos for me to compare.`
- `Use poteto-mode for <feature>. Use architect first and answer open questions with prototypes. Let me review before proceeding.`
- `Use poteto-mode to write a tutorial for how I would use <new package> first. Then use teach to explain why it beats the current one.`
- `Use arena for a second opinion on this thread and our approach.`
- `Use poteto-mode to turn this design into a plan. Small verifiable PRs, each with its own verification steps.`
- `Use poteto-mode to plan the migration of <library> to <target>. Small verifiable PRs. The result must match the original exactly, bugs included.`

## Review and ship

- `Use interrogate on the whole branch, but skeptically. Don't change anything yet. No nitpicks unless it's a real bug or regression.` Read the Dropped list too.
- `Use create-formal-verification-skill to prove <property> holds in <module>, even when <steps> interleave or retry.` After merges or refactors in that code, use maintain-formal-verification-skill.
- `Use swarm to check every package under <dir> against its check script. One worker per package, one report.`
- `Use poteto-mode to open the PR. Small ordered commits, evidence in the description.`
- `Use poteto-mode to babysit this PR and get it green.` For status only: `Use poteto-mode to check on PR <number>. Anything outstanding?`
- `Use poteto-mode to land the stack.`

## Away and back

- `Use poteto-mode. I'm stepping away. <goal> in a fresh worktree off <base>. Done means <checks>. Keep a decision log. Don't ask me before committing. Continue until done if supported; otherwise report where to resume. Stop and explain if truly stuck.`
- `Use show-me-your-work to catch me up on what you did last night.` Read its Attention section first.
- `Use ketchup` to catch up on this chat since your last message and list calls waiting on you.
- `Use poteto-mode for full autopilot on this queue. Each item is independent.`
- `Use poteto-mode to run these changes, but don't merge. I'll land them.`
- `Use reflect to capture what we learned so the next run doesn't repeat it.` Approve only edits that change a future decision.
- `Use bro` to restate the last reply in plain words.
