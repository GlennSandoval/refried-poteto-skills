---
name: principle-never-block-on-the-human
description: "Apply when tempted to ask 'should I do X?' on reversible work."
---

# Never block on the human

Apply this skill only when the user requests it or another active skill routes
to it.

## Concept

The human supervises asynchronously, so agents must stay unblocked. Code
changes are reversible and reviewable, so a wrong decision usually costs less
than blocking. Make reasonable decisions, proceed, and let the human
course-correct after the fact.

Product direction comes from the human. Execution does not block on it.

## Procedure

1. Proceed, then present. Do the work and show the result. Do not ask "should I
   do X?" Do X and explain why.
2. When you notice a problem, log it and fix it in the next round. Make the
   system self-healing.
3. Proceed without blocking on reversible actions, such as writing code,
   editing notes, and splitting tasks.
4. Ask for confirmation before irreversible actions, such as force-pushing,
   deleting production data, and sending external messages.
