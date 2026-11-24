---
name: arena
description: "Compare independent candidates for a non-trivial artifact, select a base, and graft in the strongest alternatives. Use for 'arena this', 'throw it in the arena', or when one attempt could lock in the wrong shape."
---

# Arena

Apply this skill only when the user requests it or another active skill routes
to it.

Track the phases (Frame, Fan out, Cross-judge, Pick, Graft, Verify) using the
host's task tracking if available, or a short checklist otherwise.

## Phase A: Frame

Every candidate gets the same prompt, so the prompt is the contract.

1. State the artifact each candidate is producing.
2. Derive a rubric of 3–6 concrete, gradeable criteria. Candidates see the
   task, while the picker and cross-judge use the rubric.
3. Explicitly read `~/.config/pstack/models.md` if it exists. It is optional
   and is not automatically injected. Its lines have the form
   `role: entry[, entry...]`: split at the first colon and split entries on
   commas, trimming whitespace. Ignore blank lines, lines whose first
   non-whitespace character is `#`, and unrelated roles. An empty value, empty
   entry, or duplicate line for a role makes it invalid: use its default and
   report the problem. If the file exists but cannot be read, use the defaults
   and report that configuration could not be consulted.
4. Use the `arena runners` list for candidate seats; default to three `inherit`
   entries. Each `inherit` leaves model selection unset so the host uses its
   inherited or default model. Other entries are
   model identifiers: use one only when the host supports per-agent model
   selection and confirms that exact identifier is available. If unavailable
   or rejected, use the host default for that seat and report the fallback.
   Never guess a model or claim model diversity without evidence. The list sets
   the seat count unless the user specifies a count; then take entries in order
   and fill any remaining seats with `inherit`. If only one seat is requested,
   report that no candidate comparison is possible.
5. Give each candidate a separate writable output location and the same base
   state. Use isolated worktrees when available and permitted; otherwise use
   separate directories or clearly labelled proposals without shared writes.
   Preserve existing user changes. Include the relevant working-tree state in
   each candidate's grounding when the task depends on it.

## Phase B: Fan out

When the host supports subagents, launch the candidates concurrently if
possible, subject to its permissions and limits. Give each a self-contained
brief with the task, shared grounding, output location, and a request for a
short rationale naming alternatives considered and rejected. Do not have
workers write to the same files. If unattended execution is unavailable, run
synchronously and report that limitation rather than promising background work.

Without subagents, make the candidate passes sequentially from the same base,
recording each separately before starting the next. Vary the approach, not the
task. These passes share context and are not independent; report that limit.
If a candidate produces no output, proceed with the remaining candidates and
note the dropout. If fewer than two remain, complete the artifact if possible
but report that the comparison could not be made.

## Phase C: Cross-judge

Use the `arena cross-judge pool` list from the same optional configuration,
with a default of one `inherit` entry and the same parsing and model fallback
rules as for runners. The pool is an ordered preference for one judge, not a
seat count. If the host can confirm both model selection and vendor identity,
prefer an available entry from a different vendor to the parent. If there is no
such entry or the information is unavailable, use the first entry without
claiming vendor diversity. Do not infer a vendor from an identifier. If
selection fails, use the host default and report it.

When an independent read-only subagent is available, give it the rubric and
all candidate outputs and ask it to score each criterion and recommend a base.
Otherwise perform a separate sequential critique and explicitly report that it
is not an independent cross-judge. If no critique can be performed, report the
gap. Respect the host's permissions and do not claim independent verification
from a sequential pass.

## Phase D: Pick a base

Read every candidate end to end before picking. Score each against the rubric
criterion by criterion, not on holistic feel, and compare with the critique
when one ran. Read the rationales behind any disagreement before deciding.

Pick the base a future maintainer can extend most easily without breaking
invariants. When tied, prefer the cleaner boundary or smaller API.

## Phase E: Graft

Walk each losing candidate once more for what is worth porting into the base,
usually one or two things per candidate, not most of it. Fold each graft in by
hand so the result stays coherent under one mental model. Do not paste
mechanically.

If the candidates converge on one shape, note it and ship the consensus shape.
Convergence is stronger evidence when the candidates were independent. No graft
is needed. If they wildly diverge, Phase A may have been under-specified:
reframe and rerun rather than averaging the divergence.

## Phase F: Verify

Verify the synthesised artifact using the host's available tools and the
task's relevant checks, subject to permission. If verification finds a problem
the arena missed, either Phase A was wrong (reframe and rerun) or a candidate
caught it and you missed the graft (return to Phase E). Do not paper over it.
Report checks that could not be run and do not claim they passed.

## Outputs

One synthesised artifact and a short synthesis note naming the base and why,
the cross-judge's verdict or the independence gap, each graft and its source,
what was rejected and why, convergence or dropouts, model fallbacks, and the
verification result or gap.
