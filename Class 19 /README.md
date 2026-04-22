# Tree-Based Models: Random Forests

## Objective

Benchmark tree-based regressors against a regularized linear baseline on California Housing data to quantify the predictive lift from capturing nonlinear structure and feature interactions, and examine whether predictive importance maps onto causal interpretation.

## Methodology

- Fit three regressors on 20,640 California Housing observations (8 features, 80/20 train-test split): an unrestricted Decision Tree, Ridge Regression as a regularized linear baseline, and a 100-tree Random Forest.
- Tuned Random Forest hyperparameters via 5-fold `GridSearchCV` over `n_estimators`, `max_depth`, and `max_features`, selecting on cross-validated RMSE.
- Extracted Mean Decrease in Impurity (MDI) importance from training and compared it against permutation importance computed on the held-out test set, separating split-based signal from out-of-sample contribution.
- Reframed the target as a binary classification problem (price above vs. below median) and compared Random Forest AUC against logistic regression to test whether the tree ensemble's advantage generalizes beyond regression loss.
- Packaged results into an interactive Plotly and ipywidgets dashboard exposing `n_estimators` and `max_features` sliders tied to live-updating model comparison and feature importance panels.

## Key Findings

- Random Forest achieved Test R² = 0.8051 against Ridge R² = 0.5759, a 22.9-point gap that isolates the variance explained by nonlinear interactions the linear baseline cannot capture.
- The single Decision Tree hit Train R² = 1.0 and Test R² = 0.6221, a textbook high-variance signature that the Random Forest dampens via bootstrap aggregation while retaining low bias.
- MDI and permutation importance agreed on the top two features (MedInc and Latitude) but diverged on the third: MDI ranked AveOccup third while permutation ranked Longitude third, consistent with MDI's known bias toward high-cardinality continuous features that offer more candidate splits.
- The causal caveat holds despite the strong predictive signal from MedInc. Median income is almost certainly entangled with unobserved neighborhood-quality factors (schools, amenities, employment access) that drive both income and price, so intervening on income alone is not expected to produce the predicted price response.

## Stack

Python, scikit-learn, pandas, NumPy, Matplotlib, Plotly, ipywidgets
