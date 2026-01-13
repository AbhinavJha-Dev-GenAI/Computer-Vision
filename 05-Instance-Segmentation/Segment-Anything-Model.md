# Segment Anything Model (SAM) ✨

SAM, released by Meta AI, is a foundation model for image segmentation. It can "segment anything" with zero-shot generalization through various prompts.

## 1. Key Features
- **Zero-Shot**: Works on images and objects it hasn't seen during training.
- **Promptable**: You can segment objects by:
    - Clicking (Points).
    - Drawing a Box.
    - Providing a Text description (combined with CLIP).
- **Ambiguity Aware**: If a prompt is ambiguous (e.g., clicking on a person wearing a hat), SAM can output multiple valid masks (the hat, the person, or the part of the person).

## 2. Architecture
- **Image Encoder**: A heavy-weight Vision Transformer (ViT) that pre-computes an image embedding.
- **Prompt Encoder**: Encodes points, boxes, or text.
- **Mask Decoder**: A lightweight transformer that combines embeddings and prompts to produce a mask in real-time.

## 3. The "Segment Anything" Data Engine
SAM was trained on the **SA-1B dataset**, containing over **1.1 Billion masks** on 11 Million images, which is 400x more masks than any previous dataset.

---

## 💻 Practical Code: Using SAM with Points

```python
from segment_anything import SamPredictor, sam_model_registry
import numpy as np

# Load SAM
sam = sam_model_registry["vit_h"](checkpoint="sam_vit_h.pth")
predictor = SamPredictor(sam)

# Set image
predictor.set_image(image)

# Define positive points (where the object is)
input_point = np.array([[500, 375]])
input_label = np.array([1])

# Predict
masks, scores, logits = predictor.predict(
    point_coords=input_point,
    point_labels=input_label,
    multimask_output=True,
)
```

> [!IMPORTANT]
> Because the **Image Encoder** is very heavy, it is standard practice to compute the image embedding once and then reuse it for multiple fast prompts.
