# Loss Functions for Segmentation 📉

In semantic segmentation, we often deal with **class imbalance** (e.g., a background making up 90% of the image). Standard Cross-Entropy fails here.

## 1. Cross-Entropy Loss
- **Best for**: Balanced datasets.
- **Problem**: In a medical scan with 1% tumor pixels, the model can achieve 99% accuracy by just predicting "Background" for every pixel.

## 2. Dice Loss
- **Based on**: The Dice Coefficient (Sørensen–Dice index).
- **Formula**: `2 * (Intersection) / (Sum of areas)`.
- **Why**: It is essentially a measure of overlap. It ignores the true negatives (background), focusing only on the target class.

## 3. Focal Loss
- **Origin**: RetinaNet.
- **How**: It adds a factor to standard Cross-Entropy that gives less weight to "easy" examples (well-classified pixels) and more weight to "hard" examples.

---

## 💻 PyTorch Implementation: Dice Loss

```python
import torch
import torch.nn as nn

class DiceLoss(nn.Module):
    def __init__(self, smooth=1e-6):
        super(DiceLoss, self).__init__()
        self.smooth = smooth

    def forward(self, predict, target):
        predict = torch.sigmoid(predict)
        
        # Flatten label and prediction tensors
        predict = predict.view(-1)
        target = target.view(-1)
        
        intersection = (predict * target).sum()
        dice = (2. * intersection + self.smooth) / (predict.sum() + target.sum() + self.smooth)
        
        return 1 - dice
```

### Loss Comparison

| Loss Function | Use Case | Handling Imbalance |
| :--- | :--- | :--- |
| **Cross-Entropy** | General purpose | Weak |
| **Dice Loss** | Medical / Small objects | Excellent |
| **Focal Loss** | High foreground-background ratio | Good |
| **BCE + Dice** | Hybrid (Standard practice) | Very Good |
