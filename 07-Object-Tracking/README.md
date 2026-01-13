# 07. Object Tracking 🤝

Object tracking is the process of estimating the trajectory of an object over time by maintaining a consistent ID for that object across consecutive frames of a video.



### 1. Detection vs. Tracking
- **Detection**: Analyzes one frame at a time to find objects.
- **Tracking**: Uses temporal information (previous frames) to predict the position in the current frame.

### 2. Algorithms
- **SORT (Simple Online and Realtime Tracking)**: Uses a Kalman filter for motion prediction and the Hungarian algorithm for data association (matching detection boxes to predicted positions).
- **DeepSORT**: Adds a **Deep Learning embedding** to SORT. It uses a small Re-Identification (ReID) network to match objects based on their appearance, allowing for better tracking through occlusions.
- **ByteTrack**: A simple and fast tracker that makes use of low-confidence detection boxes (often ignored by other trackers) to maintain trajectories.

### 3. Challenges
- **Occlusions**: When an object is temporarily hidden by another object.
- **ID Switches**: When the tracker incorrectly swaps the ID of two nearby objects.
- **Motion Blur/High-speed**: Managing fast-moving objects that significantly change position between frames.

---

## ⌨️ Basic BoT-SORT Usage (Ultralytics)

```python
from ultralytics import YOLO

# Load model
model = YOLO('yolov8n.pt')

# Track objects in a video
# tracking method can be 'botsort.yaml' or 'bytetrack.yaml'
results = model.track(source="highway.mp4", show=True, tracker="botsort.yaml")
```

### Tracker Comparison

| Tracker | Speed | Accuracy | Best For |
| :--- | :--- | :--- | :--- |
| **SORT** | Ultra-Fast | Low | Simple motion, few occlusions |
| **DeepSORT** | Fast | High | Handling occlusions, ReID |
| **ByteTrack** | Very Fast | Very High | Crowded scenes, real-time |
| **BoT-SORT** | Fast | SOTA | High precision, camera motion |

> [!IMPORTANT]
> **ByteTrack** and **BoT-SORT** are currently the industry standard for high-performance, real-time tracking in standard surveillance or traffic monitoring tasks.
