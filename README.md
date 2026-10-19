<div align="center">

# Crime Detector

### Real-time weapon and violence detection from a live camera feed with YOLOv8 and MediaPipe Pose.

<p>
  <img src="https://img.shields.io/badge/Python-1E293B?style=for-the-badge&logo=python&logoColor=FFD43B" alt="Python" />
  <img src="https://img.shields.io/badge/YOLOv8-111111?style=for-the-badge&logo=ultralytics&logoColor=white" alt="YOLOv8" />
  <img src="https://img.shields.io/badge/OpenCV-1A1A1A?style=for-the-badge&logo=opencv&logoColor=5C3EE8" alt="OpenCV" />
  <img src="https://img.shields.io/badge/MediaPipe-1F2937?style=for-the-badge&logo=google&logoColor=white" alt="MediaPipe" />
  <img src="https://img.shields.io/badge/PyTorch-1C1C1C?style=for-the-badge&logo=pytorch&logoColor=EE4C2C" alt="PyTorch" />
</p>

</div>

---

## ✨ Overview

**Crime Detector** is a computer-vision prototype for public-safety monitoring. It reads frames from a webcam, uses **YOLOv8** to detect people and weapon-class objects, and applies **MediaPipe Pose** heuristics to flag possible physical violence between people in the frame. When something is flagged, it draws a warning overlay and saves the frame as evidence.

## 🚀 Features

- **Weapon detection**: YOLOv8 detections are filtered to crime-relevant classes. Weapon hits (e.g. `knife`, `scissors`) get a red **WARNING: WEAPON!** box.
- **Pose-based violence scoring**: when at least two people are in view, per-person pose landmarks are compared frame to frame to spot:
  - **Punching**: a fast-moving wrist close to another person's head or neck
  - **Grabbing**: a hand held near another person's collar or neck
  - **Kicking**: a fast-moving ankle close to another person's hips
  - **Dashing**: one body moving rapidly toward another
- **Two alert levels**: a score of 80 or more is labelled **VIOLENCE: FIGHTING** (red); a score of 50 to 79 is labelled **SUSPICIOUS ACTIVITY** (yellow).
- **Evidence capture**: the flagged frame is saved to `crime_scene.jpg` and a warning is printed to the console.

> **Note:** the default `yolov8n.pt` is the standard COCO-pretrained model. Its weapon-like classes are `knife` and `scissors`. The `gun`, `pistol` and `rifle` labels in the code only fire with a custom-trained firearm model.

## 🧱 Tech Stack

- **Language:** Python
- **Detection:** Ultralytics YOLOv8 (`yolov8n.pt`)
- **Pose estimation:** MediaPipe Pose
- **Video & drawing:** OpenCV
- **Math:** NumPy
- **Runtime:** PyTorch (through Ultralytics)

## 🗂️ Project Structure

```
Crime_detector-/
├── proto_detect.py     # main detection loop (YOLOv8 + MediaPipe Pose)
├── requirements.txt    # pinned dependencies
└── alerts/
    └── sample_alert.json   # example alert record (timestamp, class, confidence, bbox)

# yolov8n.pt is downloaded automatically by Ultralytics on first run
```

## ⚡ Getting Started

**Prerequisites:** Python 3.10+ and a webcam.

```bash
git clone https://github.com/ShoaebMalik19/Crime_detector-.git
cd Crime_detector-

python -m venv venv
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate

pip install -r requirements.txt
python proto_detect.py
```

Press **`q`** to quit the video window.

## 🛣️ Roadmap

- Train or fine-tune a firearm-detection model so the gun, pistol and rifle classes work
- Send alerts to an external channel (SMS, webhook or dashboard) instead of the console only
- Support RTSP and CCTV streams in addition to the local webcam

## 👤 Author

**Mohammed Shoaeb Malik** · AI & full-stack developer, Bengaluru
GitHub: [@ShoaebMalik19](https://github.com/ShoaebMalik19)
