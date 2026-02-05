# Plate Vision — Automatic License Plate Detection & Recognition

## Overview

Plate Vision is a computer vision system for **license plate detection, tracking, and recognition from video**. The project processes a video stream, detects vehicles, assigns consistent IDs across frames, localizes license plates, reads plate numbers using OCR, and produces structured CSV outputs and an annotated video.

This project demonstrates a **full end‑to‑end LPR pipeline**, not just detection: it combines object detection, multi‑object tracking, OCR post‑processing, temporal interpolation, and visualization.

---

## System Pipeline

The system follows the pipeline below:

1. **Vehicle Detection**
   Vehicles are detected using **YOLOv8 (COCO pretrained)**. Only vehicle classes (car, bus, truck, motorcycle) are retained.

2. **Vehicle Tracking**
   Detected vehicles are tracked across frames using **SORT**, assigning a stable `car_id` to each vehicle.

3. **License Plate Detection**
   A custom YOLO model detects license plates within each frame.

4. **License Plate–Vehicle Association**
   Each detected license plate is assigned to a tracked vehicle based on spatial containment.

5. **OCR (Optical Character Recognition)**
   License plates are cropped and processed using **EasyOCR** to extract plate text and confidence scores.

6. **Plate Validation & Correction**
   OCR results are validated against a predefined license format. Common OCR confusions (e.g., O↔0, I↔1) are corrected using rule‑based mappings.

7. **Temporal Interpolation**
   Missing bounding boxes across frames are filled using **linear interpolation**, ensuring temporal continuity for visualization and analysis.

8. **Visualization & Output**
   Final results are written to CSV files and rendered into an annotated output video showing tracked vehicles, license plates, and recognized numbers.

---

## Project Structure

```
plate-vision/
├── README.md
├── requirements.txt
├── demo/
│   └── demo_video.mp4
├── src/
│   └── __init__.py
├── tracking/
│   └── __init__.py
├── sort/
│   └── sort.py
├── main.py
├── util.py
├── visualize.py
└── add_missing_data.py
```

---

## OCR Module Details

* OCR is performed using **EasyOCR**.
* Detected text is normalized (uppercase, whitespace removed).
* Plate format validation is applied before accepting results.
* Character correction mappings handle common misclassifications:

  * O ↔ 0
  * I ↔ 1
  * A ↔ 4
  * S ↔ 5
* For each vehicle, the **highest‑confidence license plate reading across frames** is selected as the final result.

---

## Outputs

The system produces:

* `test.csv` — raw detection and OCR results per frame
* `test_interpolated.csv` — temporally interpolated bounding boxes
* `out.mp4` — final annotated video with tracked vehicles and license plate numbers

---

## How to Run

1. Install dependencies:

```bash
pip install -r requirements.txt
```

2. Run detection, tracking, and OCR:

```bash
python main.py
```

3. Interpolate missing bounding boxes:

```bash
python add_missing_data.py
```

4. Generate the annotated output video:

```bash
python visualize.py
```

---

## Demo

A demonstration video showcasing real‑time vehicle tracking and license plate recognition is available in the `demo/` directory.

---

## Notes

* This project focuses on **system integration and pipeline design**, not model training.
* Models are treated as external components and can be replaced or upgraded without modifying the pipeline logic.
* The codebase is intentionally kept modular to allow future extensions (e.g., different OCR engines or tracking algorithms).

---

## License

This project is intended for educational and research purposes.

