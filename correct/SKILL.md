---
name: correct
description: "Find the mistakes agents keep repeating in this repo and make each one impossible. Try architecture first, then types, then a lint whose error names the fix, then a test, and write docs last. Prove each check fails on a real past mistake. Repeat this each time the operator corrects you. Use for /correct."
---

# Correct

Apply this skill only when the user requests it or another active skill routes
to it.

The operator keeps correcting agents in this repo for the same mistakes. This
skill changes the repo so the next agent cannot make them.

Assume that every contributor is an agent that sees only the files it opened,
copies the nearest example, and takes the shortest path that compiles. Design
the repo so that a change that looks right from one file is right for the whole
repo.

## Find the mistake classes

1. Read recent commits, reverts, review comments, agent instruction files, and
   comments that explain workarounds.
2. Group the mistakes into classes.
3. Count a class only after it has happened twice.

## Choose the fix level

Fix each class at the highest level that works. The levels are in order, from
strongest to weakest:

1. **Eliminate it with architecture.**
   - Give each piece of state one owner and each task one supported way.
   - Hide internals so that the wrong import fails.
   - Replace hand-synced lists with one source of truth.
   - Delete old ways and dead code that an agent would copy.
2. **Enforce it with types so the bad state cannot be written.**
   - If bad code still compiles, add a lint or CI check. Its error names the
     file, type, or function to use instead.
   - If the pattern is already common, fail only when a change adds more.
3. **Test the behaviour.**
   - Fix or delete any test that still passes when the behaviour it checks
     breaks.
   - Fix or delete any test that fails when only the internals change.
4. **Write docs or agent rules last, and only for judgment calls.** Nothing
   fails when an agent skips them.

## Fix and prove

1. Fix the most frequent classes now. Make one commit for each class.
2. Prove that each new check fails on a real past mistake.
3. Run the same command locally and in CI.
4. Put each exception on the offending line. Include a reason, an expiry date,
   and a human's approval.

## Keep the rule table

Keep a table in the agent instruction file. The table pairs each rule with what
enforces it.

1. When the operator corrects you, fix the mistake and add the rule.
2. If the rule was already there and nothing enforces it, treat the mistake as
   a repeat. Fix it at the highest level in the same change.
3. Drop a rule when its mistake can no longer happen.

## Reply

Reply with each class, its evidence, the level that you picked, and why a
higher level did not work.
