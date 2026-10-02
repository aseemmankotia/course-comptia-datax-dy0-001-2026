## Chapter 8: MLOps: Experiment Tracking, Deployment, and Drift Monitoring — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Data drift vs. concept drift — one-line distinction? | Data drift = input feature distribution P(X) changes. Concept drift = relationship between inputs and target P(Y\|X) changes. Exam trap: features looking 'normal' does NOT rule out concept drift. |
| 2 | Canary deployment — key traffic characteristic? | Real users ARE served predictions from the new model, starting with a small % (e.g., 5%) and ramping up gradually while monitoring health metrics. |
| 3 | Shadow deployment — key traffic characteristic? | New model receives mirrored copies of live traffic and its predictions are logged for comparison, but NEVER served to real users. Zero user-facing risk. |
| 4 | Champion-challenger pattern — purpose? | Runs current production model (champion) alongside candidate model(s) (challenger) in parallel to compare performance over a defined evaluation window before promotion. |
| 5 | Blue-green deployment — how does it differ from canary? | Blue-green switches ALL traffic at once from old (blue) to new (green) environment. Canary shifts traffic gradually in increments. Blue-green enables instant full rollback by switching router back. |
| 6 | Model Registry vs. Experiment Tracking Server — what's the difference? | Tracking server logs per-run params/metrics/artifacts for comparison. Model registry manages promoted, versioned models with lifecycle stages (Staging/Production/Archived) and lineage to the originating run. |
| 7 | MLflow: log a metric during a training run | mlflow.log_metric("accuracy", 0.94) — logged under the active run; queryable/comparable later in the Tracking UI. |
| 8 | MLflow: register a trained model to the registry | mlflow.register_model(model_uri, "model_name") — creates a new version entry in the Model Registry linked to the source run. |
| 9 | MLflow: serve a registered model as a REST endpoint | mlflow models serve -m "models:/model_name/Production" — deploys the version currently tagged 'Production' as a local inference server. |
| 10 | Population Stability Index (PSI) — drift detection heuristic thresholds | PSI < 0.1: no significant shift. 0.1–0.25: moderate shift, investigate. > 0.25: significant drift, retrain/rollback likely needed. Common industry heuristic for detecting data drift. |
| 11 | Rollback strategy — fastest recovery mechanism after a bad model promotion? | Repoint serving traffic/router to the previous version pinned in the model registry. Avoids retraining delay; relies on registry keeping prior versions available and deployable. |
| 12 | CI/CD for ML — what's added beyond traditional software CI/CD? | Traditional CI/CD validates code + tests. ML CI/CD (sometimes 'CI/CD/CT' — Continuous Training) also validates data quality, retrains/evaluates model performance against a baseline, and gates promotion on metric thresholds, not just passing unit tests. |
