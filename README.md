# Polyp Detection on Kvasir

This repository contains a small study on polyp localization in colonoscopy images
from the Kvasir-SEG dataset. We compare two approaches:

1. Direct bounding-box regression
2. Weakly supervised segmentation
3. YOLO based model

The project is carried out as part of the "Deep Learning in Medical Imaging" course.

## Dataset

We use a Kvasir-based polyp dataset consisting of:

- Input: Raw colonoscopy images (`<id>.jpg`)
- Labels: Bounding-box annotations in CSV files (`<id>.csv`) with columns:
  `class_name, x_min, x_max, y_min, y_max`
- Additional: Annotated images with drawn boxes (for visualization only).

The original Kvasir-SEG dataset provides pixel-wise polyp masks and is intended for polyp detection and segmentation research. In our setup, we only use bounding-box labels and treat them as *weak supervision* for segmentation. 

Expected local folder structure (data not included in the repo):
data/
  raw/
    annotated_images/  # <id>.jpg
    bbox/              # <id>.csv
    images/            # <id>.jpg
  processed/

## Tasks & Methods

**Direct bounding-box regression**
- *Limited to 1 polyp per image!*
- Simple CNN or ResNet backbone predicting 4 output values (x_min, x_max, y_min, y_max)

**Weakly supervised segmentation**
- Segmentation model (e.g. U-Net)
- Boundary boxes serve as masks, making this a weakly-supervised setting with inexact labels. 
- Predictions can optionally be converted back to boundary boxes.

**YOLO-based**
- Depending on time capacity:
- Build YOLO-like model OR
- Fine-tune YOLO-like model OR
- Inference YOLO-like model
