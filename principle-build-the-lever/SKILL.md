---
name: principle-build-the-lever
description: "Apply to any non-trivial work, not just bulk work: edits, migrations, analyses, checks. Build the tool that does it or proves it (codemod, script, generator, or a skill your subagents follow) instead of working by hand. The tool is the artifact a reviewer can rerun."
---

# Build the Lever

Apply this skill only when the user requests it or another active skill routes
to it.

## Principle

When the work is not trivial, build the tool that does it instead of doing it
by hand. The tool can be a codemod, a script, a generator, or a rerunnable
check. The bar is triviality, not repetition. Skip the tool only for a couple
of obvious edits.

A deterministic tool is better than fan-out. If you do fan out, the delegates
need a fixed recipe, so use the skill described in the procedure.

## Procedure

1. Do the first unit by hand.
2. Build the tool. Make it safe to rerun.
3. Prove the tool: rerun it on the first unit.
4. If you fan out, write the recipe, the verification contract, and the fences
   as one skill. The delegates read the skill and cannot edit it.
5. Build the smallest script that does or proves the job. Do not build a
   framework.
6. If the work outlives the session, commit the tool.

## Check

This principle produces a file. If the diff has no script, codemod, generator,
or delegate skill, you did not apply it.
