## Chapter 5: Unsupervised Learning: Clustering and Dimensionality Reduction — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | K-means core assumptions (2) | Clusters are spherical (isotropic) and roughly equal variance/size. Exam tip: if clusters are elongated or unequal density, k-means fails — pick DBSCAN or GMM instead. |
| 2 | DBSCAN key hyperparameters | eps (neighborhood radius) and min_samples (minimum points to form a dense region). Points not reachable within these are labeled -1 (noise). |
| 3 | Silhouette score range and formula | Range: -1 to 1. Formula per point: (b - a) / max(a, b), where a = mean intra-cluster distance, b = mean nearest-cluster distance. Closer to 1 = well-clustered. |
| 4 | Elbow method — what's plotted? | WCSS (within-cluster sum of squares / inertia) on y-axis vs. k on x-axis. Optimal k is at the 'elbow' where the rate of decrease sharply flattens. |
| 5 | PCA vs t-SNE — structure preserved | PCA: linear, preserves global variance/structure, deterministic, has transform() for new data. t-SNE: nonlinear, preserves local neighborhoods only, stochastic, no transform() for new data. |
| 6 | t-SNE vs UMAP — new data handling | t-SNE has no native way to embed new points without recomputation. UMAP learns a reusable mapping and supports .transform() on unseen data. Exam tip: choose UMAP when new data must be projected later. |
| 7 | t-SNE key hyperparameter | Perplexity (typically 5–50). Controls balance between local and global structure; exam gotcha — too low overfits noise, too high blurs cluster separation. |
| 8 | Hierarchical clustering linkage methods (4) | Single (min distance, prone to chaining), Complete (max distance, compact clusters), Average (mean distance), Ward (minimizes variance increase). Exam tip: Ward is default-safe for roughly spherical clusters. |
| 9 | Curse of dimensionality — clustering symptom | As dimensions increase, distances between nearest and farthest points converge, making distance-based clustering (k-means, k-NN) unreliable. Fix: apply PCA/dimensionality reduction first. |
| 10 | When to use PCA vs t-SNE/UMAP | PCA: preprocessing/compression before modeling, need interpretable variance-preserving axes, need transform for new data. t-SNE/UMAP: exploratory 2D/3D visualization of cluster structure, not for feeding into downstream models. |
| 11 | DBSCAN output label for outliers | -1 (noise). Exam trap: unlike k-means, DBSCAN does NOT force every point into a cluster. |
| 12 | K-means initialization method to avoid poor local minima | k-means++ — smartly spreads initial centroids based on distance, reducing risk of poor convergence vs. random initialization. |
