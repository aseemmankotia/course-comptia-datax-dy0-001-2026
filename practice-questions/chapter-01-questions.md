## Chapter 1: Exploratory Data Analysis and Data Quality Triage — Practice Questions

**Q1.** A survey of household income shows that respondents earning above $200k are far less likely to report their income than lower earners, even after controlling for age, education, and region. Which missing data mechanism best describes this pattern, and what is the BEST way to handle it?

A) MCAR — drop all rows with missing income using listwise deletion
B) MAR — impute using mean income conditioned on age and education only
C) MAR — apply SMOTE to the income column to balance the distribution
D) MNAR — the missingness depends on the unobserved income value itself, so use a missingness indicator plus a selection/sensitivity model rather than standard imputation

<details>
<summary>Answer</summary>

**Correct: D**

The probability of a value being missing depends on the value itself (higher earners hide their own income), which is the definition of MNAR. Standard imputation assumes the missingness can be explained by observed variables, which is false here — a missingness indicator and sensitivity/selection modeling is the recommended remedy.

**Why the others are wrong:**
- MCAR requires missingness to be unrelated to any variable, observed or not — here it clearly correlates with income level, so listwise deletion would bias estimates.
- This describes MAR, but MAR requires missingness to depend only on OBSERVED variables (age, education) — here it depends on the unobserved income value itself, making it MNAR, not MAR.
- SMOTE generates synthetic minority-class samples for classification imbalance; it is not a missing-data imputation technique and does not address MNAR mechanisms.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A data scientist builds a churn prediction model using a feature called 'days_since_last_support_ticket_before_cancellation'. The model achieves 98% accuracy in testing but performs poorly in production. What is the MOST likely cause?

A) Class imbalance in the training set was not corrected
B) The features have high multicollinearity causing overfitting
C) Target leakage — the feature is only computable after the cancellation event has already occurred
D) The model needs a log transform on the numeric features

<details>
<summary>Answer</summary>

**Correct: C**

The feature name explicitly references 'before_cancellation', meaning it can only exist after the churn outcome is known. This is classic target leakage — the feature encodes future/outcome information unavailable at prediction time, inflating test metrics artificially.

**Why the others are wrong:**
- Class imbalance would typically hurt accuracy on the minority class, not produce artificially inflated 98% accuracy that collapses only in production.
- Multicollinearity affects coefficient stability and interpretability but does not by itself explain a large train/test-to-production performance gap tied to a suspiciously outcome-correlated feature.
- Skewness affects distributional assumptions of some models but would not explain the specific train-production gap caused by an outcome-derived feature.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A binary fraud classifier is trained on a dataset with 0.4% positive class prevalence. The team wants to improve recall on fraud cases without discarding legitimate transaction data or introducing synthetic duplicate transactions that could mislead auditors. Which approach BEST meets these constraints?

A) Randomly undersample the majority class to a 50/50 ratio
B) Keep the full dataset and set class_weight='balanced' (or equivalent cost-sensitive weighting) in the classifier
C) Apply SMOTE to oversample the minority class to a 50/50 ratio
D) Delete all majority-class rows older than 6 months to rebalance the classes

<details>
<summary>Answer</summary>

**Correct: B**

Class weighting penalizes misclassification of the minority class more heavily during training without discarding any legitimate data or generating synthetic samples, satisfying both stated constraints (no data loss, no synthetic duplicates).

**Why the others are wrong:**
- Undersampling discards majority-class rows, which violates the 'without discarding data' constraint and can throw away useful information.
- SMOTE creates synthetic minority-class transactions, which violates the constraint about not introducing synthetic duplicates that could mislead auditors.
- Deleting rows by age is an arbitrary data-loss strategy unrelated to proper class balancing and discards potentially relevant legitimate transaction data.

</details>

---

**Q4.** A dataset has 15 correlated numeric features with clusters of points that form irregular, non-linear boundaries around the bulk of the data. Which outlier detection method is BEST suited to this scenario?

A) Univariate z-score thresholding on each feature independently
B) IQR method applied column by column
C) Manually set fixed thresholds per feature based on domain knowledge
D) Isolation Forest

<details>
<summary>Answer</summary>

**Correct: D**

Isolation Forest isolates anomalies based on how few splits are needed to separate a point across all features simultaneously, making it effective for multivariate, non-linear, correlated outlier structures that univariate methods miss.

**Why the others are wrong:**
- Z-score is univariate and assumes roughly normal distributions per feature; it cannot detect outliers defined by unusual combinations across correlated features.
- IQR is also univariate and column-by-column, missing multivariate anomalies where each individual feature value looks normal in isolation.
- Manual thresholds do not scale to 15 correlated dimensions and cannot capture non-linear joint relationships between features.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A revenue column is strictly positive and strongly right-skewed, and the team plans to feed it into a linear regression model that assumes roughly normal residuals. Which transform is the BEST first choice?

A) Min-max scaling to [0,1]
B) One-hot encoding the revenue bins
C) Z-score standardization only, with no transform
D) Log transform (e.g., log(x) or log(x+1))

<details>
<summary>Answer</summary>

**Correct: D**

Log transforms compress large values and expand small ones, reducing right skew in strictly positive data and helping satisfy linear regression's normality/homoscedasticity assumptions.

**Why the others are wrong:**
- Min-max scaling rescales the range but preserves the original skewed shape of the distribution.
- One-hot encoding is for categorical variables, not continuous skewed numeric data, and would discard magnitude information.
- Standardization centers and scales the data but does not change its underlying skewed shape.

</details>

---

**Q6.** In the standard IQR outlier detection rule, a value is flagged as an outlier if it falls below Q1 − k×IQR or above Q3 + k×IQR. What is the conventional default value of k used for standard (non-extreme) outlier detection?

A) 1.5
B) 1.0
C) 2.5
D) 3.0

<details>
<summary>Answer</summary>

**Correct: A**

1.5×IQR is the widely used Tukey convention for standard outliers; the exam distinguishes this from k=3.0, which is commonly used to flag 'extreme' outliers.

**Why the others are wrong:**
- k=1.0 is too aggressive and is not the conventional threshold taught for standard outlier detection.
- 2.5 is not a standard textbook convention for IQR outlier detection.
- 3.0 is the conventional threshold for EXTREME outliers, not standard outliers — a common exam trap swapping the two values.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A team fits a StandardScaler and a missing-value imputer on the ENTIRE dataset (train + test combined) before splitting into train and test sets, then trains and evaluates the model. What data quality problem does this introduce?

A) Class imbalance
B) MNAR missing data
C) Multicollinearity
D) Train-test contamination (information leakage from test set into training)

<details>
<summary>Answer</summary>

**Correct: D**

Fitting scalers or imputers on the full dataset before splitting lets statistics from the test set (means, std devs, imputed values) leak into training, inflating validation performance — this is train-test contamination, a specific data leakage subtype. The correct pattern is to split first, then fit preprocessing only on the training fold.

**Why the others are wrong:**
- Class imbalance refers to unequal class proportions, unrelated to when preprocessing is fitted relative to the split.
- MNAR is a missing-data mechanism describing WHY data is missing, not a leakage issue caused by preprocessing order.
- Multicollinearity is a relationship between features themselves and is unaffected by whether scaling was fit before or after splitting.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Ice cream sales and drowning deaths are strongly positively correlated across months. Which explanation correctly identifies why this correlation does NOT imply causation?

A) The sample size is too small to draw any conclusion
B) The correlation coefficient must be miscalculated
C) Correlation only applies to categorical variables, not continuous ones
D) A confounding variable (warm weather) independently increases both ice cream sales and swimming activity, driving the correlation

<details>
<summary>Answer</summary>

**Correct: D**

Warm weather is a confounding variable that increases both ice cream consumption and swimming (and thus drowning risk), producing a spurious correlation between the two without either causing the other.

**Why the others are wrong:**
- Sample size affects statistical confidence but is not the reason a real correlation could be non-causal; the classic explanation is confounding.
- The correlation coefficient can be entirely correctly calculated and still not imply causation — miscalculation is not the issue being tested.
- Correlation coefficients like Pearson's r are explicitly designed for continuous variables; this statement is factually incorrect.

</details>

---

