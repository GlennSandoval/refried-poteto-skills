---
name: swarm
description: "Coordinate workers and return one report. Use for 'swarm this', parallel coverage, races, gauntlets, and exploration."
---

# Swarm

Apply this skill only when the user requests it or another active skill routes
to it.

## Start

Track the phases with the host's task tracking if available, or a checklist
otherwise.

1. Frame
2. Fan out
3. Aggregate
4. Report

## Phase A: Frame

1. State the done predicate and the artifact or report the swarm must return.
2. Choose the shape. Partition into slices, race N workers on identical briefs, or mix both. For a race or mixed shape, declare `first pass`, `rank all`, or `best-of` before spawning.
3. Explicitly read `~/.config/pstack/models.md` if it exists; it is optional
   and is not automatically injected. Lines are `role: entry[, entry...]`:
   split at the first colon and split entries on commas, trimming whitespace.
   Ignore blank lines, lines whose first non-whitespace character is `#`, and
   unrelated roles. An empty value, empty entry, duplicate role line, or multiple
   entries for the single-valued `swarm workers` role is invalid: use its
   default and report the problem. If the file exists but cannot be read, use
   the default and report that configuration could not be consulted. The default
   is `inherit`: leave model selection unset so the host uses its inherited or
   default model. Use a configured identifier only when the host supports per-agent
   model selection and confirms it is available; otherwise inherit and report
   the fallback.
   Do not guess model identifiers. For a model race, name each confirmed model
   up front. If distinct models cannot be selected, run distinct approaches
   instead and report that the model comparison could not be performed.
   Each worker uses the selected role model unless a race assigns another
   confirmed, selectable model to its arm.
4. Give each worker its own writable output when it writes. When workers verify
   or measure commits, each brief names the exact SHAs. A measurement brief also
   names the method (sample count, what one sample is, order). The worker
   records both in its result.

## Phase B: Fan out

Use the host's available subagent mechanism to launch workers concurrently when
possible, subject to its permissions, capacity, and access to the required
files. Select any non-default base explicitly using capabilities the host
actually supports. Do not assume remote execution can access local files or
uncommitted changes. If isolation is unavailable, use separate output locations
or run writing slices serially without overwriting user changes. If unattended
execution is unavailable, run synchronously and report that limitation rather
than promising background work.

Without subagents, execute the briefs sequentially, recording each result
separately. These passes share context and are not independent; report that
limit and do not claim independent coverage or a model race.

Every brief stands alone. Include the goal, scope, exact slice or race arm, how to verify, and what to report. Reports use `PASS`, `ISSUES`, or `BLOCKED` with evidence. A worker that can prove a defect reports `ISSUES` and lists every issue it can prove, not only the first.

If a worker drops out, proceed with the remaining results and note it. If a
model selection is rejected, use the host default and report the fallback.

## Phase C: Aggregate

Read the terminal results. Drop a result that does not record the SHAs and
method its brief names, and retry that brief once using an available worker or
a sequential pass. After a second miss, record a gap. A gap does not count as a
pass. For coverage, every required slice needs a result. For a race, apply the
selection rule declared up front: first pass, rank all, or best-of. Do not
paste raw worker dumps.

## Phase D: Report

Return one consolidated in-chat report with a result table, issue one-liners,
gaps or dropouts, model fallbacks, independence limitations, and the race rule
when used.
