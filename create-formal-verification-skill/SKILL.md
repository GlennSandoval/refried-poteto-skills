---
name: create-formal-verification-skill
description: "Generate a project-local formal verification skill for high-risk code. Use to model-check a race, prove an invariant, or verify concurrency, retries, state machines, parsers, or unsafe code beyond tests."
---

# Create a formal verification skill

## Purpose

A test checks the cases that someone thought to write. Formal verification
checks every case in a stated scope: every order of steps in a model, every
input up to a bound, or every input.

This skill finds the part of the repository where that matters most and
verifies one property of it. It leaves a project-local skill that lets the next
agent check a change against that property.

Write the project-local skill for an agent that reads it cold, in the middle of
a change, and has never seen your work. The user must be able to trust the
result and act on it without learning the verification language.

Run this workflow only when the user explicitly requests it, including on hosts
that do not support opt-in-only metadata.

## Choose the target from the code

Answer from the codebase. Ask the user only about what you cannot observe. If
the user named an area or a bug, start there.

A good target is a promise that the code makes, where a break harms users and
tests rarely reach the case that breaks it. Choose the strongest such target in
the repository, not the target that is easiest to verify.

## Let the question choose the tool

Pick the tool that answers the question at the lowest cost: a model checker, a
proof assistant, an SMT-backed verifier, or another tool.

- If the question is whether events can happen in a bad order, a model checker
  over a small model of the design usually suits. TLA+ is the default for this
  question, in any language.
- If the question is whether the code itself behaves for every input (for
  example memory safety, overflow, or a data-structure invariant), a verifier
  that runs on the code usually suits.
- If no verifier runs on this language, say so. Test the real code with
  generated inputs, not a hand model of the function. Report this as testing,
  not as a formal proof.
- If a property must hold at every size and a bound is not enough, a proof can
  be necessary.

Prefer a tool that the developers of the repository can install and run. Tell
the user why you chose the tool.

## What makes a verification good

- **True to the code.** Every part of the model or proof points to code that a
  reviewer can open. What the verification treats as one indivisible step is
  one indivisible step in the code. Names come from this repository.
- **Able to fail.** A check that you have never seen fail proves nothing. Show
  each property failing on a broken variant of the code that it guards, such as
  a removed check or a reordered step.
- **Findings stay findings.** When the current code breaks the property, report
  it with the counterexample in the terms of the code. Do not weaken the
  property or the model until it passes. Do not change product code unless the
  user asks.
- **Honest about scope.** Say what is verified, under which bounds and
  assumptions, and what is left out. A pass covers the model or the bound, not
  the whole system.
- **Readable without the tool.** State the property and the harm in one plain
  sentence each. Tell a counterexample as a short sequence of steps in the
  words of the code.
- **Cheap to rerun.** Provide one command, a reproducible tool version, and a
  run that is short enough that the next agent uses it on every relevant
  change.
- **Kept in step with the code.** Record which files and functions each check
  covers, and the commit at which you last confirmed that the verification
  describes them. When the covered code changes after that commit, the next
  agent can see that the verification needs another look.

## Generate the verify skill

### Location and frontmatter

1. Find the documented project convention or the active host convention for
   project-local skills.
2. Use that supported location. If neither documents one, use
   `.agents/skills/<verification-name>/SKILL.md`.
3. Write a skill with standard Agent Skills YAML frontmatter that names the area
   and says when to use the skill.

Automatic invocation depends on the host. Check the host's discovery and
registration procedure. A file alone does not guarantee registration or a slash
command. If you cannot verify registration, report the path and tell the user
to supply the file as context.

### Content

From the skill alone, the next agent must be able to do these tasks:

- Tell whether a change touches the verified code.
- Run the check.
- Tell a real bug from a modelling error.
- Update the verification when a change is intended.

Put the coverage record and the sync commit in the skill. Tell the next agent
to move the sync commit forward only after it confirms that the verification
describes the code at the new commit. Use the real commands, paths, and nouns
of this repository. Leave no placeholders.

### TLA+ models

For a TLA+ model, tell the next agent to use a statechart or counterexample
visualisation skill, but only if the host can discover one.

If the host cannot discover such a skill, the next agent interprets the output
of the checker directly:

1. Describe each violation as a sequence of states and actions in the terms of
   the code.
2. Report a passing result with its bounds and assumptions.

Do not claim a shortest trace or a state chart unless the tool provides one.

## Prove it before you hand off

A verify skill that was never run is a draft.

1. Make a scratch change that breaks the property in the real code.
2. Follow the generated skill once, as the next agent would. The skill must
   catch the break.
3. Drop the scratch change. Confirm that the check is back where it started:
   passing, or failing only on the findings that you will report.

If the skill misses the break, or a step does not run, fix the skill or the
verification. Do not fix the scratch change.

If the verifier, the permissions, or the environment prevent the run, report
the blocker and the unverified steps. Do not claim a proof.

## Hand off

Tell the user:

- what you verified;
- which tool you used and why;
- the bounds;
- what the check found, in plain words;
- how to run the check;
- what the check does not cover.

Suggest a second target only if you found a close one.

Point the user at the `maintain-formal-verification-skill` skill, through host
discovery or its source path. That skill brings the verification back in line
after changes that did not recheck it.
