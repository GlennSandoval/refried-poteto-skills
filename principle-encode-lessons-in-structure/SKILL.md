---
name: principle-encode-lessons-in-structure
description: "Apply when you catch yourself writing the same instruction a second time, or notice a recurring correction. Encode the rule as a lint, metadata flag, runtime check, or script instead of more text."
---

# Encode Lessons in Structure

Apply this skill only when the user requests it or another active skill routes
to it.

## Principle

If the fix is structural, use only the structural fix. The instruction is the
symptom.

## Procedure

1. Encode the rule as a lint, a metadata flag, a runtime check, or a script.
2. If the lesson needs judgment and you cannot encode it, make the instruction
   more prominent. Add an example of the failure mode.
