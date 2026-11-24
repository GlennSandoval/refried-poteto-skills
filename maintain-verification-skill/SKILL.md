---
name: maintain-verification-skill
description: "Keep a project's verification skill and feature map accurate by reviewing source and driving every feature live. Use when auditing or updating a verification skill."
---

# Maintain a verification skill

## Purpose

A feature map becomes wrong as soon as the app changes. This skill is the
upkeep loop for a skill that `create-verification-skill` generated, or for any
project-local verification skill that has a feature map.

The unit of rigour is the feature, not every sentence. Cover every feature file
from source and exercise every feature live. Do not terminalise every bullet.

Run this workflow only when the user explicitly requests it, including on hosts
that do not support opt-in-only metadata.

## Outcomes

Select one outcome and say which one:

- **clean** — every feature got source coverage and live coverage, and nothing
  is worth shipping. Create no branch and no PR.
- **changed** — proven corrections to the docs, harness, or map are ready to
  ship.
- **blocked** — coverage could not finish, or a proven fix could not be made
  safely. Say exactly what blocked it.

## Edit scope

Edit only the directory of the verification skill: its SKILL.md, `features/`,
and any harness scripts that it owns. Never edit product code during a run.

If the map describes a behaviour that the app no longer has, the cause is one
of two things:

- Doc drift: fix the map.
- Product regression: report it. Do not hide it in the docs.

## Pass

### 0. Locate the target

1. Find project-local skills in the locations that the active host and the
   project document. If neither documents a location, inspect
   `.agents/skills/`.
2. Find the skill whose body has launch and drive sections and a feature map.
3. If there are several candidates, ask which one to use.
4. If there is none, point the user to the `create-verification-skill` skill
   through host discovery or its source path. Do not invent a target.

### 1. Index hygiene

1. Read the feature map README and glob its sibling files.
2. Fix missing, extra, duplicate, or dead entries.

Keep this step light. Do not generate an inventory.

### 2. Source wave

If the host supports and permits delegation:

1. Read `~/.config/pstack/models.md` if it exists. Use per-role configuration
   only when the host supports it. Otherwise use the host defaults.
2. Launch one read-only subagent for each feature file, all at the same time.
3. Each reader explains how the feature works from source, flags likely doc
   drift with citations, and returns one concise live-verification recipe.
   Children never drive the app and never edit.

If delegation is not available, do the same source passes in sequence. Disclose
that the review lost its independence.

Return shape: feature summary / source entry points / likely drift or none /
one recipe.

### 3. Reconcile

1. Confirm that every feature file has a returned summary.
2. Merge overlapping recipes into as few app states as practical.
3. Spot-check the cited drift. Do not re-prove the claims that are clean.
4. Sweep recent churn for user-facing surfaces that the map does not list.
   Require a concrete source path before you call a surface missing.

### 4. Live pass

The live pass is required even when the source looks clean. The coordinator
owns all driving.

Follow the launch model of the verification skill. Its Launch section decides
the model, not this skill:

- For servers and UIs, drive one long-lived instance in series.
- For short-lived CLIs, use a fresh isolated session for each drive.

Exercise every feature at least once. Hold these three invariants for the whole
pass, whatever the failure:

1. Never drive an instance that you have not health-checked since it last did
   something unexpected.
   - Run doctor before the first drive.
   - Where sessions are the unit, run doctor on each fresh session.
   - Run doctor again after any failed drive.
   - If doctor cannot see the failure (for example a wedged UI state on a
     healthy process), reset to a known state or relaunch. Do not hope that the
     state recovers.
2. Evidence that you captured survives every cleanup. Check this at its named
   location. Do not assume it.
3. Nothing that a drive started outlives the usefulness of that drive. Clean
   the residue of a failed iteration whether the session is stuck, exited, or
   shared. For a shared instance, clean the residue, not the instance.

Handle these cases as follows:

- If doctor fails because the skill drifted, that is drift. Fix it within the
  edit scope and retry once. Restart only what the fix invalidated. If the
  retry fails, call the pass `blocked`.
- Mark a feature `verified-unreachable` only when you can name the concrete
  prerequisite (authentication, entitlement, OS, or external state) and the
  route that you attempted. If the map omits that prerequisite, that is drift.
- Re-drive live every harness fix that comes from triage, before it ships.
- Do the final teardown after the last drive of the run, including those
  re-proofs, so that nothing outlives the run. The evidence stays, as the skill
  requires.

### 5. Triage

Classify each finding:

- The user-POV description is wrong or missing: doc drift. Fix it.
- The behaviour works but the harness cannot drive it: harness gap. Fix it. A
  harness fix follows the same helpers rule as generation: scripts are
  executable and the skill body documents their invocation.
- The app behaviour is broken: product gap. Record it for the user. Keep it out
  of the verification changes.

### 6. Ship or stop

- For **changed**, prepare one coherent set of proven corrections. Follow the
  contribution workflow of the project and the permissions of the user. Create
  a PR only when you are authorised and the host supports it. Otherwise, hand
  over the changes.
- For **clean** or **blocked**, report the outcome and the coverage honestly.
- If live driving or independent review was not available, say what you did not
  verify and why.

Keep concise run notes in a scratch location. Record the features covered, the
unreachable prerequisites, the confirmed drift, and the outcome. Do not commit
the notes.
