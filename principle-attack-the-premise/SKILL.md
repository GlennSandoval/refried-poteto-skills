---
name: principle-attack-the-premise
description: "Apply when two or more fixes that share one premise have failed the same gate. Write the premise down and test it directly before you write another fix that assumes it."
---

# Attack the Premise

Apply this skill only when the user requests it or another active skill routes
to it.

## When this applies

When two or more fixes that share one premise have failed the same gate,
suspect the premise, not the fixes.

## Procedure

1. Write down the premise. The premise is the one sentence that every failed
   fix assumed.
2. Find an observation that would come out differently if the premise were
   false. Make that observation. Look at how the failures are distributed, not
   only at how large they are.
3. If the evidence contradicts the premise, find what the failures share that
   the premise did not predict.
4. If one part always lands on the losing side, change what puts it there.
   Do not add a mechanism that cleans up after it.

Do not start the next fix before you write down the premise and test it.
