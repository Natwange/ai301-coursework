# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

## Your identity upstream

**GitHub username**

Natwange

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54#issuecomment-5901594707

I'd like to investigate this issue. I'll test the reported leading-whitespace behavior in resume section detection and post a reproduction report with my environment, steps, and results.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54#issuecomment-5902651839

I was able to reproduce the leading-whitespace issue in resume section detection.

### Environment

- OS: Windows
- Python: 3.12.6
- PathReview commit: `f89c06fc3ff292df2a04a39ac51319d32a76b779`
- Test runner: pytest 9.1.1

### Steps to reproduce

I created a `ResumeParser` and parsed resume text where the section headings had leading whitespace:

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

### Observed behavior

The output was:

```text
[]
```

Even though the input contains the `Education:` and `Skills:` section headings, neither section was detected.

I also ran:

```bash
python -m pytest tests/unit/test_resume_parser.py -v
```

The test run completed with:

```text
5 passed, 5 xfailed
```

The issue-related tests `test_parse_single_column_resume_text`, `test_parse_resume_no_work_experience`, and `test_detect_sections` were all reported as `XFAIL`.

This reproduces the behavior described in #54: section headings with leading whitespace are not detected.

## Eval iterations

**Run history**

20/20 scored items (bar: 18/20: PASS)

**Package analysis**

`pkg-01` — My rubric decided `accept`, and the gold label was also `accept`. The reproduction report recorded its environment and gave commands that another contributor could run. More importantly, its output directly matched the issue: when exactly one custom header was present, `Content-Type: application/json` was missing. The control run showed that the header appeared correctly without the custom header. Because the evidence supported the stated reproduction and the required checks passed, my rubric returned `accept`.

**Check rationale**

> `| behavior-matches | Repro report's observed output, logs, screenshots, or other artifacts read against the specific behavior described in the issue | The evidence demonstrates the behavior described by the issue, or the report clearly states that the behavior was not reproduced. Evidence of a different or merely adjacent failure does not count as reproducing the issue. | required |`

I made this check required because showing an error is not enough to prove that the specific issue was reproduced. The evidence has to match the behavior described by the issue. I also allowed an honestly documented cannot-reproduce result to pass because the goal is accurate evidence, not forcing every investigation to reproduce the bug.

**Trade-offs**

This check is deliberately strict about matching the issue's specific behavior, so it can reject a report that finds a real problem if that problem is only adjacent to the one described in the issue. I accept that trade-off because a different failure should be investigated separately rather than presented as proof that the original issue was reproduced.

---

Related paths: `eval-run.txt` in this directory; your skill's files in `tools/repro-check/`.