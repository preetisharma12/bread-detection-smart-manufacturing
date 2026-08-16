# Bread Detection for Smart Manufacturing

Before publishing this repo: this work was done at Fraunhofer IOSB-INA. Written confirmation from the supervisor/IP office that this can be public (code, write-up, and any images) has not yet been obtained. Confirmed directly: the trained model weights were produced using Fraunhofer's proprietary in-house bakery dataset, so the weights, the real detection images, and the real class names are intentionally withheld here, not just the raw dataset. Until confirmation is in hand, this repo intentionally contains no proprietary datasets, model weights, internal images, real metrics, or client-identifying details -- only a generic technical description of the approach, plus placeholders marked below for what will be filled in once cleared.

One-line description: YOLO-based computer vision system that classifies bread products on a manufacturing line into 7 classes, developed for industrial bakery deployment.

## Project Overview

This project applies object detection to an industrial bakery use case: classifying bread products in real time on a production line. It was built as part of work in the AI & Industrial Automation group at Fraunhofer IOSB-INA.

## Problem Statement

Missing -- please provide. What specific problem does classification solve on the line: quality control, sorting, inventory counting, defect detection? The technical approach (YOLO-based classification across 7 bread classes) is documented below, but not yet the business/operational problem it addresses.

## Key Features

Object detection and classification across 7 bread classes. A dataset collected and labeled specifically for this task. Models trained and optimized in PyTorch using Ultralytics YOLO. A lightweight web-based live camera view with on-demand detection capture. A deployment-focused investigation of camera height, image quality, and real-world manufacturing-floor conditions. Evaluation with precision, recall, mAP, and confusion matrix.

## System Architecture

A camera feed is captured and served as a live MJPEG stream through a small web application. On each detection request, the current frame is cropped to a configurable region of interest (to focus on the relevant counter/line area) and passed to the YOLO model for inference at a fixed confidence and IoU threshold. Each detection saves three artifacts: the raw cropped frame, a YOLO-format label file (class ID plus normalized bounding box), and a separate human-readable annotated copy with boxes drawn on it for quickly spotting mistakes. The raw image and label pair is intentionally kept separate from the annotated copy so it can be manually corrected and fed back into future training -- an active-learning-style feedback loop rather than a one-shot trained-and-forgotten model. Detection results (class counts per detection) are also logged for later review. The service is designed to run continuously as a background system service.

## Technologies

PyTorch and Ultralytics YOLO for the detection model. A lightweight Python web framework for the live camera view and detection endpoint. OpenCV for camera capture and image processing.

## Dataset

A custom dataset was collected and labeled in-house for 7 bread classes. Missing -- please provide (and consider before publishing): number of images per class, labeling tool used, and -- importantly -- whether this dataset or even sample images are allowed to be published. If not, this section should describe the dataset generically (e.g. "images captured on-site at a bakery production line, various lighting/angle conditions") without including the actual data.

## Methodology

Data collection and labeling across 7 bread classes, model training and fine-tuning with Ultralytics YOLO in PyTorch, deployment-condition testing (camera height, image quality, lighting/real-world variation), and evaluation via precision, recall, mAP, and confusion matrix. At inference time, the deployed system applies a fixed confidence/IoU threshold to filter detections and includes a human-in-the-loop correction mechanism: every detection is logged as both a raw image and a YOLO-format label file specifically so it can be manually corrected and reused as future training data.

Missing -- please provide: which YOLO variant(s) were used, training hyperparameters, and how deployment testing was actually conducted (fixed test rig? live line?).

## Installation

Missing -- needs input once the codebase exists in a publishable form (dependency list, environment setup).

## Usage

Missing -- needs input, same caveat as above -- real commands once the codebase is reconstructed in a publishable form.

## Project Structure

Recommended structure once rebuilt as a standalone public project:

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

Missing -- do not publish without real numbers. No precision/recall/mAP figures have been provided for this project, so none are included here.

## Evaluation Metrics

Metrics used: precision, recall, mAP, confusion matrix. Numeric results still needed.

## Example Outputs

Missing -- please provide, ideally sample detection images (with bounding boxes) using non-sensitive or synthetic examples if the real production images can't be published.

## Limitations

Missing -- please provide. Deployment challenges around camera height and image quality were mentioned; turning those into explicit, honest limitations (e.g. "accuracy drops under X lighting condition" or "requires camera mounted within Y range") is exactly the kind of engineering honesty that reads well to reviewers.

## Future Improvements

Extending the active-learning feedback loop (correcting logged detections and retraining on them) into a more automated retraining pipeline. Beyond that: missing -- please provide any other improvements you have in mind.

## License

MIT - see LICENSE.

## Author

Preeti Sharma - Research Assistant, AI & Industrial Automation, Fraunhofer IOSB-INA, Lemgo, Germany.
(Add any required Fraunhofer attribution/disclaimer language here once the supervisor confirms what's needed for a public repo.)
