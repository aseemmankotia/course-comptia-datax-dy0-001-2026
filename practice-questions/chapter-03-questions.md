## Chapter 3: Model Evaluation, Iteration, and Communicating Outcomes — Practice Questions

**Q1.** A fraud detection model classifies transactions where only 0.4% are fraudulent. The model achieves a ROC-AUC of 0.97, but stakeholders report it misses most real fraud cases in production. Which metric should have been prioritized during model selection?

A) PR-AUC, since it focuses on performance for the minority (positive) class
B) ROC-AUC, since it is threshold-independent
C) Overall accuracy, since it reflects total correct predictions
D) Specificity, since it measures true negative rate

<details>
<summary>Answer</summary>

**Correct: A**

With severe class imbalance, the negative class dominates ROC-AUC calculations, inflating the score even when the model performs poorly on the rare positive class. PR-AUC evaluates precision/recall tradeoffs specifically on the positive class, exposing weak fraud detection.

**Why the others are wrong:**
- ROC-AUC includes true negative rate in its calculation, which stays high just from correctly predicting the abundant negative class, masking poor recall on fraud.
- Accuracy is misleading here — predicting 'not fraud' for everything yields 99.6% accuracy while catching zero fraud.
- Specificity only measures negative class performance and says nothing about missed fraud (false negatives).

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A team is building a model to forecast next-quarter sales using 5 years of monthly historical data. Which cross-validation strategy is appropriate?

A) Time-series split (walk-forward validation)
B) Standard k-fold cross-validation with shuffling
C) Stratified k-fold cross-validation
D) Leave-one-out cross-validation

<details>
<summary>Answer</summary>

**Correct: A**

Time-series split trains only on past data and validates on future data in sequential folds, preventing the model from 'seeing the future' — essential for temporally ordered data.

**Why the others are wrong:**
- Standard k-fold shuffles data randomly, allowing future data points into training folds, causing data leakage and overly optimistic validation scores.
- Stratified k-fold preserves class distribution across folds but still shuffles temporal order, causing the same leakage problem.
- Leave-one-out is computationally expensive and still ignores temporal ordering, allowing leakage from future periods.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A retrained model shows a statistically significant improvement in AUC (p < 0.01) over the production model, increasing AUC from 0.812 to 0.816. Leadership asks whether to replace the production model. What is the BEST response?

A) Evaluate whether the 0.004 AUC gain translates into a meaningful business metric (e.g., revenue, cost savings) before deciding
B) Deploy immediately since statistical significance confirms the model is better
C) Reject the new model since the AUC difference is too small to matter
D) Rerun the test with a larger sample size until the p-value drops further

<details>
<summary>Answer</summary>

**Correct: A**

Statistical significance only confirms the difference is unlikely due to chance — it does not confirm the difference is large enough to matter for the business. The decision should be based on projected business impact (e.g., dollars saved, conversion lift), not the p-value alone.

**Why the others are wrong:**
- Statistical significance with a large sample can detect trivially small differences; deploying without assessing business impact risks unnecessary operational cost with no real gain.
- Dismissing the result outright ignores that small AUC gains can sometimes translate to meaningful gains at scale — this must be checked, not assumed.
- A larger sample size will only make an already-significant result more significant; it does not address whether the effect size matters practically.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A binary classification dataset has a 90/10 class split. Which cross-validation configuration best preserves reliable per-fold evaluation?

A) K-fold cross-validation with k=5 and random shuffling
B) Time-series split with 5 sequential folds
C) A single 50/50 train-test split
D) Stratified k-fold cross-validation, preserving the 90/10 ratio in each fold

<details>
<summary>Answer</summary>

**Correct: D**

Stratified k-fold ensures each fold maintains the original class proportions, preventing folds where the minority class is nearly or entirely absent, which would make metrics like recall unstable or undefined.

**Why the others are wrong:**
- Plain k-fold with random shuffling can produce folds with very few or zero minority-class samples, causing unstable precision/recall estimates.
- Time-series split is designed for temporally ordered data, not for addressing class imbalance in i.i.d. tabular data.
- A single split gives one noisy estimate and doesn't leverage the full dataset for validation, increasing variance in the reported metric.

</details>

---

**Q5.** A model's calibration curve shows predicted probabilities of 0.9 correspond to an observed positive rate of only 0.6 — the model is overconfident. Which technique directly addresses this issue without retraining the base model?

A) Increase the classification threshold from 0.5 to 0.9
B) Apply post-hoc calibration such as Platt scaling or isotonic regression
C) Switch the evaluation metric from PR-AUC to ROC-AUC
D) Add more features to the training data

<details>
<summary>Answer</summary>

**Correct: B**

Platt scaling (logistic) or isotonic regression are post-hoc calibration methods that remap raw model outputs to better-calibrated probabilities using a held-out calibration set, without changing or retraining the underlying model.

**Why the others are wrong:**
- Changing the decision threshold affects classification cutoffs but does not fix the underlying probability miscalibration.
- Switching the evaluation metric doesn't change the model's probability outputs — calibration and discrimination (AUC) are separate concerns.
- Adding features requires retraining and doesn't guarantee calibration improves; calibration is a distinct post-processing step.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A confusion matrix shows: TP=80, FP=20, FN=40, TN=860. What is the model's recall (rounded to two decimals)?

A) 0.80
B) 0.98
C) 0.29
D) 0.67

<details>
<summary>Answer</summary>

**Correct: D**

Recall = TP / (TP + FN) = 80 / (80 + 40) = 80/120 = 0.67.

**Why the others are wrong:**
- 0.80 is the precision value (TP / (TP+FP) = 80/100), commonly confused with recall.
- 0.98 approximates specificity (TN / (TN+FP) = 860/880), not recall.
- 0.29 comes from incorrectly dividing FN by total positives predicted instead of using the correct recall formula.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A company wants to A/B test a new recommendation model against the current production model before a full rollout. Which approach is MOST appropriate for validating the business impact?

A) Compare offline PR-AUC scores from historical logs and deploy whichever is higher
B) Randomly assign live users to control (current model) and treatment (new model) groups and compare a predefined business metric with a significance test
C) Deploy the new model to 100% of traffic and monitor dashboards for one week
D) Ask a small internal team to manually review sample outputs from both models

<details>
<summary>Answer</summary>

**Correct: B**

A proper online A/B test uses random assignment to control and treatment groups, isolates the model as the only variable, and applies a significance test on a predefined business metric (e.g., click-through rate, conversion) to validate real-world impact before full rollout.

**Why the others are wrong:**
- Offline metrics like PR-AUC don't capture real user behavior, feedback loops, or downstream business effects.
- Full deployment without a control group makes it impossible to isolate the new model's effect from external factors like seasonality.
- Manual review of samples is subjective, not statistically rigorous, and doesn't scale to detect real business impact.

</details>

---

**Q8.** Which statement BEST describes the difference between statistical significance and business significance?

A) They are the same concept — a statistically significant result is always business significant
B) Business significance is measured using p-values, while statistical significance is measured using revenue impact
C) Statistical significance indicates an observed effect is unlikely due to random chance; business significance indicates the effect size is large enough to justify action or cost
D) Statistical significance only applies to A/B tests, while business significance only applies to offline model evaluation

<details>
<summary>Answer</summary>

**Correct: C**

Statistical significance is about confidence that an effect is real (not noise), typically via p-values or confidence intervals. Business significance is about whether the magnitude of that effect matters enough to justify the cost of deployment or change — the two are independent considerations.

**Why the others are wrong:**
- A result can be statistically significant with a large sample size yet have a tiny, practically irrelevant effect size — they are not the same.
- This reverses the definitions; p-values measure statistical significance, and revenue/cost impact measures business significance.
- Both concepts apply broadly to any evaluation context, online or offline — they are not restricted to specific testing methods.

</details>

---

