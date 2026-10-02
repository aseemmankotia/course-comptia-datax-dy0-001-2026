## Chapter 6 Cheat Sheet — Deep Learning, Regularization, Bias-Variance

### Bias-Variance Diagnosis via Learning Curves
| Pattern | Diagnosis | Fix |
|---|---|---|
| Train low, Val high, large gap | High Variance (overfit) | Dropout, L2/weight decay, more data, simplify model |
| Train high, Val high, curves converge | High Bias (underfit) | Increase capacity, better features, train longer |
| Both low, small gap | Good fit | Deploy |

### Architecture Selection
| Data Type | Best Architecture | Why |
|---|---|---|
| Images / spatial grids | CNN | Convolution + pooling capture local spatial patterns |
| Sequential, short/medium dependencies | RNN/LSTM | Sequential processing, gating handles vanishing gradients |
| Long-range dependencies, parallel training | Transformer | Self-attention relates all tokens directly; parallelizable |
| Small tabular datasets | Classical ML (GBM/RF) | Less data needed, interpretable, faster to train |

### Regularization Techniques
| Technique | What it does | Typical Value |
|---|---|---|
| Dropout | Randomly zeroes activations during training | 0.2–0.5 (FC layers) |
| Batch Normalization | Normalizes activations per mini-batch | N/A — applied per layer |
| Early Stopping | Halts training when val metric stops improving | Patience = N epochs (problem-specific) |
| L2 / Weight Decay | Penalizes large weights | Small coefficient, e.g., 1e-4–1e-2 |

### Hyperparameter Tuning Methods
| Method | Approach | Best When |
|---|---|---|
| Grid Search | Exhaustive over all combos | Small search space, cheap trials |
| Random Search | Random sampling of combos | Larger space, more efficient than grid |
| Bayesian Optimization | Probabilistic model guides next trial | Expensive trials, limited budget |

### Exam Notes
- Learning curve shape is the #1 tested bias-variance signal — memorize gap vs plateau patterns.
- CNN = spatial, RNN/LSTM = sequential (slow, sequential processing), Transformer = long-range + parallel.
- Dropout only active during training, disabled at inference.
- Batch norm reduces internal covariate shift — commonly confused with dropout on the exam.
- Bayesian optimization is the answer whenever the scenario says 'expensive training' + 'limited trials'.
- Classical ML often the correct answer for small tabular datasets — don't default to deep learning.
