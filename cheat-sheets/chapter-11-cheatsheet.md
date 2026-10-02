## Chapter 11 Cheat Sheet — Optimization, NLP & CV

### Gradient Descent Variants
| Method | Update Basis | Pros | Exam Trigger |
|---|---|---|---|
| SGD | Single mini-batch gradient | Simple, cheap | 'Basic baseline optimizer' |
| SGD + Momentum | Gradient + moving avg of past gradients (β≈0.9) | Smooths oscillation, faster on ravines | 'Oscillating loss, non-convex' |
| Adam | 1st moment (mean, β1=0.9) + 2nd moment (variance, β2=0.999) + ε=1e-8 | Adaptive per-parameter LR, fast convergence | 'Adaptive learning rate needed' |

### Convex vs Non-Convex
| Property | Convex | Non-Convex |
|---|---|---|
| Minima | One global minimum | Multiple local minima / saddle points |
| Example | Linear/logistic regression | Deep neural networks |
| Guarantee | Local min = global min | No such guarantee |

### NLP Pipeline (in order)
1. **Tokenization** — split text into tokens; subword methods (BPE, WordPiece) handle OOV words.
2. **Embeddings** — map tokens to dense vectors; static (word2vec, GloVe) vs contextual (BERT-style, varies by sentence).
3. **Positional Encoding** — injects order info (transformers have no inherent recurrence).
4. **Transformer / Self-Attention** — each token weighs relevance of all others; enables long-range context, parallelizable (unlike RNN/LSTM).
5. **Task Head** — classification, generation, etc.

### CV Pipeline
1. **Convolution** — learned filters slide over input extracting local features (edges → textures → shapes with depth).
2. **Pooling** — downsamples feature maps, reduces dimensionality/computation.
3. **Transfer Learning** — reuse pretrained model (e.g., ImageNet-trained CNN); freeze early generic layers, fine-tune later task-specific layers. Use when labeled data is scarce.
4. **Object Detection** — outputs class label + bounding box per object (YOLO, Faster R-CNN family) — distinct from plain classification (single label, no location).

### Optimizer Selection Quick Rule
- Need fast convergence / adaptive rates / sparse gradients → **Adam**
- Need best generalization on large-scale vision tasks, willing to tune LR schedule → **SGD + Momentum**
- Oscillating loss on non-convex surface → add **momentum** or switch to **Adam**

### Architecture Selection Quick Rule
- Sequential/text data, long-range dependency → **Transformer**
- Spatial/grid image data → **CNN** (+ transfer learning if data-limited)
- Need object location, not just label → **Detection architecture**, not classifier

### Common Exam Traps
- Confusing momentum (1st moment only) with Adam (1st + 2nd moment).
- Assuming deep neural nets are convex — they are NOT.
- Forgetting tokenization precedes embedding lookup.
- Choosing classification when the scenario needs bounding boxes (detection).
