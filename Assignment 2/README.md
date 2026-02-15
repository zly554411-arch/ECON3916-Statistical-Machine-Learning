Audit 02: Deconstructing Statistical Lies
Overview

This audit investigates how statistical summaries can mislead decision-makers when data are skewed, rare events are misinterpreted, or failures are excluded from analysis.

Using simulation and statistical testing, this project deconstructs three common sources of distortion:

Latency Skew (Non-Robust Dispersion)

False Positives under Low Base Rates

Survivorship Bias in Heavy-Tailed Markets

Each section demonstrates how seemingly “correct” statistics can produce fundamentally incorrect conclusions when applied without context.

1️⃣ Latency Skew: When Averages Lie
Problem

A system generates response times that are mostly stable but occasionally experience extreme latency spikes. Standard deviation (SD) is often used to measure variability — but is it reliable in heavy-tailed environments?

Method

Simulated 1,000 normal latency observations

Injected 20 extreme spikes

Compared:

Standard Deviation (SD)

Median Absolute Deviation (MAD)

Findings

SD increased dramatically due to squaring large deviations.

MAD remained stable, as it measures dispersion around the median.

A small number of extreme observations inflated perceived system volatility.

Conclusion

Standard deviation is not robust in skewed distributions.

In operational monitoring systems, reliance on SD can exaggerate instability and misinform performance diagnostics. Robust measures like MAD provide more reliable dispersion estimates in the presence of outliers.

2️⃣ False Positives: The Base Rate Fallacy
Problem

A fraud detection model claims:

99% sensitivity

99% specificity

At first glance, this appears highly accurate. But what happens when fraud is rare?

Method

Applied Bayes’ Theorem:

𝑃
(
𝐹
𝑟
𝑎
𝑢
𝑑
∣
𝐹
𝑙
𝑎
𝑔
)
=
𝑆
𝑒
𝑛
𝑠
𝑖
𝑡
𝑖
𝑣
𝑖
𝑡
𝑦
⋅
𝑃
𝑟
𝑖
𝑜
𝑟
𝑆
𝑒
𝑛
𝑠
𝑖
𝑡
𝑖
𝑣
𝑖
𝑡
𝑦
⋅
𝑃
𝑟
𝑖
𝑜
𝑟
+
(
1
−
𝑆
𝑝
𝑒
𝑐
𝑖
𝑓
𝑖
𝑐
𝑖
𝑡
𝑦
)
(
1
−
𝑃
𝑟
𝑖
𝑜
𝑟
)
P(Fraud∣Flag)=
Sensitivity⋅Prior+(1−Specificity)(1−Prior)
Sensitivity⋅Prior
	​


Simulated fraud prevalence rates:

5%

1%

0.1%

Findings

At 5% prevalence → Posterior probability remains meaningful.

At 1% prevalence → Predictive value drops sharply.

At 0.1% prevalence → Most flagged cases are false positives.

Even with 99% accuracy, the majority of alerts can be incorrect when base rates are low.

Conclusion

High model accuracy does not imply high predictive reliability in rare-event environments.

Ignoring base rates leads to:

Overestimation of model performance

Misallocation of investigative resources

False confidence in automated systems

3️⃣ Survivorship Bias: The Graveyard Effect
Problem

Crypto markets often highlight successful tokens while ignoring failures.

If only survivors are analyzed, expected returns appear inflated.

Method

Simulated 10,000 token launches using a Pareto (power-law) distribution.

Assumed ~98% failure rate.

Created two datasets:

df_all → Full population (the graveyard)

df_survivors → Top 2% by peak market cap

Compared mean market capitalization.

Findings

The average market cap among survivors was dramatically higher.

The full distribution showed extreme right skew with most tokens near zero.

Removing failures created an illusion of consistent success.

Conclusion

Survivorship bias systematically inflates perceived profitability.

An analyst observing only surviving tokens would falsely conclude that token launches generate high expected returns.

This demonstrates how selective reporting distorts risk assessment in venture and crypto markets.
