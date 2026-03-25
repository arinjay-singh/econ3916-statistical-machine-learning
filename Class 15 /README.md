**The Polynomial Trap: Bias–Variance Tradeoff**

This lab investigates model complexity through two complementary experiments: a controlled synthetic setting and a real-world housing dataset.

Using 50 training observations drawn from a noisy sine wave (y = sin(2πx) + ε), I fit polynomials of degree 1–15 and tracked training versus test RMSE across a held-out 200-point evaluation set. Degrees 3–5 consistently minimized test error, while higher-degree models exhibited the characteristic divergence between training and test performance that defines overfitting. Critically, 5-fold cross-validation selected the same optimal degree as direct test-set evaluation — validating CV as a model selection tool even when holdout data is unavailable.

The second experiment applied the same framework to the Ames Housing dataset (1,460 observations, 80 features). A parsimonious 5-feature linear model outperformed a kitchen-sink specification in cross-validated RMSE, despite the full model achieving higher training R². This gap operationalizes the bias–variance tradeoff in a realistic tabular setting: additional parameters reduced in-sample error while inflating generalization error.

**Tools:** Python, NumPy, scikit-learn (PolynomialFeatures, LinearRegression, cross_val_score), Matplotlib.

**Key takeaway:** Model selection on training metrics alone is systematically misleading. Cross-validation surfaces the complexity penalty that training loss conceals.
