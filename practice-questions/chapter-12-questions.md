## Chapter 12: Recommender Systems, Anomaly Detection, and Other Applied Techniques — Practice Questions

**Q1.** A streaming platform onboards a brand-new user who has zero watch history and has filled out no profile preferences. The recommendation engine must still return a reasonably relevant top-10 list on day one. Which approach BEST addresses this cold-start scenario?

A) Use pure collaborative filtering based on similar users' rating vectors
B) Fall back to content-based or popularity-based recommendations until enough interaction data accumulates, then blend in collaborative filtering
C) Wait to serve any recommendations until the user has rated at least 20 items
D) Apply matrix factorization with randomly initialized latent factors for the new user

<details>
<summary>Answer</summary>

**Correct: B**

Content-based/popularity fallback requires no interaction history and is the standard hybrid mitigation for the new-user cold-start problem; the system transitions to collaborative signals as data accumulates.

**Why the others are wrong:**
- Pure collaborative filtering has no user vector to compare against — it cannot function for a user with zero interactions.
- Delaying recommendations for 20 ratings destroys user experience and isn't a real production strategy the exam endorses.
- Randomly initialized latent factors produce noise, not meaningful recommendations, since they haven't been trained against any signal for this user.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A credit card fraud detection dataset contains 500,000 transactions with only 250 labeled as fraud (0.05% positive rate). A model reports 99.9% accuracy. Which evaluation approach reveals whether the model is actually useful?

A) Trust the 99.9% accuracy since it exceeds typical model benchmarks
B) Report a confusion matrix but stop there since accuracy already confirms performance
C) Use precision-recall AUC and examine recall at a fixed precision threshold, since accuracy is dominated by the majority class
D) Increase the training set size until accuracy reaches 99.99%

<details>
<summary>Answer</summary>

**Correct: C**

With extreme class imbalance, a naive model predicting 'not fraud' for everything already achieves ~99.95% accuracy, so accuracy is meaningless. Precision-recall AUC and recall-at-precision are the exam-tested metrics for this scenario.

**Why the others are wrong:**
- 99.9% accuracy is trivially achievable by predicting the majority class and says nothing about fraud detection capability.
- A confusion matrix alone doesn't quantify tradeoffs across thresholds — PR curves are needed to select an operating point.
- Increasing accuracy target further reinforces the same flawed metric and doesn't address the imbalance problem.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A recommender returns a top-5 list for a user. Of those 5 items, 3 are ones the user later actually engaged with (relevant). What is precision@5?

A) 0.3
B) 0.5
C) 0.6
D) 1.0

<details>
<summary>Answer</summary>

**Correct: C**

Precision@k = (relevant items in top k) / k = 3/5 = 0.6.

**Why the others are wrong:**
- 0.3 would be 3 divided by 10, not the correct denominator for precision@5.
- 0.5 miscounts as 2.5/5 or confuses with a different k value.
- 1.0 would only be correct if all 5 returned items were relevant.

</details>

---

**Q4.** A team needs to build collaborative filtering recommendations across 50 million users and 2 million items using implicit feedback (clicks, not explicit ratings), and the solution must scale via distributed computing. Which technique BEST fits this requirement?

A) Memory-based user-user collaborative filtering computing full pairwise cosine similarity
B) Alternating Least Squares (ALS) matrix factorization distributed across a Spark cluster
C) K-nearest neighbors on raw item feature vectors
D) A single-node full SVD decomposition of the complete user-item matrix

<details>
<summary>Answer</summary>

**Correct: B**

ALS is designed for implicit feedback, decomposes efficiently in a distributed manner (e.g., Spark MLlib), and scales to tens of millions of users/items — the standard exam answer for large-scale implicit CF.

**Why the others are wrong:**
- Pairwise user-user similarity at 50M users is computationally infeasible (O(n²)) and doesn't scale.
- KNN on raw item features is content-based, not collaborative filtering, and doesn't leverage the interaction matrix.
- Single-node full SVD cannot handle a 50M x 2M sparse matrix in memory and isn't distributed.

</details>

---

**Q5.** A team must detect anomalies in a high-dimensional sensor dataset (200+ features) where anomalies don't follow a known distribution and labeled anomaly examples are extremely scarce. Which method is BEST suited?

A) A simple z-score threshold applied independently to each feature
B) A logistic regression classifier trained on the few labeled anomalies
C) IQR-based outlier detection on the raw feature set
D) Isolation Forest, since it isolates anomalies via random recursive partitioning without assuming a data distribution

<details>
<summary>Answer</summary>

**Correct: D**

Isolation Forest scales well to high-dimensional data, makes no distributional assumptions, and is explicitly built for unsupervised/semi-supervised anomaly detection — the exam's default answer for this scenario.

**Why the others are wrong:**
- Per-feature z-score ignores feature interactions and breaks down in high dimensions (curse of dimensionality).
- Logistic regression trained on a handful of labeled anomalies will severely overfit and generalize poorly.
- IQR thresholds are univariate and, like z-score, don't capture multivariate anomaly patterns in 200+ dimensions.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** When computing NDCG@k for a ranked recommendation list, what does the denominator (IDCG) represent?

A) The total number of items in the catalog
B) The DCG score of the ideal ranking, where the most relevant items are placed at the top
C) The average precision across all users
D) The number of relevant items divided by k

<details>
<summary>Answer</summary>

**Correct: B**

IDCG (Ideal DCG) is the DCG computed for the best possible ordering of relevant items, used to normalize DCG into NDCG (0 to 1 scale) so scores are comparable across queries/users.

**Why the others are wrong:**
- Catalog size is unrelated to NDCG's normalization; NDCG only concerns the ranked list and relevance labels.
- Average precision is a separate metric (MAP), not the normalization term for NDCG.
- Relevant items divided by k describes recall@k, not IDCG.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** In scikit-learn's IsolationForest, what does the `contamination` parameter control?

A) The number of trees in the ensemble
B) The expected proportion of outliers in the dataset, used to set the decision threshold
C) The maximum depth of each isolation tree
D) The percentage of features randomly sampled per split

<details>
<summary>Answer</summary>

**Correct: B**

`contamination` sets the expected fraction of anomalies, which determines the threshold on the anomaly score used to label points as outliers; default is 'auto'.

**Why the others are wrong:**
- Number of trees is controlled by `n_estimators`, a separate parameter.
- Max depth is influenced by `max_samples`/tree structure, not `contamination`.
- Feature sampling per split is controlled by `max_features`, not `contamination`.

</details>

---

**Q8.** What is the fundamental difference between content-based filtering and collaborative filtering in recommender systems?

A) Content-based filtering recommends items similar to a user's past preferences using item attributes; collaborative filtering recommends items based on patterns across many users' interactions
B) Content-based filtering requires GPU acceleration while collaborative filtering does not
C) Collaborative filtering only works for text data, while content-based filtering only works for images
D) Content-based filtering is always more accurate than collaborative filtering

<details>
<summary>Answer</summary>

**Correct: A**

This is the core conceptual distinction tested: content-based uses item feature similarity to a user's profile, while collaborative filtering uses the wisdom-of-crowds signal from the user-item interaction matrix.

**Why the others are wrong:**
- Neither method has an inherent GPU requirement; this is a fabricated distinction.
- Both techniques are data-type agnostic and can apply to text, images, or any item metadata/interactions.
- Neither approach is universally 'more accurate' — performance depends on data availability (cold-start favors content-based, rich interaction history favors collaborative).

</details>

---

