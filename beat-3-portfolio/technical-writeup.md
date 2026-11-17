\# Building an AI Issue Scout for Open-Source Contributions



\## Overview

Finding the right issue from a large pool of issues on GitHub can be challenging. To address this challenge, I built an Issue Scouter as a Claude Code skill to search for Python and TypeScript based issues and with labels such as "good first issue." I also developed an evaluation rubric to assess issues based on maintainer activity, availability, and scope feasibility. I used the scouter to evaluate the Flutter Probe issue #404, which I found through CodePath. The issue involved testing how recorded user interactions are converted into ProbeScript commands. I added 15 table-driven test cases and parser integration tests, then opened PR #534. After addressing maintainer feedback, the PR remains open and awaiting further review. \[PR #534](https://github.com/AlphaWaveSystems/flutter-probe/pull/534)



\## What happened



First, I configured the Issue Scouter with my programming experience, preferred programming languages, and project interests. I designed three search queries to return open-source issues from GitHub. The scouter filtered out irrelevant issues and ranked the remaining ones based on their labels, number of comments, and recent activity. The highest-ranked issues were then evaluated against a custom rubric made up of required and preferred checks to determine whether they should be accepted or rejected.



On October 28, 2026, I ran the scouter for the first time, which returned the following results:



```text

I ran the scan: 300 search results, 260 left after ranking, and 5 graded.

4 accepted, 1 rejected. All five candidates come from just two repos,

and every one was opened today, about 1–2 hours before the scan.

```



Although the scouter found relevant issues, the results lacked diversity. All five evaluated issues came from only two repositories. I also noticed that ranking issues based on the fewest comments favored recently created issues. To address these problems, I updated the search strategy to limit the number of candidates selected from a single repository and emphasized checking for existing pull requests before accepting an issue.



On October 30, I individually evaluated two issues using the scouter. Flutter Probe #404 was accepted, while Red Discord Bot #6794 was rejected because four open pull requests were already addressing the issue. This showed that an issue could be open and unassigned but still be actively worked on by other contributors.



On November 6, I refined the evaluation rubric by changing the preferred `scope-fits` check to a required `scope-feasible` check. The original check favored beginner-friendly issues, potentially overlooking more challenging but achievable contributions. I also introduced three difficulty ratings that described the complexity of an issue without affecting its acceptance or rejection.



After updating the rubric, I regraded both issues and received the following results:



| Evaluation | Flutter Probe #404 | Red Discord Bot #6794 |

|---|---|---|

| Scope feasible | PASS | PASS |

| Unclaimed | PASS | FAIL |

| Verdict | ACCEPT | REJECT |



I chose Flutter Probe #404 and began investigating the repository's implementation and existing test coverage. During this process, I discovered that some of the test scenarios requested in the original issue had already been implemented by other contributors, so I narrowed the scope of my contribution to the remaining gaps, including selector combinations, special-character handling, fallback behavior, and parser compatibility.



I added 15 table-driven test cases to `studio/recorder\_test.go` and created `studio/recorder\_parser\_test.go` to test the compatibility between the recorder and the ProbeScript parser. The following code is an excerpt from my parser integration tests:



```go

line := eventToProbeScriptLine(tc.params)

script := "test \\"recorded action\\"\\n" + line + "\\n"



prog, err := parser.ParseFile(script)

if err != nil {

&#x20;   t.Fatalf("failed to parse %q: %v", line, err)

}

```



Instead of only comparing the generated commands against expected strings, this test passes the commands directly to the ProbeScript parser to verify that they can be parsed successfully. I also added a negative test to verify that malformed ProbeScript is rejected. These changes expanded the existing test coverage without modifying production code.



To validate my contribution, I ran focused Go tests, Go build and vet checks, and the frontend build, all of which passed locally. However, I encountered failures when running the full Go test suites in my Windows environment. I documented these limitations in my contribution report.



On November 10, I used Claude Code's ship-gate to validate my contribution. After resolving documentation inconsistencies and Windows compatibility issues, the contribution passed all six required ship-gate checks, and I opened \[PR #534](https://github.com/AlphaWaveSystems/flutter-probe/pull/534).



On November 16, I got feedback from a Flutter Probe maintainer explaining that PR #706 had changed how the recorder handled action names containing newlines. One of my tests expected the old multiline output, but the updated implementation produced a single-line comment. I rebased my branch on the latest main branch, resolved a CHANGELOG conflict, and updated the test expectation. I reran all six local validation checks successfully, pushed the changes, and responded to the maintainer.



I also completed the Contributor License Agreement process, and the CLA Assistant check passed. 



\## Limitations and what's next



One limitation of my Issue Scouter was the lack of diversity in its initial search results. Although I updated the search strategy to limit candidates from the same repository, I did not run another full scan to confirm whether this improved the results. I would also like to improve how the scouter detects issues that already have active pull requests.



My Flutter Probe contribution also had testing limitations. The focused recorder tests and required local validation checks passed, but the full Go test suites encountered failures in my Windows environment. Also, the parser integration tests cover selected scenarios rather than every possible recorder-generated command.



My next step is to monitor PR #534 for further maintainer feedback and address any requested changes. The CLA check has passed, but the pull request has not been merged. In the future, I would check for recent upstream changes earlier and investigate contributor requirements before submitting a pull request.

