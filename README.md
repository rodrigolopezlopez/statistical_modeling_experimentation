# A/B Test and Linear Regression Equivalence

This project contains a Jupyter notebook that **proves** that an A/B test (two-sample t-test) is a special case of simple linear regression: both methods give the same t-statistic, p-value, and treatment effect.

---

## 💡 The "Aha!" Moment

When starting out in data, we often learn A/B testing and Regression in different chapters. This project bridges that gap by showing that:
* **A/B Testing** is the "What": Did group B outperform group A?
* **Regression** is the "How": It models the relationship between being in a group and the resulting outcome.

Mathematically, they are two sides of the same coin.

[Image of simple linear regression with a binary predictor]

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
- The