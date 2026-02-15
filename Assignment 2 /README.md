# Audit 02: Deconstructing Statistical Lies

A robustness, probability, and bias audit demonstrating how common statistical measures mislead — and how to defend against them.

---

## Latency Skew

Simulated 1,000 server latency logs: 980 normal-traffic observations (20–50ms) contaminated by 20 extreme spikes (1,000–5,000ms). The standard deviation exploded to **~397ms** while the Median Absolute Deviation held steady at **8ms** — a ~50× gap. The lesson: SD squares deviations, so a handful of outliers hijack the entire measure. Worse, the mean itself gets dragged upward, compounding the distortion for *every* data point. MAD, anchored to the median, is immune to this. Any latency SLA built on mean ± SD would wildly misrepresent system health; MAD gives you the ground truth.

## False Positives

Applied Bayes' Theorem to an academic cheating detector (98% sensitivity, 98% specificity) across three base-rate environments:

| Context | Base Rate | P(Cheater \| Flagged) |
|---|---|---|
| Bootcamp | 50% | **0.98** |
| Econ Class | 5% | **0.72** |
| Honors Seminar | 0.1% | **0.05** |

The same 98%-accurate tool is practically useless in low-prevalence settings — a flagged Honors student has only a 5% chance of actually cheating. This is the **false positive paradox**: when the condition is rare, even highly accurate tests produce overwhelmingly innocent positives. Any automated flagging system deployed without adjusting for base rate will punish the innocent at scale.

## Survivorship Bias

Simulated 10,000 memecoin launches drawn from a Pareto distribution. The top 1% of survivors showed a mean market cap of **~$359,556** — **45.2× the true population mean** of ~$7,961. The median across all tokens was just ~$1,971.

If you only study the coins that "made it," you conclude crypto is a goldmine. Include the 9,900 dead tokens and the picture inverts entirely. Survivorship bias is the engine behind every cherry-picked portfolio backtest and every "10 startups that succeeded" listicle. The graveyard is the dataset that matters.

---

*Built with NumPy, Matplotlib, and manual implementations of MAD, Bayesian inference, and chi-square SRM testing (no black-box libraries).*
