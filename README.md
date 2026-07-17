# Automatically Segment and Label Objects in Video

Comparing classical and deep-learning-based vehicle detectors for automated video labeling using MATLAB's Video Labeler app.

## Motivation

Building robust AI models for tasks like self-driving vehicles requires large amounts of labeled video data. Manually drawing bounding boxes on every object in every frame is extremely slow. This project explores how much of that work can be automated using existing detection algorithms, and how much manual review is still needed.

## What I Did

1. Loaded a sample traffic video (531 frames) into MATLAB's **Video Labeler** app.
2. Manually labeled a vehicle in a sample frame to understand the baseline manual labeling workflow.
3. Ran the built-in **ACF Vehicle Detector** (a classical, feature-based detector) as an automation algorithm across the full video.
4. Ran a pretrained **YOLOv2 vehicle detector** (a deep-learning-based detector) across the same video for comparison.
5. Measured and compared detection performance between the two methods.
6. Exported an annotated demo video showing the YOLOv2 detector's output.

## Results

| Detector | Frames with ≥1 Detection | Detection Rate |
|---|---|---|
| ACF Vehicle Detector | 16 / 531 | 3.0% |
| YOLOv2 (Deep Learning) | 224 / 531 | 42.2% |

Additional breakdown for YOLOv2:
- Frames with 0 detections: 307
- Frames with exactly 1 detection: 213
- Frames with 2+ detections: 11
- Total individual vehicle detections: 235

**YOLOv2 outperformed the classical ACF detector by roughly 14x** in terms of frame-level detection rate on this video.

## Files in This Repository

- `yolov2_detections.avi` — Annotated output video with bounding boxes and confidence scores from the YOLOv2 detector.
- `project_results.mat` — Saved MATLAB variables containing the raw detection counts for both detectors.

## Limitations

- Even the better-performing YOLOv2 detector missed vehicles in more than half of all frames, likely due to the elevated camera angle and relatively small size of vehicles in the frame — conditions that differ from typical training data for this pretrained model.
- Neither detector was fine-tuned on this specific footage; a custom-trained model would likely perform significantly better.
- A real-world deployment of this pipeline would still require a human review/correction pass, though this would be substantially faster than labeling every frame manually from scratch.

## Tools Used

- MATLAB R2025b
- Computer Vision Toolbox
- Deep Learning Toolbox
- Video Labeler app

## Why I Chose This Project

I picked this project to get hands-on experience with automated video labeling using MATLAB's Video Labeler and Computer Vision Toolbox. Comparing a classical detector (ACF) against a deep-learning detector (YOLOv2) let me directly measure real accuracy tradeoffs instead of just reading about them.
