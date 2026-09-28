<div align="center">
  <img src="images/logo.png" alt="UPR-Rank" width="360">
  <h1>UPR-Rank</h1>
  <p><strong>Online judge for the Universidad de Pinar del Río</strong><br>
  Competitive programming practice, grading and evaluation.</p>
  <p>
    <img alt="Django" src="https://img.shields.io/badge/Django-5.2-092E20?logo=django&logoColor=white">
    <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-16-4169E1?logo=postgresql&logoColor=white">
    <img alt="Celery" src="https://img.shields.io/badge/Celery-5.6-37814A?logo=celery&logoColor=white">
    <img alt="Redis" src="https://img.shields.io/badge/Redis-7-DC382D?logo=redis&logoColor=white">
    <img alt="License" src="https://img.shields.io/badge/license-MIT-8A8A8A">
  </p>
</div>

---

## Repositories

| Repository | What it is |
| --- | --- |
| [judge](https://github.com/UPR-Rank/judge) | The online judge: a Django site for contests, problems and submissions, plus the grader that compiles and runs each submission in a sandbox and records its verdict. |
| [safeexec](https://github.com/UPR-Rank/safeexec) | The sandbox that runs a submission under time, memory and process limits, as an unprivileged user. |
| [testlib](https://github.com/UPR-Rank/testlib) | Libraries for writing the checkers that decide whether a submission's output for a test case is correct. |
| [gcc-11.3.0](https://github.com/UPR-Rank/gcc-11.3.0) | A pinned gcc build used by the grader image to compile submissions the same way everywhere. |
| [runexe](https://github.com/UPR-Rank/runexe) | An old Windows program launcher. Unused: the judge runs on Linux and uses `safeexec`. |

## How a submission is graded

```mermaid
flowchart LR
    A["Student<br/>submits code"] --> B["judge<br/>Django web app"]
    B --> C[("PostgreSQL<br/>submission stored")]
    B -->|"queued"| D["Redis<br/>task queue"]
    D --> E["Celery worker<br/>grader"]
    E --> F["safeexec<br/>sandbox<br/>time, memory, processes"]
    E --> G[("PostgreSQL<br/>verdict recorded")]
```

Each submission is stored in PostgreSQL and handed to a background worker through a
Redis queue. The worker compiles and runs the code inside the `safeexec` sandbox,
compares the output with the expected answer using the checkers in `testlib`, and
writes the verdict back to the database.

---

<div align="center">
  <em>En honor a Ali Landeiro Gongora.</em>
</div>
