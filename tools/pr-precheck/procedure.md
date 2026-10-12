# Procedure: how this tool grades a PR package

## Read order

1. Identify the mode and the single PR package being graded. In live mode, read `scope.md` first and verify that the repository is allowed. Stop without grading if the scope is unconfigured or the repository is outside scope. In eval mode, use only the supplied bundle and ignore `scope.md`.

2. Read `rubric.md` and `references/evidence-guide.md` to identify the checks, pass conditions, and evidence locations. Confirm that `rubric.md` and `procedure.md` contain substantive instructions. Refuse to grade if either is still an empty template.

3. Read the issue description and relevant discussion thread. Record the reported problem, expected behavior, and any constraints. In eval mode, use only the issue information included in the bundle.

4. Read `plan.md` before inspecting the diff. Record the diagnosis, intended changes, named files, explicit non-goals, test plan, and `## Deviations`. This establishes the agreed scope before seeing what was implemented.

5. Read the committed diff. In live mode, run `git diff main...HEAD` from the repository's working copy and inspect `git diff main...HEAD --stat` for the complete changed-file list. In eval mode, use the bundle's diff and changed-file summary. Record each changed file, substantive edit, and potential unrelated change.

6. Read the test evidence. Record the reproduction commands, before/after results, expected outcome, and results of the repository's required checks. Compare these with the plan's test plan.

7. Read the draft PR title and description. Record claims about implementation, changed files, test outcomes, limitations, and deviations. Identify the issue reference and AI-use disclosure.

8. Read the repository standards. In live mode, inspect `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, and `voice-guide.md`. In eval mode, use only the bundle's repository-facts and standards information; ignore the voice guide.

Do not grade checks until this initial evidence inventory is complete. Reading the plan before the diff prevents the implementation from redefining its own scope.

## Evidence gathering

1. **Plan fidelity:** Create a mapping between every substantive diff change and the corresponding plan statement or documented deviation. Compare the resulting behavior with the issue's expected outcome. Record any missing implementation or unexplained additions.

2. **Silent drift:** Compare the plan's scope and non-goals with the changed-file list and diff hunks. For each departure, look for an explanation in `plan.md` under `## Deviations` and a corresponding disclosure in the PR description. Record the exact mismatch if either explanation is missing.

3. **Observable testing:** Compare the plan's expected behavior and test plan with the supplied test commands and outputs. Record the before result, after result, whether the change is observable, and whether the description accurately represents those results. Distinguish a failed test from an unperformed test.

4. Provide a concise per-check summary with the check name, grade, and deciding evidence. In live mode, include any voice-guide violations separately.

5. End with the exact fenced JSON structure required by SKILL.md and CONTRACT.md. Populate item with the PR URL or bundle ID, include every check in rubric order, and use only pass, fail, or unclear as grades. Set verdict to exactly accept or reject.

6. Ensure the JSON is syntactically valid and is the final content in the response. Do not append explanations, recommendations, or other text after the closing code fence.