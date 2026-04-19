# Clustering World Economies with K-Means & PCA

## Objective

Apply unsupervised learning to a panel of World Bank development indicators to test whether data-driven country groupings recover the World Bank's income-based classifications and identify structural patterns that single-variable GNI thresholds miss.

## Methodology

- Ingested 10 development indicators for ~160 countries via the `wbgapi` API, spanning income, health, education, infrastructure, environmental, and macroeconomic dimensions, using most-recent-non-empty-value retrieval to handle uneven reporting frequencies across series.
- Applied listwise deletion for countries missing more than 30% of indicators, followed by median imputation for remaining gaps to preserve sample size without distorting central tendency.
- Standardized all features with `StandardScaler` to ensure equal contribution to Euclidean distance calculations, preventing high-variance indicators (GDP per capita) from dominating low-variance ones (infant mortality).
- Fit K-Means with K=4 using k-means++ initialization and fixed random state for reproducibility, then projected the 10-dimensional feature space onto 2D via PCA for visualization.
- Evaluated cluster quality across K=2 through K=10 using both within-cluster sum of squares (elbow method) and mean silhouette score to triangulate on an appropriate K.
- Cross-tabulated K-Means cluster assignments against World Bank income group classifications (Low, Lower-Middle, Upper-Middle, High) to quantify alignment and surface informative mismatches.
- Replicated the full pipeline on the California Housing dataset (20,640 census tracts, 8 features) as a robustness check on the methodology's transferability across data domains.

## Key Findings

- The first two principal components captured 60.6% of total variance (PC1: 46.0%, PC2: 14.6%), with PC1 encoding an interpretable overall development axis and PC2 capturing orthogonal variation tied to inequality and resource intensity.
- Silhouette analysis favored K=2 (score 0.3054), indicating the strongest natural structure in the data is a binary developed-vs-developing split, but K=4 (score 0.2336) was retained for interpretive alignment with the World Bank's operational income tiers.
- K=4 clusters corresponded meaningfully to development tiers: a tightly-grouped high-income cluster (51 countries, avg GDP per capita $69,919, life expectancy 81.3 years), a broad upper-middle cluster (104 countries, $21,663, 74.3 years), a lower-middle cluster (64 countries, $5,333, 65.2 years), and a small anomaly cluster (11 countries) characterized by decoupled income and human development outcomes.
- Cross-tabulation with World Bank classifications showed strong but imperfect alignment: the high-income cluster achieved 96% purity against the High-income group, while roughly one-third of countries landed in a cluster that differed from what their GNI tier alone would predict, with mismatches concentrated among resource-rich and transitional economies.
- The California Housing replication produced a statistically valid but economically weak clustering dominated by latitude and longitude rather than income or housing stock features, illustrating that K-Means recovers whichever axes of variation are most separable in the scaled feature space and that methodology transferability depends on the underlying data exhibiting genuine multidimensional group structure.
- Overall, multidimensional clustering validates income-based classification as a first-order approximation while identifying a systematic subset of countries whose development profiles diverge from their GNI ranking, supporting the case for supplementing single-indicator tiers with composite measures in policy analysis.
