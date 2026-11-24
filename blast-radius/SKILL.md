---
name: blast-radius
description: "Find what a change could break somewhere else before it ships, beyond the diff, and prove the one fact it's safe because of by running real code instead of writing it up. Use for 'blast radius of X', 'what could this break', or reviewing a small diff you don't trust."
---

# Blast radius

Apply this skill only when the user requests it or another active skill routes
to it.

## Purpose

Find what a change breaks somewhere else, before it ships. Use this skill for
"blast radius of X", "what could this break", or a review of a small diff that
you do not trust yet.

This skill is a companion to `how` and `why`:

- `how` tells you what the code does.
- `why` tells you why the code has its shape.
- Blast radius tells you what the code breaks somewhere else.

Listing the callers is not the job. The agent can grep them in a second. The
job is the breakage that grep does not show.

## Do not trust your own writeup

A blast-radius writeup that sounds right is worthless. It reads as convincing
whether or not it is true. So do not hand back the writeup alone. Find the one
or two facts that the whole assessment depends on, and prove them by running
code.

### Confidence levels

For each fact that the safety of the change depends on, get the fact as far
down this list as is cheap. Say where it stopped.

1. You said so. This is worthless on its own.
2. You pointed at the line: a real `file:line`, or the source of the library.
3. You showed that the bad case cannot happen. You walked the failure step by
   step and it does not reach.
4. You ran it. A script or test that calls the real code fails loudly if you
   are wrong.
5. You reproduced it in the running app.

Level 4 is usually one small script. The script imports the same library that
the app ships and calls the exact function that you are worried about.

## Procedure

1. Read the change. Read the diff, the symbols that it adds, changes, and
   deletes, and what it now does differently, including the part that the diff
   does not spell out. Pull the PR and its commits.
2. Find the one fact that makes the change safe. Most changes that look risky
   are safe because of a single fact, such as "this call only drops
   already-dead cache entries and does nothing else". If that fact holds, most
   risky cases are cleared at once. Spend your time here, not on a long list of
   maybes.
3. Look where grep stops:
   - Read the source of the library that you call. Check its pinned version and
     any local patch.
   - Work out when things run: microtasks, unmount and teardown, Solid versus
     React.
   - Follow what a symbol search misses: the JSON that an API returns, a
     database column, a wire format, another language that reads the same
     bytes, a feature flag, and code three hops downstream.
4. Assess each risk honestly.
   - Give it a real chance of happening and a real cost if it does.
   - Keep the risks that you confirmed. List the risks that you checked and
     cleared separately.
   - Cite a real `file:line`. A search that finds nothing is still an answer.
     Never make up a caller or an API.
5. Prove the one fact. Write a script or test that runs the real code, run it,
   and paste what happened.
6. For a big or wide change, use the **arena** skill to compare independent
   assessments when the host supports it. If the host does not support it,
   examine competing hypotheses yourself and disclose that the review was not
   independent.

## What to hand back

- **What it does.** What changed, including the part that is not obvious.
- **The one fact it is safe because of.** State the fact, say which level you
  got it to, and show the proof. If you could not prove it, write unproven.
- **Risks.** For each risk, give how it breaks, the `file:line`, how likely and
  how bad it is, and how to check it. Paste the proof for the risks that
  matter.
- **Cleared.** What you checked and why it is fine.
- **Before you merge.** The cheapest test or repro that catches the real bug,
  including the script that you wrote.

Write the handback through `unslop`, cite real code, and remove anything
private before it goes anywhere public.

**Reply:** the writeup above, with the one safety fact either proven or marked
unproven.
