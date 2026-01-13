# Feature Extraction ðŸŽ¯

Feature extraction involves finding "interesting" points in an image that can be used for matching, tracking, or object recognition.

## 1. SIFT (Scale-Invariant Feature Transform)
- **Key Property**: Invariant to scale, rotation, and illumination changes.
- **How**: Detects "blobs" and describes them with a 128-d vector.
- **Status**: Was patented, but now free for use.

## 2. ORB (Oriented FAST and Rotated BRIEF)
- **Key Property**: Extremely fast and efficient.
- **Context**: Developed by OpenCV labs as a free alternative to SIFT/SURF.
- **Usage**: Standard for SLAM and real-time mobile apps.

## 3. HOG (Histogram of Oriented Gradients)
- **Concept**: Counts occurrences of gradient orientation in localized portions of an image.
- **Usage**: Famously used for **Human Detection** (combined with SVM).

---

## ðŸ’» Practical Code: ORB Feature Matching

```python
import cv2

img1 = cv2.imread('logo.png', 0)
img2 = cv2.imread('webpage_screenshot.png', 0)

# Initialize ORB detector
orb = cv2.ORB_create()

# Find keypoints and descriptors
kp1, des1 = orb.detectAndCompute(img1, None)
kp2, des2 = orb.detectAndCompute(img2, None)

# Matcher
bf = cv2.BFMatcher(cv2.NORM_HAMMING, crossCheck=True)
matches = bf.match(des1, des2)

# Sort them in the order of their distance
matches = sorted(matches, key=lambda x: x.distance)

# Draw first 20 matches
res = cv2.drawMatches(img1, kp1, img2, kp2, matches[:20], None, flags=2)

cv2.imshow('Matches', res)
cv2.waitKey(0)
```

### Techniques Comparison

| Feature | SIFT | ORB | HOG |
| :--- | :--- | :--- | :--- |
| **Speed** | Slow | Very Fast | Fast |
| **Scale Invariant**| Yes | Partial | No |
| **Rotation Invariant**| Yes | Yes | No |
| **Primary Use** | High Precision | Mobile/RT | Detection |
