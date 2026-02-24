# Recovering Experimental Truths via Propensity Score Matching

## Objective

This project demonstrates how propensity score matching can recover credible causal estimates from observational data that would otherwise produce severely biased treatment effect estimates due to systematic selection into treatment.

## Methodology

- **Diagnosed selection bias** in the observational subset of the Lalonde (1986) dataset, where naive comparison of treated and control groups yielded a spurious treatment effect of approximately −$15,204—directionally opposite to the experimentally established ground truth.
- **Estimated propensity scores** via logistic regression, modeling the probability of treatment assignment as a function of observed pre-treatment covariates (age, education, earnings history, employment status, race, and marital status).
- **Implemented nearest-neighbor matching** to construct a synthetic counterfactual control group by pairing each treated unit with its closest match in propensity score space, thereby approximating the covariate balance achieved by random assignment.
- **Validated covariate balance** post-matching to confirm that systematic differences between treatment and control groups were substantially reduced across all observed confounders.

## Key Findings

Propensity score matching corrected the naive observational estimate from **−$15,204** to approximately **+$1,800**, successfully recovering a treatment effect consistent with the Lalonde experimental benchmark. This ~$17,000 swing illustrates both the magnitude of selection bias present in unmatched observational comparisons and the power of well-executed matching estimators to recover experimental truths from non-experimental data.

## Stack

Python · Pandas · Scikit-Learn · Logistic Regression · Nearest-Neighbor Matching
