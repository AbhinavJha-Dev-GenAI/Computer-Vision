# 09. Face Recognition 👤🛡️

Face recognition is the task of identifying or verifying a person's identity based on their facial features.

## 1. Verification vs. Identification ⚖️

*   **Verification (1:1)**: "Is this the same person?" (e.g., unlocking your phone). Compare two face images and check if they match.
*   **Identification (1:N)**: "Who is this person?" (e.g., finding a criminal in a database). Compare the input face against a gallery of millions of known identities.

---

## 2. The Face Recognition Pipeline 🏗️

### Stage 1: Face Detection & Alignment
Finding the face and "flattening" it (rotating so the eyes are level and the nose is centered).
- **Tools**: MTCNN, RetinaFace, or MediaPipe Face Detection.

### Stage 2: Feature Extraction (Embeddings)
Passing the aligned face through a deep CNN to generate a "Face Embedding" (a vector of e.g., 128 or 512 numbers).
- **Goal**: Two images of the *same* person should have embeddings very close to each other in vector space. Two *different* people should be far apart.
- **Architectures**: FaceNet, ArcFace, InsightFace.

### Stage 3: Verification (Distance Metric)
Calculating the distance between two embeddings.
- **Cosine Similarity** or **Euclidean Distance**.
- If $Distance < Threshold$, they are the same person.

---

## 3. Dealing with Anti-Spoofing (Liveness) 🛑

Face recognition is useless if it can be fooled by a photo or video of a person.
- **Liveness Detection**: Checking for eye blinks, depth (using IR cameras), or texture analysis to ensure the subject is a "live" human.

---

## 🛠️ Essential Snippet (DeepFace Simple Verification)

```python
from deepface import DeepFace

# Verification (1:1)
result = DeepFace.verify(
    img1_path = "img1.jpg", 
    img2_path = "img2.jpg",
    model_name = "ArcFace" # VGG-Face, Facenet, OpenFace, DeepFace, DeepID, ArcFace, Dlib
)

if result["verified"]:
    print("Match found!")
else:
    print("Not the same person.")

# Identification (Finding in a database)
dfs = DeepFace.find(img_path = "query.jpg", db_path = "user_database/")
```

---

## 📊 Summary
Face recognition is no longer about "matching templates." It's about mapping faces to highly discriminative **High-Dimensional Latent Spaces**.
