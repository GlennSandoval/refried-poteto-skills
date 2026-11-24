---
name: automate-me
description: "Use for 'automate me', creating or updating a personal mode skill, or capturing the user's working style. Drafts or revises a mode skill using the user's own evidence and feedback."
---

# Automate me

This skill is a guided flow that turns the user's working conventions into a
skill that agents follow. The output is one `-mode` skill tailored to the user,
for example `jay-mode` or `priya-mode`.

Run this workflow only when the user explicitly requests it, including on hosts
that do not support opt-in-only metadata.

Use the active host's skill-authoring guidance if it has any. If no authoring
or prose skill is available, still apply the writing principles in this skill.
Do not assume a particular plugin or invocation mechanism.

## Flow

### 0. Check for an existing skill

Search for a matching mode skill in the project and in any user-level skill
locations that the active host documents and permits. Include established
category directories.

If a matching skill exists, confirm the user's intent through the host's
question mechanism or ordinary chat. Skip this question if the user already
requested an update. Offer these options:

- Update the existing skill. This is the default for repeat runs.
- Start fresh. This is rare. Ask why before you do it.

Update mode changes the rest of the flow:

- Step 1: if permitted and available, consider the workspace history since the
  last edit. Use the last edit time from version control when it is available.
- Step 2: ask what has changed or what is missing. Do not ask what to capture
  from zero.
- Step 4: edit the existing file in place.
  - Preserve the sections that the user has not contradicted.
  - Revise the sections that have new evidence.
  - Add new sections only for genuinely new rules.

### 1. Gather evidence

The user's direct instructions are evidence. Conversation history is more
evidence, but it needs permission.

1. Ask for permission before you access conversation history.
2. Use history only when the host exposes it for the active workspace and the
   user permits it. Never search other workspaces or unrelated transcripts.
3. If permission is not granted, or workspace-scoped history is not available,
   ask the user for representative examples.

When permitted history is available, survey recent conversations for recurring
patterns.

- If the host supports delegation and permits it, independent read-only
  subagents can inspect separate slices of that same authorised history. Each
  subagent returns patterns with evidence pointers.
- Otherwise, inspect the slices sequentially. Disclose that the pass was not
  independent.
- Before you delegate, read `~/.config/pstack/models.md` if it exists. Use a
  configured per-role model only if the host supports it. Otherwise, use the
  host defaults.

Look for these signals:

- Response preferences: length, tone, format, "dumb it down" corrections.
- Delegation habits: subagents, models, specialised workflows, parallelism.
- Verification posture: what "done" means, unit tests or live repro, reviewers.
- Code and prose discipline: style, principles cited, lint and format tools.
- Process conventions: worktrees, commits, PRs, review and merge tooling.
- Meta preferences: fixing skills mid-task, proposing new ones.

Cross-check each pattern across independent examples before you treat it as
established. A direct, explicit user instruction can establish a preference. A
lone observation is weak, so ask the user. Do not overfit.

### 2. Ask the user directly

Evidence can miss intent that has not come up yet. Ask the user directly. Use a
structured question tool if the host has one. Otherwise, ask in ordinary chat.

1. Start with one or two broad questions that offer a few relevant categories.
2. Follow up on the selected areas.
3. Allow a free-form answer for anything that the options missed.

Do not ask 20 questions at once.

### 3. Cluster findings

Group the combined signals into sections. Use only the sections that apply.
Common sections are:

- **Response style**: length, tone, format.
- **Autonomy**: how much to do without asking, MCP tool use.
- **Understand first**: which skills to use when scoping or investigating a
  change.
- **Subagents**: default, parallelism, model-to-task, specialised workflows.
- **Prose / code discipline**: principles, lint tools, style guides.
- **Review and verify**: repro posture, verification skills, live-testing
  tools.
- **Process**: git worktrees, commits, PRs, review and merge tooling.
- **Skills**: skill-authoring habits, fix-the-skill-first, proposing new
  skills.

Write concrete, actionable rules at a consistent level of detail. Do not copy
another person's mode skill. The user's rules are their own.

### 4. Draft the skill

Use the host's supported skill-authoring workflow if it is available. Otherwise,
write the skill directly.

Choose the location:

- When you update a skill, keep the existing skill's location.
- For a new skill, follow the documented project or host convention for
  project-local skills.
- If neither documents a convention, default to
  `.agents/skills/<handle>-mode/SKILL.md`.
- Use a documented user-level location only if the user requests a personal
  skill and the host supports it.

Write the skill:

- Use the user's first name or chosen identifier as the handle.
- Give the skill a `name` and a concise YAML `description`. The description
  identifies the user and "work in their style". Avoid generic triggers such as
  "write code".
- Use only standard Agent Skills frontmatter.
- Automatic invocation depends on the host. In the skill body, instruct the
  agent to apply the mode only when the user requests it, unless the user wants
  the mode applied automatically.
- Follow the host's supported invocation conventions. Do not assume a slash
  command. Do not assume that creating a file registers the skill.
- If the host cannot discover the skill, report its path and ask the user to
  provide the file as context.

### 5. Iterate on prose

Apply the host's available prose or skill-authoring guidance, if any, and the
[Guardrails](#guardrails). Otherwise, edit the draft yourself for direct,
concise instructions.

1. Show the draft to the user.
2. Take feedback.
3. Repeat. Expect multiple iterations.

Cut ruthlessly. A mode skill is not a manual.

### 6. Land it

Follow the project's contribution workflow and the user's permissions. Create a
branch, commit or PR only when the user requests it or authorises it. If those
capabilities are not available, hand over the file and explain how to use it.

## Guardrails

- **Don't overfit to one conversation.** Treat a single inferred observation or
  a contradicted preference as weak. Confirm it before you codify it. An
  explicit instruction from the user is sufficient evidence of their intent.
- **Don't be clever.** Restating other skills' contents, inventing metaphors,
  or writing "poetic" prose for an agent reader costs effort and gives no
  benefit. Keep the skill operational.
- **Reference, don't inline.** Show the other skills that the user relies on as
  path references, not pasted excerpts. Do the same for any principle documents
  that the user maintains elsewhere.
- **Keep sections minimal.** Add a section only if the user has a specific,
  non-default rule there. "Communicate clearly" is not a section. "Short
  paragraphs. Tables when comparing options. Bullets only when items are
  genuinely parallel." is a section.
- **Name conventions generically.** In imperatives, use "the user" or "the
  human". Do not use the author's first name.
- **Don't force symmetry.** If the user has no process rules worth writing
  down, skip the Process section entirely.

## Evaluation

A mode skill is subjective output.

1. Ask the user whether it reads like them and what it misses. Then revise.
2. Check discovery or invocation with the host's supported mechanism where
   possible. Otherwise, report that you did not verify registration.
3. Optimise the description only if trigger accuracy becomes a problem.

## When not to use

- The user wants a task-specific skill, not working conventions. Use the host's
  skill-authoring workflow or write the skill directly, without history mining.
- The user wants to capture one narrow workflow, for example "how I write
  commit messages". That is a regular skill, not a mode skill.
