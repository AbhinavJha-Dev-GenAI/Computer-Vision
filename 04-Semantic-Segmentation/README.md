# 04. Semantic Segmentation 🧱🎨

Semantic segmentation is the task of classifying **every single pixel** in an image into a category. There is no distinction between individual instances of the same class (e.g., all "cars" are one color).

## 1. Core Architectures 🏗️

### FCN (Fully Convolutional Network)
The pioneer that replaced dense layers with convolutions to produce spatial maps instead of single labels.

### U-Net (The Star of Bio-Medical CV)
- **Shape**: Looks like a "U" with an Encoder (downsampling) and a Decoder (upsampling).
- **Skip Connections**: The key secret of U-Net. It passes fine-grained features from the encoder directly to the decoder, helping the model recover sharp boundaries.

### DeepLab (Google)
- **Atrous (Dilated) Convolutions**: Allows a wider field of view without increasing the number of parameters.
- **ASPP (Atrous Spatial Pyramid Pooling)**: Captures multi-scale context by using different dilation rates.

---

## 2. Metrics for Success 📊

*   **IoU (Jaccard Index)**: The standard. It measures the overlap between the predicted mask and the ground truth.
*   **Dice Coefficient**: Similar to IoU but gives double weight to the overlap. Commonly used in medical imaging.
*   **Pixel Accuracy**: Often misleading if classes are imbalanced (e.g., the background is 90% of the image).

---

## 3. The Modern SOTA: SAM (Segment Anything) 🪄

Meta's **Segment Anything Model (SAM)** has revolutionized segmentation. It is a "Foundation Model" for vision:
- **Zero-shot**: Can segment objects it has never seen before.
- **Promptable**: You can click an object, draw a box, or even use text to segment anything.

---

## 🛠️ Essential Snippet (Inference with SAM)

```python
from segment_anything import SamPredictor, sam_model_registry

# 1. Load SAM model
sam = sam_model_registry["vit_h"](checkpoint="sam_vit_h.pth")
predictor = SamPredictor(sam)

# 2. Set the image
predictor.set_image(image_bgr)

# 3. Predict mask based on a single point (click)
input_point = np.array([[500, 375]])
input_label = np.array([1])

masks, scores, logits = predictor.predict(
    point_coords=input_point,
    point_labels=input_label,
    multimask_output=True,
)
```

---

## 🌍 Applications
- **Medical**: Segmenting tumors or organs in CT scans.
- **Autonomous Driving**: Distinguishing road vs. sidewalk vs. sky.
- **Satellite Imaging**: Calculating forest coverage or urban growth.
