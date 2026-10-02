## Chapter 2: Feature Engineering and Selection Strategies — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Target encoding without regularization on high-cardinality categorical — primary risk? | Target leakage/overfitting. Fix: use out-of-fold (K-fold) target encoding with smoothing toward the global mean. Exam tip: always mention CV-based encoding to avoid leakage. |
| 2 | One-hot vs target encoding — when does one-hot become impractical? | When cardinality exceeds roughly 15-20+ categories, causing sparse, high-dimensional matrices. Exam tip: high-cardinality nominal features → target/frequency/hashing encoding, not one-hot. |
| 3 | Standardization formula | z = (x - mean) / std_dev. Result: mean=0, std=1, unbounded range. Exam tip: used for linear regression, logistic regression, PCA, SVM, KNN. |
| 4 | Min-Max normalization formula and output range | x' = (x - min)/(max - min). Output bounded in [0,1]. Exam tip: use for neural nets with bounded activations or explicit bounded-range requirements; sensitive to outliers. |
| 5 | PolynomialFeatures(degree=2, interaction_only=True) on [A,B] | Produces: A, B, AB (no A², B²). Exam tip: interaction_only excludes same-feature power terms, keeps only cross-feature products. |
| 6 | Filter method examples and key trait | Chi-squared, mutual information, correlation coefficient. Trait: model-agnostic, fast, evaluated independent of any predictive model. Exam tip: filter methods don't capture feature interactions. |
| 7 | Wrapper method examples and key trait | RFE, forward selection, backward elimination. Trait: uses model performance to iteratively select features — computationally expensive, captures interactions. Exam tip: cost grows combinatorially with feature count. |
| 8 | Embedded method examples and key trait | Lasso (L1) regularization, tree-based feature importance (Gini/split gain). Trait: selection happens during model training itself. Exam tip: Lasso shrinks coefficients to exactly zero; Ridge (L2) never does. |
| 9 | chi2 filter test requirement on input features | Requires non-negative feature values (frequency-based statistical test). Exam tip: standardized/negative features will error — use raw counts or min-max scaling before chi2. |
| 10 | Mutual information vs chi-squared — key difference | Mutual information captures linear and non-linear dependencies and works with continuous or categorical variables (via k-NN estimation in sklearn); chi-squared tests independence for categorical/frequency data and requires non-negative values. Exam tip: MI is more general-purpose. |
| 11 | Ordinal encoding vs one-hot — when is ordinal correct? | Only when categories have genuine rank/order (e.g., Low<Medium<High). Exam tip: applying ordinal encoding to nominal (unordered) categories injects false numeric relationships — common exam trap. |
| 12 | Tree-based feature importance methods | Gini importance (mean decrease in impurity) and permutation importance. Exam tip: Gini importance is biased toward high-cardinality/continuous features; permutation importance is more reliable but costlier to compute. |
