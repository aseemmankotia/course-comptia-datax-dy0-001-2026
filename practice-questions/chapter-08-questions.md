## Chapter 8: MLOps: Experiment Tracking, Deployment, and Drift Monitoring — Practice Questions

**Q1.** A fraud-detection model's precision has dropped 15% over three months. Investigation shows incoming transaction feature distributions (amount, merchant category, time-of-day) are statistically unchanged from training data, but the underlying fraud patterns customers exhibit have evolved. What is this an example of?

A) Data drift
B) Concept drift
C) Training-serving skew
D) Label leakage

<details>
<summary>Answer</summary>

**Correct: B**

Concept drift occurs when the statistical relationship between inputs and the target variable changes, even though the input feature distributions remain stable — exactly the case here.

**Why the others are wrong:**
- Data drift refers to a change in the input feature distributions themselves, which the scenario explicitly rules out.
- Training-serving skew describes a mismatch between how features are computed/processed in training versus serving pipelines, not a shift over time in real-world relationships.
- Label leakage means a feature contains information from the target that shouldn't be available at prediction time — unrelated to performance degrading over time.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A team wants to validate a new model version against live production traffic without any risk of the new model's predictions being returned to end users or affecting business outcomes. Which deployment pattern should they use?

A) Shadow deployment
B) Canary deployment
C) Blue-green deployment
D) Champion-challenger with weighted routing

<details>
<summary>Answer</summary>

**Correct: A**

Shadow deployment mirrors live production requests to the new model in parallel, logging its predictions for comparison, but never serves those predictions to real users — zero user-facing risk.

**Why the others are wrong:**
- Canary deployment routes a real (small) percentage of live traffic to the new model and its predictions ARE served to those users — there is real exposure.
- Blue-green deployment switches all traffic at once between two environments; it doesn't provide a no-risk parallel evaluation phase.
- Champion-challenger with weighted routing still serves the challenger's predictions to a portion of real users, unlike shadow mode.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A team deploys a new model version to 5% of production traffic, monitors error rate and latency for 24 hours, and plans to progressively increase traffic to 25%, 50%, then 100% if metrics stay healthy. This describes which deployment pattern?

A) Shadow deployment
B) Canary deployment
C) Recreate deployment
D) Champion-challenger evaluation

<details>
<summary>Answer</summary>

**Correct: B**

Canary deployment gradually shifts a real, increasing percentage of live traffic to the new version while monitoring health metrics before full rollout — matching the scenario exactly.

**Why the others are wrong:**
- Shadow deployment does not serve any predictions to real users; this scenario explicitly serves predictions to a growing percentage of traffic.
- Recreate deployment tears down the old version entirely and replaces it in one step, with no gradual traffic ramp.
- Champion-challenger evaluation is a longer-term parallel comparison strategy for promotion decisions, not specifically defined by percentage-based traffic ramping.

</details>

---

**Q4.** Which MLOps component is responsible for storing versioned model artifacts along with stage metadata (e.g., Staging, Production, Archived) and lineage back to the training run that produced them?

A) Experiment tracking server
B) Feature store
C) Artifact repository for container images
D) Model registry

<details>
<summary>Answer</summary>

**Correct: D**

A model registry centralizes versioned models, tracks their lifecycle stage, and links each version back to its originating experiment run — the core mechanism enabling rollback and champion-challenger workflows.

**Why the others are wrong:**
- The experiment tracking server logs parameters, metrics, and artifacts per run but does not manage model lifecycle stages across versions.
- A feature store manages reusable, versioned feature data for training and serving — not model artifact versioning.
- A generic container image repository stores build artifacts but has no concept of model stage transitions or training lineage.

</details>

---

**Q5.** In an MLflow-style tracking workflow, which component logs parameters, metrics, and artifacts for each individual training run so they can be compared later?

A) Model Registry
B) Projects component
C) Tracking component
D) Model Serving component

<details>
<summary>Answer</summary>

**Correct: C**

The Tracking component records hyperparameters, evaluation metrics, and output artifacts for each run, enabling side-by-side experiment comparison.

**Why the others are wrong:**
- The Model Registry manages versioned, promoted models — it consumes tracking data but doesn't itself log per-run parameters/metrics.
- The Projects component packages code for reproducible runs (e.g., defining entry points and environments), not logging results.
- The Model Serving component exposes a registered model as an inference endpoint; it plays no role in experiment logging.

</details>

---

**Q6.** A newly promoted model version begins returning degraded predictions in production within an hour of full rollout. The team needs to restore service immediately. What is the correct rollback action?

A) Trigger a full retraining job and redeploy once complete
B) Route traffic back to the previous version pinned in the model registry
C) Increase the canary traffic percentage to gather more data before deciding
D) Manually patch the current model's weights in production

<details>
<summary>Answer</summary>

**Correct: B**

Because the model registry keeps prior versions available with their stage history, the fastest and safest rollback is repointing the serving endpoint/traffic router to the last known-good registered version.

**Why the others are wrong:**
- Retraining takes hours to days and does nothing to resolve an active production incident right now.
- Increasing canary traffic to a degraded model worsens the incident rather than resolving it.
- Manually patching weights in production is not a repeatable, auditable practice and violates version control principles central to MLOps.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** In a champion-challenger deployment strategy, what determines whether the challenger is promoted to become the new champion?

A) The challenger has been running for at least 24 hours regardless of results
B) The challenger consumes fewer compute resources than the champion
C) The challenger has a numerically higher version identifier
D) The challenger meets or exceeds a predefined performance threshold over a defined evaluation window

<details>
<summary>Answer</summary>

**Correct: D**

Promotion decisions in champion-challenger setups are based on statistically evaluating the challenger's business/performance metrics against the champion over a defined window, not arbitrary time or naming rules.

**Why the others are wrong:**
- Elapsed time alone provides no evidence of performance and is not a valid promotion criterion.
- Compute efficiency may be a secondary factor but is not the primary promotion gate — predictive performance is.
- Version numbering is an artifact of the registry and has no bearing on model quality or promotion decisions.

</details>

---

**Q8.** What is the fundamental distinction between data drift and concept drift?

A) Data drift is a change in the distribution of input features; concept drift is a change in the relationship between inputs and the target variable
B) They are two names for the same phenomenon and are used interchangeably on the exam
C) Concept drift can only be detected in shadow deployments, while data drift can only be detected in canary deployments
D) Data drift affects only regression models, while concept drift affects only classification models

<details>
<summary>Answer</summary>

**Correct: A**

Data drift = P(X) changes (input feature distribution shifts). Concept drift = P(Y|X) changes (the mapping from inputs to target shifts), even if input distributions stay stable.

**Why the others are wrong:**
- They are distinct phenomena tested separately on the exam and require different detection and mitigation strategies.
- Both types of drift can be detected regardless of deployment pattern used — detection method is independent of rollout strategy.
- Both drift types can occur in either regression or classification problems; the distinction has nothing to do with model task type.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

