# How we use the project board · Team 2

Project P4 · CLARIAH Resource Builder · Software Project · Master HAP/LAP · EHU · 2026-27
Written by: Garazi Garrido · Reviewed by: Ángela Garrido (SM) · Last update: 19 November 2026

> AI use: drafted with the help of an AI assistant (Claude) and reviewed by the team.

**Board:** <https://github.com/users/garazigg/projects/4/views/1>

## 1. What the board is

The board is a GitHub project (built from the *Team planning* template) that shows every piece of
work of the team as a card. Each card is a **GitHub issue**: a user story, a task or a risk
mitigation. Looking at the board, anyone can see what is planned, what is being done, what is
being reviewed and what is finished, and who is doing it.

All the issues of the [product backlog](../backlog/product-backlog.md) are on the board: 12 user
stories (US-01 to US-12, issues #16 to #27) traced to the requirements CR-01 to CR-12 confirmed in
Meeting 5, and 2 supporting tasks (T-01 and T-02, issues #28 and #29).

## 2. Columns

| Column | Meaning | Who moves the card here |
|---|---|---|
| **Backlog** | In the product backlog, not planned for the current sprint yet | Product Owner, when a story is created or moved out of a sprint |
| **Ready** | Planned for the current sprint and ready to start: acceptance criteria clear, points voted, tasks listed | Scrum Master, at sprint planning |
| **In progress** | Somebody is working on it now | The owner, when they start |
| **In review** | Work finished and waiting for review: a pull request reviewed by a member who did not write it, and the acceptance criteria shown to the Product Owner | The owner, when they open the pull request |
| **Done** | Reviewed, merged and meets the definition of done | The reviewer, after the pull request is merged and the PO has accepted it |

The number at the top of each column shows how many cards it holds and its limit (e.g. `0 / 5`).
**In progress** has a limit of one card per member (5), so that work is finished before new work
starts. The other columns have no limit.

## 3. Sprints and epics

Each sprint is a GitHub **milestone** (*Issues → Milestones*), and each sprint delivers one epic:

| Milestone | Epic | Issues |
|---|---|---|
| Sprint 1 | E1 · One file end to end (CLI) | US-01 to US-07 (#16–#22), T-01 (#28), T-02 (#29) |
| Sprint 2 | E2 · Agreement between two annotation files | US-08 to US-10 (#23–#25) |
| Sprint 3 | E3 · Better agreement measures and web interface | US-11, US-12 (#26–#27) |

At sprint planning, the Scrum Master moves the issues of the sprint's milestone from **Backlog**
to **Ready**. A story that is not finished at the end of a sprint stays open, moves to the next
milestone and goes back to **Ready**.

## 4. Fields and views

Every card has these project fields, filled in at sprint planning:

| Field | What we write | Who |
|---|---|---|
| **Estimate** | Story points (1, 2, 3, 5 or 8), the same as in *Planning* in the issue and in the backlog. Tasks have no points. The top of each column shows the sum. | The team votes; the SM writes it |
| **Priority** | P0 = `must`, P1 = `should`, P2 = `could`, the same as the priority label | Product Owner |
| **Assignees** | The owner of the card | The owner |

On the cards we also show the **labels** and the **milestone** (*View → Fields*).

Views (tabs at the top of the board):

| View | What it is for |
|---|---|
| **Backlog** | The main board with the five columns |
| **Priority board** | The same cards grouped by priority |
| **Team items** | A table with every card, its owner and its fields |
| **Roadmap** | The cards on a timeline, by sprint |
| **My items** | Only the cards assigned to me |

## 5. Types of card

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

## 6. Rules

1. **One owner per card.** The owner is set in *Assignees*.
2. **Signing up for tasks.** Each member signs up for a task by writing their GitHub user in its
   checklist line (`@user`). The Scrum Master checks at sprint planning that the work is shared out
   in consensus with the team (role, skills, availability). While we are learning GitHub, the
   Scrum Master creates and moves the cards; afterwards each member moves their own.
3. **Hours.** Every task line already carries its **estimated hours**. When a task is finished,
   the owner ticks it and adds the **real hours** in a comment on the issue
   (e.g. `T: core submit function · est. 4h · real 5h`).
4. **Points.** The points of each story are voted by the team at sprint planning and written in
   *Estimate* on the board, in *Planning* in the issue and in the backlog.
5. **Maximum 2 cards in *In progress* per person**, and never more cards in the column than its
   limit.
6. **Review by someone else.** A card in *In review* is reviewed by a member who did not write it.
7. **Done means done.** A card goes to *Done* only when all its tasks are ticked, its acceptance
   criteria have been shown to the Product Owner, it meets the definition of done in the
   [sprint plan](../sprints/sprint-1-plan.pdf), and its result is in the repository and linked
   from the issue.
8. **Decisions** about a card are written as comments in its issue, in English.
9. **Stand-ups** are posted in the issue *"Stand-ups Sprint 1"*: what I did, what I will do,
   what is blocking me.

## 7. Step by step

**Create a card**

1. Go to **Issues → New issue** and choose the template (*User story* or *Task*).
2. Fill the title and the template, add the labels, the milestone of the sprint and yourself (or
   the owner) in *Assignees*.
3. In *Projects*, choose our board. The card appears in **Backlog**.
4. Open the card on the board and fill *Estimate* and *Priority*.

**Work on a card**

1. Open the board and drag your card from **Ready** to **In progress**.
2. Tick each task when it is done and write its real hours in a comment.
3. When you finish, open a pull request with `Closes #<n>`, link the result in the issue and drag
   the card to **In review**.
4. The reviewer checks the pull request; the owner shows the acceptance criteria to the Product
   Owner.
5. When the pull request is merged (the issue closes automatically) and the PO has accepted it,
   the reviewer drags the card to **Done**.

## 8. Snapshot

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
| 19 November 2026 | Updated to the real board (*Team planning* template): five columns (Backlog, Ready, In progress, In review, Done), column limits, *Estimate* and *Priority* fields, views; all backlog issues are on the board | Garazi Garrido |
