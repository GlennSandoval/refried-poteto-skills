---
name: principle-guard-the-context-window
description: "Apply when context is filling up: large outputs, long files, repeated reads, fan-out planning. Route bulk to subagents; keep summaries in the main thread, not raw payloads."
---

# Guard the Context Window

Apply this skill only when the user requests it or another active skill routes
to it.

## Why this matters

Context overflow degrades reasoning quality, creates compression artifacts, and
halts progress.

## Procedure

1. Size phases and cap scope. Limit the files per phase. Set turn budgets.
   Account for the cost of each mechanism.
2. Route bulk work to subagents.
3. Keep summaries in the main thread. Do not keep raw payloads there.
