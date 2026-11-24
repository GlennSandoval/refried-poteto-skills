---
name: how
description: "Use for \"how does X work\", code walkthroughs before changing something, and placement / ownership / layering questions (\"where should this live\", \"which package owns this\", \"is this the right layer\"). Explains subsystem architecture, runtime flow, onboarding mental models. Use why for motivation."
---

# How

Apply this skill only when the user requests it or another active skill routes
to it.

This skill answers "how does X work?" questions by exploring the codebase.

If the scope is ambiguous, state your interpretation and explore. The user can
redirect you.

## Explain

If the host supports delegation, ask a read-only subagent to explore and explain
in one pass. Otherwise, explore the codebase directly. Use the user's question
and this brief:

> You are writing an architectural explanation for a senior engineer. Explore the codebase and write an explanation that a senior engineer unfamiliar with this area could read and walk away with a solid mental model. They should understand the architecture well enough to start working in it confidently. You have read-only access to the codebase.

## Present

Present the explanation. Ground it in the code that you or the subagent
inspected.
