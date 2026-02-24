# Hypothesis Testing & Causal Evidence Architecture

## The Epistemology of Falsification: Hypothesis Testing on the Lalonde Dataset

---

## Objective

Most applied data science stops at *estimation* — fitting a model, reading a coefficient, and shipping a result. This project goes one step further by operationalizing **falsification**: the rigorous, Popperian process of stress-testing a causal claim until it either breaks or holds.

Using the Lalonde (1986) randomized experimental dataset — the canonical benchmark of causal inference — I adjudicate between two competing narratives: did job training *cause* a measurable lift in real earnings, or is the observed difference statistical noise masquerading as signal?

---

## Technical Approach

- **Signal-to-Noise Decomposition via Welch's T-Test** — Rather than treating the T-statistic as a black-box output, I explicitly decompose it as a signal-to-noise ratio: the Average Treatment Effect (ATE) in the numerator, pooled standard error in the denominator. This framing makes the inferential logic transparent and auditable.

- **Non-Parametric Validation via Permutation Testing** — Earnings distributions are notoriously heavy-tailed and right-skewed, violating the normality assumptions that parametric tests rely on. To guard against this, I ran a 10,000-resample permutation test using `scipy.stats.permutation_test`, constructing an empirical null distribution by randomly shuffling treatment labels. Convergence between the parametric and non-parametric p-values confirms the result is not an artifact of distributional assumptions.

- **Type I Error Control** — All hypothesis tests were evaluated against a pre-specified significance threshold of α = 0.05, enforced *before* observing results. This commitment to a fixed decision boundary is a deliberate safeguard against p-hacking and post-hoc threshold adjustment — two of the most common failure modes in exploratory data analysis.

- **Tooling** — `scipy.stats`, `pandas`, `seaborn` (KDE visualization of counterfactual distributions)

---

## Key Findings

The analysis finds a statistically significant Average Treatment Effect of approximately **+$1,795 in real 1978 earnings** among participants who received job training versus the control group. The null hypothesis — that training had no effect — is rejected via **Proof by Statistical Contradiction**: the probability of observing a difference this large under the null is sufficiently low that chance is no longer a credible explanation.

Both the parametric T-test and the non-parametric permutation test converge on consistent p-values, strengthening confidence that the result is robust to modeling assumptions.

---

## Business Insight: Hypothesis Testing as the Safety Valve of the Algorithmic Economy

At scale, data is not neutral — it is a surface for spurious correlations to hide in plain sight. Every additional feature, every new cohort cut, every model iteration is an opportunity to find a pattern that *looks* real but isn't. This is the core problem of **data dredging**: when you interrogate data long enough, it will eventually confess to something, whether or not it's true.

Rigorous hypothesis testing — with pre-specified thresholds, non-parametric validation, and explicit null hypotheses — functions as the **safety valve** of the algorithmic decision pipeline. It forces a separation between *exploration* and *confirmation*, between a pattern observed and a claim earned. In product, policy, or financial contexts where model outputs drive real decisions, this discipline is not academic overhead. It is the mechanism that keeps false positives from becoming strategy.

The Lalonde dataset is a reminder that even in a cleanly randomized experiment, the inferential machinery still needs to be run correctly. In observational settings — which is most of industry — the stakes are considerably higher.

---

*Dataset: Lalonde (1986) Experimental Subset | Testing Framework: scipy.stats | Resamples: 10,000*
