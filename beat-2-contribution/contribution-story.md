# Contribution: Studio recorder: unit tests for the event-to-ProbeScript mapping

**Contribution Number:** 1
**Student:** Natwange Chiwele
**GitHub Username:** Natwange
**Issue:** https://github.com/AlphaWaveSystems/flutter-probe/issues/404
**Pull Request:** Not opened yet

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built and refined my issue-scout skill**

I configured Claude Code's issue-scout skill with my programming experience, project interests, search strategy, and grading rubric. My initial scan returned 300 issues but produced candidates from only two repositories, limiting the variety of results. I updated the search strategy to limit candidates from each repository and check for existing pull requests. When I graded issues individually, the scout accepted Flutter Probe #404 and rejected Red Discord Bot #6794 because four open pull requests were already addressing it.

**Unit 6: Built a voice guard and repository memory file**

I installed a Claude Code voice guard to check outgoing GitHub comments against my writing rules before posting. The guard initially failed because its Python subprocess could not launch Claude through the Windows command wrapper, so I updated it to use `claude.cmd` and confirmed that my claim draft passed. I also created a local repository memory file for Flutter Probe, documenting contribution rules, recorder-related files, existing tests, and testing commands. During orientation, I discovered that other contributors had already implemented some of the tests requested in issue #404, so I narrowed my planned work to the remaining test gaps.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I searched for open-source issues using my issue-scout tool and reviewed the results for clear, manageable contributions. My initial search surfaced several possibilities, but some were already being addressed by other contributors. I eventually found [Flutter Probe issue #404](https://github.com/AlphaWaveSystems/flutter-probe/issues/404), which asks for unit tests covering the conversion of recorded events into ProbeScript. After updating my scout's rubric and regrading the issue, it returned an **ACCEPT** verdict with a **straightforward** difficulty rating. I chose this issue because it has a clearly defined scope, involves testing and code analysis, and gives me an opportunity to strengthen my open-source contribution skills while learning more about Go.

The search also exposed a weakness in my issue-scout tool: its original rubric favored beginner-friendly issues rather than evaluating whether the work was actually feasible. I replaced that preference with a required `scope-feasible` check and added difficulty ratings that do not affect acceptance. This made the evaluation more useful because a challenging issue should not automatically be rejected if its scope is clear. I hope to learn how to navigate an unfamiliar codebase, write meaningful table-driven tests, and follow a project's contribution guidelines.

**Claim comment:** https://github.com/AlphaWaveSystems/flutter-probe/issues/404#issuecomment-6691326859

**Toolkit**

- **Tool:** issue-scout — I used my custom search strategy and rubric to evaluate open-source issues, then regraded Flutter Probe #404 after updating the rubric.
- **What it produced:** The initial scan surfaced several candidates. After regrading, issue #404 received an **ACCEPT** verdict with a **straightforward** difficulty rating.
- **Difficulties:** The original rubric favored beginner-friendly issues, which could exclude valid contributions with clear scopes. Another candidate was already being addressed by multiple pull requests.
- **What changed:** I replaced `scope-fits` with a required `scope-feasible` check and added difficulty ratings that describe complexity without affecting the verdict.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
