# CLARIAH Resource Builder · Team 2

**Software Project** (Language Technologies) · Master HAP/LAP · EHU · 2026-27
Project **P4 · CLARIAH Resource Builder** · Client: **Jon**, technical coordinator and data steward
for CLARIAH-EUS (played by a Latxa-based agent)

> A tool that helps CLARIAH-EUS data stewards turn imperfect linguistic resources into clean,
> validated and documented packages, without ever changing the original files.
> ([Product vision](docs/product/vision.md))

**Quick links:** [Team charter](docs/team/team-charter.md) ·
[Product vision](docs/product/vision.md) ·
[Product backlog](docs/backlog/product-backlog.md) ·
[Sprint 1 plan](docs/sprints/sprint-1-plan.md) ·
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
7. [Sprint 1 checklist](#sprint-1-checklist)
8. [Git workflow](#git-workflow)
9. [Data, keys and external services](#data-keys-and-external-services)

---

## The product

A data steward submits a resource in **CSV or JSONL** and receives a validation report that says
precisely what is wrong and where (file, row, field, found value, expected value), separating
**errors**, **warnings** and **missing decisions**. Errors block acceptance. The report is available
as **JSON**, as a **web page** and as a **PDF**, and can be compared with the previous one (fixed,
still open, new). The steward then supplies the mandatory **Dublin Core** metadata (title, language
code, producer, description, licence), chooses the licence from an approved list (CC0 1.0, CC-BY 4.0,
CC-BY-SA 4.0), applies safe formatting fixes, **approves** the result and exports a **ZIP** package.
The original file is preserved byte for byte (checked with a checksum), and every fix is a separate,
logged revision.

```
CSV / JSONL ──► validate ──► report: JSON · web · PDF  (errors · warnings · missing decisions)
                                 │        ▲
                                 │        └── compare with the previous report
                                 ▼
          steward adds Dublin Core metadata + licence, applies safe fixes (each one a revision)
                                 │
                                 ▼
                     steward approves the package
                                 │
                                 ▼
   <resource>_<version>.zip = data + metadata + README + licence + reports + revision history
   (original file kept byte for byte, checksum included)
```

**Epics (V1):** E1 Validation · E2 Reporting · E3 Metadata and licences · E4 Preservation and
revisions · E5 Export. Confirmed client requirements CR-01 to CR-12 are listed in the
[product vision](docs/product/vision.md#5-scope-in-version-1).

**Out of scope (V1):** uploading packages to CLARIAH or any other repository; FAIR certification;
automatic licence detection or legal advice; a universal validator for every format or schema; very
large files (a size limit is documented); a full web application with user roles, permissions and
e-mail notifications; Excel or ZIP files as input; training and community channels.

## The team

| Member | Background | Belbin (P / M) | Role in sprint 1 | Looks after |
|---|---|---|---|---|
| **Ali Faraz** | BSc Computer Science | Coordinator / Monitor Evaluator | **Product Owner** | Leads every conversation with the client; approves and orders the final user stories; the vision and the demo |
| **Ángela Garrido** | Translation and Interpreting (German and French) | Resource Investigator / Shaper | **Scrum Master** | Communicates the tasks, logs the working hours, internal communication; the board, the sprint plan and report, the retrospective |
| **Olga** | Linguistics / data analysis | Completer Finisher / Coordinator | Developer | Client interview guide; reviews the user stories and the technical parts of the vision (clear, buildable and testable) |
| **Marta Salvatierra** | Spanish and English Philology | Completer Finisher / Teamworker | Developer | Client meeting logs and transcripts; turns Jon's confirmed needs into user stories; the requirements document; reviews the wording of our documents; supports the Scrum Master |
| **Garazi Garrido** | Artificial Intelligence | Resource Investigator / Specialist | Developer | GitHub set-up (repository, folders, board) and teaching the team to use it; GitHub issues from the user stories; reviews the risk register and creates the mitigation issues; sample data and licences; this README |

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
  - *Implementer* → the Scrum Master splits the work into small tasks on the board, each with an
    owner and a deadline.
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
| **Communication** | Work and decisions in **GitHub issues**; logistics in the WhatsApp group and by e-mail. We answer within **2 hours** during working hours (Mon–Fri, 10:00–14:00), otherwise on the next working day. |
| **Availability** | About **15 hours per member in sprint 1** (≈ 7 h/week). Exact hours are set in each sprint plan. |
| **Decisions** | Majority vote of the whole team, giving weight to each member's expertise on the topic (linguistic or technical). On a tie, the Scrum Master decides. Every decision is written in the related issue. |
| **Tasks** | The Scrum Master assigns tasks in consensus with the team (role, skills, availability). Each task logs **estimated** and **real** hours. |
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
| [`docs/requirements/`](docs/requirements/) | Stakeholders, use cases, constraints | Marta |
| [`docs/uml/`](docs/uml/) | Component diagram and deployment diagram | &lt;owner&gt; |
| [`docs/risks/`](docs/risks/) | Risk register and mitigation issues | Garazi (review and issues) |
| [`docs/sprints/`](docs/sprints/) | Sprint plan, sprint report and retrospective, one set per sprint | Ángela (SM) |
| [`docs/board/`](docs/board/) | How we use the GitHub project board, with a snapshot | Ángela (SM) · Garazi (set-up) |
| [`data/README.md`](data/README.md) | Sample datasets recommended by Jon (20 Newsgroups, OMW, NLTK) and their licences (the data itself is not committed) | Garazi |
| [`src/`](src/) | Python skeleton: one module per component of the diagram, nothing implemented yet | developers |
| [`scripts/`](scripts/) | Helper scripts | developers |
| [`.github/`](.github/) | Issue templates (user story, task) and pull request template | Garazi |

## Sprint 1 checklist

Deliverables for the **Sprint 1 review (S06, 17 November)**.

| Deliverable | File | Owner | Status |
|---|---|---|---|
| Team charter | [`docs/team/team-charter.md`](docs/team/team-charter.md) | whole team | ✅ done |
| Product vision | [`docs/product/vision.md`](docs/product/vision.md) | Ali | ✅ done |
| Client conversation logs with confirmed requirements | [`docs/client/`](docs/client/) | Marta | ⬜ to do |
| 10 to 15 user stories as issues | [`docs/backlog/product-backlog.md`](docs/backlog/product-backlog.md) + Issues tab | Marta · Ali · Garazi | ⬜ to do |
| Requirements (use cases, stories, constraints) | [`docs/requirements/requirements.md`](docs/requirements/requirements.md) | Garazi |  ✅ done |
| Architecture (component and deployment diagrams) | [`docs/uml/`](docs/uml/) | &lt;owner&gt; | ⬜ to do |
| Risk register | [`docs/risks/risks.md`](docs/risks/risks.md) | Garazi | 🔄 in progress |
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
  The [board](https://github.com/users/garazigg/projects/4/views/1) shows where each one is.
- Each issue records the estimated and the real hours of the task.
- Commits, issues, pull requests and documents are written in English. Pull requests that used AI
  include an `AI use: …` line.

## Data, keys and external services

- Keys and data never enter the repository: `.env` and `data/` are ignored (except
  `data/README.md`). `.env.example` lists the variables without values.
- The application runs entirely on CPU and needs no external service. If the optional Latxa API is
  used, its responses are recorded once and replayed in tests and in the demonstration, so nothing
  depends on a live service.
- Only instructor-provided, instructor-approved or client-recommended data is processed, after
  checking the licence of the exact files in [`data/README.md`](data/README.md).
