Plate Vision

Real-Time License Plate Detection & Tracking System

Overview

Plate Vision is a computer vision system designed to detect and track vehicle license plates in images and video streams.
The system combines a deep learning–based object detector with a multi-object tracking algorithm to achieve stable, real-time plate localization.

This project focuses on practical deployment, not just model training.

Problem Statement

Manual license plate monitoring is slow, error-prone, and does not scale.
This project addresses the problem by automating license plate detection and tracking using modern computer vision techniques.

System Pipeline

Input image or video

License plate detection using YOLOv8

Object tracking using SORT

Frame-by-frame visualization and result export

Technologies Used

Python 3

YOLOv8 (Ultralytics)

OpenCV

SORT tracking algorithm

NumPy

Project Structure
plate-vision/
├── main.py              # Entry point
├── util.py              # Helper functions
├── visualize.py         # Visualization logic
├── add_missing_data.py  # Dataset handling utilities
├── sort/
│   └── sort.py          # Tracking algorithm
├── requirements.txt
└── README.md

How to Run
python main.py


Note: Model weights and datasets are excluded from the repository to keep it lightweight and reproducible.

Future Improvements

OCR integration for plate text recognition

Performance optimization for edge devices

Model fine-tuning on country-specific plates

REST API for deployment

Author

Sharmarke Mohamed Ibrahim
Computer Engineering
