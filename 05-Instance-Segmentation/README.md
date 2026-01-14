# 05. Instance Segmentation 👤👤

Instance segmentation combines the "What" and "Where" of Object Detection with the pixel-level precision of Semantic Segmentation. It distinguishes between **individual objects** of the same class (e.g., Car #1, Car #2).

## 1. Top Architecture: Mask R-CNN 🎭

Mask R-CNN is the industry standard. It extends Faster R-CNN by adding a third "branch":
1.  **Classification Branch**: What is it? (Cat)
2.  **Bounding Box Branch**: Where is it? (Rectangle)
3.  **Mask Branch**: Which exact pixels? (Binary mask)

### Key Innovation: RoIAlign
Unlike RoIPool (which has quantization errors), **RoIAlign** uses bilinear interpolation to ensure that features are perfectly aligned with the original image pixels, which is crucial for high-precision masks.

---

## 2. Real-Time Alternatives ⚡

Mask R-CNN is slow. For real-time video (e.g., surgery or traffic), we use:
*   **YOLACT (You Only Look At CoefficienTs)**: A one-stage approach that generates "Protonets" (mask prototypes) and assembles them.
*   **Segmenting Objects with Transformers (SOLO)**: A simpler approach that assigns each pixel a "location" category.

---

## 3. Panoptic Segmentation: The Ultimate Goal 🌍

Panoptic segmentation is the total visual understanding of a scene:
- **Things**: Individual instances (Cars, People, Dogs).
- **Stuff**: Background stuff (Sky, Grass, Road).
**Panoptic = Instance Segmentation + Semantic Segmentation**.

---

## 🛠️ Essential Snippet (Detectron2 / Mask R-CNN)

```python
import detectron2
from detectron2.engine import DefaultPredictor
from detectron2.config import get_cfg

# 1. Setup Configuration
cfg = get_cfg()
cfg.merge_from_file(model_zoo.get_config_file("COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_3x.yaml"))
cfg.MODEL.ROI_HEADS.SCORE_THRESH_TEST = 0.5 
cfg.MODEL.WEIGHTS = model_zoo.get_checkpoint_url("COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_3x.yaml")

# 2. Run Predictor
predictor = DefaultPredictor(cfg)
outputs = predictor(image)

# 3. Access Masks
masks = outputs["instances"].pred_masks
```

---

## 📊 Summary
Instance segmentation is the "Heavy Lifter" of Computer Vision. It provides the highest level of granularity needed for robotics, medical automation, and high-end video editing.
