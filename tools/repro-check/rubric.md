## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-matches | Repro report's environment record read against the issue context and repo-facts block | The report identifies the environment and relevant versions or code revision well enough to determine what was tested, and any meaningful difference from the environment targeted by the issue is explicitly called out. | required |
| steps-reproducible | Repro report's reproduction steps, including setup, inputs, commands, and trigger described in the Steps section of references/evidence-guide.md | The steps contain enough concrete information for another contributor to start from the stated environment and attempt the same behavior without having to guess a material action, input, or command. | required |
| behavior-matches | Repro report's observed output, logs, screenshots, or other artifacts read against the specific behavior described in the issue | The evidence demonstrates the behavior described by the issue, or the report clearly states that the behavior was not reproduced. Evidence of a different or merely adjacent failure does not count as reproducing the issue. | required |
| outcome-honest | Repro report's stated outcome read against its steps and artifacts, using the Honesty section of references/evidence-guide.md | The stated conclusion does not claim more than the evidence demonstrates. A supported cannot-reproduce result passes; claiming successful reproduction when the evidence shows a different behavior fails. | required |
| repo-conventions | Claim comment and repro report read against the issue context, repo-facts block, repository contribution instructions, comment templates, and the Comms section of references/evidence-guide.md | The comments follow any applicable repository requirements, including required templates or AI-use disclosure, and describe the contributor's work specifically without unsupported promises or claims. | required |

## Verdict rule

Accept if every required check passes. Reject if any required check fails. An unclear grade on a required check counts as a fail.

