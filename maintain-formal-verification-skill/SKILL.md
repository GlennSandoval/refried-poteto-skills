---
name: maintain-formal-verification-skill
description: "Bring a project's formal verification back in line with changed code: update the model, harness, or properties, rerun, and distinguish verification drift from bugs. Use to check whether a model remains true to the code after merges or refactors."
---

# Maintain a formal verification skill

## Purpose

A formal check proves a property of what it describes. When the code changes
and the verification does not, the check can keep passing while it describes
code that no longer exists. That pass is the dangerous case, because it looks
like a proof.

This skill is the upkeep loop for a verify skill that
`create-formal-verification-skill` generated, or for any project-local skill
that runs a model checker, prover, or code-level verifier against named code.

The project-local skill handles a change that an agent makes while it uses that
skill. This skill handles the changes that skipped it: merges, edits made
without the skill, and drift that builds up across many commits.

Run this workflow only when the user explicitly requests it, including on hosts
that do not support opt-in-only metadata.

## Outcomes

Give each check one outcome and say which one:

- **in sync**: no change since the last sync alters what the check describes,
  and the check passes.
- **updated**: the code changed, the verification now describes the new code,
  and the check passes.
- **bug**: the verification describes the current code, and the code breaks the
  property. This is a finding about the code. It is not drift.
- **blocked**: the check could not be brought back in line, or could not run.
  Say exactly why.

A check can be both updated and bug: the update makes the verification describe
the code again, and then the property fails on it.

## Edit scope

Edit only the verification: models, harnesses, property files, and the verify
skill itself. Never edit product code during a run, unless the user asks you
to.

When a property fails on the current code, do not weaken the property or the
model to make it pass. Report the failure.

## Pass

### 1. Find the checks

1. A verify skill has no fixed name. Find project-local skills in the locations
   that the active host and the project document. If neither documents a
   location, inspect `.agents/skills/`.
2. Find the skills that run a model checker, a prover, or another verifier
   against named code.
3. Read each skill that you find, or the skill that the user named.
4. For each check, collect:
   - the property;
   - the code that it covers;
   - the bounds and assumptions;
   - the command that runs it;
   - the commit where it was last confirmed to describe the code.
5. If no verify skill exists, point the user to
   `create-formal-verification-skill` through host discovery or its source
   path.
6. If the skill does not record a sync commit, use the last commit that changed
   the verification files, and say that you did. This is a fallback. It is not
   proof that the old verification matched that commit.

### 2. Run it as it is

1. Run each check once before you change anything.
2. Record the result.

A pass here does not tell you that the code is correct. It tells you that the
old description still holds. A failure here can be drift or a bug. Do not
decide which until step 5.

### 3. Read every change to covered code

1. Diff the covered files from the sync commit to the current commit.
2. Read each commit message.
3. Look for code that moved. A covered function that is renamed, split, or
   moved to another file is still covered code.
4. Look for new code that touches the state that a check guards, such as a new
   function that writes the same fields.

Decide which of these four categories each change belongs to:

- **No effect.** The change does not alter anything that the verification
  describes, such as formatting, comments, or code paths that the verification
  does not cover. Check this against the model or harness, not against the
  commit message.
- **The verification no longer describes the code.** A step that was one
  indivisible action is now two, a branch was added or removed, a check moved,
  a new path reaches the guarded state, or a value now has a different range.
  The model or harness must change.
- **The promise changed on purpose.** The change alters what the code promises,
  and evidence in the change says that this is intended: the doc comment, the
  tests, the changelog, or the commit message. The property must change, and
  you must cite that evidence.
- **The promise may be broken.** The code changed, and no evidence says that
  the promise changed. Treat a failure that follows as a bug candidate.

### 4. Update from the code, not from the result

1. Change the model or harness so that each changed part again points to code
   that a reviewer can open.
2. Keep one indivisible step in the code as one step in the verification.
3. Write the update from the code before you rerun. Do not shape it by what
   makes the check pass.
4. Change a property only for a promise that changed on purpose. Write down the
   old wording, the new wording, and the evidence.
5. Keep the bounds, unless the change makes them wrong. If you must reduce a
   bound, say so in the report.

### 5. Rerun and judge each result

If the check passes:

1. Remember that the check can now pass on a description that has lost the
   ability to fail.
2. Break the new code in the way that the property guards against, such as
   removing a new check or reordering a new step.
3. Confirm that the check catches the break.
4. Drop the break.

If the check fails:

1. Replay the counterexample against the real code, step by step.
2. If a step cannot happen in the code, the verification is wrong. Fix the
   verification and say what was wrong.
3. If every step can happen, it is a bug. Then:
   - Name the commit that introduced it.
   - Tell the counterexample as a sequence of steps in the words of the code.
   - State the harm in one sentence.
   - If a cheap test or reproduction against the real code shows the bug, add
     it to the report as evidence. Do not commit it to the product code.

### 6. Update the verify skill

1. Update the code that each check covers, the commands, the bounds, the
   assumptions, and the sync commit.
2. Set the sync commit to the commit that you checked.
3. Do not move the sync commit for a blocked check, and say so in the report.
4. Follow the verify skill once as the next agent would, so that you know its
   steps still run.
5. If tools, access, or permissions prevent this, report the blocked check and
   the unverified steps. Do not claim that it is in sync.

## Report

Tell the user, for each check:

- the outcome, and the commits that you read;
- what changed in the verification and why, with a short reason for each
  change: the code changed shape, or the promise changed on purpose (with the
  evidence);
- the rerun result, and the break that you used to show that the updated check
  can still fail;
- each bug, in plain words: the counterexample as steps in the words of the
  code, the harm, and the commit that introduced it;
- what the verification still does not cover, including new code that it should
  cover and does not.

Say outright which failures were drift in the verification and which were bugs
in the code. For a check that passed before you updated it and fails after, say
that the old pass was on a stale description.

Put the verification updates in a change of their own, separate from any
product fix.
