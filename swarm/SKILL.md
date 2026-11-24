---
name: swarm
description: "Coordinate workers and return one report. Use for 'swarm this', parallel coverage, races, gauntlets, and exploration."
---

# Swarm

Apply this skill only when the user requests it or another active skill routes
to it.

This skill coordinates workers and returns one report. It has four phases:

1. Frame
2. Fan out
3. Aggregate
4. Report

## Start

Track the phases with the task tracking of the host if available. Otherwise,
use a checklist.

## Phase A: Frame

1. State the done predicate and the artefact or report that the swarm must
   return.
2. Choose the shape: partition into slices, race N workers on identical briefs,
   or mix both. For a race or mixed shape, declare `first pass`, `rank all`, or
   `best-of` before you spawn.
3. Choose the worker model. See [Read the model configuration](#read-the-model-configuration).
4. Give each worker its own writable output when it writes.
5. When workers verify or measure commits, name the exact SHAs in each brief.
   A measurement brief also names the method: the sample count, what one
   sample is, and the order. The worker records both in its result.

### Read the model configuration

Read `~/.config/pstack/models.md` explicitly if it exists. The file is
optional. The host does not inject it automatically.

1. Parse each line as `role: entry[, entry...]`. Split at the first colon.
   Split entries on commas. Trim whitespace.
2. Ignore blank lines, lines whose first non-whitespace character is `#`, and
   unrelated roles.
3. Treat the `swarm workers` role as invalid if it has an empty value, an empty
   entry, a duplicate line, or multiple entries (the role is single-valued).
   Use its default and report the problem.
4. If the file exists but you cannot read it, use the default and report that
   you could not consult the configuration.
5. The default is `inherit`. It leaves model selection unset, so that the host
   uses its inherited or default model.
6. Use a configured identifier only when the host supports per-agent model
   selection and confirms that the identifier is available. Otherwise,
   inherit and report the fallback. Do not guess model identifiers.
7. Each worker uses the selected role model, unless a race assigns another
   confirmed, selectable model to its arm.
8. For a model race, name each confirmed model up front. If you cannot select
   distinct models, run distinct approaches instead. Report that the model
   comparison could not be performed.

## Phase B: Fan out

### Launch the workers

1. Use the subagent mechanism that the host provides to launch workers
   concurrently when possible. Respect its permissions, its capacity, and its
   access to the required files.
2. Select any non-default base explicitly, using capabilities that the host
   actually supports.
3. Do not assume that remote execution can access local files or uncommitted
   changes.
4. If isolation is unavailable, use separate output locations, or run writing
   slices serially. Do not overwrite user changes.
5. If unattended execution is unavailable, run synchronously and report that
   limitation. Do not promise background work.

If subagents are not available, execute the briefs sequentially. Record each
result separately. These passes share context and are not independent. Report
that limit. Do not claim independent coverage or a model race.

### Write the briefs

Make every brief stand alone. Include the goal, the scope, the exact slice or
race arm, how to verify, and what to report.

Workers report `PASS`, `ISSUES`, or `BLOCKED`, with evidence. A worker that can
prove a defect reports `ISSUES` and lists every issue that it can prove, not
only the first.

### Handle failures

- If a worker drops out, proceed with the remaining results and note the
  dropout.
- If the host rejects a model selection, use the host default and report the
  fallback.

## Phase C: Aggregate

1. Read the terminal results.
2. Drop a result that does not record the SHAs and the method that its brief
   names. Retry that brief once, using an available worker or a sequential
   pass.
3. After a second miss, record a gap. A gap does not count as a pass.
4. For coverage, make sure that every required slice has a result.
5. For a race, apply the selection rule that you declared up front: first pass,
   rank all, or best-of.
6. Do not paste raw worker dumps.

## Phase D: Report

Return one consolidated in-chat report. Include these items:

- a result table
- issue one-liners
- gaps or dropouts
- model fallbacks
- independence limitations
- the race rule, when used
