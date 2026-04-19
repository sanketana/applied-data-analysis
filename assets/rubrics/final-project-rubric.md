# Final Project Rubric — Applied Data Analysis Track

**You're seeing this on Day 1. That's intentional.** This is what you're building toward over 16 sessions. Refer back to it often. By Session 11, you'll start drafting research questions against it. By Session 16, you'll deliver on it.

---

## What the final project is

A short, self-contained mini-research analysis using NHANES data, completed in Sessions 15–16 and defended in Session 16.

**Components:**
1. A clear research question (one sentence)
2. A merged, cleaned NHANES dataset answering that question
3. 2–3 research-grade charts
4. A short write-up (1–2 pages) explaining what you did and what you found
5. A 5-minute verbal walk-through in Session 16, where the instructor plays skeptical reviewer

**This is your portfolio piece.** It's what you show a teacher, a research mentor, or use to apply for a research program.

---

## Rubric (how we evaluate it)

Each dimension is scored: Emerging / Solid / Research-grade.

### 1. Research question

- **Emerging:** Question is too broad ("How does diet affect health?") or not answerable with NHANES
- **Solid:** Question is specific and answerable ("Is there a relationship between sleep duration and BMI in US adults aged 40–59?")
- **Research-grade:** Question is specific, answerable, *and* motivated — you can explain why it matters and what prior knowledge led you to it

### 2. Data handling

- **Emerging:** Data loads but merging, missing-value handling, or filtering has silent errors
- **Solid:** Merges are correct (row counts verified), missing values explicitly handled, variables correctly interpreted
- **Research-grade:** All of Solid, plus you've documented the NHANES cycle you used, the specific variable codes, and you've noted limitations (e.g., "not using survey weights — results are unweighted")

### 3. Analysis

- **Emerging:** Descriptive stats present but not clearly tied to the question
- **Solid:** Stats directly answer the question, grouped appropriately, reported with uncertainty (mean ± SD, or median/IQR)
- **Research-grade:** All of Solid, plus you've segmented by relevant demographics and noted where findings are consistent vs. inconsistent

### 4. Charts

- **Emerging:** Charts exist but have default matplotlib styling, missing labels, or don't clearly answer the question
- **Solid:** Charts have proper titles, axis labels, legends, appropriate chart type, readable font sizes
- **Research-grade:** All of Solid, plus the chart would be at home in a science fair poster or research paper — deliberate color choices, publication-ready dpi, no chartjunk

### 5. Write-up

- **Emerging:** Describes what you did step-by-step but doesn't interpret findings
- **Solid:** Has an intro (question + why), methods (what data, what was done), results (what you found), and a brief discussion
- **Research-grade:** All of Solid, plus explicitly acknowledges limitations and what you'd do next with more time

### 6. Defense (Session 16 walk-through)

- **Emerging:** Can describe what the code does but struggles to explain why
- **Solid:** Can explain each decision: why this variable, why this chart, why this cycle, why this cut
- **Research-grade:** All of Solid, plus can handle adversarial questions gracefully ("What if you had used a different age range?" "Could sample size be too small?")

---

## What "done" looks like

By end of Session 16, you will have:

- `final-project/` folder in your Drive with:
  - `analysis.ipynb` — your full analysis notebook, cleanly organized, re-runnable
  - `chart-1.png`, `chart-2.png`, (optional `chart-3.png`) — exported at publication dpi
  - `writeup.md` — 1–2 pages, following the structure in dimension 5
  - `data-sources.md` — NHANES cycle(s) used, file names, variable codes

- Successfully delivered the 5-minute walk-through in Session 16

That's it. That's the bar.

---

## Common ways projects go wrong (avoid these)

1. **Question too broad.** "How does diet affect disease?" is a lifetime's work. "Is higher sugar intake associated with higher fasting glucose in adults 20–39?" is a tractable project.

2. **Data chosen before question.** Pick the question first, then find the variables. Not the other way around.

3. **Merging errors go unnoticed.** If your row count tripled after a merge, something's wrong. Always verify.

4. **Charts that are pretty but wrong.** A gorgeous chart of wrong data is worse than a basic chart of right data.

5. **Executing without interpreting.** "The mean BMI is 27.3" is not a finding. "Adults in the lowest income bracket had mean BMI 2.1 points higher than the highest bracket, which is meaningful given the clinical threshold for obesity is 30" — that's a finding.

6. **Leaving defense prep for the end.** The walk-through isn't a presentation you rehearse at the last minute. Every decision you make during Sessions 14–16 should be something you can defend. If you can't explain *why* you did something, don't do it.

---

*This rubric is your contract. We're designing every session to get you here.*
