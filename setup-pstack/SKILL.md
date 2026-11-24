---
name: setup-pstack
description: "Configure optional per-role model choices for pstack using the active host's supported capabilities. Use for 'configure pstack models', 'pstack budget', or changing pstack's model choices."
---

# Setup pstack

Configure the optional file `~/.config/pstack/models.md`. Workflows explicitly
read it when needed; no host is assumed to load it automatically. If the file
or a role is absent, that role uses the host's default model. Configuration is
not required to use pstack.

## Configuration format

The file is plain text. Each non-comment line is `role: entry[, entry...]`.
Split at the first colon, then split the value on commas and trim whitespace.
Ignore blank lines and lines whose first non-whitespace character is `#`.
Role names are exact and case-sensitive. `inherit` is a reserved entry meaning
leave model selection unset so the host uses its inherited or default model;
every other entry is an exact model identifier.
Identifiers containing commas or newlines cannot be represented in this format:
use `inherit` for those rather than inventing an identifier.

An empty value, empty entry, or duplicate line for a role invalidates that role;
its reader uses the role default and reports the problem. A single-valued role
with multiple entries is also invalid. Unknown roles do not affect readers.
The roles and defaults are:

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

The runner and reviewer lists specify one seat per entry unless the user
requests a count; readers take entries in order and fill extra seats with
`inherit`. The cross-judge list is an ordered preference for one judge, not a
seat count. Repeated `inherit` entries are valid and preserve seat counts even
when the host cannot select models. A seat is not evidence of an independent
agent or a distinct model.

For example, this file configures three inherited arena seats and leaves every
other role at its default:

```text
# Optional pstack model choices
arena runners: inherit, inherit, inherit
```

## Set up

1. Determine whether the active host permits selecting a model for the
   relevant agents and can confirm available model identifiers. Use its
   documented discovery mechanism if available. A model shown elsewhere or
   supplied by a user is not proof that this host can select it. If selection
   or availability cannot be confirmed, use `inherit` and explain the limit;
   do not invent, transform, or substitute identifiers.
2. Read the existing file if present. If it cannot be read, report the problem
   and do not overwrite it. Show the current role choices and any malformed or
   duplicate role lines. Preserve existing choices and unrelated lines unless
   the user asks to change them; do not silently migrate a host-specific rule
   or discard choices from another host. Existing model identifiers are
   rechecked by each workflow when used.
3. Agree the requested roles and, for lists, their order and number of seats.
   Offer only identifiers confirmed selectable by this host and `inherit`.
   If model selection is unavailable, repeated `inherit` entries still allow
   a panel size to be recorded. If no settings are needed, leave the file
   absent; the defaults already work.
4. Validate changed entries against the format and the active host's confirmed
   capabilities. A previously saved identifier that is not confirmed here may
   be preserved unchanged, but never presented as available or newly selected.
   Resolve malformed lines for roles being changed, and report any others that
   remain invalid. Show the resulting choices before writing; obtain any
   required permission, then create the directory and update the file. Do not
   overwrite unrelated user content.
5. Tell the user what changed, where it was written, and any capability gaps.
   A reader must use an exact model identifier only if its current host supports
   model selection and confirms that identifier is available; otherwise it uses
   `inherit` and reports the fallback. If selection is rejected at runtime, it
   likewise falls back and reports it. Do not claim a model or vendor was used
   unless confirmed.

## Reasoning budget

Model identifiers and reasoning settings are separate host capabilities. If
the user requests a budget and the host exposes supported reasoning controls,
offer the host's actual supported choices and apply them using that interface
when permitted. Do not derive reasoning levels by editing model identifiers.
This file does not configure reasoning budgets; if the host cannot set one,
report that limitation and retain the host default.

## Optional verification skills

If the project lacks a way to exercise the real app or a formal verification
workflow, offer the relevant project-local skill once. Discover available
skills using the host's mechanism and invoke a suitable one only if it exists,
the user agrees, and permissions allow it. Otherwise explain the limitation or
offer to help create the workflow without assuming a plugin or command exists.
