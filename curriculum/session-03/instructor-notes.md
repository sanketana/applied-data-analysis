# Session 3 — Instructor Notes

> **For the instructor, not the learner.** Read this before delivering Session 3.

---

## Session metadata

- **Session number:** 3 of 16
- **Phase:** 1 — Python for Data
- **Duration:** 60 minutes
- **Format:** 1:1 or 1:2, live on video call
- **Tooling:** Google Colab, shared Drive folder
- **Dataset:** `patient_measurements_small.csv` (from Session 1)

---

## Learning objective (one sentence)

*The learner can use if/else to classify values, for loops to iterate over lists, and boolean filtering to select subsets of a DataFrame — and understands why pandas filtering replaces the loop-through-rows pattern.*

---

## Prerequisite check

- Session 2 attended
- Session 2 homework submitted (check Parts 3–5 especially — column selection and NHANES)
- Session 3 pre-read completed
- Learning journal has Session 2 entry

**If the stretch section was attempted (Part 7 — boolean filtering preview):** that's your opening for Block B. Ask the learner to explain what they think `df[df['sex'] == 'M']` does. Their answer tells you where to start.

**If the stretch section was skipped:** no problem. Block B builds from scratch.

---

## Core concepts introduced

1. **Comparison operators** — `==`, `!=`, `>`, `<`, `>=`, `<=` (covered in pre-read, reinforced here)
2. **if/elif/else** — conditional branching (covered in pre-read, applied to data here)
3. **for loops** — iterating over lists (covered in pre-read, applied here)
4. **Boolean Series** — `df['age'] > 50` returns a True/False column. This is the bridge from plain Python to pandas.
5. **Boolean filtering** — `df[df['age'] > 50]` selects rows where the condition is True
6. **Combining conditions** — `&` (and) and `|` (or) with mandatory parentheses
7. **Loop vs vectorized** — the stall point: why you should avoid looping through DataFrame rows

---

## Session block plan (60 min)

### Block A — Warm-up & homework review (0:00–0:10)

1. (3 min) Open the learner's Session 2 homework. Walk through Parts 3–4 (column selection, analysis). "Show me your summary sentence from Part 4."
2. (3 min) Check Part 5 (NHANES body measures). Ask: "What surprised you about the NHANES data compared to our patient CSV?" This is a genuine question — their observation reveals how they're thinking about data.
3. (2 min) If they attempted Part 7 (stretch): "Can you explain what `df[df['sex'] == 'M']` does?" Listen to their explanation. Don't correct yet — file it away for Block B.
4. (2 min) Ask: "How did the pre-read go? if/else and loops — anything confusing?" This sets your pacing for Block B.

---

### Block B — Concept bridge: from if/else to boolean columns (0:10–0:22)

The pre-read covered the syntax. Your job: connect it to DataFrames.

Open `classwork.ipynb`. Live-code with the learner watching:

1. **Start with a single value.** Type:
   ```python
   systolic_bp = 135

   if systolic_bp < 120:
       category = "Normal"
   elif systolic_bp < 130:
       category = "Elevated"
   else:
       category = "High"

   print(f"BP {systolic_bp} → {category}")
   ```
   Ask: "What would you do if you had 20 patients and wanted to classify each one?" They'll probably say "a loop." Good — hold that thought.

2. **Quick loop on a list.** Type:
   ```python
   bp_values = [119, 135, 128, 142, 115]

   for bp in bp_values:
       if bp < 120:
           print(f"{bp} → Normal")
       elif bp < 130:
           print(f"{bp} → Elevated")
       else:
           print(f"{bp} → High")
   ```
   This works. But it only works on a list, not on 9,000 NHANES respondents.

3. **The bridge moment.** Load the patient CSV and type:
   ```python
   df['age'] > 50
   ```
   Ask: "What did pandas just give us?" Let them look at the output — a column of True/False. "Pandas ran the comparison on every single row at once. No loop needed."

   This is the conceptual bridge. Make sure it lands before moving to Block C.

---

### Block C — Guided hands-on: boolean filtering (0:22–0:42)

**Learner drives.** Instructor asks Socratic questions.

Task sequence (from the classwork notebook):

1. **Create a boolean mask:** `df['sex'] == 'F'`. Ask: "How many True values do you see? How could you check without counting by hand?" Answer: `.sum()`.

2. **Use the mask to filter:** `females = df[df['sex'] == 'F']`. Then `females.shape`. Ask: "How many rows? Does that match the number of Trues?"

3. **Filter + stat:** `df[df['sex'] == 'M']['weight_kg'].mean()`. Ask: "Read this left to right. What's happening at each step?"

4. **Group comparison:** Have them compute mean systolic BP for males and females separately, and print both. This is the first "mini-analysis" — comparing groups.

5. **Combining conditions:** `df[(df['age'] > 40) & (df['sex'] == 'F')]`. The parentheses around each condition are required — without them, Python's operator precedence breaks things. Have the learner try it without parentheses first and see the error.

**Pedagogical goal:** the learner can independently write a boolean filter, apply it, and compute a stat on the filtered result.

---

### Block D — Stall point: loop vs vectorized (0:42–0:55)

Deliberately engineered contrast. This is where the "don't loop through DataFrames" rule gets internalized.

1. **Pose the challenge:** "Compute the mean weight of patients over 50. Use a for loop."

2. **Let them try.** The natural approach:
   ```python
   total = 0
   count = 0
   for i in range(len(df)):
       if df['age'][i] > 50:
           total += df['weight_kg'][i]
           count += 1
   print(total / count)
   ```
   This works. It gives the right answer. Let them feel the victory for a moment.

3. **Now the pandas way:**
   ```python
   df[df['age'] > 50]['weight_kg'].mean()
   ```
   Same answer. One line.

4. **Discussion:** "Both give the same number. When would the difference matter?" Answer: when you have 9,000 NHANES rows, or a million. The loop gets slow. The pandas way is built for this.

5. **The rule they should write in their reference sheet:**
   > If you're writing a `for` loop over DataFrame rows, there's almost always a pandas way to do it instead.

**Why this matters:** this stall point prevents a pattern that will haunt them for the rest of the course. Learners who fall into the "loop through rows" habit write code that's 10x longer and 100x slower. Better to break the habit now.

---

### Block E — Wrap & next steps (0:55–1:00)

1. (1 min) Save notebook in Drive
2. (1 min) Remind: 15-min consolidation + journal entry after class
3. (2 min) Walk through `homework.ipynb`. Point out: "Part 4 is the main artifact — a group comparison mini-report. Part 5 uses NHANES. Everything else is practice."
4. (1 min) Preview Session 4: "We'll learn functions — how to wrap up work into reusable pieces. The pre-read will be up by [day]."

---

## Common mistakes to watch for

### In Block B:
- **Learner confuses `=` and `==`.** They'll write `if bp = 120` and get a syntax error. This is extremely common. Correct once, add to reference sheet.
- **Indentation errors.** If the learner's code isn't running, it's almost always indentation. Colab shows a red highlight — point it out.

### In Block C:
- **Forgetting the outer brackets in boolean filtering.** They write `df[df['age'] > 50]` correctly, but then try `df[df['age'] > 50, df['sex'] == 'M']` instead of using `&`. The comma-syntax doesn't work here.
- **Missing parentheses with `&`.** `df[df['age'] > 40 & df['sex'] == 'F']` fails because `&` binds tighter than `>`. Each condition needs parentheses: `df[(df['age'] > 40) & (df['sex'] == 'F')]`. Let them hit this error — it's memorable.
- **Using `and` instead of `&` in pandas.** Python's `and` doesn't work on Series. They need `&` for element-wise boolean operations in pandas. This is confusing because the pre-read taught `and`. Acknowledge the inconsistency: "In plain Python, use `and`. In pandas, use `&`. It's annoying, but that's how it works."

### In Block D:
- **Learner uses `df.iloc[i]` instead of `df['col'][i]` in the loop.** Either works — don't correct the approach, just make sure the final answer is right. The pedagogical point is the contrast with the one-liner, not the loop syntax.
- **Learner is skeptical that the one-liner is "real code."** Some learners feel the loop is more "legitimate" because they can see every step. Validate: "The loop is real code. The pandas version is also real code. The pandas version just hides the loop inside a highly optimized implementation."

### General:
- **Learner tries to memorize the syntax instead of understanding the logic.** Push for understanding: "Don't memorize `df[df['age'] > 50]`. Instead, think: 'I want rows where age is over 50. I make a True/False column, then use it to pick rows.'"

---

## Assessment signal

The learner has grasped Session 3 if:

1. ✅ Can write an if/elif/else to classify a single value
2. ✅ Can write a for loop over a list with an if condition inside
3. ✅ Can explain what `df['age'] > 50` returns (a True/False column)
4. ✅ Can independently write `df[df['sex'] == 'F']` to filter a DataFrame
5. ✅ Can chain a filter with a stat: `df[df['sex'] == 'M']['weight_kg'].mean()`
6. ✅ Can articulate why the pandas way is preferred over a loop for DataFrames

**Red flags:**
- 🚩 They can write the filter syntax but can't explain *why* it works. This means the boolean-Series concept hasn't landed. In Session 4, open with a quick review.
- 🚩 They keep reaching for loops when a pandas operation would work. Reinforce the rule gently over the next few sessions.

---

## Pacing notes

- **If the pre-read was skipped:** Block B needs to cover if/else and loop syntax from scratch. Extend Block B to 0:28, compress Block C to 15 minutes (cut the combining-conditions exercise), and keep Block D intact — the stall point is non-negotiable.
- **If the learner is ahead:** In Block C, add NHANES filtering live: `demo[demo['RIDAGEYR'] >= 18]` to show the same filtering on 9,000 rows. This previews the homework.
- **Sacrosanct:** Block D. The loop-vs-vectorized contrast is the lasting takeaway from this session.

---

## Post-session checklist (instructor)

- [ ] Confirm homework notebook copied into learner's Drive folder
- [ ] WhatsApp: "Great session. Homework in your folder. Session 4 pre-read up by [day]."
- [ ] Add one-paragraph delivery note below if anything notable happened

---

## Future delivery notes

*(Append after each delivery.)*
