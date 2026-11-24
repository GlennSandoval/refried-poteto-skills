---
name: principle-minimize-reader-load
description: "Apply when reviewing or shaping code that's hard to trace. Count layers between question and answer, and hidden state in the reader's head; collapse one-caller wrappers and shrink mutable scope."
---

# Minimize reader load

Apply this skill only when the user requests it or another active skill routes
to it.

## Concept

Reader load is the work a reader must do to understand code. It has two
independent axes:

- The layers the reader must trace between the question and the answer.
- The hidden or mutable state the reader must hold in their head.

Guard both axes.

## Procedure

1. Collapse layers that only forward. Inline wrappers with one caller, adapters
   with no second implementation, and pass-through methods.
2. Shrink the scope of state. Prefer these options in order:
   - Returns over mutations.
   - Locals over fields.
   - Fields over module state.
   - Module state over globals.
3. Derive values instead of syncing them.
4. Name an invariant once at the boundary. Do not name it in every consumer.

## Test

A new reader must be able to answer "where does X come from?" and "what can
change X?" in under 30 seconds. If the reader cannot, cut layers or cut state.
