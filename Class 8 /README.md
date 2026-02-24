# Hypothesis Testing & Causal Evidence Architecture

## Objective

Estimation tells you *how big* an effect might be. Falsification tells you *whether to believe it*. This project pivots from point estimation to formal hypothesis testing on the Lalonde (1986) dataset, operationalizing the scientific method as a decision framework for causal inference. Rather than simply computing an Average Treatment Effect (ATE), the goal here is to stress-test that estimate against the Null Hypothesis — the claim that job training produced no real earnings lift — and determine whether the observed signal survives rigorous statistical scrutiny.

The core question is not "What is the effect?" but "Can we reject the world in which there is no effect?" — a subtle but critical distinction for any data scientist building models that inform real resource allocation.

## Technical Approach

- **Parametric Testing (Welch's T-Test via `scipy.stats.ttest_ind`):** Computed the signal-to-noise ratio of the treatment effect by comparing mean real earnings between the treated and control groups. Welch's variant was selected over Student's T-Test to account for unequal variances and sample sizes across groups — a common property of observational program evaluation data.

- **Non-Parametric Validation (Permutation Test, 10,000 resamples):** Because earnings distributions are heavily right-skewed and violate normality assumptions, a permutation test was conducted to construct an empirical null distribution from the data itself. This distribution-free approach validates the parametric result without relying on Central Limit Theorem approximations, providing a second independent line of evidence.

- **Type I Error Control:** Both tests were evaluated against a conventional α = 0.05 significance threshold. The dual-method design — parametric plus non-parametric — functions as an internal replication check, reducing the risk of reporting a false positive driven by distributional artifacts rather than a genuine treatment effect.

## Key Findings

The analysis identified a statistically significant lift in post-intervention real earnings of approximately **$1,795** for program participants. Both the Welch's T-Test and the permutation test rejected the Null Hypothesis, converging on the same conclusion via independent statistical logic. This constitutes a **Proof by Statistical Contradiction**: if the training program had no effect, the probability of observing a difference this large (or larger) under random assignment alone falls below the 5% decision boundary.

## Business Insight

In production ML and analytics environments, hypothesis testing is the **safety valve of the algorithmic economy**. Without it, teams are vulnerable to data dredging — the practice of mining large feature spaces until something "looks significant" by chance alone. Spurious correlations scale dangerously when they enter automated decision systems: a false positive in a recommendation engine wastes ad spend; in a lending model, it encodes bias; in a clinical trial, it costs lives.

Formal falsification enforces discipline. It forces practitioners to articulate a null hypothesis *before* inspecting results, establish a rejection criterion *before* running the test, and distinguish between statistical significance and business materiality *after* the evidence is in. For organizations operating at scale, this isn't academic rigor for its own sake — it's infrastructure-level quality control for every causal claim that flows downstream into strategy, policy, or product.
