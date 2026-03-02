# Polyp Detection - Final Project (Deep Learning in Medical Imaging)
*Marco La Cagnina, Rime El Bahi, Niklas Kessler*

This repository contains a small study on polyp localization in colonoscopy images
from the Kvasir-SEG dataset. The project is carried out as part of the "Deep Learning in Medical Imaging" course.

**Problem Definition**: 

We address the problem of automatic polyp detection in colonoscopy images using the Kvasir-SEG dataset. Early detection of polyps is critical for preventing colorectal cancer, but polyps are often easily missed due to large appearance variability (size, shape, texture) and their visual similarity to the colon wall (camouflaging).

**Dataset:**

We use a Kvasir-based polyp dataset consisting of:

- Input: Raw colonoscopy images (`<id>.jpg`)
- Labels: Bounding-box annotations in CSV files (`<id>.csv`) with columns:
  `class_name, x_min, x_max, y_min, y_max`
- Additional: Annotated images with drawn boxes (for visualization only).

The original Kvasir-SEG dataset provides pixel-wise polyp masks and is intended for polyp detection and segmentation research. In our setup, we only use bounding-box labels and treat them as *weak supervision* for segmentation. 

**Expected File Structure:**

```
Experiments.ipynb
yolo_runs
checkpoints
|-model2_niklas_03_01_26
|-model4_niklas_04_01_26
Kvasir-SEG
|-annotated_images
|-bbox
|-images
|-yolo_dataset (will be generated)
```

**Objectives:**

1. Implement a detection model based on Faster R_CNN with a ResNet-50 and FPN backbone + quantile-anchors

2. Develop an Advanced Model improving on specific challenges:
- Geometric Adaptation: Using K-Means clustering to generate custom anchor box proposals for tiny/irregular polyps.
- Visual Enhancement: Using CLAHE to improve contrast.
- Replacing the backbone with hierarchical vision transformer (swin)

3. Compare performance using mAP and qualitative analysis.

We first explore the dataset and analyze the distribution of bounding box sizes to motivate the anchor design choices. We then implement preprocessing (including CLAHE) and fine-tune Faster R-CNN from pretrained weights under a controlled training setup. Next, we evaluate the baseline and the improved Faster R-CNN variant on a held-out test split using standard detection metrics (mAP) and qualitative examples. As an external reference, we also compare our results against a YOLO-based detector to contextualize accuracy–speed trade-offs.
