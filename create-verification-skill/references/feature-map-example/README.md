# Notes verification map

This directory is the maintained source for verifying the user-facing behaviour
of Notes. Read the index before you drive the app. Then use the matching
feature file as the recipe.

This is a fictional example of the map structure. Its app, harness commands,
paths, and fixtures are illustrative. Do not copy them into a real skill as
dependencies.

## Baseline preconditions

- Launch Notes at `http://127.0.0.1:4173` with a disposable data directory.
- Set `NOTES_DATA_DIR=/tmp/notes-verify-$RUN_ID` so that concurrent runs do not
  share state.
- Seed notes titled `Quarterly plan` and `Grocery list`.
- Put `control-notes` and the `notes` CLI on `PATH`.
- Run `control-notes doctor` and require the expected URL, data directory, and
  build revision.
- Never drive an instance that this verification run did not start.

## Driving conventions

- Start every recipe from the baseline state, unless its preconditions say
  otherwise.
- Use ARIA roles and accessible names. Do not use CSS selectors or DOM
  position.
- Treat every command as literal. Do not change quoted names and flags.
- Run browser actions through `control-notes browser`.
- Run terminal actions through `control-notes cli -- <command>`.
- Restore the seeded data after a mutation. Do not remove proof artifacts
  during cleanup.

## Proof and skip reporting

- Capture the user action and the resulting state, not only the final screen.
- For UI proof, include an ARIA snapshot and a screenshot with the app identity
  visible.
- For CLI proof, include the command, stdout, stderr, and exit code.
- For mutation proof, include a read-only second view of the stored value.
- Record the feature ID and the entry point that you used with every artifact.
- If a path is unreachable, report the attempted command and the unmet
  precondition.
- Do not report a skipped entry point as verified through a different path.

## Feature entry contract

Each feature file starts with an H1 title and one paragraph that describes the
user-visible behaviour. It then has exactly four H2 sections, in this order:

1. `Sub-features` lists short IDs, with one line for each behaviour.
2. `How to get to it (user POV)` lists every user entry point.
3. `Driving it with <harness>` starts with `Preconditions:`. It then uses
   labelled bullets that pair each user action with an exact command and an
   observable result.
4. `Gotchas` lists traps that can waste or invalidate a verification run.

Keep implementation details out of the map. Name only user paths, stable
handles, required state, commands, and observable proof.

## Features

- [Create a note](./create-note.md) covers browser and CLI creation,
  cancellation, persistence, and cleanup.
- [Search notes](./search.md) covers toolbar, keyboard, and CLI search with
  matching, empty, and clear states.
