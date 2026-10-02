# Answer Key — Practice Test 2

**Q1. Correct: A**

The feature is derived from events occurring after the churn outcome has already occurred, meaning it cannot exist at the time a real prediction must be made. This creates artificially inflated test performance that collapses once the feature is unavailable (or meaningless) in production.

---

**Q2. Correct: D**

With extreme class imbalance and a ranking-based business use case, PR-AUC focuses on performance for the minority (fraud) class and is not inflated by the large number of true negatives, making it the most informative metric for comparing model quality on rare-event ranking tasks.

---

**Q3. Correct: A**

Because the probability of missingness is driven directly by the (unobserved) income value itself rather than by any observed variable, this is MNAR. Standard imputation methods assume MAR and will be biased; approaches like selection models or pattern-mixture models are needed to explicitly account for the missingness mechanism.

---

**Q4. Correct: B**

Because the costs of false negatives and false positives are explicitly asymmetric and quantified, the threshold should be chosen to minimize total expected business cost using those weights directly, rather than a metric that implicitly assumes equal error costs.

---

**Q5. Correct: D**

Wrapper methods (e.g., recursive feature elimination) select features by repeatedly training and evaluating a specific model, which is expensive but captures interactions between features; filter methods (e.g., correlation, chi-square, mutual information) score features independently of any model, making them fast but potentially blind to feature interactions.

---

**Q6. Correct: B**

SHAP values provide a local, instance-level explanation, attributing the contribution of each feature to one specific prediction, which is exactly what is needed to explain an individual applicant's adverse decision as regulations often require.

---

**Q7. Correct: D**

Aggregating post-event transactions into a feature leaks future/outcome-adjacent information into the training data. This is a classic temporal leakage pattern: the feature is only 'known' after the event it is trying to predict has already occurred, which artificially inflates offline performance and will collapse in production. The fix is to enforce a point-in-time feature computation (only using data available before the reference/churn date).

---

**Q8. Correct: D**

With severe imbalance, ROC-AUC can remain high even when precision for the minority class is poor, because the false positive rate is computed against a huge number of negatives and stays low in relative terms. PR-AUC (precision-recall AUC) or a cost-sensitive F-beta score focuses directly on performance for the rare positive class and better reflects real-world alert quality, which is what stakeholders actually experienced as a problem.

---

**Q9. Correct: A**

A VIF above the common threshold of 10 indicates severe multicollinearity, which causes unstable, high-variance coefficient estimates even when overall fit (R²) looks fine — exactly the symptom described (sign flipping). The standard remedy is to remove one of the redundant predictors or combine them into a single engineered feature, restoring interpretability and coefficient stability.

---

**Q10. Correct: B**

Near-zero training error with a large and widening gap to validation error is the textbook signature of high variance (overfitting). The correct remedies are to increase regularization (shallower trees, higher min_child_weight, subsampling/column sampling) and/or add more training data, both of which directly reduce variance without requiring a change of model family.

---

**Q11. Correct: A**

AUC measures ranking/discrimination ability, not the accuracy of the predicted probability values themselves. When probabilities are used directly for business decisions like pricing, they must be well-calibrated. Platt scaling (logistic calibration) or isotonic regression are standard post-hoc techniques to correct miscalibrated probability outputs while preserving the model's ranking performance.

---

**Q12. Correct: C**

When the number of features vastly exceeds the number of samples, the data is already likely to be linearly separable in the high-dimensional space, so a linear kernel provides sufficient capacity without adding unnecessary nonlinear complexity, reducing overfitting and avoiding costly kernel matrix computations.

---

**Q13. Correct: C**

Larger k averages predictions over more neighbors, smoothing the decision boundary. This smoothing increases bias (the model becomes less flexible and can miss local patterns) while reducing variance (predictions become less sensitive to noise in any single training point).

---

**Q14. Correct: D**

Random Forest uses bootstrap aggregation (bagging) combined with random feature subsetting, which averages out the high variance of individual overfit trees, directly targeting the variance problem described without increasing bias much.

---

**Q15. Correct: B**

UMAP is built on a learned fuzzy topological representation that supports a proper transform() method for new data, scales significantly better than t-SNE on large datasets due to its optimized nearest-neighbor and embedding graph construction, and is designed to better preserve global structure alongside local neighborhoods compared to t-SNE.

---

**Q16. Correct: B**

Standard self-attention computes an n x n attention score matrix (every token attending to every other token), giving quadratic O(n^2) time and memory complexity in sequence length, which is a well-known limitation motivating techniques like sparse or linear attention for long sequences.

---

**Q17. Correct: A**

Elastic Net combines the L1 penalty (which drives coefficients to exactly zero for feature selection) with the L2 penalty (which stabilizes coefficient estimates and handles grouped, correlated predictors by shrinking them together rather than arbitrarily picking one), directly satisfying both stated requirements.

---

**Q18. Correct: D**

Elastic Net combines L1's sparsity-inducing penalty with L2's grouping effect, so it can zero out irrelevant coefficients while stably keeping or dropping correlated features together, avoiding the arbitrary selection instability that pure Lasso exhibits with correlated predictors.

---

**Q19. Correct: C**

The RBF kernel implicitly maps data into an infinite-dimensional feature space and naturally models radial/circular decision boundaries, making it the standard choice when data separates along curved, non-linear boundaries without manual feature engineering.

---

**Q20. Correct: C**

Shallower trees combined with row subsampling are standard gradient boosting regularization techniques that directly reduce variance and overfitting by limiting each tree's capacity to memorize training data, while the ensemble still learns complex patterns across many boosting rounds.

---

**Q21. Correct: A**

t-SNE is explicitly designed to preserve local neighborhood relationships for 2D/3D visualization by modeling pairwise similarity distributions, deliberately trading off accurate global distances for clearer local cluster separation, matching the stated goal exactly.

---

**Q22. Correct: C**

In self-attention, every token attends directly to every other token in a single layer, giving a constant O(1) path length between any two positions regardless of their distance in the sequence, which avoids the vanishing/exploding gradient problems that arise when information must propagate step-by-step through an RNN's O(n) sequential path.

---

**Q23. Correct: A**

Industry-standard PSI thresholds classify <0.1 as no significant shift, 0.1-0.25 as moderate shift worth watching, and >0.25 as significant shift requiring investigation and likely retraining.

---

**Q24. Correct: C**

A feature store maintains consistent, versioned feature definitions and provides both a low-latency online store for real-time serving and an offline store for training, directly preventing train-serve skew.

---

**Q25. Correct: D**

Canary deployment reduces blast radius by exposing only a small, real subset of production traffic to the new version, allowing teams to detect regressions before increasing exposure.

---

**Q26. Correct: D**

Champion/challenger is an ongoing evaluation pattern where challengers are continuously scored against the reigning production model with defined promotion thresholds, whereas an A/B test is typically time-boxed with a defined stopping point and statistical decision.

---

**Q27. Correct: C**

A model registry retains prior validated, versioned artifacts, enabling near-instant rollback to a known-good state, which is the fastest and most reliable recovery path when a new deployment causes regressions.

---

**Q28. Correct: C**

DAG-based orchestrators explicitly model task dependencies, support conditional branching, retries, and scheduling, making them the standard tool for managing complex multi-stage data science pipelines.

---

**Q29. Correct: B**

A PSI above 0.25 signals a major shift in feature distributions, which is the definition of data (covariate) drift. Because accuracy has not degraded, the drift has not yet impacted the feature-target relationship (that would be concept drift). The correct operational response is to investigate the root cause upstream and keep monitoring performance metrics rather than reflexively retraining.

---

**Q30. Correct: A**

A feature store is purpose-built to provide point-in-time correct, versioned feature values consistently to both offline training pipelines and online low-latency serving, directly preventing training-serving skew.

---

**Q31. Correct: A**

The root cause is that the load operation is not idempotent — re-running a partially completed insert reprocesses already-loaded rows. Converting the load to an idempotent upsert/merge keyed on a business key ensures that reruns after failure produce the same end state without duplication, which is a core MLOps/data-engineering pipeline design principle.

---

**Q32. Correct: B**

Shadow deployment mirrors live production traffic to the candidate model in parallel with the current model, logging its predictions for comparison, but never returns the candidate's output to actual users — exactly meeting the 'no user exposure' requirement.

---

**Q33. Correct: C**

Tukey's HSD test is specifically designed for pairwise mean comparisons after a significant ANOVA result, and it controls the family-wise error rate across all comparisons simultaneously.

---

**Q34. Correct: D**

The Poisson distribution models the number of rare, independent events occurring within a fixed interval at a constant average rate, which exactly matches this failure-count scenario.

---

**Q35. Correct: B**

Degrees of freedom for a chi-squared test of independence equal (rows - 1) x (columns - 1) = (4-1) x (5-1) = 3 x 4 = 12.

---

**Q36. Correct: B**

This correctly captures the fundamental distinction: the Bayesian credible interval is a direct probability statement about the parameter conditioned on the data and prior, while the frequentist confidence interval is a statement about the long-run behavior of the interval-construction procedure across repeated sampling.

---

**Q37. Correct: C**

ARIMA modeling requires stationary input data. The ADF test checks for the presence of a unit root, and if the series is found non-stationary due to trend, differencing is the standard correction before proceeding to model fitting.

---

**Q38. Correct: C**

Oscillating, diverging loss during gradient descent is a classic symptom of an excessively large learning rate causing the optimizer to overshoot the minimum on each step. Reducing the learning rate produces smaller, more stable update steps that allow convergence.

---

**Q39. Correct: D**

Total variance = 52.6. The first eigenvalue alone accounts for 42.1/52.6 = 80.0%. Adding the second (8.3) gives (42.1+8.3)/52.6 = 95.8%, which crosses the 90% threshold. Therefore 2 components are the minimum needed.

---

**Q40. Correct: B**

The ADF null hypothesis is that a unit root is present (non-stationary). Since the test statistic (-1.35) is greater than the critical value (-2.86, i.e., not negative enough) and p = 0.61 > 0.05, the analyst fails to reject the null, meaning the series is non-stationary. The correct remedy before fitting an ARMA-type model is to apply differencing (or transform to induce stationarity).

---

**Q41. Correct: B**

Genetic algorithms are derivative-free metaheuristics that handle discrete, non-differentiable, non-convex search spaces with multiple local optima by maintaining a population and using selection, crossover, and mutation to escape local optima.

---

**Q42. Correct: B**

BPE subword tokenization decomposes unseen or rare words into known subword units, drastically reducing out-of-vocabulary issues while keeping the vocabulary compact—ideal for domain-specific rare terms like medical vocabulary.

---

**Q43. Correct: D**

NMS compares IoU against a threshold; when overlap exceeds that threshold (0.75 > 0.5), the box with the lower confidence score is discarded as a duplicate detection, keeping only the highest-confidence box for that object.

---

**Q44. Correct: A**

Content-based filtering builds recommendations from item attributes (genre, cast, director) and can generate relevant suggestions for new users immediately, without requiring any prior interaction history—directly solving the user cold-start problem.

---

**Q45. Correct: A**

Isolation Forest isolates points via random recursive feature splits, using average path length to a leaf as the anomaly score, with no distance computation. LOF instead compares each point's local density to that of its k-nearest neighbors, flagging points in sparser regions as anomalies.

---

**Q46. Correct: A**

Bayesian optimization builds a probabilistic surrogate model of the objective and uses an acquisition function to intelligently select the next most promising configuration to evaluate, making it highly sample-efficient—critical when each evaluation costs 6 hours of compute.

---

