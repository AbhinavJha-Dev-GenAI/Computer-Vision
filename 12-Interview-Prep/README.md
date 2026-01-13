# 12. CV Interview Prep 🎓

Preparing for an ML/AI Engineer role with a focus on Computer Vision? Here are common topics you'll encounter.

## 🔷 1. Foundations
- How does a Convolutional layer work? Explain padding and stride.
- What is the difference between a 1x1 convolution and a standard 3x3 convolution?
- Explain the vanishing gradient problem and how ResNet solves it.

## 🔷 2. Object Detection
- Describe the difference between One-stage and Two-stage detectors.
- What is Non-Maximum Suppression (NMS) and why do we need it?
- Explain mAP (Mean Average Precision). How is it different at @50 vs @50:95?

## 🔷 3. Segmentation
- What are Skip Connections in U-Net and why are they important?
- How does Mask R-CNN differ from Faster R-CNN?
- What is Dice Loss and when should you use it over Cross-Entropy?

## 🔷 4. Deployment & Edge
- How do you optimize a model for inference on a mobile device? (Quantization, Pruning).
- What is the difference between FP32, FP16, and INT8 precision?
- Have you used TensorRT? How much speedup did you achieve?

---

## 📈 Tips for the Interview
- **Architecture knowledge**: Be ready to draw the architecture of YOLO or U-Net on a whiteboard.
- **Dataset knowledge**: Know your COCO, Pascal VOC, and ImageNet stats.
- **Hands-on experience**: Talk about the specific trade-offs you made in your projects (e.g., "I chose YOLOv8n because I needed 30 FPS on a Raspberry Pi").

> [!TIP]
> **Practical Test**: You might be asked to implement a simple convolution or IoU calculation in pure NumPy. Practice that!
