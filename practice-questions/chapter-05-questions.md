## Chapter 5: Unsupervised Learning: Clustering and Dimensionality Reduction — Practice Questions

**Q1.** A retail company clusters customers based on purchase amount and visit frequency. The scatter plot shows clusters that are elongated and non-spherical, with clusters of very different sizes. Applying k-means produces poor groupings where points near cluster boundaries are misassigned. Which algorithm BEST addresses this limitation?

A) K-means with a higher value of k
B) K-means with standardized features only
C) DBSCAN with tuned eps and min_samples
D) Hierarchical clustering with single linkage

<details>
<summary>Answer</summary>

**Correct: C**

DBSCAN is density-based and makes no assumption of spherical, equal-variance clusters, so it correctly handles elongated, arbitrarily shaped clusters and naturally separates them from noise.

**Why the others are wrong:**
- Increasing k does not fix k-means' core assumption problem — it still forces spherical, equal-variance partitions.
- Standardizing features helps with scale but does not remove k-means' spherical-cluster assumption; the shape problem remains.
- Single linkage hierarchical clustering is prone to 'chaining' and produces unstable results on noisy, unevenly sized data — it is not the best fit here.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A data science team builds a 2D visualization of user embeddings using t-SNE for an internal dashboard. Next month, new users must be projected onto the same visualization without retraining on the full dataset. Which technique should replace t-SNE to satisfy this requirement?

A) UMAP, because it supports transforming new data points via a learned mapping
B) PCA, because it preserves the most global variance
C) t-SNE with a fixed random seed for reproducibility
D) Hierarchical clustering to assign new points to existing branches

<details>
<summary>Answer</summary>

**Correct: A**

UMAP learns a reusable embedding function (via .transform()), so new points can be projected without recomputing the entire embedding — t-SNE has no native out-of-sample transform.

**Why the others are wrong:**
- PCA can transform new data, but it is linear and preserves global variance rather than local neighborhood structure, which is why t-SNE-style visualization was chosen in the first place.
- A fixed seed only makes t-SNE reproducible for the same run; it still cannot project new points onto an existing embedding without recomputation.
- Hierarchical clustering assigns cluster labels, not 2D coordinates, and does not provide a transform for unseen points.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A dataset has 500 numeric features and only 8,000 samples. K-means clustering produces near-random assignments because pairwise distances between points become nearly indistinguishable. This is a direct symptom of which phenomenon, and what is the standard mitigation?

A) Curse of dimensionality; apply PCA to reduce dimensions before clustering
B) Overfitting; apply cross-validation before clustering
C) Class imbalance; apply oversampling before clustering
D) Multicollinearity; apply one-hot encoding before clustering

<details>
<summary>Answer</summary>

**Correct: A**

In high-dimensional spaces, Euclidean distances between points converge, making distance-based algorithms like k-means ineffective — this is the curse of dimensionality. Reducing dimensions with PCA before clustering restores meaningful distance structure.

**Why the others are wrong:**
- Cross-validation is a supervised-learning technique for model evaluation; it does not address distance degradation in unsupervised clustering.
- Class imbalance applies to labeled classification problems, not unsupervised clustering with numeric features.
- One-hot encoding is for categorical variables and would increase, not reduce, dimensionality, worsening the problem.

</details>

---

**Q4.** Which clustering algorithm requires the number of clusters to be specified in advance AND assumes clusters are spherical with roughly equal variance?

A) K-means
B) DBSCAN
C) Agglomerative hierarchical clustering
D) OPTICS

<details>
<summary>Answer</summary>

**Correct: A**

K-means requires k to be chosen beforehand and minimizes within-cluster variance under the assumption that clusters are spherical (isotropic) and of similar size.

**Why the others are wrong:**
- DBSCAN does not require specifying the number of clusters; it derives clusters from density parameters eps and min_samples.
- Agglomerative hierarchical clustering builds a dendrogram and the number of clusters is chosen afterward by cutting the tree, not specified upfront.
- OPTICS, like DBSCAN, is density-based and does not assume spherical clusters or require k in advance.

</details>

---

**Q5.** A dataset contains clusters of arbitrary shape (crescents, spirals) along with scattered outlier points that should not be forced into any cluster. Which algorithm is BEST suited for this scenario?

A) K-means with k selected via the elbow method
B) Hierarchical clustering with complete linkage
C) DBSCAN, which labels outliers as noise
D) PCA followed by k-means on the top 2 components

<details>
<summary>Answer</summary>

**Correct: C**

DBSCAN naturally handles arbitrary-shaped clusters based on density and explicitly labels low-density points as noise (-1), rather than forcing every point into a cluster.

**Why the others are wrong:**
- K-means always assigns every point to a cluster and assumes convex, spherical shapes, so it fails on crescents/spirals and cannot isolate true outliers.
- Complete linkage hierarchical clustering tends to produce compact, roughly spherical clusters and has no built-in mechanism to flag noise points.
- Reducing to 2D with PCA does not change k-means' spherical-cluster assumption or its inability to designate noise points.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A silhouette score is computed for a k-means clustering result and returns a value of 0.85. What does this indicate?

A) Clusters are poorly separated and overlapping heavily
B) Points are well-matched to their own cluster and poorly matched to neighboring clusters, indicating strong clustering structure
C) The chosen k is too high and should be reduced immediately
D) The dataset is not suitable for clustering and should be discarded

<details>
<summary>Answer</summary>

**Correct: B**

Silhouette score ranges from -1 to 1; values close to 1 mean each point is much closer to points in its own cluster (cohesion) than to points in the nearest other cluster (separation) — indicating strong, well-separated clusters.

**Why the others are wrong:**
- A score near -1, not 0.85, indicates poor separation or overlapping clusters.
- A high silhouette score is evidence the current k is a good fit, not a signal that k is too high — no action is implied here.
- A high score means the data DOES have meaningful clustering structure, the opposite of being unsuitable for clustering.

</details>

---

**Q7.** To select the optimal number of clusters k for a k-means model using the elbow method, which value should be plotted against k on the y-axis?

A) The silhouette score for each k
B) The number of iterations until convergence
C) The within-cluster sum of squares (WCSS / inertia)
D) The eps parameter value

<details>
<summary>Answer</summary>

**Correct: C**

The elbow method plots WCSS (inertia) against k; the optimal k is where the marginal decrease in WCSS sharply diminishes, forming a visible 'elbow' in the curve.

**Why the others are wrong:**
- Silhouette score is a separate, complementary validity metric with its own plot (score vs. k) — it is not what defines the elbow method.
- Iterations to convergence is an implementation detail of Lloyd's algorithm, unrelated to choosing k.
- Eps is a DBSCAN hyperparameter, not part of k-means or the elbow method.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** As the number of dimensions in a dataset increases, what happens to Euclidean distances between data points, and why does this matter for clustering?

A) Distances between nearest and farthest neighbors converge, making distance-based similarity less meaningful
B) Distances shrink toward zero uniformly, making all points identical
C) Distances increase without bound, making clusters more distinct
D) Distances remain unaffected because Euclidean distance is scale-invariant

<details>
<summary>Answer</summary>

**Correct: A**

This is the curse of dimensionality: in high-dimensional space, the ratio between the distance to the nearest and farthest point approaches 1, so distance-based methods like k-means and k-NN lose discriminative power.

**Why the others are wrong:**
- Distances don't converge to zero — they typically grow in magnitude, but the relative difference between near and far points shrinks, not the absolute values.
- Increasing dimensionality degrades cluster separability in distance terms; it does not make clusters more distinct.
- Euclidean distance is not scale-invariant, and dimensionality directly affects its discriminative usefulness, contradicting this option.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

