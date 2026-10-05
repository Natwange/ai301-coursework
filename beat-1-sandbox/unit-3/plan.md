# Plan for Issue #54

## Diagnosis

The reproduction showed that resume section headings with leading whitespace are not detected. For example, when the input contained:

    Education:
    Skills: Python

`detected_sections` returned `[]`.

The issue is in `_detect_sections()` in `ingestion/parsers/resume_parser.py`. The regular-expression patterns expect the section name to appear immediately at the beginning of a line or immediately after a newline. They allow whitespace after the section name, but not before it. As a result, indented headings such as `    Education:` do not match the patterns and are never added to the `detected` list.

## Scope

### In scope

- Update the section-detection logic in `ingestion/parsers/resume_parser.py` so recognized resume headings can have leading whitespace.
- Verify the change using the existing section-detection tests and the reproduction from issue #54.
- Add or adjust a regression test if necessary to explicitly preserve the leading-whitespace behavior.

### Out of scope

- Changing which section names are included in `SECTION_HEADERS`.
- Redesigning the resume parser or Markdown parsing logic.
- Fixing unrelated failing or xfailed tests that are not caused by leading whitespace in section headings.

## Files

- `ingestion/parsers/resume_parser.py` — update the section-heading detection patterns.
- `tests/unit/test_resume_parser.py` — verify the fix with the existing issue #54 tests and add or adjust a regression test if needed.

## Approach

Update `_detect_sections()` so its regular-expression patterns allow optional whitespace before recognized section headings.

The change will preserve the existing behavior for headings without indentation while also allowing headings such as `    Education:` and `    Skills: Python` to be detected.

Keep the change limited to section detection rather than stripping indentation from the entire resume text, since the problem is specifically how `_detect_sections()` matches headings.

## Test Plan

1. Re-run the Unit 2 reproduction using indented `Education:` and `Skills:` headings.
   - Before the fix, `detected_sections` returned `[]`.
   - After the fix, expect `Education` and `Skills` to appear in `detected_sections`.

2. Run:

   `python -m pytest tests/unit/test_resume_parser.py -v`

   Confirm that the tests related to leading-whitespace section detection now pass rather than xfail.

3. Verify that headings without leading whitespace are still detected, so the fix does not break the existing behavior.

## Risks and Unknowns

- Allowing leading whitespace must not make ordinary resume text look like section headings when it is not.
- Some tests currently marked `xfail` for issue #54 may fail for reasons unrelated to section detection. Those failures will be investigated separately rather than automatically included in this fix.
- The exact regression-test changes will depend on which existing tests pass after the section-detection fix.

## Deviations

The implementation expanded slightly from the original plan. After fixing leading-whitespace handling in `_detect_sections()`, three of the five issue #54 tests passed, but two Markdown-related tests remained xfailed. Further investigation showed that `_strip_markdown()` had the same leading-whitespace problem: its Markdown header pattern expected `#` immediately at the beginning of a line.

I updated the Markdown header pattern to allow leading whitespace and removed the remaining obsolete issue #54 `xfail` markers. After these changes, all 10 tests in `tests/unit/test_resume_parser.py` pass.
