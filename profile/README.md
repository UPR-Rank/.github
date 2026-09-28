# UPR-Rank

Competitive programming tooling, forked from
[Matcom Online Grader (MOG)](https://github.com/MatcomOnlineGrader/judge).

| Repository | What it is |
| --- | --- |
| [judge](https://github.com/UPR-Rank/judge) | The online judge: a Django site for contests, problems and submissions, plus the grader that compiles and runs each submission in a sandbox and records its verdict. |
| [safeexec](https://github.com/UPR-Rank/safeexec) | The sandbox that runs a submission under time, memory and process limits, as an unprivileged user. |
| [testlib](https://github.com/UPR-Rank/testlib) | Libraries for writing the checkers that decide whether a submission's output for a test case is correct. |
| [gcc-11.3.0](https://github.com/UPR-Rank/gcc-11.3.0) | A pinned gcc build used by the grader image to compile submissions the same way everywhere. |
| [runexe](https://github.com/UPR-Rank/runexe) | An old Windows program launcher. Unused: the judge runs on Linux and uses `safeexec`. |
