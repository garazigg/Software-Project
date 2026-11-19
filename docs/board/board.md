# How we use the project board · Team 2

Project P4 · CLARIAH Resource Builder · Software Project · Master HAP/LAP · EHU · 2026-27
Written by: Garazi Garrido · Reviewed by: Ángela Garrido (SM) · Last update: 19 November 2026

> AI use: drafted with the help of an AI assistant (Claude) and reviewed by the team.

**Board:** <https://github.com/users/garazigg/projects/4/views/1>

## 1. What the board is

The board shows every piece of work of the team as a card. Each card is a **GitHub issue**: a user
story, a task or a risk mitigation. Looking at the board, anyone can see what is planned, what is
being done and what is finished, and who is doing it.

The issues come from the [product backlog](../backlog/product-backlog.md): 12 user stories
(US-01 to US-12, issues #16 to #27) traced to the requirements CR-01 to CR-12 confirmed in
Meeting 5, and 2 supporting tasks (T-01 and T-02, issues #28 and #29).

## 2. Columns

| Column | Meaning | Who moves the card here |
|---|---|---|
| **Todo** | Planned for this sprint, not started yet | Scrum Master, at sprint planning |
| **In Progress** | Somebody is working on it now | The owner, when they start |
| **Done** | Finished and meets the definition of done | The owner, when it is finished |

Only the issues of the **current sprint** are on the board. The others stay in the product
backlog ([`docs/backlog/`](../backlog/)) and in their milestone until their sprint is planned.

## 3. Sprints and epics

Each sprint is a GitHub **milestone** (*Issues → Milestones*), and each sprint delivers one epic:

| Milestone | Epic | Issues |
|---|---|---|
| Sprint 1 | E1 · One file end to end (CLI) | US-01 to US-07 (#16–#22), T-01 (#28), T-02 (#29) |
| Sprint 2 | E2 · Agreement between two annotation files | US-08 to US-10 (#23–#25) |
| Sprint 3 | E3 · Better agreement measures and web interface | US-11, US-12 (#26–#27) |

At sprint planning, the Scrum Master adds the issues of the sprint's milestone to the board.
A story that is not finished stays open and moves to the next milestone.

## 4. Types of card

| Type | Template | Labels | Title |
|---|---|---|---|
| User story | *User story* | `story` + priority (`must`, `should`, `could`) + epic (`E1`, `E2`, `E3`) | `US-xx · <short name>` |
| Task | *Task* | `task` | `T-xx · <verb> <what>` |
| Risk mitigation | *Task* | `risk` | `R-xx · Mitigate: <what>` |

The priority label is set by the Product Owner. The epic label must match the epic of the story in
the backlog.

**Tasks of a story.** The tasks that build a story (2 to 8 hours each) are the checklist in the
*Tasks* section of the story issue, not separate cards. A separate task card is only for work with
no direct user value (data, set-up, documentation) or for a risk mitigation. If such a task belongs
to a story or a risk, write `Part of #<n>` in its description.

## 5. Rules

1. **One owner per card.** The owner is set in *Assignees*.
2. **Signing up for tasks.** Each member signs up for a task by writing their GitHub user in its
   checklist line (`@user`). The Scrum Master checks at sprint planning that the work is shared out
   in consensus with the team (role, skills, availability). While we are learning GitHub, the
   Scrum Master creates and moves the cards; afterwards each member moves their own.
3. **Hours.** Every task line already carries its **estimated hours**. When a task is finished,
   the owner ticks it and adds the **real hours** in a comment on the issue
   (e.g. `T: core submit function · est. 4h · real 5h`).
4. **Points.** The points of each story are in *Planning*. They are voted by the team at sprint
   planning and updated in the issue and in the backlog.
5. **Maximum 2 cards in *In Progress* per person**, so that work is finished before new work
   starts.
6. **Done means done.** A card goes to *Done* only when all its tasks are ticked, its acceptance
   criteria have been shown to the Product Owner, it meets the definition of done in the
   [sprint plan](../sprints/sprint-1-plan.pdf), and its result is in the repository and linked
   from the issue.
7. **Decisions** about a card are written as comments in its issue, in English.
8. **Stand-ups** are posted in the issue *"Stand-ups Sprint 1"*: what I did, what I will do,
   what is blocking me.

## 6. Step by step

**Create a card**

1. Go to **Issues → New issue** and choose the template (*User story* or *Task*).
2. Fill the title and the template, add the labels, the milestone of the sprint and yourself (or
   the owner) in *Assignees*.
3. In *Projects*, choose our board. The card appears in **Todo**.

**Work on a card**

1. Open the board and drag your card to **In Progress**.
2. Tick each task when it is done and write its real hours in a comment.
3. When you finish, link the result (file or pull request) and drag the card to **Done**.
4. If a pull request finishes the issue, write `Closes #<n>` in the pull request: the issue
   closes automatically when it is merged.

## 7. Snapshot

Snapshot of the board at the end of each sprint, for the sprint report.

| Sprint | Date | Snapshot |
|---|---|---|
| 1 | <date of the review> | ![Board at the end of sprint 1](board-sprint-1.png) |
| 2 | <date of the review> | ![Board at the end of sprint 2](board-sprint-2.png) |
| 3 | <date of the review> | ![Board at the end of sprint 3](board-sprint-3.png) |

## Change log

| Date | Change | By |
|---|---|---|
| 16 November 2026 | Board guide created | Garazi Garrido |
| 19 November 2026 | Updated for the Meeting 5 backlog: issues #16 to #29, sprints as milestones (one epic each), priority and epic labels, story tasks as checklists with sign-up, task titles `T-xx` | Garazi Garrido |
