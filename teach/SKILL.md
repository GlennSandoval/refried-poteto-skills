---
name: teach
description: "Explain a body of work plainly so a person actually understands it. Runs the `how` and `why` skills and weaves what they find into one clear explanation. Use for 'teach me this', 'help me really understand X', 'explain this change or subsystem to me'."
---

# Teach

Apply this skill only when the user requests it or another active skill routes
to it.

**Explain what a thing is, how it works, and why it is built that way, in one
plain account at the pace of the person. The goal is that they understand it,
not that you change anything.**

Teach sits on top of `how` and `why`. Get your bearings on what the work is and
what it touches. Then run `how` for how it works and `why` for why it is that
way. Those are real skill invocations that do their own digging. Blend what
they find into one plain explanation. Lead with what matters to the person, and
go deeper when they ask.

Reword freely for teaching, with one exception. Keep the confidence language of
`why` intact. Its hedges are findings, not style.

## Plan the explanation

1. Decide the few things that the person should walk away understanding.
   - Choose them from why the person is asking (about to change it, reviewing
     it, debugging it, or new to it) and from what they already know. Read
     both from the conversation. Do not quiz the person.
   - Skip what they plainly already know.
   - Put the depth where their question is.
2. Let `how` and `why` do the work. Do not redo it.
   - Read the code yourself to get oriented.
   - Apply `how` for how it works and `why` for why.
   - Run them in parallel if the host supports it. Otherwise, run them
     sequentially. Combine the results.
   - Match the size to the question. Use both for a subsystem. One can be
     enough for a small change.

## Write the explanation

3. Start with a plain definition.
   - Name the thing and say what it is in general terms, the way a senior
     engineer would say it out loud, with its common name if it has one.
   - Then tie it to the case in front of you ("in X, we use this to ...") and
     build from there: how it works, the deeper reasons, and the edge cases.
   - For each part, explain the idea so that it clicks: the problem that it
     solves and how it actually works.
   - When it helps the idea land, walk through what happens as the person does
     the thing (opens a long chat, scrolls up).
   - Listing functions and constants is reference, not teaching.
   - Do not print framing labels such as "the one idea to hold onto", "the thing
     to walk away with", "the key insight", "at its core", or "TL;DR".
   - Give the smallest complete answer first: a sentence or two, not a dense
     paragraph. Then stop. Add layers when the person asks. Never write a wall
     of text.
4. Keep it a conversation, not a lecture or a performance.
   - Offer to go deeper or move on, and follow the lead of the person.
   - Do not run quizzes. Do not use pacing theatre.
   - Do not print "Pause". Do not ask the person to say it back. Do not
     announce "the sentence to nail".
   - Do not flag a part as important or hard ("here is the part worth slowing
     down on", "this is the tricky part", "here is where it gets
     interesting"). Just say it.
   - When you would pause, stop and let the person respond.
   - If you run one-shot with no live human, deliver the explanation cleanly
     and put any offer to go deeper at the end.
5. Show, and do not only tell. Build the picture up diagram by diagram.
   - Open the diff, the code, or the debugger when that is the fastest way to
     land the idea.
   - Draw when a picture lands faster than words. A single simple point needs
     no figure.
   - For anything with three or more moving parts, do not draw one diagram with
     all of them at once. Draw a short series instead. Each diagram redraws the
     last and adds a single part, so that the reader watches the system
     assemble. A single all-at-once diagram, especially one saved for the end,
     is a reference, not teaching.
   - To teach a flow from A to B to C, draw it three times. First, draw A to B.
     Then redraw and add C. Then redraw and add the return edge or the next
     piece.
   - Match the medium to the idea. Use both kinds when both help.
     - Use a mermaid diagram for a flow or structure where the labels carry the
       meaning.
     - When the idea is spatial, such as layout, overlap, scroll position, or a
       before and after, use the image-generation tool. Draw it in a
       marker-on-whiteboard style with a few short labels, because image models
       garble long text. Generate that picture. Do not settle for describing it
       in words.
   - The build-up rule holds for generated images too.

## Style

Write every response with the **unslop** skill, in plain spoken English, the
way you would explain it to a colleague.

- Be tight, not terse. Cut filler and hedging. Keep the part that makes it
  click.
- State the concrete mechanism, not a metaphor, a framing, or a preview of what
  is coming.
- Match this target density: "Virtualization runs in two parts, one for
  rendering and one for loading from disk. When an item scrolls out past the
  buffer, both its DOM node and its in-memory data are evicted."
- Use normal sentence case, not all-lowercase.
- Use no em dashes.
- Prefer periods over commas. Keep each sentence to one or two commas. If
  clauses pile up, split them into separate sentences.
- Give each concept one name and keep it.
- Avoid mirror sentences ("A without B, or B without A") and tidy closers ("the
  rest follows", "it all falls out").
- Treat the words in these steps as directions to you, not labels to print. Do
  not echo the structure as headers or stock phrases.

## Reply

Reply with the explanation itself, never a report about what you did or
delivered. Lead with the main point. Then give the plain account of what it is,
how it works, and why. End with the threads that are worth chasing with `how`
or `why`.
