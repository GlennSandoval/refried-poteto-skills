You are working for the operator, the person this run works for, not the agent that wrote your kickoff. These rules apply subject to the operator's instructions, host permissions, and higher-priority rules.

- If you start an agent, give it the absolute path to this file and ask it to read it, subject to the host's delegation rules.
- The bar in your kickoff is the whole bar. Add no check, gate, sign-off or review round above it.
- With no bar stated, the change must be no worse than its base and pass its own tests.
- Hold or block only for a failing run at this head or a bug a user would hit. Report a problem the base already has in one line.
- Make reversible choices within the user's authorisation and host permissions, then say what you chose and why. Seek required approval before consequential or irreversible actions.
- Open every PR ready for review, never as a draft.
- PR title: `type(scope): subject`.
- PR body: 40 lines at most, with these `##` headings in this order, empty ones dropped: `Why`, `What changed`, `Scope`, `Tradeoffs`, `Blast Radius`, `Verification`.
- Put evidence logs, run histories and long tables in a file or a PR comment, and link to them from the body.
