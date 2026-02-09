# Lab 6: The Architecture of Bias

**Investigating the Data Generating Process (DGP), Sampling Bias, and Selection Mechanisms in Machine Learning**

## Objective

This lab provides a hands-on forensic investigation into how bias enters machine learning pipelines *before* a model is ever trained — at the level of data collection, sampling, and experimental design. Using the Titanic dataset and simulated A/B test data, we demonstrate three core failure modes: sampling error from naive random sampling, covariate shift from unstratified splits, and sample ratio mismatch (SRM) from broken experimental infrastructure.

## Tech Stack

Python · pandas · NumPy · SciPy (Chi-Square) · scikit-learn (StratifiedShuffleSplit)

## Methodology

### 1. Simple Random Sampling & High-Variance Failure

Drew repeated simple random samples from the Titanic dataset to empirically show that naive SRS produces unstable class distributions across draws. Measured variance in survival-rate estimates to quantify sampling error and demonstrate why SRS alone is insufficient for ML train/test splits on imbalanced data.

### 2. Stratified Sampling to Eliminate Covariate Shift

Replaced SRS with `StratifiedShuffleSplit` from scikit-learn, stratifying on the target variable to guarantee that train and test sets mirror the population's class distribution. Compared distributional stability against the SRS baseline, confirming that stratification eliminates the covariate shift observed in Method 1.

### 3. Sample Ratio Mismatch (SRM) Forensic Audit

Simulated an A/B test with a planned 50/50 allocation (n = 1,000) that produced an anomalous 550/450 split. Applied a Chi-Square goodness-of-fit test (`scipy.stats.chisquare`) to formally detect SRM (χ² = 10.0, p ≈ 0.0016). A deviation of ~3.16σ from the expected mean rules out natural variance, indicating a systematic engineering failure (e.g., broken load balancer, bot contamination, or redirect asymmetry) that would invalidate any downstream causal inference.

## Theoretical Extension: Survivorship Bias & the Heckman Correction

### The Problem

Analyzing only successful Unicorn startups from sources like TechCrunch produces **survivorship bias** — a form of **selection on the dependent variable**. The observed dataset is filtered through a selection mechanism (only companies that reached $1B+ valuation are covered), which truncates the joint distribution of features and outcomes. Any model trained on this data learns the characteristics of *survivors conditional on survival*, not the characteristics that *cause* success.

Concretely, this creates two distortions:

- **Inflated feature-outcome correlations.** If both "aggressive burn rate" and "success" are required for a startup to appear in the dataset, the data will show a spurious positive correlation between burn rate and success — even if aggressive spending *increases* the probability of failure in the full population.
- **Missing counterfactual mass.** The failed startups that shared identical observable features with the unicorns are absent. Without this *ghost data*, it is impossible to estimate the true conditional probability P(Success | Features).

### The Ghost Data

The specific ghost data required consists of **observations from the non-selected population**: startups that received comparable funding, operated in similar markets, and shared similar founding-team profiles, but failed to reach unicorn status — the companies that *could have* appeared in TechCrunch but didn't. This includes both outright failures and modest-outcome companies that never triggered media coverage.

### The Heckman Correction

A **Heckman two-stage selection model** addresses this by explicitly modeling the selection mechanism:

1. **Selection Equation (Stage 1):** Estimate a probit model for the probability of appearing in the dataset — i.e., P(Observed | Z), where Z includes variables that influence media coverage or survival but are excludable from the outcome equation (e.g., geographic proximity to tech media hubs, founder public visibility, or PR spend).

2. **Outcome Equation (Stage 2):** Include the **Inverse Mills Ratio (λ)** — derived from Stage 1 — as a correction term in the substantive regression. λ captures the expected bias from truncation, effectively reconstructing the contribution of the missing ghost data to the outcome distribution.

The key identification requirement is at least one valid **exclusion restriction**: a variable that predicts selection into the dataset but has no direct causal effect on the outcome of interest. Without this, the correction is unidentified and λ absorbs specification error.
