# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-fidelity | Compare the issue and `plan.md`, including `## Deviations`, against the diff's changed files and behavior. | The implementation addresses the issue and every substantive change is consistent with the plan or explicitly documented in its deviations. An honestly disclosed limitation is allowed if the PR accurately describes what was and was not implemented. | required |
| no-silent-drift | Compare the diff against the plan's scope and non-goals, then compare both with the PR description's Changes and Notes for Reviewers sections. | No substantive change, omission, or departure from the plan is concealed. Any deviation is documented in the plan and accurately disclosed in the description. | required |
| observable-test-evidence | Compare the plan's test plan and expected behavior with the actual commands, before/after outputs, and results in the test evidence and PR description. | Evidence demonstrates an observable before/after result relevant to the issue, or honestly identifies an incomplete or unsuccessful verification. The description does not claim that unperformed or failing tests passed. Unsupported claims of successful testing fail. | required |
| repository-checks | Compare the repository's stated testing requirements in its contributing guidance and PR template with the commands and results in the test evidence. | Required checks have recorded outcomes, or any unavailable, failing, or unrun checks are explicitly disclosed with a reason. A known failing check is not automatically disqualifying when its limitation is honestly documented. | required |
| diff-reviewability | Inspect the diff's changed files and hunks against the issue, the plan, and the described changes. | The diff contains no unrelated edits, leftover debugging statements, unnecessary dead code, or avoidable formatting churn that obscures the fix. Changes remain understandable and relevant to the issue. | required |
| claims-supported | Compare the PR title, Summary, Changes, and Testing claims against the actual diff, issue, and test evidence. | Every material claim is consistent with observable evidence. Unverified outcomes are clearly qualified rather than presented as proven facts. | required |
| repository-standards | Compare the PR title and description against the requirements in the package's repository-facts block, PR template, and contribution policy. | All mandatory repository requirements are satisfied, including applicable template sections, issue reference, and an explicit, meaningful AI-use disclosure when required. An honestly disclosed technical shortfall does not excuse omission of mandatory submission requirements. | required |
| reviewer-clarity | Read the PR title and description alongside the diff and supporting evidence. | The title communicates the change, and the description helps a reviewer understand its purpose, implementation, and verification without unnecessary effort. Minor wording or presentation weaknesses do not block submission. | preferred |

## Verdict rule

Grade every check as `pass`, `fail`, or `unclear`, citing specific evidence from the package.

Return `accept` if every `required` check passes. Return `reject` if any `required` check fails or is unclear. An `unclear` grade counts as a failure for required checks because readiness cannot be assumed from missing or unverifiable evidence.

`preferred` checks provide feedback but never independently change the verdict, even when graded `fail` or `unclear`.

Judge the actual implementation and its supporting evidence, not the polish or length of the write-up. An honestly disclosed limitation or failed test is not automatically grounds for rejection when the description accurately states the outcome and the repository's mandatory requirements are satisfied. However, disclosure does not excuse unrelated changes, hidden deviations, fabricated results, or omitted mandatory PR requirements.