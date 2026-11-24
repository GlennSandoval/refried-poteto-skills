---
name: principle-foundational-thinking
description: "Apply before writing logic: choosing core types and data structures, sequencing scaffold-vs-feature work, asking what concurrent actors share. Get the data structures right so downstream code becomes obvious."
---

# Foundational Thinking

Apply this skill only when the user requests it or another active skill routes
to it.

## Principle

Get the data shape right before you write logic. DRY the structure, not every
line.

## Data shape

1. Define the core types early.
2. Trace every access pattern.
3. Choose structures that match the dominant paths.

## Shared state

Before you share state between actors, ask what happens if another actor
modifies it concurrently. If the answer is not "nothing", isolate the state.

## Sequence of work

1. Remove dead code.
2. Scaffold first. Do first whatever helps every later phase, such as CI,
   tests, and shared types.
3. Keep commits small and single-purpose.
