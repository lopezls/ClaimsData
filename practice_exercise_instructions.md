# Practice Exercise: Solutions Engineer Data Task Simulation

**Scenario:** You just received a data export from a new client (a primary care group). This is exactly the kind of "messy client-submitted data" the Keebler Health posting describes. Your job: clean it, join it, and produce a short summary — as if you had 2 hours before a client call.

**Files:**
- `messy_claims_data.csv` — the raw claims export (has real-world messiness on purpose)
- `provider_lookup.csv` — a reference table to join against

**Do this in a Jupyter notebook, a Python script, or even just pandas in a Python shell — whatever you're comfortable with. Time yourself loosely, but the point is honest self-assessment, not speed.**

---

## Tasks

### 1. Load and inspect
- Load `messy_claims_data.csv` into a pandas DataFrame
- Look at the shape, column types, and first several rows
- Identify what's messy about it (don't fix yet — just list what you notice)

### 2. Clean it
- **Dates:** `claim_date` has multiple formats mixed together (e.g., `2025-05-21`, `01/16/2025`, `14-Jul-2025`, `07-22-25`). Convert the whole column to a single, consistent datetime format.
- **Text inconsistency:** `claim_status` has inconsistent casing and stray whitespace (`Paid`, `paid`, `PAID`, `denied `). Standardize it to a clean, consistent set of values.
- **Diagnosis codes:** `diagnosis_code` has inconsistent casing, some blank/empty values, and stray whitespace. Decide how to handle the blanks (drop? flag? fill with "Unknown"?) and standardize formatting.
- **Missing values:** `claim_amount` and `provider_id` both have missing values. Decide what to do with each — this isn't a trick, there's more than one reasonable answer, but you should be able to explain your choice.
- **Duplicates:** There are exact duplicate rows hidden in the data. Find and remove them.

### 3. Join
- Join the cleaned claims data with `provider_lookup.csv` on `provider_id`, so each claim shows the provider's name and specialty.
- Think about what should happen to claims where `provider_id` was missing — do they disappear from the join, or should you keep them with an "Unknown provider" label?

### 4. Summarize
Produce a short summary (a few printed lines or a small table) answering:
- How many valid claims are there after cleaning?
- Total and average claim amount
- Claim count and total amount broken down by `claim_status`
- Claim count broken down by provider specialty

### 5. Reflect (the actual point of this exercise)
After you finish, answer honestly:
- What parts did you do quickly, without needing to look anything up?
- What parts did you need to search for (Stack Overflow, docs, ChatGPT/Claude, etc.)?
- Roughly how long did the whole thing take you?
- If a client asked you to explain your cleaning decisions in plain language on a call, could you do it confidently?

---

## How to score yourself honestly

- **Finished in under ~90 minutes, mostly without help:** You're genuinely ready to apply now.
- **Finished, but leaned heavily on searching/AI help for syntax:** Totally normal and not disqualifying — this is how most working data people operate. Apply, but expect the interview (if you get one) to probe your reasoning, not just your syntax memory — make sure you can explain *why* you made each cleaning decision.
- **Got stuck or didn't know where to start on more than one task:** Not a failure — it just means a week or two of deliberate pandas practice (this exact kind of messy-data cleaning, repeated a few times with different datasets) would meaningfully strengthen your application and interview performance before you apply.

There's no submission or "grading" here beyond your own honest read of how it went.
