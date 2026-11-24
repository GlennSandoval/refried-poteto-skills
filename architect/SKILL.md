---
name: architect
description: "Sketch types, signatures, and module structure before code, then stay in the loop while implementation fills in. Use for /architect, 'architect this', 'design this', or non-trivial work where jumping to code would lock in the wrong shape."
---

# Architect

Apply this skill only when the user requests it or another active skill routes
to it.

Writing code first can lock in the wrong shape. This skill fixes the shape
before the code exists. A good shape gives each piece of state one owner, gives
each task one way to do it, and asks callers to know as little as possible.

## Design the shape

1. Trace every system the change touches.
2. Sketch two different shapes for the change. Include types, signatures, and
   module boundaries.
3. Pick the shape where each piece of state has one owner, each task has one
   way to do it, and callers need to know least.
4. If workarounds repeat, redesign instead of patching.

## Contested designs

For a large or contested design, run the **arena** skill instead of sketching
alone.
