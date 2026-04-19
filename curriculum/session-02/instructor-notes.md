# Session 2 — Instructor Notes

> **For the instructor, not the learner.** Read this before delivering Session 2.

---

## Session metadata

- **Session number:** 2 of 16
- **Phase:** 1 — Python for Data
- **Duration:** 60 minutes
- **Format:** 1:1 or 1:2, live on video call
- **Tooling:** Google Colab, shared Drive folder
- **Dataset:** Same patient CSV from Session 1 (`patient_measurements_small.csv`)

---

## Learning objective (one sentence)

*The learner can create and manipulate lists and dictionaries, and can use pandas to load a CSV, inspect it, and select columns — understanding that a pandas column is conceptually a list.*

---

## Prerequisite check

- Session 1 attended
- Session 1 homework submitted (at minimum: partial attempt visible in Drive)
- Session 2 pre-read completed
- Learning journal has Session 1 entry

**If the learner shows up without the pre-read done:** this is the first real test of the weekly loop. Don't punish, but do have the conversation. Say something like: "The class is designed assuming you've done the pre-read. Without it, we'll go more slowly today and cover less — that's the trade-off. Going forward, protect the 30 minutes for the pre-read. It's the single thing that makes this work."

Then adjust: trim Block B, spend more time on syntax in Block C. Note it in the delivery notes at the bottom.

---

## Core concepts introduced

1. **Lists** — ordered collections; indexing; basic operations (`append`, `len`, slicing)
2. **Dictionaries** — key-value pairs; accessing values by key
3. **The bridge concept** — a pandas column behaves like a list; a DataFrame row behaves like a dictionary
4. **Loading CSVs with pandas** — `pd.read_csv`, `.head()`, `.shape`, `.columns`, `.dtypes`
5. **Column selection** — `df['col']` vs `df[['col1', 'col2']]` (the stall point)

---

## Session block plan (60 min)

### Block A — Warm-up & homework review (0:00–0:10)

Standard structure from here on. Don't skip.

1. (3 min) Open the learner's Session 1 homework notebook in Drive. Ask them to walk through it: "Show me what you did. Where did you get stuck?"
2. (3 min) **Focus on the reflection questions** — their answers reveal the mental model. If they wrote "a variable is a box that holds data," good. If they wrote "a variable is a line of code," their model is off — correct gently.
3. (2 min) Look at their **learning journal** entry. Don't critique. Just acknowledge.
4. (2 min) Ask: "How did the pre-read go? Anything confusing?" This is your signal for how to pace Block B.

**Red flag to watch for:** if the learner didn't do the homework and didn't do the pre-read, that's a pattern forming after one session. Address it directly, kindly: "I want to make sure the course works for you. The out-of-class work is where it lands. Is something getting in the way?"

---

### Block B — Concept bridge: Lists and dictionaries in action (0:10–0:22)

The pre-read has introduced the syntax. Your job: show *why* we care.

Open `classwork-template.ipynb`. Live-code with the learner watching:

1. **A list of values is how pandas thinks.** Type:
   ```python
   ages = [34, 45, 62, 28, 51]
   print(ages)
   print(len(ages))
   print(ages[0])
   print(sum(ages) / len(ages))
   ```
   Ask: "What do you notice? What's the average age here?" They compute it. This is exactly what pandas does under the hood, just with prettier output.

2. **A dictionary is how we describe one patient.** Type:
   ```python
   patient = {
       "patient_id": "P001",
       "age": 58,
       "sex": "M",
       "height_cm": 176.3,
       "weight_kg": 79.5
   }
   print(patient["age"])
   print(patient["height_cm"])
   ```
   Ask: "Which of these is more like a row in the patient CSV? Which is more like a column?" Let them reason. This is the bridge moment. Don't skip it.

3. **Plant the seed:** "A pandas DataFrame is basically a list of dictionaries — or equivalently, a dictionary of lists. When we load a CSV, that's what pandas gives us."

---

### Block C — Guided hands-on: Revisit the patient CSV (0:22–0:42)

**Learner drives.** Instructor asks questions.

Task sequence (from the session notebook):

1. Mount Drive (they remember this from last week — let them do it without guidance unless they're stuck)
2. Load the CSV
3. `df.head()` — "What are we looking at?"
4. `df.shape` — "How many rows? How many columns?"
5. `df.columns` — "Now try `list(df.columns)`. What's different about the output? Why does that matter?" (They see that columns behave like a list.)
6. `df.dtypes` — "What types did pandas infer for each column? Does that match what we'd expect?"
7. **Select one column:** `df['age']`. Show them. Ask: "What does this look like? A list? Something else?"
8. Compute `df['age'].mean()` and `df['age'].max()`. Point out: "This is exactly what we did manually with the `ages` list at the start. Pandas just does it faster."

**Pedagogical goal:** the learner walks away saying "a column is like a list with superpowers."

---

### Block D — Stall point: Single vs double brackets (0:42–0:55)

Deliberately engineered moment. The learner **will** get this wrong the first time — that's the whole point.

1. Have the learner type:
   ```python
   single = df['age']
   double = df[['age']]
   print(type(single))
   print(type(double))
   ```
   They'll see `<class 'pandas.core.series.Series'>` vs `<class 'pandas.core.frame.DataFrame'>`.

2. Ask: "They *look* similar. But pandas is telling us they're different. Why might that matter?"

3. Have them run `single.mean()` and `double.mean()`. Both work, but the output shape differs.

4. Then ask them to select two columns: `df[['age', 'weight_kg']]`. Have them try `df['age', 'weight_kg']` (single brackets, two names) and watch it fail. Read the error together.

5. **The rule they should write down in their reference sheet:**
   > `df['col']` → a Series (one column, like a list)
   > `df[['col1', 'col2']]` → a DataFrame (one or more columns, still a table)
   > If you want multiple columns, you *need* the list inside the brackets.

**Why this matters:** this single confusion is responsible for ~30% of pandas debugging time for beginners. Burning 10 minutes on it here saves hours over the track.

---

### Block E — Wrap & next steps (0:55–1:00)

1. (1 min) Save notebook as `session-02-notes.ipynb` in `/session-02/` in Drive
2. (1 min) Remind: 15-min consolidation + journal entry after class
3. (2 min) Walk through `homework.ipynb`. Flag the stretch section as optional.
4. (1 min) Preview Session 3: "We'll do control flow — if/else and loops — on this same CSV. The pre-read will be up [when]."

---

## Common mistakes to watch for

### In Block B:
- **Learner confuses list indexing with counting from 1.** Lists are zero-indexed. `ages[0]` is the first element. Common source of confusion. Have them explicitly say "zero is the first position" out loud once.
- **Learner tries `patient.age` (dot-notation) instead of `patient["age"]`.** Dot-notation exists in pandas for DataFrames (with caveats) but not for plain dictionaries. Don't go down that rabbit hole — just correct and move on.

### In Block C:
- **`df.columns` looks confusing** (prints `Index([...])` rather than a plain list). That's why we have them wrap it: `list(df.columns)`. Good habit.
- **Learner tries to modify `df` and then is confused when the original "isn't changed."** Don't introduce assignment semantics yet — just tell them "we're only reading, not modifying" and keep moving.

### In Block D:
- **Learner memorizes the rule without internalizing it.** Test them: "Okay, you want height and weight — how do you ask pandas for it?" Make them type it.
- **Learner asks why pandas made two ways to do this.** Good question. Honest answer: it's historical, and both are useful in different contexts. Don't pretend it's clean design.

### General:
- **Learner tries to type everything from memory instead of using the pre-read.** Encourage them to keep the pre-read open in another tab. Looking things up is a real skill.

---

## Assessment signal

The learner has grasped Session 2 if:

1. ✅ Can create a list, access elements by index, compute basic stats
2. ✅ Can create a dictionary, access values by key
3. ✅ Can load the CSV and answer: "how many rows?", "what are the columns?", "what's the average age?"
4. ✅ Can articulate the difference between `df['col']` and `df[['col']]` without looking it up
5. ✅ Says something like "oh, a column is basically a list" — if they say this unprompted, you've nailed the bridge concept

**Red flags:**
- 🚩 They can type the code but can't explain what it's doing. Slow down, ask more "why" questions.
- 🚩 They're treating `df` as magic. Unpack: "What do you think is inside `df`?" If they can't answer, the bridge concept isn't landing. Spend Session 3's opening redoing this.

---

## Pacing notes

- **If the pre-read was skipped:** cut Block B from 12 to 8 minutes, move list/dict syntax into a quick pre-read-in-class. Cut Block D's step 4 (the multi-column error). Still hit the single-vs-double brackets teaching.
- **If learner is ahead:** the stretch section in the homework has them load a different CSV (we'll provide one) and do the same moves on unfamiliar data. Mention this in Block E.
- **Sacrosanct:** Block D. This stall point is non-negotiable — it pays off for the rest of the track.

---

## Post-session checklist (instructor)

- [ ] Confirm homework notebook copied into learner's Drive folder
- [ ] WhatsApp: "Great session. Homework in your folder. Session 3 pre-read up by [day]."
- [ ] Add one-paragraph delivery note below if anything notable happened

---

## Future delivery notes

*(Append after each delivery.)*
