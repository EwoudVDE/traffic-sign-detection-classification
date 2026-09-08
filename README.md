# Traffic Sign Detection & Classification

Computer vision project for detecting and classifying Belgian traffic signs using **YOLO**, with additional experiments using **CBAM attention** and **class activation maps**.

## Overview

The goal of this project was to build a complete object detection pipeline for Belgian traffic signs using the **BelgiumTS** dataset.

The project covered the full workflow from raw dataset preparation to training and evaluating YOLO models:

- Selecting a reduced set of traffic sign classes
- Converting dataset annotations to YOLO format
- Preparing training and validation datasets
- Training YOLO object detection models
- Experimenting with different model configurations and hyperparameters
- Exploring CBAM attention mechanisms
- Visualizing model behaviour using class activation maps

---

## Approach

### 1. Dataset Preparation

The project uses the **BelgiumTS** traffic sign dataset.

Several preprocessing scripts were created to prepare the original dataset for YOLO training:

- `reducedSet.py` — filters the dataset to selected traffic sign classes
- `YOLOConversion.py` — converts the original annotations to YOLO format
- `split.py` — creates an 80% training / 20% validation split
- `rewriteIds.py` — remaps class IDs to the reduced label set
- `convertToJpg.py` — converts `.jp2` images to `.jpg` for YOLO compatibility

This preprocessing pipeline transforms the original dataset into a structure that can directly be used for YOLO training.

---

### 2. YOLO Training

YOLO models were trained for traffic sign detection and classification.

The training setup supports experimenting with different model variants, including models such as:

- YOLOv8
- YOLO11

Model selection and hyperparameters can be changed in the training configuration to compare different setups.

GPU availability can be checked using the included `cuda.py` script before starting training.

---

### 3. CBAM Attention

The project also includes experiments with **CBAM (Convolutional Block Attention Module)**.

A modified Ultralytics YOLOv8 implementation is included as a Git submodule and used to experiment with adding attention mechanisms to the detection architecture.

The corresponding model configuration is available in:

`yolov8-CBAM.yaml`

The goal of these experiments was to explore whether attention mechanisms could help the model focus more effectively on relevant visual features.

---

### 4. Class Activation Maps

Class activation maps were explored to better understand which regions of an image influence the model's predictions.

The project uses **YOLO-V11-CAM** for these visualizations.

This provides additional insight into how the detector responds to traffic sign features instead of only evaluating the final bounding-box predictions.

---

## My Work

My work on this project included:

- Preparing and preprocessing the BelgiumTS dataset
- Converting annotations to YOLO format
- Building the train / validation dataset split
- Training YOLO traffic sign detection models
- Experimenting with different YOLO model configurations and hyperparameters
- Exploring CBAM attention mechanisms
- Working with class activation maps to inspect model behaviour
- Testing trained models on images and video

---

## Project Structure

```text
traffic-sign-detection-classification/
│
├── scripts/
│   ├── reducedSet.py
│   ├── YOLOConversion.py
│   ├── split.py
│   ├── rewriteIds.py
│   ├── convertToJpg.py
│   ├── train.py
│   ├── cuda.py
│   └── video.py
│
├── ultralytics/          # Modified Ultralytics submodule for CBAM experiments
├── annotations.txt
├── data.yaml
├── defined.txt
├── requirements.txt
├── yolov8-CBAM.yaml
└── README.md
```

---

## Technologies

- Python
- YOLOv8 / YOLO11
- Ultralytics
- Computer Vision
- Object Detection
- Deep Learning
- CBAM
- Class Activation Maps
- CUDA
- Git / GitHub

---

## Setup

### 1. Download the Dataset

Download and extract the required files from the **BelgiumTS** dataset:

- `DefinedTS.tar.gz`
- `reducedSetTS.txt`
- `Annotations/camera00.tar` through `camera07.tar`
- `Annotations/annotations.tar`
- `Annotations/BelgiumTSD_annotations.zip`

Place the images in an `/images` folder.

### 2. Install Dependencies

```bash
pip install -r requirements.txt
git submodule update --init --recursive
```

### 3. Preprocess the Dataset

Run the preprocessing scripts in this order:

```text
reducedSet.py
YOLOConversion.py
split.py
rewriteIds.py
convertToJpg.py
```

### 4. Train a Model

Use `cuda.py` to check whether your GPU is available.

Then use `train.py` to start training.

The training script can be modified to use different YOLO models and hyperparameters.

### 5. Test the Model

A trained model can be tested with the Ultralytics CLI:

```bash
yolo detect predict model=path/to/model.pt source=path/to/image.png
```

The included `video.py` script can also be used to test the model on video input.

---

## Dataset

This project uses the **BelgiumTS** dataset by Radu Timofte and collaborators.

Dataset website:

https://btsd.ethz.ch/shareddata/

---

## Third-Party Code

### Ultralytics YOLOv8

A modified version of Ultralytics YOLOv8 is included for the CBAM experiments.

- Purpose: CBAM integration
- License: AGPL-3.0
- Original project: `ultralytics/ultralytics`

### YOLO-V11-CAM

YOLO-V11-CAM is used for class activation map experiments.

- Purpose: Class activation maps
- License: MIT

---

## Notes

This repository documents both the practical object detection pipeline and additional experiments around model attention and interpretability.

The main focus of the project was gaining hands-on experience with the complete computer vision workflow: **dataset preparation → model training → evaluation → experimentation → inference**.
