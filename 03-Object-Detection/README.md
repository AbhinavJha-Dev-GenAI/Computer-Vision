# 03. Object Detection 🎯

Object detection is the task of identifying the **location** (Bounding Box) and **class** of objects within an image.



### 1. Sliding Window vs Region Proposals
- **Sliding Window**: Moving a fixed-size window over the image and classifying each crop (Slow).
- **Region Proposals**: Using algorithms like Selective Search to guess where objects might be (Faster R-CNN).

### 2. Architecture Types
- **Two-Stage**: First propose regions, then classify (e.g., R-CNN, Faster R-CNN). High accuracy, slower.
- **One-Stage**: Predict boxes and classes in a single pass (e.g., YOLO, SSD, RetinaNet). Fast, ideal for real-time.

### 3. Key Components
- **Backbone**: CNN used for feature extraction (ResNet, CSPDarknet).
- **Neck**: Aggregates features from different layers (FPN, PAN).
- **Head**: The final layer that predicts bounding boxes and class scores.

---

## ⌨️ Basic YOLOv8 Usage (Ultralytics)

```python
from ultralytics import YOLO

# Load a pretrained model
model = YOLO('yolov8n.pt') 

# Run inference
results = model('image.jpg')

# Process results
for r in results:
    print(r.boxes) # Print Bounding Boxes
    r.show() # Display output
```

> [!IMPORTANT]
> Modern Object Detection is dominated by the **YOLO (You Only Look Once)** family due to its incredible speed-to-accuracy trade-off.
