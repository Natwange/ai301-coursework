# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

**Where it lives:** In eval mode, read the candidate plan's diagnosis or stated cause against the issue context and Repro evidence block, especially the reproduced behavior, outputs, and any cause-related evidence. In live mode, use the GitHub issue and thread, the posted reproduction comment, and the diagnosis in the draft plan.

**What good looks like:** The stated cause explains the behavior that was actually reproduced and does not contradict the available evidence. A plausible-sounding cause is not enough when the reproduction does not support it.

## Scope

**Where it lives:** In eval mode, read the candidate plan's scope, non-goals, files or areas to change, and proposed approach. Compare them with the diagnosed issue. In live mode, use the same parts of the draft plan and relevant repository files when needed to understand the boundary.

**What good looks like:** The plan proposes one bounded change focused on the diagnosed issue. It identifies meaningful limits or non-goals and does not add unrelated cleanup, refactoring, features, or other drive-by work.

## Executability

**Where it lives:** In eval mode, read the candidate plan's named files or code areas, implementation approach, and relevant repo facts or code context included in the package. In live mode, read the draft plan and inspect the named repository files when necessary.

**What good looks like:** Another contributor can identify where to begin and what change is intended without guessing a material implementation decision. Unknown details may remain when they are explicitly identified rather than presented as settled facts.

## Test plan

**Where it lives:** In eval mode, read the candidate plan's test plan against the Repro evidence's original steps, inputs, outputs, and artifacts. In live mode, compare the draft test plan with the posted reproduction comment and the relevant repository tests.

**What good looks like:** The planned verification exercises the behavior that demonstrated the bug and states an observable expected result. The result must distinguish the original failure from a successful fix rather than merely showing that unrelated tests run.

## Honesty

**Where it lives:** In eval mode, read the candidate plan's risks, unknowns, assumptions, and claims about the diagnosis or implementation. In live mode, use the draft plan, plan comment, and any later recorded implementation deviations.

**What good looks like:** Unverified assumptions and unresolved decisions are identified as such. The plan does not present speculation as confirmed fact, and any meaningful deviation discovered during implementation is recorded rather than silently hidden.

## Comms

**Where it lives:** In eval mode, read the candidate plan comment against the issue context, thread highlights, repo-facts block, contribution requirements, templates, and any AI-use policy. In live mode, read the current GitHub issue thread, repository contribution documentation, and the draft plan comment.

**What good looks like:** The comment is specific to the issue and consistent with relevant maintainer guidance and repository requirements. It does not ignore important thread context, required disclosures, templates, or make unsupported promises about the fix or timeline.