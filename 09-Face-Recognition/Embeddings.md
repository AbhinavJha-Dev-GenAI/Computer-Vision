# Face Embeddings ðŸ§¬

How do computers "compare" faces? They don't compare pixels directly. Instead, they convert faces into a high-dimensional vector of numbers called an **Embedding**.

## 1. What is an Embedding?
A face embedding is a vector (usually 128 or 512 dimensions) where:
- Similar faces are placed **close together** in the vector space.
- Different faces are placed **far apart**.

## 2. Triplet Loss
This is a common loss function used to train face recognition models like FaceNet. It uses three images:
1. **Anchor**: A picture of Person A.
2. **Positive**: Another picture of Person A.
3. **Negative**: A picture of Person B.
- **The Goal**: Minimize the distance between (Anchor, Positive) and maximize the distance between (Anchor, Negative).

## 3. Comparing Embeddings
Once you have the vectors, you compare them using:
- **Euclidean Distance**: Standard straight-line distance.
- **Cosine Similarity**: Measures the angle between vectors (often more robust for faces).

---

## ðŸ’» Python Logic: Comparing Embeddings

```python
import numpy as np
from scipy.spatial.distance import cosine

# Hypothetical embeddings from a model
emb1 = np.array([0.1, 0.5, ...])
emb2 = np.array([0.12, 0.48, ...])

# Calculate Similarity
similarity = 1 - cosine(emb1, emb2)

if similarity > 0.9:
    print("Match Found!")
```

### Popular Models

| Model | Dimensions | Paper Link |
| :--- | :--- | :--- |
| **FaceNet** | 128-d | [Google Research](https://arxiv.org/abs/1503.03832) |
| **ArcFace** | 512-d | [InsightFace](https://arxiv.org/abs/1801.07698) |
| **DeepFace** | 4096-d | [Facebook AI](https://ieeexplore.ieee.org/document/6909616) |
