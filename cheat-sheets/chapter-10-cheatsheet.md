## Chapter 10 Cheat Sheet: Bayesian, Linear Algebra & Calculus Foundations

### Bayes' Theorem
`P(A|B) = P(B|A)·P(A) / P(B)`
| Term | Meaning |
|---|---|
| P(A) | Prior |
| P(B\|A) | Likelihood |
| P(B) | Evidence (normalizer) |
| P(A\|B) | Posterior |

**Classic trap:** confusing sensitivity/specificity with posterior probability. Low base rate (prevalence) can make posterior much lower than sensitivity suggests — always recompute with Bayes, don't guess.

### Bayesian vs Frequentist
| Aspect | Frequentist | Bayesian |
|---|---|---|
| Parameter view | Fixed, unknown constant | Random variable with distribution |
| Probability meaning | Long-run frequency | Degree of belief |
| Interval type | Confidence Interval (coverage over repeated sampling) | Credible Interval (probability parameter is in range) |
| Uses prior? | No | Yes |

**Exam note:** CI ≠ "95% probability parameter is in range" — that interpretation belongs to Bayesian credible intervals, not frequentist CIs.

### PCA & Eigen-concepts
- Eigenvectors of covariance matrix = principal component directions
- Eigenvalues = variance explained along each direction
- Sort eigenvalues descending; keep top-k covering target cumulative variance (e.g., ≥90%)
- Practical computation: apply **SVD** to the data matrix (works for non-square matrices); eigendecomposition requires a square, diagonalizable matrix

| Method | Requires square matrix? | Common use |
|---|---|---|
| Eigendecomposition | Yes | Covariance matrix analysis |
| SVD | No | PCA on raw data matrix, dimensionality reduction |

### Gradients & Chain Rule
- Gradient = vector of partial derivatives; points toward steepest ascent
- Gradient descent: `θ = θ − α∇J(θ)`
- Chain rule (backprop): `dL/dw = dL/dy · dy/dz · dz/dw`
- **Vanishing gradient:** sigmoid derivative max = 0.25 → repeated multiplication across layers shrinks gradient to ~0
- **Exploding gradient:** large weights → repeated multiplication grows gradient unbounded

### Stationarity & ARIMA
- Stationary series: constant mean, variance, autocovariance over time
- ADF test: null hypothesis = unit root (non-stationary). High p-value → fail to reject → non-stationary → difference the series
- ARIMA(p, d, q):
  - p = autoregressive order (lagged observations)
  - d = differencing order (integration, achieves stationarity)
  - q = moving average order (lagged forecast errors)

**Common mistake:** fitting ARIMA directly on non-stationary data without checking ADF p-value and setting d appropriately.
