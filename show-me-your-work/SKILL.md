---
name: show-me-your-work
description: "Keep a reviewable decision trail for long-running or unattended work: a TSV log with one row per decision (what, why, evidence, result). Local by default; commit it when a reviewer needs the trail to trust the result."
---

# Show me your work

Apply this skill only when the user requests it or another active skill routes
to it.

Keep one canonical log. The log is a single TSV file with one row for each
decision. A reviewer reads the log to see what the agent decided, why, and what
proves it.

## The format

Cells stay single-line. Evidence is a pointer, not prose.

To start a clean log, copy [the template](references/decision-log-template.tsv)
(the header row). Resolve the path relative to this installed skill, not the
project working directory.

### Columns

- **ts.** ISO8601 timestamp.
- **phase.** The phase or workstream.
- **decision.** What was chosen or done, in one line.
- **why.** The reason in plain words. If a principle drove the decision, say so
  plainly. Do not use a jargon tag.
- **evidence.** A link or path that proves the decision: a commit SHA, a PR
  number, `file:line`, or an artifact, trace or screenshot path. Never a
  paragraph.
- **result.** The outcome or predicate state: `tests green`, `reverted`,
  `pixel-diff 0`, `INCONCLUSIVE`, `open`.

### Example

This example is plain-spoken, so a reviewer can read it at a glance.

```
ts	phase	decision	why	evidence	result
2026-05-24T09:02:00Z	frame	counted the work first, about 100 components and roughly 75 hours	wanted to know the size before starting a long run	commit 3a9f1c2	found 5 things to sort out before starting
2026-05-24T09:40:00Z	harness	took screenshots of the old version before changing anything	so we can compare old against new and catch any visual change	scripts/snapshot.sh, baseline/	saved 120 reference screenshots
2026-05-24T11:15:00Z	widget	moved the widget styles over without changing how it looks	keep the change small and the result identical	commit 7c21e0a, pixel-diff 0	looks identical, tests pass
2026-05-24T12:30:00Z	widget	threw out a helper's work because its screenshots were blank	checked the real files instead of trusting its summary	worktree reset	reverted, tightened the instructions for next time
```

## Log a row

Write each entry the way you would tell a teammate what you did. Use plain
words and concrete actions. Do not use AI speak or abstract jargon. The
**unslop** skill applies to log text too.

### What to log

Log decision points and checkpoints. Do not log every action. Log these events:

- A fork that you chose.
- A unit that you completed, with its verification result.
- A pivot or revert, with its trigger.
- A blocker that you surfaced.
- A gate that you fixed.

For loop runs, write one row for each iteration. Skip the trivial and
self-evident.

### How to write the row

Use the helper at `scripts/log.sh`, relative to this installed skill.

1. Set `SKILL_DIR` to the installed skill directory.
2. Run the helper from the project directory. Pass
   `<logfile> <phase> <decision> <why> <evidence> <result>`.

```sh
bash "$SKILL_DIR/scripts/log.sh" decisions.tsv "build" "chose option A" \
  "it meets the constraint" "design.md" "open"
```

The helper does these things:

- It stamps `ts`.
- It writes the header on first use.
- It strips stray tabs and newlines.
- It prefixes any cell that starts with `=`, `+`, `-` or `@` with a single
  quote.

A bare `printf` that appends a row also works. If the cells come from generated
or user-supplied text, handle those same bytes.

### Runs and `start` rows

A run is one agent conversation, including its later turns and any summary of
it. A pickup, a replacement agent or a new chat starts a new run. A log can
therefore contain rows from more than one run. The `start` row marks where each
run begins.

When a run adds to a log that already has rows:

1. Before you write, read the last rows of the log to see whether another run
   wrote since your last turn. This applies when a run comes back to a log in a
   later turn.
2. Write a first row with phase `start`. Do the same for the first row after
   another run's `start` row.
3. In the `start` row, name the `ts` range of the earlier rows that this run
   did not write.
4. In the `start` row, name this run in the evidence column, for example with
   its agent id.

Use phase `start` for nothing else.

## Where the log lives

By default, the log is a working artifact. Do not commit it.

- Keep it at `decisions.tsv` in the work directory.
- When several efforts run at once, keep it at `.audit/<task-slug>.tsv`.
- Leave it out of git.

Commit the log only when the work is ambitious enough that a reviewer needs the
trail to trust the result.

## Rules

- The log is append-only. A wrong call gets a new row that supersedes it. Never
  edit or delete history.
- Prefer evidence that committed scripts produce over hand-made one-offs. This
  follows the **encode-lessons-in-structure** principle skill.

## Audit the log against the transcript

At the end of the run, before you hand back, check that the log told the truth.

### Sources

- Use the active host's available transcript or conversation history for this
  run. Stay within the current workspace and the user's permissions.
- Never search unrelated private chats.
- If no complete transcript is available, audit against the accessible
  conversation and evidence. Report that the transcript audit was partial or
  unavailable.

### Procedure

Walk this run's rows against the accessible sources. Each stretch begins at one
of this run's `start` rows, or at the first row if this run created the log. It
ends at the next `start` row of another run.

1. Check that every row maps to a real decision or action.
2. Check that the evidence of each row resolves and shows what the row claims.
3. Look for a fork, pivot or abandoned approach that shaped the work but is not
   logged. This is a gap. Add a row for it.

### Corrections

Correct the log, not the story. The audit never edits or removes a row, even an
invented one.

If a row records neither a real decision nor a real action, or if its claim or
evidence is wrong, add a row that supersedes it. The new row states what
actually happened and gives a pointer that resolves.

The audit does not check rows outside this run's stretches. If this run's own
work shows that one of those rows is wrong, supersede it like any wrong call.

## Independent review of the trail

Before you hand back, ask an independent subagent to read the trail and the
available run transcript. The subagent flags what the user must pay attention
to. The review is a scan for risk. It is not a redo of the work.

- Use a different vendor's model if the host supports it.
- Read the optional `~/.config/pstack/models.md` explicitly for any relevant
  role choice. Use the choice only if the host supports it. Otherwise, use the
  host defaults.

If independent subagents are not available:

1. Review the trail in a separate sequential pass against the available
   evidence.
2. State that it was a self-review, not an independent review.
3. If the transcript is not available, also state which claims you could not
   check.

Never invent a reviewer or a model.

The reviewer flags these items:

- Decisions that have weak or absent evidence.
- Verification steps that were skipped, or claimed without proof in the
  transcript.
- Choices that look risky in hindsight: premature choices, scope creep, and
  choices that paper over a symptom.
- Gaps that the user would otherwise miss on a casual skim.

### The Attention section

Every reply for a run that produced a trail ends with an **Attention**
section. In that section:

- Identify whether the review was independent or a sequential self-review.
- Name the reviewer's model only if you know it.
- List each flag with the specific rows or moments.
- Say "No flags" only when you reviewed the available evidence.
- State any limits on the review or the transcript audit next to the result.

## Review the trail

Read the log from top to bottom, follow the evidence pointers, and spot-check.
GitHub renders a committed TSV as a table. In a terminal,
`column -s$'\t' -t decisions.tsv` renders it.

## Compose this skill with others

Other skills route their audit trail to this skill instead of inventing one.
Reference this skill by name and let it own the format. Do not restate the
columns.
