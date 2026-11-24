---
name: principle-explain-the-number
description: "Apply before you measure, and before you trust, report, or act on a number you measured: a speedup, a regression, a throughput, a latency, or an eval result. Find what limits it, and rule out that it measured something other than the work you think."
---

# Explain the Number

Apply this skill only when the user requests it or another active skill routes
to it.

## Procedure

1. **Write the decision before you run.** Name the result that would change the
   decision. Name the noise floor. Stop when the run-to-run spread is larger
   than the effect.
2. **Ask "why not double?"** Name the resource or code path that bounds the
   result. Take the evidence from a profile or from counters recorded during a
   run. A guess from reading the code is not a limiter.
3. **List what else the number could measure.** Examples are errors, skipped
   or cached work, code that never ran, an untuned side, noise, and a piece too
   small to matter. Rule out each one with evidence.
4. **Keep the run count, the spread, and the limiter with the number.**

## Specific kinds of number

- For a performance number, run the
  [benchmark-checklist](../benchmark-checklist/SKILL.md) skill.
- For an eval result, check three things: whether every run did the task,
  whether the gap holds across trials and models, and whether the scenario
  matters.
