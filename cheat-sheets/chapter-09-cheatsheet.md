## Chapter 9: Probability Distributions & Hypothesis Testing

### Common Distributions
| Distribution | Data Type | Use Case |
|---|---|---|
| Normal | Continuous | Symmetric, bell-shaped data (heights, errors) |
| Binomial | Discrete | Fixed # trials, success/failure outcomes |
| Poisson | Discrete (count) | # events per fixed interval, constant rate |
| Exponential | Continuous | Time between independent events |

### Central Limit Theorem (CLT)
- Sample mean distribution → approaches Normal as n increases, regardless of population shape.
- Rule of thumb: **n ≥ 30** is 'large enough' on the exam.
- Enables use of normal-based inference (CI, t-tests) even on non-normal populations.

### Hypothesis Testing Framework
1. State **H0** (no effect/no difference) and **H1** (alternative).
2. Choose significance level **alpha** (default 0.05).
3. Compute test statistic → p-value.
4. **p < alpha** → reject H0. **p ≥ alpha** → fail to reject H0 (never 'accept' H0).

### Choosing the Right Test
| Test | Use When |
|---|---|
| t-test (independent) | Compare means of 2 unrelated groups |
| t-test (paired) | Compare means of same subjects, 2 conditions |
| ANOVA (one-way) | Compare means of 3+ independent groups |
| Chi-squared | Test association between 2 categorical variables |

### p-values and Confidence Intervals
- p-value = P(data this extreme | H0 true). NOT P(H0 true).
- 95% CI: over repeated sampling, 95% of such intervals contain the true parameter — not a probability statement about one specific interval.

### Type I vs Type II Errors
| Error | Definition | Symbol |
|---|---|---|
| Type I | Reject a TRUE H0 (false positive) | alpha |
| Type II | Fail to reject a FALSE H0 (false negative) | beta |

- **Tradeoff:** Lowering alpha → fewer Type I errors, but MORE Type II errors (all else equal).
- **Power = 1 - beta**: probability of correctly detecting a true effect. Increasing sample size raises power.

### Multiple Comparisons Correction
- Running k tests at alpha=0.05 uncorrected inflates family-wise error rate.
- **Bonferroni correction:** adjusted alpha = alpha / k (e.g., 0.05/20 = 0.0025).
- Conservative but simple; exam favors Bonferroni as the standard correction method.

### Exam Traps
- Confusing p-value with 'probability null is true'.
- Using multiple t-tests instead of ANOVA for 3+ groups (inflates Type I error).
- Applying chi-squared to continuous data instead of categorical counts.
- Forgetting that CLT applies to the sampling distribution of the mean, not raw data.
- Believing lower alpha is 'always better' — ignoring the Type II error tradeoff.
