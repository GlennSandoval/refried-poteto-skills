### Authoring or modifying a skill

You own the skill's voice.

#### Principles for the text

When in doubt, delete. Keep only prose that changes a decision. Tell the reader
to do the thing and skip the reason. Explain only when the rule is confusing
without a reason. Match the tone to the scope.

Point at structural sources (types, READMEs, config) per the
**encode-lessons-in-structure** principle skill. Delegate to other skills by
path. Do not restate them. When you keep hitting a workflow that no skill
captures, propose a new skill.

#### Procedure

1. If the host provides skill-authoring guidance, use it. Otherwise follow the
   repository's existing skill format and write the workflow directly.
2. Validate the skill:
   - The frontmatter has `name` and `description`.
   - Each referenced file exists.
   - Each cross-skill link resolves.
3. If the skill is structural, add test cases. If it is subjective, skip the
   test cases.
4. Run **Opening a PR**.

#### Reply

Give a summary of the skill, the key design decisions, and the validation
notes.
