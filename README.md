# YOLO-algorithms-Thesis
Comparative analysis of YOLOv8 architectural enhancements (CBAM vs. CoordConv) using the COCO 2017 dataset for object detection.

OVERVIEW
This repository contains the research, implementation, and evaluation of various architectural modifications to the YOLOv8 (You Only Look Once) framework. The primary goal of this thesis was to investigate whether integrating specialized modules—specifically Attention Mechanisms (CBAM) and Coordinate Convolutions (CoordConv)—could significantly improve detection performance on the complex MS COCO 2017 dataset.

The research focuses on the trade-off between architectural complexity, spatial awareness, and detection accuracy in real-time object detection systems.

📋 Table of Contents
Architectures

Dataset & Preprocessing

Experimental Setup

Current Results & Analysis

Future Work (Phase 2)

Installation & Usage

Project Structure

🏗 Architectures <a name="architectures"></a>
To isolate the impact of different structural changes, I developed and compared four distinct model variants based on the YOLOv8nano backbone:

Model A: The Baseline
Description: An unmodified YOLOv8n model.

Purpose: Served as the control group to establish a performance benchmark for the COCO 2017 subset.

Model B: YOLOv8 + CBAM (Attention)
Feature: Integrated the Convolutional Block Attention Module (CBAM).

Focus: This model applies both channel and spatial attention, allowing the network to focus on "what" is important and "where" the most informative features are located within the feature maps.

Model C: YOLOv8 + CoordConv (Spatial Awareness)
Feature: Replaced initial standard convolutions with Coordinate Convolutions.

Focus: [TOP PERFORMER] Standard convolutions are translation-invariant, which can be a disadvantage for precise localization. CoordConv gives the model explicit access to the coordinates of pixels, significantly improving spatial reasoning.

Model D: Combined Architecture
Feature: A hybrid model featuring both CBAM and CoordConv.

Focus: An attempt to achieve synergy between attention-based feature selection and coordinate-aware spatial localization.

📊 Dataset & Preprocessing <a name="dataset--preprocessing"></a>Source: Microsoft COCO 2017Subset Size: 50,000 images (Curated to ensure class diversity while managing computational constraints).Preprocessing: Images were resized to $640 \times 640$ pixels. Standard augmentations (mosaic, mixup, and flips) were applied via the Ultralytics pipeline to ensure model robustness.

⚙️ Experimental Setup <a name="experimental-setup"></a>
Environment: Kaggle Notebooks

Hardware: NVIDIA Tesla T4 GPU

Framework: ultralytics (YOLOv8)

Epochs: 50

Optimizer: SGD / AdamW (Auto-selected by YOLOv8)

Batch Size: 16 (optimized for T4 VRAM)


📈 Current Results & Analysis <a name="current-results--analysis"></a>
The initial phase of the thesis concluded with the following findings:

Model C (CoordConv) achieved the highest overall accuracy (mAP@50-95). This suggests that for general object detection on COCO, enhancing the model's spatial coordinate awareness is more effective than adding standard attention blocks.

Model B (CBAM) showed improvements in detecting smaller, textured objects but struggled with precise bounding box localization compared to Model C.

Model D (Combined) showed promising results but indicated signs of diminishing returns, suggesting that the added parameters require a more extensive training schedule to converge.

🚀 Future Work (Phase 2) <a name="future-work-phase-2"></a>
I am currently preparing for a second phase of experimentation to further refine these results. The upcoming work includes:

Data-to-Epoch Trade-off: I plan to reduce the dataset size to a highly concentrated sub-batch of 12,000–15,000 images.

Extended Training: With the smaller dataset, I will increase the training duration to 100–150 epochs. This will help determine if the models (particularly the Combined Model D) can reach a higher global minimum with more iterations on a more focused data sample.

Hyperparameter Tuning: Implementing a more aggressive learning rate decay and fine-tuning the augmentation ratios for the CoordConv layers.

Inference Speed Analysis: Measuring the Latency (ms) of each model to ensure the architectural changes do not compromise the "Real-Time" requirement of the YOLO family.


🛠 Installation & Usage <a name="installation--usage"></a>
To replicate this work, follow these steps:

Clone the repo:

Bash

git clone https://github.com/[YOUR-USERNAME]/[YOUR-REPO-NAME].git
cd [YOUR-REPO-NAME]
Install dependencies:

Bash

pip install -r requirements.txt
Run a Notebook:
Navigate to the notebooks/ directory and open any of the YOLO variants to view training logs or run inference.































