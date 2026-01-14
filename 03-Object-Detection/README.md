# 03. Object Detection 🎯🔍

Object detection goes beyond classification by identifying **where** objects are in an image using bounding boxes.

## 1. The Core Paradox: Speed vs. Accuracy ⚖️

### Two-Stage Detectors (Accuracy Priority)
- **Examples**: Faster R-CNN, Cascade R-CNN.
- **Mechanics**: 1. Propose regions (RPN) -> 2. Classify and refine those regions.
- **Pros**: High accuracy, great for small objects.
- **Cons**: Slow, hard to run in real-time.

### One-Stage Detectors (Speed Priority)
- **Examples**: YOLO (v1-v10), SSD, RetinaNet.
- **Mechanics**: Treat detection as a regression problem. Single pass through the network predicts everything.
- **Pros**: Extremely fast (60+ FPS), lightweight for edge devices.
- **Cons**: Can struggle with very small or overlapping objects.

---

## 2. Critical Mechanics ⚙️

*   **Anchors**: Pre-defined boxes of different shapes/sizes that help the model guess bounding box dimensions.
*   **IoU (Intersection over Union)**: Measures how well the predicted box overlaps with the real "Ground Truth" box.
*   **NMS (Non-Maximum Suppression)**: If the model predicts 10 boxes for the same cat, NMS keeps only the one with the highest confidence and removes the others.

---

## 3. Metrics: mAP (mean Average Precision) 📊

mAP is the industry standard for detection. It's the average of the "Average Precision" across all classes.
- **mAP@.5**: Performance when the overlap (IoU) is 50%.
- **mAP@.5:.95**: A stricter metric averaged across multiple IoU thresholds (very hard!).

---

## 🛠️ Essential Snippet (YOLOv8 Inference)

```python
from ultralytics import YOLO

# 1. Load a pre-trained model (n=nano, s=small, m=medium, l=large, x=extra)
model = YOLO('yolov8n.pt') 

# 2. Run inference on an image
results = model('car.jpg')

# 3. Process results
for r in results:
    print(r.boxes.xyxy) # Bounding box coordinates
    print(r.boxes.conf) # Confidence scores
    print(r.boxes.cls)  # Class IDs
    
# 4. Save/Plot result
r.save(filename='result.jpg')
```

---

## 🌎 Current Trends
- **Vision Transformers (ViT)**: DETR (Detection Transformer) eliminates the need for NMS and Anchors entirely.
- **Zero-Shot Detection**: Using text prompts (e.g., Grounding DINO) to find objects the model was never explicitly trained on.
