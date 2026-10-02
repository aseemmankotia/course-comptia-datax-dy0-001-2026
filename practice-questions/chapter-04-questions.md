## Chapter 4: Supervised Learning: Regression, Trees, and Ensembles — Practice Questions

**Q1.** A model trained on a fraud detection dataset shows 99% accuracy on training data but only 62% on validation data. The data science team wants an ensemble method that primarily reduces variance without significantly increasing bias. Which technique BEST meets this requirement?

A) Gradient Boosting with a learning rate of 0.3
B) AdaBoost with 500 sequential weak learners
C) Random Forest with bootstrap sampling and feature subsampling
D) A single deep decision tree with max_depth=None

<details>
<summary>Answer</summary>

**Correct: C**

Random Forest is a bagging method: it trains many high-variance trees in parallel on bootstrapped samples with random feature subsets, then averages predictions. Averaging independent, high-variance estimators reduces variance while bias stays roughly the same as a single tree.

**Why the others are wrong:**
- Gradient Boosting reduces bias by sequentially fitting residuals; it is more prone to increasing variance/overfitting if not tuned, not the primary fix here.
- AdaBoost is also a boosting method — it lowers bias by focusing on misclassified points, which can push variance up, the opposite of what's needed.
- A single unpruned deep tree is exactly what caused the overfitting (high variance) in the first place.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A regression model has 500 features, many of which are believed to be irrelevant. The team wants the model to automatically zero out the coefficients of unimportant features to produce a sparse, interpretable model. Which regularization approach BEST fits this requirement?

A) L2 (Ridge) regularization with alpha=1.0
B) Elastic Net with l1_ratio=0.0
C) L1 (Lasso) regularization
D) No regularization with early stopping

<details>
<summary>Answer</summary>

**Correct: C**

L1/Lasso adds the absolute value of coefficients (|w|) to the loss, which drives many coefficients exactly to zero, performing implicit feature selection and producing a sparse model.

**Why the others are wrong:**
- L2/Ridge penalizes squared coefficients (w²), shrinking weights toward zero but almost never to exactly zero — it does not produce sparsity.
- Elastic Net with l1_ratio=0.0 is mathematically equivalent to pure L2/Ridge, so it will not zero out coefficients.
- No regularization with early stopping controls overfitting on iterative training but does nothing to induce sparsity in coefficients.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A dataset shows classes that are not linearly separable in the original 2D feature space, but the boundary appears to be a smooth curved surface. Which SVM kernel should be selected FIRST to model this decision boundary?

A) Radial Basis Function (RBF) kernel
B) Linear kernel
C) Polynomial kernel of degree 1
D) Sigmoid kernel with default gamma

<details>
<summary>Answer</summary>

**Correct: A**

RBF (Gaussian) kernel maps data into an infinite-dimensional space and is the standard default choice for non-linear, smooth curved boundaries. It has two tunable parameters (C and gamma) that control the flexibility of the boundary.

**Why the others are wrong:**
- A linear kernel only produces a straight-line/hyperplane boundary and cannot fit curved separations.
- A degree-1 polynomial kernel is mathematically equivalent to a linear kernel — no added flexibility.
- The sigmoid kernel behaves like a neural network activation and is rarely the first/best choice for general non-linear boundaries; it can also fail to satisfy Mercer's condition for some parameter values.

</details>

---

**Q4.** Which ensemble mechanism trains base learners in parallel on independent bootstrap samples and combines predictions via averaging or majority vote?

A) Boosting
B) Stacking
C) Bagging
D) Blending

<details>
<summary>Answer</summary>

**Correct: C**

Bagging (Bootstrap Aggregating) trains multiple models independently and in parallel on bootstrapped subsets of data, then aggregates via averaging (regression) or voting (classification), primarily reducing variance.

**Why the others are wrong:**
- Boosting trains learners sequentially, each correcting the errors of the previous one — not parallel or independent.
- Stacking trains a meta-model on the out-of-fold predictions of diverse base models — it does not use bootstrap sampling of the same algorithm.
- Blending is similar to stacking but uses a held-out validation set instead of k-fold out-of-fold predictions — also not parallel bootstrap aggregation.

</details>

---

**Q5.** Which ensemble technique builds trees sequentially, where each new tree is trained to minimize the residual errors (gradient of the loss function) of the combined ensemble so far?

A) Random Forest
B) Gradient Boosting (e.g., XGBoost, LightGBM)
C) Bagged decision trees
D) K-Nearest Neighbors ensemble

<details>
<summary>Answer</summary>

**Correct: B**

Gradient Boosting fits each new weak learner to the negative gradient (residual error) of the loss function, sequentially improving the ensemble and primarily reducing bias.

**Why the others are wrong:**
- Random Forest builds trees independently and in parallel — no sequential residual correction.
- Bagged decision trees also train independently on bootstrap samples, not sequentially on residuals.
- KNN is a non-parametric distance-based method, not an ensemble of sequentially trained models.

</details>

---

**Q6.** A classification decision tree is being configured, and the team wants the split criterion computationally faster than entropy while producing similar splits in practice. Which impurity measure should be configured?

A) Mean Squared Error (MSE)
B) Log loss on the full tree
C) Gini impurity
D) Mean Absolute Error (MAE)

<details>
<summary>Answer</summary>

**Correct: C**

Gini impurity = 1 − Σ(pᵢ²) avoids the logarithm computation used in entropy = −Σ(pᵢ·log₂(pᵢ)), making it faster to compute per split while typically producing very similar tree structures.

**Why the others are wrong:**
- MSE is the standard splitting criterion for regression trees, not classification.
- Log loss is used to evaluate probabilistic classifier output overall, not as a per-node splitting criterion in standard CART trees.
- MAE is also a regression-tree criterion (more robust to outliers than MSE), not applicable to classification splits.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** In logistic regression, the inverse regularization strength parameter C is set very small (e.g., C=0.001). What is the expected effect on the model?

A) Regularization is strengthened, coefficients shrink toward zero, increasing bias
B) Regularization is weakened, increasing risk of overfitting
C) The decision boundary becomes purely non-linear
D) The model switches from L2 to L1 penalty automatically

<details>
<summary>Answer</summary>

**Correct: A**

In scikit-learn's logistic regression, C is the inverse of regularization strength (λ = 1/C). A small C means strong regularization, which shrinks coefficients toward zero, simplifying the model and increasing bias while reducing variance.

**Why the others are wrong:**
- This is backwards — small C means STRONGER, not weaker, regularization.
- Logistic regression with regularization still produces a linear decision boundary in the original feature space; regularization strength doesn't add non-linearity.
- The penalty type (L1 vs L2) is set independently via the 'penalty' parameter — changing C does not change the penalty type.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which of the following is NOT a standard assumption of ordinary least squares (OLS) linear regression?

A) Features must be normally distributed
B) Linearity between independent variables and the dependent variable
C) Homoscedasticity (constant variance of residuals)
D) Independence of errors

<details>
<summary>Answer</summary>

**Correct: A**

OLS assumptions are: linearity, independence of errors, homoscedasticity, and normality of the RESIDUALS (errors) — not the raw features themselves. Features are not required to be normally distributed.

**Why the others are wrong:**
- Linearity is a core OLS assumption — the relationship between X and y must be linear in the coefficients.
- Homoscedasticity is a core assumption — residual variance should be constant across all predicted values.
- Independence of errors is a core assumption — residuals should not be correlated with each other (e.g., no autocorrelation).

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

