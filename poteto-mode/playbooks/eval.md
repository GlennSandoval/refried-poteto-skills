### Eval

**You own the experiment design. Plan, blind, run, synthesize.**

**Non-negotiables for blinding:**

- No `eval`, `test`, `judge`, `experiment`, `rubric`, `score`, `compare`, `benchmark`, `candidate`, or `arena` in any directory, file, or prompt the candidate sees.
- The candidate prompt looks like an organic user request. State the goal, not the meta.
- No chain-eliciting cues. Don't ask the candidate to list which skills, principles, or files they applied. Ask for design notes generally and grade chain-following from code shape, not self-report.
- Sanitize directory and slug names. Use project-shaped names a user might pick.
- Don't tell the candidate other candidates exist.
- The judge can know it's judging but sees outputs by sanitized label only, never by model name.
- Comparing two variants: one judge scores both sets in a single pass on one scale, blind to which set each came from.

**Steps:**

1. **Frame.** State what variant is under test and what behavior counts as success. Write the rubric (3-6 concrete criteria) for the judge only. Hold it back from candidates.
2. **Set up sanitized environments.** Per-candidate working dir with the variant in place. Plant any context an organic task would have: a project skeleton, the skills the candidate would naturally read.
3. **Author one organic prompt.** What a user would type. No leakage of what's being measured.
4. **Run N candidates** in separate sanitised environments with the same prompt, using **arena**. Use parallel agents and different supported models where available; otherwise run independent passes sequentially and disclose any loss of model or agent independence. Follow the Subagents section for model configuration.
5. **Judge blindly** using a separate agent and a different supported model family when available. Otherwise apply the rubric yourself and explicitly report that judging was not independent. The judge sees sanitised labels and the rubric, never model names.
6. **Verify the chain from available evidence, not self-report.** Inspect candidate transcripts only if the host exposes them and permits access, scoped to this run. Check which files were opened and the resulting code. If transcripts are unavailable, report chain-following as unverified rather than inferring it from claims.
7. **Read every candidate output yourself** end to end. Compare to the judge's verdict, investigate disagreements and ambiguous rubric criteria, and synthesise.

**Reply:** variant under test, rubric, per-candidate notes, judge's verdict, your synthesis, and a recommendation for whether to promote the variant.
