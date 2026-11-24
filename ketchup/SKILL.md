---
name: ketchup
description: "Catch the user up on what changed in this chat since their last message, in plain words and small visuals. List every item waiting on them with what they need to decide it from the reply alone. Use for /ketchup."
---

# Ketchup

Apply this skill only when the user requests it or another active skill routes
to it.

Catch the user up on what changed in this chat since the last message they
wrote before `/ketchup`. Help them understand each change, not only where it
stands. Then lay out every call that waits on them, so that they can make it
from your reply alone.

Notifications and subagent results are not the user's messages. Assume that the
user remembers their last message and nothing after it.

## Voice

Use the voice of [`/bro`](../bro/SKILL.md), not its task. Write in plain words
and short sentences, with no jargon, like one person catching up another.

- Say what changed for the user, not how you did it. Say "the tests pass", not
  "CI is green".
- Leave out hashes, file paths, commands, build numbers, and test counts unless
  the user needs one to act.
- Call each PR, branch, or agent by a name that the user would know, not by a
  label that you invented.
- If a fact needs context to make sense, give the context or leave the fact
  out.

## Gather what changed

Keep this turn read-only. Make visuals only from what you already have. Do not
change code, start an app or a job, or post anything.

1. Collect your own work since that message, reports from subagents, and
   messages from anyone else in this chat.
2. Check the current state of each PR, CI run, or agent that this chat touched.
3. Check each number that you will show against the facts it comes from. Say so
   when you correct one.

### Identify action items

An action item is a call or step that only the user can take. Examples are a
product choice, an approval, an irreversible action, or access that you lack.

- Include any item that still waits on the user, even one raised before their
  last message.
- Do not include work that you can still do yourself.
- Never make up a call to fill the reply.
- A step that the user did not ask for and the work does not need is not an
  action item. The exception is a step that is irreversible and waits on the
  user. Give that step one line and no visual.

One call can cover many items, such as each PR in a set that awaits merge. For
each item, collect:

- its link
- what it changes for users
- the evidence behind your pick
- its risk
- your pick

Write "unknown" for a fact that the call needs and you do not know. Leave out a
link that you do not have.

## Write the reply

### Length

Spend words on the calls, not on the story.

- Keep what happened under 100 words, not counting pictures. Use fewer words
  when less happened.
- Leave out work that changed nothing for the user.
- Give each item about 30 words.
- Let the reply grow with the number of items. Two items need well under 150
  words in all, not counting pictures. Thirty items need far more.
- Never cut items or shrink them to stay under a word count. Do not replace a
  list with a count. Do not replace an item with a link. A link can add depth,
  but the reply alone must be enough to decide.

### Order

1. Open with one short sentence that names what waits on the user, or says that
   nothing does. The action items give the detail. If nothing happened and
   nothing waits on the user, say so and stop.
2. Show what happened, pictures first.
   1. Embed inline the screenshots and videos that the work produced.
   2. Embed any diagram that explains a change.
   3. Sum up in one short bullet for each thing the user asked for: what came
      of it, and whether it is done, still running, failed, or not checked.
3. Under the summary, give at most three short lines that change what the user
   knows or must do. Then name in one line any work left that you can do
   yourself.
4. List the action items.

### Summary bullets

Write each bullet the way you would say it out loud: "Search was slow from a
missing index", not "Search review: done" or "Slow search: missing index".

- Name any bug that you found and fixed on the way.
- Make each line true when read alone.
- Never mark something done if it still waits on the user.
- Leave out anything that the action items say.

### Action items

Ask the call that the user owns, such as merge, approve, or pick, and give your
pick. Put these in your pick: a step that you would take first, anything that
must happen first, and anything that cannot be undone. Give the number or link
of each PR, issue, or agent that a call is about, also in a call between
options.

Fit the shape to the call:

- **A call about one item.** Write one bullet: the call, your pick, what it
  changes for users, the evidence behind your pick, and its risk. Name the item
  once.
- **Items that share a call.** Write the call and your pick once. Then give
  each item its own bullet, riskiest first. Include its link and name, what it
  changes for users, the evidence behind your pick, and its risk. Name an
  item's pick only where it differs from the call's. Give each item's risk even
  when it is low, such as "Low risk: only the colors change."
- **A call between options.** Give every option that the work weighed, each
  with what it gets the user and what it costs, and the current state when
  there is one. Those costs are the call's risk, so add no separate risk line.
  When the screenshots above show the options, write each option's gain and
  cost under its screenshot.

Say what waiting costs only when it is more than a delay, such as a deadline or
lost data.

## Visuals

A visual is a screenshot, video, diagram, chart, or generated image. Use the
host's available drawing or rendering tools. No particular visualisation skill
is required. A Markdown table is not a visual.

### When to draw

Draw when something is easier to grasp as a picture than as sentences. Examples
are how a design or system works, a PR stack or dependency chain with each PR's
state, a before and after of a fix, or options side by side.

- Never draw a status list, a list of action items, or boxes with nothing
  connecting them.
- Never give a fact twice, in text or across visuals.

### How to draw

- Keep each visual small enough to read at a glance. Use at most six boxes,
  with at most eight words in each.
- Write labels as plain words that a person would say, not as tags like "Tests:
  pass".
- Put a fact that needs a sentence in the text, or leave it out.
- Embed screenshots and videos inline when the host supports it. Otherwise,
  link to accessible artifacts or describe the visible result in text.
- If a visible change has no screenshot, mark its summary line "No screenshot
  yet," and say what changed on screen.
- Draw diagrams and charts from facts that you have, using Mermaid or another
  supported format.
- Never invent a number or a screen that you did not capture.
- Link only artifacts that exist.
