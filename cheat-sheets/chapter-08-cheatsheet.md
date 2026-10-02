## Chapter 8 Cheat Sheet: MLOps Operations

### Drift Types
| Type | What Changes | Detection Signal | Exam Trap |
|---|---|---|---|
| Data drift | Input feature distribution P(X) | PSI, KS-test on features | Features look fine ≠ no concept drift |
| Concept drift | Relationship P(Y\|X) | Rising prediction error despite stable features | Confused with data drift constantly |

### Deployment Patterns
| Pattern | Real users see predictions? | Traffic shift | Primary use |
|---|---|---|---|
| Shadow | No | 100% mirrored, not served | Safe validation, zero risk |
| Canary | Yes | Gradual % increase (e.g. 5→25→50→100) | Progressive rollout with rollback trigger |
| Blue-green | Yes | Instant 100% cutover | Fast full switch + instant rollback |
| Champion-challenger | Yes (challenger gets a portion) | Parallel long-run comparison | Promotion decision based on metrics |

### Rollback Priority Order
1. Route traffic back to prior registry version (fastest, minutes)
2. Reduce canary % to 0 if mid-rollout
3. Retrain only if root cause is data/concept drift (slowest)

### MLOps Components
| Component | Role |
|---|---|
| Tracking server | Logs params, metrics, artifacts per run |
| Model registry | Versioned models + stage (Staging/Production/Archived) + lineage |
| Feature store | Versioned, reusable features for train/serve consistency |
| CI/CD/CT pipeline | Automates test → train → evaluate → gate → promote |

### Key MLflow-style Commands
```
mlflow.log_param("lr", 0.01)
mlflow.log_metric("accuracy", 0.94)
mlflow.register_model(model_uri, "fraud_model")
mlflow models serve -m "models:/fraud_model/Production"
```

### Production Monitoring Metrics (must track)
- Prediction distribution vs. training distribution (data drift)
- Ground-truth-based error/accuracy over time (concept drift, when labels available with delay)
- Latency (p50/p95/p99)
- Error/exception rate
- Feature null-rate / schema violations

### Drift Heuristic
PSI < 0.1 stable | 0.1–0.25 investigate | > 0.25 act (retrain/rollback)

### Promotion Gate (Champion-Challenger)
Challenger promoted only if it beats champion on the defined metric over the defined evaluation window — never based on elapsed time or version number alone.
