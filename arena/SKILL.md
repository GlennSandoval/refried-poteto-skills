---
name: arena
description: "Compare independent candidates for a non-trivial artifact, select a base, and graft in the strongest alternatives. Use for 'arena this', 'throw it in the arena', or when one attempt could lock in the wrong shape."
---

# Arena

Apply this skill only when the user requests it or another active skill routes
to it.

Arena produces several independent candidates for one artifact, picks the best
as a base, and grafts in the strongest parts of the others. Use it when one
attempt could lock in the wrong shape.

Track the phases (Frame, Fan out, Cross-judge, Pick, Graft, Verify) with the
host's task tracking if it is available. Otherwise, use a short checklist.

## Phase A: Frame

Every candidate gets the same prompt, so the prompt is the contract.

1. State the artifact that each candidate produces.
2. Derive a rubric of 3–6 concrete, gradeable criteria. Candidates see the
   task. The picker and the cross-judge use the rubric.
3. Read the model configuration. See [Read the configuration](#read-the-configuration).
4. Choose the candidate seats. See [Choose candidate seats](#choose-candidate-seats).
5. Give each candidate a separate writable output location and the same base
   state.
   - Use isolated worktrees when they are available and permitted.
   - Otherwise, use separate directories or clearly labelled proposals without
     shared writes.
   - Preserve existing user changes.
   - If the task depends on the working-tree state, include that state in each
     candidate's grounding.

### Read the configuration

Explicitly read `~/.config/pstack/models.md` if it exists. The file is
optional, and the host does not inject it automatically.

- Its lines have the form `role: entry[, entry...]`.
- Split each line at the first colon. Split the entries on commas and trim
  whitespace.
- Ignore blank lines, lines whose first non-whitespace character is `#`, and
  unrelated roles.
- An empty value, an empty entry or a duplicate line makes a role invalid. Use
  the default for that role and report the problem.
- If the file exists but you cannot read it, use the defaults and report that
  you could not consult the configuration.

### Choose candidate seats

Use the `arena runners` list for the candidate seats. The default is three
`inherit` entries.

- Each `inherit` entry leaves model selection unset, so the host uses its
  inherited or default model.
- Every other entry is a model identifier. Use it only when the host supports
  per-agent model selection and confirms that the exact identifier is
  available. If the identifier is unavailable or the host rejects it, use the
  host default for that seat and report the fallback.
- Never guess a model. Never claim model diversity without evidence.
- The list sets the seat count, unless the user specifies a count. If the user
  specifies a count, take the entries in order and fill any remaining seats with
  `inherit`.
- If the user requests only one seat, report that no candidate comparison is
  possible.

## Phase B: Fan out

### With subagents

When the host supports subagents, launch the candidates concurrently if
possible. Follow the host's permissions and limits.

1. Give each candidate a self-contained brief. The brief contains the task, the
   shared grounding and the output location.
2. Ask each candidate for a short rationale that names the alternatives it
   considered and rejected.
3. Do not let workers write to the same files.

If unattended execution is not available, run the candidates synchronously.
Report that limitation. Do not promise background work.

### Without subagents

1. Make the candidate passes sequentially from the same base.
2. Record each pass separately before you start the next.
3. Vary the approach, not the task.
4. Report that the passes share context and are not independent.

### Dropouts

If a candidate produces no output, proceed with the remaining candidates and
note the dropout. If fewer than two candidates remain, complete the artifact if
possible. Report that the comparison could not be made.

## Phase C: Cross-judge

Use the `arena cross-judge pool` list from the same optional configuration. The
default is one `inherit` entry. The parsing and model fallback rules are the
same as for runners.

The pool is an ordered preference for one judge. It is not a seat count.

- If the host can confirm both model selection and vendor identity, prefer an
  available entry from a different vendor than the parent.
- If there is no such entry, or the information is not available, use the first
  entry. Do not claim vendor diversity.
- Do not infer a vendor from an identifier.
- If selection fails, use the host default and report it.

Run the cross-judge:

- When an independent read-only subagent is available, give it the rubric and
  all candidate outputs. Ask it to score each criterion and recommend a base.
- Otherwise, perform a separate sequential critique. Report explicitly that it
  is not an independent cross-judge.
- If you cannot perform any critique, report the gap.

Respect the host's permissions. Do not claim independent verification from a
sequential pass.

## Phase D: Pick a base

1. Read every candidate end to end before you pick.
2. Score each candidate against the rubric, criterion by criterion. Do not rely
   on a holistic feel.
3. Compare your scores with the critique, when one ran.
4. Read the rationales behind any disagreement before you decide.

Pick the base that a future maintainer can extend most easily without breaking
invariants. When candidates tie, prefer the cleaner boundary or the smaller API.

## Phase E: Graft

Walk each losing candidate once more for what is worth porting into the base.
Expect one or two things from each candidate, not most of it.

Fold each graft in by hand, so the result stays coherent under one mental
model. Do not paste mechanically.

Two outcomes need different handling:

- **The candidates converge on one shape.** Note the convergence and ship the
  consensus shape. No graft is needed. Convergence is stronger evidence when
  the candidates were independent.
- **The candidates diverge wildly.** Phase A may have been under-specified.
  Reframe and rerun. Do not average the divergence.

## Phase F: Verify

Verify the synthesised artifact. Use the host's available tools and the
relevant checks for the task, subject to permission.

If verification finds a problem that the arena missed, one of two things went
wrong. Do not paper over the problem.

- Phase A was wrong. Reframe and rerun.
- A candidate caught the problem and you missed the graft. Return to Phase E.

Report the checks that you could not run. Do not claim that they passed.

## Outputs

Produce one synthesised artifact and a short synthesis note. The note names:

- The base and why you chose it.
- The cross-judge's verdict, or the independence gap.
- Each graft and its source.
- What you rejected and why.
- Convergence or dropouts.
- Model fallbacks.
- The verification result or gap.
