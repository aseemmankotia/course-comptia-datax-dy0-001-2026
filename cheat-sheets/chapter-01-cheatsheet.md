## Chapter 1 Cheat Sheet — EDA & Data Quality Triage

### Missing Data Mechanisms
| Mechanism | Missingness depends on... | Valid Fix |
|---|---|---|
| MCAR | Nothing (pure randomness) | Listwise deletion OK |
| MAR | Observed variables only | Model-based/conditional imputation |
| MNAR | The unobserved value itself | Missingness indicator + sensitivity/selection model |

**Trap:** Mean/median imputation assumes MCAR/MAR — invalid under MNAR.

### Outlier Detection Methods
| Method | Type | Best For | Key Threshold |
|---|---|---|---|
| Z-score | Univariate | Roughly normal data | \|z\| > 3 |
| IQR | Univariate | Skewed/non-normal, robust | Q1−1.5×IQR / Q3+1.5×IQR (standard); ×3.0 = extreme |
| Isolation Forest | Multivariate | Correlated, non-linear, high-dim | contamination param sets expected outlier % |

### Data Leakage Types
| Type | Cause | Example |
|---|---|---|
| Target leakage | Feature encodes post-outcome info | 'refund_issued' predicting fraud |
| Train-test contamination | Preprocessing fit on full data before split | Scaler fit on train+test combined |

**Fix:** Split → fit preprocessing on train only → transform test with train params. Use sklearn `Pipeline`.

### Class Imbalance Remedies
| Technique | Data Impact | Cost | Use When |
|---|---|---|---|
| SMOTE | Adds synthetic minority rows | Highest | Need more minority signal, synthetic data OK |
| Random undersampling | Removes majority rows | Medium (less data) | Majority class is huge/redundant |
| Class weights | No row changes | Lowest | Want all data kept, cheapest option |

SMOTE default `k_neighbors=5` (imbalanced-learn). `class_weight='balanced'` reweights loss inversely to class frequency.

### Skewness Transforms
| Transform | Requires | Notes |
|---|---|---|
| Log(x) or log(x+1) | x > 0 (or ≥0 with +1) | Simplest fix for right skew |
| Box-Cox | x > 0 strictly | Finds optimal lambda |
| Yeo-Johnson | Any real value incl. negatives/zero | Generalized Box-Cox |

### Correlation vs Causation
Always check for: **confounding variables**, **reverse causality**, **coincidence**. Classic exam example: ice cream sales & drownings — confounded by warm weather.

### Exam Notes
- MNAR + missingness indicator is heavily tested — don't default to mean imputation.
- IQR multiplier 1.5 (standard) vs 3.0 (extreme) is a common swap trap.
- Leakage questions test whether you can spot a feature that's only known AFTER the target event.
- Class imbalance questions test constraints (no synthetic data allowed → class weights; can't lose data → avoid undersampling).
