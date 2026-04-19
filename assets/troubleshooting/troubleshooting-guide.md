# "I'm stuck — what do I try?"

Before pinging the instructor on WhatsApp, try these steps in order. About 70% of stuck moments resolve here. The other 30% — that's what we're here for, don't suffer alone.

---

## Rule of thumb

**15-minute rule:** if you've been staring at the same error for 15 minutes, stop, try steps below. If those don't help, ping the group. Don't lose a whole evening.

---

## Step 1: Read the error message out loud

Seriously. Beginners often scan errors visually and miss what they say. Read the *last line* of the error message out loud. Python errors are usually specific about what went wrong — e.g., `KeyError: 'SEQN'` literally tells you `SEQN` isn't a column in the DataFrame.

Common Python error types and what they mean:

| Error | Usually means |
|---|---|
| `NameError: name 'xyz' is not defined` | You used `xyz` before creating it, OR typo'd the name, OR forgot to run the cell that created it |
| `KeyError: 'column_name'` | That column isn't in your DataFrame. Check spelling (case-sensitive!) and run `df.columns` to see what's actually there |
| `TypeError: ...` | You passed the wrong kind of thing to a function (e.g., a string where a number was expected) |
| `ValueError: ...` | The type was right but the value made no sense (e.g., can't convert "hello" to a number) |
| `FileNotFoundError` | The file path is wrong, or the file isn't where you think it is |
| `IndentationError` | Python is strict about spacing. Check that your indents are consistent (all spaces, not mixed with tabs) |
| `SyntaxError` | Usually a missing `:`, `)`, or `]`. Look at the line *before* the one Python flags — that's often where the real problem is |

## Step 2: Run it again, from the top

In Colab/Jupyter, sometimes cells are out of order because you ran them in a weird sequence. Try:

1. `Runtime → Restart runtime`
2. Run every cell from the top, one by one
3. See where it breaks

If it works this time, your problem was cell execution order — a common trap.

## Step 3: Inspect your data

When pandas does something weird, 90% of the time the data isn't what you think it is. Run:

```python
df.shape          # How many rows and columns?
df.head()         # What do the first few rows look like?
df.columns        # What are the column names, exactly?
df.dtypes         # What are the data types?
df.isna().sum()   # How many missing values per column?
```

If `df.shape` surprises you — e.g., you expected 5,000 rows and got 47,000 — your merge went wrong. Stop and investigate.

## Step 4: Simplify

If your code is complicated and not working, break it down:

- Split a one-liner into three lines
- Print intermediate values between steps
- Try it on a tiny piece of data first (`df.head(10)`) before the whole thing

## Step 5: Check your reference sheet

You've been building a reference sheet since Session 1. Have you already solved something like this? Search it.

## Step 6: Consult the pre-read

The answer is often in the pre-read for the session where the concept was introduced. Scan the pre-read for the relevant session, even if it was weeks ago.

## Step 7: Ping the WhatsApp group

When you do, include:

1. **What you were trying to do** (one sentence)
2. **What you expected to happen**
3. **What actually happened** (the error message, or the wrong output)
4. **What you've already tried**
5. **A screenshot** of your code + the error

Bad ask: "It's not working, help!"
Good ask: "I'm trying to merge DEMO and BMX on SEQN. I expected ~9,000 rows but got 47,000. I checked that SEQN is spelled the same in both. Here's my code + output [screenshot]."

The good ask gets a fast answer. The bad ask triggers a round of clarifying questions.

---

## NHANES-specific gotchas

These come up in Phase 2 and beyond. Keep this list in mind.

### "My merge produced way too many rows"

The SEQN column is not unique in some NHANES files (e.g., questionnaires where a respondent answered multiple sub-questions). Check `df['SEQN'].duplicated().sum()` before merging. If > 0, you need to decide what to do (usually: filter or aggregate before merging).

### "My means include bogus values"

NHANES uses specific codes for missing/refused/don't-know: often `.`, `7777`, `9999`, or similar. These get read as real numbers and destroy your averages. **Always check the variable's documentation on the CDC site** for its missing-value codes, and replace them with `NaN` before computing anything.

```python
# Example: treat 7777 and 9999 as missing for variable XYZ
df['XYZ'] = df['XYZ'].replace([7777, 9999], pd.NA)
```

### "The variable name I expected doesn't exist in this cycle"

NHANES changes variable names and files across cycles. The variable called `BPXSY1` in 2017–2018 might be `BPXOSY1` in 2021–2023 (hypothetical example). Always check the cycle's variable list. If you're comparing across cycles, do the variable-mapping work up front.

### "read_sas is crashing / very slow"

For `.xpt` files, try `pyreadstat.read_xport()` instead of `pandas.read_sas()`. It's faster and more reliable.

---

## Colab-specific gotchas

### "My session disconnected and I lost my data"

Colab disconnects idle sessions. Two defenses:
1. Save your notebook frequently (Ctrl+S)
2. If you downloaded a file, save it to Drive (`drive.mount(...)` and save there), not to the ephemeral Colab disk

### "I can't find the file I downloaded"

By default Colab saves to `/content/`. If you restart the runtime, `/content/` wipes. Always save important files to your mounted Drive.

### "Colab is running really slowly"

- Close other Colab tabs
- `Runtime → Restart runtime`
- If still slow, the free tier is congested — try again later, or switch to local Jupyter (we can set this up mid-track)

---

*Add to this doc as you discover more gotchas. It's a living reference.*
