# Word the prompt

A prompt states the intent and the check for done. The playbook supplies the
steps, so a few plain sentences work better than a spec.

## Put in

- The goal. Say what is wrong or what the user wants.
- The done check. It can pass or fail. "Make it better" and a duration are not
  checks.
- The proof to show. Ask for the real command output, a video of the flow, the
  stored value, or a before and after number.
- What the user already knows. A symptom, a repro step, a log or a link saves
  the agent a search.
- The real constraints. "repro first", "don't change any code yet", "zero
  behaviour change" and "let me review before proceeding" each change what the
  agent does.

## Leave out

- The how. Say what to achieve, and leave the agent room to find a better way.
- A list of skills or steps. A hand-written order drops or reorders steps that
  the playbook keeps. Name a skill only to override one choice.
- The user's theory of the cause, until the agent restates the problem. A
  stated guess narrows the search.

## Load the context first

- For a noisy report, ask the agent to restate the underlying issue in its own
  words and in plain English before it does anything else. A misreading shows
  up before any code exists.
- In a fresh chat, ask **recall** for earlier work on the topic if the host
  exposes relevant history. Otherwise, provide the relevant notes or links.
- Before changing unfamiliar code, ask **how** for the mechanics and **why**
  for the reasons. An agent with no traced model fixes the first plausible
  spot.
- Ask **teach** to make the case for a choice, as in "convince me it fixes the
  cause and not the symptom". A case is easier to check than a summary.

## Design before the plan

- Never take the first design. Ask for prototypes of a few options, with
  screenshots or videos for UI, and pick from the evidence.
- Let prototypes answer the open questions. Do not review an abstract plan
  adversarially, because reviewers invent risks that never happen.
- For a shared package or API, ask for the README or a tutorial first, then
  work back to the code. The document becomes the target that the agent checks
  itself against.
- Ask for the plan only after the design is settled. Each step of the plan ends
  in a check.

## Follow up short

- "do it", "continue" and "keep going until done" are whole prompts once the
  chat holds the task.
- Start with "new task" when the subject changes. Otherwise, the mode treats
  the message as the next step.

## Before stepping away

Do these steps before you leave the agent running:

1. Say "I'm stepping away". State the boundaries for decisions that the agent
   may make without asking. Host permissions and approval rules still apply.
2. Write done as checks that every iteration can run.
3. If the host supports unattended continuation, give it that predicate and an
   exit condition. Otherwise, resume iterations manually. Do not promise an
   overnight run.
4. If the host can create one, ask for a fresh worktree off a named base.
5. Pre-answer what the agent would stop for, such as "don't ask me before
   committing". Stay within the host's approval rules.
6. Ask for a decision log to audit later.
7. Give an exit: "if you're truly stuck after a few hours, stop and write up
   why".

## Steer in one line

- Restate the goal: "i said the goal is to repro. i did not ask for a fix yet."
- Name the principle: "apply prove it works. show me the real output, not the
  build log."
- Ask the agent to read the relevant principle before it applies the principle,
  and to name the decision that the principle changed.
