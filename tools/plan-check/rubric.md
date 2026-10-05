# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-supported | The plan's stated diagnosis/cause read against the issue description and Repro evidence, including the reproduced behavior and artifacts | The proposed cause reasonably follows from the reproduced evidence and does not contradict it. When the exact internal mechanism is not directly established, the plan identifies it as a hypothesis or leaves room to verify it during implementation rather than presenting unsupported certainty. | required |
| cause-targeted | The plan's proposed approach and files to change read against its diagnosis and the Repro evidence | The proposed change addresses the identified cause rather than only hiding or working around the visible symptom, unless the evidence justifies a symptom-level change. | required |
| scope-bounded | The plan's scope statement, files to change, and explicit non-goals read against the diagnosed issue | The proposed work is limited to what is necessary to address the diagnosed issue, identifies meaningful boundaries, and does not introduce unrelated changes or scope creep. | required |
| executable-plan | The plan's files and implementation approach read against the repo facts and relevant code context provided in the package | The plan identifies the relevant change location and approach concretely enough that another contributor could begin the work. Remaining implementation details may be unresolved when the plan identifies the uncertainty and gives a concrete way to resolve it during implementation. | required |
| test-proves-fix | The plan's test plan read against the Repro evidence's steps, inputs, and observed behavior | The planned verification would exercise the behavior that demonstrated the bug and has an observable expected result that would distinguish a successful fix from the reproduced failure. | required |
| repo-conventions | The plan comment read against the issue/thread highlights, repo-facts block, and repository contribution or communication requirements described in the evidence guide | The comment is consistent with relevant thread context and follows applicable repository requirements, including any required disclosure or contribution conventions, without unsupported claims or promises. | required |

## Verdict rule

Accept only if every required check passes. Reject if any required check fails. An unclear grade on a required check counts as a fail because a plan should not be built from when material evidence needed to judge its readiness is missing or ambiguous.