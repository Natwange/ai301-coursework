# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives**

- **Eval mode:** Read the package's plan-context block, especially the diagnosis, scope, intended files, non-goals, and deviation notes. Compare these with the candidate PR's changed-file list, unified diff, and description.
- **Live mode:** Read `plan.md`, including `## Deviations`, alongside `git diff main...HEAD` and `git diff main...HEAD --stat`. Compare the changes with the linked issue's requirements and the Summary, Changes, and Notes for Reviewers sections of `pr_draft.md`.

**What good looks like**

Every substantive change in the diff is justified by the plan or a documented deviation. Any planned work that was omitted is accurately disclosed rather than silently ignored. The description matches the actual implementation.

Silent drift includes adding an unplanned change without documenting it, omitting planned behavior without explanation, or claiming that the implementation follows the plan when the diff shows otherwise.

An honest deviation must be recorded in `plan.md` and explained in the PR description. Disclosure does not automatically justify unrelated changes.

## Test evidence (harness category: not-tested)

**Where it lives**

- **Eval mode:** Compare the plan-context block's test plan and reproduction steps with the candidate PR's test-evidence section and Testing claims. Check the repo-facts block for required test commands and verification standards.
- **Live mode:** Read `plan.md` and the original reproduction evidence alongside `test_evidence.md` and the Testing section of `pr_draft.md`. Compare the recorded results with `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.

**What good looks like**

Evidence identifies the command or procedure used, the observable behavior before the change, the expected behavior after the change, and the actual result. The evidence should let a reviewer determine whether the reported issue was addressed.

Repository-required checks have visible outcomes, including passing, failing, unavailable, or unrun checks with explanations.

A statement such as "tests pass" without supporting output is insufficient. A failing check may be acceptable when the failure and its implications are accurately disclosed, but an unperformed test must not be represented as successful verification.

## Diff quality (harness category: unreviewable)

**Where it lives**

- **Eval mode:** Inspect the candidate PR's unified diff, changed-file summary, and commit list. Compare the changes against the issue and plan-context block.
- **Live mode:** Inspect `git diff main...HEAD`, `git diff main...HEAD --stat`, and the branch's commit history. Compare the changed files and hunks with `plan.md` and the issue.

**What good looks like**

The actual fix is identifiable in the diff, and the changes are limited to code, tests, and supporting modifications relevant to the issue.

Look for leftover debug statements, commented-out experiments, dead code, unnecessary formatting churn, generated artifacts, and unrelated refactoring. These can make the PR unreviewable even when the core fix works.

Do not reject a PR merely because it changes several files or contains multiple commits. Judge whether the additional changes are relevant and reviewable.

Standards and comms (harness category: standards-wall)

Where it lives

Eval mode: Read the repo-facts block's PR template requirements, contributing instructions, stated policies, and any maintainer directions included in the package. Compare them with the candidate PR's title and description.

Live mode: Read .github/PULL_REQUEST_TEMPLATE.md, docs/CONTRIBUTING.md, and relevant maintainer instructions in the linked issue thread. Compare them with pr_draft.md. Also read voice-guide.md for personal communication rules.

What good looks like

The PR follows all mandatory repository requirements. Required template sections contain meaningful, relevant content rather than empty headings or placeholders.

For Path Review, verify that the description includes a Summary, an issue reference such as Closes #54, Changes, Testing, Screenshots / Demo (or an explained N/A), and Notes for Reviewers.

The Notes for Reviewers section must contain an explicit, meaningful AI-use disclosure written in the contributor's own words. It should also disclose relevant deviations and limitations.

Check whether specific maintainer instructions or contribution policies have been followed. Do not invent requirements absent from the provided repository evidence.

In live mode, report voice-guide violations separately. They affect the verdict only when an explicit rubric check makes them relevant.

A polished description does not compensate for missing mandatory sections, ignored repository policies, or an absent AI-use disclosure.