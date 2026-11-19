# Product backlog · CLARIAH Resource Builder

Project P4 · Software Project · Master HAP/LAP · EHU · 2026-27 · **Team 2**
Written by: Garazi Garrido · Review: Olga (pending) · Approval and order: Ali Faraz (PO, pending) ·
Issues: Garazi Garrido · Last update: 19 November 2026

> Each story is a GitHub issue with the label `story` and the label of its epic (`E1`, `E2`, `E3`).
> Every story is traced to a requirement confirmed by Jon in **Meeting 5** (`CR-nn` in
> [`docs/client/client-interviews.pdf`](../client/client-interviews.pdf)), also listed in the
> [product vision](../product/vision.md) §5. The use cases are in the
> [requirements](../requirements/requirements.md) §4.
>
> The requirements confirmed in Meeting 4 were withdrawn in Meeting 5 when the scope of V1 changed.
> This backlog replaces the version of 17 November 2026 (see the change log).

**Priority:** must · should · could · **Points:** 1, 2, 3, 5, 8

## Epics

One epic per sprint. Each epic ends with a demo that runs from start to finish.

| ID | Epic | Description | Stories |
|---|---|---|---|
| E1 | **One file end to end (CLI)** | Submit one CSV or JSONL file, keep the original untouched, check its format, report every issue, log every action and package the results in a ZIP, all from the command line. | US-01 to US-07 |
| E2 | **Agreement between two annotation files** | Submit two annotation files of the same items, compute their percentage agreement with per-label detail, and refuse files that cannot be compared. | US-08, US-09, US-10 |
| E3 | **Better agreement measures and web interface** | Add a chance-corrected agreement measure and a web interface that reuses the same core as the CLI. | US-11, US-12 |

## Backlog

Order set by the Product Owner. *Issue* = number of the GitHub issue. *Sprint* = GitHub milestone.

| ID | Story | Epic | Source | Use case | Priority | Points | Sprint | Issue |
|---|---|---|---|---|---|---|---|---|
| US-01 | Submit one resource | E1 | CR-01 (one file), CR-03 | UC1 | must | 3 | 1 | #16 |
| US-02 | Keep the original untouched | E1 | CR-02 | UC1 | must | 3 | 1 | #17 |
| US-03 | Check the format of a resource | E1 | CR-04 | UC2 | must | 5 | 1 | #18 |
| US-04 | Format check report | E1 | CR-05 | UC2 | must | 3 | 1 | #19 |
| US-05 | Log every action | E1 | CR-08 | UC1–UC4 | must | 2 | 1 | #20 |
| US-06 | Package the results in a ZIP | E1 | CR-09 | UC4 | must | 3 | 1 | #21 |
| US-07 | Run every step from the command line | E1 | CR-10 | UC1–UC4 | must | 3 | 1 | #22 |
| US-08 | Submit two annotation files | E2 | CR-01 (two files) | UC1 | must | 2 | 2 | #23 |
| US-09 | Percentage agreement between two annotation files | E2 | CR-06 | UC3 | must | 5 | 2 | #24 |
| US-10 | Refuse files that cannot be compared | E2 | CR-07 | UC3 | must | 3 | 2 | #25 |
| US-11 | Chance-corrected agreement | E3 | CR-11 | UC3 | should | 3 | 3 | #26 |
| US-12 | Web interface for the same steps | E3 | CR-12 | UC1–UC4 | could | 8 | 3 | #27 |

**Total:** 12 stories · 43 points (E1: 22 · E2: 10 · E3: 11). Points are a first estimate, to be voted by the team.

Supporting work (label `task`, no direct user value):

| ID | Task | Sprint | Issue |
|---|---|---|---|
| T-01 | Prepare sample and test data | 1 | #28 |
| T-02 | Project set-up: core module, CLI skeleton and tests | 1 | #29 |

## Stories and acceptance criteria

### E1 · One file end to end (CLI)

#### US-01 · Submit one resource

As a data steward, I want to submit one CSV or JSONL file from the command line, so that the resource is registered with an id and its metadata without me typing anything in.

Source: CR-01 (one file), CR-03 · Use case: UC1 · Priority: must · Points: 3

- Given a valid CSV or JSONL file, when I run `submit <file>`, then the tool prints a new resource id and stores a metadata record with name, format, size, SHA-256 checksum, submission date and submitter, all taken from the file and the run.
- Given a file that is not CSV or JSONL (e.g. `.xlsx`) or a path that does not exist, when I run `submit <file>`, then I see a clear error message, nothing is stored and no id is created.

#### US-02 · Keep the original untouched

As a data steward, I want the submitted file to stay unchanged byte for byte, with a SHA-256 checksum taken at submission, so that I can prove that no step of the tool modified the original.

Source: CR-02 · Use case: UC1 · Priority: must · Points: 3

- Given a submitted resource, when the format check and the packaging have run, then the SHA-256 of the stored original is identical to the one recorded at submission, and the stored copy is read-only.
- Given a stored original whose bytes were changed outside the tool, when any later step runs on it, then the tool stops and reports that the checksum no longer matches.

#### US-03 · Check the format of a resource

As a data steward, I want the tool to check the structure, column names, missing values and inconsistent labels of a submitted file, so that I no longer have to check each file by hand.

Source: CR-04 · Use case: UC2 · Priority: must · Points: 5

- Given a submitted CSV or JSONL file that has a missing value, an unexpected column name and a label written in two ways (e.g. `Positive` / `positive`), when I run `check <id>`, then the tool finds all three issues.
- Given a file that cannot be parsed (e.g. a broken JSONL line or rows with a different number of columns), when I run `check <id>`, then the tool reports a structure issue instead of crashing.

#### US-04 · Format check report

As a data steward or researcher, I want the format check to return either "OK, no issues" or a report that gives the file, row or line, column or field and type of every issue, so that we can quickly identify and fix each issue.

Source: CR-05 · Use case: UC2 · Priority: must · Points: 3

- Given a file with no issues, when the format check finishes, then the tool prints "OK, no issues".
- Given a file with issues, when the format check finishes, then the report lists each issue with file, row or line, column or field and issue type, and the tool does not go on to the agreement step; the report goes into the ZIP package.

#### US-05 · Log every action

As a data steward, I want every action of the tool to be logged as a separate entry, so that every result can be traced back to who produced it, when, with which tool version and from which input.

Source: CR-08 · Use case: UC1–UC4 · Priority: must · Points: 2

- Given a resource that was submitted, checked and packaged, when I open its log, then there is one entry per action with date and time, user, tool version, input file with its checksum and output file.
- Given a step that fails (e.g. a file that cannot be parsed), when I open the log, then the failed action is also recorded, with its error, and no entry has empty or invented fields.

#### US-06 · Package the results in a ZIP

As a data steward, I want one ZIP package with the report, the metadata of the files and the log, so that I no longer assemble the package by hand at the end.

Source: CR-09 · Use case: UC4 · Priority: must · Points: 3

- Given a resource that passed or failed the format check, when I run `package <id>`, then I get one ZIP with the report, the metadata and the log, and the original is copied or referenced with the same SHA-256 as at submission.
- Given a resource id that does not exist or has not been checked yet, when I run `package <id>`, then I see a clear message and no ZIP is created.

#### US-07 · Run every step from the command line

As a data steward, I want to run every step from the command line, so that I can use the tool the way I already check files today.

Source: CR-10 · Use case: UC1–UC4 · Priority: must · Points: 3

- Given the tool is installed, when I run `submit`, `check` and `package` (and `run <file>` for the three in a row), then each command works on its own and prints where its output was saved.
- Given a command with a missing or unknown argument, when I run it, then I see a usage message with the correct syntax and the exit code is not 0.

### E2 · Agreement between two annotation files

#### US-08 · Submit two annotation files

As a data steward, I want to submit two annotation files of the same items together, so that the tool can compare them.

Source: CR-01 (two files) · Use case: UC1 · Priority: must · Points: 2

- Given two CSV or JSONL files, when I run `submit <file1> <file2>`, then each file gets its own id, metadata, checksum and log entry, both are linked as one pair, and both go through the format check.
- Given only one file or more than two files, when I run the two-file command, then I see a message saying that exactly two files are needed.

#### US-09 · Percentage agreement between two annotation files

As a data steward, I want the overall agreement of two annotation files of the same items as a percentage, with the detail per label, so that I know whether the labels of a resource are reliable before accepting it.

Source: CR-06 · Use case: UC3 · Priority: must · Points: 5

- Given two valid files of the same 100 items that give the same label to 85 of them, when I run `agree <id1> <id2>`, then the tool reports 85% overall agreement and the agreement for each label, and adds them to the ZIP report with the files' metadata.
- Given items matched by a shared ID column, or by row order when there is none, when the rows of one file are in a different order, then the result is the same as with the rows in the same order (ID column case) and the report says which matching was used.

#### US-10 · Refuse files that cannot be compared

As a data steward, I want files that cannot be compared to be refused with a clear message, so that I never get a misleading agreement score.

Source: CR-07 · Use case: UC3 · Priority: must · Points: 3

- Given two files with a different number of records, or with IDs that do not match, when I run `agree <id1> <id2>`, then no score is computed and the message says what differs (e.g. "file A has 100 records, file B has 98; 2 IDs only in A").
- Given a pair where one file has format issues, when I run `agree <id1> <id2>`, then no score is computed and I am pointed to that file's format report.

### E3 · Better agreement measures and web interface

#### US-11 · Chance-corrected agreement

As a data steward, I want a chance-corrected agreement measure in addition to the percentage, so that a high score is not misleading when one label dominates.

Source: CR-11 · Use case: UC3 · Priority: should · Points: 3

- Given two valid annotation files, when I run `agree <id1> <id2>`, then the report shows the percentage and Cohen's kappa, and the kappa matches a reference implementation (e.g. scikit-learn `cohen_kappa_score`) to three decimals.
- Given two files where every item has the same single label, when I run `agree`, then the tool does not divide by zero and explains that kappa is undefined for this pair.

#### US-12 · Web interface for the same steps

As a data steward or researcher, I want a web interface with the same steps as the command line, so that I can use the tool from a browser.

Source: CR-12 · Use case: UC1–UC4 · Priority: could · Points: 8

- Given the web interface is running, when I upload one file, or two annotation files, and start the process, then I see the format check result, the agreement when there are two files, and I can download the same ZIP the CLI produces.
- Given I upload a file that is not CSV or JSONL, when I start the process, then I see the same clear error message as in the CLI and nothing is stored.

## Open points that affect the backlog

To settle with Jon or the team before the story is planned (Meeting 5, open points):

- **US-03:** the fixed list of issue types (duplicate IDs, encoding, data types?) and which issues stop the process.
- **US-09, US-10:** what counts as "different items" when matching by ID column or by row order.
- **US-11:** Cohen's kappa (two annotators) or Krippendorff's alpha.
- **US-04, US-06:** the report format inside the ZIP (JSON, web page, PDF or several).
- **US-01:** a documented size limit for input files (typical files: a few MB to 200 MB).

## Out of scope (future versions)

Withdrawn in Meeting 5 together with the Meeting 4 requirements, and kept as candidates: metadata forms (Dublin Core), licences and access categories, automatic corrections, steward approval before export, comparison between reports, report languages, upload to the CLARIAH repository.

## Change log

| Date | Change | By |
|---|---|---|
| 17 November 2026 | Backlog created: 12 stories in 5 epics, one per confirmed requirement CR-01 to CR-12 | Team 2 |
| 19 November 2026 | Backlog rewritten for the new scope confirmed in Meeting 5: the Meeting 4 requirements and their 12 stories are withdrawn; 12 new stories from the new CR-01 to CR-12 in 3 epics (one per sprint), 2 supporting tasks, issues #16 to #29 | Garazi Garrido |
