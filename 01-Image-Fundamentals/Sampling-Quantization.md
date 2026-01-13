# Sampling & Quantization ðŸ“±

Converting a continuous scene into a digital image involves two key processes: **Sampling** and **Quantization**.

## 1. Sampling (Space)
Sampling is the process of digitizing the **spatial coordinates**.
- It determines the **Resolution**.
- Higher sampling rate = More pixels = Sharper image.
- **Aliasing**: This occurs when the sampling rate is too low, causing "jaggies" or Moire patterns.

## 2. Quantization (Intensity)
Quantization is the process of digitizing the **amplitude (intensity)**.
- It determines the **Bit Depth**.
- **8-bit**: 256 levels (Standard).
- **1-bit**: 2 levels (Binary image).
- **Low Quantization**: Can lead to "false contours" where smooth gradients look like distinct bands.

---

## ðŸ’» Visualizing Quantization Levels

```python
import cv2
import numpy as np

img = cv2.imread('portrait.jpg', cv2.IMREAD_GRAYSCALE)

# Reduce intensity levels to 4 (Quantization)
# Step size = 256 / 4 = 64
quantized = (img // 64) * 64

cv2.imshow('Original', img)
cv2.imshow('Quantized (4 Levels)', quantized)
cv2.waitKey(0)
```

### Recap Table

| Feature | Sampling | Quantization |
| :--- | :--- | :--- |
| **Domain** | Space (x, y) | Intensity (Brightness) |
| **Result** | Resolution (Width x Height) | Bit Depth (e.g., 8-bit) |
| **Artifacts** | Aliasing / Jaggies | False Contours |
