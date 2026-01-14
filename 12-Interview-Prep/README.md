# 12. Computer Vision Interview Preparation 🧠🏛️

Technical, practical, and design questions for Computer Vision Engineering roles.

## 1. Architecure & Mechanics 📖

*   **Q: Difference between RoIPool and RoIAlign?**
    - *A:* RoIPool uses quantization (rounding coordinates), which leads to slight misalignments. RoIAlign uses bilinear interpolation to extract features at exact floating-point locations, making it much better for segmentation masks.
*   **Q: Why use a "Bottleneck" block in ResNet?**
    - *A:* It uses $1\times1$ convolutions to reduce the number of channels before the more expensive $3\times3$ convolution, significantly saving computation while maintaining performance.
*   **Q: What is the purpose of NMS (Non-Maximum Suppression)?**
    - *A:* It removes redundant, overlapping bounding boxes for the same object by keeping only the one with the highest confidence score and discarding those with high IoU (overlap) with it.

---

## 2. Practical Scenarios 🛠️

*   **Q: Your model works perfectly on high-res images but fails on blurry security camera footage. Why?**
    - *A:* Distribution Shift. The model was likely trained on sharp datasets (COCO/ImageNet). Fix: Add **Data Augmentation** (Blur, Noise, Low-res) to your training pipeline.
*   **Q: You need to detect thousands of tiny objects in a 4K satellite image. What approach do you take?**
    - *A:* Sliding windows or "Tiled Inference." Divide the 4K image into overlapping $640\times640$ patches, run detection on each, and then merge the results using NMS.

---

## 3. General Theory 🧪

*   **Q: Sliding Window vs. RPN (Region Proposal Network)?**
    - *A:* Sliding window is a brute-force approach (checking every location). RPN (in Faster R-CNN) is a small neural network that *learns* where interesting regions are, making it significantly more efficient.
*   **Q: What is a "Ghost Prediction"?**
    - *A:* When a tracker continues an object's path even if it has disappeared or been occluded for too long.

---

## 🎯 CV Engineering Cheat Sheet
1. **Best for Speed**: YOLOv8 / YOLOv10.
2. **Best for Detail**: Mask R-CNN.
3. **Best for Zero-Shot**: SAM (Segment Anything).
4. **Best for Small Devices**: MediaPipe / MobileNet.
