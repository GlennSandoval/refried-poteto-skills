---
name: ketchup-video
description: "Catch the user up like /ketchup, with a short subtitled video of slides for what happened and the waiting calls as text under it. Use for /ketchup-video."
---

# Ketchup video

Apply this skill only when the user requests it or another active skill routes
to it.

Follow the [ketchup skill](../ketchup/SKILL.md), but show what happened in a
short subtitled video instead of its summary and visuals.

## Scope and reply

- The window starts at the last message that the user wrote before this
  request.
- Writing and rendering the video outside the repo is the one exception to the
  read-only rule of ketchup.
- The reply contains these parts, in order: the opening sentence of ketchup, the
  video, one line that names any work left that you can do yourself, and the
  action items.
- When the video shows the options of a call, call each option by the name that
  the video gives it.
- If the host cannot render or share a video, say so and provide the normal
  ketchup recap instead. Do not omit what happened.

## Slides

Use the screenshots, recordings, diffs, and data that the work produced, not
the prose of the chat about them.

### Plan the slides

1. Before you draw, write the one sentence that the user should leave with.
2. Write one line for each slide.
3. Drop each slide that does not change what the user knows.
4. Use at most 10 slides. Fewer is better.

Do not put either note in the reply.

### Design each slide

- Make each slide carry one point.
- Build the slides on one picture and change it from slide to slide, rather
  than cut to an unrelated one.
- Use a colour or shape for one meaning only, on every slide.
- Show the work in pictures, such as how a system works, a PR stack with each
  PR's state, a before and after of a fix, or options side by side.
- Point at what changed with arrows, highlights, and motion.
- Never make a slide a bullet list, a status list, a table, or boxes with
  nothing connecting them.

### Text on slides

- Keep text to the minimum.
- Put each label on the thing it names, in plain words that a person would
  say, not tags like "Tests: pass".
- Never caption what a picture shows.
- Never give a fact twice, across slides or in the text under them.

### Content rules

- Show what came of each thing that the user asked for, and whether it is done,
  still running, failed, or not checked.
- Never show something as done if it still waits on the user.
- Show any bug that you found and fixed on the way.
- If a visible change has no screenshot, say so on its slide and name what
  changed on screen.
- Draw only from facts that you have. Never invent a number, and never draw a
  screen that you did not capture.

## Subtitles

1. Give each slide one short subtitle line, about ten words.
2. Say the point of the slide the way you would tell the user, from only what
   that slide shows. Say what the picture means rather than read out its
   labels.
3. Put the subtitle in a strip below the slide. Make the strip the same height
   on every slide, and keep it empty except for the subtitle, so that it never
   covers the slide.
4. Set the subtitle small, but readable when the video plays at chat size.

## Render

1. Render one silent landscape video, such as an mp4, with motion between
   slides.
2. Make every frame the slide itself, edge to edge, above its subtitle strip.
3. Make the frames from the slides. Never record a screen.
4. Burn each subtitle into the frames of its slide, so that it stays on screen
   for the whole hold of the slide.

The hold is the time that a slide is fully on screen, not counting the motion
into or out of it. Hold each slide long enough to read the words that it adds.
Allow at least one second for each three words. A slide adds its subtitle and
each word that was not on the slide before it, including a label that it
changes. The first slide adds all its words. Words inside a screenshot do not
count.

### Check the rendered file

Do these checks before you embed the video:

1. Look at one frame from each slide at chat size. Check that its subtitle is
   readable and covers nothing.
2. Measure each hold by matching the frames of the file to the slide. Do not
   use a still-frame detector, because it counts the faint ends of a fade as
   still.
3. Count the words that each slide adds against its measured hold.
4. Fix any slide that you cannot read in that time. Render again, and check
   again.
