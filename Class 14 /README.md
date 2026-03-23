## AI Capex Diagnostic Modeling

**Objective:** Diagnose and remediate structural failures in an OLS revenue forecasting model by identifying heteroscedasticity and multicollinearity in 2026 Nvidia AI capital expenditure and deployment data, and applying HC3-robust standard error correction to restore inferential validity.

**Methodology:**

- Constructed a baseline OLS regression using `statsmodels` to model AI software revenue as a function of capital expenditure tiers and deployment metrics; established naive coefficient estimates and p-values as a diagnostic benchmark
- Performed heteroscedasticity diagnosis via residual-vs-fitted scatter plots and scale-location plots using `matplotlib` and `seaborn`; confirmed systematic variance expansion at high capex tiers consistent with multiplicative error structure
- Assessed multicollinearity across deployment regressors by computing Variance Inflation Factors (VIF); flagged predictors with VIF scores exceeding conventional thresholds indicating redundant explanatory signal
- Re-estimated the model using HC3 heteroscedasticity-consistent covariance estimation, the MacKinnon-White sandwich estimator, to correct standard errors without altering point estimates; compared naive and robust coefficient tables to quantify inferential distortion

**Key Findings:**

The naive OLS specification produced artificially deflated standard errors and inflated t-statistics in the high capex regime, a direct consequence of heteroscedastic error variance that violated the Gauss-Markov homoscedasticity assumption. Deployment metrics that appeared statistically significant under naive OLS lost conventional significance thresholds once HC3-robust standard errors were applied, revealing that the original model overstated confidence in those regressors. The corrected specification provides a statistically defensible basis for inference on AI deployment elasticity across capex tiers, and underscores the practical cost of treating heteroscedasticity as a second-order concern in high-variance capital expenditure data.
