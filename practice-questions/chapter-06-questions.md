## Chapter 6: Deep Learning Architectures, Regularization, and Bias-Variance Tradeoff — Practice Questions

**Q1.** A model achieves 98% accuracy on the training set but only 76% on the validation set, and the gap does not close as training continues. Which learning curve diagnosis and fix BEST addresses this?

A) High variance — apply dropout, add L2 regularization, or gather more training data
B) High bias — add more layers and train longer
C) High bias — reduce model capacity and stop training early
D) The model is optimal — deploy as-is since training accuracy is high

<details>
<summary>Answer</summary>

**Correct: A**

A large, persistent gap between low training error and high validation error is the signature of high variance (overfitting). Dropout, L2/weight decay, and more training data are the standard remedies.

**Why the others are wrong:**
- Adding more layers increases capacity, which worsens overfitting rather than fixing it.
- Reducing capacity may help, but 'stop training early' alone doesn't address the root cause the way regularization does, and this option mislabels the problem as high bias.
- A 22-point accuracy gap is a textbook overfitting signal, not an optimal model.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Both training and validation error plateau at 35% error and stay close together (within 2%) even after adding more training data. What does this pattern indicate?

A) High variance — add dropout and batch normalization
B) Data leakage — audit the train/test split
C) High bias — increase model complexity or add more informative features
D) The model has converged optimally and no changes are needed

<details>
<summary>Answer</summary>

**Correct: C**

Converged, high, and close training/validation error curves indicate underfitting (high bias). The fix is increasing model capacity (deeper network, more features) rather than adding data, since more data does not help high-bias models.

**Why the others are wrong:**
- High variance shows a large gap between curves, not convergence to a high error plateau.
- Data leakage typically causes suspiciously LOW error, not high error.
- A 35% error plateau on both curves indicates underfitting, not convergence to an acceptable solution.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A company needs to classify high-resolution medical images (X-rays) into disease categories, leveraging spatial patterns like edges and textures. Which architecture BEST fits this requirement?

A) Recurrent Neural Network (RNN) with LSTM cells
B) Convolutional Neural Network (CNN) with convolution and pooling layers
C) A vanilla fully-connected feedforward network
D) A decision tree ensemble (e.g., random forest)

<details>
<summary>Answer</summary>

**Correct: B**

CNNs use convolutional filters to detect local spatial patterns (edges, textures) and pooling to reduce dimensionality while preserving key features — the standard choice for image classification.

**Why the others are wrong:**
- LSTMs are designed for sequential/temporal data, not spatial image data.
- A fully-connected network ignores spatial locality and requires far more parameters, performing worse on images.
- Tree ensembles do not scale well to raw high-resolution pixel data and can't learn spatial hierarchies.

</details>

---

**Q4.** An NLP team needs a model that captures long-range dependencies across a 2,000-token document and must train efficiently in parallel on GPUs. Which architecture BEST meets these requirements?

A) A vanilla RNN processing tokens sequentially
B) An LSTM with a large hidden state
C) A Transformer using self-attention
D) A 1D CNN with small kernel sizes

<details>
<summary>Answer</summary>

**Correct: C**

Transformers use self-attention to relate any two tokens directly regardless of distance, and process all tokens in parallel during training, making them superior for long sequences and GPU efficiency.

**Why the others are wrong:**
- Vanilla RNNs process sequentially (no parallelism) and suffer from vanishing gradients over long sequences.
- LSTMs mitigate vanishing gradients but still process sequentially and struggle with very long-range dependencies compared to attention.
- 1D CNNs with small kernels have a limited receptive field and require many stacked layers to capture long-range context.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** During hyperparameter tuning of a deep learning model, dropout rate for fully-connected layers is typically set within which range in most exam scenarios?

A) 0.01–0.05
B) 0.2–0.5
C) 0.7–0.9
D) 1.0 (always drop all units)

<details>
<summary>Answer</summary>

**Correct: B**

A dropout rate of 0.2–0.5 is the standard range for fully-connected layers, balancing regularization strength with retained model capacity.

**Why the others are wrong:**
- 0.01–0.05 is too low to provide meaningful regularization.
- 0.7–0.9 is unusually aggressive and typically destroys too much signal, hurting convergence.
- A dropout rate of 1.0 would drop every unit, making the layer output all zeros — not a valid configuration.

</details>

---

**Q6.** A team has an expensive-to-train deep learning model and only enough compute budget for ~20 hyperparameter trials. Which tuning strategy is MOST appropriate?

A) Bayesian optimization, which models past trial results to select the next most promising configuration
B) Exhaustive grid search over all hyperparameter combinations
C) Random search only
D) Manual tuning based on intuition alone

<details>
<summary>Answer</summary>

**Correct: A**

Bayesian optimization builds a probabilistic surrogate model (e.g., Gaussian process) from prior trial results to intelligently choose the next hyperparameters, making it the most sample-efficient choice when trials are expensive and limited.

**Why the others are wrong:**
- Grid search requires evaluating every combination, which is computationally infeasible at 20 trials for anything but a tiny search space.
- Random search is more efficient than grid search but does not use past results to guide future trials, making it less efficient than Bayesian optimization under a tight budget.
- Manual tuning does not scale reliably and lacks a systematic method for exploring the search space.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** What is the primary purpose of batch normalization in a deep neural network?

A) To randomly deactivate neurons during training to prevent co-adaptation
B) To normalize layer activations to stabilize distributions across mini-batches, enabling higher learning rates and faster convergence
C) To reduce the number of trainable parameters in the network
D) To stop training automatically once validation loss stops improving

<details>
<summary>Answer</summary>

**Correct: B**

Batch normalization normalizes the activations of a layer (typically to zero mean, unit variance) per mini-batch, reducing internal covariate shift and allowing higher learning rates and faster, more stable training.

**Why the others are wrong:**
- That describes dropout, a different regularization technique.
- Batch norm adds a small number of learnable scale/shift parameters per layer; it does not reduce overall parameter count.
- That describes early stopping, not batch normalization.

</details>

---

**Q8.** A company has a tabular dataset with 5,000 rows and 20 numeric features and needs a fast, interpretable model for a regulated industry. Which approach BEST fits these requirements?

A) A gradient-boosted tree or random forest (classical ML)
B) A deep Transformer model trained from scratch
C) A 10-layer CNN with dropout and batch normalization
D) An LSTM with attention mechanism

<details>
<summary>Answer</summary>

**Correct: A**

For small tabular datasets requiring interpretability and fast training, classical ML methods like gradient-boosted trees or random forests typically outperform deep learning, which needs large data volumes to justify its complexity and is harder to interpret.

**Why the others are wrong:**
- Transformers require large datasets to train effectively and offer poor interpretability, making them a poor fit here.
- CNNs are designed for spatial data (e.g., images), not tabular numeric features, and add unnecessary complexity for only 5,000 rows.
- LSTMs are for sequential data; tabular features are not inherently sequential, and this adds unneeded complexity and reduced interpretability.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

