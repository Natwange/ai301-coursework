# Procedure: how this skill grades a plan package

## Read order

1. Read the issue description and thread highlights first. Record the reported bug, expected behavior, and any maintainer constraints or repository expectations.
2. Read the Repro evidence before reading the proposed plan. Record the reproduced behavior, the steps and inputs that produced it, and any evidence about the cause.
3. Read the proposed plan. Record its diagnosis, proposed scope and non-goals, files to change, implementation approach, test plan, risks or uncertainties, and proposed plan comment.
4. Compare the plan against the evidence already recorded rather than treating statements in the plan as evidence for themselves.

## Evidence gathering

For each rubric check, gather the following evidence:

- `diagnosis-supported`: compare the plan's stated cause with the issue and Repro evidence. Record whether the reproduction actually supports that cause.
- `cause-targeted`: compare the proposed implementation approach and files with the supported diagnosis. Record whether the change addresses the cause or only the visible symptom.
- `scope-bounded`: record what the plan says will change, what will not change, and which files are involved. Compare these boundaries with what is necessary for the diagnosed issue.
- `executable-plan`: record the named files, implementation approach, and unresolved uncertainties. Determine whether another contributor could begin the work without guessing a material implementation decision.
- `test-proves-fix`: compare the planned test with the reproduction steps and observed failure. Record the expected post-fix behavior and whether it would distinguish a successful fix from the original failure.
- `repo-conventions`: compare the proposed plan comment with thread highlights, repo facts, and applicable repository requirements identified using the evidence guide.

Do not infer missing evidence from what would normally be true. If required evidence is genuinely absent or ambiguous, record that explicitly.

## Check execution

1. Grade the checks in this order: `diagnosis-supported`, `cause-targeted`, `scope-bounded`, `executable-plan`, `test-proves-fix`, then `repo-conventions`.
2. For each check, use only the evidence sources named by that rubric row and the facts gathered above.
3. Grade `pass` only when the evidence satisfies the complete pass condition.
4. Grade `fail` when the available evidence contradicts the pass condition.
5. Grade `unclear` when the evidence needed to decide the check is genuinely missing or ambiguous.
6. Do not turn an `unclear` into a pass by assuming what the contributor probably meant.
7. Once the needed evidence has been gathered, grade the check from those notes without changing the standard based on the likely overall verdict.

## Verdict assembly

1. Apply the verdict rule in `rubric.md`: accept only when every required check passes.
2. A `fail` or `unclear` on any required check produces a reject verdict.
3. Identify the required check or checks responsible for rejection.
4. For the deciding check, quote the specific submission evidence that caused it to pass, fail, or remain unclear, and briefly explain the comparison that produced the grade.
5. Return the per-check grades and the final binary verdict consistently with the skill's required output format.