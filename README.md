# Sanketana — Applied Data Analysis Track

> **Audience for this repo:** curriculum designers and instructors at Sanketana School of Code.
> **Not for learners.** Learners interact with the track through their own Google Drive folder (see `assets/learner-facing/start-here.md` for what they see).

---

## What this track is

A 16-session, 1-hour-per-session, 1:1 or 1:2 track that takes a beginner with no Python background to producing a research-grade mini-analysis on NHANES (CDC's National Health and Nutrition Examination Survey) data.

Full design brief: see the track handover document (external).

## Working with Claude Code on this repo

A `CLAUDE.md` file at the repo root encodes all design decisions, pedagogical framework, style conventions, and track status. When starting a Claude Code session in this repo, Claude Code reads it automatically. If you're editing any part of the curriculum, read `CLAUDE.md` first.

## Repo structure

```
/curriculum
  /session-01 ... /session-16     One folder per session. Each contains:
    pre-read.ipynb                 Learner reads before the session (~30–45 min)
    classwork-template.ipynb           Skeleton used during the live session
    classwork-solution.ipynb           Instructor solutions (never shared with learner)
    homework.ipynb                 Assigned at end of session, due before next
    instructor-notes.md            Pedagogical guidance, stall points, common pitfalls

/assets
  /reference-sheets                Living docs the learner accumulates (pandas idioms, NHANES quirks)
  /rubrics                         Final project rubric, homework review rubric
  /troubleshooting                 "I'm stuck — try this first" guide
  /learner-facing                  Docs that get copied into the learner's Drive folder
                                   (start-here, track-overview, how-this-course-works)

/datasets
  /nhanes-samples                  Pre-downloaded small NHANES slices for early sessions
                                   (full NHANES downloads happen live from Session 6 onward)
```

## Weekly instructor workflow

For each upcoming session N:

1. Pull latest from this repo: `git pull`
2. Open `curriculum/session-N/` and review `instructor-notes.md`
3. Copy the session-N folder into the learner's Drive folder (`/session-N/`)
4. Share pre-read with learner 2 days before class (WhatsApp nudge + Drive link)
5. After class: copy homework template into learner's folder, set expectations
6. Post-session: if anything in the session needs updating, edit the files here and commit

## Versioning principle

Every change to a session's content goes through a commit. The commit message names the reason (e.g., `S07: split merge exercise into two steps, learners stalling on SEQN concept`). This is how the curriculum improves cohort-over-cohort.

## Track status

- ✅ Session 1 — complete
- ✅ Session 2 — complete
- ⏳ Sessions 3–16 — in design

---

*Maintained by Sanketana School of Code.*
