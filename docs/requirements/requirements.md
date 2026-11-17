# Requirements · CLARIAH Resource Builder

Project P4 · Software Project · Master HAP/LAP · EHU · 2026-27 · **Team 2**
Written by: Garazi Garrido · Reviewed by: Olga · Approved by: Ali Faraz (PO)
Status: **draft v2** · Last update: 17 November 2026

> Every requirement points to its source: the project brief (`Brief`) or a requirement confirmed
> by the client (`CR-nn`). The confirmed requirements CR-01 to CR-12 and the additional V1
> decisions are listed in the [product vision](../product/vision.md) §5 and recorded in
> [`docs/client/`](../client/). Items marked **to confirm** still need a decision.
>
> AI use: drafted with the help of an AI assistant (Claude) and reviewed by the team.

## Contents

1. [Purpose and scope](#1-purpose-and-scope)
2. [Glossary](#2-glossary)
3. [Stakeholders](#3-stakeholders)
4. [Use cases](#4-use-cases)
5. [User stories](#5-user-stories)
6. [Constraints](#6-constraints)
7. [Open questions for Jon](#7-open-questions-for-jon)

---

## 1. Purpose and scope

The CLARIAH Resource Builder helps a data steward of CLARIAH-EUS turn an imperfect linguistic
resource into a clean, validated and documented package. The steward submits a resource (CSV or
JSONL), receives an actionable validation report, supplies the metadata that cannot be inferred,
applies controlled fixes, approves the result and exports a reproducible ZIP package. The original
file is never modified.

**In scope (V1)**

- Submission of resources in **CSV and JSONL** (CR-01).
- Automatic checks of structure, missing values, duplicate IDs, encoding, data types and language
  codes (CR-03).
- Reports that classify each finding as error, warning or missing decision, in **JSON**, **web
  page** and **PDF**, and comparison with the previous report (CR-04 to CR-07).
- Collection of mandatory **Dublin Core** metadata and of the licence, chosen from an approved list
  (CR-08, CR-09).
- Preservation of the original byte for byte with a checksum; safe fixes as logged revisions
  (CR-02, CR-10).
- Export of a **ZIP** package after explicit approval by the data steward (CR-11, CR-12).

**Out of scope (V1)** (Brief · product vision §6)

- Uploading packages to the CLARIAH repository or any other repository (CLARIN, Zenodo…).
- FAIR certification.
- Automatic licence detection or legal advice.
- A universal validator for every format or metadata schema.
- Very large files (up to 1 GB): the prototype documents a size limit instead.
- A full web application with five user roles, permissions and e-mail notifications.
- Excel files and ZIP archives as **input** (ZIP is only an export format).
- Training, workshops and community channels.
- Mandatory use of GPU or of an LLM.

## 2. Glossary

| Term | Meaning in this project |
|---|---|
| **Resource** | A linguistic dataset in CSV or JSONL submitted for preparation |
| **Original** | The file exactly as submitted. It is preserved byte for byte and verified with a checksum |
| **Checksum** | A fingerprint of a file (for example SHA-256). The same file always gives the same checksum |
| **Revision** | A new version of the resource produced by one fix. Each revision is logged |
| **Finding** | One problem found by the validation, with file, row, field, found value and expected value |
| **Error** | A finding that blocks acceptance (for example a duplicate ID or a missing required field) |
| **Warning** | An unusual but valid value that the steward should look at |
| **Missing decision** | Information only a person can provide (for example the licence). It is neither an error nor a warning |
| **Safe fix** | A formatting fix that cannot change the meaning (for example encoding or whitespace). It can be applied by the tool as a revision |
| **Metadata** | Descriptive information in Dublin Core: title, language code, producer, description, licence… |
| **Access category** | CLARIAH repository category derived from the licence: `PUB` (CC0), `ACA` (CC-BY), `RES` (CC-BY-SA) |
| **Approval** | The explicit decision of the data steward, after final quality control, that a package can be exported |
| **Package** | The ZIP export: data, metadata, README, licence, reports and revision history, named by resource and version |
| **History** | The ordered log of every action and revision applied to the resource |

## 3. Stakeholders

| Stakeholder | Interest | How they use the tool |
|---|---|---|
| **Data steward** (Jon, our client) | Validate resources predictably and produce a package he can trust | Main user: submits, validates, completes metadata, fixes, approves, exports |
| **Researcher** (resource provider) | Get the resource accepted without long e-mail exchanges | Receives the human-readable report (web or PDF) and fixes their own file |
| **Package consumer** (CLARIAH-EUS, future users) | Find, understand and reuse the resource legally | Receives the package; relies on metadata, licence and history |
| **Teaching team** | Assess the process and the product | Reviews the repository, the documents and the demonstration |

## 4. Use cases

### UC-1 · Validate a resource and get an actionable report

| | |
|---|---|
| **Primary actor** | Data steward |
| **Goal** | Know exactly what is wrong with a resource, and where, so that it can be fixed |
| **Source** | Brief · CR-01, CR-02, CR-03, CR-04, CR-05, CR-06 |
| **Preconditions** | The steward has a CSV or JSONL file within the documented size limit |
| **Postconditions** | The original is stored unchanged with its checksum; a validation report is available |

**Main flow**

1. The steward submits a CSV or JSONL file.
2. The system stores the original and records its checksum.
3. The system checks structure, missing values, duplicate IDs, encoding, data types and language
   codes.
4. The system shows a report with the number of findings of each severity and, for each finding:
   its type (error, warning or missing decision), the file, the row, the field, the found value and
   the expected value.
5. The steward downloads the report as JSON, as a web page or as a PDF to send it to the researcher.

**Alternative flows**

- 2a. The format is not CSV or JSONL (for example Excel or a ZIP archive) or the file exceeds the
  size limit → the system rejects it and says why.
- 4a. No problems are found → the report says so explicitly and lists only the missing decisions,
  if any.

### UC-2 · Compare a report with the previous one

| | |
|---|---|
| **Primary actor** | Data steward |
| **Goal** | See what the researcher (or a fix) has solved since the last validation |
| **Source** | CR-07 |
| **Preconditions** | The resource has been validated at least twice (UC-1) |
| **Postconditions** | The steward sees the findings grouped as fixed, still open and new |

**Main flow**

1. The steward chooses a report and the previous one.
2. The system compares the findings.
3. The system shows three groups: **fixed**, **still open** and **new**, with the counts of each.

### UC-3 · Complete the metadata that cannot be inferred

| | |
|---|---|
| **Primary actor** | Data steward |
| **Goal** | Provide the information that only a person can decide, such as the licence |
| **Source** | CR-08, CR-09 · Dublin Core (V1 decision) |
| **Preconditions** | The resource has been validated (UC-1) |
| **Postconditions** | All mandatory metadata fields are filled; the missing decisions are resolved |

**Main flow**

1. The system lists the mandatory Dublin Core fields that are still empty: title, language code,
   producer, description and licence.
2. The steward fills each field. The licence is chosen from the approved list (CC0 1.0, CC-BY 4.0,
   CC-BY-SA 4.0).
3. The system checks each value (format, allowed values) and saves it. From the licence it shows
   the CLARIAH access category (`PUB`, `ACA` or `RES`).
4. The system updates the report: resolved missing decisions disappear.

**Alternative flows**

- 2a. The licence the steward needs is not in the approved list → the system does not allow free
  text; the missing decision stays open and the package cannot be exported. The list can be edited
  by the steward in the configuration.
- 3a. A value is invalid (for example a language code that is not valid) → the system explains what
  is expected and keeps the field empty.

### UC-4 · Apply a safe fix

| | |
|---|---|
| **Primary actor** | Data steward |
| **Goal** | Fix formatting problems (for example encoding or whitespace) in a traceable way |
| **Source** | CR-02, CR-10 |
| **Preconditions** | The resource has been validated (UC-1) |
| **Postconditions** | A new revision exists; the original and earlier revisions are unchanged; the history records the fix |

**Main flow**

1. The steward chooses a safe fix from the list of available ones.
2. The system shows what will change before applying it.
3. The steward confirms.
4. The system creates a new revision and records in the history: fix, parameters, date and number
   of rows changed.
5. The system validates the new revision and updates the report.

**Alternative flows**

- 1a. The problem can only be solved with a change that may alter the meaning → the tool does not
  offer an automatic fix; the finding stays open for a person to decide.
- 3a. The steward cancels → nothing changes.
- 5a. The fix introduces new errors → the system shows them; the steward can go back to the
  previous revision.

### UC-5 · Approve and export the package

| | |
|---|---|
| **Primary actor** | Data steward |
| **Goal** | Obtain a clean, reproducible package ready for catalogue deposit |
| **Source** | CR-04, CR-11, CR-12 |
| **Preconditions** | No errors remain and all missing decisions are resolved |
| **Postconditions** | A ZIP package named by resource and version is created and the approval is recorded in the history |

**Main flow**

1. The steward reviews the final report (final quality control).
2. The steward approves the package explicitly.
3. The system checks that there are no errors and no open missing decisions.
4. The system builds the ZIP package: latest revision of the data, Dublin Core metadata, README,
   licence, validation reports, revision history and the checksum of the original. The ZIP is named
   by resource and version.
5. The steward downloads the package.

**Alternative flows**

- 2a. The steward does not approve → nothing is exported.
- 3a. Errors or missing decisions remain → the system blocks the export and lists what is still
  open.

## 5. User stories

Each story is also a GitHub issue created from the *User story* template, with its acceptance
criteria. The full list and the order are in the
[product backlog](../backlog/product-backlog.md). Priority: **M** must · **S** should · **C** could.
The epics are the ones of the [product vision](../product/vision.md) §4.

### Epic E1 · Validation

| ID | Story | Use case | Priority | Source |
|---|---|---|---|---|
| US-01 | As a data steward, I want to submit a resource in CSV or JSONL so that I can check it without changing the original | UC-1 | M | CR-01 |
| US-02 | As a data steward, I want the tool to check structure, missing values, duplicate IDs, encoding, data types and language codes so that I do not have to check them by hand | UC-1 | M | CR-03 |

### Epic E2 · Reporting

| ID | Story | Use case | Priority | Source |
|---|---|---|---|---|
| US-03 | As a data steward, I want each finding classified as error, warning or missing decision, with errors blocking acceptance, so that I know what to fix first | UC-1 | M | CR-04 |
| US-04 | As a data steward, I want each finding to show the file, row, field, found value and expected value so that the researcher can fix it | UC-1 | M | CR-05 |
| US-05 | As a researcher, I want the report as a web page and as a PDF, with the counts of each severity, so that I can fix my own file | UC-1 | M | CR-06 |
| US-06 | As a data steward, I want the report in JSON so that other tools can read it | UC-1 | M | CR-06 |
| US-07 | As a data steward, I want to compare a new report with the previous one so that I see what is fixed, still open and new | UC-2 | S | CR-07 |

### Epic E3 · Metadata and licences

| ID | Story | Use case | Priority | Source |
|---|---|---|---|---|
| US-08 | As a data steward, I want to see which mandatory Dublin Core fields (title, language code, producer, description, licence) are missing so that nothing is guessed | UC-3 | M | CR-08 |
| US-09 | As a data steward, I want to choose the licence from an approved, editable list (CC0 1.0, CC-BY 4.0, CC-BY-SA 4.0) so that only valid licences are used and none is guessed | UC-3 | M | CR-09 |

### Epic E4 · Preservation and revisions

| ID | Story | Use case | Priority | Source |
|---|---|---|---|---|
| US-10 | As a data steward, I want the original file preserved byte for byte, with a checksum as proof, so that I can always go back to it | UC-1 | M | CR-02 |
| US-11 | As a data steward, I want safe formatting fixes saved as separate, logged revisions, and fixes that may change meaning left to a person, so that every change is traceable | UC-4 | M | CR-10 |

### Epic E5 · Export

| ID | Story | Use case | Priority | Source |
|---|---|---|---|---|
| US-12 | As a data steward, I want to export a ZIP with data, metadata, README, licence, reports and revision history, named by resource and version, so that I can hand it over | UC-5 | M | CR-11 |
| US-13 | As a data steward, I want to approve a package explicitly before it is exported so that no package leaves the tool without final quality control | UC-5 | M | CR-12 |

## 6. Constraints

| ID | Constraint | Type | Source |
|---|---|---|---|
| C-01 | The application runs entirely on CPU; no GPU is required | Technical | Brief |
| C-02 | The application works without any external service. If the optional Latxa API is used, its responses are recorded once and replayed in tests and in the demo | Technical | Brief |
| C-03 | Implementation language: Python | Technical | Team decision (`src/` skeleton) |
| C-04 | Files above a documented size limit are rejected with a clear message. The limit is chosen and documented by the team (files up to 1 GB are out of scope) | Technical | Brief · product vision §6 · value **to confirm** |
| C-05 | Only CSV and JSONL are accepted as input; Excel and ZIP archives are rejected | Technical | CR-01 · product vision §6 |
| C-06 | The original file is never modified (byte-for-byte preservation, verified by checksum) | Data integrity | CR-02 |
| C-07 | Every fix produces a new, logged revision; no change happens silently; fixes that may change meaning need a person | Data integrity | CR-10 |
| C-08 | The licence is never inferred automatically; it is always chosen by a person from the approved list (CC0 1.0, CC-BY 4.0, CC-BY-SA 4.0) | Legal | CR-09 |
| C-09 | Metadata follow Dublin Core in V1 | Interoperability | V1 decision |
| C-10 | The access category follows the CLARIAH repository policy: CC0 → `PUB`, CC-BY → `ACA`, CC-BY-SA → `RES`. This is a repository policy, not a condition of the licences | Legal | V1 decision |
| C-11 | Reports are produced as JSON (machine-readable) and as web page and PDF (human-readable) | Technical | CR-06 |
| C-12 | No package is exported without explicit approval by the data steward | Process | CR-12 |
| C-13 | Only instructor-provided, instructor-approved or client-recommended data is processed, after checking the licence of the exact files ([`data/README.md`](../../data/README.md)) | Data / legal | Brief · product vision §7 |
| C-14 | Keys and data never enter the repository (`.env` and `data/` are ignored) | Security | Course rules |
| C-15 | Code, documents, issues and pull requests are written in English | Process | Course rules · Team charter |
| C-16 | Every requirement is traceable to the brief or to a confirmed client requirement | Process | Course rules |
| C-17 | Documents or pull requests that used AI say so in one line (`AI use: …`) | Process | Team charter |

## 7. Open questions for Jon

Answered in the Sprint 1 client conversations (see [product vision](../product/vision.md) §5):

| # | Question | Answer |
|---|---|---|
| 1 | Which file formats must the tool accept first? | CSV and JSONL (CR-01) |
| 2 | Which metadata fields are mandatory? | Title, language code, producer, description and licence (CR-08) |
| 3 | Which licences are in the approved list? | CC0 1.0, CC-BY 4.0, CC-BY-SA 4.0; the list is editable (CR-09) |
| 5 | What should the package look like? Which metadata format? | ZIP named by resource and version (CR-11); Dublin Core |
| 6 | Who reads the report, in which format? | Steward and researcher; JSON + web page + PDF (CR-06) |

Still open:

4. What size are typical resources? Which size limit should the prototype document?
7. Which safe fixes does he need most often (encoding, whitespace, empty rows…)?
8. Which language-code standard should be checked (for example ISO 639-1 or ISO 639-3)?
9. Should the README inside the package follow a template provided by CLARIAH-EUS?
