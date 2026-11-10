# Contribution: Studio recorder: unit tests for the event-to-ProbeScript mapping

**Contribution Number:** 1
**Student:** Natwange Chiwele
**GitHub Username:** Natwange
**Issue:** https://github.com/AlphaWaveSystems/flutter-probe/issues/404
**Pull Request:** https://github.com/AlphaWaveSystems/flutter-probe/pull/534

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

**Unit 7: Validated my contribution using the ship-gate and manifest**

I used Claude Code's ship-gate and a gate manifest to validate my `test/404-recorder-mapping` branch before opening a pull request. The gate passed all six required checks after I corrected documentation inconsistencies and confirmed the commits had DCO sign-offs. I encountered Windows compatibility problems when the gate tried to launch Claude, so I updated the local command to use `claude.cmd`. After validation, I opened PR #534 through Claude Code and resolved a changelog merge conflict.

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

- **OS:** Windows 11 Pro 10.0.26200
- **Go:** 1.27.3 windows/amd64
- **Project:** AlphaWaveSystems/flutter-probe, `main` at `e80270e`, clean working tree
- **Package manager:** npm, used to build the Studio frontend

The `studio/` directory is its own Go module, joined to the root module through `go.work`. `studio/main.go` embeds the built frontend (`frontend/dist`), so the Go package will not compile until the frontend has been built. Before running any Go tests, I ran these commands in `studio/frontend`, and both succeeded:

```
npm ci --no-audit --no-fund
npm run build
```

The main challenge was choosing a test filter. A `-run` pattern using `Recorder` missed `TestRecordedTextStaysOnOneLine`, so I used `Recorde` instead. Running the full suite with `go test ./...` on Windows also showed failures unrelated to the recorder (Unix-only syscalls in `studio/e2e`, a URL-token discovery-file permission test, and symlink tests that need admin rights or Developer Mode). Several failures appear related to Windows platform differences, but the URL-token permission failure was not fully investigated. I kept my reproduction focused on the recorder tests.

**Steps to Reproduce**

1. Clone flutter-probe and check out `main` (`e80270e`).
2. In `studio/frontend`, run `npm ci --no-audit --no-fund` and then `npm run build`.
3. From `studio/`, run the focused recorder tests:

   ```
   go test -count=1 -v -run 'Recorde|EventToProbeScript|Obscured|PlainType' .
   ```

4. Compare the existing tests in `studio/recorder_test.go` and `studio/recorder_obscured_test.go` against the three acceptance criteria in issue #404.
5. **Observed result:** all existing recorder tests pass, but several acceptance criteria in #404 are not yet covered by any test.

**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:** excerpt of the focused test run:

  ```
  --- PASS: TestRedactTreeHidesObscuredAndSecretFields
  --- PASS: TestObscuredTypeEventWritesNoTypeStep
  --- PASS: TestPlainTypeEventKeepsItsText
  --- PASS: TestEventToProbeScriptLine
  --- PASS: TestRecordedTextStaysOnOneLine
  ok  github.com/alphawavesystems/flutter-probe/studio
  ```

- **My findings:** Issue #404 is about missing test coverage, not a failing behavior, so "reproducing" it meant confirming which acceptance criteria are still untested. Some recorder tests were added by other contributors after #404 was opened, and they all pass. Checked against the three criteria:
  1. **Event kinds × selector choices — partly met.** Tap is tested with every selector choice. Long press and see are tested only with a text selector, and input (`type`) only with an id selector or no target. The `params["id"]` fallback and the empty-selector fall-through cases are not tested for any event kind.
  2. **Sanitizing quotes, backslashes, and control characters — mostly not met.** Only CR/LF flattening in selector text is tested. Quotes, backslashes, tabs, and other control characters have no tests.
  3. **Every generated line parses with `internal/parser` — not met.** No recorder test imports the parser, although `studio/run_scope_test.go` shows that a Studio test can import it.

  Based on this, I narrowed my planned work to the remaining gaps rather than the full original scope of the issue.

**Toolkit**

- **Tool:** Claude Code's repro-check skill. I used it to grade my claim comment and reproduction report against issue #404 before posting anything upstream.
- **What it produced:** A graded verdict on whether the reproduction package was ready to post. My first draft was rejected; after revisions, the final package received a **5/5 ACCEPT** verdict.
- **Difficulties:** The first draft was rejected because it raised public security-disclosure concerns: it described possible problems in more detail than is appropriate for a public issue thread.
- **What changed:** I revised the reproduction report to match the issue's exact acceptance criteria, distinguish existing test coverage from missing coverage, and document the Windows test limitations accurately. After the initial rejection, I removed potentially security-sensitive details from the public-facing report and clarified which experimental findings had not been independently reproduced. The revised report passed repro-check with a 5/5 ACCEPT verdict.

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

**PR Link:** https://github.com/AlphaWaveSystems/flutter-probe/pull/534

**PR Description:** Expanded Studio recorder unit tests for event-to-ProbeScript mapping, selector edge cases, text sanitization, and parser compatibility. Added table-driven tests and malformed-script validation without changing production code. Focused recorder tests, Go build checks, and the frontend build passed locally. Full Go test suites were attempted but did not pass in the Windows environment.

**Maintainer Feedback:**

- November 10, 2026: No maintainer review feedback received yet. The PR is awaiting workflow approval and review.

**Status:** Awaiting review

**Toolkit**

- **Tool:** Claude Code ship-gate, gate manifest, and voice guard.
- **What it produced:** A passing ship-gate report confirming that my branch met all six required checks, followed by PR #534 in the original Flutter Probe repository.
- **Difficulties:** The ship-gate initially had Windows command compatibility problems, and its review identified documentation inconsistencies. After opening the PR, GitHub reported a changelog merge conflict, and the CLA workflow failed to start because of a GitHub Actions billing issue.
- **What changed:** I updated the local gate command, corrected the documentation, resolved the changelog conflict, pushed the updated branch, and notified maintainers about the blocked workflow.

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
