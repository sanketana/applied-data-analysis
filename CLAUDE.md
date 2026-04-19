# CLAUDE.md

> **Read this at the start of every Claude Code session on this repo.** It encodes the design decisions, quality bar, and conventions already agreed — so you don't have to re-derive them.

---

## What this repo is

A curriculum repository for **Sanketana School of Code's Applied Data Analysis Track** — a 16-session, 1-hour-per-session, 1:1 or 1:2 live-instructed program that takes a beginner with no Python background to producing a research-grade mini-analysis on NHANES (CDC's National Health and Nutrition Examination Survey) data.

**Primary audience of this repo:** curriculum designers and instructors (Sanketana staff).
**Not for learners.** Learners interact with the track through their own Google Drive folder — files from this repo get copied into their folder weekly.

---

## Track design (immutable — don't deviate without explicit confirmation)

### Who it's for
- Adult or motivated high-school learners with **zero to minimal Python background**
- Learners who want to use data analysis for **health research** (their own, or to mentor students doing research projects)
- Learners who value **depth over breadth** — would rather master a narrow workflow than skim many tools

### What success looks like (Section 3 of the brief)
By end of Session 16, the learner can **independently**:
1. Download an NHANES cycle (demographics, labs, questionnaires, examinations)
2. Load XPT/SAS-format files into Python
3. Merge datasets correctly using SEQN (respondent ID)
4. Handle NHANES-specific missing data conventions
5. Compute descriptive statistics grouped by demographic variables
6. Produce research-grade visualizations (matplotlib/seaborn)
7. Formulate a research question, execute the analysis, and produce a shareable output

The final deliverable per learner is a **mini-research project**, not a set of code exercises.

### Curriculum phases
- **Phase 1 (S1–5):** Python for Data — variables, lists/dicts, control flow, functions, CSV basics
- **Phase 2 (S6–9):** Pandas + NHANES — download, read XPT, merge on SEQN, missing data handling
- **Phase 3 (S10–12):** Visualization & descriptive statistics — matplotlib, seaborn, research-grade charts
- **Phase 4 (S13–16):** Applied research — reinforcement + guided mini-project

### Out of scope (do NOT drift into these)
- Inferential statistics (t-tests, ANOVA, regression beyond descriptive)
- Survey-weighted analysis (NHANES's complex sampling design — explicitly set aside)
- Machine learning
- R / RStudio
- Web scraping, APIs (beyond direct NHANES downloads)
- Git version control as a taught topic
- Jupyter-specific workflows beyond basic use

If a learner asks about these, the instructor acknowledges and redirects. Session content never drifts into them.

---

## Pedagogical framework (agreed — don't reinvent)

### Weekly loop
Every session sits inside this 7-day cycle:

1. **Pre-read** (2 days before class, ~30–45 min) — learner alone. Ends with 3 self-check questions.
2. **Pre-session warm-up** (last 5 min before class) — one tiny task to prime environment.
3. **Live session** (60 min, structured — see below).
4. **Post-session consolidation** (same day, ~15 min) — save notebook, 2–3 lines in learning journal.
5. **Homework** (across the week, 2–3 hours) — applies concept to a **new** context, produces one artifact, contains one deliberate stall point.

Total learner time per week: ~1 hr class + 3–4 hrs outside. The ratio is deliberate.

### Live session structure (60 min, same every time)

| Block | Time | What happens | Mode |
|---|---|---|---|
| **A. Warm-up & homework review** | 0:00–0:10 | Learner walks through their homework. "Where did you get stuck?" | Learner-led, instructor listens |
| **B. Concept bridge** | 0:10–0:20 | Instructor live-codes a realistic example of today's new concept. Syntax already covered in pre-read. | Instructor-led live coding |
| **C. Guided hands-on** | 0:20–0:40 | **Learner drives the keyboard.** Instructor asks Socratic questions. | Learner-driven |
| **D. Stretch / stall-point** | 0:40–0:55 | Deliberately engineered pitfall. Collaborative debugging. | Collaborative |
| **E. Wrap & next steps** | 0:55–1:00 | Save, set homework, preview next session. | Instructor-led |

**Non-negotiables:**
- Block C must be ~20 minutes of learner-at-keyboard. Instructor talks <20% of session total.
- Block D must exist in every session. The stall point is pedagogically designed, not incidental.
- If pre-read is skipped, Block B lengthens; if still running short, cut Block D before Block C.

### Three delivery modes & when to use each
- **Guided hands-on (~70%)** — default for Block C. Learner drives.
- **Live coding by instructor (~20%)** — Block B and parts of D. Used sparingly.
- **Slides / whiteboarding (~5–10%)** — only for the handful of concepts where a picture beats code:
  - Session 6–7: NHANES file organization (SEQN linkage diagram)
  - Session 8: merge row-explosion failure mode
  - Session 10: matplotlib figure → axes → artist hierarchy
  - Session 12: research-grade vs. throwaway chart comparison
  - Session 14–15: scoping a research question

### Six pedagogical principles (Section 5 of the brief — memorize these)
1. **Data-first, not syntax-first.** Every concept introduced through a data example.
2. **Real datasets, not toys.** NHANES or realistic approximations. Never "sort this list of numbers."
3. **Research-grade output from day one.** Every session produces a tangible artifact.
4. **Anticipate the stall points.** Design exercises that surface real pitfalls.
5. **Reproducibility, not just results.** Scripts saved, clear names, commented.
6. **Avoid scope creep.** See out-of-scope list above. No silent expansion.

### Known stall points (Section 5.4 — design exercises AROUND these)
- **Sessions 3–4:** Conceptual leap from lists/dicts to DataFrames. Needs explicit bridging.
- **Session 7:** First NHANES merge — often produces unexpected row counts.
- **Sessions 8–9:** Missing data handling — learners silently include missing-coded values in calculations.
- **Session 10:** matplotlib's figure/axes object model is confusing.
- **Sessions 14–15:** Learners pick research questions too broad. Guide toward tractable scope.

---

## Repo structure

```
/curriculum
  /session-01 ... /session-16     One folder per session.
/assets
  /reference-sheets                Starter materials learner extends over the track
  /rubrics                         Final project rubric, etc.
  /troubleshooting                 "I'm stuck" reference
  /learner-facing                  Docs that get copied into learner's Drive folder
/datasets
  /nhanes-samples                  Pre-downloaded small slices for early sessions
```

### Per-session files (standard structure)

Every session folder (S2 onwards) contains exactly these four files:

1. **`pre-read.ipynb`** — Learner reads before class. Introduces syntax/vocabulary. Ends with 3 self-check questions with hidden answers.
2. **`session-notebook-template.ipynb`** — Skeleton used live in class. Scaffolding with `# Your code here` placeholders. **Solutions deliberately blank** — learner types during Block C.
3. **`homework.ipynb`** — Assigned end of session, due before next. Multi-part with reflection cells + hooks to journal and reference sheet.
4. **`instructor-notes.md`** — Full session plan: metadata, learning objective, prerequisites, block-by-block delivery, common mistakes, assessment signals, pacing notes, post-session checklist, future delivery notes section.

**Session 1 is the only exception:** `before-session-1-setup.md` instead of `pre-read.ipynb`, because there's no "session 0."

### Pending: instructor-solutions.ipynb (per session)

Agreed but not yet implemented: each session folder should also have an `instructor-solutions.ipynb` — the expected solutions to every exercise, with instructor comments. Stays in this repo only; **never copied to learner's Drive folder**. Add this for Session 1 and 2 retroactively, and for all new sessions from creation.

---

## Quality bar & style conventions

### For `instructor-notes.md`
- Section structure must match Sessions 1 and 2 exactly (for consistency across instructors)
- Block timings must sum to 60 minutes
- "Common mistakes to watch for" must be specific and pedagogical, not generic
- "Assessment signal" must be observable — what does the instructor *see* or *hear* that confirms understanding
- Always include a "Future delivery notes" empty section at the bottom for instructors to append to

### For `pre-read.ipynb`
- Time estimate stated at top (target: 30–45 min)
- Every concept grounded in health-data context — never abstract
- At least one "tiny exercise" embedded mid-way so the learner is doing, not just reading
- 3 self-check questions at the end, with answers hidden below (reveal pattern: "try first, then peek")
- Tone: patient but not patronizing. Assume intelligent adult with no prior Python.

### For `session-notebook-template.ipynb`
- Opens with the session's learning goal stated plainly
- Includes a quick recap of the pre-read (3–5 cells max)
- Block C exercises use `# Your code here` placeholders — solutions are NEVER pre-filled in the template
- Always ends with the wrap instructions (save, journal, homework)

### For `homework.ipynb`
- Time estimate at top (target: 2–3 hours total)
- 5–7 parts, each ~15–40 min, producing one clear artifact
- At least one reflection markdown cell for learner's own words
- Optional stretch section clearly labeled — previews something from the next session
- Always ends with "Journal + reference sheet" section as the final part

### Voice & tone across all materials
- Direct, warm, specific. No corporate-speak. No false cheerfulness.
- Use "you" for learner-facing content; use "the learner" / "the instructor" in instructor notes
- Avoid em-dashes if possible; prefer sentence breaks
- Never condescend. Assume the learner is smart and motivated.
- Second-person instructor notes are fine ("you'll want to watch for...")

### Data & code conventions
- All health-data examples should use realistic value ranges (ages 18–75, BMI 18–40, BP within physiological bounds)
- Variable names use snake_case and are descriptive (`patient_age`, not `a` or `x`)
- When introducing a new pandas idiom, always show `.head()` / `.shape` / `.dtypes` inspection around it
- Python comments explain **why**, not **what** (the code shows the what)

---

## Weekly instructor workflow (what the instructor does in this repo)

For each upcoming session N:

1. `git pull` to get latest
2. Open `curriculum/session-N/` and read `instructor-notes.md`
3. Copy relevant files into the learner's Drive folder:
   - ✅ `pre-read.ipynb`
   - ✅ `session-notebook-template.ipynb` (renamed to `session-NN-notes.ipynb` for the learner)
   - ✅ `homework.ipynb`
   - ❌ NOT `instructor-notes.md`
   - ❌ NOT `instructor-solutions.ipynb` (when it exists)
4. Share pre-read with learner 2 days before class (WhatsApp nudge + Drive link)
5. Deliver the session per the block plan
6. Post-session: add any useful observations to `instructor-notes.md` → "Future delivery notes" section, commit

---

## Track status

- ✅ **Session 1** — Orientation, first code, first DataFrame (files complete, solutions pending)
- ✅ **Session 2** — Lists/dicts → Pandas columns, single-vs-double brackets stall point (files complete, solutions pending)
- ⏳ **Sessions 3–16** — To design

### Session 3 design (next up)
- **Topic:** Control flow — if/else and loops — applied to the patient CSV
- **Pre-read covers:** if/else syntax, for loops over lists, comparison operators, boolean logic
- **Live session focus:** Using control flow for data filtering; bridges to the boolean-filtering stretch from Session 2 homework ("remember that weird `df[df['sex']=='M']` thing? Here's why it works")
- **Stall point:** Likely the difference between iterating with a Python loop vs. using pandas vectorized operations — learner will want to loop through DataFrame rows (common beginner trap); we show them the pandas way is both faster and more readable
- **Homework artifact:** A short filter-and-summarize exercise producing a group comparison (e.g., mean BP by sex, mean weight by age bracket)

### Sessions 4–16 (outline only — full design pending)
- **S4:** Functions — reusable operations. Introduce `def`, parameters, return values. Build a small health-data utility.
- **S5:** CSV workflow consolidation — the learner takes a messy CSV and produces a clean analysis script. Capstone of Phase 1.
- **S6:** NHANES introduction — file organization, XPT format, first download. Pre-read includes CDC site navigation.
- **S7:** **Big stall point session.** First merge on SEQN. Design to surface row-explosion.
- **S8:** Missing data — NHANES's specific codes. Design exercise that breaks if learner doesn't handle them.
- **S9:** Derived columns + groupby. Phase 2 capstone: mean BMI by income bracket, or equivalent.
- **S10:** matplotlib fundamentals — figure/axes model. Use the diagram.
- **S11:** seaborn for statistical visualization. **Research question drafting begins here.**
- **S12:** Research-grade styling — labels, legends, dpi, publication quality. Phase 3 capstone.
- **S13:** Flexible reinforcement + research question refinement.
- **S14:** Research question committed. Begin project execution.
- **S15:** Project execution continues. Write-up begins.
- **S16:** Final walk-through with instructor as skeptical reviewer. Defense practice.

---

## When working on this repo

### Good instincts
- When designing a new session, **first read Sessions 1 and 2** to match the style and quality bar
- **Always validate notebooks** (`nbformat.validate`) after generating them — a broken `.ipynb` wastes learner time in class
- **Run code in notebooks mentally** — imagine you're the learner typing this. Does it work? Is the error message helpful if they mistype?
- **Propose the design before generating files.** For a new session: learning objective + stall point + homework artifact, reviewed first, then four files generated.
- **Commit frequently** with descriptive messages: `S07: split merge exercise into two steps, learners stall on SEQN concept`

### Things to avoid
- Don't drift from the block structure. Every session = A/B/C/D/E, 60 min.
- Don't add out-of-scope content even if it seems useful (see out-of-scope list above).
- Don't pre-fill solutions in `session-notebook-template.ipynb` — that kills productive struggle.
- Don't over-explain in instructor notes. Instructors are professionals; they need signal, not hand-holding.
- Don't add emoji or exclamation marks to learner-facing content beyond what Sessions 1 and 2 already use (minimal).
- Don't introduce new pedagogical patterns without flagging the deviation and checking with the maintainer.

### Working rhythm
When the maintainer asks to design a new session:

1. Read the target session's entry in the Sessions 4–16 outline above
2. Read Sessions 1 and 2 for style reference
3. Propose: learning objective, block-by-block outline, stall point, homework artifact
4. Wait for review
5. Generate all four files (or five, once solutions notebooks are added as standard)
6. Validate notebooks
7. Suggest a commit message
8. Update this file's "Track status" section

---

## Useful commands

```bash
# Validate a notebook
python3 -c "import nbformat; nbformat.validate(nbformat.read('path/to/notebook.ipynb', as_version=4))"

# Normalize a notebook (add cell IDs, silence warnings)
python3 -c "import nbformat; nb = nbformat.read('path.ipynb', as_version=4); _, nb = nbformat.validator.normalize(nb); nbformat.write(nb, 'path.ipynb')"

# Standard weekly workflow
git pull
# ... work ...
git add .
git commit -m "SNN: <specific description of change>"
git push
```

---

## References (external — not in this repo)

- Track handover document (Abhinav maintains separately) — the authoritative design brief
- NHANES public data: https://wwwn.cdc.gov/nchs/nhanes
- Sanketana internal pedagogy docs (if any exist)

---

*Last updated: with Session 2 completion. Update the "Track status" section whenever a session is completed or the design outline changes.*
