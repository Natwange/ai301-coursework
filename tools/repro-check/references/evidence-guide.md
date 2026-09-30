## Environment

**Where it lives:** In an eval bundle, look at the issue context and repo-facts block for the environment or versions the issue targets, then compare them with the environment record in the repro report. In live mode, compare the issue and repository documentation with the environment recorded in the student's draft report.

**What good looks like:** The report identifies the operating system or platform, relevant tool/runtime versions, and repository version or revision when those details affect reproduction. Any meaningful difference from the issue's target environment is clearly stated rather than hidden.

## Steps

**Where it lives:** In an eval bundle, look at the reproduction steps in the repro report and use the issue context to determine what action is supposed to trigger the problem. In live mode, read the student's steps alongside the issue and relevant repository setup documentation.

**What good looks like:** Another contributor can follow the described setup, inputs, commands, and triggering action from the stated starting point without guessing a material step. The steps should reproduce the attempted test, not merely summarize what the contributor tried.

## Behavior shown

**Where it lives:** Look at the output excerpts, logs, screenshots, error messages, or other artifacts in the repro report and compare them directly with the behavior described in the issue.

**What good looks like:** The artifact visibly supports the reported outcome. A successful reproduction shows the same relevant behavior described by the issue, not merely another error that occurred nearby. If the expected behavior does not occur, the evidence should support a cannot-reproduce result instead.

## Honesty

**Where it lives:** Compare the repro report's conclusion and descriptive claims with its steps and artifacts. Also compare any statement in the claim comment about what has or has not already been tested with the evidence available at that point.

**What good looks like:** The contributor says only what the evidence supports. A clear cannot-reproduce or partial result is acceptable when supported by evidence. The report should not call an issue reproduced when the artifacts demonstrate a different behavior or when necessary evidence is missing.

## Comms

**Where it lives:** In an eval bundle, compare the claim comment and repro report with the issue context, repo-facts block, and any supplied contribution policy, comment template, or disclosure requirement. In live mode, check the GitHub issue thread and the repository's contribution documentation before evaluating the student's draft.

**What good looks like:** The comments identify the specific issue and work being attempted, follow applicable repository requirements, and make only claims or commitments supported by the contributor's actual work. If the repository requires disclosure of AI assistance or another specific convention, the comment follows that requirement.