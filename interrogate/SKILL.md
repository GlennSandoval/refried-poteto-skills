---
name: interrogate
description: "Adversarially review a change or design and report findings proven by a run. Use for 'interrogate', 'adversarial review', 'multi-model review', 'challenge this', 'stress test this code', 'find blind spots', or 'tear this apart'."
---

# Interrogate

Apply this skill only when the user requests it or another active skill routes
to it.

Adversaries try to break a change or design. A finding survives only when a run
proves it. Report findings. Do not apply fixes.

If execution or verification is unavailable or not permitted, report the
coverage gap. Do not present unrun concerns as proven findings. Do not claim a
clean review.

## Frame

1. Set the scope.
   - Use what the user names.
   - Otherwise, use the branch diff from its merge base with the base branch,
     through the working tree. Include relevant staged, unstaged, and untracked
     files.
2. Restate the intent from the user's message, the commits, and the PR
   description when available.
3. Ask the user if you cannot establish the intent or the base branch from the
   available context.

## Fan out

### Read the model configuration

Read `~/.config/pstack/models.md` explicitly if it exists. The file is
optional. The host does not inject it automatically.

1. Parse each line as `role: entry[, entry...]`. Split at the first colon.
   Split entries on commas. Trim whitespace.
2. Ignore blank lines, lines whose first non-whitespace character is `#`, and
   unrelated roles.
3. If a role has an empty value, an empty entry, or a duplicate line, treat the
   role as invalid. Use its default and report the problem.
4. If the file exists but you cannot read it, use the default and report that
   you could not consult the configuration.

### Choose the reviewers

1. Use the `interrogate reviewers` list. The default is three `inherit`
   entries.
2. Let the list set the reviewer count, unless the user specifies a count. If
   the user specifies a count, take entries in order and fill the remaining
   seats with `inherit`.
3. Treat each `inherit` entry as "leave model selection unset", so that the host
   uses its inherited or default model.
4. Use another entry only when the host supports per-agent model selection and
   confirms that the exact identifier is available. Otherwise, use the host
   default and report the fallback.
5. If the host rejects a selection, inherit and report it.
6. Do not infer model diversity.

### Launch the reviewers

When subagents are available:

1. Launch the reviewers concurrently if possible. If unattended execution is
   unavailable, run synchronously and report that limitation. Do not promise
   background work.
2. Give each reviewer the same scope and intent.
3. Give each reviewer a separate writable location that contains the same
   relevant state, including uncommitted changes. Use isolated worktrees or
   copies where permitted. Never overwrite user changes.
4. If isolation is not available, use separate repro locations and do not
   modify the source.

When there are no subagents, run distinct adversarial passes sequentially
against the same state. Record each pass separately. These passes share context
and are not independent. Report that limit.

### Reviewer brief

Give each reviewer this brief:

> Break this change. Prove each finding with a run against the real code, such
> as a failing test, a repro script, or command output showing the wrong
> behaviour. For a design or plan, run a prototype or probe the current tree.
> Keep repros in your own location. Report each finding with a title, the exact
> command, its output, and the output the intent requires. Leave out anything
> you did not run, including style, naming, structure, and risks that need a
> future change to matter. No findings is a valid result only when the review
> could be performed.

## Verify

1. Rerun the command of each finding against the same relevant state, subject
   to permissions.
2. Keep the finding when the output shows the failure and the failure breaks the
   intent.
3. Drop the other findings and record why. Distinguish a failed reproduction
   from one that you could not attempt.
4. Merge findings that share a root cause.
5. Keep every verified finding, not only the list of one reviewer.
6. Report any unavailable execution or verification as a gap.

A sequential rerun is corroboration, not an independent review.

## Output

- **Intent**: the restatement.
- **Findings**: for each verified finding, the command, the output, how it
  breaks the intent, and the reviewers that found it. Say "no verified
  findings" when none survive. If review or verification was incomplete, say so
  explicitly.
- **Dropped**: for each reviewer, the count of dropped findings and why.
- **Gaps**: unavailable execution, verification, model selection, dropouts, or
  lack of independent reviewers, as applicable.
