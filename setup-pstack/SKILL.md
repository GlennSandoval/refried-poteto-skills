---
name: setup-pstack
description: "Configure optional per-role model choices for pstack using the active host's supported capabilities. Use for 'configure pstack models', 'pstack budget', or changing pstack's model choices."
---

# Setup pstack

This skill configures the optional file `~/.config/pstack/models.md`.
Workflows read the file explicitly when they need it. No host is assumed to
load it automatically. If the file or a role is absent, that role uses the
host's default model. Configuration is not required to use pstack.

## Configuration format

The file is plain text. Each non-comment line has the form
`role: entry[, entry...]`.

### Parsing rules

Readers parse the file as follows:

1. Ignore blank lines and lines whose first non-whitespace character is `#`.
2. Split each remaining line at the first colon.
3. Split the value on commas and trim whitespace.

Role names are exact and case-sensitive. The entry `inherit` is reserved. It
leaves model selection unset, so the host uses its inherited or default model.
Every other entry is an exact model identifier.

The format cannot represent identifiers that contain commas or newlines. For
those models, use `inherit`. Do not invent an identifier.

### Invalid lines

A role is invalid in these cases:

- It has an empty value.
- It has an empty entry.
- It has a duplicate line.
- It is single-valued and has multiple entries.

When a role is invalid, its reader uses the role default and reports the
problem. Unknown roles do not affect readers.

### Roles and defaults

| Role | Value | Default |
| --- | --- | --- |
| `feature, refactoring` | One entry | `inherit` |
| `bug-fix` | One entry | `inherit` |
| `perf-issue` | One entry | `inherit` |
| `hillclimb` | One entry | `inherit` |
| `judgment and prose` | One entry | `inherit` |
| `swarm workers` | One entry | `inherit` |
| `arena runners` | List | `inherit, inherit, inherit` |
| `arena cross-judge pool` | Ordered list | `inherit` |
| `interrogate reviewers` | List | `inherit, inherit, inherit` |

### List roles

The runner and reviewer lists specify one seat for each entry, unless the user
requests a count. Readers take the entries in order and fill extra seats with
`inherit`.

The cross-judge list is an ordered preference for one judge. It is not a seat
count.

Repeated `inherit` entries are valid. They preserve seat counts even when the
host cannot select models. A seat is not evidence of an independent agent or a
distinct model.

### Example

This file configures three inherited arena seats. It leaves every other role at
its default:

```text
# Optional pstack model choices
arena runners: inherit, inherit, inherit
```

## Set up

Follow these steps in order.

1. Determine whether the active host permits model selection for the relevant
   agents. Determine whether the host can confirm available model identifiers.
   Use the host's documented discovery mechanism if one is available.
   - A model that is shown elsewhere is not proof that this host can select it.
     A model that the user supplies is also not proof.
   - If you cannot confirm selection or availability, use `inherit` and explain
     the limit.
   - Do not invent, transform or substitute identifiers.
2. Read the existing file if it is present.
   - If you cannot read it, report the problem. Do not overwrite the file.
   - Show the current role choices and any malformed or duplicate role lines.
   - Preserve existing choices and unrelated lines, unless the user asks you to
     change them.
   - Do not silently migrate a host-specific rule. Do not discard choices from
     another host.
   - Each workflow rechecks existing model identifiers when it uses them.
3. Agree the requested roles with the user. For lists, agree the order and the
   number of seats.
   - Offer only identifiers that you confirmed as selectable on this host, and
     `inherit`.
   - If model selection is not available, repeated `inherit` entries still
     record a panel size.
   - If no settings are needed, leave the file absent. The defaults already
     work.
4. Validate the changed entries against the format and the confirmed
   capabilities of the active host.
   - You can preserve a previously saved identifier that is not confirmed here.
     Do not present it as available or newly selected.
   - Resolve malformed lines for the roles that you change.
   - Report any other lines that remain invalid.
5. Show the resulting choices to the user. Obtain any required permission. Then
   create the directory and update the file. Do not overwrite unrelated user
   content.
6. Tell the user what changed, where you wrote it, and any capability gaps. Do
   not claim that a model or vendor was used unless you confirmed it.

### How readers use the file

This behaviour explains why step 1 confirms capabilities. A reader uses an
exact model identifier only if both of these conditions are true:

- Its current host supports model selection.
- The host confirms that the identifier is available.

Otherwise, the reader uses `inherit` and reports the fallback. If the host
rejects the selection at runtime, the reader also falls back and reports it.

## Reasoning budget

Model identifiers and reasoning settings are separate host capabilities. This
file does not configure reasoning budgets.

If the user requests a budget and the host exposes supported reasoning
controls:

1. Offer the host's actual supported choices.
2. Apply the chosen setting through that interface, when permissions allow.

Do not derive reasoning levels by editing model identifiers. If the host cannot
set a budget, report that limitation and keep the host default.

## Optional verification skills

If the project has no way to exercise the real app, or no formal verification
workflow, offer the relevant project-local skill once.

1. Discover the available skills with the host's mechanism.
2. Invoke a suitable skill only if all of these conditions are true: the skill
   exists, the user agrees, and permissions allow it.
3. Otherwise, explain the limitation, or offer to help create the workflow.
   Do not assume that a plugin or command exists.
