# Color Spaces ðŸŒˆ

Color spaces are mathematical models used to represent colors as tuples of numbers. Depending on the task (segmentation, tracking, or lighting adjustment), different color spaces are preferred.

## 1. RGB / BGR (Red, Green, Blue)
The default for screens and cameras.
- **RGB**: Standard in Matplotlib, PIL, and most web apps.
- **BGR**: The default in **OpenCV**.
- **Pros**: Intuitive for representation.
- **Cons**: High correlation between channels. A change in lighting affects all three channels, making it poor for color-based segmentation.

## 2. HSV (Hue, Saturation, Value)
Closer to how humans perceive color.
- **Hue**: The "color" type (0-179 in OpenCV).
- **Saturation**: The "vibrancy" or "purity" (0-255).
- **Value**: The brightness (0-255).
- **Usage**: Excellent for **Color Filtering** (e.g., detecting a yellow ball regardless of shadows).

## 3. LAB Space
Designed to be perceptually uniform.
- **L**: Lightness.
- **A**: Green-Red axis.
- **B**: Blue-Yellow axis.
- **Usage**: Removing shadows or matching colors across different lighting conditions.

---

## ðŸ’» Practical Code: BGR to HSV

```python
import cv2
import numpy as np

img = cv2.imread('color_wheel.jpg')

# Convert to HSV
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

# Define range for "Blue" color
lower_blue = np.array([100, 50, 50])
upper_blue = np.array([130, 255, 255])

# Threshold the HSV image to get only blue colors
mask = cv2.inRange(hsv, lower_blue, upper_blue)

cv2.imshow('Original', img)
cv2.imshow('Mask', mask)
cv2.waitKey(0)
```

> [!IMPORTANT]
> When defining color ranges in HSV using OpenCV, remember that **Hue range is 0-179**, not 0-360, because 8-bit integers can only store up to 255.
