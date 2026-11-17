# Product vision · CLARIAH Resource Builder

Project P4 · Software Project · Master HAP/LAP · EHU · 2026-27 · **Team 2**
Written by: Ali Faraz (PO) · Reviewed by: Olga · Version 1.1 · Sprint 1 draft

## 1. Product goal

A tool that helps CLARIAH-EUS data stewards turn imperfect linguistic resources into clean,
validated and documented packages, without ever changing the original files.

## 2. Vision

Researchers currently send linguistic resources with structural, content and metadata problems,
requiring repeated manual checks and email-based corrections. The CLARIAH Resource Builder will
validate submitted resources, provide clear reports, support metadata and licence completion,
preserve originals and their revision history, and produce a reproducible export package. This will
reduce manual effort and errors while making resources easier to prepare for catalogue deposit.

## 3. Line of research

Research data stewardship for CLARIAH-EUS, the Basque node of the CLARIN and DARIAH research
infrastructures, with a focus on preparing, validating, documenting and preserving linguistic
resources.

## 4. Epics

| ID | Epic | Description |
|---|---|---|
| E1 | **Validation** | Submit CSV and JSONL resources and automatically check structure, missing values, duplicate IDs, encoding, data types and language codes. |
| E2 | **Reporting** | Classify findings as errors, warnings or missing decisions; provide detailed locations and values; generate machine-readable and human-readable reports and compare report versions. |
| E3 | **Metadata and licences** | Collect mandatory metadata, use Dublin Core for V1, and require licence selection from the approved list without guessing. |
| E4 | **Preservation and revisions** | Keep original files unchanged byte for byte, verify them with checksums, and record corrections as traceable revisions. |
| E5 | **Export** | Create a ZIP package containing resource data, metadata, README, licence information, validation reports and revision history, with explicit Data Steward approval before export. |

## 5. Scope in (Version 1)

| ID | Confirmed client requirement | Epic |
|---|---|---|
| CR-01 | Jon needs to submit resources in CSV and JSONL formats. | E1 |
| CR-02 | Jon needs the original file to stay unchanged byte for byte, with proof through a checksum. | E4 |
| CR-03 | Jon needs automatic checks of structure, missing values, duplicate IDs, encoding, data types and language codes. | E1 |
| CR-04 | Jon needs each finding classified as an error, warning or missing decision; errors block acceptance. | E2 |
| CR-05 | Jon needs each report finding to show the file, row, field, found value and expected value. | E2 |
| CR-06 | Jon needs machine-readable and human-readable reports, with counts for each severity level. The human-readable report will be available as both a web page and a PDF; JSON will provide the machine-readable format. | E2 |
| CR-07 | Jon needs to compare a new report with the previous one to identify fixed, still-open and new problems. | E2 |
| CR-08 | Jon needs mandatory metadata (title, language code, producer, description and licence) to be collected and missing fields flagged. | E3 |
| CR-09 | Jon needs licences to be selected from an approved, editable list (CC0 1.0, CC-BY 4.0 and CC-BY-SA 4.0); the tool must never guess a licence. | E3 |
| CR-10 | Jon needs safe formatting fixes applied as separate, logged revisions; fixes that may change meaning require a person. | E4 |
| CR-11 | Jon needs a ZIP export package containing data, metadata, README, licence, reports and revision history, named by resource and version. | E5 |
| CR-12 | Jon needs to approve a package explicitly before it is exported. | E5 |

### Additional confirmed V1 decisions

- **Metadata standard:** Dublin Core.
- **Reports:** human-readable as both web page and PDF; machine-readable as JSON.
- **Licence → access category:** the official CLARIAH repository policy maps CC0 to `PUB`, CC-BY to
  `ACA` and CC-BY-SA to `RES`. Jon confirmed this is a repository-specific policy, not a restriction
  imposed by the Creative Commons licences themselves.
- **Approval gate:** the Data Steward approves the package after final quality control and before
  export or download.

## 6. Scope out (Version 1)

Excluded by the project brief or left for future versions:

- Uploading packages directly to the CLARIAH repository or any other repository.
- Very large files up to 1 GB; the prototype will document a size limit instead.
- A full web application with five user roles, permissions and email notifications.
- Automatic licence detection or legal advice.
- Excel files and ZIP archive submissions as input. ZIP export packages are in scope; ZIP input
  submissions are not part of V1.
- Training, workshops and community channels.

## 7. Data and licences

Sample linguistic datasets recommended by Jon for demonstration and testing. Details and the
licence check of each file are kept in [`data/README.md`](../../data/README.md).

| # | Dataset | Content | Licence | Source |
|---|---|---|---|---|
| 1 | 20 Newsgroups | About 20,000 newsgroup messages | CC-BY-SA 4.0 (as clarified by Jon) | <https://www.kaggle.com/datasets/20newsgroup> |
| 2 | Open Multilingual WordNet (OMW) | Multilingual lexical database: word senses, synonyms, hyponyms | CC-BY 4.0 for the recommended version; individual language resources may have other terms | <http://compling.hss.ntu.edu.sg/omw/download> |
| 3 | Selected NLTK corpora | Brown Corpus, Penn Treebank, Wall Street Journal Corpus | CC0 1.0, as specified by Jon for these three corpora; other NLTK corpora may differ | <https://www.nltk.org/nltk_data/packages/> |

**Usage note:** before using any dataset in the demo or tests, the team must review the applicable
licence and terms for the exact dataset version and files selected. Jon specifically noted that some
OMW language resources and other NLTK corpora may have additional or different licensing terms.

## 8. Success criteria

- Every problem in the report shows the file, row, field, found value and expected value.
- The original file has the same checksum before and after processing.
- A complete package can be exported for a sample resource with all its mandatory metadata.
