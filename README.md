# Adaptive XAI-Based Cow Detection with Uncertainty Estimation

This project was developed as a self-learning and experimentation exercise to explore **explainable artificial intelligence (XAI)** and **uncertainty estimation** in object detection models.  
The work focuses on cow detection in farm images and aims to understand not only *what* the model predicts, but also *how confident* it is and *which image regions influence each prediction*.

---

## Problem Motivation

Deep learning-based object detectors often produce high-confidence predictions, but:

- the **reasoning behind detections** is not transparent,
- the **reliability of predictions** is not explicitly quantified,
- incorrect but confident predictions can be difficult to identify.

In agricultural and animal-monitoring contexts, such limitations can reduce trust and practical usability.  
Therefore, combining **object detection**, **explainability**, and **uncertainty estimation** is an important step toward more reliable AI systems.

---

## Project Overview

The project consists of three main components:

1. **Object Detection**  
   A YOLO-based detector is used to localize cows in images.

2. **Explainability (Grad-CAM)**  
   For each detected bounding box, Grad-CAM heatmaps are generated to visualize which regions of the image contribute most to the detection.

3. **Uncertainty Estimation (MC Dropout)**  
   Monte Carlo Dropout is applied during inference to estimate epistemic uncertainty for each detected cow.  
   Variability in confidence scores and bounding box coordinates is used as a measure of uncertainty.

The final output combines:
- bounding boxes,
- uncertainty metrics,
- and explainability visualizations.

---

## Example Results

### Input Image
Example input images are provided in: assets/input_examples/

### Grad-CAM per Detection
Grad-CAM heatmaps are computed **per detected cow**, not globally for the image.  
This allows instance-level explanations. assets/xai_examples/
These heatmaps highlight image regions that most strongly influenced each individual detection.

### Uncertainty Visualization
Final images include bounding boxes annotated with uncertainty information derived from MC Dropout sampling.
assets/uncertainty_examples/

Each bounding box includes:
- detection confidence,
- confidence standard deviation,
- bounding box variability.

---

## Uncertainty Estimation Approach

Epistemic uncertainty is estimated using **Monte Carlo Dropout**:

- Dropout layers are activated during inference.
- Multiple stochastic forward passes are performed.
- Detection results are matched across samples using IoU.
- Uncertainty is computed as:
  - standard deviation of confidence scores,
  - mean standard deviation of bounding box coordinates.

This provides an indication of how stable the model’s predictions are under stochastic perturbations.

---

## Output Format

For each image, a structured JSON output is generated containing:
- bounding box coordinates,
- confidence scores,
- uncertainty metrics per detected object.

An example is available in: results/example_output.json
---

## Learning Outcomes

Through this project, the following concepts were explored and implemented:

- practical object detection using pretrained deep learning models,
- instance-level explainability with Grad-CAM,
- epistemic uncertainty estimation using MC Dropout,
- matching stochastic detections across multiple inference runs,
- interpretation of uncertainty in detection-based tasks.

The project helped bridge theoretical understanding of XAI and uncertainty with practical implementation challenges.

---

## Limitations and Future Work

- The uncertainty estimation relies on heuristic matching of detections across samples.
- Only epistemic uncertainty is considered; aleatoric uncertainty is not explicitly modeled.
- The current implementation is evaluated qualitatively rather than with quantitative uncertainty benchmarks.

Future extensions could include:
- ensemble-based uncertainty estimation,
- uncertainty-aware decision thresholds,
- integration into real-time monitoring systems.

---

## Implementation Note

The source code for this project is currently kept private, as the repository is intended to document **methodology, results, and learning outcomes** rather than provide a reusable software package.

---

## Author
Balaji Subburaj
Focus areas: Computer Vision, Explainable AI, and Uncertainty Estimation



