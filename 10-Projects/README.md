# 10. Computer Vision Projects 🛠️📸

Turn theory into reality with these hands-on, portfolio-ready projects.

## Project 1: Real-time PPE Detector (YOLOv8) 👷‍♂️
*   **Goal**: Detect if workers on a construction site are wearing Helmets, Vests, and Safety Boots.
*   **Tech Stack**: YOLOv8, PyTorch, Custom Datasets (Roboflow).
*   **Key Learning**: Custom object detection, dataset labeling, and real-time inference on a video stream.

## Project 2: Automatic License Plate Recognition (ALPR) 🚗
*   **Goal**: Detect vehicles, crop their license plates, and extract the alphanumeric characters.
*   **Tech Stack**: YOLOv8 (Detection) + PaddleOCR (Recognition).
*   **Key Learning**: Pipeline chaining (output of one model is input to another) and OCR optimization.

## Project 3: Virtual Try-On Assistant (Pose + Segmentation) 👕
*   **Goal**: Track a person's body posing and overlay a virtual "T-shirt" that moves realistically.
*   **Tech Stack**: MediaPipe (Pose) + Segment Anything Model (SAM).
*   **Key Learning**: Combining pose keypoints with high-fidelity masks.

## Project 4: Sports Action Annotator (DeepSORT) 🏀
*   **Goal**: Automatically track players during a basketball game and calculate their "Distance Traveled" and "Average Speed."
*   **Tech Stack**: YOLOv8 + ByteTrack / DeepSORT.
*   **Key Learning**: Multi-Object Tracking, handling occlusions, and temporal analysis.

---

## 🚀 Getting Started
1.  **Datasets**: Use **Roboflow Universe** to find pre-labeled datasets for almost any vision task.
2.  **Hardware**: If you don't have an NVIDIA GPU, use **Google Colab** to train your models.
3.  **Deployment**: Try deploying your project as a live web app using **Streamlit**—it's very vision-friendly!
