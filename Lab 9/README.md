# Recovering Experimental Truths via Propensity Score Matching

---

## Objective

Demonstrated that observational data, left uncorrected, produces directionally wrong causal estimates — and applied Propensity Score Matching to surgically remove selection bias and recover a treatment effect consistent with the randomized experimental benchmark.

---

## The Problem: Observational Failure

The Lalonde observational dataset is a controlled trap. Unlike the randomized experimental subset, participants *self-selected* into job training — meaning the treated and control groups differ systematically on pre-treatment characteristics like prior earnings, education, and employment history. Running a naive comparison on this data produces an estimated treatment effect of **-$15,204**: not just wrong in magnitude, but wrong in direction. The data, taken at face value, suggests job training *destroys* earnings. This is the textbook definition of **Selection Bias** — and the core failure mode of uncritical observational analysis.

---

## Methodology

- **Selection Bias Modeling** — Identified the confounders driving both training participation and earnings outcomes: age, education, race, marital status, degree attainment, and real earnings in 1974 and 1975. These pre-treatment variables define the selection mechanism that must be controlled.

- **Propensity Score Estimation** — Fit a logistic regression model to estimate each individual's conditional probability of receiving treatment given their observed covariates, P(treat = 1 | X). This scalar score collapses the multi-dimensional confounder space into a single balancing quantity — the propensity score.

- **Nearest Neighbor Matching** — Implemented 1:1 nearest neighbor matching with replacement using Scikit-Learn, pairing each treated unit to its closest control unit in propensity score space. Matching with replacement was chosen deliberately: the observational control pool is large but sparse in the relevant covariate region, and forcing unique matches would introduce worse bias than it removes.

- **Balance Validation** — Verified covariate balance post-matching using Standardized Mean Differences (SMD), confirming that all covariates fell below the SMD < 0.1 threshold — the accepted industry standard for declaring groups exchangeable.

- **Tooling** — Python, Pandas, Scikit-Learn (`LogisticRegression`, `NearestNeighbors`), SciPy

---

## Key Findings

| Estimate | Method | Value |
|---|---|---|
| Naive ATE | Raw difference in means (no adjustment) | -$15,204 |
| Recovered ATE | Post-matching difference in means | ~+$1,800 |
| Experimental Benchmark | Lalonde (1986) RCT ground truth | ~+$1,794 |

The matched estimate recovers the randomized experimental benchmark to within rounding error — a result that is both statistically significant and directionally correct. The $17,000 swing between the naive and corrected estimates is not a modeling artifact; it is the measurable cost of ignoring selection bias. This exercise validates that when the selection mechanism is correctly modeled and controlled, observational data can be rehabilitated to approximate experimental-quality causal inference.

---

## Why It Matters

In industry, true randomization is expensive, slow, or ethically constrained. Propensity Score Matching is one of the workhorses of applied causal inference precisely because it operates on data that already exists — historical records, administrative data, platform logs. But the Lalonde exercise is also a warning: the method only works if the analyst correctly identifies and models the selection mechanism. A misspecified propensity model produces a false sense of balance and a biased estimate dressed in the language of rigor. The discipline is not in running the algorithm — it is in understanding *why* the selection happened in the first place.

---

*Dataset: Lalonde Observational Subset | Matching: 1:1 Nearest Neighbor with Replacement | Balance Criterion: SMD < 0.1*
