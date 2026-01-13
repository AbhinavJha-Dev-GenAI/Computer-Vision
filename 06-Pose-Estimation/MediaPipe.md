# MediaPipe Pose 🚀

MediaPipe is an open-source framework by Google for building high-performance, cross-platform Computer Vision pipelines. Its pose estimation component (BlazePose) is famous for its speed and mobile-friendliness.

## 1. How it Works
MediaPipe Pose tracks **33 3D landmarks** on the human body.
- It uses a two-step detector-tracker pipeline.
- The detector first finds the body’s bounding box.
- The tracker then predicts the landmarks.
- **Critical Feature**: It uses the previous frame's landmark predictions to localize the box in the current frame, significantly speeding up video processing.

## 2. Landmarks Map
The 33 landmarks include:
- **0 - 10**: Face landmarks (Nose, Eyes, Ears).
- **11 - 16**: Upper body (Shoulders, Elbows, Wrists).
- **23 - 28**: Lower body (Hips, Knees, Ankles).
- **29 - 32**: Feet (Heels and Toes).

---

## 💻 Python Implementation: Real-time Pose

```python
import cv2
import mediapipe as mp

mp_pose = mp.solutions.pose
pose = mp_pose.Pose()
mp_draw = mp.solutions.drawing_utils

cap = cv2.VideoCapture(0)

while cap.isOpened():
    success, img = cap.read()
    img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    
    # Process
    results = pose.process(img_rgb)
    
    # Draw landmarks
    if results.pose_landmarks:
        mp_draw.draw_landmarks(img, results.pose_landmarks, mp_pose.POSE_CONNECTIONS)
        
    cv2.imshow("Pose", img)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
```

### Why use MediaPipe?

| Feature | MediaPipe | YOLOv8-Pose |
| :--- | :--- | :--- |
| **Speed** | Ultra-fast (optimized for CPU/Mobile) | Fast (optimized for GPU) |
| **Landmarks** | 33 Landmarks | 17 Landmarks |
| **Environment** | Web, Android, iOS, Desktop | Mostly Python/Server |
| **Ease of use** | Plug & Play | Training required for custom objects |
