---
name: interrogate
description: "Adversarially review a change or design and report findings proven by a run. Use for 'interrogate', 'adversarial review', 'multi-model review', 'challenge this', 'stress test this code', 'find blind spots', or 'tear this apart'."
---

# Interrogate

Apply this skill only when the user requests it or another active skill routes
to it.

Adversaries try to break a change or design. A finding survives only when a
run proves it. Report findings; do not apply fixes. If execution or verification
is unavailable or not permitted, report the coverage gap rather than presenting
unrun concerns as proven findings or claiming a clean review.

## Frame

The scope is what the user names. Otherwise use the branch diff from its merge
base with the base branch, through the working tree, including relevant staged,
unstaged, and untracked files. Restate the intent from the user's message,
commits, and PR description when available. Ask the user when intent or the
base branch cannot be established from the available context.

## Fan out

Explicitly read `~/.config/pstack/models.md` if it exists. It is optional and is
not automatically injected. Lines are `role: entry[, entry...]`: split at the
first colon and split entries on commas, trimming whitespace. Ignore blank
lines, lines whose first non-whitespace character is `#`, and unrelated roles.
An empty value, empty entry, or duplicate line for a role makes that role
invalid: use its default and report the problem. If the file exists but cannot
be read, use the default and report that configuration could not be consulted.
Use the `interrogate reviewers` list, defaulting to three `inherit` entries.
The list sets the reviewer count unless the user specifies a count; then take
entries in order and fill remaining seats with `inherit`. Each `inherit` leaves
model selection unset so the host uses its inherited or default model. Use
another entry only when the host supports per-agent model selection and
confirms that exact identifier is available; otherwise use the host default and
report the fallback. If selection is rejected, inherit and report it. Do not
infer model diversity.

When subagents are available, launch the reviewers concurrently if possible.
If unattended execution is unavailable, run synchronously and report that
limitation rather than promising background work. Give each the same scope and
intent and a separate writable location containing the same relevant state,
including uncommitted changes. Use isolated worktrees or copies where permitted;
never overwrite user changes. If isolation is not
available, use separate repro locations and do not modify the source. When
there are no subagents, run distinct adversarial passes sequentially against
the same state and record each separately. These passes share context and are
not independent; report that limit.

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

Rerun each finding's command, subject to permissions, against the same relevant
state. Keep it when the output shows the failure and the failure breaks the
intent. Drop the rest, recording why; distinguish a failed reproduction from
one that could not be attempted. Merge findings that share a root cause. A
sequential rerun is corroboration, not an independent review. Report any
unavailable execution or verification as a gap.

Keep every verified finding, not just one reviewer's list.

## Output

- **Intent**: the restatement.
- **Findings**: for each verified finding, the command, output, how it breaks
  the intent, and the reviewers that found it. Say "no verified findings" when
  none survive; if review or verification was incomplete, say so explicitly.
- **Dropped**: for each reviewer, the count of dropped findings and why.
- **Gaps**: unavailable execution, verification, model selection, dropouts, or
  lack of independent reviewers, as applicable.
