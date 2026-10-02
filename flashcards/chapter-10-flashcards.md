## Chapter 10: Bayesian Reasoning, Linear Algebra, and Calculus Foundations — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | State Bayes' theorem formula. | P(A\|B) = P(B\|A)·P(A) / P(B). Exam tip: P(A) = prior, P(B\|A) = likelihood, P(B) = evidence/normalizer, P(A\|B) = posterior. |
| 2 | Bayesian vs Frequentist: how is 'probability' defined in each? | Bayesian: degree of belief, updated with data (parameters are random variables). Frequentist: long-run frequency over repeated trials (parameters are fixed, unknown constants). Exam tip: this is the single most tested distinction in the domain. |
| 3 | What do eigenvalues represent in PCA? | The amount of variance explained along the direction of the corresponding eigenvector. Sorted descending, larger eigenvalue = more important principal component. |
| 4 | What do eigenvectors represent in PCA? | The directions (axes) of maximum variance in the data — the principal components themselves, orthogonal to each other. |
| 5 | SVD decomposition formula and components? | A = UΣVᵀ. U = left singular vectors, Σ = diagonal matrix of singular values, V = right singular vectors. Exam tip: SVD works on any matrix shape, unlike eigendecomposition which requires square matrices. |
| 6 | Eigendecomposition requirement? | A = QΛQ⁻¹ requires A to be a square, diagonalizable matrix. Exam tip: for rectangular data matrices, use SVD instead. |
| 7 | What is a gradient in optimization? | A vector of partial derivatives of a function with respect to each parameter; it points in the direction of steepest ascent. Gradient descent moves opposite to it. |
| 8 | Gradient descent update rule? | θ = θ − α·∇J(θ), where α is the learning rate. Exam tip: too large α causes divergence/oscillation; too small α causes slow convergence. |
| 9 | Chain rule role in backpropagation? | dL/dw = dL/dy · dy/dz · dz/dw — composes local derivatives layer-by-layer to compute gradients for weights deep in the network. |
| 10 | What causes vanishing gradients with sigmoid activations? | Sigmoid derivative max = 0.25. Repeated multiplication of small values across many layers via the chain rule shrinks gradients toward zero in early layers. |
| 11 | Definition of stationarity in a time series? | Mean, variance, and autocovariance structure remain constant over time (do not depend on time index t). Required assumption for standard ARIMA modeling. |
| 12 | ADF test null hypothesis and ARIMA 'd' parameter? | ADF null hypothesis: series has a unit root (non-stationary). High p-value → fail to reject → non-stationary → increase differencing order 'd' in ARIMA(p,d,q) until stationary. |
