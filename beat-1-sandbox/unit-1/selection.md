# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54

**Verdict output**

Scope check: codepath/pathreview-ai301-fa26-s1 is the repo named in
scope.md, so #54 is a valid candidate. The Path Review house rule
(classmates' claim signals don't block) applies to unclaimed,
though nothing triggers it here — the thread is empty. Evidence is
the live GitHub API read from this session: repo metadata,
default-branch commits, releases, PR list, and the issue's body,
labels, assignees and timeline.

Grades

- maintainer-active — pass. Five recent main commits, all authored
  by the human account Aburke225; newest 2026-09-16, five days
  before today. Threshold is 2 human commits in 90 days.
- repo-in-use — pass. No releases exist, so this passes on the
  condition's activity branch: archived: false, pushed_at
  2026-09-16, 72 open issues, and student PR #74 opened 2026-09-21.
- unclaimed — pass. assignees: [], comments: 0, and the timeline
  holds only four label events by Aburke225 on the creation date.
  No assignee, no linked PR, no claim to read either way.
- scope-fits — pass (preferred). One function, _detect_sections()
  in resume_parser.py, with a copy-pasteable repro and three named
  failing tests in tests/unit/test_resume_parser.py. Labels good
  first issue and tier-1. Nothing umbrella-shaped.
- issue-recent — pass (preferred). created_at 2026-09-10, 11 days
  old.
- human-authored — pass (required). Opened by Aburke225, account
  type User, no [bot] suffix.

Verdict: accept — every required check passes, so the rule accepts.
Both preferred checks also pass, which is the strongest
combination available here: the beginner label is the maintainer's
own signal that it's friendly, and the three named failing tests
give you an unambiguous definition of done.

One caveat on fit: scope.md's fit profile is still the placeholder
(Write a few sentences here.), so "what made it fit" above rests on
the preferred checks, not on your background. With a single
candidate that changes nothing about the verdict, but fill that
section in before you use this skill to choose between several
issues.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54",
  "checks": [
    {
      "name": "maintainer-active",
      "grade": "pass",
      "evidence": "5 recent main commits authored by human Aburke225; newest 2026-09-16, within 90 days of today 2026-09-21"
    },
    {
      "name": "repo-in-use",
      "grade": "pass",
      "evidence": "No releases, but archived:false, pushed_at 2026-09-16, 72 open issues, and student PR #74 opened 2026-09-21"
    },
    {
      "name": "unclaimed",
      "grade": "pass",
      "evidence": "assignees: [], comments: 0, timeline holds only 4 label events by Aburke225 — no assignee, no linked PR, no claim"
    },
    {
      "name": "scope-fits",
      "grade": "pass",
      "evidence": "One function `_detect_sections()` in resume_parser.py with a repro snippet and 3 named failing tests; labels include 'good first issue' and 'tier-1'"
    },
    {
      "name": "issue-recent",
      "grade": "pass",
      "evidence": "created_at 2026-09-10, 11 days before today"
    },
    {
      "name": "human-authored",
      "grade": "pass",
      "evidence": "opened by Aburke225, account type 'User', no [bot] suffix"
    }
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

**Run history**

3/3  
4/5  
4/5  
4/5  
1/2  
3/5  
4/5  
3/5  
1/2  
17/20  
5/5  
18/20 scored items (bar: 18/20: PASS)

**Issue analysis**

`issue-20` — My rubric initially returned `accept`, while the gold label was `reject`. The repository was active, the issue was unclaimed, and the scope appeared bounded, so the existing required checks passed. Looking more closely at the evidence showed that the issue was opened by `cursor[bot]`. My rubric did not have a check for bot-authored issues, so it accepted the issue.

**Check rationale**

`| human-authored | Issue header: author username and author type shown next to "opened by" | The issue was opened by a human account, not an account explicitly identified as a bot (for example, an author shown as [bot]) | required |`

I added this check after analyzing `issue-20`. The other checks did not distinguish between human-created issues and bot-created issues. Making this required gives the rubric a clear and objective way to reject an issue that was explicitly opened by a bot.

**Trade-offs**

After adding `human-authored`, I re-ran `issue-01`, `issue-04`, `issue-06`, `issue-19`, and `issue-20` with `--only`. The run scored `5/5`: the four known accepted issues remained accepted, while `issue-20` changed from accept to reject. This gave me evidence that the new check fixed the targeted failure without changing those canary results.

---

## Selection rationale

**Selection rationale**

1. Issue #54 fits my interests because it involves Python and debugging, which are areas I have experience with. It also looks manageable in the time available because it is labeled `tier-1` and `good first issue`, focuses on one function, and provides specific failing tests.

2. The verdict correctly identified that the repository is active, the issue is unclaimed, the scope is focused, and there are clear tests that define when the fix is complete. I also weighed my own familiarity with Python and whether I would feel comfortable understanding and testing the code, which the rubric cannot fully judge for me.

3. I anticipate relatively little difficulty claiming it because the issue currently has no assignee, no comments, and no linked pull request. However, another student could still claim it before I do, so I would check the issue again before claiming it.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.