---
name: principle-prove-it-works
description: "Apply after completing a task, before declaring done. Verify against the real artifact (run the feature, read the actual value, inspect the diff), not a proxy, self-report, or 'it compiles.'"
---

# Prove it works

Apply this skill only when the user requests it or another active skill routes
to it.

## Concept

Proxies do not prove that work is correct. File mtimes, self-reports, cached
output, and "it compiles" do not count. Verify every output by checking the
real thing directly.

## Procedure

1. Check the real artifact directly. Run the feature, read the actual value, or
   inspect the diff.
2. If a check fails, suspect the observation method before you suspect the
   system.
3. Script the check when you can. A deterministic script that reruns the
   comparison is better than a one-time look.
4. Keep the script output where the human can see it.
5. Commit the script only when the trail must be auditable later.
