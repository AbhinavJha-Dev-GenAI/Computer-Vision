# Metrics & Post-Processing ðŸ“ˆ

Evaluation in Object Detection is more complex than simple Accuracy because we must evaluate both **localization** and **classification**.

## 1. IoU (Intersection over Union)
Measures the overlap between the Predicted box and the Ground Truth box.
- **Formula**: `Area of Overlap / Area of Union`.
- **Threshold**: Usually 0.5. If IoU > 0.5, the detection is considered a True Positive (TP).

## 2. mAP (Mean Average Precision)
The primary metric for Object Detection.
- **Precision**: How many of the boxes we predicted are correct?
- **Recall**: How many of the total objects did we actually find?
- **mAP**: The area under the Precision-Recall curve, averaged over all classes. Usually reported as `mAP@50` or `mAP@50:95`.

## 3. NMS (Non-Maximum Suppression)
A post-processing step to remove redundant or overlapping boxes.
- **Problem**: A model might predict 5 boxes for the same cat.
- **Solution**: Keep the box with the highest confidence and remove all other boxes that have a high IoU with it.

---

## ðŸ’» Python Visualization: IoU Logic

```python
def calculate_iou(boxA, boxB):
    # Determine the (x, y)-coordinates of the intersection rectangle
    xA = max(boxA[0], boxB[0])
    yA = max(boxA[1], boxB[1])
    xB = min(boxA[2], boxB[2])
    yB = min(boxA[3], boxB[3])

    # Compute the area of intersection
    interArea = max(0, xB - xA + 1) * max(0, yB - yA + 1)

    # Compute the area of both rectangles
    boxAArea = (boxA[2] - boxA[0] + 1) * (boxA[3] - boxA[1] + 1)
    boxBArea = (boxB[2] - boxB[0] + 1) * (boxB[3] - boxB[1] + 1)

    # Compute IoU
    iou = interArea / float(boxAArea + boxBArea - interArea)
    return iou
```

### Interpretation Table

| Metric | Result | Meaning |
| :--- | :--- | :--- |
| **High IoU** | > 0.7 | Model is localized very accurately. |
| **High Precision**| low FP | Rarely makes mistakes in classification. |
| **High Recall** | low FN | Rarely misses objects. |
