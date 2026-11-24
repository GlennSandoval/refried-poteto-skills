---
name: automate-me
description: "Use for 'automate me', creating or updating a personal mode skill, or capturing the user's working style. Drafts or revises a mode skill using the user's own evidence and feedback."
---

# Automate me

A guided flow for turning the user's working conventions into a skill agents will follow. The output is one `-mode` skill tailored to them (e.g. `jay-mode`, `priya-mode`).

Run this workflow only when the user explicitly requests it, including on hosts
that do not support opt-in-only metadata.

Use the active host's available skill-authoring guidance if it has any. Apply
the concise writing principles below even when no authoring or prose skill is
available; do not assume a particular plugin or invocation mechanism.

## Flow

### 0. Check for an existing skill

Search the project and any user-level skill locations that the active host
documents and permits, including established category directories, for a
matching mode skill. If one exists, confirm intent through the host's question
mechanism or ordinary chat (unless the user already requested an update):

- Update the existing skill (default for repeat runs)
- Start fresh (rare, ask why before doing it)

Update mode changes the rest of the flow:
- Step 1, if permitted and available, considers workspace history since the
  last edit; use the last edit time from version control when available.
- Step 2 asks what's changed or missing, not what to capture from zero.
- Step 4 edits the existing file in place. Preserve sections the user hasn't contradicted. Revise ones with new evidence. Add new sections only for genuinely new rules.

### 1. Gather evidence

Ask for permission before accessing conversation history. Use it only when the
host exposes history for the active workspace and the user permits it. Never
search other workspaces or unrelated transcripts. If permission is not granted
or workspace-scoped history is unavailable, ask the user for representative
examples instead. The user's direct instructions are also evidence.

When permitted history is available, survey recent conversations for recurring
patterns. If the host supports delegation and permits it, independent read-only
subagents may inspect separate slices of that same authorised history and
return patterns with evidence pointers. Otherwise inspect the slices
sequentially and disclose that the pass was not independent. Before delegating,
read `~/.config/pstack/models.md` if it exists; use a configured per-role model
only if the host supports it, otherwise use host defaults. Signals to look for:

- Response preferences (length, tone, format, "dumb it down" corrections)
- Delegation habits (subagents, models, specialized workflows, parallelism)
- Verification posture (what "done" means, unit tests vs live repro, reviewers)
- Code and prose discipline (style, principles cited, lint/format tools)
- Process conventions (worktrees, commits, PRs, review/merge tooling)
- Meta preferences (fixing skills mid-task, proposing new ones)

Cross-check patterns across independent examples before treating them as
established. A direct, explicit user instruction can establish a preference;
otherwise treat a lone observation as weak and ask rather than overfit.

### 2. Ask the user directly

Evidence can miss intent that has not come up yet. Use a structured question
tool if the host has one, or ask in ordinary chat. Start with one or two broad
questions offering a few relevant categories, follow up on selected areas,
and allow a free-form answer for anything the options missed.

Don't dump 20 questions.

### 3. Cluster findings

Group the combined signals into sections. Common ones (use only what applies):

- **Response style**: length, tone, format.
- **Autonomy**: how much to do without asking, MCP tool use.
- **Understand first**: which skills to reach for when scoping or investigating a change.
- **Subagents**: default, parallelism, model-to-task, specialized workflows.
- **Prose / code discipline**: principles, lint tools, style guides.
- **Review and verify**: repro posture, verification skills, live-testing tools.
- **Process**: git worktrees, commits, PRs, review/merge tooling.
- **Skills**: skill-authoring habits, fix-the-skill-first, proposing new skills.

Use concrete, actionable rules at a consistent level of detail. Do not copy
another person's mode skill: the user's rules are their own.

### 4. Draft the skill

Use the host's supported skill-authoring workflow if available; otherwise
write the skill directly. Preserve the existing skill's location when updating.
For a new skill, follow the documented project or host convention for
project-local skills; only when neither documents one, default to
`.agents/skills/<handle>-mode/SKILL.md`. Use a documented user-level location
only if the user requests a personal skill and the host supports it.

- Use the user's first name or chosen identifier as the handle.
- Give the skill a `name` and a concise YAML `description` identifying the
  user and "work in their style"; avoid generic triggers such as "write code".
- Use only standard Agent Skills frontmatter. Automatic invocation is
  host-dependent; instruct the agent in the skill body to apply the mode only
  when the user requests it, unless they want it applied automatically.
  Follow the host's supported invocation conventions, without assuming a slash
  command or that creating a file registers it. If the host cannot discover it,
  report its path and ask the user to provide the file as context.

### 5. Iterate on prose

Apply the host's available prose or skill-authoring guidance, if any, and the
guardrails below. Otherwise edit for direct, concise instructions yourself.

Show the draft to the user and take feedback. Expect multiple iterations. Cut ruthlessly. A mode skill is not a manual.

### 6. Land it

Follow the project's contribution workflow and the user's permissions. Create a
branch, commit, or PR only when requested or authorised; if those capabilities
are unavailable, hand over the file and explain how to use it.

## Guardrails

- **Don't overfit to one conversation.** Treat a single inferred observation or
  a contradicted preference as weak; confirm it before codifying it. An explicit
  instruction from the user is sufficient evidence of their intent.
- **Don't be clever.** Restating other skills' contents, inventing metaphors, or writing "poetic" prose for an agent reader is cost without benefit. Keep it operational.
- **Reference, don't inline.** Other skills the user relies on should appear as path references, not pasted excerpts. Same for any principle docs they maintain elsewhere.
- **Keep sections minimal.** Only add a section if the user has a specific, non-default rule there. "Communicate clearly" is not a section. "Short paragraphs. Tables when comparing options. Bullets only when items are genuinely parallel." is.
- **Name conventions generic.** Use "the user" or "the human" in imperatives, not the author's first name.
- **Don't force symmetry.** If a user has no process rules worth writing down, skip the Process section entirely.

## Evaluation

A mode skill is subjective output. Ask the user whether it reads like them and
what it misses, then revise. Check discovery or invocation using the host's
supported mechanism where possible; otherwise report that registration was not
verified. Optimise the description only if trigger accuracy becomes a problem.

## When not to use

- User wants a task-specific skill (not working conventions): use the host's
  skill-authoring workflow or write one directly, without history mining.
- User wants to capture one narrow workflow (e.g. "how I write commit messages"). That's a regular skill, not a mode skill.

