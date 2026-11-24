# 🥔 Refried-Poteto Skills

Based on [poteto's pstack skills](https://github.com/poteto/plugins/tree/main/pstack/skills).

> This is for my benefit. Do with it what you will.

## About

- **Harness-agnostic:** the skills have been un-cursorfied, so they should work with any harness.
- **New Zealand English:** used throughout, because that's where I live.

## Skills and principles

- **Skills** provide workflows for specific tasks, such as reviewing a change or explaining a system.
- **Principles** provide guidance for decisions that arise across many tasks, such as fixing root causes or testing observable behaviour.

Both are defined as skill files.

## Skills

| Skill | Description |
| --- | --- |
| [`architect`](architect/SKILL.md) | Design types, signatures, and module structure before implementation. |
| [`arena`](arena/SKILL.md) | Compare independent candidates and combine their strongest ideas. |
| [`automate-me`](automate-me/SKILL.md) | Create or update a personal mode skill from the user's working style. |
| [`benchmark-checklist`](benchmark-checklist/SKILL.md) | Vet performance measurements before reporting or acting on them. |
| [`blast-radius`](blast-radius/SKILL.md) | Find what a change could break and verify its safety with real code. |
| [`bro`](bro/SKILL.md) | Restate the last message in plain language without jargon. |
| [`correct`](correct/SKILL.md) | Prevent recurring agent mistakes with structural checks and regression safeguards. |
| [`create-formal-verification-skill`](create-formal-verification-skill/SKILL.md) | Generate a project-local formal verification skill for high-risk code. |
| [`create-verification-skill`](create-verification-skill/SKILL.md) | Generate a project-local skill that verifies an application as a user would. |
| [`figure-it-out`](figure-it-out/SKILL.md) | Create an auditable playbook for complex work without a narrower workflow. |
| [`how`](how/SKILL.md) | Explain how a subsystem works and where its responsibilities belong. |
| [`in-your-own-words`](in-your-own-words/SKILL.md) | Restate the user's goals and the problem they are trying to solve. |
| [`interrogate`](interrogate/SKILL.md) | Adversarially review a change or design and prove findings by running it. |
| [`ketchup`](ketchup/SKILL.md) | Summarize work since the user's last message and identify decisions awaiting them. |
| [`ketchup-video`](ketchup-video/SKILL.md) | Catch the user up with a short subtitled slide video and pending decisions. |
| [`maintain-formal-verification-skill`](maintain-formal-verification-skill/SKILL.md) | Update formal models and properties to match changed code. |
| [`maintain-verification-skill`](maintain-verification-skill/SKILL.md) | Keep a project's verification skill and feature map accurate through live checks. |
| [`make-bot-ui`](make-bot-ui/SKILL.md) | Build a custom UI for a webhook-capable agent service. |
| [`no-comments`](no-comments/SKILL.md) | Review comments and suppressions, fix accepted findings, and encode constraints where possible. |
| [`poteto-help`](poteto-help/SKILL.md) | Guide users through pstack setup and choosing skills, playbooks, or principles. |
| [`poteto-mode`](poteto-mode/SKILL.md) | Apply poteto's style of concise communication, deliberate delegation, simple code, and verified work. |
| [`recall`](recall/SKILL.md) | Reconstruct recent working context from history, live state, and shared records. |
| [`reflect`](reflect/SKILL.md) | Turn durable lessons from the active transcript into edits to existing skills. |
| [`reframe`](reframe/SKILL.md) | Find useful expert terminology and rewrite a description using it. |
| [`setup-pstack`](setup-pstack/SKILL.md) | Configure optional per-role model choices for pstack. |
| [`sharpen`](sharpen/SKILL.md) | Deepen a task and rewrite its prompt without expanding its scope. |
| [`show-me-your-work`](show-me-your-work/SKILL.md) | Keep a reviewable, evidence-backed decision trail for long-running work. |
| [`statechart`](statechart/SKILL.md) | Check a TLA+ state model and render its behavior as a Mermaid statechart. |
| [`swarm`](swarm/SKILL.md) | Coordinate parallel workers and consolidate their results. |
| [`tdd`](tdd/SKILL.md) | Use test-driven development when requested or when a bug has an obvious cheap test target. |
| [`teach`](teach/SKILL.md) | Explain a body of work by combining how it works with why it was designed that way. |
| [`technical-writing`](technical-writing/SKILL.md) | Write and review technical documentation using layered style standards. |
| [`typescript-best-practices`](typescript-best-practices/SKILL.md) | Apply TypeScript best practices when reading or editing TypeScript. |
| [`unslop`](unslop/SKILL.md) | Remove AI writing tells from prose. |

## Principles

| Principle | Description |
| --- | --- |
| [`principle-attack-the-premise`](principle-attack-the-premise/SKILL.md) | Test a shared assumption directly when multiple fixes based on it fail. |
| [`principle-boundary-discipline`](principle-boundary-discipline/SKILL.md) | Validate external inputs at boundaries and keep business logic focused. |
| [`principle-build-the-lever`](principle-build-the-lever/SKILL.md) | Build reusable tools to perform or prove non-trivial work. |
| [`principle-encode-lessons-in-structure`](principle-encode-lessons-in-structure/SKILL.md) | Encode recurring lessons in checks or tooling instead of repeated instructions. |
| [`principle-exhaust-the-design-space`](principle-exhaust-the-design-space/SKILL.md) | Compare competing prototypes before committing to an unfamiliar design. |
| [`principle-experience-first`](principle-experience-first/SKILL.md) | Favor a polished user experience over implementation convenience. |
| [`principle-explain-the-number`](principle-explain-the-number/SKILL.md) | Understand what limits a measurement and verify what it actually measures. |
| [`principle-fix-root-causes`](principle-fix-root-causes/SKILL.md) | Trace symptoms to their root causes and fix them there. |
| [`principle-foundational-thinking`](principle-foundational-thinking/SKILL.md) | Choose sound data structures and foundations before writing logic. |
| [`principle-guard-the-context-window`](principle-guard-the-context-window/SKILL.md) | Keep bulky outputs and unnecessary detail out of the main working context. |
| [`principle-laziness-protocol`](principle-laziness-protocol/SKILL.md) | Prefer deletion and the smallest change that solves the problem. |
| [`principle-make-operations-idempotent`](principle-make-operations-idempotent/SKILL.md) | Design operations to converge on the same state after retries or interruptions. |
| [`principle-migrate-callers-then-delete-legacy-apis`](principle-migrate-callers-then-delete-legacy-apis/SKILL.md) | Migrate all callers and remove obsolete internal APIs in the same change. |
| [`principle-minimize-reader-load`](principle-minimize-reader-load/SKILL.md) | Reduce layers and hidden state that make code hard to follow. |
| [`principle-model-the-domain`](principle-model-the-domain/SKILL.md) | Model domain concepts explicitly when building stateful or branching logic. |
| [`principle-never-block-on-the-human`](principle-never-block-on-the-human/SKILL.md) | Proceed with reversible work instead of asking unnecessary permission. |
| [`principle-outcome-oriented-execution`](principle-outcome-oriented-execution/SKILL.md) | Converge on the target architecture without throwaway compatibility layers. |
| [`principle-prove-it-works`](principle-prove-it-works/SKILL.md) | Verify the real artifact before declaring work complete. |
| [`principle-redesign-from-first-principles`](principle-redesign-from-first-principles/SKILL.md) | Reconsider the design from first principles when integrating a new requirement. |
| [`principle-separate-before-serializing-shared-state`](principle-separate-before-serializing-shared-state/SKILL.md) | Eliminate shared writes before introducing serialization. |
| [`principle-sequence-verifiable-units`](principle-sequence-verifiable-units/SKILL.md) | Order multi-step work as small, independently verifiable units. |
| [`principle-subtract-before-you-add`](principle-subtract-before-you-add/SKILL.md) | Remove obsolete code and redundancy before building on top. |
| [`principle-test-behavior-not-implementation`](principle-test-behavior-not-implementation/SKILL.md) | Test observable behavior rather than internal implementation details. |
| [`principle-type-system-discipline`](principle-type-system-discipline/SKILL.md) | Use types to represent valid states and validate external data at boundaries. |
