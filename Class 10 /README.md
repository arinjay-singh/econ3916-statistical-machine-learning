**Spurious Correlation & Multicollinearity in Macroeconomic Time-Series**

This project investigates a common pitfall in applied econometrics: the tendency of raw macroeconomic level data to produce misleading correlation and regression estimates due to shared stochastic trends. Using the FRED API, I collected monthly observations for CPI, Unemployment, Fed Funds Rate, Industrial Production, and M2 Money Supply spanning 2010–2024.

The analysis proceeds in three stages. First, I constructed correlation heatmaps on the raw level series using pandas and seaborn to expose spurious relationships driven by co-trending rather than genuine co-movement. Second, I applied Variance Inflation Factor (VIF) diagnostics via statsmodels to quantify multicollinearity, demonstrating that several predictors carry near-redundant information in level form — a direct threat to coefficient interpretability in any downstream regression. Third, I transformed all series into Year-over-Year growth rates to induce stationarity, substantially reducing both spurious correlations and VIF scores. To close the analysis, I constructed Directed Acyclic Graphs (DAGs) to articulate the assumed structural causal pathways among variables, making explicit the economic theory that should govern model specification rather than correlation structure alone.

**Stack:** Python · pandas · seaborn · statsmodels · Plotly · pandas-datareader (FRED)

**Key takeaways:** Pearson correlation on non-stationary series measures co-trending, not co-movement. VIF operationalizes redundancy but does not identify causal direction. DAGs bridge the gap between statistical structure and economic theory, guarding against both omitted variable bias and overcontrol.
