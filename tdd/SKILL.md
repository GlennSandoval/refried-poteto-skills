---
name: tdd
description: "Use only when the user explicitly asks for TDD, a failing test, or a regression test, OR when the bug has an obvious cheap local test target. Skip when the test path is unclear, expensive, integration-heavy, or not requested."
---

# TDD bug fix

Apply this skill only when the user requests it or another active skill routes
to it.

When you fix a bug that has a clear, cheap test path, make the broken behaviour
executable before you change production code. The goal is a focused regression
test that fails before the fix and passes after it.

## When to skip the test

Do not force a test when it would be impractical. Skip adding a new test if the
available test would need any of these:

- broad harness setup
- brittle mocks
- slow end-to-end infrastructure
- production-only state
- vague reproduction steps
- large unrelated fixture churn

In that case, use the closest useful verification instead. See
[Use a different check](#use-a-different-check-when-a-failing-test-is-impractical).

## Workflow

1. **Understand the bug.** Identify the intended behaviour, the current
   behaviour, the affected path, and the smallest observable reproduction.
2. **Choose the narrowest executable check.** Prefer the closest unit,
   component, integration, or regression test that the codepath already uses.
   If no practical test path is obvious, do not create one from scratch just to
   satisfy the workflow.
3. **Write the failing test first.** Add the smallest focused test that would
   have caught the bug. Make the test encode the intended behaviour. Do not
   mirror the current implementation.
4. **Run the new test before you fix the bug.** Confirm that it fails for the
   intended reason. If it passes, or fails for an unrelated reason, correct the
   test or the reproduction before you edit the implementation.
5. **Fix the bug.** Make the smallest production change that satisfies the
   intended behaviour and preserves nearby contracts.
6. **Rerun the regression test.** Confirm that the test now passes.

## Use a different check when a failing test is impractical

Use the closest executable regression check instead. Examples are a targeted
script, a manual reproduction command, browser automation, a snapshot
comparison, a log assertion, or a focused integration check.

Prefer no new test over a bad test. A bad test has one or more of these
properties:

- It mostly tests mocks.
- It encodes current implementation details.
- It depends on timing or unrelated global state.
- It needs expensive infrastructure for a small fix.
- Someone would delete it immediately after it proves the fix.

## Guardrails

- Do not change tests merely to match a wrong implementation.
- Do not weaken existing assertions unless the expected behaviour has
  genuinely changed and the reason is clear.
- Keep the regression test focused on the bug. Avoid broad fixture churn and
  unrelated coverage expansion.
- If the bug is flaky, make the test deterministic where possible. Document the
  signal that the test locks down.
- If the bug exposes a broader class of failures, land the focused regression
  path first. Then consider additional sibling coverage.

## Final response

Report the evidence, not only the outcome:

- Name the failing-before test or executable check and the failure that it
  produced.
- Name the passing-after test run and any nearby validation that you performed.
- If you could not demonstrate failing-before evidence, state why and describe
  the closest regression check that you used instead.
