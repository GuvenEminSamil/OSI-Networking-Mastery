# Question Bank

> This folder contains practice tests. The “Check Your Understanding” questions inside lesson files are short warm-ups; question-bank tests are used for larger knowledge checks.

## Structure

| Folder | Area code | Coverage |
|---|---|---|
| `FOUNDATIONS/` | FND | 00-01 – 00-09 |
| `PHYSICAL/` | PHY | 01-* |
| `DATA-LINK/` | DL | 02-* |
| `NETWORK/` | NET | 03-* |
| `TRANSPORT/` | TRN | 04-* |
| `SESSION/`, `PRESENTATION/`, `APPLICATION/` | SES, PRS, APP | 05-*, 06-*, 07-* |
| `SECURITY/`, `OPERATIONS/` | SEC, OPS | 14-*, 15-* |
| `COMPREHENSIVE-EXAMS/` | CE | CE-00 – CE-06 |

Each question file has a separate answer file under `answers/`. Question IDs use the format `<AREA>-<TOPIC>-NNN`, for example `FND-OSI-004`.

## Question Categories

| Code | Category | What it measures |
|---|---|---|
| B | Basic understanding | Correct definition and role of a concept |
| O | Intermediate technical | Calculations, field values, behaviour, or command output |
| I | Advanced reasoning | Cause and effect; “what changes if…” |
| S | Real-world scenario | Applying knowledge to a described network |
| A | Troubleshooting | Finding likely causes from symptoms |
| MC | CCNA-style multiple choice | One or multiple correct answers |
| K | Explain in your own words | Open-ended answer scored using a rubric |
| KK | Compare | Which option is appropriate, when, and why |

Difficulty is rated from 1 (basic) to 3 (challenging).

## How to Take a Test

1. Try to complete a test in one sitting without looking at lesson files or the answer key. Do not use a calculator unless the question explicitly allows it.
2. Write your answers on paper or in a separate file. Mark uncertain answers with `?`.
3. When finished, use the answer file to score your work.
4. For every incorrect or uncertain answer, review the linked lesson section.

## Scoring

- Each question is worth **1 point**.
- For multiple-answer MC questions, every required option must be correct to earn the point.
- For multi-part O, I, S, and A questions, parts have equal weight unless stated otherwise.
- K and KK questions use the scoring rubric in the answer key; scores may be awarded in 0.25-point increments.

**Knowledge-check target:** Aim for **at least 85%** in the relevant topic area. Record completed test results in `MY-NOTES/RESULTS.md`.

Example:

```text
| 2026-11-25 | FND (40 questions) | 35/40 | Review: FND-DAT-006, FND-OSI-005 |
```

## Current Files

| File | Questions | Coverage |
|---|---:|---|
| `FOUNDATIONS/Q-FND-DAT.md` | 12 | Information, number systems, Boolean logic, data representation (00-01, 00-02, 00-03, 00-06) |
| `FOUNDATIONS/Q-FND-HW.md` | 9 | Electricity, transistors, computer architecture (00-04, 00-05, 00-07) |
| `FOUNDATIONS/Q-FND-NET.md` | 9 | Networking fundamentals (00-08) |
| `FOUNDATIONS/Q-FND-OSI.md` | 10 | Layered models (00-09) |
| `COMPREHENSIVE-EXAMS/CE-00.md` | 25 | Historical starting-point diagnostic; not a mastery test |
