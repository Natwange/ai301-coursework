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

## Your branch

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

**Package analysis**

Package: `pkg-14`

Gold label: `accept`

My rubric verdict: `reject`

The deciding check was `diagnosis-supported`. My rubric read the plan's diagnosis strictly because the package stated that on reattach, Zellij wires the client's input to the session before OSC color-query responses have been consumed. The reproduction established that fresh attaches were clean, reattaches leaked the responses, version 0.44.1 was clean, and clearing the cache temporarily changed the behavior. However, it did not directly establish the exact internal ordering mechanism.

My `diagnosis-supported` check requires the proposed cause to be supported by the reproduced evidence and not claim a cause that the reproduction does not establish. Because the plan stated that internal mechanism as fact rather than as
