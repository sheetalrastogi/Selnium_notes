# List of Tools for Computer Vision in Python

## Core Computer Vision Libraries

| Tool | Purpose |
|--------|---------|
| OpenCV (cv2) | Image processing, object detection, video analytics |
| scikit-image | Scientific image processing and analysis |
| Pillow (PIL) | Basic image manipulation and conversion |
| ImageIO | Image and video reading/writing |
| Mahotas | Computer vision and image processing algorithms |

---

## Deep Learning Based Computer Vision

| Tool | Purpose |
|--------|---------|
| PyTorch | Deep learning framework for CV models |
| TensorFlow | Deep learning and production deployment |
| KerasCV | Pre-built CV components and models |
| FastAI | High-level computer vision training |
| MXNet | Scalable deep learning framework |

---

## Object Detection & Segmentation

| Tool | Purpose |
|--------|---------|
| Ultralytics YOLO | Real-time object detection |
| Detectron2 | Facebook's detection and segmentation framework |
| MMDetection | OpenMMLab object detection toolkit |
| YOLOX | Advanced YOLO object detection |
| Segment Anything (SAM) | Image segmentation by Meta |

---

## OCR (Optical Character Recognition)

| Tool | Purpose |
|--------|---------|
| Tesseract OCR | Open-source OCR engine |
| EasyOCR | Deep-learning-based OCR |
| PaddleOCR | High-accuracy OCR framework |
| docTR | Document text recognition |
| OCRmyPDF | OCR for scanned PDFs |

---

## Face Recognition & Biometrics

| Tool | Purpose |
|--------|---------|
| face_recognition | Simple face recognition library |
| DeepFace | Face verification and analysis |
| InsightFace | Face recognition and detection |
| MediaPipe Face Mesh | Facial landmark detection |
| OpenFace | Face recognition toolkit |

---

## Pose & Gesture Detection

| Tool | Purpose |
|--------|---------|
| MediaPipe | Pose, hand, face tracking |
| OpenPose | Human pose estimation |
| MoveNet | Fast pose detection |
| MMPose | OpenMMLab pose estimation framework |

---

## Image Similarity & Visual Testing

| Tool | Purpose |
|--------|---------|
| SikuliX | Image-based UI automation |
| Applitools Eyes | AI-powered visual testing |
| Percy | Visual regression testing |
| Resemble.js | Image comparison |
| OpenCV Template Matching | Visual element identification |

---

## Document AI & Layout Analysis

| Tool | Purpose |
|--------|---------|
| LayoutParser | Document layout analysis |
| Donut | OCR-free document understanding |
| PaddleOCR | Form and document extraction |
| Amazon Textract SDK | Document intelligence |
| Azure AI Vision | OCR and document analysis |

---


# Install Common Computer Vision Tools in Python

## Upgrade pip

```bash
python -m pip install --upgrade pip
```

---

## Core Computer Vision Libraries

```bash
pip install opencv-python
pip install scikit-image
pip install pillow
pip install imageio
pip install mahotas
```

Or:

```bash
pip install opencv-python scikit-image pillow imageio mahotas
```

---

## Deep Learning Frameworks

### PyTorch

```bash
pip install torch torchvision torchaudio
```

### TensorFlow

```bash
pip install tensorflow
```

### FastAI

```bash
pip install fastai
```

### KerasCV

```bash
pip install keras-cv
```

---

## Object Detection & Segmentation

### YOLO (Ultralytics)

```bash
pip install ultralytics
```

### Detectron2

```bash
pip install detectron2
```

### MMDetection

```bash
pip install mmdet
```

### Segment Anything (SAM)

```bash
pip install segment-anything
```

---

## OCR Tools

### Tesseract Python Wrapper

```bash
pip install pytesseract
```

### EasyOCR

```bash
pip install easyocr
```

### PaddleOCR

```bash
pip install paddleocr
```

### docTR

```bash
pip install python-doctr
```

### OCRmyPDF

```bash
pip install ocrmypdf
```

---

## Face Recognition

### face_recognition

```bash
pip install face-recognition
```

### DeepFace

```bash
pip install deepface
```

### InsightFace

```bash
pip install insightface
```

---

## Pose & Gesture Detection

### MediaPipe

```bash
pip install mediapipe
```

### OpenPose Wrapper

```bash
pip install openpose-python
```

### MMPose

```bash
pip install mmpose
```

---

## Visual Testing & Image Similarity

### SikuliX (Java-based)

Download separately:

```text
https://sikulix.github.io/
```

### Percy

```bash
pip install percy-python-selenium
```

### Resemble (Python Alternative)

```bash
pip install ImageHash
```

---

## Document AI

### LayoutParser

```bash
pip install layoutparser
```

### Amazon Textract SDK

```bash
pip install boto3
```

### Azure AI Vision

```bash
pip install azure-ai-vision-imageanalysis
```

---

# One-Line Installation for QA Automation

```bash
pip install opencv-python pillow scikit-image ultralytics paddleocr pytesseract easyocr mediapipe face-recognition deepface layoutparser boto3 azure-ai-vision-imageanalysis
```

---

# Verify Installation

```bash
python -c "import cv2, torch, tensorflow, mediapipe, easyocr, paddleocr; print('All libraries installed successfully')"
```

---

# Create a Dedicated Virtual Environment

```bash
python -m venv cv-env

# Windows
cv-env\Scripts\activate

# Linux/Mac
source cv-env/bin/activate
```

Then install the required packages inside the virtual environment.



