## Chapter 10: Bayesian Reasoning, Linear Algebra, and Calculus Foundations — Practice Questions

**Q1.** A medical test for a disease with 1% prevalence has 99% sensitivity and 95% specificity. A patient tests positive. Using Bayes' theorem, what is P(disease | positive test)?

A) 99%
B) 16.7%
C) 95%
D) 50%

<details>
<summary>Answer</summary>

**Correct: B**

P(D|pos) = [P(pos|D)P(D)] / P(pos) = (0.99×0.01) / (0.99×0.01 + 0.05×0.99) = 0.0099/0.0594 ≈ 16.7%. Low prevalence dominates even a highly accurate test.

**Why the others are wrong:**
- 99% confuses sensitivity (P(pos|D)) with the posterior P(D|pos) — the most common exam trap.
- 95% confuses specificity with the answer being asked.
- 50% assumes equal weighting of prior and likelihood with no base-rate correction.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A frequentist statistician reports a 95% confidence interval of [2.1, 4.3] for a parameter. Which interpretation is CORRECT under frequentist theory?

A) There is a 95% probability the true parameter lies in [2.1, 4.3]
B) The parameter has a 95% credible probability distribution centered in this range
C) If the experiment were repeated many times, 95% of such constructed intervals would contain the true parameter
D) 95% of the data falls within this interval

<details>
<summary>Answer</summary>

**Correct: C**

Frequentist CIs are about long-run coverage of the interval-construction procedure — the parameter is fixed, not random.

**Why the others are wrong:**
- This is the Bayesian credible-interval interpretation, a classic swapped-answer trap.
- 'Credible' language belongs to Bayesian posterior distributions, not frequentist CIs.
- Confidence intervals describe the parameter estimate, not the raw data spread.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A team performs PCA on a dataset and obtains eigenvalues [8.2, 3.1, 0.4, 0.1] for the covariance matrix. They want to retain components explaining at least 90% of variance. How many components should they keep?

A) 1
B) 3
C) 4
D) 2

<details>
<summary>Answer</summary>

**Correct: D**

Total variance = 11.8. Component 1 = 69.5%, +Component 2 = 95.8% cumulative, which exceeds 90%. Keep 2 components.

**Why the others are wrong:**
- 1 component only covers 69.5%, below the 90% threshold.
- 3 components (99.2%) retains unnecessary dimensions, wasting compression.
- 4 keeps all dimensions, defeating the purpose of PCA dimensionality reduction.

</details>

---

**Q4.** You need to decompose a non-square (rectangular) data matrix to compute principal components efficiently. Which decomposition method should you use?

A) Singular Value Decomposition (SVD)
B) Eigendecomposition of the raw data matrix directly
C) LU decomposition
D) Cholesky decomposition

<details>
<summary>Answer</summary>

**Correct: A**

SVD (A = UΣVᵀ) works on any m×n matrix and is the standard practical method for computing PCA without explicitly forming the covariance matrix.

**Why the others are wrong:**
- Eigendecomposition requires a square matrix — applying it directly to a rectangular data matrix is undefined.
- LU decomposition is for solving linear systems, not extracting variance-maximizing directions.
- Cholesky requires a symmetric positive-definite square matrix and is used for covariance factorization, not raw rectangular data.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** During backpropagation in a deep network using sigmoid activations, gradients in early layers become extremely small after several layers. Which concept explains this, applying the chain rule?

A) Vanishing gradients — repeated multiplication of small sigmoid derivatives (max 0.25) shrinks the gradient toward zero
B) Exploding gradients from large weight initialization
C) Overfitting due to too many parameters
D) Learning rate set too high causing divergence

<details>
<summary>Answer</summary>

**Correct: A**

The chain rule multiplies local derivatives layer by layer; sigmoid's derivative max is 0.25, so many multiplications compound toward zero — the vanishing gradient problem.

**Why the others are wrong:**
- Exploding gradients produce large, not small, values — the opposite symptom.
- Overfitting relates to generalization gap, not gradient magnitude during backprop.
- A high learning rate causes oscillation/divergence, not systematically shrinking gradients.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** An Augmented Dickey-Fuller (ADF) test on a time series returns a p-value of 0.62. What should you conclude and do next before fitting ARIMA?

A) The series is stationary; fit ARIMA with d=0
B) The series has seasonality; apply Fourier transform only
C) The p-value is irrelevant to stationarity testing
D) The series is non-stationary; difference the series (increase d) and re-test

<details>
<summary>Answer</summary>

**Correct: D**

ADF null hypothesis is 'series has a unit root (non-stationary)'. A p-value of 0.62 fails to reject the null, indicating non-stationarity — differencing is required to increase d.

**Why the others are wrong:**
- A high p-value fails to reject non-stationarity — it does not indicate stationarity, reversing the correct conclusion.
- Seasonality is a separate issue from the unit-root test; Fourier transforms don't address ADF results directly.
- The p-value is exactly the mechanism used to test stationarity in this method.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Which parameter in ARIMA(p, d, q) represents the number of times the raw series must be differenced to achieve stationarity?

A) p
B) q
C) d
D) None — differencing is unrelated to ARIMA parameters

<details>
<summary>Answer</summary>

**Correct: C**

'd' is the integration order — the number of differencing operations applied to make the series stationary before fitting AR and MA terms.

**Why the others are wrong:**
- p is the autoregressive order (number of lagged observations used).
- q is the moving average order (number of lagged forecast errors used).
- Differencing is the 'I' (Integrated) component and is central to ARIMA's design.

</details>

---

**Q8.** Which statement correctly differentiates the Bayesian and frequentist paradigms as tested on the exam?

A) Bayesian treats parameters as fixed unknowns; frequentist treats them as random variables with distributions
B) Bayesian incorporates a prior belief updated by data into a posterior; frequentist relies solely on the observed data's long-run frequency properties
C) Frequentist methods always require more data than Bayesian methods
D) Bayesian and frequentist approaches always produce identical point estimates

<details>
<summary>Answer</summary>

**Correct: B**

Bayesian inference formally combines a prior distribution with the likelihood via Bayes' theorem to produce a posterior; frequentist inference treats parameters as fixed and evaluates estimator behavior over repeated sampling.

**Why the others are wrong:**
- This reverses the actual definitions — a classic swapped-terms distractor.
- Data requirements depend on the model and problem, not the paradigm itself.
- The two frameworks can and often do diverge, especially with strong priors or small samples.

</details>

---

