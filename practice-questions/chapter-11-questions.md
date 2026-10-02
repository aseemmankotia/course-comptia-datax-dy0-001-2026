## Chapter 11: Optimization Methods, NLP, and Computer Vision Applications — Practice Questions

**Q1.** A model training run uses plain SGD with a fixed learning rate of 0.1 and the loss oscillates wildly without converging on a non-convex deep network. Which change BEST addresses this while keeping training simple?

A) Increase the learning rate to 0.5 to escape the oscillation faster
B) Switch to SGD with momentum (e.g., 0.9) to smooth updates using an exponentially weighted average of past gradients
C) Switch to full-batch gradient descent to eliminate noise entirely
D) Remove the loss function's regularization term

<details>
<summary>Answer</summary>

**Correct: B**

Momentum accumulates a moving average of gradients, dampening oscillations across steep dimensions while accelerating progress along shallow, consistent-gradient directions — the standard fix for oscillating SGD.

**Why the others are wrong:**
- Raising the learning rate further amplifies oscillation instead of reducing it.
- Full-batch gradient descent is computationally impractical at scale and doesn't specifically fix oscillation caused by learning rate/curvature issues.
- Regularization is unrelated to oscillation from step size and gradient noise.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Which optimizer maintains per-parameter adaptive learning rates using estimates of both the first moment (mean) and second moment (uncentered variance) of the gradients?

A) Vanilla SGD
B) SGD with momentum
C) Adam
D) Batch gradient descent

<details>
<summary>Answer</summary>

**Correct: C**

Adam combines momentum (first moment, default beta1=0.9) with RMSProp-like scaling by the second moment (default beta2=0.999), giving each parameter its own adaptive learning rate.

**Why the others are wrong:**
- Vanilla SGD uses a single fixed learning rate applied uniformly with no moment estimates.
- SGD with momentum tracks only the first moment, not the second.
- Batch gradient descent just refers to using the full dataset per update; it has no adaptive rate mechanism.

</details>

---

**Q3.** A function has a single global minimum and any local minimum found is guaranteed to also be the global minimum. This describes which property?

A) Non-convex optimization
B) Convex optimization
C) Stochastic optimization
D) Gradient explosion

<details>
<summary>Answer</summary>

**Correct: B**

Convex functions have a bowl shape with one global minimum, so any local minimum is the global minimum — this is why linear/logistic regression training is convex and reliably converges.

**Why the others are wrong:**
- Non-convex functions (typical of deep neural networks) can have multiple local minima and saddle points, the opposite of this description.
- Stochastic optimization refers to using random mini-batches, not the shape of the loss surface.
- Gradient explosion refers to gradients growing uncontrollably large during backpropagation, unrelated to convexity.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A team is building an NLP pipeline and needs to convert raw text into subword units that can handle out-of-vocabulary words (e.g., splitting 'unhappiness' into 'un', 'happi', 'ness'). Which pipeline stage does this describe?

A) Tokenization (subword/BPE-style)
B) Embedding lookup
C) Attention scoring
D) Positional encoding

<details>
<summary>Answer</summary>

**Correct: A**

Tokenization is the first NLP pipeline step that segments raw text into tokens; subword methods like Byte Pair Encoding (BPE) or WordPiece handle rare/unknown words by breaking them into known sub-units.

**Why the others are wrong:**
- Embedding lookup maps tokens (already produced) to dense vectors — it happens after tokenization.
- Attention scoring computes relevance weights between tokens inside a transformer, not text splitting.
- Positional encoding injects sequence order information into embeddings; it doesn't split words.

</details>

---

**Q5.** A company needs to classify medical X-ray images but only has 800 labeled images — far too few to train a deep CNN from scratch. Which approach BEST meets this requirement?

A) Train a large CNN from random initialization for many epochs on the 800 images
B) Use a fully connected network with no convolutional layers to reduce parameters
C) Use transfer learning: take a pretrained CNN (e.g., trained on ImageNet), freeze early convolutional layers, and fine-tune later layers on the X-ray dataset
D) Switch to unsupervised clustering since labeled data is insufficient

<details>
<summary>Answer</summary>

**Correct: C**

Transfer learning reuses low-level features (edges, textures) learned from large datasets and fine-tunes higher layers on the small target dataset, drastically reducing the data needed and avoiding overfitting.

**Why the others are wrong:**
- Training a deep CNN from scratch on only 800 images will overfit badly and underperform.
- Removing convolutional layers discards spatial feature extraction critical for image tasks and doesn't solve the small-data problem.
- Unsupervised clustering discards the labels the company already has and doesn't produce a classifier matching the labeling task.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** In a convolutional neural network, what is the primary purpose of the convolution operation applied via learned filters/kernels?

A) To reduce the number of training epochs required
B) To normalize pixel values to a 0-1 range
C) To extract local spatial features such as edges and textures by sliding filters across the input
D) To assign class probabilities at the output layer

<details>
<summary>Answer</summary>

**Correct: C**

Convolutional layers slide small learnable filters over the input to detect local patterns (edges, textures, shapes), building a hierarchy of spatial features layer by layer.

**Why the others are wrong:**
- Convolution doesn't directly control epoch count — that's a training hyperparameter unrelated to the operation itself.
- Pixel normalization is a preprocessing step, not the function of convolution.
- Class probability assignment happens at the output layer (typically softmax), not in convolutional layers.

</details>

---

**Q7.** A team needs a model that outputs both the class label AND a bounding box location for multiple objects in a single image. Which task/architecture category BEST fits this requirement?

A) Object detection (e.g., YOLO or Faster R-CNN style architectures)
B) Image classification
C) Text summarization
D) Word embedding generation

<details>
<summary>Answer</summary>

**Correct: A**

Object detection architectures predict both class labels and bounding box coordinates (localization) for potentially multiple objects per image, unlike classification which outputs only one label per image.

**Why the others are wrong:**
- Image classification outputs a single label for the whole image with no location information.
- Text summarization is an NLP task unrelated to image bounding boxes.
- Word embedding generation produces vector representations of tokens, not image object locations.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which NLP component uses self-attention to let each token weigh the relevance of every other token in the sequence, enabling models like BERT and GPT to capture long-range dependencies?

A) Bag-of-words vectorization
B) Transformer architecture
C) TF-IDF weighting
D) Stemming

<details>
<summary>Answer</summary>

**Correct: B**

The transformer architecture's self-attention mechanism computes weighted relationships between all token pairs in a sequence in parallel, which is why transformers replaced RNNs for capturing long-range context.

**Why the others are wrong:**
- Bag-of-words ignores word order and relationships entirely, just counting occurrences.
- TF-IDF is a statistical weighting scheme for term importance, not a context-modeling mechanism.
- Stemming reduces words to root forms during preprocessing and has no attention mechanism.

</details>

---

