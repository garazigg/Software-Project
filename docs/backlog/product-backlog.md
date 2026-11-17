# Product backlog · CLARIAH Resource Builder

Project P4 · Software Project · Master HAP/LAP · EHU · 2026-27 · **Team 2**
Written by: Marta Salvatierra · Reviewed by: Olga · Approved and ordered by: Ali Faraz (PO) ·
Issues: Garazi Garrido · Last update: 17 November 2026

> Each story is a GitHub issue with the label `story`. Every story is traced to a requirement
> confirmed by Jon (`CR-nn` in [`docs/client/client-interviews.pdf`](../client/client-interviews.pdf)),
> also listed in the [product vision](../product/vision.md) §5. The use cases are in the
> [requirements](../requirements/requirements.md) §4.

**Priority:** must · should · could · **Points:** 1, 2, 3, 5, 8

## Epics

| ID | Epic | Description | Stories |
|---|---|---|---|
| E1 | **Validation** | Submit CSV and JSONL resources and automatically check structure, missing values, duplicate IDs, encoding, data types and language codes. | US-02, US-04 |
| E2 | **Reporting** | Classify findings as errors, warnings or missing decisions; give detailed locations and values; produce machine-readable and human-readable reports and compare report versions. | US-01, US-05, US-06, US-07 |
| E3 | **Metadata and licences** | Collect mandatory Dublin Core metadata and require licence selection from the approved list without guessing. | US-08, US-09 |
| E4 | **Preservation and revisions** | Keep original files unchanged byte for byte, verify them with checksums, and record corrections as traceable revisions. | US-03, US-10 |
| E5 | **Export** | Create a ZIP package with data, metadata, README, licence, reports and revision history, after explicit Data Steward approval. | US-11, US-12 |

## Backlog

Order set by the Product Owner. *Issue* = number of the GitHub issue.

| ID | Story | Epic | Source | Use case | Priority | Points | Sprint | Issue |
|---|---|---|---|---|---|---|---|---|
| US-01 | Actionable validation report | E2 | CR-05 | UC-1 | must | 3 | — | #<n> |
| US-02 | Submit supported formats | E1 | CR-01 | UC-1 | must | 2 | — | #<n> |
| US-03 | Preserve original file | E4 | CR-02 | UC-1 | must | 3 | — | #<n> |
| US-04 | Run automatic checks | E1 | CR-03 | UC-1 | must | 5 | — | #<n> |
| US-05 | Classify validation findings | E2 | CR-04 | UC-1 | must | 3 | — | #<n> |
| US-06 | View reports in formats | E2 | CR-06 | UC-1 | should | 5 | — | #<n> |
| US-07 | Compare validation reports | E2 | CR-07 | UC-2 | should | 5 | — | #<n> |
| US-08 | Complete required metadata | E3 | CR-08 | UC-3 | must | 3 | — | #<n> |
| US-09 | Choose approved licence | E3 | CR-09 | UC-3 | must | 3 | — | #<n> |
| US-10 | Apply safe corrections | E4 | CR-10 | UC-4 | must | 5 | — | #<n> |
| US-11 | Export resource package | E5 | CR-11 | UC-5 | must | 5 | — | #<n> |
| US-12 | Approve before export | E5 | CR-12 | UC-5 | could | 2 | — | #<n> |

**Total:** 12 stories · 44 points. No code is written in sprint 1: the stories are programmed from sprint 2.

## Stories and acceptance criteria

### E1 · Validation

#### US-02 · Submit supported formats

As a researcher, I want to submit a linguistic resource in CSV or JSONL format, so that the resource can be checked by the Resource Builder.

Source: CR-01 · Use case: UC-1 · Priority: must · Points: 2

- Given a CSV file, when I submit it, then the system accepts it as an input resource.
- Given a JSONL file, when I submit it, then the system accepts it as an input resource.

#### US-04 · Run automatic checks

As a data steward, I want the system to automatically check resource structure, missing values, duplicate IDs, encoding, data types and language codes, so that common data-quality problems are detected consistently.

Source: CR-03 · Use case: UC-1 · Priority: must · Points: 5

- Given a submitted CSV or JSONL resource, when I run validation, then the system checks its structure and required fields.

### E2 · Reporting

#### US-01 · Actionable validation report

As a data steward, I want the report to show the file, row, field, found value and expected value of every problem, so that the researcher can fix the file without emailing me.

Source: CR-05 · Use case: UC-1 · Priority: must · Points: 3

- Given a CSV with an empty "language" field in row 12, when I validate it, then the report shows row 12, field "language", found: empty, expected: ISO 639-1 code.
- Given a valid CSV, when I validate it, then the report says it has no errors.

#### US-05 · Classify validation findings

As a data steward, I want each validation finding to be classified as an error, warning or missing decision, so that I can distinguish blocking problems from issues that need attention.

Source: CR-04 · Use case: UC-1 · Priority: must · Points: 3

- Given a validation finding, when the report is generated, then it is classified as an error, warning or missing decision.
- Given a resource with one or more errors, when acceptance is assessed, then acceptance is blocked.
- Given a resource with warnings but no errors, when acceptance is assessed, then the warnings remain visible and are not treated as errors.

#### US-06 · View reports in formats

As a data steward, I want validation reports in machine-readable JSON and human-readable web-page and PDF formats, with counts by severity, so that both people and other tools can understand the validation results.

Source: CR-06 · Use case: UC-1 · Priority: should · Points: 5

- Given a completed validation, when the report is generated, then a machine-readable JSON report is available.
- Given a completed validation, when the report is generated, then a human-readable report is available as a web page and PDF.
- Given a report with findings, when I view it, then it shows the number of errors, warnings and missing decisions.

#### US-07 · Compare validation reports

As a data steward, I want to compare a new validation report with the previous report for the same resource, so that I can see which problems have been fixed, remain open or are newly detected.

Source: CR-07 · Use case: UC-2 · Priority: should · Points: 5

- Given two reports for the same resource, when I compare them, then the comparison identifies findings that have been fixed.
- Given two reports for the same resource, when I compare them, then the comparison identifies findings that are still open.
- Given two reports for the same resource, when I compare them, then the comparison identifies newly detected findings.

### E3 · Metadata and licences

#### US-08 · Complete required metadata

As a researcher, I want to provide the required metadata for my resource, including its title, language code, producer, description and licence, so that the resource is properly described before it is packaged.

Source: CR-08 · Use case: UC-3 · Priority: must · Points: 3

- Given a resource requiring metadata, when I complete its metadata form, then I can provide its title, language code, producer, description and licence.
- Given one or more mandatory metadata fields are empty, when the metadata is checked, then the system flags the missing fields.
- Given all mandatory metadata fields are completed, when the metadata is checked, then the system reports that all required fields are present.

#### US-09 · Choose approved licence

As a data steward, I want the resource licence to be selected from an approved, editable list, so that no resource is assigned an invented or incorrect licence by the tool.

Source: CR-09 · Use case: UC-3 · Priority: must · Points: 3

- Given a resource without a licence, when I provide its licence, then I can choose from the approved list: CC0 1.0, CC-BY 4.0 or CC-BY-SA 4.0.
- Given no licence has been selected, when the resource is prepared for export, then the system does not guess a licence and flags the missing decision.
- Given an authorised update to the approved licence list, when the list is edited, then the updated list is available for subsequent licence selection.

### E4 · Preservation and revisions

#### US-03 · Preserve original file

As a data steward, I want the original uploaded file to remain unchanged byte for byte and have a checksum recorded, so that the original resource can be verified and recovered.

Source: CR-02 · Use case: UC-1 · Priority: must · Points: 3

- Given an uploaded resource, when the system processes or corrects it, then the original file remains unchanged.

#### US-10 · Apply safe corrections

As a data steward, I want safe formatting fixes to be applied as separate, logged revisions and fixes that may change the meaning to require human review, so that corrections are traceable and do not silently change the resource’s meaning.

Source: CR-10 · Use case: UC-4 · Priority: must · Points: 5

- Given a formatting problem classified as safe, when the fix is applied, then it is saved as a separate revision and recorded in the revision log.
- Given a proposed fix that may change the meaning, when the system detects it, then it requires human review before it is applied.
- Given a correction has been applied, when I inspect the revision history, then I can identify the change as a recorded revision.

### E5 · Export

#### US-11 · Export resource package

As a data steward, I want to export a ZIP package containing the resource data, metadata, README, licence information, validation reports and revision history, so that I can provide a complete and traceable resource package.

Source: CR-11 · Use case: UC-5 · Priority: must · Points: 5

- Given a resource is ready for packaging, when I export it, then the ZIP package contains the resource data, metadata, README, licence information, validation reports and revision history.
- Given a package is exported, when I inspect its name, then it identifies the resource and its version.
- Given the package is created, when I inspect its contents, then the original file is preserved unchanged.

#### US-12 · Approve before export

As a data steward, I want to explicitly approve the final package after quality control and before export, so that only an approved package can be downloaded.

Source: CR-12 · Use case: UC-5 · Priority: could · Points: 2

- Given a package has completed final quality control, when the data steward reviews it, then an explicit approval action is available.
- Given the data steward has not approved the package, when someone attempts to export or download it, then the system blocks the action.
- Given the data steward approves the package, when export is requested, then the package becomes available for export.

## Change log

| Date | Change | By |
|---|---|---|
| 17 November 2026 | Backlog created: 12 stories in 5 epics, one per confirmed requirement CR-01 to CR-12 | Team 2 |
