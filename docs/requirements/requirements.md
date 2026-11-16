# Requirements · CLARIAH Resource Builder

Project P4 · Software Project · Master HAP/LAP · EHU · 2026-27 · **Team 2**
Written by: Marta Salvatierra · Reviewed by: Olga · Approved by: Ali Faraz (PO)
Status: **draft** · Last update: <date>

> Every requirement points to its source: the project brief (`Brief §n`) or a requirement confirmed
> by the client (`CR-nn`), recorded in [`docs/client/`](../client/). Items marked **to confirm**
> still need Jon's confirmation before the Sprint 1 review (17 November).
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

The CLARIAH Resource Builder helps a data steward prepare a linguistic resource for handover. The
steward submits a resource, receives an actionable validation report, supplies the metadata that
cannot be inferred, applies controlled transformations and exports a reproducible package. The
original file is never modified.

**In scope**

- Validation of a resource with an actionable report (errors, warnings, missing decisions).
- Collection of the metadata that must not be guessed (for example the licence).
- Controlled transformations, each one stored as a separate, logged revision.
- Export of a package with data, metadata, validation report and history.

**Out of scope** (Brief)

- Real deposit into CLARIN, Zenodo or any other repository.
- FAIR certification.
- Automatic licence detection or legal advice.
- A universal validator for every metadata schema.
- Very large files (a documented size limit applies).
- Mandatory use of GPU or of an LLM.

## 2. Glossary

| Term | Meaning in this project |
|---|---|
| **Resource** | A linguistic dataset (for example a corpus file) submitted for preparation |
| **Original** | The file exactly as submitted. It is preserved byte for byte |
| **Revision** | A new version of the resource produced by one transformation. Each revision is logged |
| **Error** | A problem that makes the resource unacceptable (for example a malformed record or a missing required field) |
| **Warning** | An unusual but valid value that the steward should look at |
| **Missing decision** | Information only a person can provide (for example the licence). It is neither an error nor a warning |
| **Metadata** | Descriptive information about the resource: title, creators, language, licence, etc. |
| **Package** | The export: data, metadata, validation report and history of what was done |
| **History** | The ordered log of every action and transformation applied to the resource |

## 3. Stakeholders

| Stakeholder | Interest | How they use the tool |
|---|---|---|
| **Data steward** (Jon, our client) | Validate resources predictably and produce a package he can trust | Main user: submits, validates, completes metadata, transforms, exports |
| **Researcher** (resource provider) | Get the resource accepted without long e-mail exchanges | Receives the validation report and fixes their own file |
| **Package consumer** (CLARIAH-EUS, future users) | Find, understand and reuse the resource legally | Receives the package; relies on metadata, licence and history |
| **Teaching team** | Assess the process and the product | Reviews the repository, the documents and the demonstration |

## 4. Use cases

### UC-1 · Validate a resource and get an actionable report

| | |
|---|---|
| **Primary actor** | Data steward |
| **Goal** | Know exactly what is wrong with a resource, and where, so that it can be fixed |
| **Source** | Brief · CR-<nn> (**to confirm**) |
| **Preconditions** | The steward has a resource file in a supported format and within the size limit |
| **Postconditions** | The original is stored unchanged; a validation report is available |

**Main flow**

1. The steward submits a resource file.
2. The system stores the original and records its checksum.
3. The system validates the resource.
4. The system shows a report that lists, for each problem: its type (error, warning or missing
   decision), the record, the field, what was found and what was expected.
5. The steward exports the report to send it to the researcher.

**Alternative flows**

- 2a. The format is not supported or the file exceeds the size limit → the system rejects it and
  says why.
- 4a. No problems are found → the report says so explicitly and lists only the missing decisions,
  if any.

### UC-2 · Complete the metadata that cannot be inferred

| | |
|---|---|
| **Primary actor** | Data steward |
| **Goal** | Provide the information that only a person can decide, such as the licence |
| **Source** | Brief · CR-<nn> (**to confirm**) |
| **Preconditions** | The resource has been validated (UC-1) |
| **Postconditions** | All mandatory metadata fields are filled; the missing decisions are resolved |

**Main flow**

1. The system lists the mandatory metadata fields that are still empty.
2. The steward fills each field. The licence is chosen from a fixed list of approved licences.
3. The system checks each value (format, allowed values) and saves it.
4. The system updates the report: resolved missing decisions disappear.

**Alternative flows**

- 2a. The licence the steward needs is not in the approved list → the system does not allow free
  text; the missing decision stays open and the package cannot be exported.
- 3a. A value is invalid → the system explains what is expected and keeps the field empty.

### UC-3 · Apply a controlled transformation

| | |
|---|---|
| **Primary actor** | Data steward |
| **Goal** | Fix common problems (for example encoding or label normalisation) in a traceable way |
| **Source** | Brief · CR-<nn> (**to confirm**) |
| **Preconditions** | The resource has been validated (UC-1) |
| **Postconditions** | A new revision exists; the original and earlier revisions are unchanged; the history records the transformation |

**Main flow**

1. The steward chooses a transformation from the list of available ones.
2. The system shows what will change (preview) before applying it.
3. The steward confirms.
4. The system creates a new revision and records in the history: transformation, parameters,
   date and number of records changed.
5. The system validates the new revision and updates the report.

**Alternative flows**

- 3a. The steward cancels → nothing changes.
- 5a. The transformation introduces new errors → the system shows them; the steward can go back
  to the previous revision.

### UC-4 · Export the package

| | |
|---|---|
| **Primary actor** | Data steward |
| **Goal** | Obtain a clean, reproducible package ready for handover |
| **Source** | Brief · CR-<nn> (**to confirm**) |
| **Preconditions** | No errors remain and all missing decisions are resolved |
| **Postconditions** | A package is created with data, metadata, validation report and history |

**Main flow**

1. The steward asks to export the package.
2. The system checks that there are no errors and no open missing decisions.
3. The system builds the package: latest revision of the data, metadata, final validation report,
   history and the checksum of the original.
4. The steward downloads the package.

**Alternative flows**

- 2a. Errors or missing decisions remain → the system blocks the export and lists what is still
  open.

## 5. User stories

Each story is also a GitHub issue created from the *User story* template, with its acceptance
criteria. The full list and the order are in the
[product backlog](../backlog/product-backlog.md). Priority: **M** must · **S** should · **C** could.

### Epic E1 · Validation

| ID | Story | Use case | Priority | Source |
|---|---|---|---|---|
| US-01 | As a data steward, I want to upload a resource file so that I can check it without changing the original | UC-1 | M | Brief |
| US-02 | As a data steward, I want the original file to be preserved byte for byte so that I can always go back to it | UC-1 | M | Brief |
| US-03 | As a data steward, I want a report that separates errors, warnings and missing decisions so that I know what to fix first | UC-1 | M | Brief |
| US-04 | As a data steward, I want each problem to show the record, the field, what was found and what was expected so that the researcher can fix it | UC-1 | M | Brief |
| US-05 | As a researcher, I want to receive the report in a readable format so that I can fix my own file | UC-1 | S | to confirm |

### Epic E2 · Metadata and transformations

| ID | Story | Use case | Priority | Source |
|---|---|---|---|---|
| US-06 | As a data steward, I want to see which mandatory metadata fields are missing so that nothing is guessed | UC-2 | M | Brief |
| US-07 | As a data steward, I want to choose the licence from an approved list so that only valid licences are used | UC-2 | M | Brief |
| US-08 | As a data steward, I want to preview a transformation before applying it so that I know what will change | UC-3 | S | to confirm |
| US-09 | As a data steward, I want each transformation saved as a separate revision so that I can undo it | UC-3 | M | Brief |
| US-10 | As a data steward, I want a history of every action so that the preparation can be reproduced | UC-3 | M | Brief |

### Epic E3 · Packaging

| ID | Story | Use case | Priority | Source |
|---|---|---|---|---|
| US-11 | As a data steward, I want to export a package with data, metadata, report and history so that I can hand it over | UC-4 | M | Brief |
| US-12 | As a data steward, I want the export to be blocked while errors or missing decisions remain so that no incomplete package leaves the tool | UC-4 | M | Brief |
| US-13 | As a package consumer, I want the package to include the checksum of the original so that I can verify where the data comes from | UC-4 | C | to confirm |

## 6. Constraints

| ID | Constraint | Type | Source |
|---|---|---|---|
| C-01 | The application runs entirely on CPU; no GPU is required | Technical | Brief |
| C-02 | The application works without any external service. If the optional Latxa API is used, its responses are recorded once and replayed in tests and in the demo | Technical | Brief |
| C-03 | Implementation language: Python | Technical | Team decision (`src/` skeleton) |
| C-04 | Files above a documented size limit are rejected with a clear message | Technical | Brief · limit **to confirm** |
| C-05 | Only a defined set of input formats is supported (not a universal validator) | Technical | Brief · formats **to confirm** |
| C-06 | The original file is never modified (byte-for-byte preservation, verified by checksum) | Data integrity | Brief |
| C-07 | Every transformation produces a new, logged revision; no change happens silently | Data integrity | Brief |
| C-08 | The licence is never inferred automatically; it is always chosen by a person from the approved list | Legal | Brief |
| C-09 | Only instructor-provided or instructor-approved data is processed | Data / legal | Brief |
| C-10 | Keys and data never enter the repository (`.env` and `data/` are ignored) | Security | Course rules |
| C-11 | Code, documents, issues and pull requests are written in English | Process | Course rules · Team charter |
| C-12 | Every requirement is traceable to the brief or to a confirmed client requirement | Process | Course rules |
| C-13 | Documents or pull requests that used AI say so in one line (`AI use: …`) | Process | Team charter |

## 7. Open questions for Jon

To ask in the next client conversation and record in [`docs/client/`](../client/). Each answer
becomes a `CR-nn` that replaces a **to confirm** above.

1. Which file formats must the tool accept first (CSV, TSV, CoNLL-U, XML/TEI…)?
2. Which metadata fields are mandatory, and which can be left empty?
3. Which licences are in the approved list?
4. What size are typical resources? What would be an acceptable size limit?
5. What should the package look like (folder, ZIP…)? Which metadata format (for example Dublin Core or CMDI)?
6. Who reads the validation report: only the steward, or also the researcher directly? In which format?
7. Which transformations does he need most often (label normalisation, encoding fixes, removing empty records…)?
8. What has gone wrong in the past that the tool must prevent?
