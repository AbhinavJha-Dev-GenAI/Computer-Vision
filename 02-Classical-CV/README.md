# 02. Classical CV 🔬🏛️

Classical CV consists of mathematics-heavy techniques used before the rise of Deep Learning. They remain critical for speed, low-power devices, and data prep.

## 1. Image Filtering (Kernels) 🌫️

A kernel is a small matrix (e.g., $3 \times 3$) that slides over the image to perform a mathematical operation on each pixel.
- **Gaussian Blur**: Smooths the image and reduces noise.
- **Median Blur**: Excellent for removing "salt and pepper" noise.
- **Sobel / Laplacian**: Used for finding gradients and edges.

---

## 2. Morphological Operations 🏗️

Operations based on the shape of objects in white-on-black binary images.
*   **Erosion**: Shrinks foreground (useful for splitting touching objects).
*   **Dilation**: Grows foreground (useful for joining broken parts).
*   **Opening**: Erosion then Dilation (removes small background noise).
*   **Closing**: Dilation then Erosion (fills small holes in the foreground).

---

## 3. Feature Detectors (SIFT, SURF, ORB) 🧿

Instead of looking at every pixel, we look for **Keypoints** (corners or edges) that are distinct.
- **SIFT (Scale-Invariant Feature Transform)**: Robust to rotation and scale but computationally heavy (and historically patented).
- **ORB (Oriented FAST and Rotated BRIEF)**: A fast, efficient, and open-source alternative used in real-time SLAM.

---

## 4. Edge Detection (Canny) 🔪
The Canny edge detector is the "Gold Standard" because it uses multi-stage processing:
1. Noise reduction.
2. Gradient calculation.
3. Non-maximum suppression (thinning the edges).
4. Hysteresis thresholding (connecting edges).

---

## 🛠️ Essential Snippet (Classical Pipeline)

```python
import cv2
import numpy as np

img = cv2.imread('coins.jpg')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# 1. Blur to remove noise
blurred = cv2.GaussianBlur(gray, (5, 5), 0)

# 2. Canny Edge Detection
edges = cv2.Canny(blurred, 50, 150)

# 3. Find and Draw Contours
contours, _ = cv2.findContours(edges, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
cv2.drawContours(img, contours, -1, (0, 255, 0), 2)

# 4. ORB Feature Detection
orb = cv2.ORB_create()
kp, des = orb.detectAndCompute(gray, None)
img_kp = cv2.drawKeypoints(img, kp, None, color=(255, 0, 0))
```

---

## ⚖️ Pro-Tip: Efficiency
In production, if you only need to detect a bright green object on a dark background, a simple **HSV Color Mask** is $1000\times$ faster than a Deep Learning model.
