# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-active | Repo-facts block: last 5 default-branch commit dates and recent maintainer activity | At least 2 human commits were made to the default branch within the last 90 days | required |
| repo-in-use | Repo-facts block: latest release date and recent repository activity | The repository has a release or meaningful project activity within the last 12 months | required |
| unclaimed | Repo-facts block: assignee field and linked pull requests; comment thread: claim commands, bot/maintainer claim responses, statements that someone is working on the issue, and later release/unassignment messages | No current assignee, no active linked pull request, and the comment thread does not indicate an active claim or that someone is currently working on the issue. A past claim does not fail this check if a later comment explicitly releases or unassigns that contributor. If the latest claim status cannot be determined from the available comments, grade unclear. | required |
| scope-fits | Issue body and labels: requested outcome, listed work, affected components, and beginner-oriented labels | Prefer issues with a bounded goal suitable for a first contribution. Multiple files, steps, causes, or related changes may still fit when they support the same goal. Large tracking or megaissues containing many independent contribution opportunities fail this check. | preferred |
| issue-recent | Repo-facts block: issue creation date | The issue was created within the last 12 months | preferred |
| human-authored | Issue header: author username and author type shown next to "opened by" | The issue was opened by a human account, not an account explicitly identified as a bot (for example, an author shown as `[bot]`) | required |

## Verdict rule

Accept if every required check passes. Reject if any required check fails. An unclear grade on a required check counts as a fail. Preferred checks never change the accept/reject verdict; they are used only to rank accepted issues. 
