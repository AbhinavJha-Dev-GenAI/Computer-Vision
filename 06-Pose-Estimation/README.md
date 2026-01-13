# 06. Pose Estimation ðŸ“‹

Human Pose Estimation (HPE) is the task of identifying the location of specific keypoints (joints) like the nose, eyes, shoulders, elbows, and knees on a human body.

## ðŸ“š Core Concepts

### 1. Keypoints & Skeleton
A human body is represented as a set of keypoints (usually 17-33) connected by "limbs" to form a skeleton.

### 2. Approaches
- **Top-Down**: 
    1. Detect humans in an image using a detector (like YOLO).
    2. Run a pose estimator on each cropped human box.
    - *Example*: AlphaPose, HRNet.
- **Bottom-Up**:
    1. Detect all keypoints in the image simultaneously.
    2. Group them into individual skeletons.
    - *Example*: OpenPose, HigherHRNet.

### 3. Applications
- Fitness tracking (Counting reps).
- Sign language recognition.
- Augmented Reality (AR) filters.
- Gesture-based controls.

---

## ðŸ“‚ Detailed Guides

1. [**MediaPipe**](file:///d:/Vol-3%20ML%20AI/Computer-Vision/06-Pose-Estimation/MediaPipe.md): Google's framework for real-time cross-platform pose tracking.

---

## âŒ¨ï¸  Basic YOLOv8 Pose Inference

```python
from ultralytics import YOLO

# Load a pose model
model = YOLO('yolov8n-pose.pt') 

# Predict
results = model('yoga.jpg')

# View keypoints
for r in results:
    print(r.keypoints) # x, y coordinates
    r.show()
```

> [!TIP]
> **Top-Down** methods are generally more accurate but their speed depends on the number of people in the image. **Bottom-Up** methods have a constant speed regardless of the number of people.
