### Eval

You own the experiment design. Plan, blind, run, and synthesise.

#### Blinding rules

These rules are mandatory.

- Do not use `eval`, `test`, `judge`, `experiment`, `rubric`, `score`,
  `compare`, `benchmark`, `candidate`, or `arena` in any directory, file, or
  prompt that the candidate sees.
- Write the candidate prompt as an organic user request. State the goal, not
  the meta.
- Do not use chain-eliciting cues. Do not ask the candidate to list which
  skills, principles, or files it applied. Ask for design notes generally.
  Grade chain-following from code shape, not from self-report.
- Sanitise directory and slug names. Use project-shaped names that a user might
  pick.
- Do not tell the candidate that other candidates exist.
- The judge can know that it is judging, but it sees outputs by sanitised label
  only, never by model name.
- When you compare two variants, use one judge. The judge scores both sets in
  a single pass on one scale and stays blind to which set each came from.

#### Procedure

1. **Frame.** State which variant is under test and what behaviour counts as
   success. Write the rubric (3-6 concrete criteria) for the judge only. Hold
   it back from candidates.
2. **Set up sanitised environments.** Make a working directory for each
   candidate with the variant in place. Plant any context that an organic task
   would have, such as a project skeleton and the skills that the candidate
   would naturally read.
3. **Author one organic prompt.** Write what a user would type. Do not leak
   what you measure.
4. **Run N candidates** in separate sanitised environments with the same
   prompt, using **arena**. Use parallel agents and different supported models
   where available. Otherwise run independent passes sequentially and disclose
   any loss of model or agent independence. Follow the Subagents section for
   model configuration.
5. **Judge blindly.** Use a separate agent and, when available, a different
   supported model family. Otherwise apply the rubric yourself and report that
   the judging was not independent. The judge sees sanitised labels and the
   rubric, never model names.
6. **Verify the chain from available evidence, not self-report.** Inspect
   candidate transcripts only if the host exposes them and permits access,
   scoped to this run. Check which files the candidate opened and the resulting
   code. If transcripts are unavailable, report chain-following as unverified.
   Do not infer it from claims.
7. **Read every candidate output yourself**, end to end. Compare it to the
   judge's verdict. Investigate disagreements and ambiguous rubric criteria.
   Then synthesise.

#### Reply

Give the variant under test, the rubric, per-candidate notes, the judge's
verdict, your synthesis, and a recommendation on whether to promote the
variant.
