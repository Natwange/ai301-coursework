# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong label is not graded.

---

## Posted upstream

**GitHub username**

Natwange

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54#issuecomment-5987378430

I reproduced the leading-whitespace section detection issue and traced it to `_detect_sections()` in `ingestion/parsers/resume_parser.py`. The current patterns allow whitespace after a section name but expect the section name to begin immediately at the start of a line, so indented headings such as `Education:` and `Skills:` are not detected.

My plan is to update the section-detection patterns to allow leading whitespace while preserving detection of non-indented headings. I'll keep the change limited to section detection and verify it by re-running the reproduction, the existing issue #54 tests, and a non-indented-heading control. Any unrelated parser or Markdown failures will remain out of scope.

---

## Branch

**Branch**

fix/54-leading-whitespace-sections

**Evidence**

### Before

Unit 2 reproduction:

```python
from ingestion.parsers.resume_parser import ResumeParser

r = ResumeParser()

res = r.parse("""
    John Smith
    john@example.com

    Education:
    - B.S. Computer Science

    Skills: Python
""")

print(res.metadata["detected_sections"])
```

Output:

```text
[]
```

Before the fix, I also ran:

```bash
python -m pytest tests/unit/test_resume_parser.py -v
```

Output:

```text
5 passed, 5 xfailed
```

### After

I re-ran the same reproduction against the built change:

```python
from ingestion.parsers.resume_parser import ResumeParser

r = ResumeParser()

res = r.parse("""
    John Smith
    john@example.com

    Education:
    - B.S. Computer Science

    Skills: Python
""")

print(res.metadata["detected_sections"])
```

Output:

```text
['Education', 'Skills']
```

I then ran:

```bash
python -m pytest tests/unit/test_resume_parser.py -v
```

Output:

```text
10 passed in 1.25s
```

## Eval iterations

**Run history**

My eval runs, in order:

1. Partial smoke run (`--limit 3`): `agreement: 3/3 scored items`
2. Full run: `agreement: 18/20 scored items (bar: 18/20: PASS)`
3. Partial targeted run (`--only pkg-02,pkg-14,pkg-01,pkg-10`): `agreement: 3/4 scored items`
4. Partial targeted run (`--only pkg-14`): `agreement: 0/1 scored items`
5. Final full run: `agreement: 19/20 scored items (bar: 18/20: PASS)`

The final run matched 19 of 20 scored packages and had matches in every category.

Package analysis
Package: pkg-14
Gold label: accept
My rubric verdict: reject
The deciding check was diagnosis-supported. My rubric read the plan's diagnosis too strictly. The package said that on reattach, Zellij wires client input to the session before OSC color-query responses are consumed. The reproduction supported the important observations—fresh attach was clean, reattach leaked the responses, version 0.44.1 was clean, and clearing the cache temporarily changed the behavior—but it did not directly prove the exact internal ordering mechanism.
My diagnosis-supported check required the proposed cause to be supported by the reproduced evidence and not claim a cause the reproduction did not establish. Because the plan stated the internal mechanism as fact rather than uncertainty, the rubric rejected it. The gold label accepted the package, so this remained the one disagreement in my final 19/20 run.
Check rationale
The check I chose is:
diagnosis-supported | The plan's stated diagnosis/cause read against the issue description and Repro evidence, including the reproduced behavior and artifacts | The proposed cause is consistent with and supported by the reproduced evidence. It does not contradict the evidence or claim a cause the reproduction does not establish. | required

I kept this check because I wanted the rubric to distinguish between a diagnosis that follows from reproduction evidence and one that merely sounds plausible. During evaluation, pkg-14 showed the trade-off in that wording: the observed behavior strongly suggested the proposed mechanism, but the reproduction did not directly establish the internal ordering the plan claimed. I chose to keep the requirement that a diagnosis not present an unestablished cause as fact rather than loosening the check just to turn that package into an accept.
Trade-offs
The main trade-off is that diagnosis-supported can reject a reasonable plan when the reproduction strongly supports a hypothesis but cannot directly prove the internal mechanism. pkg-14 demonstrates this: the gold label is accept, while my rubric returns reject because the plan states the reattach/OSC ordering mechanism more confidently than the reproduction establishes.
I accepted that false-negative risk because loosening the check could also allow wrong-cause plans to pass when they fit the symptoms but are not grounded in the available evidence. My final run still matched all four wrong-cause packages and finished at 19/20 overall, so I kept the stricter evidence requirement.

Related paths: plan.md and eval-run.txt in this directory; your skill's files in tools/plan-check/.
