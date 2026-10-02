# Ch12 Cheatsheet: Recommenders, Anomaly Detection & Applied ML

## Recommender Techniques
| Method | Data Needed | Cold-Start? | Notes |
|---|---|---|---|
| Collaborative Filtering (user/item-based) | User-item interactions | Fails on new users/items | Wisdom of the crowd |
| Content-Based Filtering | Item attributes/metadata | Handles new items OK | No cross-user signal |
| Matrix Factorization (SVD, ALS) | Sparse interaction matrix | Fails on new users/items | Latent factors, scalable via ALS |
| Hybrid (weighted/switching/feature combo) | Both | Best mitigation | Exam default answer for cold-start |

## Cold-Start Problem
- **New user**: no history → fallback to popularity/content-based/demographic recs.
- **New item**: no interactions → fallback to content-based (metadata) recs.
- **Standard fix**: hybrid system, switch strategy as data accumulates.

## Recommender Evaluation Metrics
| Metric | Formula | Use |
|---|---|---|
| Precision@k | relevant in top k / k | Relevance density |
| Recall@k | relevant in top k / total relevant | Coverage of relevant items |
| NDCG@k | DCG/IDCG; DCG = Σ rel_i / log2(i+1) | Rank-position-aware relevance |
| MAP | Mean of Average Precision across users | Overall ranking quality |

## Anomaly Detection Methods
| Method | Best For | Key Param/Concept |
|---|---|---|
| Statistical threshold (z-score, IQR) | Low-dim, single-feature | z-score cutoff ~3; IQR 1.5x rule |
| Isolation Forest | High-dim, no distribution assumption | `contamination` (default 'auto') |
| Autoencoder | High-dim, nonlinear patterns | Train on normal only; threshold = reconstruction error percentile |

## Extreme Imbalance — Evaluation
- Accuracy is misleading (majority-class baseline near 100%).
- Use: Precision-Recall AUC, F1/F-beta, recall at fixed precision, confusion matrix breakdown.

## Hybrid Recommender Strategies (Burke)
- **Weighted**: combine CF + content scores numerically.
- **Switching**: pick method based on context (e.g., cold-start → content-based).
- **Feature Combination**: merge signals into single model's feature set.

## Common Exam Traps
- Confusing precision@k with recall@k denominators.
- Assuming CF works for brand-new users/items (it doesn't — cold-start).
- Trusting accuracy on imbalanced anomaly datasets.
- Forgetting NDCG requires IDCG normalization for cross-user comparability.
