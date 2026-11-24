---
name: poteto-help
description: Guides users through pstack setup, poteto-mode, and choosing a skill, playbook, or principle for a task.
---

# Poteto help

Apply this skill only when the user requests it or another active skill routes
to it.

## Scope

This skill answers help questions about pstack. It does not start the work.

1. Give the user a prompt they can send.
2. Identify the source skill for that prompt.
3. If the message asks for work instead of help, discover and read
   [poteto-mode](../poteto-mode/SKILL.md), then do the work.

## How this skill routes

This skill is a map. It routes each question to the skill that owns the
details. The skills own the details, so read the selected skill file before you
quote it.

Links in this skill are relative to this installed skill. Sibling links work
when those skills are installed alongside this one.

- Discover skills through the active host.
- If a link is missing, find that skill in the host's skill locations.
- Give the user an accessible path or a verified public source.
- Do not construct a repository URL.
- Do not link to a guide that is not installed.

Invoke skills by name with the host's supported mechanism. If the host has no
skill invocation, read the skill file and follow its instructions directly.
Prompts in this skill use plain language. They do not need a slash-command
syntax.

## Find out what the user needs

Infer the need from the message and the conversation. If the message names a
situation, route it directly. If the need is unclear, ask one question: is it
setup, starting a task, choosing a skill, fixing a run, or customising pstack?

Check state only when it affects the answer:

- The optional model configuration is `~/.config/pstack/models.md`. The host
  does not inject it automatically, so read it explicitly when it is relevant.
  If a role setting is missing or unsupported, the host defaults stay in place.
- If the project has no verification skill and no app harness, agents have no
  scripted way to drive the app. For questions about proving a change works,
  mention [create-verification-skill](../create-verification-skill/SKILL.md).
- If the project has no formal verification skill, do not claim that a property
  is proved beyond the checks that ran. For races or invariants, mention
  [create-formal-verification-skill](../create-formal-verification-skill/SKILL.md).
  If a relevant existing proof has drifted, mention
  [maintain-formal-verification-skill](../maintain-formal-verification-skill/SKILL.md).

## Get set up

Subagents and review panels cost extra. Availability, model selection,
persistent modes and unattended execution depend on the host and its
permissions.

To reduce cost, use fewer independent passes or the host's default models. If a
sequential review cannot be independent, tell the user.

To set up pstack:

1. Make the skill directories available. Follow the active host's skill
   discovery instructions. If the host does not support discovery, open the
   relevant `SKILL.md` files directly.
2. Optional: use [setup-pstack](../setup-pstack/SKILL.md) to choose supported
   per-role models. If you skip this step, the host defaults apply. Workflows
   that use model choices read them from `~/.config/pstack/models.md`.
3. Start a task. Ask the agent to use poteto-mode, and state a goal and a check
   that can pass or fail. Offer to help word the prompt with the
   [prompting guidance](references/prompting.md).

## Start a task with poteto-mode

Poteto-mode matches a task to a playbook and follows the playbook steps. A good
prompt states the goal and how to tell that the goal is done. It does not
prescribe every skill.

To help the user word a prompt:

1. Read the [prompting guidance](references/prompting.md).
2. If the host offers a persistent mode, use it. Otherwise, invoke or read
   poteto-mode again for each new task.
3. Tell the user to say "new task" when the goal changes.

## Pick a skill

The default answer is poteto-mode. Name a skill directly when the user wants
more or less than the playbook gives.

To recommend a skill:

1. Read the skill.
2. Give one example prompt.

The table names skills. It does not give mandatory command syntax.

| The user wants to | Skill |
|---|---|
| Do a non-trivial task with rigour | [poteto-mode](../poteto-mode/SKILL.md) |
| Check that the agent understood the goal before starting | [in-your-own-words](../in-your-own-words/SKILL.md) |
| Rewrite a prompt deeper, without doing the task | [sharpen](../sharpen/SKILL.md) |
| Find expert terminology and rewrite a description using checked sources | [reframe](../reframe/SKILL.md) |
| Know how code works or where new code belongs | [how](../how/SKILL.md) |
| Know why code is shaped this way or where a number came from | [why](../why/SKILL.md) |
| Understand a change or subsystem in plain words | [teach](../teach/SKILL.md) |
| Catch up on recent work on a topic | [recall](../recall/SKILL.md) |
| Catch up on this chat and the decisions waiting on the user | [ketchup](../ketchup/SKILL.md) |
| Get that chat catch-up as a subtitled video | [ketchup-video](../ketchup-video/SKILL.md) |
| Find what a small diff could break outside itself | [blast-radius](../blast-radius/SKILL.md) |
| Settle types and module shape before code crosses a boundary | [architect](../architect/SKILL.md) |
| Merge the best parts of several attempts at one brief | [arena](../arena/SKILL.md) |
| Run checks over slices or race workers and get one report | [swarm](../swarm/SKILL.md) |
| Have independent reviewers try to break a diff | [interrogate](../interrogate/SKILL.md) |
| Fix a bug test-first when a cheap local test exists | [tdd](../tdd/SKILL.md) |
| Apply TypeScript rules to TypeScript work | [typescript-best-practices](../typescript-best-practices/SKILL.md) |
| Strip comments before review with an independent reviewer | [no-comments](../no-comments/SKILL.md) |
| Clean AI tells out of prose | [unslop](../unslop/SKILL.md) |
| Write documentation, an RFC, a PR description or a commit message | [technical-writing](../technical-writing/SKILL.md) |
| Hear the last reply in plain words | [bro](../bro/SKILL.md) |
| Give agents a scripted way to drive and verify the app | [create-verification-skill](../create-verification-skill/SKILL.md) |
| Bring a verification skill and feature map back in line with the app | [maintain-verification-skill](../maintain-verification-skill/SKILL.md) |
| Formally verify a race, invariant or other property | [create-formal-verification-skill](../create-formal-verification-skill/SKILL.md) |
| Bring a formal verification back in line after code changes | [maintain-formal-verification-skill](../maintain-formal-verification-skill/SKILL.md) |
| Show user-visible states checked by a TLA+ model and paths to violations | [statechart](../statechart/SKILL.md) |
| Vet a performance number before reporting it | [benchmark-checklist](../benchmark-checklist/SKILL.md) |
| Run a large or cross-cutting change, or one to review after stepping away | [figure-it-out](../figure-it-out/SKILL.md) |
| Keep and review a decision log | [show-me-your-work](../show-me-your-work/SKILL.md) |
| Choose supported models per role and a reasoning budget | [setup-pstack](../setup-pstack/SKILL.md) |
| Turn personal working habits into a mode skill | [automate-me](../automate-me/SKILL.md) |
| Turn a finished task's lessons into skill edits | [reflect](../reflect/SKILL.md) |
| Stop agents repeating mistakes in this repository | [correct](../correct/SKILL.md) |
| Build a page that wakes a Grok Bot webhook routine | [make-bot-ui](../make-bot-ui/SKILL.md) |
| Find their way around pstack | poteto-help |

If an installed skill is missing from the table, read its frontmatter and route
by its description. The `principle-*` skills are covered in
[Playbooks and principles](#playbooks-and-principles).

### Close calls

Some skills look alike. Use these distinctions:

- how explains what code does. why explains the reasons. teach makes the result
  understandable.
- arena gives workers the same brief and combines the results. swarm splits work
  into slices or a race.
- interrogate reviews the diff. blast-radius looks outside the diff for
  breakage.
- recall rebuilds prior context where available. ketchup covers this chat.
- figure-it-out designs a rigorous run. The Autonomous run playbook drives a
  task to a finish condition.

External tools and skills are optional capabilities. They are not part of this
bundle. Discover them on the active host before you recommend them.

## Playbooks and principles

### Playbooks

Playbooks are step lists inside poteto-mode. To use one, describe the task or
name the playbook. Examples are Babysit for a PR, Shipping to land a stack,
Session pickup to take over a branch, Pause safely, Autopilot-full,
Autopilot-stack and Eval.

1. Read the [playbook list](../poteto-mode/SKILL.md).
2. Read the selected playbook for its actual boundaries.

Unattended execution requires host support and permissions. If it is not
available, run the steps that you can reach and report the gap.

- For work that spans phases or stacked PRs, request the
  [Multi-phase plan](../poteto-mode/playbooks/multi-phase-plan.md) playbook. It
  writes a plan without implementing it.
- For a design question, request Prototype or architect.

### Principles

Principles are individual skills that guide decisions. The
[principles list](../poteto-mode/SKILL.md) identifies them.

To apply a principle, ask for it by name, such as "prove it works". Discover and
read its skill before you cite it.

## Fix a run that went wrong

| Symptom | Fix |
|---|---|
| The mode stopped applying | Use the host's persistent mode if available, or ask to use poteto-mode again. |
| A question was treated as the previous task's next step | Say "new task" or say the turn does not need the mode. |
| A model choice had no effect | Check that the workflow read `~/.config/pstack/models.md` and the host supports that role and choice. Otherwise it uses the host default. |
| Runs cost more than expected | Use fewer independent passes or host defaults; see Get set up. |
| A skill did not load | Discover and invoke it with the host's supported mechanism, or read its file directly. |
| Parallel agents overwrote each other | Give agents separate worktrees or disjoint files; otherwise run the work sequentially. |
| An unattended run stopped early | Check whether the host supports unattended continuation, and give it a pass-or-fail completion predicate. If not, resume manually and report the limitation. |
| A reply claims success from a green build | Ask for the real command, flow, stored value or profile that proves the outcome. |

For a run that drifts, the [prompting guidance](references/prompting.md) has
one-line steers. The [recipes](references/recipes.md) have example prompts.

## Make pstack my own

- [automate-me](../automate-me/SKILL.md) drafts a personal mode from the user's
  working habits, where the needed history is available.
- [reflect](../reflect/SKILL.md) turns session lessons into skill edits for the
  user to approve.
- Ask poteto-mode to write a skill for a workflow. Its authoring and eval
  playbooks cover writing and evaluating the skill.
- Fix a misbehaving skill separately from the feature work where it went wrong.

## Reply

Lead with the answer. Keep the reply short, unless the user asked for the whole
map.

1. Give at most one example prompt in a code block. If an example in
   [`references/recipes.md`](references/recipes.md) fits, adapt it.
2. Add the link to that file.
