# 07. Object Tracking 🏃‍♂️👀

Object tracking is about maintaining a unique identity for an object across multiple frames in a video video ($ID_1$ remains $ID_1$ even after moving).

## 1. Tracking Paradigms 🏗️

### SOT (Single Object Tracking)
Tracking one specific object defined in the first frame (e.g., following a specific runner).

### MOT (Multi-Object Tracking)
Tracking every object of a certain class (e.g., all cars on a highway).

---

## 2. Core Algorithms ⚙️

### SORT (Simple Online and Realtime Tracking)
- **Kalman Filter**: Predicts where the object will be in the next frame based on its current velocity/direction.
- **Hungarian Algorithm**: Assigns new detections to existing tracks by maximizing overlap (IoU).

### DeepSORT
Adds a **CNN Feature Extractor** to SORT.
- **Benefit**: If a person goes behind a tree (occlusion) and reappears, DeepSORT uses their "looks" (embeddings) to re-identify them, even if the Kalman filter's prediction was off.

### ByteTrack
Instead of throwing away low-confidence detections (which might be blurred or occluded objects), ByteTrack uses them to bridge gaps in tracks. It is currently one of the fastest and most robust MOT algorithms.

---

## 3. Key Challenges ⚠️

*   **Occlusion**: When objects overlap or go behind background items.
*   **ID Switching**: When two objects cross paths and the tracker accidentally swaps their IDs.
*   **Motion Blur**: Low-quality frames making detection difficult.

---

## 🛠️ Essential Snippet (DeepSORT with YOLO)

```python
from ultralytics import YOLO
from deep_sort_realtime.deepsort_tracker import DeepSort

# 1. Initialize YOLO and Tracker
model = YOLO("yolov8n.pt")
tracker = DeepSort(max_age=30)

# 2. Loop through frames
while cap.isOpened():
    success, frame = cap.read()
    results = model(frame)
    
    # Extract [x, y, w, h, conf, class] for DeepSORT
    detections = []
    for r in results:
        # Format detections for tracker...
        pass
        
    # 3. Update Tracker
    tracks = tracker.update_tracks(detections, frame=frame)
    for track in tracks:
        if not track.is_confirmed():
            continue
        track_id = track.track_id
        bbox = track.to_ltrb() # Left, Top, Right, Bottom
```

---

## 🚨 Summary
Tracking transforms "Image AI" into "Video AI." It is the difference between seeing a car and measuring a traffic jam.
