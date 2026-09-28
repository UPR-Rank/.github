# UPR-Rank

Competitive programming tooling. Everything here began as a fork of
[Matcom Online Grader (MOG)](https://github.com/MatcomOnlineGrader/judge), the
judge that runs the ICPC Caribbean Finals.

The forks exist so the pieces a judge depends on can be built and changed from
our own side. A competition cannot wait on somebody else's uptime to compile a
submission.

## The repositories

### [judge](https://github.com/UPR-Rank/judge) — the online judge

The judge itself: a Django web application for contests, problems,
submissions and standings, plus the grader that compiles a submission, runs it
against every test case in a sandbox, and records a verdict with the time and
memory it used.

This is where the active work is. The judge is being modernized in sprints,
each on its own branch:

| | |
| --- | --- |
| 0 — Independence | Done. `safeexec` built from our fork, baseline tests |
| 1 — Judge modularization | Done. A 532-line command split into a `judging` package |
| 2 — Queue | Done. Grading moved to Celery workers on Redis, with a reaper |
| 3 — Shared cache | Next |

The judge is MIT licensed and its [README](https://github.com/UPR-Rank/judge)
covers how grading works and how the sandbox isolates submissions.

### [safeexec](https://github.com/UPR-Rank/safeexec) — the sandbox

The wrapper that actually runs a submission. It is setuid-root, drops
privileges into an unprivileged user, applies the time, memory and process
limits, and reports back what happened. The judge's verdict table is built
around the outcomes it prints.

This is the fork that unblocks a build: the grader image builds `safeexec`
from here instead of cloning upstream.

### [testlib](https://github.com/UPR-Rank/testlib) — the checker libraries

A judge problem ships a *checker*: a small program that decides whether one
test case's output is correct. `testlib` is the standard toolkit for writing
those, and the judge ships the headers from this fork
(`testlib.h`, `testlib4j.jar`). MIT licensed, by Mike Mirzayanov.

### [gcc-11.3.0](https://github.com/UPR-Rank/gcc-11.3.0) — the compiler toolchain

A pinned gcc build for the grader image, so submissions are compiled the same
way on every machine and every contest.

**Not wired up yet.** The judge still downloads the prebuilt tarball from
upstream, because this fork has no published release to point at. That is the
remaining dependency on somebody else's uptime.

### [runexe](https://github.com/UPR-Rank/runexe) — unused

A fork of the old Google Code `runexe`, which launched a program under
Windows. Nothing in the judge references it: MOG's grader runs on Linux and
uses `safeexec`. It is here because the fork was taken for completeness, and
it would be better deleted than left unexplained.

## Licensing

[`judge`](https://github.com/UPR-Rank/judge) and
[`testlib`](https://github.com/UPR-Rank/testlib) are MIT. `safeexec`, `runexe`
and `gcc-11.3.0` carry no license file in this organization, so treat them as
covered by whatever their upstreams grant and check before redistributing.
