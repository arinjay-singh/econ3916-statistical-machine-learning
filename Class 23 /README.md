# FedSpeak Analysis — NLP on FOMC Minutes

## Objective

Apply natural language processing and unsupervised learning to two decades of Federal Open Market Committee meeting minutes to quantify shifts in central bank communication tone, identify structural breaks in monetary policy language, and test whether algorithmic clustering recovers recognizable policy regimes.

## Methodology

- Ingested FOMC meeting minutes spanning 2000 to present, then preprocessed the corpus through tokenization, lemmatization, and stopword removal to normalize vocabulary and reduce noise from procedural boilerplate.
- Constructed a TF-IDF document-term matrix with `min_df=5`, `max_df=0.85`, and `max_features=2000`, incorporating both unigrams and bigrams to capture policy-relevant phrases (monetary policy, labor market, inflation expectations) alongside individual terms.
- Computed Loughran-McDonald sentiment scores using the finance-specific lexicon to measure both net sentiment (positive minus negative word frequency) and uncertainty (hedging language frequency), normalized by document length to control for varying minutes length.
- Reduced the 2,000-dimensional TF-IDF matrix to 50 components via TruncatedSVD (preserving 79.9% of variance), then applied K-Means clustering with K=3 to identify distinct communication regimes across the sample period.
- Visualized clusters in 2D PCA projection space with key policy dates annotated (December 2008 Lehman aftermath, March 2020 COVID response, June 2022 tightening pivot) to validate temporal alignment of algorithmically-identified regimes.
- Segmented the corpus into pre-COVID (before March 2020) and post-COVID (March 2020 onward) subsamples, then compared sentiment distributions via kernel density estimation and boxplots to isolate the effect of the pandemic-era policy environment on Fed communication.

## Key Findings

- K-Means clustering identified a sharp structural break in FOMC language at December 16, 2008, the exact meeting where the Fed cut rates to the zero lower bound and launched quantitative easing, with one cluster (79 documents) cleanly capturing the pre-GFC era from March 2000 to October 2008 and a second cluster (134 documents) spanning the entire post-crisis period through the present.
- The hypothesized post-COVID regime did not emerge as linguistically distinct from the broader post-2008 era, suggesting the Fed adapted to the pandemic using communication vocabulary already developed during the GFC rather than generating a fundamentally new policy lexicon.
- A third cluster (27 documents spanning the full sample period) captured meetings with distinctive thematic vocabulary on an orthogonal dimension, indicating that while the dominant structure in FOMC language is temporal, a secondary axis reflects topic-specific variation that cuts across policy regimes.
- Loughran-McDonald sentiment analysis validated face validity by independently identifying December 16, 2008 as the most negative meeting in the sample and June 30, 2004 (the start of the mid-2000s tightening cycle) as the most positive, confirming the lexicon captures genuine economic tone rather than noise.
- Post-COVID net sentiment declined roughly 65% relative to the pre-COVID baseline (0.0028 vs 0.0081), reflecting the compounding effects of the pandemic, supply chain disruptions, the 2021-2022 inflation surge, and the fastest tightening cycle since the 1980s.
- Uncertainty language remained essentially flat across the two periods (0.0212 vs 0.0219), indicating the Fed did not increase its rate of hedging or probabilistic qualifiers but rather shifted toward more explicitly negative framing, which is consistent with a communication strategy of maintaining forecast confidence while acknowledging adverse conditions directly.
- The post-COVID sentiment distribution was also narrower and more concentrated near zero than the pre-COVID distribution, suggesting the Fed's tone became not just more negative but also more consistently so across meetings, reflecting a sustained period of elevated economic stress rather than isolated shocks.
- Overall, the combination of clustering and sentiment analysis demonstrates that FOMC communication exhibits a single sharp regime break (2008) with continuous tonal variation within regimes, and that quantitative NLP methods can recover both structural shifts and gradual policy orientation changes that align with recognizable macroeconomic events.
