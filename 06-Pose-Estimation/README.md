# 06. Pose Estimation 🤸‍♀️🏗️

Pose estimation is the task of identifying the orientation and position of a person (or object) by detecting **keypoints** like joints, eyes, and limbs.

## 1. Paradigms: Top-Down vs. Bottom-Up ⚖️

### Top-Down
1. Detect all humans first (Object Detection).
2. Estimate keypoints for each detected person.
- **Example**: AlphaPose.
- **Pros**: Very accurate, handles small/overlapping people well.
- **Cons**: Slows down as more people enter the frame.

### Bottom-Up
1. Detect all keypoints in the image (e.g., all 500 elbows).
2. Group keypoints into individual human skeletons.
- **Example**: OpenPose.
- **Pros**: Constant speed regardless of the number of people.
- **Cons**: Struggles with complex poses or overlapping limbs.

---

## 2. Key Frameworks 🛠️

*   **MediaPipe (Google)**: The "Gold Standard" for real-time mobile/web pose estimation (BlazePose). It provides 33 landarks for the body, plus hands and face mesh.
*   **OpenPose (CMU)**: The first real-time multi-person system. Uses "Part Affinity Fields" (PAF) to connect joints.
*   **HRNet**: A high-resolution network that maintains high-res features throughout the entire process, leading to superior accuracy.

---

## 3. Human Mesh Recovery (3D Pose) 🧊

Moving beyond 2D $(x,y)$ dots to 3D skeletons or full 3D body meshes (SMPL model). This is critical for AR/VR and animation.

---

## 🛠️ Essential Snippet (MediaPipe Pose)

```python
import mediapipe as mp
import cv2

mp_pose = mp.solutions.pose
pose = mp_pose.Pose()

# Load Image
img = cv2.imread('sport.jpg')
results = pose.process(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))

# Access Keypoints
if results.pose_landmarks:
    for id, lm in enumerate(results.pose_landmarks.landmark):
        h, w, c = img.shape
        cx, cy = int(lm.x * w), int(lm.y * h)
        print(f"ID: {id}, Coord: ({cx}, {cy})")
```

---

## 🏀 Applications
- **Sports Analysis**: Tracking athlete form and calculating joint angles.
- **Fall Detection**: Monitoring elderly safety in smart homes.
- **Sign Language Recognition**: Tracking hand and body movement.
- **AR Filters**: Placing virtual clothes or items on a human body.
