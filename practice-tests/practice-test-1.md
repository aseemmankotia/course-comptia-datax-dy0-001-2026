# Practice Test 1: CompTIA DataX (DY0-001): Expert Data Science Exam Prep

- **Questions:** 46
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-1.md`. Track results in `score-tracker.md`.

---

**Q1.** A data scientist builds a churn prediction model achieving 99% AUC on validation but only 62% AUC in production. Investigation reveals that a categorical feature was encoded using the target variable's mean computed on the entire dataset before splitting into train and test sets. Which BEST describes the problem and the correct fix?

A) Data leakage occurred because the target-derived encoding used information from the full dataset — recompute encodings using only training-fold statistics within cross-validation
B) The model is overfitting due to excessive complexity — reduce tree depth or add regularization
C) Class imbalance is inflating the AUC score — apply SMOTE to balance the classes before retraining
D) Covariate shift between training and production data exists — apply domain adaptation techniques to recalibrate the model

---

**Q2.** A fraud detection dataset contains 0.5% positive (fraud) cases and 99.5% negative cases. Which metric BEST evaluates model performance for this highly imbalanced classification problem?

A) Overall accuracy
B) Precision-Recall AUC
C) Mean Squared Error
D) ROC-AUC

---

**Q3.** Data is considered Missing Not At Random (MNAR) when:

A) Missingness depends only on other observed variables and can be fully modeled using those variables
B) Missingness occurs completely randomly and is unrelated to any variable in the dataset
C) Missingness depends on the value that is missing itself, such as high-income individuals declining to report income
D) The missingness pattern can be safely ignored without introducing any bias into the analysis

---

**Q4.** During feature engineering, a data scientist calculates the Variance Inflation Factor (VIF) for each numeric predictor to assess multicollinearity. Which VIF threshold is commonly used to flag a feature as problematic and worth removing or combining with another feature?

A) VIF greater than 1.0
B) VIF greater than 5 to 10
C) VIF greater than 100
D) VIF greater than 2.0

---

**Q5.** A housing price dataset contains a small number of legitimate but extreme luxury property listings that are skewing the coefficients of a linear regression model. Which approach BEST addresses this issue without discarding valid data?

A) Remove all rows where price exceeds 1.5 times the IQR from the median
B) Convert the regression problem into a binary classification problem
C) Apply a log transformation to the price variable to reduce the influence of extreme values
D) Impute the extreme prices with the median price of the dataset

---

**Q6.** A data science team presents a customer churn model with 85% accuracy to business stakeholders, who are confused about its practical value. Which approach BEST communicates the model's business impact?

A) Report the model's F1 score and explain how the harmonic mean of precision and recall is calculated
B) Present the ROC curve and provide a mathematical explanation of the area under the curve
C) Translate model performance into an expected reduction in customer churn and estimated revenue retained
D) Show the full confusion matrix with raw counts of true positives, true negatives, false positives, and false negatives

---

**Q7.** A data scientist is building a fraud-detection model. To handle a high-cardinality categorical feature, they compute target encoding (mean of the target variable per category) using the entire dataset, then split into train/test sets and train the model. Validation AUC is 0.97, but production performance drops sharply to 0.71 within the first week. Which issue BEST explains this behavior?

A) The model is overfitting because too many one-hot encoded features were created
B) The categorical feature has too many unique values for any encoding scheme to work correctly
C) Target leakage occurred because the encoding was computed using the full dataset, including test rows, before splitting
D) Feature scaling was not applied before encoding the categorical variable

---

**Q8.** A churn-prediction dataset has 1% positive (churn) cases and 99% negative cases. Which evaluation metric BEST captures model performance on the minority class in this scenario?

A) ROC-AUC
B) Overall classification accuracy
C) Mean Absolute Error
D) Precision-Recall AUC

---

**Q9.** During feature selection for a regression model, an analyst calculates Variance Inflation Factor (VIF) for each predictor to detect multicollinearity. What VIF value is commonly used as the threshold above which a feature is flagged for removal or further investigation?

A) VIF less than 1
B) VIF equal to 0
C) VIF greater than 100
D) VIF greater than 10

---

**Q10.** A credit-risk model denies a specific loan application, and a non-technical loan officer asks the data science team why this particular applicant was denied. Which technique should the analyst use to communicate the reasoning for this individual decision?

A) Global feature importance rankings from the Random Forest model
B) A confusion matrix summarizing the entire test set
C) k-fold cross-validation scores from model training
D) SHAP values computed for that specific prediction

---

**Q11.** In the context of monitoring a deployed model over time, which statement correctly distinguishes concept drift from data drift?

A) Data drift refers to a change in the relationship between features and the target, while concept drift refers to a change in the distribution of input features
B) Concept drift and data drift are two different terms describing the exact same phenomenon
C) Concept drift only applies to time-series forecasting models and has no relevance to classification models
D) Concept drift refers to a change in the underlying relationship between features and the target over time, while data drift refers to a change in the distribution of input features while that relationship remains stable

---

**Q12.** A data scientist trains a decision tree that achieves 99% accuracy on training data but only 62% accuracy on a held-out test set. Which technique BEST addresses this issue while preserving the tree-based modeling approach?

A) Increase the maximum tree depth to capture more patterns in the training data
B) Apply a Random Forest ensemble using bagging to reduce variance
C) Train a single deeper decision tree with pruning disabled
D) Add polynomial interaction features to the input data before retraining the tree

---

**Q13.** A dataset with 10,000 features and only 500 samples needs to be reduced to two dimensions specifically to visually inspect natural groupings in a scatter plot. Which technique is BEST suited for this visualization task?

A) Principal Component Analysis (PCA)
B) t-SNE
C) Linear Discriminant Analysis (LDA)
D) Truncated SVD

---

**Q14.** A team must build a model to translate variable-length English sentences into French, capturing dependencies between words that may be far apart in the sequence. Which architecture is BEST suited for this task?

A) Convolutional Neural Network (CNN)
B) Vanilla Recurrent Neural Network (RNN)
C) Transformer using self-attention
D) Random Forest trained on n-gram features

---

**Q15.** A data scientist wants linear regression training to automatically perform feature selection by driving many coefficient values to exactly zero. Which regularization configuration should be used?

A) L1 (Lasso) regularization
B) L2 (Ridge) regularization
C) Elastic Net with the L1 mixing ratio set to 0 (pure L2)
D) No regularization, relying only on early stopping

---

**Q16.** Which statement BEST describes how bias and variance typically change as model complexity increases?

A) Bias decreases and variance increases as model complexity increases
B) Bias increases and variance decreases as model complexity increases
C) Both bias and variance increase together as model complexity increases
D) Bias and variance remain constant regardless of model complexity

---

**Q17.** A dataset contains customer locations forming clusters of arbitrary shapes, including a ring-shaped group surrounding a dense central cluster, plus scattered points that do not belong to any group. Which clustering algorithm BEST handles this scenario?

A) K-means with k set to 3
B) Hierarchical clustering with Ward linkage
C) DBSCAN
D) Gaussian Mixture Model with 3 components

---

**Q18.** A data science team is building a model to predict equipment failure using 200 sensor readings that have complex, nonlinear interactions with the target. The dataset is moderately sized (15,000 rows), and stakeholders require the model to output probability estimates while also handling mild class imbalance without heavy preprocessing. Which algorithm BEST meets these requirements?

A) Simple linear regression with polynomial feature expansion
B) K-means clustering followed by manual failure labeling
C) Gradient Boosted Trees (e.g., XGBoost) with a logistic loss function
D) Linear Discriminant Analysis (LDA)

---

**Q19.** An analyst has a 50-dimensional customer dataset and needs to project it into 2D purely to visually inspect whether natural clusters exist, prioritizing preservation of local neighborhood structure over global variance. Which technique is the BEST choice?

A) Linear Discriminant Analysis (LDA)
B) Principal Component Analysis (PCA)
C) t-distributed Stochastic Neighbor Embedding (t-SNE)
D) Random feature selection

---

**Q20.** A data scientist has a linear regression model with 300 input features, many of which are believed to be irrelevant. The primary goal is to automatically drive the coefficients of irrelevant features to exactly zero, effectively performing feature selection during training. Which regularization approach should be configured?

A) Ridge regression (L2 penalty)
B) No regularization, increase training epochs
C) Dropout regularization
D) Lasso regression (L1 penalty)

---

**Q21.** A model exhibits consistently high training error and high test error, and adding more training data does not improve performance. Which condition does this describe, and what is the appropriate remedy?

A) High variance; the remedy is to reduce model complexity
B) High bias; the remedy is to increase model complexity or add features
C) Overfitting; the remedy is to add L2 regularization
D) Data leakage; the remedy is to re-split the dataset

---

**Q22.** A team is building a text classification model that must capture long-range dependencies across a 2,000-word document, and training must be parallelizable across GPUs for reasonable training time on large corpora. Which architecture is the BEST fit?

A) Vanilla Recurrent Neural Network (RNN)
B) Transformer with self-attention
C) Convolutional Neural Network (CNN) with small fixed kernel size
D) Long Short-Term Memory (LSTM) network

---

**Q23.** A company deployed a fraud-detection model into production. Over three months, precision dropped from 92% to 74%, but monitoring shows the incoming feature distributions still closely match the training data distribution. What is the MOST likely explanation?

A) Data drift caused by a covariate shift in the input features
B) Concept drift, where the relationship between features and the fraud label has changed over time
C) Training-serving skew caused by inconsistent feature computation between training and inference
D) Label leakage that inflated training performance but not production performance

---

**Q24.** A team wants to deploy a new recommendation model with minimal risk. They plan to route only 5% of live production traffic to the new model, monitor online business metrics against the incumbent model, and roll back quickly if problems appear, while 95% of users continue receiving results from the current model. Which deployment strategy is being described?

A) Blue-green deployment
B) Canary deployment
C) Shadow deployment
D) A/B testing

---

**Q25.** In an MLflow experiment tracking workflow, which artifact should be logged alongside the model file to ensure the model can be fully and exactly reproduced later, including its runtime dependencies?

A) Only the final hyperparameter dictionary used for the run
B) Only the serialized model weights file
C) Only the evaluation metrics recorded for the run
D) An environment specification file (e.g., conda.yaml or requirements.txt) capturing exact library versions

---

**Q26.** A data engineering team must ingest continuous telemetry from thousands of IoT sensors and support sub-second latency for real-time anomaly detection. Which ingestion architecture BEST meets this requirement?

A) Streaming ingestion using a message broker (e.g., Kafka) paired with a stream processing engine
B) A nightly batch ETL job that loads sensor data into a data warehouse
C) Manual CSV file uploads collected periodically from each sensor gateway
D) A scheduled ODBC connector performing bulk loads every few hours

---

**Q27.** In MLOps maturity models, what specifically distinguishes Continuous Training (CT) from traditional Continuous Integration/Continuous Delivery (CI/CD)?

A) CT is simply another name for the code integration and testing stage of CI/CD
B) CT refers exclusively to running training jobs on GPU hardware instead of CPU
C) CT automatically retrains and redeploys models in response to triggers such as data drift or new data, while CI/CD automates building, testing, and releasing code
D) CT means continuously testing model code without ever deploying it to production

---

**Q28.** A data science team has multiple members running experiments with different feature engineering pipelines on a shared 50GB dataset stored in cloud object storage. They need to track exactly which dataset version each model was trained on for reproducibility, without duplicating the full 50GB dataset for every experiment. Which approach BEST meets this requirement?

A) Manually copy the full dataset into each experiment's local folder before training
B) Store the entire dataset directly inside the Git repository alongside the code
C) Use informal file naming conventions such as dataset_v1_final_v2.csv to track changes
D) Use a data versioning tool (e.g., DVC) that tracks lightweight metadata/hashes pointing to immutable dataset snapshots in object storage

---

**Q29.** A team deployed a fraud-detection model into production. Over three months, precision dropped from 0.92 to 0.71, but monitoring shows the input feature distributions have remained statistically stable compared to the training data. Which phenomenon BEST explains this degradation?

A) Data drift
B) Concept drift
C) Training-serving skew
D) Label leakage

---

**Q30.** Several independent data science teams at a company each write their own code to compute customer lifetime value from raw transaction data for their respective models. This has led to duplicated logic, inconsistent feature definitions, and training-serving skew. Which MLOps component BEST solves this problem?

A) Feature store
B) Model registry
C) Data lake
D) Experiment tracking system

---

**Q31.** A team wants to release a new model version to production while limiting the blast radius of any errors. They plan to route only 5% of live traffic to the new version, monitor error rates and latency, and gradually increase traffic if metrics remain healthy. Which deployment strategy does this describe?

A) Blue-green deployment
B) Canary deployment
C) Shadow deployment
D) A/B testing

---

**Q32.** A data scientist needs to guarantee that a machine learning experiment's results can be exactly reproduced six months later by another team member. Which combination of artifacts is REQUIRED to achieve full reproducibility?

A) Code version, dataset version/snapshot, hyperparameters, and random seed
B) The final trained model file along with its reported accuracy metrics
C) A requirements.txt file listing the Python library versions used
D) The Docker image used to run the training job

---

**Q33.** A data scientist wants to test whether customer preference for product category (A, B, C) is independent of the marketing channel used to reach the customer (email, social media, search ads). Both variables are categorical. Which test should be used?

A) Two-sample t-test
B) One-way ANOVA
C) Pearson correlation coefficient
D) Chi-squared test of independence

---

**Q34.** A researcher wants to compare mean conversion rates across five different website designs (an A/B/C/D/E test) using continuous conversion rate data. Which approach best controls the family-wise error rate compared to running multiple pairwise tests?

A) Run 10 pairwise two-sample t-tests at alpha = 0.05
B) Chi-squared goodness-of-fit test
C) Bootstrap resampling of a single group's mean
D) One-way ANOVA followed by Tukey's HSD post-hoc test

---

**Q35.** A 95% confidence interval for a population mean is calculated as (10.2, 15.8). Which statement correctly interprets this frequentist confidence interval?

A) If the sampling process were repeated many times and a CI constructed each time, 95% of those intervals would contain the true population mean.
B) There is a 95% probability that the true population mean lies between 10.2 and 15.8.
C) 95% of the individual data values fall between 10.2 and 15.8.
D) The true population mean equals 13 with 95% certainty.

---

**Q36.** A data scientist is performing dimensionality reduction using PCA on a high-dimensional dataset. Which linear algebra concept determines the amount of variance explained by each principal component?

A) Determinant of the design matrix
B) Eigenvalues of the covariance matrix
C) Rank of the identity matrix
D) Trace of the Jacobian matrix

---

**Q37.** A data scientist has a sample of n = 15 observations drawn from a normally distributed population with unknown population standard deviation. She wants to construct a 95% confidence interval for the population mean. Which distribution and degrees of freedom should she use for the critical value?

A) Student's t-distribution with 14 degrees of freedom
B) Standard normal (z) distribution, z = 1.96
C) Student's t-distribution with 15 degrees of freedom
D) Chi-squared distribution with 14 degrees of freedom

---

**Q38.** A time series exhibits a clear upward trend and increasing variance over time. Before fitting an ARIMA model, which preprocessing step directly addresses non-stationarity in the mean?

A) Applying differencing (e.g., first-order differencing)
B) Applying a log transformation only
C) One-hot encoding the time index
D) Standardizing the series to z-scores

---

**Q39.** A data scientist is analyzing monthly retail sales data that shows a clear upward trend and increasing variance over time. Before fitting an ARIMA(p,d,q) model, they need to formally determine whether the series is stationary. Which method BEST accomplishes this?

A) Shapiro-Wilk test on the raw series values
B) Chi-squared test of independence between month and sales bin
C) Durbin-Watson test on the fitted model's residuals
D) Augmented Dickey-Fuller (ADF) test on the raw series

---

**Q40.** A data scientist computes a 95% confidence interval for a population mean using classical (frequentist) methods. A colleague computes a 95% credible interval for the same parameter using Bayesian methods with an informative prior on the same dataset. Which statement correctly distinguishes the interpretation of these two intervals?

A) The confidence interval requires specifying a prior distribution, while the credible interval does not need one
B) The credible interval is mathematically guaranteed to always be narrower than the equivalent confidence interval
C) They are computed differently but have identical probabilistic interpretations about the true parameter
D) The credible interval states there is a 95% probability the true parameter lies within it given the data and prior, whereas the confidence interval means 95% of such intervals constructed from repeated sampling would contain the true parameter — it makes no direct probability statement about this specific interval

---

**Q41.** An e-commerce platform launches a new product line with zero purchase history. The current recommendation engine relies on collaborative filtering built from a user-item interaction matrix, so the new products never appear in recommendations because there is no interaction data to leverage. Which approach BEST addresses this cold-start problem?

A) Implement a hybrid model that uses content-based features (product attributes, category, description) for new items while retaining collaborative filtering for items with sufficient interaction history
B) Increase the number of latent factors in the matrix factorization model
C) Apply k-means clustering to group users by demographic data only
D) Reduce the regularization parameter in the collaborative filtering objective function

---

**Q42.** A support team wants to automatically extract specific product names, dates, and monetary amounts from incoming customer tickets so they can be routed to downstream billing and inventory systems. Which NLP technique is BEST suited for this task?

A) Named entity recognition (NER)
B) Sentiment analysis
C) Topic modeling with Latent Dirichlet Allocation (LDA)
D) Standalone Word2Vec embeddings

---

**Q43.** During object detection post-processing, a model produces multiple overlapping bounding boxes for the same object. Non-maximum suppression (NMS) is applied with an IoU threshold configured at 0.9. What is the MOST LIKELY effect of this configuration?

A) Many overlapping duplicate boxes will be suppressed, potentially causing missed detections of nearby objects
B) The model's confidence threshold will automatically adjust to compensate for the IoU setting
C) Very few boxes will be suppressed, so duplicate detections of the same object are likely to remain in the final output
D) All boxes with any overlap below the threshold will be merged into a single averaged box

---

**Q44.** A manufacturing plant streams readings from 500 sensors per machine, sampled every second, and needs to detect anomalies in this high-dimensional, unlabeled time-series data without assuming a specific underlying data distribution. Which technique is BEST suited for this scenario?

A) One-class SVM with a linear kernel
B) Autoencoder-based reconstruction error thresholding
C) Z-score thresholding applied independently to each sensor
D) Simple linear regression fit per sensor

---

**Q45.** Which statement BEST describes the primary difference between content-based filtering and collaborative filtering in recommender systems?

A) Content-based filtering requires a large existing user base to function, while collaborative filtering works effectively with a single user
B) Collaborative filtering only works for text data, while content-based filtering only works for image data
C) Content-based filtering recommends items similar to those a user has liked, based on item attributes, while collaborative filtering recommends items based on patterns of behavior across many users
D) Content-based filtering cannot produce personalized recommendations, while collaborative filtering is inherently personalized

---

**Q46.** An operations team must schedule delivery routes for 200 trucks subject to nonlinear fuel-cost constraints, time-window restrictions, and discrete truck-assignment decision variables. The resulting objective function and constraint set are non-convex and non-differentiable in several regions. Which optimization approach is MOST appropriate?

A) A genetic algorithm (evolutionary optimization)
B) Standard linear programming using the simplex method
C) Ordinary least squares regression
D) Gradient descent with a fixed learning rate

---

