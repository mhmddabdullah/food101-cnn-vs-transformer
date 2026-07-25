Food-101 Image Classification: CNN vs. Vision Transformer Fine-Tuning Comparison

A systematic comparison of three deep learning architectures — two CNNs and one Vision Transformer — on the Food-101 image classification dataset, each evaluated under three progressively deeper fine-tuning strategies for a full 3×3 experimental grid.

Overview:
This project benchmarks how CNN and transformer-based architectures respond to different transfer-learning depths on a large-scale, fine-grained image classification task. Rather than fine-tuning each model a single way, every architecture was trained under three configurations — from training only the classification head to unfreezing progressively larger portions of the backbone — to isolate how much of each model's pretrained representation needs to be adapted for strong performance on food imagery.

Dataset:
Food-101 — 101 food categories, 101,000 images total (750 training / 250 test images per class), sourced from real-world, noisy web photography.

Models & Fine-Tuning Strategies:
Model	V1 (head only)	V2 (intermediate)	V3 (larger unfreeze)

- MobileNetV3-Large	classifier only	features[-3:] + classifier	features[-6:] + Dropout(0.3) + classifier
- EfficientNet-B0	classifier only	features[8] + classifier	features[6,7,8] + Dropout(0.25) + classifier
- Swin-Tiny	head only	norm + head	layers[3] + norm + head
  
V1 freezes the entire pretrained backbone and trains only the classification head — the cheapest configuration, testing how well off-the-shelf ImageNet features transfer to food imagery without adaptation.
V2 unfreezes a small set of late-stage layers alongside the head, allowing limited adaptation of higher-level features.
V3 unfreezes a larger portion of the backbone (with added dropout for regularization on MobileNetV3 and EfficientNet-B0), allowing deeper representation adaptation at higher risk of overfitting.
