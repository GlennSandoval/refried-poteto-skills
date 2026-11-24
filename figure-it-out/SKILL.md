---
name: figure-it-out
description: "Design an auditable playbook when no narrower one fits: a large migration, an ambitious multi-part change, or work a human reviews after stepping away. Scales rigour to the task, runs a hypothesis loop, and logs decisions. Use for /figure-it-out or 'figure it out'."
---

# Figure it out

Apply this skill only when the user requests it or another active skill routes
to it.

When the task matches no playbook, design one. The deliverable before any code
is the workflow itself. The workflow is a sequence of phases that scales rigour
to the task, runs the scientific method, and leaves a decision trail that a
human can audit after stepping away.

## Start

Open a todolist. Make its first item "Read the Principles section of the
**poteto-mode** skill". Then add the phases below as todos.

## Phase A: Frame

Ground the task first, then commit. Do not start the run until you can state
all of these:

- The definition of done as a falsifiable predicate (the **prove-it-works**
  principle skill).
- The scope, quantified: rough units and effort, plus the blockers that
  grounding surfaced.
- The rigour level, biased high. One-way doors and high blast radius get more
  rigour. Reversible low-stakes steps get less. Rigour means gates and
  artefacts, not "try harder".

Present the framing and the tradeoffs before you commit to a long run.
Reversible work proceeds (the **never-block-on-the-human** principle skill), but
a multi-hour run earns one checkpoint.

## Phase B: Design the workflow

1. Decompose the work into atomic units that can land independently.
2. Sequence the units with the riskiest unknown first. Put scaffold and
   verification before features (the **foundational-thinking** principle
   skill).
3. Build the verification harness before the work. Capture the baseline from
   the pre-change state, so that the check reads as "old value vs new value".
4. For one-way-door design decisions, run the **architect** skill (it runs
   **arena**). Skip it for mechanical work whose shape is already concrete. A
   second arena over a settled design is over-engineering (the
   **laziness-protocol** principle skill).
5. Decide what fans out.
   - If delegation is available, parallelise only across seams. Give each
     worker its own worktree or branch (the
     **separate-before-serializing-shared-state** principle skill). Avoid
     unnecessary fan-out.
   - Otherwise, execute the units sequentially.
6. Write the designed phase list down. The human reviews that list.

Then execute the design:

1. Add its steps to the todolist as concrete items between the Phase C and
   Phase D entries.
2. Run each step under the loop discipline of Phase C.
3. Weave the log of Phase D through the steps. Add a row as each step lands.
   Do not save the whole trail for the end.

## Phase C: Run the loop

Each unit is an experiment. Apply the **sequence-verifiable-units** principle
skill: verify each unit before you start the next one, instead of batching
checks at the end.

1. State the hypothesis.
2. Make the smallest change.
3. Measure against the predicate on the real artefact.
4. Keep the change if it advanced. Revert it if it did not.

### Verification rules

- Verify by inspecting the artefact, never a self-report. When something passes
  too easily, suspect the observation method before the system.
- Pair delegated work with an independent judge when one is available.
  Otherwise, inspect the artefact directly and disclose that the review is not
  independent.
- If a worker games the gate, reset and harden the contract. If the gate itself
  is wrong, fix the gate. Do not route around it.
- Give each verdict as VERIFIED, NOT VERIFIED, or INCONCLUSIVE. Inconclusive is
  not a pass. Do not hide a negative.

## Phase D: Keep the audit trail

Log the run with the **show-me-your-work** skill. The work of figure-it-out is
usually ambitious enough to commit the trail, so that the reviewer can read it
in the PR. The trail plus the diff lets the human come back and trust the work.

## Phase E: Verify and hand back

1. Check the whole against the predicate of Phase A on the real product, not
   only the harness.
2. Encode any recurring correction as a gate, a lint rule, a check, or a script
   (the **encode-lessons-in-structure** principle skill).

## Reply

Reply with the playbook that you designed, the rigour level and why, the
decision-trail path, what is verified against the predicate, and what is still
open.
