---
name: principle-experience-first
description: "Apply when product, UX, or feature-scope tradeoffs come up. Choose user delight over implementation convenience; ship fewer polished features over more rough ones."
---

# Experience First

Apply this skill only when the user requests it or another active skill routes
to it.

## Principle

When implementation convenience conflicts with user delight, choose delight.

The user is whoever consumes the work. For a UI, the user is the end user. For
a library or an internal API, the user is the colleague who imports it. The
engineer who maintains the code next is also a user. Weigh their experience
the same way, and explain impact from their perspective.

Foundations serve the experience. Foundational thinking governs the *sequence*
of work. This principle governs the *target*.

## Guidelines

- Justify every feature, control, and option.
- Ship less and ship better. A polished experience with three features beats a
  rough one with ten.
- Prototype before you commit. Design decisions are cheaper in throwaway HTML
  than in production code.
- Get the details right: transitions, alignment, spacing, feedback, and error
  states.
- Tighten the core loop. Every feature must serve the central workflow or get
  out of the way.
