# The Architecture of Dimensionality: Hedonic Pricing & the FWL Theorem

## Objective
Estimated a multivariate hedonic pricing model on 2026 California residential real estate data to decompose the independent marginal effects of structural and locational attributes on sale price, and formally validated the Frisch-Waugh-Lovell theorem as a proof of OLS's ceteris paribus mechanism.

## Methodology
- **Data:** Synthetic Zillow 2026 California market data comprising `Sale_Price`, `Property_Age`, and `Distance_to_Tech_Hub` across a representative cross-sectional sample
- **Hedonic OLS:** Specified and estimated a multivariate OLS regression via `statsmodels.formula.api`, treating sale price as a linear function of property age and proximity to technology employment centers
- **OVB Diagnostic:** Estimated a bivariate model omitting `Distance_to_Tech_Hub` to isolate and quantify the direction and magnitude of omitted variable bias on the age coefficient
- **FWL Residual Partialling:** Manually implemented the Frisch-Waugh-Lovell theorem by regressing both `Sale_Price` and `Property_Age` on `Distance_to_Tech_Hub`, extracting the respective residual vectors, and re-estimating the slope of interest on the partialled-out components
- **Algebraic Verification:** Confirmed exact numerical equivalence between the FWL-derived coefficient and the multivariate OLS estimate, validating the theorem computationally

## Key Findings
Omitting `Distance_to_Tech_Hub` from the pricing model produced severe upward bias in the coefficient on `Property_Age` — the bivariate model incorrectly attributed excess price appreciation to the physical age of the home, when in fact that variation was driven by the confounded proximity signal. Properties near tech employment hubs are systematically newer, causing age and location to share covariance that a misspecified model cannot disentangle.

Manually partialling out `Distance_to_Tech_Hub` via the FWL theorem stripped this shared variance from both the outcome and the regressor of interest, recovering the true partial effect of age on price. The residual-on-residual regression produced a coefficient numerically identical to the full multivariate estimate — a result that is not approximate, but exact by construction. This confirms that multivariate OLS does not merely *adjust* for covariates statistically; it performs an explicit orthogonal projection, isolating each regressor's contribution to outcome variance in a subspace orthogonal to all other controls.
