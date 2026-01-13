# 08. OCR (Optical Character Recognition) 🔍

OCR is the technology used to convert different types of documents, such as scanned paper documents, PDF files, or images captured by a digital camera, into editable and searchable data.

## ðŸ“š Core Concepts

### 1. The OCR Pipeline
Modern OCR is usually a two-step process:
1. **Text Detection**: Finding the bounding boxes of text in an image (e.g., using CRAFT, DBNet, or YOLOv8).
2. **Text Recognition**: Converting the pixels within those boxes into characters (e.g., using CRNN or Transformer-based models like TrOCR).

### 2. Layout Analysis
Understanding the structure of the document (e.g., separating columns, identifying tables, figures, and headers).

### 3. Preprocessing for OCR
OCR accuracy highly depends on image quality. Common steps include:
- Binarization (Otsu thresholding).
- Deskewing (correcting the angle of the image).
- Denoising.

---

## ðŸ“‚ Detailed Guides

1. [**Tesseract & PaddleOCR**](file:///d:/Vol-3%20ML%20AI/Computer-Vision/08-OCR/Tesseract-PaddleOCR.md): Comparing the classic engine with the modern SOTA.

---

## ⌨️ Basic EasyOCR Usage

```python
import easyocr

# Initialize reader (supports 80+ languages)
reader = easyocr.Reader(['en'])

# Read text from image
results = reader.readtext('invoice.jpg')

# Process results
for (bbox, text, prob) in results:
    print(f"Detected: {text} (Confidence: {prob:.2f})")
```

> [!TIP]
> **Tesseract** is great for scanned documents with high contrast, while **PaddleOCR** or **EasyOCR** excel at "Scene Text" (text found in the wild, like on signs or license plates).
