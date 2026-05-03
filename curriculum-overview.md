# Curriculum Overview — Applied Data Analysis Track

16 sessions, 60 minutes each, 1:2 live instruction. Takes a beginner with no Python background to a research-grade mini-analysis on NHANES data.

---

## Phase 1 — Python for Data (Sessions 1–5)

Build core Python fluency through health-data examples. Every concept is grounded in a patient dataset, never abstract exercises.

| Session | Topic | Key concepts | Stall point |
|---|---|---|---|
| **S1** | Orientation, first code, first DataFrame | Colab environment, variables, data types (`int`, `float`, `str`, `bool`), `print()`, first CSV load | File path + Drive mounting |
| **S2** | Lists, dicts, and DataFrame columns | Lists, dictionaries, `pd.read_csv`, `.head()` / `.shape` / `.columns` / `.dtypes`, column selection | Single vs double bracket (`df['col']` vs `df[['col']]`) |
| **S3** | Control flow — if/else and loops | Comparison operators, boolean logic, `if`/`else`, `for` loops, boolean filtering in pandas | Python loop vs pandas vectorized operations |
| **S4** | Functions — stop repeating yourself | `def`, parameters, `return` vs `print()`, reusable classification functions on patient CSV + NHANES | `print()` vs `return` confusion (`None` result) |
| **S5** | CSV workflow consolidation (Phase 1 capstone) | End-to-end: messy CSV → clean analysis script | — |

**Phase 1 outcome:** The learner can write a Python script that loads a CSV, inspects it, filters rows, computes summary statistics, and produces a clean output.

---

## Phase 2 — Pandas + NHANES (Sessions 6–9)

Transition from synthetic patient CSVs to real CDC data. Introduces the NHANES survey structure and the pandas operations needed to work with it.

| Session | Topic | Key concepts | Stall point |
|---|---|---|---|
| **S6** | NHANES introduction | CDC site navigation, XPT/SAS file format, downloading a cycle, file organization | — |
| **S7** | First NHANES merge | Merging datasets on SEQN (respondent ID), join types, inspecting merge results | Row-explosion from incorrect merge |
| **S8** | Missing data handling | NHANES-specific missing codes, detecting and handling missing values, impact on calculations | Silently including missing-coded values in statistics |
| **S9** | Derived columns + groupby (Phase 2 capstone) | Creating new columns, `.groupby()`, summary tables (e.g., mean BMI by income bracket) | — |

**Phase 2 outcome:** The learner can download an NHANES cycle, merge demographics with lab/exam data on SEQN, handle missing values correctly, and produce grouped summary statistics.

---

## Phase 3 — Visualization and Descriptive Statistics (Sessions 10–12)

Turn analysis results into research-grade visualizations. Research question drafting begins here.

| Session | Topic | Key concepts | Stall point |
|---|---|---|---|
| **S10** | matplotlib fundamentals | Figure/axes object model, basic plot types, labels and titles | matplotlib's figure → axes → artist hierarchy |
| **S11** | seaborn for statistical visualization | Distribution plots, categorical plots, layering on matplotlib. Research question drafting begins | — |
| **S12** | Research-grade styling (Phase 3 capstone) | Labels, legends, DPI, publication-quality formatting, research-grade vs throwaway chart comparison | — |

**Phase 3 outcome:** The learner can produce publication-quality visualizations and has drafted a research question for their final project.

---

## Phase 4 — Applied Research (Sessions 13–16)

Reinforcement and guided execution of a mini-research project. The learner applies everything from Phases 1–3 to an original research question using NHANES data.

| Session | Topic | What happens |
|---|---|---|
| **S13** | Reinforcement + research question refinement | Flexible session to shore up weak spots. Research question reviewed and scoped for feasibility |
| **S14** | Project execution begins | Research question committed. Learner begins analysis with instructor guidance |
| **S15** | Project execution + write-up | Analysis continues. Written narrative and visualizations take shape |
| **S16** | Final walk-through and defense | Instructor plays skeptical reviewer. Learner presents findings and defends methodology |

**Phase 4 outcome:** A completed mini-research project — original research question, NHANES data analysis, research-grade visualizations, and a written summary — ready to share.

---

## Track progression at a glance

```
S1 ─── S2 ─── S3 ─── S4 ─── S5     Phase 1: Python fluency
                                ↓
                              S6 ─── S7 ─── S8 ─── S9     Phase 2: Real data
                                                      ↓
                                                    S10 ── S11 ── S12     Phase 3: Visualization
                                                                    ↓
                                                                  S13 ── S14 ── S15 ── S16     Phase 4: Research
```

**Final deliverable:** A mini-research project, not a set of code exercises.
