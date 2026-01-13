# 04. Semantic Segmentation 🧩

Semantic Segmentation is the process of classifying every single pixel in an image into a category. Unlike Object Detection, it provides fine-grained boundaries but does not differentiate between multiple instances of the same object.

## 📚 Core Concepts

### 1. FCN (Fully Convolutional Networks)
Replacing the fully connected layers of a standard CNN with convolutions, allowing the output to be a spatial map (heatmap) rather than a single vector.

### 2. U-Net Architecture
Encapsulates an **Encoder** (Contracting path) and a **Decoder** (Expanding path) with **Skip Connections**.
- **Encoder**: Extracts features while reducing spatial dimensions.
- **Decoder**: Up-samples the features back to the original image size.
- **Skip Connections**: Pass fine-grained detail from the encoder directly to the decoder to preserve edge information.

### 3. DeepLabV3+
Uses **Atrous (Dilated) Convolutions** to capture multi-scale context without increasing the number of parameters.

---

## 📂 Detailed Guides

1. [**Loss Functions**](file:///d:/Vol-3%20ML%20AI/Computer-Vision/04-Semantic-Segmentation/Loss-Functions.md): Why standard Cross-Entropy isn't enough for segmentation.

---

## ⌨️ Basic PyTorch Inference (DeepLabV3)

```python
import torch
from torchvision import models, transforms
from PIL import Image

# Load model
model = models.segmentation.deeplabv3_resnet101(pretrained=True).eval()

# Preprocess image
input_image = Image.open('street.jpg')
preprocess = transforms.Compose([
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.485, 0.456, 0.406], std=[0.229, 0.224, 0.225]),
])
input_tensor = preprocess(input_image).unsqueeze(0)

# Inference
with torch.no_grad():
    output = model(input_tensor)['out'][0]
output_predictions = output.argmax(0)
```

> [!TIP]
> **U-Net** is the industry standard for Medical Imaging and Satellite imagery segmentation due to its accuracy with limited data.
