# Software Project
# CLARIAH Resource Builder · Team <TEAM NAME>

**Software Project** (Language Technologies) · Master HAP/LAP · EHU · 2026-27
Project **P4 · CLARIAH Resource Builder** · Client: **Jon**, technical coordinator and data steward
for CLARIAH-EUS (played by a Latxa-based agent)

> A tool that takes an imperfect linguistic resource, tells the researcher exactly what is wrong
> with it in a way they can act on, collects the metadata that must not be guessed, and produces a
> clean, reproducible package, leaving the original file untouched.

**Quick links:** [Team charter](docs/team/team-charter.md) ·
[Product vision](docs/product/vision.md) ·
[Product backlog](docs/backlog/product-backlog.md) ·
[Sprint 1 plan](docs/sprints/sprint-1-plan.md) ·
[Issues](../../issues) · [Project board](../../projects)

---

## Contents

1. [The product](#the-product)
2. [The team](#the-team)
3. [How we work](#how-we-work)
4. [What is where](#what-is-where)
5. [Sprint 1 checklist](#sprint-1-checklist)
6. [Git workflow](#git-workflow)
7. [Data, keys and external services](#data-keys-and-external-services)

---

## The product

A data steward submits a resource and receives a validation report that says precisely what is
wrong and where (record, field, what was found, what was expected), separating **errors**,
**warnings** and **missing decisions**. The steward then supplies the metadata that cannot be
inferred (for example the licence, chosen from a fixed approved list), applies controlled
transformations, and exports a package with the data, the metadata, the validation report and the
history of what was done. The original file is preserved byte for byte, and every transformation is
a separate, logged revision.

```
resource ──► validate ──► report (errors · warnings · missing decisions)
                              │
                              ▼
              steward adds metadata + applies transformations (each one logged)
                              │
                              ▼
           package = data + metadata + validation report + history
           (original file kept byte for byte)
```

**Out of scope:** real deposit into CLARIN, Zenodo or any other repository; FAIR certification;
automatic licence detection; a universal validator for every metadata schema; very large files.

## The team

| Member | Background | Role in sprint 1 | Belbin (P / M) | Looks after |
|---|---|---|---|---|
| Ali Faraz | BSc Computer Science | **Product Owner** | &lt;P&gt; / &lt;M&gt; | the client, the order of the backlog, the vision, the demo |
| Ángela Garrido Linares | Translation and Interpreting | **Scrum Master** | &lt;P&gt; / &lt;M&gt; | the board, the sprint plan and report, the retrospective |
| Olga | Linguistics / data analysis | Developer | &lt;P&gt; / &lt;M&gt; | client meeting logs, use cases |
| Marta | &lt;background&gt; | Developer | &lt;P&gt; / &lt;M&gt; | diagrams |
| Garazi | BSc Artificial Intelligence | Developer | &lt;P&gt; / &lt;M&gt; | risk register, data and licences |

P = preferred Belbin roles, M = manageable roles. The team diagnosis is in
[docs/belbin/](docs/belbin/).

The Product Owner keeps the role for the whole course. Whether the other roles rotate in sprint 2
is set in the [team charter](docs/team/team-charter.md).

## How we work

Summary of the [team charter](docs/team/team-charter.md), which every member has signed. The charter
is the reference if anything here disagrees with it.

| | |
|---|---|
| **Meetings** | &lt;weekly meeting: day, time, place or Zoom&gt; · &lt;stand-up format and frequency&gt; |
| **Communication** | Work is discussed in GitHub issues; logistics in &lt;chat channel&gt;. Expected answer time: &lt;…&gt; |
| **Decisions** | Consensus by default. Without consensus: the Product Owner decides scope and priorities, the Scrum Master decides process, &lt;…&gt; decides technical choices. Decisions are written in &lt;…&gt; |
| **Tasks** | Picked from the board; estimated and real hours logged in the issue; max. &lt;n&gt; cards in progress per person |
| **AI assistants** | &lt;how the team uses them and how it says so in its work&gt; |

## What is where

| Folder | What it holds | Owner |
|---|---|---|
| [`docs/team/`](docs/team/) | Team charter: roles, rules, how we decide, conflicts, signatures | whole team |
| [`docs/belbin/`](docs/belbin/) | Belbin roles of each member and the team diagnosis | whole team |
| [`docs/client/`](docs/client/) | One log per conversation with Jon, plus the exported transcripts | Olga (logs) · Ali (client contact) |
| [`docs/product/`](docs/product/) | Product vision | Ali (PO) |
| [`docs/backlog/`](docs/backlog/) | Product backlog: epics and user stories. Each story is also a GitHub issue | Ali (PO) |
| [`docs/requirements/`](docs/requirements/) | Stakeholders, use cases, constraints | Olga |
| [`docs/uml/`](docs/uml/) | Component diagram and deployment diagram | Marta |
| [`docs/risks/`](docs/risks/) | Risk register, data and licences | Garazi |
| [`docs/sprints/`](docs/sprints/) | Sprint plan, sprint report and retrospective, one set per sprint | Ángela (SM) |
| [`docs/board/`](docs/board/) | How we use the GitHub project board, with a snapshot | Ángela (SM) |
| [`src/`](src/) | Python skeleton: one module per component of the diagram, nothing implemented yet | developers |
| [`scripts/`](scripts/) | Helper scripts | developers |
| [`.github/`](.github/) | Issue templates (user story, task) and pull request template | — |

## Sprint 1 checklist

Deliverables for the **Sprint 1 review (S06, 17 November)**.

| Deliverable | File | Owner | Status |
|---|---|---|---|
| Team charter | [`docs/team/team-charter.md`](docs/team/team-charter.md) | whole team | ⬜ to do |
| Product vision | [`docs/product/vision.md`](docs/product/vision.md) | Ali | ⬜ to do |
| Client conversation logs with confirmed requirements | [`docs/client/`](docs/client/) | Olga | ⬜ to do |
| 10 to 15 user stories as issues | [`docs/backlog/product-backlog.md`](docs/backlog/product-backlog.md) + Issues tab | Ali | ⬜ to do |
| Requirements (use cases, stories, constraints) | [`docs/requirements/requirements.md`](docs/requirements/requirements.md) | Olga | ⬜ to do |
| Architecture (component and deployment diagrams) | [`docs/uml/`](docs/uml/) | Marta | ⬜ to do |
| Risk register | [`docs/risks/risk-register.md`](docs/risks/risk-register.md) | Garazi | ⬜ to do |
| Sprint 1 plan with the definition of done | [`docs/sprints/sprint-1-plan.md`](docs/sprints/sprint-1-plan.md) | Ángela | ⬜ to do |
| Sprint 1 report | [`docs/sprints/sprint-1-report.md`](docs/sprints/sprint-1-report.md) | Ángela | ⏳ at S06 |
| Retrospective 1 | [`docs/sprints/retrospective-1.md`](docs/sprints/retrospective-1.md) | Ángela | ⏳ at S06 |

Status key: ⬜ to do · 🔄 in progress · ✅ done · ⏳ at the review session.

All documents are kept as Markdown so GitHub renders them and every change is visible in the
history. For the eGela submission each document is exported to PDF.

## Git workflow

- `main` holds what has been reviewed. During sprint 1 we work on the branch `Sprint1`, which is
  merged into `main` through a pull request reviewed by a member who did not write it.
- Every member commits with their own GitHub account.
- Every story and every task is an issue, created from the templates in `.github/ISSUE_TEMPLATE/`.
  The board shows where each one is; move your own cards.
- Commits, issues, pull requests and documents are written in English.

## Data, keys and external services

- Keys and data never enter the repository: `.env` and `data/` are ignored. `.env.example` lists
  the variables without values.
- The application runs entirely on CPU and needs no external service. If the optional Latxa API is
  used, its responses are recorded once and replayed in tests and in the demonstration, so nothing
  depends on a live service.
- Only instructor-provided or instructor-approved data is processed.
