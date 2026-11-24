---
name: create-verification-skill
description: "Generate a project-local verification skill that drives an app as a user would, for any language, framework, or platform. Use when a project has no scripted way to prove UI, CLI, or service behaviour."
---

# Create a verification skill

## Purpose

Every serious project needs a scripted way to drive the real app and prove its
behaviour: launch the app, exercise a feature the way a user would, and capture
evidence. This skill generates a project-local `verify-<app>` skill that is
tailored to the repository.

The generated skill is written for the next agent, not for a human. An agent
that has never seen the app reads it cold, in the middle of a task. Write it
for that reader.

Run this workflow only when the user explicitly requests it, including on hosts
that do not support opt-in-only metadata.

## 1. Interview the repository, not the user

Answer each question from the codebase. Ask the user only about what you cannot
observe.

- **Surface:** Find what a user touches: a web UI, a CLI or TUI, a desktop app,
  an API, a mobile app, or a library. A repository can have more than one
  surface. Select the primary surface and note the others.
- **Run:** Find how the app starts locally. Use the repository's own documented
  development command first (package scripts, Makefile, README quickstart).
  Note the ports, environment variables, seed data, and authentication.
- **Drive:** Find how an agent can interact with the app programmatically. Use
  existing harnesses first: Playwright or Cypress specs, expect scripts, PTY
  helpers, endpoints that curl can call, or a debug port. If none exists,
  select a generic recipe: browser or CDP for web and Electron, a tmux or PTY
  harness for CLI and TUI, plain HTTP for services.
- **Observe:** Find the evidence that you can capture: screenshots, terminal
  transcripts, response bodies, logs, exit codes, and database state.
- **Isolate:** Find out if two instances can run side by side (ports, data
  directories, profiles). If they cannot, say so in the generated skill. A
  refusal to double-drive a shared instance is better than a corrupted user
  session.

If the checkout does not build or start as it is, fix that problem first, or
report it precisely, before you generate the skill. A skill that is written
against a broken base teaches wrong steps.

If an irrelevant missing asset blocks startup (for example a static directory
that the API never serves, or a sample config), the generated skill can create
that asset. Mark it clearly as verification scaffolding and remove it in
cleanup.

## 2. Generate the skill

### Location and frontmatter

1. Find the documented project convention or the active host convention for
   project-local skills.
2. Use that supported location. If neither convention is documented, use
   `.agents/skills/verify-<app>/`.
3. Write `SKILL.md` in that location with standard Agent Skills YAML
   frontmatter: `name: verify-<app>` and a `description` that names the app,
   the surface, and when to use the skill.

Automatic invocation depends on the host. Check the host's discovery and
registration procedure. Do not assume that a file or a slash command registers
the skill. If registration is not available or you cannot verify it, report the
path and tell the user to supply the file as context.

### Required sections

Include these sections. Base each section on what the interview found. Leave no
placeholders.

- **Launch:** Give the exact command that starts the app for verification and
  the way to tell that the app is ready (a log line or a prompt).
  - Launch must reach a usable state from an empty data directory, including
    all migrations and seed data.
  - Ready means usable, not only that a process answers. A database health
    check can pass while its init scripts are still running.
  - Include teardown.
  - A short-lived CLI or TUI has no server to keep alive. For these, launch
    means: build the binary (or install dependencies) once, then start each
    drive in its own isolated PTY or tmux session.
- **Doctor:** Give one read-only check that answers "is this instance worth
  driving?" It checks that the process is up, that the version or build is
  right, that this run owns the port, and that authentication is valid. An
  agent runs it first whenever anything looks wrong.
- **Drive:** Give the harness recipe with real selectors and commands from this
  repository, not examples. Use stable handles (ARIA labels, data attributes,
  prompt strings, route paths) instead of coordinates and tab order.
- **Evidence:** State what to capture for a proof and where to store it. State
  these proof standards:
  - Exercise the real user path. Do not use internal setters or test-only
    endpoints.
  - Capture the action and the resulting state, not only the final screen.
  - Verify side effects (files written, rows inserted, messages sent) together
    with what is visible.
  - Use mocks only where a production boundary already isolates the external
    system.
  - If the safe path is a dry-run or test mode, observe what it skips (files,
    network, git refs). Do not trust its name. Some dry-runs still touch the
    network or open a browser.
- **Cleanup:** Give the steps that tear down the instances that the run
  created.
  - Never kill by process name. Kill only what you started.
  - Cleanup removes instances and scratch state. It never removes the evidence.
    Proof artifacts survive the teardown, in a location that the skill names.
- **Helpers:** Make each script that the skill ships executable, and show its
  invocation in the skill body. A helper that the reader must reverse-engineer
  is not a helper.

## 3. Seed the feature map

1. Create `features/README.md` in the chosen skill directory.
2. Create one file for each user-facing feature that you can identify. Start
   with the top 3 to 5 features, taken from routes, commands, menus, or docs.
3. Follow the shape in
   [`references/feature-map-example/`](references/feature-map-example/): a
   README index and one file for each feature.

Each feature file answers four questions from the user's point of view: what
the feature is, how to reach it, how to drive it with the harness, and what
observable end state proves that it works. The four H2 headings are
`Sub-features`, `How to get to it (user POV)`, `Driving it with <harness>`, and
`Gotchas`.

If the seed data lacks a precondition that a journey needs, the journey reports
a failure. Write the reason in the `Gotchas` section of that feature. Never
weaken the journey to make it pass.

The map is the maintained verification source of the repository. A proof that
drives one convenient entry point is incomplete when the map lists other entry
points.

## 4. Prove the generated skill before hand-over

A generated skill that was never executed is a draft, not a proven deliverable.

1. Run the instructions of the generated skill from start to end once:
   1. Launch the app.
   2. Run doctor.
   3. Drive ONE mapped feature. One feature is enough, because the map exists
      so that later runs can cover the rest.
   4. Capture the evidence.
   5. Clean up.
2. After cleanup, confirm that the evidence still exists at the named location.
   A cleanup that deletes the proof fails this step.
3. Fix each failure. After every failed iteration, run the generated cleanup,
   so that broken attempts do not leave processes and ports behind.
4. If access, tools, or permissions prevent the run, report the blocker and the
   unverified steps. Do not claim success.
5. If you proved the skill in a stand-in for the real target (for example a
   container in place of a fresh VM, or a local stack in place of a remote
   one), list every setup step that the stand-in did and that the target will
   not do. Those steps stay unverified until a run on the real target covers
   them.

## 5. Offer the maintenance loop

Point the user at the `maintain-verification-skill` skill. It keeps the map
accurate as the app changes. Discover it through the host if possible.
Otherwise, give its source path for direct use. Suggest a cadence only if the
user asks.
