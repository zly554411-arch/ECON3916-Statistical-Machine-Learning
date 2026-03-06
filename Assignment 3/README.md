# SwiftCart Econometric Analysis: Bias Correction and Causal Inference

## Project Overview

This project analyzes several statistical and econometric problems using Python.  
The objective is to demonstrate how modern empirical methods can address issues such as skewed distributions, invalid parametric assumptions, and selection bias in observational data.

The analysis is divided into four phases:

1. Bootstrap inference for skewed tip distributions  
2. Non-parametric permutation testing for A/B experiments  
3. Propensity Score Matching (PSM) for causal inference  
4. Covariate balance diagnostics using a Love Plot  

All code was implemented in Python using **NumPy, pandas, scikit-learn, seaborn, and matplotlib**.

---

## Phase 1: Bootstrap Inference on Skewed Data

Driver tips exhibit two problematic characteristics:

- **Zero inflation** (many users tip $0)
- **Heavy right skew** due to occasional large tips

Because the sampling distribution of the median is unknown under this distribution, a **bootstrap resampling approach** was used.

Procedure:
- Generate a dataset with **100 zero tips** and **150 exponential tips**
- Resample the dataset **10,000 times with replacement**
- Compute the **median tip** for each bootstrap sample
- Construct a **95% confidence interval** using percentile methods

Bootstrap methods provide a robust way to estimate uncertainty when traditional assumptions (normality) do not hold.

---

## Phase 2: Non-Parametric Permutation Test

An A/B experiment tested whether the **Batch Routing algorithm** reduced delivery times.

Data generation:
- Control group: Normal distribution (mean = 35 minutes, sd = 5)
- Treatment group: Log-normal distribution (highly skewed)

Because treatment data contains **extreme outliers**, the **homoscedasticity assumption of a t-test is violated**.

A **Permutation Test** was therefore used:

1. Combine all 1000 delivery observations
2. Randomly shuffle them
3. Split into two groups of 500
4. Calculate the difference in means
5. Repeat the process **5000 times**

The **empirical p-value** is the proportion of simulated differences that are at least as extreme as the observed difference.

This approach avoids distributional assumptions and produces a valid significance test even with skewed data.

---

## Phase 3: Propensity Score Matching (PSM)

### The Selection Bias Problem

The marketing team claims SwiftPass subscribers spend **300% more per month** than non-subscribers.  
However, this comparison suffers from **selection bias** because heavy users are more likely to voluntarily subscribe.

### Naive Estimate

The **Simple Difference in Means (SDO)** compares average post-treatment spending:
SDO = E[Y | D = 1] − E[Y | D = 0]


This estimate mixes the **true program effect** with **pre-existing differences between users**.

### Propensity Score Matching

To isolate the causal effect, we estimate each user's probability of subscribing using **pre-treatment characteristics**:

- pre_spend
- account_age
- support_tickets

A **Logistic Regression model** estimates the propensity score:
P(D = 1 | X)


Each subscriber is then matched with the **nearest non-subscriber** using a **Nearest Neighbors algorithm**.

### Average Treatment Effect on the Treated (ATT)

The causal effect is estimated as:


ATT = E[Y₁ − Y₀ | D = 1]

where the matched control group approximates the counterfactual outcome.

Results from the example:

| Method | Estimated Effect |
|------|------|
| Naive SDO | $17.57 |
| PSM ATT | $10.14 |

The smaller ATT indicates that a substantial portion of the naive difference was caused by **self-selection of high-usage users into the loyalty program**, not the program itself.

---

## Phase 4: Love Plot (Covariate Balance Diagnostics)

After matching, it is essential to verify whether the treated and control groups are balanced.

A **Love Plot** visualizes **Standardized Mean Differences (SMD)** for each covariate before and after matching.

Standardized Mean Difference:
SMD = (Mean_Treated − Mean_Control) / Pooled Standard Deviation


Interpretation:

- |SMD| < 0.1 → acceptable balance
- |SMD| < 0.05 → excellent balance

If post-matching values cluster near **zero**, it provides visual evidence that **selection bias has been mitigated**.

---

## Libraries Used

- numpy
- pandas
- scikit-learn
- seaborn
- matplotlib

---

## Conclusion

This project demonstrates several key econometric techniques used in empirical research:

- **Bootstrap methods** for inference under non-normal distributions
- **Permutation testing** when classical parametric tests are invalid
- **Propensity Score Matching** to correct selection bias in observational data
- **Love Plots** for validating covariate balance

Together, these tools allow researchers to produce more credible causal estimates when working with real-world data.
