# 09. Face Recognition 👤

Face Recognition is the task of identifying or verifying a person's identity using their face. It involves a series of steps including detection, alignment, and matching.


### 1. Detection vs. Recognition
- **Face Detection**: "Is there a face in this image?" (e.g., MTCNN, BlazeFace, YOLOv8-face).
- **Face Recognition**: "Whose face is this?" (e.g., FaceNet, ArcFace, DeepFace).

### 2. Verification vs. Identification
- **Verification (1:1)**: Am I who I claim to be? (e.g., FaceID on iPhone).
- **Identification (1:N)**: Who is this person in a database of thousands? (e.g., Law enforcement databases).

### 3. Face Alignment
Rotating and scaling the face so that the eyes are always at a fixed location. This significantly improves recognition accuracy.

---

## ⌨️ Basic DeepFace Usage

```python
from deepface import DeepFace

# Verify if two images are of the same person
result = DeepFace.verify(img1_path = "img1.jpg", img2_path = "img2.jpg")
print("Is Match:", result["verified"])

# Search for a face in a database
df = DeepFace.find(img_path = "img.jpg", db_path = "C:/my_db")
```

> [!CAUTION]
> Face recognition carries significant **ethical and privacy concerns**. Always ensure you have consent and comply with local regulations (GDPR, BIPA) when building face-related systems.
