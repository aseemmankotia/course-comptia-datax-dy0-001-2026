## Chapter 4 Cheat Sheet: Regression, Trees & Ensembles

### Regularization: L1 vs L2
| | L1 (Lasso) | L2 (Ridge) |
|---|---|---|
| Penalty | λΣ\|w\| | λΣw² |
| Sparsity | Yes — zeros out coefficients | No — shrinks but rarely zero |
| Use case | Feature selection, many irrelevant features | Multicollinearity, keep all features |
| Elastic Net | l1_ratio blends both (0=Ridge, 1=Lasso) | |

### Linear Regression Assumptions
1. Linearity (X→y linear in coefficients)
2. Independence of errors
3. Homoscedasticity (constant residual variance)
4. Normality of **residuals** (not raw features)

### Logistic Regression
- Cost: log loss / binary cross-entropy
- C = inverse regularization strength (small C = strong regularization = more bias)

### Tree Splitting Criteria
| Criterion | Formula | Task | Notes |
|---|---|---|---|
| Gini | 1 − Σpᵢ² | Classification | Default in sklearn, faster |
| Entropy | −Σpᵢ log₂pᵢ | Classification | Slightly more sensitive |
| MSE | Σ(y−ȳ)² | Regression | Standard default |
| MAE | Σ\|y−ȳ\| | Regression | Robust to outliers |

### Bagging vs Boosting (HEAVILY TESTED)
| | Bagging | Boosting |
|---|---|---|
| Training | Parallel, independent | Sequential, dependent |
| Data sampling | Bootstrap (with replacement) | Reweighted / residual-focused |
| Primary effect | Reduces **variance** | Reduces **bias** |
| Overfitting risk | Low | Higher if untuned |
| Examples | Random Forest, Bagged trees | AdaBoost, Gradient Boosting, XGBoost, LightGBM |

### Random Forest Defaults
- max_features: sqrt(n) classification, n regression (or n/3 common manual choice)
- More trees → lower variance, diminishing returns after a point

### Gradient Boosting Key Params
- learning_rate (shrinkage): typical 0.01–0.3
- n_estimators, max_depth, subsample, colsample_bytree
- reg_alpha (L1), reg_lambda (L2) — XGBoost regularization

### SVM Kernels (HEAVILY TESTED)
| Kernel | Use Case |
|---|---|
| Linear | Linearly separable data, high-dim sparse (e.g., text) |
| Polynomial | Curved boundary, interaction features, degree matters |
| RBF (Gaussian) | Default for unknown non-linear boundaries |
| Sigmoid | Rarely optimal, behaves like neural net layer |

- **C**: high C = narrow margin, low bias/high variance; low C = wide margin, high bias/low variance
- **gamma** (RBF): high gamma = tight fit/overfit risk; low gamma = smoother/underfit risk

### Stacking vs Blending
| | Stacking | Blending |
|---|---|---|
| Meta-model input | Out-of-fold (k-fold) predictions | Single held-out validation predictions |
| Data efficiency | Higher (uses full training set) | Lower (wastes held-out portion) |
| Leakage risk | Lower | Slightly higher |

### Exam Traps
- Confusing which method reduces bias vs variance (Bagging=variance, Boosting=bias)
- Assuming L1 and L2 are interchangeable for sparsity — only L1 zeros coefficients
- Picking linear/polynomial kernel when data needs RBF for unknown non-linear boundary
- Forgetting normality assumption applies to residuals, not raw features
