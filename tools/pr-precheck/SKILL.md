---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Determine whether exactly one PR package is ready to submit. A PR package contains the proposed title, description, commits, code diff, test evidence, and implementation plan, read against the issue it addresses and the repository's requirements. Do not grade unrelated work or multiple packages in one run.

## Inputs and modes

**Live mode:** Read the student's `plan.md`, including `## Deviations`; the committed branch diff from `git diff main...HEAD`; the draft PR title and description in `pr_draft.md`; the test results in `test_evidence.md`; and the linked issue and its discussion thread. Also read the repository's `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`. Run the diff command from the Path Review working copy. Compare the actual changes, evidence, and description against the plan, issue, and repository standards. For a house-chain submission, use the provided house plan, reproduction package, and working branch in place of the student's own artifacts.

**Eval mode:** Read only the supplied package bundle. Treat it as the complete evidence source. Do not fetch external information, inspect the local repository, or supplement missing facts. Execute every rubric check and apply the complete verdict rule to the bundle.

## The scope seam (live mode only)

Read `scope.md` before gathering any live evidence. Verify that the PR targets the repository named by `Repo:` and follow its stated rules.

If the repository is outside scope, refuse to grade and explain why. If `Repo:` contains an unfilled placeholder, stop without grading and instruct the student to configure `scope.md`. Never guess the repository.

Ignore `scope.md` entirely in eval mode.

## The voice seam (live mode only)

Read `voice-guide.md` and evaluate the outgoing PR title and description against its communication rules. Report specific violations in the readable summary, quoting the relevant text.

Voice issues do not independently change the verdict unless a check in `rubric.md` explicitly evaluates them.

Ignore `voice-guide.md` entirely in eval mode.

## Component reads

Read `rubric.md` for the named checks, their evidence requirements, pass conditions, weights, and verdict rule. Read `references/evidence-guide.md` to locate each evidence family in the selected mode. Execute `procedure.md` as written to gather evidence, compare artifacts, grade checks, and assemble the verdict.

If `rubric.md` or `procedure.md` contains no substantive instructions beyond template comments, refuse to grade and identify the missing component.

If the procedure does not explain how to perform a necessary step, report that gap instead of inventing an alternative procedure. Do not create additional checks or change rubric conditions during a run.

## Verdict and output

Return exactly one binary verdict:

- `accept`: The PR is ready to submit under the rubric's verdict rule.
- `reject`: The PR should be held because it does not satisfy that rule.

Before the machine-readable result, provide a concise summary of each check, its grade, and the deciding evidence. Include any live-mode voice concerns.

End every completed grading response with a valid fenced JSON block matching the fixed schema below. Include every rubric check, use only `pass`, `fail`, or `unclear` grades, and provide one line of concrete evidence for each. Use the PR URL or package ID as the item identifier. Do not add anything after the JSON block.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- **Evidence first:** Every check must cite a specific fact, artifact, or quote supporting its grade. Do not use unsupported judgments.
- **Grade the thing, not the polish:** A concise but complete PR can pass; a polished PR with hidden scope drift or missing evidence must not pass.
- **The rubric decides:** Apply each check's written pass condition and weight consistently, even when intuition suggests a different outcome. Revise the rubric between runs, not during grading.
- **The procedure decides how:** Follow `procedure.md` in its stated order. Report missing procedural guidance instead of improvising.
- **Unclear defaults to fail:** Apply the rubric's explicit handling of `unclear`. If the verdict rule is silent, treat unverifiable required evidence as failing rather than assuming it exists.