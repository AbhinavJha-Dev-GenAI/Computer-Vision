# 05. Instance Segmentation 🎭

Instance Segmentation is the task of identifying and delineating each distinct object (instance) in an image. It combines **Object Detection** (finding instances) and **Semantic Segmentation** (pixel-level mask for each instance).

## ðŸ“š Core Concepts

### 1. Mask R-CNN
The pioneering architecture for instance segmentation.
- It extends **Faster R-CNN** by adding a branch for predicting segmentation masks on each Region of Interest (RoI).
- **RoIAlign**: A quantization-free pooling method that preserves spatial exactness, which is critical for masks.

### 2. Detectron2
Facebook (Meta) AI Research's next-generation library that implements state-of-the-art algorithms like Mask R-CNN, RetinaNet, and Panoptic Segmentation.

### 3. Panoptic Segmentation
Combines Semantic Segmentation (stuff like grass, sky) and Instance Segmentation (things like cars, people) into a single task.

---

## ðŸ“‚ Detailed Guides

1. [**Segment Anything Model (SAM)**](file:///d:/Vol-3%20ML%20AI/Computer-Vision/05-Instance-Segmentation/Segment-Anything-Model.md): The Foundation Model for Vision.

---

## ⌨️ Basic Detectron2 Usage

```python
import detectron2
from detectron2.utils.visualizer import Visualizer
from detectron2.data import MetadataCatalog
from detectron2.engine import DefaultPredictor
from detectron2.config import get_cfg

# Create config
cfg = get_cfg()
cfg.merge_from_file(model_zoo.get_config_file("COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_3x.yaml"))
cfg.MODEL.WEIGHTS = model_zoo.get_checkpoint_url("COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_3x.yaml")
cfg.MODEL.ROI_HEADS.SCORE_THRESH_TEST = 0.5

# Predict
predictor = DefaultPredictor(cfg)
outputs = predictor(im)

# Visualize
v = Visualizer(im[:, :, ::-1], MetadataCatalog.get(cfg.DATASETS.TRAIN[0]))
out = v.draw_instance_predictions(outputs["instances"].to("cpu"))
cv2.imshow('Instances', out.get_image()[:, :, ::-1])
```

> [!NOTE]
> Instance segmentation is computationally heavier than object detection because it requires predicting a mask for every detected object.
