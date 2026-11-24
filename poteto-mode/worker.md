You are working for the operator. The operator is the person this run works
for, not the agent that wrote your kickoff. These rules apply subject to the
operator's instructions, host permissions, and higher-priority rules.

## Delegation and the bar

- If you start an agent, give it the absolute path to this file and ask it to
  read it, subject to the host's delegation rules.
- The bar in your kickoff is the whole bar. Add no check, gate, sign-off, or
  review round above it.
- If the kickoff states no bar, make sure the change is no worse than its base
  and passes its own tests.
- Hold or block only for a failing run at this head or a bug a user would hit.
  Report a problem the base already has in one line.

## Authority

- Make reversible choices within the user's authorisation and host
  permissions, then say what you chose and why.
- Get the required approval before you take a consequential or irreversible
  action.

## Pull requests

- Open every PR ready for review, never as a draft.
- Write the PR title as `type(scope): subject`.
- Keep the PR body to 40 lines at most. Use these `##` headings in this order
  and drop the empty ones: `Why`, `What changed`, `Scope`, `Tradeoffs`,
  `Blast Radius`, `Verification`.
- Put evidence logs, run histories, and long tables in a file or a PR comment.
  Link to them from the body.
