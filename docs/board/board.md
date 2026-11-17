# How we use the project board · Team 2

Project P4 · CLARIAH Resource Builder · Software Project · Master HAP/LAP · EHU · 2026-27
Written by: Garazi Garrido · Reviewed by: Ángela Garrido (SM) · Last update: 16 November 2026

> AI use: drafted with the help of an AI assistant (Claude) and reviewed by the team.

**Board:** <https://github.com/users/garazigg/projects/4/views/1>

## 1. What the board is

The board shows every piece of work of the team as a card. Each card is a **GitHub issue**: a user
story, a task or a risk mitigation. Looking at the board, anyone can see what is planned, what is
being done and what is finished, and who is doing it.

## 2. Columns

| Column | Meaning | Who moves the card here |
|---|---|---|
| **Todo** | Planned for this sprint, not started yet | Scrum Master, at sprint planning |
| **In Progress** | Somebody is working on it now | The owner, when they start |
| **Done** | Finished and meets the definition of done | The owner, when it is finished |

Stories that are not planned for the current sprint stay in the product backlog
([`docs/backlog/`](../backlog/)) and are not on the board yet.

## 3. Types of card

| Type | Template | Label | Title |
|---|---|---|---|
| User story | *User story* | `story` | `US-xx · <short name>` |
| Task | *Task* | `task` | `<verb> <what>` |
| Risk mitigation | *Task* | `risk` | `R-xx · Mitigate: <what>` |

Every task belongs to a story or to a risk: write `Part of #<n>` in its description.

## 4. Rules

1. **One owner per card.** The owner is set in *Assignees*.
2. **Assigning tasks.** The Scrum Master assigns the tasks in consensus with the team (role,
   skills, availability). While we are learning GitHub, the Scrum Master creates and moves the
   cards; afterwards each member moves their own.
3. **Hours.** When a task is created, the owner writes the **estimated hours** in *Planning*.
   When it is finished, they add the **real hours** in a comment before moving it to *Done*.
4. **Maximum 2 cards in *In Progress* per person**, so that work is finished before new work
   starts.
5. **Done means done.** A card goes to *Done* only when it meets the definition of done in the
   [sprint plan](../sprints/sprint-1-plan.pdf) and its result is in the repository and linked
   from the issue.
6. **Decisions** about a card are written as comments in its issue, in English.
7. **Stand-ups** are posted in the issue *"Stand-ups Sprint 1"*: what I did, what I will do,
   what is blocking me.

## 5. Step by step

**Create a card**

1. Go to **Issues → New issue** and choose the template (*User story* or *Task*).
2. Fill the title and the template, add the label and yourself (or the owner) in *Assignees*.
3. In *Projects*, choose our board. The card appears in **Todo**.

**Work on a card**

1. Open the board and drag your card to **In Progress**.
2. When you finish, write the real hours in a comment, link the result (file or pull request),
   and drag the card to **Done**.
3. If a pull request finishes the issue, write `Closes #<n>` in the pull request: the issue
   closes automatically when it is merged.

## 6. Snapshot

Snapshot of the board at the end of each sprint, for the sprint report.

| Sprint | Date | Snapshot |
|---|---|---|
| 1 | <date of the review> | ![Board at the end of sprint 1](board-sprint-1.png) |
