# 01. Image Fundamentals 🖼️🔬

Understanding how machines perceive and represent visual data is the absolute foundation of Computer Vision.

## 1. Digital Representation 🔢

An image is essentially a matrix of numbers.
- **Pixel**: The smallest addressable element.
- **Resolution**: Total pixel count (e.g., $1920 \times 1080$).
- **Bit Depth**: Determines the range of colors/intensities ($2^8 = 256$ values for standard 8-bit images).

---

## 2. Color Spaces: How we see light 🌈

| Space | Characteristics | Best For... |
| :--- | :--- | :--- |
| **RGB/BGR** | Additive color model (Red, Green, Blue). | Displaying images / Standard storage. |
| **HSV** | Hue (color), Saturation (intensity), Value (brightness). | Color-based segmentation (e.g., "detect all red objects"). |
| **YUV / LAB** | Separates Luminance (brightness) from Chrominance (color). | Compression and human-perception-based tasks. |

> [!CAUTION]
> **BGR vs RGB**: OpenCV reads images as BGR by default. Matplotlib and PyTorch expect RGB. Always convert using `cv2.cvtColor(img, cv2.COLOR_BGR2RGB)`.

---

## 3. Sampling & Quantization 📐

- **Sampling**: Digitizing the spatial coordinates (converting a continuous scene into discrete pixels). High sampling = High resolution.
- **Quantization**: Digitizing the amplitude (converting continuous light intensity into discrete levels, e.g., 0-255). Low quantization leads to "contouring" artifacts.

---

## 🛠️ Essential Snippet (Image Properties & Conversions)

```python
import cv2

# Load image
img = cv2.imread('input.jpg')

# 1. Properties
print(f"Shape: {img.shape}") # (H, W, Channels)
print(f"Data type: {img.dtype}") # uint8 is standard

# 2. Color Conversion (BGR -> HSV for target detection)
hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

# 3. Resizing (Changing Sampling)
# Interpolation: INTER_AREA for shrinking, INTER_CUBIC for zooming
resized = cv2.resize(img, (224, 224), interpolation=cv2.INTER_AREA)

# 4. Normalization (Preparing for Deep Learning)
normalized = img.astype('float32') / 255.0
```

---

## 📊 Summary
Before building complex models, remember that **Garbage In = Garbage Out**. Mastering these fundamentals ensures your data is correctly formatted and optimized for the next stages of the CV pipeline.
