# 01. Image Fundamentals 🖼️

This folder covers the building blocks of digital images. Understanding how machines store and manipulate visual data is the first step toward advanced Computer Vision.



### 1. What is a Digital Image?
A digital image is a numeric representation (typically 2D) of a visual scene. At the lowest level, it is a **grid of pixels**.

- **Pixel (Picture Element)**: The smallest unit of an image.
- **Resolution**: The number of pixels in an image (Width x Height).
- **Bit Depth**: The number of bits used to represent each pixel (e.g., 8-bit for 256 levels of intensity).

### 2. Coordinate Systems
In OpenCV and most CV libraries:
- `(0, 0)` is the **top-left** corner.
- `x` increases to the right.
- `y` increases downwards.

### 3. Image Types
- **Binary**: 1 bit per pixel (Black & White).
- **Grayscale**: 8 bits per pixel (0-255 intensity levels).
- **Color**: Multiple channels (typically 3 for RGB/BGR).

---

## ⌨️ Basic OpenCV Operations

```python
import cv2

# Load an image
img = cv2.imread('image.jpg')

# Check dimensions (Height, Width, Channels)
h, w, c = img.shape
print(f"Resolution: {w}x{h}, Channels: {c}")

# Access a specific pixel (BGR order)
blue, green, red = img[100, 100]

# Slice a Region of Interest (ROI)
roi = img[50:150, 200:300]

# Display image
cv2.imshow('Image', img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

> [!TIP]
> **OpenCV uses BGR**, not RGB! This is the most common cause of "weird colors" when using other libraries like Matplotlib (which expects RGB).
