## Chapter 2: Feature Engineering and Selection Strategies — Practice Questions

**Q1.** A dataset contains a 'zip_code' feature with 15,000 unique values used to predict loan default. Which encoding approach is BEST for a gradient boosting model?

A) One-hot encoding of all 15,000 categories
B) Target encoding with out-of-fold (K-fold) computation and smoothing toward the global mean
C) Ordinal encoding based on alphabetical order of zip codes
D) Drop the feature entirely to avoid dimensionality issues

<details>
<summary>Answer</summary>

**Correct: B**

Out-of-fold target encoding compresses high-cardinality categories into a single informative numeric feature while preventing target leakage through cross-fold computation and smoothing.

**Why the others are wrong:**
- One-hot at 15,000 categories creates an extremely sparse, high-dimensional matrix that hurts tree-based model performance and training time.
- Alphabetical ordinal encoding imposes a false numeric ordering with no relationship to default risk.
- Dropping the feature discards potentially predictive geographic signal unnecessarily.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A team has 500 features and needs a selection method that accounts for interactions relevant to their chosen model while keeping compute cost manageable. Which method fits BEST?

A) Filter method using chi-squared test
B) Wrapper method using exhaustive forward selection
C) Manual removal based on a correlation matrix
D) Embedded method using Lasso (L1) regularization

<details>
<summary>Answer</summary>

**Correct: D**

Embedded methods like Lasso perform selection as part of a single model training pass, capturing feature relevance to the model at a fraction of the cost of exhaustive search.

**Why the others are wrong:**
- Chi-squared is model-agnostic and evaluates features independently, missing interactions.
- Exhaustive forward selection over 500 features requires training an infeasible number of model subsets.
- Correlation matrix removal only addresses pairwise linear redundancy, not model-specific relevance.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** Which scenario calls for min-max normalization instead of standardization?

A) Linear regression assuming Gaussian-distributed residuals with outliers present
B) PCA where preserving variance structure across features matters
C) K-means clustering with Euclidean distance on non-Gaussian, unbounded data
D) A neural network layer using a sigmoid activation that requires inputs in a fixed [0,1] range

<details>
<summary>Answer</summary>

**Correct: D**

Bounded activation functions expect inputs constrained to a specific range, making min-max normalization the correct choice.

**Why the others are wrong:**
- Linear regression with outliers is better served by standardization, which is less distorted by scale than min-max bounding.
- PCA relies on variance comparability across features, which standardization provides directly.
- K-means with unbounded, non-Gaussian data typically uses standardization to equalize feature influence on distance.

</details>

---

**Q4.** A categorical feature 'education_level' has a natural order: High School < Bachelors < Masters < PhD. Which encoding preserves this relationship without inflating dimensionality?

A) One-hot encoding
B) Target encoding
C) Ordinal encoding with an explicitly defined order mapping
D) Frequency encoding

<details>
<summary>Answer</summary>

**Correct: C**

Ordinal encoding directly represents genuine rank order as a single numeric feature, matching the underlying data structure.

**Why the others are wrong:**
- One-hot discards the ordinal relationship and adds unnecessary dimensions.
- Target encoding introduces target-dependent values unrelated to the natural ordering.
- Frequency encoding reflects category prevalence, not the ordinal relationship.

</details>

---

**Q5.** You need a feature selection method for a categorical target and categorical features that tests statistical independence, is fast, and is model-agnostic. Which method fits?

A) Recursive Feature Elimination (wrapper method)
B) Lasso regression (embedded method)
C) Chi-squared test (filter method)
D) Tree-based feature importance (embedded method)

<details>
<summary>Answer</summary>

**Correct: C**

Chi-squared is a classic filter method that tests independence between categorical variables and the target without training any predictive model.

**Why the others are wrong:**
- RFE requires repeatedly training a model, making it slower and model-dependent.
- Lasso is a regression-based embedded method requiring numeric coefficients and model fitting.
- Tree-based importance requires training a tree ensemble model first.

</details>

---

**Q6.** Given features [A, B], what does sklearn's PolynomialFeatures(degree=2, interaction_only=True) produce?

A) A, B, A², B², AB
B) A², B² only
C) A, B, AB (no squared terms)
D) AB only

<details>
<summary>Answer</summary>

**Correct: C**

interaction_only=True excludes same-feature power terms (A², B²) and retains only original features plus cross-feature interaction products.

**Why the others are wrong:**
- This includes squared terms, which interaction_only explicitly removes.
- This omits the original single features, which are still included by default.
- This omits the original features A and B, which remain in the output.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** Before applying sklearn's chi2 filter method for feature selection, which preprocessing step is REQUIRED?

A) Standardize all features to zero mean and unit variance
B) Apply PCA to remove correlated features first
C) Ensure all feature values are non-negative
D) Convert all continuous features into categorical bins

<details>
<summary>Answer</summary>

**Correct: C**

chi2 is a frequency-based statistical test that requires non-negative input values; negative values will raise an error.

**Why the others are wrong:**
- Standardization produces negative values, which is incompatible with chi2's requirement.
- PCA is unrelated to chi2's input constraints and changes feature interpretability.
- Discretization is not required — chi2 works with non-negative continuous or count-based features directly.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the key structural difference between wrapper and embedded feature selection methods?

A) Wrapper methods evaluate feature subsets by repeatedly training and scoring a model in an external loop; embedded methods perform selection as part of the model's own training process
B) Wrapper methods use statistical tests independent of any model; embedded methods always require deep learning models
C) Wrapper methods are always faster than embedded methods due to single-pass evaluation
D) Embedded methods cannot use tree-based models, only linear models

<details>
<summary>Answer</summary>

**Correct: A**

Wrapper methods (e.g., RFE) iteratively train and score models on feature subsets, while embedded methods (e.g., Lasso, tree importance) integrate selection directly into a single training process.

**Why the others are wrong:**
- This describes filter methods, not wrapper methods.
- Wrapper methods are typically slower due to repeated model training, not faster.
- Embedded methods commonly use tree-based models (e.g., Gini importance) as well as linear models.

</details>

---

