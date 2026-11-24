---
name: principle-test-behavior-not-implementation
description: "Apply when you write, change, or keep a test. Assert what the code's users can observe, so that the test fails when that behaviour breaks and keeps passing when only the internals change."
---

# Test behaviour, not implementation

Apply this skill only when the user requests it or another active skill routes
to it.

## Concept

A test is a claim about what users of the code can observe through its
interface. Observable behaviour includes return values, errors, state that
users can read back, and effects on outside systems. What an external service
receives is behaviour.

Private helpers, internal call order, and intermediate data are implementation.
A call to an internal helper is not behaviour.

## Judge each test with two imagined edits

- **Break the behaviour.** Imagine a wrong value, or a skipped or doubled
  effect. If the test still passes, it proves nothing. The usual causes are a
  loose assertion, an expected value that the code under test computes, and an
  assertion on data that the test built itself.
- **Change the internals** and keep every observable result. If the test fails,
  it is pinned to the implementation.

Keep a test that catches the first edit and survives the second. Rewrite or
delete the rest.

## Procedure for writing a test

1. Drive the code through its public interface with a concrete input.
2. Derive the expected value from the requirement.
3. Pair "this never happens" with a case where it does happen.
4. Assert the error type that callers branch on. Do not assert the message.
