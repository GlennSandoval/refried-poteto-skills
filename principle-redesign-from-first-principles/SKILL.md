---
name: principle-redesign-from-first-principles
description: "Apply when integrating a new requirement into an existing design."
---

# Redesign from first principles

Apply this skill only when the user requests it or another active skill routes
to it.

## Concept

When you integrate a change, do not bolt it onto the existing design. Redesign
as if the requirement had been a foundational assumption from the start. This
method preserves option value when you integrate changes into an existing
design.

## Procedure

1. Read all affected files and understand the current design.
2. Ask: "if we were writing this from scratch with this new requirement, what
   would we build?"
3. Propagate the change through every reference: types, docs, examples, and
   rationale sections.
4. Think about the whole redesign, then deliver it incrementally.
