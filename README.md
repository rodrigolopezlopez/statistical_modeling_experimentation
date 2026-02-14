# A/B Test and Linear Regression Equivalence

This project contains a Jupyter notebook that **proves** that an A/B test (two-sample t-test) is a special case of simple linear regression: both methods give the same t-statistic, p-value, and treatment effect.

---

## 💡 The "Aha!" Moment

When starting out in data, we often learn A/B testing and Regression in different chapters. This project bridges that gap by showing that:
* **A/B Testing** is the "What": Did group B outperform group A?
* **Regression** is the "How": It models the relationship between being in a group and the resulting outcome.

Mathematically, they are two sides of the same coin.

---

## Step-by-Step: What This Notebook Does

### 1. What we're proving
We show that **two different "recipes"** (the t-test and regression) give **exactly the same answer** when we ask: "Does the treatment group have a different average than the control group?"

In statistical terms, we compare:
* **T-test:** $H_0: \mu_{treatment} = \mu_{control}$
* **Regression:** $y = \beta_0 + \beta_1x + \epsilon$ (where $x$ is 0 or 1)

### 2. Making up the data (Synthetic Dataset)
- We simulate **1000 people**.
- **Half** get "no treatment" (control, $x=0$), **half** get "treatment" ($x=1$).
- We know the "ground truth": Treatment adds exactly **0.5** to the average score.

### 3. Recipe 1: The T-Test
- We split the data into two piles.
- We run a standard `ttest_ind` to find the **t-statistic** and **p-value**.
- We calculate the **difference in means**.

### 4. Recipe 2: Regression
- We fit a line to the data: $y = \beta_0 + \beta_1(Group)$.
- The **intercept ($\beta_0$)** is the control mean.
- The **slope ($\beta_1$)** is the "step up" from control to treatment.
- We extract the **t-statistic** and **p-value** for that slope.

### 5. The Proof: Side-by-Side Comparison
We verify the identity by comparing the outputs:

| Metric | Recipe 1 (T-Test) | Recipe 2 (Regression) |
| :--- | :--- | :--- |
| **Effect Size** | Difference in Means | $\beta_1$ Coefficient |
| **Significance** | T-Statistic | T-Statistic |
| **Probability** | P-Value | P-Value |

*Note: These values are identical to 4+ decimal places.*

### 6. Visualizations
The notebook generates:
- **Distribution Plots:** Violin and Box plots showing the spread of the two groups.
- **Regression Plot:** A plot showing the regression line connecting the two group means, illustrating that the "slope" is the "lift."

---

## 🚀 Why This Matters

1.  **Same Answer:** Understanding this equivalence removes the "magic" from the formulas and shows the underlying unity of statistics.
2.  **Regression Superpowers:** Once you treat an experiment as a model, you can add **covariates** (like age or pre-experiment spend) to reduce noise. 
3.  **Foundation for CUPED:** This is the logic behind variance reduction techniques like **CUPED** (Controlled-experiments Using Pre-Experiment Data) used by companies like Netflix and Booking.com.

---

## 🛠 Behind the Project

This repository was born out of a personal "aha!" moment while learning in public. To document this clearly, I used an AI-augmented workflow:
* **Claude (via Cursor):** Helped me write the Python implementation and ensure the statistical proof was rigorous.
* **Gemini:** Helped me structure the documentation and explain these concepts simply for other practitioners starting their journey.

---

## Files
* `ab_test_regression_equivalence.ipynb`: Jupyter notebook with the full proof and plots.

## Requirements
```bash
pip install numpy pandas matplotlib seaborn scipy statsmodels