## Feature Engineering & Selection Cheat Sheet

### Categorical Encoding
| Method | Best For | Risk |
|---|---|---|
| One-hot | Low cardinality (<15-20 categories), nominal | Dimensionality explosion at high cardinality |
| Ordinal | Genuine ranked categories | False magnitude relationships if applied to nominal data |
| Target | High-cardinality nominal | Leakage — must use K-fold/out-of-fold + smoothing |
| Frequency/Count | High-cardinality, fast baseline | Collisions when categories share frequency |
| Hashing | Very high cardinality, streaming data | Hash collisions, less interpretable |

### Scaling
| Technique | Formula | Range | Use When |
|---|---|---|---|
| Standardization (Z-score) | (x-μ)/σ | Unbounded, mean=0 std=1 | Linear/logistic regression, SVM, PCA, KNN |
| Normalization (Min-Max) | (x-min)/(max-min) | [0,1] | Neural nets w/ bounded activations, bounded input requirement |

Both are sensitive to outliers; Min-Max is more sensitive since it's anchored to extremes.

### Polynomial / Interaction Features
- `PolynomialFeatures(degree=d, interaction_only=False)` → all terms up to degree d, including single-feature powers
- `interaction_only=True` → excludes single-feature powers, keeps only cross-feature products
- Exam trap: feature count grows combinatorially with degree and original feature count — watch for overfitting risk

### Feature Selection Methods
| Type | Examples | Model-dependent? | Captures Interactions? | Speed |
|---|---|---|---|---|
| Filter | Chi-squared, Mutual Information, Correlation | No | No | Fast |
| Wrapper | RFE, Forward/Backward Selection | Yes | Yes | Slow (combinatorial) |
| Embedded | Lasso (L1), Tree importance | Yes | Partial | Moderate |

### Key Requirements / Traps
- chi2 requires **non-negative** input values — standardized data will error
- Mutual information (sklearn `mutual_info_classif`/`mutual_info_regression`) handles continuous features natively via k-NN estimation — no discretization required
- Lasso (L1) zeroes out coefficients — true feature selection; Ridge (L2) shrinks but never zeroes
- Tree/Gini importance is biased toward high-cardinality and continuous features — use permutation importance for a less biased ranking
- Target encoding MUST use cross-validation/out-of-fold computation to avoid leakage; naive global-mean encoding is a common exam trap

### Exam Domain Weight
Modeling, Analysis, and Outcomes = 24% of exam. Feature engineering/selection is heavily tested within this domain — especially filter vs wrapper vs embedded distinctions, high-cardinality encoding strategy, and polynomial/interaction term generation.
