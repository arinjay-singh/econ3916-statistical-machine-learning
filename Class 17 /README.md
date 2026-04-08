# NY Fed Yield Curve Recession Model — Replication
## Objective
Replication of the Federal Reserve Bank of New York's yield curve recession model, fitting a logistic regression on FRED macroeconomic data to generate 12-month-ahead recession probability forecasts analogous to those published monthly by the NY Fed.
## Methodology
- Data: FRED T10Y3M (10Y–3M Treasury yield spread, daily → monthly) and USREC (NBER recession indicator), 1970–present. Predictor is the spread lagged 12 months to align with the forecast horizon.
- Baseline LPM: Linear Probability Model estimated via OLS to motivate the logistic specification; shown to produce out-of-bounds predictions (p < 0, p > 1) on real data.
- Logistic regression: Fitted via scikit-learn LogisticRegression; statsmodels Logit used for coefficient standard errors and 95% confidence intervals.
- Validation: Walk-forward evaluation via scikit-learn TimeSeriesSplit to respect temporal ordering and prevent lookahead leakage.
- Visualization: NY Fed-style chart — predicted recession probability (blue) overlaid with NBER recession shading (red), paired with contemporaneous yield spread panel.
## Key Findings
- LPM pathology confirmed: The linear model generates predicted probabilities outside [0, 1] on held-out data, motivating the logistic specification on first principles.
- Odds ratio: A 1 percentage-point increase in the yield spread multiplies recession odds by the estimated OR (95% CI extracted); a steeper curve is associated with meaningfully lower near-term recession risk.
- 2006–2007: Model produced a directionally correct but low-magnitude signal (<25%) ahead of the 2008–2009 recession — correct in direction, weak in conviction relative to the eventual severity.
- 2022–2024 inversion: Despite the deepest yield curve inversion in decades (10Y–3M reaching ~−1.8pp), the model peaked near 43% — never crossing the 50% decision threshold. No NBER recession materialized, illustrating that a well-calibrated probabilistic forecast is not falsified by a single non-event at elevated probability; the episode also highlights a plausible structural limitation in the model's inability to condition on the source of the inversion.
## Stack
Python · pandas · numpy · scikit-learn · statsmodels · matplotlib · fredapi
