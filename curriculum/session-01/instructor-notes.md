# Session 1 — Instructor Notes

> **For the instructor, not the learner.** Read this before delivering Session 1.

---

## Session metadata

- **Session number:** 1 of 16
- **Phase:** 1 — Python for Data
- **Duration:** 60 minutes
- **Format:** 1:1 or 1:2, live on video call
- **Tooling:** Google Colab, shared Drive folder

---

## Learning objective (one sentence)

*The learner can open Google Colab, run Python code, store values in variables, and use basic data types (numbers, strings, booleans) through a health-data example — and understands how this course will work.*

---

## Prerequisite check

- Before-Session-1 setup doc completed (Colab opened, "Hello, Sanketana!" cell run successfully)
- `start-here.md` and `final-project-rubric.md` skimmed

**If the learner hasn't done these:** don't punish them in Session 1, but take 5 minutes at the top of class to do them together, and flag that this pattern (pre-work done before class) is the single thing that makes the course work.

---

## Core concepts introduced

1. **How this course works** — the weekly loop, what the learner owns, what we own
2. **Colab as an environment** — cells, running cells, saving to Drive
3. **Variables** — a label that holds a value
4. **Basic data types** — integers, floats, strings, booleans — through health examples
5. **`print()` function** — how to see what's going on

Syntax coverage is minimal. We're establishing *posture* (how to learn) as much as *skills*.

---

## Session block plan (60 min)

### Block A — Warm-up & orientation (0:00–0:12)

*This session's Block A replaces "homework review" with "course orientation." First session only.*

- (2 min) Welcome. Confirm the Drive folder opens and Colab is accessible.
- (5 min) Walk through `start-here.md` with the learner. Emphasize the weekly loop. **Let them ask questions about expectations** — this is the moment to calibrate.
- (5 min) Walk through `final-project-rubric.md`. Be reassuring: "You won't understand this yet. That's fine. It exists so you always know where we're going."

**If 1:2 (Padma + son):** explicitly acknowledge that they'll learn at different paces. Reassure both that the track is designed for this — faster learner gets stretch variants, slower learner sets the floor pace. Don't skip this conversation.

---

### Block B — Concept bridge: Python as a calculator for health data (0:12–0:22)

Open `classwork-template.ipynb` together in Colab. Live-code these four things in order:

1. **Print a string.** Type and run `print("I'm learning data analysis")`. Explain: a cell is a block of code; Shift+Enter runs it; output appears below.

2. **Variables.** Type:
   ```python
   patient_age = 45
   print(patient_age)
   ```
   Explain: `patient_age` is a label. We can use it later.

3. **Types.** Type these one at a time and run each:
   ```python
   age = 45                  # integer
   weight_kg = 72.4          # float (has a decimal)
   patient_name = "Priya"    # string (in quotes)
   has_diabetes = False      # boolean (True or False)
   ```
   Ask: "Why do you think `weight_kg` has a decimal but `age` doesn't?" Let them answer. Correct them gently if needed.

4. **Using variables in expressions.** Type:
   ```python
   height_m = 1.65
   weight_kg = 72.4
   bmi = weight_kg / (height_m ** 2)
   print(bmi)
   ```
   Pause. Ask: "What do you think this computes?" Let them explain BMI in their own words. This is our first tiny health-data moment.

**Instructor notes for Block B:**
- Keep typing slow enough for the learner to follow, but *don't* make them copy yet. They watch, they think, they ask.
- Resist the urge to explain everything. If they don't ask about a concept, don't lecture it.
- The `**` for exponentiation will be new. Mention it, but don't dwell — it's in the pre-read for Session 2.

---

### Block C — Guided hands-on: Learner drives (0:22–0:42)

*Now switch: learner's screen is shared, learner types. Instructor asks questions.*

Task: "Compute and print the BMI for three different patients using variables."

Give them this starter setup verbally or in the notebook:

```
Patient A: height 1.70 m, weight 68 kg
Patient B: height 1.58 m, weight 82 kg
Patient C: height 1.82 m, weight 75 kg
```

Let them work it out. Resist over-helping. If they struggle, ask:
- "What variables do you need?"
- "How did we compute BMI for the first one?"
- "What would you change for Patient B?"

**Expected outcome:** three `print()` statements showing three BMI values.

**Stretch variant (if 1:2 with a faster learner, or if this takes <10 min):**
- "Which patient has the highest BMI?" — introduces the idea of comparing values, which becomes the bridge to Session 2's control flow
- "Can you print a message that says 'Patient B's BMI is X'?" — introduces f-strings or string concatenation naturally

---

### Block D — Stall point: The load-a-CSV moment (0:42–0:55)

*This session's stall point is deliberately gentle — it's Session 1. The real stall points come from Session 7 onward. But we need one small moment of productive struggle.*

Show the learner the `patient_measurements_small.csv` file in the Drive folder. 20 rows, 7 columns, synthetic patient data.

Live-code together (learner still drives):

```python
import pandas as pd
df = pd.read_csv("/content/drive/MyDrive/[learner-folder]/session-01/patient_measurements_small.csv")
df.head()
```

**This is the first stall point:** the path to the file. It won't be `/content/drive/MyDrive/...` out of the box. The learner needs to:
1. Mount their Drive in Colab (`from google.colab import drive; drive.mount('/content/drive')`)
2. Find the file path

**Don't rescue immediately.** Let them:
- Try the wrong path first and see the `FileNotFoundError`
- Read the error out loud
- Figure out that they need to mount Drive

Then show them `df.head()` and `df.shape`. First sight of a real DataFrame. Let them spend a minute just looking at it. Ask: "What do you notice? What questions does this data raise?"

**Why this matters pedagogically:** we're establishing on Day 1 that (a) errors are useful information, not scary, and (b) data comes with structure we need to understand before we analyze it. These two ideas are the spine of the entire track.

---

### Block E — Wrap & next steps (0:55–1:00)

1. (1 min) Save the notebook. Name it `session-01-notes.ipynb`. Save to the `/session-01/` folder in Drive.
2. (1 min) Set the learning journal expectation: "Right after class — 5 minutes — open your journal, write 2–3 lines."
3. (2 min) Walk through the homework: `homework.ipynb`. Brief — don't solve it for them.
4. (1 min) Set expectation for next session: "Before Session 2, you'll have a pre-read with short exercises. It'll show up in your Drive folder on [day]. Do it, including the self-check, before class."

---

## Common mistakes to watch for

### In Block B:
- **Learner tries to type `patient age = 45` (with a space).** Python will error. Good teaching moment: variable names can't have spaces; use `_`.
- **Learner types `"Priya` (missing closing quote).** Jupyter will show a weird continuation prompt. Reassure — Python is just waiting for the string to end.

### In Block C:
- **Reusing variable names across patients** (i.e., overwriting `weight_kg` for patient B, so patient A's value is lost). Totally fine for this exercise. Later we'll see why unique names matter. Don't over-correct now.

### In Block D:
- **Learner pastes the Windows/Mac file path with backslashes.** Colab is Linux; use forward slashes. Common confusion.
- **Learner assumes Drive is auto-mounted.** It isn't. They must run `drive.mount(...)`. This will likely be the first real authentication flow the learner encounters in Colab.

### General (throughout):
- **Learner apologizes for asking a "basic question."** Reframe immediately: "There are no basic questions in Session 1. Asking is the job." This sets the tone for the whole course.
- **Learner tries to race ahead** ("What if I also did...?"). Welcome it, but redirect: "Hold that thought — we'll get there. Add it to your journal."

---

## Assessment signal

The learner has grasped Session 1 if:

1. ✅ They can explain, in their own words, what a variable is and why we use them
2. ✅ They can write a new `print()` statement without help
3. ✅ They ran `df.head()` on the CSV and saw the table
4. ✅ They say something like "I get it" or ask a curious question rather than a worried one

**Red flags (intervene):**

- 🚩 They seem anxious or overwhelmed. Pause. Reassure. Cut scope if needed — drop Block D and spend time in Block C instead.
- 🚩 They're silent throughout Block C. Pedagogy isn't working. Shift to more questions, less code.
- 🚩 Time is running out and you haven't done Block D. Skip it. Don't rush. Better to end at Block C solidly than skim Block D.

---

## Pacing notes

- **If things are going fast:** extend Block C with the stretch variants. Don't rush to Block D.
- **If things are going slow:** trim Block D to just "here's what a DataFrame looks like, we'll load CSVs properly in Session 2." Do not skip Block A (orientation) or Block E (wrap).
- **Sacrosanct:** Block A's orientation portion, and the 15-min consolidation ask at the end. These set the rhythm of the course.

---

## Post-session checklist (instructor)

Within 1 hour of Session 1:

- [ ] Confirmed learner saved the session notebook to Drive
- [ ] Confirmed homework is visible in the Drive folder
- [ ] Sent a brief WhatsApp: "Great first session. Pre-read for Session 2 will be up on [day]. Homework due before [date]. Any questions — ping."
- [ ] Added any notes to `/curriculum/session-01/instructor-notes.md` about what could be improved (under a "Delivery notes" section you create)

---

## Future delivery notes (append as you teach this session more than once)

*(Start empty. After each delivery, add one paragraph: who was the learner, what worked, what didn't, what you'd change. This is how the curriculum improves.)*
