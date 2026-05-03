# Session 4 — Instructor Notes

> **For the instructor, not the learner.** Read this before delivering Session 4.

---

## Session metadata

- **Session number:** 4 of 16
- **Phase:** 1 — Python for Data
- **Duration:** 60 minutes
- **Format:** 1:1 or 1:2, live on video call
- **Tooling:** Google Colab, shared Drive folder
- **Dataset:** `patient_measurements_small.csv` (from Session 1)

---

## Learning objective (one sentence)

*The learner can write a Python function that takes health data as input, applies classification logic, and returns a result — and understands the difference between `print()` and `return`.*

---

## Prerequisite check

- Session 3 attended
- Session 3 homework submitted (check Parts 1–4 especially — classification and group comparisons)
- Session 4 pre-read completed
- Learning journal has Session 3 entry

**If Part 1 (BMI classification) was copy-pasted three times:** perfect — that's your opening. "You wrote the same block three times. Let's fix that today."

**If the learner already used a loop to avoid repetition in Part 1:** also good. "You used a loop, which helped. But what if you need that same classification in a different part of your code?"

---

## Core concepts introduced

1. **Defining a function** — `def function_name(parameters):` (covered in pre-read, applied here)
2. **Parameters** — inputs the function works with (covered in pre-read, reinforced here)
3. **`return`** — giving back a result so the caller can use it (covered in pre-read, this is the critical concept)
4. **Calling a function** — `result = function_name(value)` (covered in pre-read, practiced extensively here)
5. **print vs return** — the stall point: `print()` inside a function displays text but returns `None`

---

## Session block plan (60 min)

### Block A — Warm-up & homework review (0:00–0:10)

1. (3 min) Open the learner's Session 3 homework. Look at Part 1 (BMI classification). Ask: "How many times did you write the if/elif/else block?" Most will say 3 (once per patient). "Did anything bother you about that?"
2. (3 min) Check Part 4 (group comparison mini-report). "Show me your observation sentence. What did you notice about the groups?" This keeps the data-analysis focus.
3. (2 min) If they attempted Part 5 (NHANES filtering): "Any surprises with the NHANES data?" Listen for whether they stumbled on numeric gender codes (1/2 vs M/F).
4. (2 min) Ask: "How did the pre-read go? Anything about `def` or `return` that felt unclear?" Their answer calibrates Block B's pacing.

---

### Block B — Concept bridge: from repeated code to a function (0:10–0:20)

The pre-read covered the syntax. Your job: connect it to the learner's own code.

Open `classwork.ipynb`. Live-code with the learner watching:

1. **Start with the problem.** Show (or have the learner pull up) the repeated BMI classification from their Session 3 homework. Three nearly identical blocks. "What changes between copies?" Just the height and weight values. Everything else is the same.

2. **Wrap it in a function.** Type:
   ```python
   def classify_bmi(weight_kg, height_cm):
       height_m = height_cm / 100
       bmi = weight_kg / (height_m ** 2)

       if bmi < 18.5:
           return "Underweight"
       elif bmi < 25:
           return "Normal"
       elif bmi < 30:
           return "Overweight"
       else:
           return "Obese"
   ```
   Walk through each part: the name, the parameters, the logic (unchanged from Session 3), the `return` statements.

3. **Call it on a few patients.** Type:
   ```python
   print(classify_bmi(79.5, 176.3))  # Patient P001
   print(classify_bmi(47.7, 167.6))  # Patient P015
   print(classify_bmi(92.1, 157.7))  # Patient P014
   ```
   Ask: "How many lines of classification code did you write?" One block. "How many patients can you classify?" As many as you want.

   Key moment: the function *returns* a string. That's why `print()` can display it. If it didn't return anything, `print()` would show `None`.

---

### Block C — Guided hands-on: write your own functions (0:20–0:40)

**Learner drives.** Instructor asks Socratic questions.

Task sequence (from the classwork notebook):

1. **Write `classify_bp(systolic)`.** The learner writes a function that takes a systolic blood pressure value and returns "Normal" (< 120), "Elevated" (120–129), or "High" (130+). They already know this classification from Session 3 — the new part is wrapping it in a function.

   After writing it, test on 3 values: `classify_bp(115)`, `classify_bp(125)`, `classify_bp(140)`.

2. **Write `age_group(age)`.** Returns "Young adult" (18–44), "Middle-aged" (45–64), or "Senior" (65+). This is new classification logic, but the function structure is the same.

3. **Use functions with the patient CSV.** Load the CSV and use a loop to classify a few patients:
   ```python
   for i in range(5):
       pid = df['patient_id'][i]
       bp_cat = classify_bp(df['systolic_bp'][i])
       age_cat = age_group(df['age'][i])
       print(f"{pid}: BP is {bp_cat}, age group is {age_cat}")
   ```
   This cements the connection: define once, call many times. The loop calls the function on each patient.

**Pedagogical goal:** the learner can independently write a function with parameters and `return`, and call it with different inputs.

---

### Block D — Stall point: print vs return (0:40–0:55)

Deliberately engineered. This is the single most common function mistake beginners make.

1. **Present the buggy function.** Give the learner this version:
   ```python
   def classify_bmi_buggy(weight_kg, height_cm):
       height_m = height_cm / 100
       bmi = weight_kg / (height_m ** 2)

       if bmi < 18.5:
           print("Underweight")
       elif bmi < 25:
           print("Normal")
       elif bmi < 30:
           print("Overweight")
       else:
           print("Obese")
   ```
   "This looks almost the same as the one we wrote. It even seems to work — try calling it."

2. **It "works" at first.**
   ```python
   classify_bmi_buggy(79.5, 176.3)
   ```
   Output: `Overweight`. Looks fine.

3. **Now try to store the result.**
   ```python
   result = classify_bmi_buggy(79.5, 176.3)
   print(f"The category is: {result}")
   ```
   Output:
   ```
   Overweight
   The category is: None
   ```
   "What happened? Where did `None` come from?"

4. **Collaborative debugging.** Guide the learner to understand:
   - `print()` sends text to the screen but doesn't give anything back to the caller
   - `return` sends a value back so the caller can use it
   - Without a `return`, the function returns `None` by default
   - The first `Overweight` was the `print()` inside the function. The `None` is what the function actually returned.

5. **The fix.** The learner changes `print()` to `return` in the buggy function. Verify the fix works:
   ```python
   result = classify_bmi(79.5, 176.3)
   print(f"The category is: {result}")
   ```

6. **The rule for their reference sheet:**
   > Use `return` when you need the function's result in your code. Use `print()` when you just want to display something.

**If time remains (0:50–0:55):** show what happens when you forget to call a function — `classify_bmi` without parentheses returns the function object itself: `<function classify_bmi at 0x...>`. This is a minor but memorable gotcha.

---

### Block E — Wrap & next steps (0:55–1:00)

1. (1 min) Save notebook in Drive
2. (1 min) Remind: 15-min consolidation + journal entry after class
3. (2 min) Walk through `homework.ipynb`. Point out: "Part 4 is the main artifact — a patient health report using your functions. Part 5 applies functions to NHANES."
4. (1 min) Preview Session 5: "Next session is the Phase 1 capstone — you'll take a messy CSV and produce a clean analysis, using everything from Sessions 1 through 4."

---

## Common mistakes to watch for

### In Block B:
- **Learner forgets the colon after `def`.** `def classify_bmi(weight_kg, height_cm)` without `:` gives a syntax error. Quick fix, but point it out as a syntax pattern: `def`, `if`, `for` — they all end with `:`.
- **Indentation errors inside the function.** Everything inside the function must be indented. If the learner mixes tabs and spaces, Colab usually catches it, but the error message is confusing.

### In Block C:
- **Learner writes the classification logic but forgets `return`.** The function runs but returns `None`. This often doesn't surface until they try to store or print the result. If it happens naturally here, great — it sets up Block D perfectly.
- **Learner hard-codes values instead of using parameters.** They write `bmi = 79.5 / (1.763 ** 2)` inside the function instead of using the parameter names. Ask: "What happens if you call this function with a different patient?"
- **Learner confuses the parameter name with a variable name from earlier.** They define `classify_bp(systolic)` but inside write `if systolic_bp < 120`. The parameter is `systolic`, not `systolic_bp`. The error message usually makes this clear.

### In Block D:
- **Learner doesn't see the problem immediately.** The `print()` version "looks like it works" because text appears on screen. That's the design. Let them sit with the confusion for a moment before guiding them to the `result = ...` test.
- **Learner thinks `print()` and `return` do the same thing.** This is the core misconception. The key distinction: `print()` talks to the *screen*; `return` talks to the *code that called the function*. If no code needs the result, `print()` is fine. If any code needs to use the result, you need `return`.

### General:
- **Learner asks "when would I use `print()` inside a function?"** Good question. Answer: for debugging, or when the function's purpose is to display output (like a formatted report). But for functions that compute a result (like classify_bmi), always use `return`.

---

## Assessment signal

The learner has grasped Session 4 if:

1. ✅ Can define a function with `def`, parameters, and `return`
2. ✅ Can call a function with different arguments and use the returned value
3. ✅ Can explain the difference between `print()` and `return` in their own words
4. ✅ Can write a new classification function independently (not just modifying the instructor's example)
5. ✅ Can use a function inside a loop to process multiple data points

**Red flags:**
- 🚩 They can copy and modify the instructor's function but can't write one from scratch. The homework will expose this — watch for it in Session 5's warm-up.
- 🚩 They still confuse `print()` and `return` after Block D. This needs to be resolved before Session 5, or the CSV capstone will produce mysterious `None` values.

---

## Pacing notes

- **If the pre-read was skipped:** Block B needs to cover `def` syntax from scratch. Extend Block B to 0:25, compress Block C to 15 minutes (cut the `age_group` function — just do `classify_bp`), and keep Block D intact — the print/return stall point is non-negotiable.
- **If the learner is ahead:** In Block C, after the loop exercise, show how the function could eventually work with pandas: "In a few sessions, you'll be able to do `df['bmi_category'] = df.apply(...)` instead of looping. Functions are what make that possible." Don't teach `.apply()` — just plant the seed.
- **Sacrosanct:** Block D. The print vs return distinction is the lasting takeaway from this session. If you skip it, the learner will silently produce `None` values for sessions to come.

---

## Post-session checklist (instructor)

- [ ] Confirm homework notebook copied into learner's Drive folder
- [ ] WhatsApp: "Great session. Homework in your folder. Session 5 pre-read up by [day]."
- [ ] Add one-paragraph delivery note below if anything notable happened

---

## Future delivery notes

*(Append after each delivery.)*
