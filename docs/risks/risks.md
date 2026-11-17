# Risk register · CLARIAH Resource Builder

Project P4 · Software Project · Master HAP/LAP · EHU · 2026-27 · **Team 2**
Written by: Garazi Garrido · Reviewed by: Marta Salvatierra · Approved by: Ali Faraz (PO)
Status: **draft** · Last update: 17 November 2026

> AI use: drafted with the help of an AI assistant (Claude) and reviewed by the team.

## How we use this register

- Every risk has an **owner**, who watches it and acts if it happens.
- Risks that need a specific action this sprint have a **mitigation issue** in GitHub
  (label `risk`), created by Garazi and linked in the last column. The other risks are covered
  by our normal way of working (stand-ups, hours log, pull request reviews).
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
| R-01 | Requirements are not confirmed by Jon before he stops being available (17 Nov), so stories rest on assumptions | Client | 1 | 3 | 🟡 3 | Prepare the questions in advance (interview guide, requirements §7); ask the most important first; log every answer as a `CR-nn` | Mark unconfirmed items as assumptions in the backlog and validate them at the review | Ali | mitigated: CR-01 to CR-12 confirmed (product vision §5); a few details still open (requirements §7) | to create |
| R-02 | Some members are not yet comfortable with GitHub (issues, board, branches, pull requests) | Process | 3 | 2 | 🔴 6 | Garazi gives a short GitHub session; step-by-step guide in `docs/board/`; stand-ups copied to GitHub by the SM meanwhile | Pair a member with Garazi for their first commits and pull requests | Garazi | open | to create |
| R-03 | Misunderstandings because of different backgrounds, cultures and levels of English | Team | 2 | 2 | 🟡 4 | Decisions written in English in the issues; ask instead of assuming; help members who do not master English | Clarify in the moment, focusing on the work (team charter §6) | Ángela | open | — |
| R-04 | A member falls behind, stops answering or misses a deadline | Team | 2 | 3 | 🔴 6 | Internal deadlines before the official ones; progress shared in WhatsApp; warn in advance | The SM follows up and the task is split or shared; if it happens again, the instructors are told | Ángela | open | — |
| R-05 | Hours are underestimated, so the sprint plan cannot be completed | Process | 3 | 2 | 🔴 6 | Small tasks with estimated hours; real hours logged in each issue; ~15 h per member in sprint 1 | Move the lowest-priority stories back to the backlog | Ángela | open | — |
| R-06 | Scope creep: trying to support too many formats or schemas (out of scope in the brief) | Product | 1 | 3 | 🟡 3 | Input limited to CSV and JSONL, metadata to Dublin Core (confirmed with Jon); out-of-scope list in the product vision §6 | The PO cuts the extra work and sends it to the backlog | Ali | mitigated | — |
| R-07 | The original file is modified or lost by a bug | Product / data | 2 | 3 | 🔴 6 | Original stored read-only with a checksum; every transformation creates a new revision; automated test that compares checksums | Restore from the stored original; report the bug as an issue with priority | Garazi | open | — |
| R-08 | Data without approval or with an unclear licence is used in the project (Jon warned that some OMW languages and other NLTK corpora have different terms) | Legal / data | 2 | 3 | 🔴 6 | Only the datasets recommended by Jon or approved by the instructors; the licence of the exact version and files is checked and marked in `data/README.md` before use | Remove the file from the work and from the history, and tell the instructors | Garazi | open | — |
| R-09 | A wrong licence or access category is assigned to a resource in a package | Legal / product | 2 | 3 | 🔴 6 | Licence never inferred; chosen by a person from the approved list confirmed by Jon (CC0 1.0, CC-BY 4.0, CC-BY-SA 4.0); access category derived from the CLARIAH policy table; explicit approval before export | Regenerate the package with the correct licence; the history shows the change | Garazi | open | to create |
| R-10 | Keys or data are committed to the repository | Security | 1 | 3 | 🟡 3 | `.env` and `data/` in `.gitignore`; `.env.example` without values; check in pull request review | Revoke the key immediately and remove it from the history | Garazi | open | — |
| R-11 | The optional Latxa API is unavailable, slow or gives different answers | Technical | 2 | 2 | 🟡 4 | Product works without it (CPU only); responses recorded once and replayed in tests and demo | Disable the Latxa feature; the rest of the tool still works | Garazi | open | — |
| R-12 | Large files make validation too slow or break the tool | Technical | 2 | 2 | 🟡 4 | Size limit chosen and documented by the team (files up to 1 GB are out of scope in V1); test with a file at the limit | Reject the file with a clear message | Garazi | open | — |
| R-13 | Not every member understands the architecture well enough to explain it at the reviews | Team | 2 | 2 | 🟡 4 | Diagrams explained in a team meeting; each member presents one part before the review | Rehearsal of the review the day before | Olga | open | — |
| R-14 | AI-generated content contains errors or is not understood by its author | Quality | 2 | 2 | 🟡 4 | Each member reviews what they commit and can explain it; `AI use: …` line; peer review in pull requests | Correct the content and note it in the retrospective | whole team | open | — |
| R-15 | Nobody turns plans into concrete steps (no Implementer in the team) | Team | 2 | 2 | 🟡 4 | The SM splits the work into small tasks on the board, each with an owner and a deadline | Re-plan in the next stand-up | Ángela | open | — |
| R-16 | Producing the report in three formats (JSON, web page, PDF) takes more effort than planned or adds a heavy PDF dependency | Technical | 2 | 2 | 🟡 4 | Build JSON first and generate the web page and the PDF from the same HTML template with one light library | Deliver JSON + web page first; PDF moves to the next sprint after agreement with the PO | Garazi | open | — |

## Top risks this sprint

1. **R-02** · GitHub learning curve.
2. **R-04** · Different working rhythms.
3. **R-08** · Licences of the sample datasets.

## Review log

| Date | Sprint | Change | By |
|---|---|---|---|
| 16 November 2026 | 1 | Register created | Garazi Garrido |
| 17 November 2026 | 1 | Updated with the product vision v1.1: R-01 and R-06 mitigated; R-08, R-09 and R-12 updated; R-16 added | Garazi Garrido |
