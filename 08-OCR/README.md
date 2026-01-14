# 08. OCR - Optical Character Recognition 📄🔤

OCR is the process of converting digital images containing text into machine-readable text data. It is a fundamental part of Intelligent Document Processing (IDP).

## 1. The OCR Pipeline 🏗️

OCR is generally divided into two distinct sub-tasks:

### Text Detection (Where is the text?)
Finding the bounding boxes or polygons that contain text.
- **EAST (Efficient and Accurate Scene Text detector)**: A classic, fast detector for standard text.
- **DBNet / TextSnake**: Modern detectors that can handle curved or rotated text.

### Text Recognition (What does it say?)
Converting the pixels within a detection box into characters.
- **CRNN (Convolutional Recurrent Neural Network)**: Combines CNNs for feature extraction and RNNs (LSTMs) for sequence modeling.
- **CTC (Connectionist Temporal Classification)**: A loss function that allows the model to predict sequences without needing it to perfectly align with every pixel.

---

## 2. Industry Standard Tools 🛠️

*   **Tesseract (Google)**: The most famous open-source OCR engine. Good for clean documents but struggles with "Scene Text" (text on real-world objects).
*   **PaddleOCR (Baidu)**: Currently one of the most powerful and comprehensive OCR toolkits, supporting 80+ languages and layout analysis.
*   **EasyOCR**: A user-friendly Python library based on PyTorch that works well for scene text "out of the box."

---

## 3. Intelligent Document Processing (IDP) 🧠

Modern OCR doesn't just "read text." It uses **Layout Analysis** to understand the structure:
- Identifying Tables, Headers, and Footers.
- Converting a photo of an invoice into a JSON object with `vendor_name`, `total_amount`, and `tax_id`.

---

## 🛠️ Essential Snippet (Simple EasyOCR)

```python
import easyocr
import cv2

# 1. Initialize Reader
reader = easyocr.Reader(['en']) # Add more languages if needed

# 2. Read Text from Image
results = reader.readtext('invoice.jpg')

# 3. Process Results
for (bbox, text, prob) in results:
    print(f"Text: {text} (Confidence: {prob:.2f})")
    
    # Draw on image
    (top_left, top_right, bottom_right, bottom_left) = bbox
    cv2.rectangle(img, top_left, bottom_right, (0, 255, 0), 2)
```

---

## 🌎 Summary
OCR has moved from simple "Character Matching" to advanced "Multi-Modal Understanding." High-performing OCR today requires a mix of robust Detection and Transformer-based Recognition.
