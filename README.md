# CLARIAH Resource Builder · Team 2

**Software Project** (Language Technologies) · Master HAP/LAP · EHU · 2026-27
Project **P4 · CLARIAH Resource Builder** · Client: **Jon**, technical coordinator and data steward
for CLARIAH-EUS (played by a Latxa-based agent)

> A tool that prepares linguistic resources for CLARIAH-EUS: it checks their format, measures how
> far two annotations agree and packages the results in a ZIP, without ever changing the original
> files. ([Product vision](docs/product/vision.md))

**Quick links:** [Team charter](docs/team/team-charter.md) ·
[Product vision](docs/product/vision.md) ·
[Product backlog](docs/backlog/product-backlog.md) ·
[Risk register](docs/risks/risks.md) ·
[Initial sprint backlog](docs/sprints/initial-sprint-backlog.md) ·
[Issues](../../issues) ·
[Project board](https://github.com/users/garazigg/projects/4/views/1)

---

## Contents

1. [The product](#the-product)
2. [The team](#the-team)
3. [Our objectives](#our-objectives)
4. [How we work](#how-we-work)
5. [Team rules](#team-rules)
6. [What is where](#what-is-where)
7. [Initial sprint checklist](#initial-sprint-checklist)
8. [Git workflow](#git-workflow)
9. [Data, keys and external services](#data-keys-and-external-services)

---

## The product

A data steward submits one or two resources in **CSV or JSONL**. The tool stores the original
read-only with a **SHA-256 checksum** and records its metadata (name, format, size, checksum, date,
submitter) from the file and the run, never typed in. It then **checks the format** (structure,
column names, missing values, inconsistent labels) and returns either "OK, no issues" or a report
that says where every issue is (file, row or line, column or field, type). For two annotation files
of the same items, it computes their **agreement** as a percentage with the detail per label, and
refuses files that cannot be compared. Finally it **packages** the report, the metadata and the log
into one **ZIP**. Every action is logged, and the original file is never modified.

```
1 or 2 files (CSV / JSONL)
        │
        ▼
 1. submit ── original stored read-only + SHA-256 + metadata + log entry
        │
        ▼
 2. format check ── issues? ──yes──► issue report ──────────────┐
        │ no                                                    │
        ▼                                                       │
 3. agreement (2 files) ── % + per label (later: Cohen's kappa)  │
        │                                                       │
        ▼                                                       ▼
 4. package ── ZIP = report + metadata + log (originals copied or referenced, never modified)
```

Command line first; a web interface with the same steps later, on top of the same core.

**Epics (V1), one per sprint:** E1 One file end to end (CLI) · E2 Agreement between two annotation
files · E3 Better agreement measures and web interface. The client requirements CR-01 to CR-12,
confirmed in Meeting 5, are listed in the [product vision](docs/product/vision.md) and traced to
the user stories in the [product backlog](docs/backlog/product-backlog.md).

**Out of scope (V1), agreed with Jon in Meeting 5:** metadata forms (Dublin Core); licences and
access categories; automatic corrections; steward approval before export; comparison between
reports; report languages; uploading packages to CLARIAH or any other repository; Excel or ZIP files
as input; user roles, permissions and notifications; very large files (a size limit is documented).
These are kept as candidates for future versions.

## The team

| Member | Background | Belbin (P / M) | Role in sprint 1 | Looks after |
|---|---|---|---|---|
| **Ali Faraz** | BSc Computer Science | Coordinator / Monitor Evaluator | **Product Owner** | Leads every conversation with the client; approves and orders the final user stories; the vision and the demo |
| **Ángela Garrido Linares** | Translation and Interpreting (German and French) | Resource Investigator / Shaper | **Scrum Master** | Communicates the tasks, logs the working hours, internal communication; the board, the sprint plan and report, the retrospective |
| **Olga Makarova** | Linguistics / data analysis | Completer Finisher / Coordinator | Developer | Client interview guide; reviews the user stories and the technical parts of the vision (clear, buildable and testable) |
| **Marta Salvatierra** | Spanish and English Philology | Completer Finisher / Teamworker | Developer | Client meeting logs and transcripts; turns Jon's confirmed needs into user stories; the requirements document; reviews the wording of our documents; supports the Scrum Master |
| **Garazi Garrido** | Artificial Intelligence | Resource Investigator / Specialist | Developer | GitHub set-up (repository, folders, board, milestones) and teaching the team to use it; GitHub issues from the user stories; reviews the risk register and creates the mitigation issues; sample data and licences; this README |

P = preferred Belbin roles, M = manageable roles.

**Role rotation:** the Scrum Master role rotates at the start of each sprint. The Product Owner
keeps the role for the whole course.

### Team diagnosis

- **Covered naturally:** Coordinator (Ali), Resource Investigator (Ángela, Garazi), Completer
  Finisher (Olga, Marta). We organise well, look for ideas and tools outside the team, and check
  the quality of what we deliver.
- **Somebody steps up:** Monitor Evaluator (Ali), Shaper (Ángela, as Scrum Master), Teamworker
  (Marta), Specialist (Garazi), Coordinator as backup (Olga).
- **Uncovered: Plant and Implementer.**
  - *Implementer* → every story issue is split into small tasks (2 to 8 hours) in its checklist,
    and the Scrum Master makes sure each one has an owner and a deadline.
  - *Plant* → at the start of each sprint we hold a short brainstorming in which everyone proposes
    ideas, and the Resource Investigators bring examples and tools from outside the team.

## Our objectives

- Deliver a CLARIAH Resource Builder that Jon can really use, combining our linguistic profiles
  (translation, philology, linguistics) with our technical ones (computer science, AI).
- Learn the tools of a real software team (Scrum, GitHub issues, board, pull requests): the
  linguists gain confidence with them, and the technical members learn to work with linguistic
  requirements.
- Understand the architecture of our project well enough that every member can explain any part of
  it at the reviews.

## How we work

Summary of the [team charter](docs/team/team-charter.md). The charter is the reference if anything
here disagrees with it.

| | |
|---|---|
| **Meetings** | Day and time agreed each week according to availability; face-to-face or on Google Meet. Stand-ups go to the GitHub issue *"Stand-ups Sprint 1"* (while the team learns GitHub, they are posted in WhatsApp and the Scrum Master copies them there). |
| **Communication** | Work and decisions in **GitHub issues**; logistics in the WhatsApp group and by e-mail. We answer within **2 hours** on working days between 10:00 and 20:00; messages sent later are answered the next working day. |
| **Availability** | About **15 hours per member in sprint 1** (≈ 7 h/week). Exact hours are set in each sprint plan. |
| **Decisions** | Majority vote of the whole team, giving weight to each member's expertise on the topic (linguistic or technical). On a tie (e.g. if someone abstains), the Scrum Master decides. Product decisions (priority and order of the backlog) are taken by the Product Owner after hearing the team. Every decision is written in the related issue. |
| **Tasks** | The Scrum Master assigns tasks in consensus with the team (role, skills, availability); the owner is written next to each task in its GitHub issue. Each task logs **estimated** and **real** hours. |
| **Sprints** | An *Initial sprint* (10–22 November: team, client, vision, backlog, no code), then one epic per sprint. Each sprint is a GitHub milestone (*Initial sprint*, *Sprint 1*, *Sprint 2*, *Sprint 3*); see [how we use the board](docs/board/board.md). |
| **AI assistants** | Used to draft, review and explain. Each member reviews what they commit and can explain it. Every document or pull request that used AI says so in one line: `AI use: …` |

## Team rules

1. **Working language: English.** We help those who do not master it to communicate.
2. **Respect** for each other and each other's efforts: if a deadline or the expected quality is
   missed despite genuine effort, no one is blamed.
3. **Deadlines and attendance:** we aim to meet every deadline with the expected quality. A member
   who cannot attend a meeting warns in advance and catches up through chat or e-mail.
4. **Disagreeing constructively:** we always propose an alternative instead of only criticising.
5. **Healthy environment:** assertiveness and active listening come first.

**Conflicts.** Misunderstandings are clarified in the moment, focusing on the work. Work that meets
the definition of done is finished; extra improvements go to the backlog. If a member falls behind,
the Scrum Master follows up and the task is split or shared; if it happens again, the instructors
are told. Full table in the [team charter](docs/team/team-charter.md).

## What is where

| Folder | What it holds | Owner |
|---|---|---|
| [`docs/team/`](docs/team/) | Team charter: roles, rules, how we decide, conflicts, signatures | Ángela (harmonises) · whole team |
| [`docs/belbin/`](docs/belbin/) | Belbin roles of each member and the team diagnosis | whole team |
| [`docs/client/`](docs/client/) | Interview guide, one log per conversation with Jon, exported transcripts | Marta (logs) · Olga (guide) · Ali (lead) |
| [`docs/product/`](docs/product/) | Product vision | Ali (PO) · reviewed by Olga |
| [`docs/backlog/`](docs/backlog/) | Product backlog: epics and user stories. Each story is also a GitHub issue | Marta (writes) · Olga (reviews) · Ali (approves and orders) · Garazi (issues) |
| [`docs/requirements/`](docs/requirements/) | Stakeholders, use cases, constraints and the use case diagram | Marta · Garazi |
| [`docs/uml/`](docs/uml/) | Component diagram and deployment diagram | Olga |
| [`docs/risks/`](docs/risks/) | Risk register and mitigation issues | Garazi (review and issues) |
| [`docs/sprints/`](docs/sprints/) | Sprint backlog, sprint report and retrospective, one set per sprint | Ángela (SM) |
| [`docs/board/`](docs/board/) | How we use the GitHub project board and milestones, with a snapshot per sprint | Ángela (SM) · Garazi (set-up) |
| [`data/README.md`](data/README.md) | Synthetic test data made by the team and sample datasets recommended by Jon (20 Newsgroups, OMW, NLTK), with their licences (the data itself is not committed) | Garazi |
| [`src/`](src/) | Python skeleton: a core module (submit, check, agreement, package) and a thin command-line layer on top; the web interface will be a second layer in Epic 3 | developers |
| [`scripts/`](scripts/) | Helper scripts | developers |
| [`.github/`](.github/) | Issue templates (user story, task) and pull request template | Garazi |

## Initial sprint checklist

Deliverables of the **initial sprint (10–22 November)** for the review at **S06 (<date>)**.

| Deliverable | File | Owner | Status |
|---|---|---|---|
| Belbin roles and team diagnosis | [`docs/belbin/`](docs/belbin/) | whole team | ⬜ to do |
| Team charter | [`docs/team/`](docs/team/) | Ángela (harmonises) · whole team | ✅ done (review by Ángela) |
| Client conversation logs with confirmed requirements | [`docs/client/client-interviews.pdf`](docs/client/client-interviews.pdf) | Marta | ✅ done (Meetings 1 to 5, CR-01 to CR-12) |
| Product vision | [`docs/product/`](docs/product/) | Ali | ✅ done |
| 10 to 15 user stories as issues | [`docs/backlog/product-backlog.md`](docs/backlog/product-backlog.md) + [Issues tab](../../issues?q=label%3Astory) (12 stories, #16 to #27) | Marta · Ali · Garazi | ✅ done |
| Requirements (use cases, constraints) | [`docs/requirements/requirements.md`](docs/requirements/requirements.md) | Marta · Garazi | 🔄 to update for Meeting 5 |
| Use case diagram | [`docs/requirements/`](docs/requirements/) | Garazi | 🔄 final version to choose |
| Architecture (component and deployment diagrams) | [`docs/uml/`](docs/uml/) | Olga | ⬜ to do |
| Risk register | [`docs/risks/risks.md`](docs/risks/risks.md) | Garazi | ✅ done (review pending) |
| Project board | [Board](https://github.com/users/garazigg/projects/4) · [`docs/board/board.md`](docs/board/board.md) | Ángela · Garazi | ✅ done (review pending) |
| Initial sprint backlog with hours per member | [`docs/sprints/initial-sprint-backlog.md`](docs/sprints/initial-sprint-backlog.md) | Ángela · whole team | 🔄 hours to fill in |
| Initial sprint retrospective | [`docs/sprints/initial-sprint-retrospective.md`](docs/sprints/initial-sprint-retrospective.md) | Ángela · whole team | ⏳ at S06 |

Status key: ⬜ to do · 🔄 in progress · ✅ done · ⏳ at the review session.

All documents are kept as Markdown so GitHub renders them and every change is visible in the
history. For the eGela submission each document is exported to PDF.

## Git workflow

- `main` holds what has been reviewed. During each sprint we work on a sprint branch (e.g. `Sprint1`), which is
  merged into `main` through a pull request reviewed by a member who did not write it.
- Every member commits with their own GitHub account.
- Every story and every task is an issue, created from the templates in `.github/ISSUE_TEMPLATE/`,
  with its labels (`story` or `task`, priority, epic) and the milestone of its sprint.
  The [board](https://github.com/users/garazigg/projects/4/views/1) shows where each one is.
- Each issue records the estimated and the real hours of the task.
- A pull request that finishes an issue says `Closes #<n>`.
- Commits, issues, pull requests and documents are written in English. Pull requests that used AI
  include an `AI use: …` line.

## Data, keys and external services

- Keys and data never enter the repository: `.env` and `data/` are ignored (except
  `data/README.md`). `.env.example` lists the variables without values.
- The application runs entirely on CPU and needs no external service.
- Only synthetic data made by the team, instructor-provided, instructor-approved or
  client-recommended data is processed, after checking the licence of the exact files in
  [`data/README.md`](data/README.md).
