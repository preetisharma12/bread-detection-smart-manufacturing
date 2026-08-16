# Bread Detection for Smart Manufacturing

 YOLO-based computer vision system that classifies bread products on a manufacturing line into 7 classes, developed for industrial bakery deployment.

## Project Overview

This project applies object detection to an industrial bakery use case: classifying bread products in real time on a production line.
Automated bread detection and classification for bakery production lines using YOLO-based computer vision.
Detects and classifies 7 different bread types in real-time.
Reduces manual inspection and supports automated counting, sorting, and quality monitoring.
Improves robustness across different camera distances, viewpoints, and production conditions.
Uses Intel RealSense D455 for deployment in real-world bakery environments.

## Problem Statement

A robust computer vision system is needed to automatically detect and classify bread products in real-world production conditions.

## Key Features

Object detection and classification across 7 bread classes. A dataset collected and labeled specifically for this task. Models trained and optimized in PyTorch using Ultralytics YOLO. A lightweight web-based live camera view with on-demand detection capture. A deployment-focused investigation of camera height, image quality, and real-world manufacturing-floor conditions. Evaluation with precision, recall, mAP, and confusion matrix.

## System Architecture

A camera feed is captured and served as a live MJPEG stream through a small web application. On each detection request, the current frame is cropped to a configurable region of interest (to focus on the relevant counter/line area) and passed to the YOLO model for inference at a fixed confidence and IoU threshold. Each detection saves three artifacts: the raw cropped frame, a YOLO-format label file (class ID plus normalized bounding box), and a separate human-readable annotated copy with boxes drawn on it for quickly spotting mistakes. The raw image and label pair is intentionally kept separate from the annotated copy so it can be manually corrected and fed back into future training -- an active-learning-style feedback loop rather than a one-shot trained-and-forgotten model. Detection results (class counts per detection) are also logged for later review. The service is designed to run continuously as a background system service.

## Technologies

PyTorch and Ultralytics YOLO (yolo26m) for the detection model. A lightweight Python web framework for the live camera view and detection endpoint. OpenCV for camera capture and image processing.

## Dataset

10,000 images collected and labeled in-house from a bakery production environment.
Covers 7 bread classes with images captured at different heights, angles, backgrounds, and lighting conditions.
Annotations were created using CVAT.
Dataset designed to improve model robustness under real-world production conditions.
Dataset/images are not publicly published due to confidentiality.

## Methodology

Data collection and labeling across 7 bread classes, model training and fine-tuning with Ultralytics YOLO in PyTorch, deployment-condition testing (camera height, image quality, lighting/real-world variation), and evaluation via precision, recall, mAP, and confusion matrix. At inference time, the deployed system applies a fixed confidence/IoU threshold to filter detections and includes a human-in-the-loop correction mechanism: every detection is logged as both a raw image and a YOLO-format label file specifically so it can be manually corrected and reused as future training data.

YOLO variant - yolo26m 

training hyperparameters

yolo detect train \
model=/data/pool/bhe-mk3/runs/bread_yolo26m/weights/best.pt \
data=/data/pool/bhe-mk3/breadbakery/Bread.yolov8/data.yaml \
epochs=120 \
imgsz=640 \
batch=16 \
device=0 \
workers=8 \
patience=20 \
project=/data/pool/bhe-mk3/runs \
name=bread_yolo26m_finetune \
optimizer=auto \
hsv_h=0.01 \
hsv_s=0.30 \
hsv_v=0.15 \
fliplr=0.5 \
flipud=0.5 \
degrees=5 \
translate=0.05 \
scale=0.10 \
mosaic=0 \
mixup=0 \
copy_paste=0

## Installation

Missing -- needs input once the codebase exists in a publishable form (dependency list, environment setup).



## Project Structure
```
bread-detection-smart-manufacturing/
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
├── configs/          # YOLO training configs
├── data/             # sample/synthetic images only, not the real production dataset
├── src/              # data loading, training, inference code
├── scripts/          # train.py, evaluate.py, infer.py entry points
├── notebooks/        # exploratory analysis, if useful to show
├── results/          # confusion matrix, PR curves, sample metric outputs
└── tests/
```

## Results

<img width="1920" height="1100" alt="val_batch1_pred" src="https://github.com/user-attachments/assets/2fb93ae5-4036-44ae-b9bf-7222f698cecb" />





<img width="1920" height="1100" alt="val_batch2_labels" src="https://github.com/user-attachments/assets/a029ad43-a22c-4459-abab-21816140d41f" />




## Evaluation Metrics

Metrics used: precision, recall, mAP, confusion matrix. 

## Future Improvements

Extending the active-learning feedback loop (correcting logged detections and retraining on them) into a more automated retraining pipeline.

## License

MIT - see LICENSE.

## Author

Preeti Sharma - Research Assistant, AI & Industrial Automation, Fraunhofer IOSB-INA, Lemgo, Germany.
