# Practice Test 2: CompTIA DataX (DY0-001): Expert Data Science Exam Prep

- **Questions:** 46
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-2.md`. Track results in `score-tracker.md`.

---

**Q1.** A data scientist is building a churn prediction model to predict whether a customer will churn within the next 30 days. The dataset includes a feature called 'support_tickets_after_churn_decision', which captures the number of support tickets the customer opened in the 30 days following the churn event. The model achieves 98% accuracy on the holdout test set, but performance drops to 62% in production. What is the MOST likely cause of this discrepancy?

A) Target leakage occurred because the feature captures information generated after the outcome is known, which is unavailable at prediction time
B) The holdout test set was too small to accurately reflect production performance
C) The model overfit due to an excessive number of trees in the ensemble
D) The production data distribution shifted due to seasonal effects, causing model drift

---

**Q2.** A data science team is building a fraud detection model where fraudulent transactions represent only 0.3% of all transactions. The business requires the model to rank transactions by fraud risk so that only the top 1% highest-risk transactions are sent for manual review. Which evaluation metric is MOST appropriate for comparing candidate models in this scenario?

A) Overall classification accuracy
B) Area under the ROC curve (ROC-AUC)
C) F1 score computed at a fixed threshold of 0.5
D) Area under the precision-recall curve (PR-AUC)

---

**Q3.** An analyst discovers that income data is missing for high-income survey respondents at a substantially higher rate than for low-income respondents, and no observed variable in the dataset explains this pattern. Which missing data mechanism best describes this situation, and what is an appropriate strategy?

A) Missing Not at Random (MNAR); the missingness depends on the unobserved value itself, requiring explicit modeling of the missingness mechanism rather than standard imputation
B) Missing Completely at Random (MCAR); listwise deletion is unbiased and appropriate here
C) Missing at Random (MAR); multiple imputation conditioned on observed covariates fully resolves the bias
D) Missing at Random (MAR); mean imputation is sufficient since the overall distribution is roughly preserved

---

**Q4.** A credit default prediction model outputs predicted probabilities. The business assigns a cost of $500 for a false negative (a missed default) and $50 for a false positive (unnecessarily denying credit to a good customer). Which approach should the data scientist use to select the classification threshold instead of the default 0.5 cutoff?

A) Select the threshold that maximizes the F1 score, which balances precision and recall equally
B) Select the threshold that minimizes the expected total cost, computed as (FN count x $500) + (FP count x $50), evaluated across candidate thresholds on validation data
C) Select the threshold using Youden's J statistic to maximize sensitivity plus specificity minus one
D) Select the threshold that minimizes the overall misclassification error rate on the validation set

---

**Q5.** Which statement correctly differentiates wrapper methods from filter methods in feature selection?

A) Filter methods evaluate feature subsets using the performance of a specific downstream model, while wrapper methods rank features using statistical measures independent of any model
B) Both wrapper and filter methods require repeatedly training the downstream model, differing only in the statistical test applied to the results
C) Filter methods and wrapper methods are functionally identical to embedded methods such as LASSO regularization, differing only in implementation details
D) Wrapper methods evaluate feature subsets using the performance of a specific downstream model, making them computationally expensive but able to capture feature interactions, while filter methods use statistical measures independent of the model and are cheaper but may miss interactions

---

**Q6.** A loan officer asks the data science team to explain why one specific applicant's loan application was denied by the model, so the officer can communicate the specific reasons to that applicant as required by regulation. Which explainability technique is MOST appropriate for this request?

A) Partial dependence plots (PDP) showing the average effect of each feature across the entire training dataset
B) SHAP (SHapley Additive exPlanations) values computed for that individual applicant's prediction, showing each feature's contribution to that specific decision
C) Global feature importance rankings extracted from the trained random forest model
D) The overall model accuracy and AUC reported on the validation dataset

---

**Q7.** A data scientist builds a customer churn model. One engineered feature, 'total_lifetime_transaction_count', is computed by aggregating ALL transaction records for each customer in the raw event log, including transactions that occurred after the customer's churn date. The model achieves 0.98 AUC on a held-out test set, far exceeding the team's baseline of 0.75. What is the MOST likely explanation and correct fix?

A) The model has learned a genuinely strong signal; deploy it immediately since the high AUC confirms production readiness
B) The class imbalance between churned and retained customers is inflating the AUC, so the fix is to apply SMOTE to the training set
C) The test set is too small to be reliable; the fix is to increase the holdout size and re-run cross-validation
D) This is target leakage — the feature encodes information from after the prediction cutoff date, so it must be recomputed using only data available up to each customer's churn/reference timestamp

---

**Q8.** A fraud detection model is trained on a dataset with a 1:200 class imbalance (fraud:legitimate). During model selection, the team compares candidates using ROC-AUC and picks the highest scorer (0.95). After deployment, investigators report that the model misses a large share of actual fraud cases relative to the alerts it raises. Which change to the model selection process would have BEST addressed this issue?

A) Continue using ROC-AUC but average scores across more cross-validation folds
B) Switch to plain classification accuracy as the primary selection metric
C) Retrain using only the minority (fraud) class samples to remove the imbalance entirely
D) Select models based on Precision-Recall AUC (or a cost-weighted F-beta score) instead of ROC-AUC, since ROC-AUC can look excellent even when precision on the rare positive class is poor

---

**Q9.** In a linear regression model predicting housing prices, the coefficient sign for 'square_footage' flips between positive and negative depending on which random subset of training data is used, even though the overall model R² is stable. A variance inflation factor (VIF) analysis shows VIF = 15 for both 'square_footage' and 'number_of_rooms'. What is the BEST next step?

A) Remove or combine one of the two highly collinear features (e.g., drop one, or engineer a combined feature such as square_footage-per-room) before re-estimating coefficients
B) Increase the polynomial degree of both features to capture nonlinear relationships
C) Ignore the VIF values since R² is stable, and proceed to deployment
D) Add L1 regularization only to the intercept term to stabilize the fit

---

**Q10.** A gradient boosted tree model shows training error near zero, while validation error plateaus at a much higher level, and the gap between the two curves widens as more training rounds are added. Which combination of actions is MOST appropriate to address this specific diagnostic pattern?

A) Increase max_depth and reduce min_child_weight to let the trees fit the training data more precisely
B) Apply stronger regularization (e.g., lower max_depth, higher min_child_weight, subsampling) and/or gather more training data to reduce the train-validation gap
C) Add more boosting rounds with a higher learning rate to help the validation error catch up to the training error
D) Switch to a linear model class entirely, since tree ensembles cannot be regularized

---

**Q11.** A model predicting loan default probability achieves strong discrimination (AUC = 0.89), and the business team plans to use the predicted probabilities directly to set risk-based interest rates. Upon inspection, a reliability (calibration) plot shows predicted probabilities cluster heavily near 0 and 1, diverging substantially from observed default rates in each probability bin. What should be done before this model is used for probability-based pricing?

A) Apply a calibration technique such as Platt scaling or isotonic regression to align predicted probabilities with observed frequencies, since good discrimination (AUC) does not guarantee well-calibrated probabilities
B) Report the AUC of 0.89 to stakeholders as sufficient evidence that the probabilities are trustworthy for pricing
C) Retrain using SMOTE to rebalance the classes, which will automatically fix the calibration
D) Increase the maximum depth of the underlying trees to sharpen the probability estimates further

---

**Q12.** A data scientist is training an SVM classifier on a dataset with 50,000 engineered features but only 300 training samples (severe p >> n scenario). Which kernel choice minimizes overfitting risk while keeping training time reasonable?

A) Polynomial kernel of degree 3
B) Sigmoid kernel
C) Linear kernel
D) RBF kernel with default gamma

---

**Q13.** As the value of k increases in a k-nearest neighbors classifier, what happens to the model's bias and variance?

A) Bias decreases and variance increases
B) Both bias and variance decrease
C) Bias increases and variance decreases
D) Neither bias nor variance changes, only training time is affected

---

**Q14.** A single decision tree model exhibits very low training error but significantly higher validation error, indicating high variance and severe overfitting. Which ensemble technique is BEST suited to directly address this specific problem?

A) AdaBoost, which reweights misclassified samples on each iteration
B) Gradient Boosting Machines with a deep base learner
C) Stacking with a linear meta-learner on top of the single tree
D) Random Forest, which aggregates predictions from bagged trees

---

**Q15.** A data scientist needs a nonlinear dimensionality reduction technique that preserves both local and global structure, scales efficiently to datasets with over 1 million rows, and supports transforming new, previously unseen data points after the model is fit. Which technique should be chosen?

A) t-SNE
B) UMAP
C) Principal Component Analysis (PCA)
D) Isomap

---

**Q16.** The standard self-attention mechanism in a Transformer architecture computes pairwise attention scores between all tokens in a sequence. What is the computational complexity of this operation with respect to sequence length n?

A) O(n)
B) O(n^2)
C) O(2^n)
D) O(n log n)

---

**Q17.** A dataset contains 200 features, many of which are highly correlated with one another. The data scientist wants automatic feature selection (driving irrelevant coefficients toward zero) while maintaining stable coefficient estimates despite the multicollinearity. Which regularization approach BEST meets these requirements?

A) Elastic Net regularization
B) L1 (Lasso) regularization only
C) No regularization, combined with manual stepwise feature selection
D) L2 (Ridge) regularization only

---

**Q18.** A data scientist is building a linear regression model with 200 features, many of which are highly correlated with each other. Only about 15 features are believed to be truly predictive, and the final model must produce a sparse, interpretable set of coefficients for stakeholder reporting. Which regularization approach BEST meets these requirements?

A) Ridge regression (L2) with a large penalty term
B) Lasso regression (L1) alone
C) No regularization, followed by manual feature elimination
D) Elastic Net with a high L1 mixing ratio

---

**Q19.** A dataset has two classes that are not linearly separable in the original two-dimensional feature space, but visual inspection suggests the classes could be separated by a circular decision boundary. Which SVM kernel is BEST suited to capture this boundary without manually engineering polynomial features?

A) Linear kernel
B) Polynomial kernel of degree 1
C) RBF (Gaussian) kernel
D) Sigmoid kernel

---

**Q20.** A gradient boosting model (e.g., XGBoost) is overfitting significantly, achieving 99% training accuracy but only 78% validation accuracy. The current configuration uses learning_rate=0.3, n_estimators=500, and max_depth=10. Which single configuration change is MOST likely to reduce overfitting while preserving the model's ability to learn complex patterns?

A) Increase max_depth to 15 to capture more complex splits
B) Increase n_estimators to 1000 while keeping learning_rate at 0.3
C) Reduce max_depth to 3-5 and set subsample to 0.8
D) Increase learning_rate to 0.5 to converge faster

---

**Q21.** A data scientist needs to visualize a 50-dimensional dataset in 2D specifically to reveal local cluster structure among data points, even if global distances between distant clusters become distorted in the process. Which technique is BEST suited for this specific visualization goal?

A) t-SNE
B) Principal Component Analysis (PCA)
C) Linear Discriminant Analysis (LDA)
D) Factor Analysis

---

**Q22.** A team must process sequences up to 10,000 tokens long for a task requiring the model to accurately capture relationships between tokens that are far apart in the sequence. Memory is not a constraint. Which characteristic makes the standard Transformer's self-attention mechanism BEST suited for this task compared to a vanilla RNN/LSTM?

A) Self-attention has O(n) time complexity per layer, faster than an RNN's O(n^2)
B) Self-attention processes tokens strictly sequentially, similar to RNNs but with added memory cells
C) Self-attention directly connects any two tokens with a constant path length, avoiding the vanishing-gradient issues RNNs face over long sequential distances
D) Self-attention reduces the vocabulary size needed for the embedding lookup table

---

**Q23.** A team monitors a production credit-risk model using the Population Stability Index (PSI), computed weekly between the current feature distribution and the training baseline. This week the PSI for the applicant-income feature is 0.31. Based on standard drift-monitoring thresholds tested on the exam, which action is BEST justified?

A) Investigate the feature and consider retraining, since PSI above 0.25 indicates significant population shift
B) No action is needed because PSI values below 0.5 indicate a stable population
C) Switch the model permanently to a rule-based fallback system
D) Increase the model's L2 regularization coefficient to compensate for the drift

---

**Q24.** A team is building a real-time fraud-scoring service. They need identical feature computation logic used at both training time and inference time, low-latency lookups (single-digit milliseconds) for pre-computed features, and versioned feature definitions shared across multiple models. Which component BEST satisfies these requirements?

A) A raw data lake storing unprocessed event logs
B) A relational data warehouse optimized for batch analytics queries
C) A feature store with online and offline serving layers
D) A Kafka topic used only as a message broker between microservices

---

**Q25.** A team deploys a new fraud-detection model version using a canary release strategy, initially routing 5% of production traffic to it while comparing latency and accuracy metrics against the existing model before increasing the rollout percentage. Which statement correctly describes this configuration?

A) The canary model must be trained using only the 5% of traffic it will initially receive
B) Canary deployment duplicates every incoming request to both models without exposing users to the new model's output
C) Canary deployment is functionally identical to a full blue-green cutover of all traffic at once
D) Canary deployment limits risk exposure by serving real users a small fraction of traffic while metrics are validated before full rollout

---

**Q26.** What BEST distinguishes a champion/challenger evaluation framework from a standard fixed-duration A/B test in an MLOps context?

A) Champion/challenger frameworks apply only to classification models, while A/B tests apply only to regression models
B) A/B testing requires no traffic splitting, while champion/challenger requires splitting 100% of traffic to the challenger
C) Champion/challenger is used exclusively for UI experiments, while A/B testing is used exclusively for backend model changes
D) Champion/challenger continuously evaluates candidate models against the current production model with ongoing promotion criteria, while A/B testing runs a fixed-duration randomized experiment that ends with a single winner selection

---

**Q27.** A CI/CD pipeline automatically promotes new model versions to production after passing validation tests. Shortly after a new version deploys, monitoring alerts trigger for a significant spike in prediction latency and error rate. Which MLOps practice BEST enables rapid recovery from this incident?

A) Wait until the next scheduled deployment window to apply a fix
B) Manually edit the serving code directly on the production instance to patch the issue
C) Roll back to the previously validated model version stored in the model registry
D) Immediately begin retraining the model from scratch on the full historical dataset

---

**Q28.** A data science team needs to orchestrate a pipeline involving conditional branching, explicit task dependencies across ingestion, feature engineering, and training stages, automatic retries on failure, and scheduled execution. Which orchestration approach is BEST suited for this requirement?

A) A single monolithic shell script executing all steps sequentially
B) A simple cron job triggering each script independently with no dependency awareness
C) A directed acyclic graph (DAG)-based workflow orchestrator managing task dependencies and retries
D) A message queue used solely to pass raw data between independent consumer services

---

**Q29.** A team monitors a production credit-scoring model. Over three months, the model's classification accuracy on labeled outcomes remains stable at 91%, but the Population Stability Index (PSI) on the model's input features rises from 0.05 to 0.35. Which statement best describes the situation and the appropriate next step?

A) Concept drift is occurring, so the team should retrain the model immediately using the most recent labeled data
B) Data (covariate) drift is occurring in the input feature distributions; the team should investigate upstream data source changes and continue monitoring performance before retraining
C) Label leakage has occurred, so the team should audit the training pipeline for target leakage
D) The model is overfitting to the training set, so the team should reduce model complexity

---

**Q30.** A data science team needs a system that stores versioned, point-in-time correct feature values so that the exact same feature computations used during model training are available with low latency for real-time inference, eliminating training-serving skew. Which MLOps component should they implement?

A) A feature store
B) A model registry
C) A raw data lake
D) An experiment tracking system

---

**Q31.** A daily batch ingestion pipeline loads sales transactions into a data warehouse table. Occasionally the job fails midway through loading and is automatically retried. After several such failures, engineers discover duplicate rows in the target table. Which design change would BEST fix this at the pipeline architecture level?

A) Redesign the load step to be idempotent, using upsert/merge operations keyed on a natural or business key instead of plain inserts
B) Increase the retry count configured for the failing task
C) Provision additional compute resources for the ingestion job
D) Increase the frequency of the pipeline schedule so smaller batches are loaded more often

---

**Q32.** An ML team wants to evaluate a new candidate model against real production traffic to compare its predictions with the current live model's predictions, but they must ensure that no end user is ever exposed to the candidate model's output during this evaluation period. Which deployment strategy satisfies this requirement?

A) Canary deployment
B) Shadow deployment
C) Blue-green deployment
D) A/B testing

---

**Q33.** A data science team runs a one-way ANOVA comparing average time-on-page across four redesigned landing page variants (A, B, C, D). The ANOVA F-test returns p = 0.008, rejecting the null hypothesis of equal means. The team must now determine exactly which pairs of variants differ significantly while controlling the family-wise error rate. Which approach BEST accomplishes this?

A) Run six separate two-sample t-tests between each pair of variants using alpha = 0.05 for each
B) Re-run the ANOVA separately for each pair of variants
C) Apply Tukey's Honestly Significant Difference (HSD) test to compare all pairwise means
D) Apply a chi-squared test of independence to the four variant groups

---

**Q34.** A reliability engineer is modeling the number of hard-drive failures that occur in a data center per week. Failures are rare, independent, and occur at a constant average rate. Which probability distribution is MOST appropriate to model this count data?

A) Normal distribution
B) Binomial distribution
C) Exponential distribution
D) Poisson distribution

---

**Q35.** A researcher builds a contingency table to test independence between customer region (4 categories) and product preference (5 categories) using a chi-squared test of independence. How many degrees of freedom does this test have?

A) 20
B) 12
C) 9
D) 19

---

**Q36.** A data scientist computes a 95% credible interval for a parameter using a Bayesian posterior distribution, and a colleague computes a 95% confidence interval for the same parameter using frequentist methods. Which statement correctly distinguishes the interpretation of these two intervals?

A) Both intervals mean there is a 95% probability the true parameter lies within the stated bounds
B) The credible interval means there is a 95% probability the true parameter value lies within the interval, given the observed data and prior; the confidence interval means 95% of intervals constructed the same way from repeated sampling would contain the true parameter
C) The confidence interval is always narrower than the credible interval because it does not depend on a prior distribution
D) The credible interval requires no prior information, while the confidence interval always requires a specified prior

---

**Q37.** An analyst wants to fit an ARIMA model to a company's monthly revenue time series, which shows a clear upward trend over five years. Before selecting model parameters, which step should be performed FIRST to ensure valid results?

A) Fit the ARIMA model directly to the raw revenue series and evaluate residual autocorrelation
B) Apply a chi-squared goodness-of-fit test to confirm the data follows a Poisson distribution
C) Apply an Augmented Dickey-Fuller (ADF) test to check for stationarity, and difference the series if a unit root is found
D) Increase the training window to include more historical data points

---

**Q38.** While training a regression model using gradient descent, the analyst observes that the loss value oscillates wildly and diverges to increasingly large values after each iteration instead of decreasing. Which adjustment is MOST likely to resolve this issue?

A) Increase the learning rate to help the optimizer escape the oscillation
B) Switch from mean squared error to mean absolute error as the loss function
C) Decrease the learning rate so that gradient update steps are smaller
D) Increase the batch size to include the entire dataset in a single update

---

**Q39.** A data scientist computes the covariance matrix of a 5-feature dataset and extracts eigenvalues: 42.1, 8.3, 1.2, 0.9, and 0.1. Using PCA, what is the minimum number of principal components needed to retain at least 90% of the total variance?

A) 3 components
B) 1 component
C) 4 components
D) 2 components

---

**Q40.** A time-series analyst runs an Augmented Dickey-Fuller (ADF) test on a stock price series and obtains a test statistic of -1.35 with a p-value of 0.61. The 5% critical value is -2.86. What should the analyst conclude and do next?

A) Reject the null hypothesis; the series has a unit root, so apply seasonal decomposition only
B) Fail to reject the null hypothesis; the series is non-stationary, so apply differencing before modeling
C) Fail to reject the null hypothesis; the series is stationary, so no transformation is needed
D) Reject the null hypothesis; the series is stationary, so proceed to fit an ARMA model directly

---

**Q41.** A manufacturing team needs to optimize a production schedule with 200 discrete variables. The objective function is non-differentiable and non-convex, with many local optima caused by machine changeover constraints. Which optimization approach BEST meets these requirements?

A) Gradient descent with momentum
B) Genetic algorithm with tournament selection
C) Newton's method
D) Linear programming simplex method

---

**Q42.** A team is building a text classifier for clinical notes that must handle rare medical terms, drug names, and misspellings not seen during training, while keeping vocabulary size manageable. Which tokenization approach BEST meets these requirements?

A) Word-level tokenization with a fixed 30,000-word vocabulary
B) Byte-Pair Encoding (BPE) subword tokenization
C) Character n-gram bag-of-words counts only
D) Whitespace tokenization

---

**Q43.** During non-maximum suppression (NMS) in an object detection pipeline, two bounding boxes predicted for the same object have an IoU of 0.75, and the NMS IoU threshold is set to 0.5. What happens to these two boxes?

A) Both boxes are kept because the IoU exceeds the confidence threshold
B) Both boxes are automatically merged into a single averaged box
C) The box with the higher confidence score is suppressed to reduce false positives
D) The box with the lower confidence score is suppressed because the IoU exceeds the NMS threshold

---

**Q44.** A streaming platform launches a new service with zero historical interaction data for brand-new users, but it has rich content metadata including genre, cast, and director for every title. Which recommendation approach BEST meets these requirements for serving new users?

A) Content-based filtering using item metadata features
B) Collaborative filtering using user-item matrix factorization
C) Deep collaborative filtering with neural embeddings trained on interaction history
D) Association rule mining on purchase co-occurrence

---

**Q45.** Which statement correctly differentiates Isolation Forest from Local Outlier Factor (LOF) for anomaly detection?

A) LOF measures local density deviation relative to neighbors, while Isolation Forest isolates anomalies via random recursive partitioning without computing distances
B) Isolation Forest requires computing pairwise distances between all points, while LOF does not
C) Isolation Forest only works on labeled data, while LOF is fully unsupervised
D) LOF scales better than Isolation Forest to high-dimensional, large datasets

---

**Q46.** A team needs to tune 8 continuous hyperparameters for a deep learning model where each training run takes 6 hours to complete. Which optimization strategy BEST meets these requirements to minimize total tuning time while finding near-optimal settings?

A) Bayesian optimization using a Gaussian process surrogate model
B) Exhaustive grid search over all combinations
C) Random search with 1,000 iterations
D) Manual trial and error based on intuition

---

