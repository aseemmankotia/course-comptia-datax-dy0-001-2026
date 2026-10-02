## Model Evaluation, Iteration & Communicating Outcomes

### Metric Formulas
| Metric | Formula | Use When |
|---|---|---|
| Precision | TP/(TP+FP) | False positives are costly |
| Recall | TP/(TP+FN) | False negatives are costly |
| F1 | 2·(P·R)/(P+R) | Need balance of P & R |
| ROC-AUC | Area under TPR vs FPR | Balanced classes |
| PR-AUC | Area under Precision vs Recall | Imbalanced/rare positive class |

### ROC-AUC vs PR-AUC
| Scenario | Prefer |
|---|---|
| Balanced classes (~50/50) | ROC-AUC |
| Rare positive class (fraud, disease, churn) | PR-AUC |
| Communicating to non-technical stakeholders | Precision/Recall at chosen threshold |

### Cross-Validation Strategy Selection
| Data Type | Strategy | Why |
|---|---|---|
| i.i.d., balanced classes | K-fold | Simple, unbiased |
| i.i.d., imbalanced classes | Stratified k-fold | Preserves class ratio per fold |
| Temporally ordered (forecasting, sensor logs) | Time-series split | Prevents future data leakage |
| Very small dataset | Leave-one-out | Maximizes training data per fold (costly) |

### Confusion Matrix Cheat
```
              Predicted +   Predicted -
Actual +         TP            FN
Actual -         FP            TN
```
Precision ↓ with more FP. Recall ↓ with more FN.

### Calibration
- Calibration curve diagonal = perfect calibration.
- Above diagonal = under-confident; below = over-confident.
- Fix: Platt scaling (small data, monotonic) or isotonic regression (larger data, flexible).
- Calibration ≠ discrimination — a model can have high AUC but be poorly calibrated.

### Iterative Refinement Loop
1. Baseline → 2. Error analysis (confusion matrix, misclassifications) → 3. Adjust features/data → 4. Retrain → 5. Re-validate with SAME CV strategy → 6. Compare to baseline.
Exam trap: changing CV strategy between iterations invalidates comparisons.

### Statistical vs Business Significance
| Concept | Measures | Exam Trap |
|---|---|---|
| Statistical significance | Is the effect real (p-value, CI)? | Large samples make tiny effects 'significant' |
| Business significance | Does the effect size justify cost/action? | Always tie metric deltas to revenue/cost/risk before recommending deployment |

### A/B Testing Production Models
- Random assignment to control/treatment.
- One predefined business metric (not multiple, post-hoc chosen).
- Pre-calculated sample size/duration; no early peeking.
- Apply significance test (t-test/chi-square) before deciding rollout.

### Stakeholder Communication Rule
Translate metrics into cost/revenue/risk terms, not raw statistics. Example: 'A 2% recall increase catches an estimated 400 additional fraud cases/month, saving ~$120K.' Avoid presenting AUC or F1 alone to non-technical audiences.
