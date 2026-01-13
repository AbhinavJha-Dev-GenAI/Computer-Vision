# 02. Classical CV ðŸ”¬

Classical Computer Vision refers to the set of techniques that don't rely on deep learning. These are essential for preprocessing, real-time edge applications, and understanding the foundations of Vision.

## ðŸ“š Core Concepts

### 1. Image Filtering
Using kernels (small matrices) to perform operations like blurring, sharpening, or edge detection.

### 2. Histograms
A graphical representation of the intensity distribution of an image. Useful for contrast stretching and equalization.

### 3. Morphological Operations
Non-linear operations related to the shape or morphology of features.
- **Erosion**: Erodes away the boundaries of foreground objects.
- **Dilation**: Adds pixels to the boundaries of objects.
- **Opening**: Erosion followed by Dilation (Removes noise).
- **Closing**: Dilation followed by Erosion (Fills small holes).

### 4. Contours
Curves joining all the continuous points along a boundary which have the same color or intensity.

---

## ðŸ“‚ Detailed Guides

1. [**Filters & Kernels**](file:///d:/Vol-3%20ML%20AI/Computer-Vision/02-Classical-CV/Filters-Kernels.md): Gaussian, Median, Sobel, and Canny.
2. [**Feature Extraction**](file:///d:/Vol-3%20ML%20AI/Computer-Vision/02-Classical-CV/Feature-Extraction.md): SIFT, ORB, and HOG.

---

## âŒ¨ï¸  Basic OpenCV Workflow

```python
import cv2
import numpy as np

img = cv2.imread('shapes.png', 0) # Read as grayscale

# Thresholding
_, thresh = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Finding Contours
contours, _ = cv2.findContours(thresh, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)

# Drawing Contours
cv2.drawContours(img, contours, -1, (0, 255, 0), 3)

cv2.imshow('Contours', img)
cv2.waitKey(0)
```

> [!NOTE]
> Even in the age of Deep Learning, **Classical CV is critical** for data augmentation, ROI extraction, and lightweight processing.
