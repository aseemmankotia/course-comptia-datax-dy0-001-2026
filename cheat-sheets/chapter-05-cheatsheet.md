# Chapter 5 Cheat Sheet — Unsupervised Learning

## Clustering Algorithm Comparison
| Algorithm | Needs k? | Cluster Shape | Handles Noise? | Key Params |
|---|---|---|---|---|
| K-means | Yes | Spherical, equal variance | No | k, init (k-means++) |
| Agglomerative Hierarchical | No (cut dendrogram) | Depends on linkage | No | linkage (single/complete/average/ward) |
| DBSCAN | No | Arbitrary | Yes (-1 label) | eps, min_samples |

**Exam note:** K-means fails on elongated/unequal-density clusters — recognize this scenario pattern instantly.
**Common mistake:** Choosing k-means for arbitrary-shaped data because it's 'the default' clustering algorithm.

## Dimensionality Reduction Comparison
| Method | Linear? | Preserves | New-Data Transform? | Typical Use |
|---|---|---|---|---|
| PCA | Yes | Global variance | Yes | Preprocessing, compression, noise reduction |
| t-SNE | No | Local neighborhoods only | No | One-off 2D/3D visualization |
| UMAP | No | Local + more global structure than t-SNE | Yes | Visualization + reusable embeddings for new data |

**Exam note:** t-SNE cluster sizes/inter-cluster distances are NOT meaningful — never interpret them literally.
**Common mistake:** Using t-SNE output as features for a downstream classifier (no transform for new data = broken pipeline).

## Cluster Validity Metrics
- **Silhouette score**: range -1 to 1; formula (b-a)/max(a,b); closer to 1 = well-separated, well-cohesive clusters.
- **Elbow method**: plot WCSS (inertia) vs. k; pick k at the point of diminishing returns.
- **Exam trap**: A high silhouette score for k=2 doesn't mean 2 is 'correct' — always sanity-check against domain knowledge.

## Curse of Dimensionality
- As dimensions ↑, distance between nearest and farthest neighbor ratio → 1 (distances become meaningless).
- Distance-based methods (k-means, k-NN, DBSCAN) degrade in high-dimensional space.
- **Fix**: Apply PCA (or other reduction) before distance-based clustering when features are numerous.

## Quick Decision Rules
- Non-spherical clusters + noise present → **DBSCAN**
- Need dendrogram / unknown k / hierarchical relationships → **Agglomerative**
- Need fast, scalable, spherical clusters, k known → **K-means**
- Need variance-preserving linear reduction with reusable transform → **PCA**
- Need best 2D visualization of local structure, one-time plot → **t-SNE**
- Need visualization AND ability to embed new points later → **UMAP**

**Exam note:** Always standardize/scale features before k-means or PCA — scale-sensitive algorithms are heavily tested via scenario questions with mismatched units (e.g., income in dollars vs. age in years).
