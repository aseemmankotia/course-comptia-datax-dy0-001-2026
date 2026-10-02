## Chapter 6: Deep Learning Architectures, Regularization, and Bias-Variance Tradeoff — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | Learning curve: low training error, high validation error, large persistent gap — diagnosis? | High variance (overfitting). Fix: dropout, L2 regularization, more training data, or reduce model complexity. Exam tip: gap size = variance signal. |
| 2 | Learning curve: training and validation error both high and converge to a plateau — diagnosis? | High bias (underfitting). Fix: increase model capacity or add better features — more data will NOT help. Exam tip: closeness of curves + high error = bias signal. |
| 3 | CNN core building blocks tested on the exam? | Convolution (learns spatial filters/feature maps) and pooling (max/average, reduces spatial dimensions, adds translation invariance). Best fit for image/spatial data. |
| 4 | CNN vs RNN vs Transformer — when to choose each? | CNN: spatial/grid data (images). RNN/LSTM: sequential data with short-to-medium dependencies, sequential processing. Transformer: long-range dependencies, needs parallel training, dominant for NLP and increasingly vision (ViT). |
| 5 | Why do Transformers train faster than RNNs on GPUs? | Self-attention processes all tokens in parallel; RNNs process tokens sequentially (one timestep depends on the previous), preventing parallelization. |
| 6 | LSTM vs vanilla RNN — key difference? | LSTM uses gating (input, forget, output gates) to control information flow, mitigating the vanishing gradient problem that limits vanilla RNNs on long sequences. |
| 7 | Typical dropout rate range for fully-connected layers? | 0.2–0.5. Exam tip: dropout randomly zeroes activations during training only (not at inference) to reduce co-adaptation and overfitting. |
| 8 | What does batch normalization normalize, and why? | Normalizes layer activations to ~zero mean/unit variance per mini-batch. Reduces internal covariate shift, allows higher learning rates, speeds convergence. |
| 9 | Early stopping — what does it monitor and when does it stop? | Monitors validation loss/metric; stops training when no improvement is seen for a set number of epochs (patience). Prevents overfitting without needing extra regularization. |
| 10 | Grid search vs Random search vs Bayesian optimization? | Grid: exhaustive, expensive, thorough for small spaces. Random: samples randomly, more efficient than grid for large spaces. Bayesian: uses prior trial results (e.g., Gaussian process) to pick next promising hyperparameters — most sample-efficient for expensive training runs. |
| 11 | When should you prefer classical ML over deep learning? | Small datasets (thousands of rows), tabular data, need for interpretability/regulatory compliance, or limited compute — gradient-boosted trees/random forests typically outperform DL here. |
| 12 | Bias-variance tradeoff — one-line summary | High bias = underfitting (both errors high & close). High variance = overfitting (train error low, val error high, large gap). Total error = bias² + variance + irreducible error. |
