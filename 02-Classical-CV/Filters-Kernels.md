# Filters & Kernels ðŸ§²

Filters are used to transform images by performing a convolution between an input image and a small matrix called a **Kernel**.

## 1. Smoothing (Blurring)
Used to reduce noise.
- **Gaussian Blur**: Weighted average of neighbors. Smoothens while preserving edges better than a simple box filter.
- **Median Blur**: Replaces pixel with the median of neighbors. Best for **Salt-and-Pepper noise**.
- **Bilateral Filter**: Smoothens noise while **leaving edges sharp**. Computationally expensive but effective.

## 2. Edge Detection
Finding areas with sharp changes in intensity.
- **Sobel**: Calculates the gradient of image intensity. Useful for finding horizontal and vertical edges.
- **Canny Edge Detector**: The "Gold Standard". A multi-stage algorithm that includes:
    1. Grayscale conversion.
    2. Gaussian smoothing.
    3. Finding gradients.
    4. Non-maximum suppression.
    5. Hysteresis thresholding.

---

## ðŸ’» Practical Code: Edge Detection

```python
import cv2

img = cv2.imread('road.jpg', 0)

# Apply Gaussian Blur
blur = cv2.GaussianBlur(img, (5, 5), 0)

# Apply Canny
edges = cv2.Canny(blur, 50, 150)

cv2.imshow('Edges', edges)
cv2.waitKey(0)
```

> [!TIP]
> Always apply a blur (like Gaussian) before Canny Edge detection to reduce noise that might be mistaken for edges.
