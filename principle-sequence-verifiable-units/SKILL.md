---
name: principle-sequence-verifiable-units
description: "Apply to multi-step work (sweeps, migrations, runs of similar edits) and to how you stack commits and PRs. Break work into small units that each end in a verifiable state, check each before the next, and order delivery so the sequence proves itself to a reviewer."
---

# Sequence work into verifiable units

Apply this skill only when the user requests it or another active skill routes
to it.

## Concept

Order work as small units. Each unit ends in a state that you can check. Do not
advance until the current unit is green.

## Procedure for sweeps and migrations

Use this procedure for a sweep, a migration, or a run of similar edits. Treat
each unit as a bracket:

1. Start from a known-good state.
2. Make one change.
3. Run the check.
4. Proceed only when the check passes.

Run the per-unit check even when a tool does the edits.

## Order of delivery

Deliver in the order that proves the work:

- Deliver the failing test first, then the fix.
- Deliver the subtraction before the reshape.
- Deliver the baseline before the treatment.

Each commit lands on its own.
