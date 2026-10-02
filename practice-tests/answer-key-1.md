# Answer Key — Practice Test 1

**Q1. Correct: A**

Computing target-based encoding on the full dataset before splitting lets test-set target information leak into training features, artificially inflating validation performance. The fix is to fit encodings only on training folds (e.g., within a cross-validation loop) and apply them to validation/test data.

---

**Q2. Correct: B**

With extreme class imbalance, Precision-Recall AUC focuses on performance for the rare positive class and is far more sensitive to changes in false positives/negatives among the minority class than ROC-AUC, which can look deceptively high due to the large number of true negatives.

---

**Q3. Correct: C**

MNAR occurs when the probability of a value being missing is related to the unobserved value itself — for example, individuals with very high or very low incomes being more likely to withhold that information. This is the hardest missingness mechanism to handle because it cannot be corrected using observed data alone.

---

**Q4. Correct: B**

A VIF value between 5 and 10 is the widely accepted rule-of-thumb threshold indicating problematic multicollinearity that inflates coefficient variance and destabilizes model interpretation, warranting feature removal, combination, or dimensionality reduction.

---

**Q5. Correct: C**

A log transformation compresses the scale of extreme values, reducing their leverage on the regression coefficients while preserving the legitimate data points and their relative ordering, rather than discarding or distorting valid information.

---

**Q6. Correct: C**

Business stakeholders care about outcomes tied to organizational goals. Translating model performance into concrete business metrics — such as reduced churn rate and estimated retained revenue — makes the value of the model tangible and actionable for non-technical decision makers.

---

**Q7. Correct: C**

Computing target-based encodings on the full dataset before the train/test split leaks information about the test set's target values into the training features, inflating validation metrics artificially. In production, this leaked signal doesn't exist, so performance collapses. Target/mean encoding must always be fit on the training fold only (or via out-of-fold encoding within CV).

---

**Q8. Correct: D**

Precision-Recall AUC is preferred for severely imbalanced datasets because it focuses on the positive (minority) class's precision and recall, which are directly affected by false positives and false negatives on the rare class, without being diluted by the large number of true negatives.

---

**Q9. Correct: D**

A VIF greater than 10 is the widely used industry rule of thumb indicating a predictor is highly correlated with other predictors, meaning its coefficient estimate is inflated and unstable, warranting removal or combination with correlated features. Some conservative practitioners use a VIF > 5 threshold, but 10 is the standard exam-tested cutoff.

---

**Q10. Correct: D**

SHAP (SHapley Additive exPlanations) values provide a local, instance-level explanation showing how each feature value contributed positively or negatively to that specific prediction, making them ideal for explaining individual decisions to non-technical stakeholders such as loan officers or regulators.

---

**Q11. Correct: D**

Concept drift occurs when the statistical relationship between the inputs and the target variable changes over time (e.g., customer behavior patterns shift), degrading a model's predictive validity even if input distributions look similar. Data drift occurs when the distribution of the input features themselves shifts, which can also degrade performance even if the underlying feature-target relationship hasn't changed.

---

**Q12. Correct: B**

Random Forest averages many bagged trees trained on bootstrap samples with random feature subsets, which reduces variance and overfitting while remaining tree-based.

---

**Q13. Correct: B**

t-SNE is a nonlinear technique specifically designed to preserve local neighborhood structure, making it ideal for visualizing clusters in 2D.

---

**Q14. Correct: C**

Transformers use self-attention to directly relate any two tokens in a sequence regardless of distance, effectively capturing long-range dependencies without the sequential bottleneck of RNNs.

---

**Q15. Correct: A**

L1 (Lasso) regularization's penalty geometry drives many coefficients to exactly zero, effectively performing automatic feature selection.

---

**Q16. Correct: A**

As model complexity increases, the model fits training data more closely, reducing bias, but becomes more sensitive to fluctuations in the training data, increasing variance — the core bias-variance tradeoff.

---

**Q17. Correct: C**

DBSCAN is a density-based algorithm that can identify arbitrarily shaped clusters, such as rings, and naturally labels sparse outlier points as noise without requiring the number of clusters to be specified.

---

**Q18. Correct: C**

Gradient boosted trees natively capture nonlinear feature interactions, handle mixed-scale sensor data without heavy preprocessing, support class-weighting for imbalance, and produce calibrated probability outputs via the logistic loss objective.

---

**Q19. Correct: C**

t-SNE is a nonlinear dimensionality reduction technique specifically designed to preserve local neighborhood structure, making it ideal for visualizing cluster separability in low dimensions.

---

**Q20. Correct: D**

L1 (Lasso) regularization adds a penalty proportional to the absolute value of coefficients, which geometrically encourages sparsity and drives irrelevant feature coefficients to exactly zero, performing implicit feature selection.

---

**Q21. Correct: B**

High training AND high test error indicates the model is too simplistic to capture the underlying pattern (underfitting/high bias). Adding more data does not help because the issue is model capacity, not sample size; the fix is increasing complexity or adding informative features.

---

**Q22. Correct: B**

Transformers use self-attention to directly model relationships between all tokens regardless of distance, capturing long-range dependencies effectively, and unlike RNNs/LSTMs, computations across sequence positions can be parallelized, making training on large corpora much faster.

---

**Q23. Correct: B**

Concept drift occurs when the underlying relationship between inputs and the target variable changes (e.g., fraudsters adopting new tactics), causing performance decay even when input feature distributions remain stable. This matches the scenario exactly.

---

**Q24. Correct: B**

Canary deployment gradually exposes a small percentage of live traffic to a new model version to detect issues early and enables fast rollback, which is exactly the risk-mitigation pattern described.

---

**Q25. Correct: D**

Reproducibility requires capturing the exact software environment (library and dependency versions) used to train the model, which is why MLflow automatically logs a conda.yaml/requirements.txt alongside the model artifact.

---

**Q26. Correct: A**

Streaming ingestion via a message broker combined with a stream processing engine (e.g., Kafka + Spark Streaming/Flink) provides the low-latency, continuous, high-throughput pipeline required for real-time anomaly detection on sensor telemetry.

---

**Q27. Correct: C**

Continuous Training extends CI/CD principles to the ML pipeline by automatically retraining and redeploying models when triggers like data drift, schedule, or new data volume are detected, addressing model staleness that pure code-focused CI/CD does not handle.

---

**Q28. Correct: D**

Data versioning tools like DVC track dataset versions using small metadata files and content hashes that reference immutable snapshots already stored in object storage, enabling exact reproducibility without duplicating large datasets for every experiment.

---

**Q29. Correct: B**

Concept drift occurs when the underlying relationship between the input features and the target variable changes over time (e.g., fraud tactics evolve), even though the feature distributions themselves haven't shifted. This explains falling performance without a change in input data statistics.

---

**Q30. Correct: A**

A feature store centralizes feature computation and definitions, ensuring consistent, reusable, and versioned features are shared across teams for both training and serving, eliminating duplicated logic and skew.

---

**Q31. Correct: B**

Canary deployment gradually shifts a small, increasing percentage of live traffic to a new version while actively monitoring health metrics, allowing rollback before wide impact if problems are detected.

---

**Q32. Correct: A**

Full reproducibility requires tracking the exact code version, the exact dataset snapshot used (since source data can change), the hyperparameters, and the random seed controlling stochastic processes (initialization, shuffling, splits). Missing any one of these can produce different results even with the same model.

---

**Q33. Correct: D**

The chi-squared test of independence is designed to determine whether two categorical variables are statistically associated by comparing observed frequencies in a contingency table to expected frequencies under independence.

---

**Q34. Correct: D**

One-way ANOVA first tests whether any of the five group means differ overall, and Tukey's HSD then performs pairwise comparisons while controlling the family-wise error rate, avoiding the inflated Type I error of running many uncorrected t-tests.

---

**Q35. Correct: A**

In frequentist statistics, the population mean is a fixed but unknown constant, not a random variable, so probability statements apply to the long-run behavior of the interval-construction procedure: 95% of intervals generated this way, over repeated sampling, would contain the true mean.

---

**Q36. Correct: B**

In PCA, the covariance matrix is decomposed into eigenvectors and eigenvalues; each eigenvalue represents the amount of variance captured along its corresponding eigenvector (principal component), and components are ranked by descending eigenvalue.

---

**Q37. Correct: A**

When the population standard deviation is unknown and the sample size is small, the t-distribution must be used with degrees of freedom equal to n - 1, which is 14 for a sample of 15.

---

**Q38. Correct: A**

Differencing subtracts each observation from the previous one, removing trend and stabilizing the mean of the series over time, which is a core requirement for ARIMA modeling and is validated using tests like the Augmented Dickey-Fuller (ADF) test.

---

**Q39. Correct: D**

The Augmented Dickey-Fuller test is the standard unit-root test used to formally check stationarity in a time series. A non-rejected null hypothesis indicates the presence of a unit root (non-stationary), signaling the need for differencing (choosing the 'd' parameter) before ARIMA modeling.

---

**Q40. Correct: D**

This captures the core philosophical distinction tested on the exam: Bayesian credible intervals treat the parameter as a random variable and make a direct probability statement conditioned on observed data and prior beliefs, while frequentist confidence intervals treat the parameter as fixed and describe the long-run behavior of the interval-construction procedure across repeated samples.

---

**Q41. Correct: A**

Hybrid recommenders solve cold-start by falling back to content-based similarity (item attributes) when interaction data is absent, while still exploiting collaborative signals once enough interactions accumulate. This is the standard, exam-tested fix for the item cold-start problem.

---

**Q42. Correct: A**

NER is specifically designed to identify and classify spans of text into predefined categories such as product names, dates, and monetary values, which is exactly the extraction task described.

---

**Q43. Correct: C**

NMS suppresses a lower-scoring box only when its IoU with a higher-scoring box exceeds the threshold. A threshold as high as 0.9 requires near-total overlap before suppression occurs, so boxes with moderate overlap (e.g., 0.5-0.8) are NOT suppressed and duplicate detections persist.

---

**Q44. Correct: B**

Autoencoders learn a compressed latent representation of normal high-dimensional data without any distributional assumption; samples that reconstruct poorly (high reconstruction error) are flagged as anomalous. This scales well to 500+ correlated sensor dimensions and captures cross-sensor relationships.

---

**Q45. Correct: C**

This is the core distinction: content-based filtering uses item feature similarity relative to a user's own past preferences, while collaborative filtering leverages the collective interaction patterns of many users (or items) to infer preferences, requiring no item metadata.

---

**Q46. Correct: A**

Genetic algorithms are derivative-free metaheuristics well-suited to non-convex, non-differentiable, mixed discrete-continuous optimization problems like vehicle routing with complex constraints, since they don't require gradient information or convexity.

---

