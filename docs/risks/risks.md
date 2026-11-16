# Risk register · CLARIAH Resource Builder

Project P4 · Software Project · Master HAP/LAP · EHU · 2026-27 · **Team 2**
Written by: Garazi Garrido · Reviewed by: Marta Salvatierra · Approved by: Ali Faraz (PO)
Status: **draft** · Last update: 16 November 2026

> AI use: drafted with the help of an AI assistant (Claude) and reviewed by the team.

## How we use this register

- Every risk has an **owner**, who watches it and acts if it happens.
- Every risk with a score of **4 or more** has a **mitigation issue** in GitHub (label `risk`),
  created by Garazi and linked in the last column.
- The register is reviewed at the **start and end of each sprint** (sprint planning and
  retrospective). Changes are recorded in the [review log](#review-log).

**Scale**

| Value | Probability | Impact |
|---|---|---|
| 1 | Low: unlikely in this course | Low: small delay, easy to fix |
| 2 | Medium: could happen | Medium: a deliverable is late or incomplete |
| 3 | High: likely to happen | High: the sprint goal or the product is at risk |

**Score = Probability × Impact** · 1–2 🟢 low · 3–4 🟡 medium · 6–9 🔴 high

## Risks

| ID | Risk | Category | P | I | Score | Mitigation (prevent) | Contingency (if it happens) | Owner | Status | Issue |
|---|---|---|---|---|---|---|---|---|---|---|
| R-01 | Requirements are not confirmed by Jon before he stops being available (17 Nov), so stories rest on assumptions | Client | 3 | 3 | 🔴 9 | Prepare the questions in advance (interview guide, requirements §7); ask the most important first; log every answer as a `CR-nn` | Mark unconfirmed items as assumptions in the backlog and validate them at the review | Ali | open | to create |
| R-02 | Some members are not yet comfortable with GitHub (issues, board, branches, pull requests) | Process | 3 | 2 | 🔴 6 | Garazi gives a short GitHub session; step-by-step guide in `docs/board/`; stand-ups copied to GitHub by the SM meanwhile | Pair a member with Garazi for their first commits and pull requests | Garazi | open | to create |
| R-03 | Misunderstandings because of different backgrounds, cultures and levels of English | Team | 2 | 2 | 🟡 4 | Decisions written in English in the issues; ask instead of assuming; help members who do not master English | Clarify in the moment, focusing on the work (team charter §6) | Ángela | open | to create |
| R-04 | A member falls behind, stops answering or misses a deadline | Team | 2 | 3 | 🔴 6 | Internal deadlines before the official ones; progress shared in WhatsApp; warn in advance | The SM follows up and the task is split or shared; if it happens again, the instructors are told | Ángela | open | to create |
| R-05 | Hours are underestimated, so the sprint plan cannot be completed | Process | 3 | 2 | 🔴 6 | Small tasks with estimated hours; real hours logged in each issue; ~15 h per member in sprint 1 | Move the lowest-priority stories back to the backlog | Ángela | open | to create |
| R-06 | Scope creep: trying to support too many formats or schemas (out of scope in the brief) | Product | 2 | 3 | 🔴 6 | Fixed list of supported formats confirmed with Jon; out-of-scope list in the requirements | The PO cuts the extra work and sends it to the backlog | Ali | open | to create |
| R-07 | The original file is modified or lost by a bug | Product / data | 2 | 3 | 🔴 6 | Original stored read-only with a checksum; every transformation creates a new revision; automated test that compares checksums | Restore from the stored original; report the bug as an issue with priority | Garazi | open | to create |
| R-08 | Data without approval or with an unclear licence is used in the project | Legal / data | 1 | 3 | 🟡 3 | Only instructor-provided or approved data; each sample file listed in `data/README.md` with its source and licence | Remove the file from the work and from the history, and tell the instructors | Garazi | open | — |
| R-09 | A wrong licence is assigned to a resource in a package | Legal / product | 2 | 3 | 🔴 6 | Licence never inferred; chosen by a person from an approved list confirmed by Jon; export blocked without it | Regenerate the package with the correct licence; the history shows the change | Garazi | open | to create |
| R-10 | Keys or data are committed to the repository | Security | 1 | 3 | 🟡 3 | `.env` and `data/` in `.gitignore`; `.env.example` without values; check in pull request review | Revoke the key immediately and remove it from the history | Garazi | open | — |
| R-11 | The optional Latxa API is unavailable, slow or gives different answers | Technical | 2 | 2 | 🟡 4 | Product works without it (CPU only); responses recorded once and replayed in tests and demo | Disable the Latxa feature; the rest of the tool still works | Garazi | open | to create |
| R-12 | Large files make validation too slow or break the tool | Technical | 2 | 2 | 🟡 4 | Documented size limit, confirmed with Jon; test with a file at the limit | Reject the file with a clear message | Garazi | open | to create |
| R-13 | Not every member understands the architecture well enough to explain it at the reviews | Team | 2 | 2 | 🟡 4 | Diagrams explained in a team meeting; each member presents one part before the review | Rehearsal of the review the day before | Olga | open | to create |
| R-14 | AI-generated content contains errors or is not understood by its author | Quality | 2 | 2 | 🟡 4 | Each member reviews what they commit and can explain it; `AI use: …` line; peer review in pull requests | Correct the content and note it in the retrospective | whole team | open | to create |
| R-15 | Nobody turns plans into concrete steps (no Implementer in the team) | Team | 2 | 2 | 🟡 4 | The SM splits the work into small tasks on the board, each with an owner and a deadline | Re-plan in the next stand-up | Ángela | open | to create |

## Top risks this sprint

1. **R-01** · Requirements not confirmed by Jon in time.
2. **R-02** · GitHub learning curve.
3. **R-04** · Different working rhythms.

## Review log

| Date | Sprint | Change | By |
|---|---|---|---|
| 16 November 2026 | 1 | Register created | Garazi Garrido |
