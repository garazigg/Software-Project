# Software Project
# CLARIAH Resource Builder · Team <TEAM NAME>

Software Project (Language Technologies) · Master HAP/LAP · EHU · 2026-27
Project **P4 · CLARIAH Resource Builder** · Client: **Jon**, technical coordinator and data steward
for CLARIAH-EUS (played by a Latxa-based agent)

> A tool that takes an imperfect linguistic resource, tells the researcher exactly what is wrong
> with it in a way they can act on, collects the metadata that must not be guessed, and produces a
> clean, reproducible package, leaving the original file untouched.

## The product in one paragraph

A data steward submits a resource and receives a validation report that says precisely what is
wrong and where (record, field, what was found, what was expected), separating **errors**,
**warnings** and **missing decisions**. The steward then supplies the metadata that cannot be
inferred (for example the licence, chosen from a fixed approved list), applies controlled
transformations, and exports a package with the data, the metadata, the validation report and the
history of what was done. The original file is preserved byte for byte, and every transformation is
a separate, logged revision.

Out of scope: real deposit into CLARIN, Zenodo or any other repository; FAIR certification;
automatic licence detection; a universal validator for every metadata schema; very large files.

## The team

| Member | Role in sprint 1 | Belbin roles (P / M) | Looks after |
|---|---|---|---|
| <name> | Product Owner | <primary> / <secondary> | the client, the order of the backlog, the vision |
| <name> | Scrum Master | <primary> / <secondary> | the board, the sprint plan, the retrospective |
| <name> | Developer | <primary> / <secondary> | the skeleton, the risk register, checking documents |

Roles rotate at the start of sprint 2. See [docs/team/team-charter.md](docs/team/team-charter.md).

## What is where

| Folder | What it holds | Written by |
|---|---|---|
| `docs/team/` | Team charter: roles, rules, how we decide, signatures | the whole team |
| `docs/belbin/` | Belbin roles of each member and the team diagnosis | <name> |
| `docs/client/` | One log per conversation with Jon, plus the exported transcripts | Product Owner |
| `docs/product/` | Product vision | Product Owner |
| `docs/backlog/` | Product backlog: epics and user stories. Each story is also a GitHub issue | <name> |
| `docs/requirements/` | Stakeholders, use cases, constraints | <name> |
| `docs/uml/` | Component diagram and deployment diagram | <name> |
| `docs/risks/` | Risk register | <name> |
| `docs/sprints/` | Sprint plan, sprint report and retrospective, one set per sprint | Scrum Master |
| `docs/board/` | How we use the GitHub project board, with a snapshot | Scrum Master |
| `src/` | Python skeleton: one module per component of the diagram, nothing implemented yet | <name> |
| `scripts/` | Helper scripts | <name> |

## Sprint 1 checklist

Deliverables for the Sprint 1 review (S06, 17 November).

| Deliverable | File | Status |
|---|---|---|
| Team charter | `docs/team/team-charter.md` | to do |
| Product vision | `docs/product/vision.md` | to do |
| Client conversation logs with confirmed requirements | `docs/client/` | to do |
| 10 to 15 user stories as issues | `docs/backlog/product-backlog.md` and the Issues tab | to do |
| Requirements (use cases, stories, constraints) | `docs/requirements/requirements.md` | to do |
| Architecture (component and deployment diagrams) | `docs/uml/` | to do |
| Risk register | `docs/risks/risk-register.md` | to do |
| Sprint 1 plan with the definition of done | `docs/sprints/sprint-1-plan.md` | to do |
| Sprint 1 report | `docs/sprints/sprint-1-report.md` | at S06 |
| Retrospective 1 | `docs/sprints/retrospective-1.md` | at S06 |

All documents are kept as Markdown so GitHub renders them and every change is visible in the
history. For the eGela submission each document is exported to PDF.

## How we work in Git

- `main` holds what has been reviewed. During sprint 1 we work on the branch `Sprint1`, which is
  merged into `main` through a pull request reviewed by a member who did not write it.
- Every member commits with their own GitHub account.
- Every story and every task is an issue. The board shows where each one is; move your own cards.
- Keys and data never enter the repository: `.env` and `data/` are ignored. `.env.example` lists
  the variables without values.
- The application runs entirely on CPU and needs no external service. If the optional Latxa API is
  used, its responses are recorded once and replayed in tests and in the demonstration, so nothing
  depends on a live service.
- Only instructor-provided or instructor-approved data is processed.
