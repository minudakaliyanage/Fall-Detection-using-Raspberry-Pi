# Video-Based Fall Detection Model

## 📋 Overview

This directory contains the video-based fall detection system using computer vision and deep learning. The system processes real-time camera feeds or video files to detect falls using optimized TensorFlow Lite models and YOLOv5 object detection.

## 📁 Contents

### Model Files
- **Fall-Detector.h5** - Full TensorFlow model (training)
- **Fall-detector-lite.tflite** - TensorFlow Lite model (deployment)
- **yolov5s.pt** - YOLOv5 weights for object detection

### Scripts
- **real-time detector.py** - Real-time fall detection from camera
- **video-detector.py** - Fall detection from video files
- **Model.ipynb** - Model training and development notebook

### Data
- **my-video.mp4** - Sample video for testing

## 🏗️ Model Architecture

### Fall Detection Model
- **Input:** 128x128 RGB images
- **Architecture:** Custom CNN optimized for fall detection
- **Output:** Binary classification (Fall/Non-Fall)
- **Optimization:** Quantized TensorFlow Lite for edge deployment

### YOLOv5 Integration
- **Purpose:** Person detection and tracking
- **Model:** YOLOv5s (small variant for edge devices)
- **Input:** Full camera frame
- **Output:** Bounding boxes for detected persons

## 🔄 Detection Pipeline

### Real-Time Detection Flow

1. **Frame Capture**
   - Capture frame from camera (Raspberry Pi Camera Module)
   - Frame rate: 30 FPS

2. **Person Detection**
   - Run YOLOv5 to detect persons in frame
   - Extract bounding boxes
   - Filter for person class only

3. **Region Extraction**
   - Crop detected person regions
   - Resize to model input size (128x128)
   - Normalize pixel values

4. **Fall Classification**
   - Run TensorFlow Lite model inference
   - Get fall probability
   - Apply confidence threshold

5. **Post-Processing**
   - Track consecutive fall frames
   - Confirm fall detection (reduce false positives)
   - Trigger alert if confirmed

6. **Evidence Capture**
   - Save screenshot on fall detection
   - Upload to cloud storage (AWS S3)
   - Log detection event

## 🚀 Usage

### Real-Time Detection

```bash
python "real-time detector.py"
```

**Features:**
- Live camera feed processing
- Real-time fall detection
- Visual feedback with bounding boxes
- Automatic evidence capture
- Cloud upload integration

**Features:**
- Process pre-recorded videos
- Frame-by-frame analysis
- Generate detection report
- Export annotated video

## 🔧 Configuration

### Model Parameters
```python
# TensorFlow Lite model
tflite_model_path = "Fall-detector-lite.tflite"

# YOLOv5 model
yolov5_pt_path = "yolov5s.pt"

# Detection settings
consecutive_fall_frames = 5  # Frames to confirm fall
confidence_threshold = 0.7   # Minimum confidence
```

### Camera Settings
- **Resolution:** Configurable (default: 640x480)
- **Frame Rate:** 30 FPS
- **Format:** RGB

## 📊 Model Training

### Training Process (Model.ipynb)

1. **Data Preparation**
   - Load Roboflow dataset
   - Image augmentation
   - Train/validation split

2. **Model Development**
   - Transfer learning (VGG16, MobileNetV2)
   - Custom CNN architecture
   - Hyperparameter tuning

3. **Model Optimization**
   - Convert to TensorFlow Lite
   - Quantization for edge deployment
   - Model size reduction

4. **Evaluation**
   - Accuracy metrics
   - Confusion matrix
   - Performance analysis

## 🎯 Key Features

### Real-Time Processing
- Low-latency inference (< 100ms per frame)
- Efficient memory usage
- Optimized for Raspberry Pi 5

### Dual Model Approach
- **YOLOv5:** Fast person detection
- **Custom CNN:** Accurate fall classification
- Combined for robust detection

### False Positive Reduction
- Consecutive frame confirmation
- Confidence threshold filtering
- Temporal consistency checks

## 📝 Code Structure

### Main Classes

#### `FallDetectionApp`
Main application class handling:
- Model loading
- Camera initialization
- Detection loop
- Alert triggering
- Cloud upload

### Key Functions

#### Model Loading
```python
def load_tflite_model():
    # Load TensorFlow Lite model
    # Initialize interpreter
    # Get input/output details
```

#### Person Detection
```python
def detect_persons(frame):
    # Run YOLOv5 inference
    # Filter person detections
    # Return bounding boxes
```

#### Fall Classification
```python
def classify_fall(person_roi):
    # Preprocess image
    # Run TensorFlow Lite inference
    # Return fall probability
```

## 🔍 Detection Logic

### Fall Confirmation
- Requires consecutive fall detections
- Reduces false positives
- Configurable threshold

### Alert Triggering
- Fall confirmed → Trigger alert
- Capture evidence screenshot
- Upload to cloud storage
- Log detection event

## 📈 Performance

### Inference Speed
- **YOLOv5:** ~50ms per frame
- **Fall Classifier:** ~30ms per frame
- **Total Pipeline:** ~80-100ms per frame

### Accuracy
- High accuracy on test dataset
- Low false positive rate
- Robust to lighting conditions

## 🛠️ Dependencies

```python
tensorflow>=2.10.0
torch>=1.12.0
opencv-python>=4.6.0
numpy>=1.21.0
PIL>=9.0.0
boto3>=1.26.0
python-dotenv>=0.20.0
```

## ⚠️ Important Notes

- **Model Files:** Ensure model files are in the same directory
- **Camera Access:** Requires camera permissions on Raspberry Pi
- **Cloud Configuration:** Set up AWS credentials in .env file
- **Performance:** Optimized for Raspberry Pi 5, may vary on other devices

## 🔗 Integration

### With Audio Detection
- Can run alongside audio detection
- Dual-mode confirmation increases accuracy
- Shared alert system

### With Web Dashboard
- Uploads screenshots to cloud
- Dashboard fetches and displays
- Real-time monitoring integration

---

**Note:** This module provides video-based fall detection optimized for edge deployment on Raspberry Pi devices.
