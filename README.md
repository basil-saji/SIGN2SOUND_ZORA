# SignVox by Zora

![Python](https://img.shields.io/badge/Python-3.10+-green)
![Platform](https://img.shields.io/badge/Platform-CPU%20Optimized-orange)
![License](https://img.shields.io/badge/License-MIT-blue)

### **Check out our live prototype at [SignVox](https://signvox.vercel.app) now!**

> **Sign2Sound** is an integrated communication system that bridges the gap between static fingerspelling and fluent digital conversation. Unlike standard recognition models, we utilize **Geometric Feature Extraction** and **Predictive Text Intelligence** to deliver zero-latency, high-precision translation without the need for heavy GPUs.

---

## 🚀 Key Features

### 1. Geometric Vision Core
We moved away from raw coordinate-based recognition. Our system calculates **63-dimensional geometric feature vectors** (joint angles, surface normals, and relative distances).
* **Rotation Invariant:** Recognition holds stable even if the wrist rotates.
* **Scale Invariant:** Works across varying hand sizes and distances.

### 2. Intelligent Prediction Engine
Fingerspelling every letter is slow. Our **N-Gram Context Engine** accelerates communication by:
* **Autocompleting words** after just 1-3 letters.
* **Predicting the next word** based on sentence context (e.g., *"WE"* → suggests *"ARE"*).
* **Adaptive Memory:** The system learns from user habits over time.

### 3. Remote Broadcasting ("The Studio")
We solved the visibility problem. The signer does not need to show their laptop screen to the audience.
* **Real-Time Sync:** Text is pushed to a Supabase cloud database in <50ms.
* **PWA Receiver:** Any external device (smartphone, tablet, laptop) can scan a QR code to view and listen to the live transcript instantly. The best part? **No signup or installation required!**. Try [Sign2Sound Studio](https://sign2sound.vercel.app)
  
  <img width="2560" height="1600" alt="image" src="https://github.com/user-attachments/assets/945f67d5-7862-4f0b-a839-2125bb511a9d" />



---

## 📂 Repository Structure

The codebase is organized into modular components, with core logic residing in `src/`.

```text
SIGN2SOUND_TeamZora/
│
├── main.py                         # Root Entry Point
├── requirements.txt
├── .gitignore
├── README.md
├── LICENSE
│
├── 📂 src/                         # CORE LOGIC MODULES
│   ├── features_alphabet.py        # Geometric feature extraction (Math)
│   ├── word_predictor.py           # Asynchronous N-Gram prediction engine
│   ├── gesture_utils.py            # Logic for "Thumb Up/Down" control gestures
│   ├── vocab_memory.py             # Memory management for predictions
│   ├── tts_engine.py               # Text-to-Speech handler
│   ├── broadcast.py                # Supabase API connector
│   └── broadcast_window.py         # TKinter GUI for the QR Code display
│
├── 📂 models/                      # TRAINED ARTIFACTS
│   ├── alphabet_pose_mlp_24letters.keras  # Optimized Geometric MLP
│   ├── alphabet_labels_24letters.npy      # Label encoder mapping
│   └── pose_feature_spec.json             # Input specification
│
├── 📂 training/                    # DEVELOPMENT PIPELINE
│   ├── vocab_trainer.py            # Script to initialize/train predictive memory
│   ├── train_model.py              # Main training script
│   └── 01_extract_...py            # (Preprocessing scripts)
│
├── 📂 preprocessing/               # DATA PREPARATION
│   └── 01_extract_alphabet...py    # Landmark extraction script
│
├── 📂 results/                     # PERFORMANCE METRICS
│   ├── confusion_matrix.png
│   ├── model_accuracy_&_loss.png
│   └── Classification_report.txt
│
└── 📂 notebooks/
    └── Sign2Sound_Zora.ipynb       # Exploratory Analysis
```

## 🛠️ Installation & Setup

### Prerequisites
- Python 3.9 or higher
- Webcam (Built-in or USB)
- Active Internet connection (for Broadcasting features)

### Step 1: Clone & Install Dependencies

```
# Clone the repository
git clone [https://github.com/basil-saji/sign2sound_zora.git](https://github.com/basil-saji/sign2sound_zora.git)
cd sign2sound_zora

# Install required libraries
pip install -r requirements.txt
````

### Step 2: Initialize Predictive Memory

Before running the system for the first time, you must initialize the predictive engine's vocabulary database. This script loads the N-Gram weights.

```
python training/vocab_trainer.py
```

Output should confirm: `"SUCCESS! Memory updated."`

---

## 🖥️ Usage Guide

### 1. Launch the System

Run the main inference engine from the root directory:

**Bash**

```bash
python inference/main.py
```

### 2. The Interface

* **Main Window:** Shows your camera feed with the "Studio Dark" UI.
* **Broadcast Window:** A second window will pop up displaying a QR Code.
* **Action:** Scan this with your phone to see the live text appear on your mobile device.

### 3. How to Communicate

The system uses a Hybrid Input Method:

* **Spell:** Sign letters (A-Z). The system smooths jitter and locks onto letters.
* **Confirm (Thumb Up):** Locks in the currently spelled word.
* **Smart Select (Rock On 🤘):** Selects the AI-Predicted Word shown in green.
* **Clear (Thumb Down):** Deletes the last word or clears the buffer.

---

## 📊 Performance Metrics

* **Accuracy:** 98.0% (Weighted F1-Score on IEEE Test Set).
* **Inference Speed:** 18ms per frame (approx. 55 FPS on i5 CPU).
* **Robustness:** Maintained >90% accuracy with ±30° hand rotation.

See results/confusion_matrix.png for a detailed per-class breakdown.

---

## 👥 Team Zora

* **Focus:** Accessibility & Human-Computer Interaction.
* **Mission:** To build tools that don't just "demo well," but actually work in the real world



