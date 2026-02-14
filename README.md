# A/B Test and Linear Regression Equivalence

This project contains a Jupyter notebook that **proves** that an A/B test (two-sample t-test) is a special case of simple linear regression: both methods give the same t-statistic, p-value, and treatment effect.

---

## Step-by-Step: What This Notebook Does (Simple Explanation)

### 1. **What we're proving**

We show that **two different "recipes"** (the t-test and regression) give **exactly the same answer** when we ask: "Does the treatment group have a different average than the control group?"

---

### 2. **Making up the data (like a game)**

- We **pretend** we have **1000 people**.
- **Half** get "no treatment" (control), **half** get "treatment."
- For each person we make up a **score** (the number `y`):
  - Control: score is around **1** (plus a little random wobble).
  - Treatment: score is around **1.5** (so **0.5 higher** on average).
- We put all of that in a **table**: who is in which group, and what their score is.

So we **create** the dataset ourselves, and we know the true story: treatment really does add 0.5 on average.

---

### 3. **First recipe: the t-test**

- We **split** the table into two piles: control scores and treatment scores.
- We ask: "Are the **averages** of these two piles different?"
- The t-test gives us:
  - **How different** the two averages are (that's related to the **t-statistic**).
  - **How sure** we can be that the difference isn't just luck (that's the **p-value**).
- We also compute: treatment average minus control average = **difference in means**.

---

### 4. **Second recipe: regression**

- We draw a **line** that best fits the data:
  - On the left (group = 0) the line is at one height.
  - On the right (group = 1) the line is at a higher height.
- That **step up** of the line is a number (the **slope**, β₁). It means: "When you go from control to treatment, the score goes up by this much."
- The computer also gives us a **t-statistic** and **p-value** for that step (for the "group" coefficient).

So: regression is just another way to say "control average" and "how much higher the treatment average is."

---

### 5. **The proof: we compare the two recipes**

We put side by side:

| What we compare | Recipe 1 (t-test) | Recipe 2 (regression) |
|-----------------|-------------------|------------------------|
| "How different?" (t-statistic) | Same number | Same number |
| "How sure?" (p-value) | Same number | Same number |
| "How much higher is treatment?" (effect) | Same number | Same number |

We check that these numbers are the **same to 4 decimal places**. So the two recipes are really the **same math** in disguise.

---

### 6. **Pictures**

- **First picture:** Two blobs (violin/box) — one for control scores, one for treatment scores. You can see they're in different places.
- **Second picture:** Dots (each person's score) and a **line** that goes from the control average to the treatment average. The **slope** of that line is exactly the "how much higher" number we got from both recipes.

---

### 7. **Why it matters**

- **Same answer:** t-test and regression give the **same** t-statistic, p-value, and treatment effect for this simple A/B comparison.
- **Regression can do more:** With regression you can later add more stuff (like age, baseline score) to control for them and still ask "how much does treatment add?" So regression is like a **bigger version** of the t-test that works in messier, real-world data.

---

## One-Sentence Summary

We made up data for two groups, used the t-test and regression to compare them, showed they give the same numbers, and drew pictures so we can see that the "step" in the regression line is the same as the difference between the two group averages.

---

## Files

- **`ab_test_regression_equivalence.ipynb`** — Jupyter notebook with the full proof (synthetic data, t-test, OLS regression, comparison table, and plots).

## Requirements

Install dependencies (e.g. with conda):

```bash
conda install -c conda-forge numpy pandas matplotlib seaborn scipy statsmodels
```

Or with pip:

```bash
pip install numpy pandas matplotlib seaborn scipy statsmodels
```

Then open the notebook and run all cells.
