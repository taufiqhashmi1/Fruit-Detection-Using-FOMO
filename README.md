# FOMO Fruit Detection (ESP32-CAM)

![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg) ![Platform](https://img.shields.io/badge/platform-ESP32-green) ![Edge Impulse](https://img.shields.io/badge/Edge%20Impulse-FOMO-orange)

![ESP32-CAM FOMO Fruit Detection Demo](FomoFruit.webp)
*Real-time fruit detection predictions shown on the Serial Monitor alongside the source image.*

A lightweight computer vision project that implements real-time fruit detection on the ESP32-CAM development board. By utilizing Edge Impulse's **FOMO (Faster Objects, More Objects)** architecture, this system achieves object localization and classification on a microcontroller with only 4MB PSRAM, where standard object detection models (like YOLO or MobileNet SSD) would fail or run too slowly.

## 🎯 Project Overview

Standard object detection models require significant processing power and memory. This project solves that bottleneck by using **FOMO**, a constrained object detection algorithm that:
1.  Performs pixel-wise segmentation instead of region proposal.
2.  Outputs the centroid coordinates (x, y) of the object rather than a full bounding box.
3.  Runs significantly faster (up to 30x) than MobileNet SSD on DSP-capable silicon.

**Target Hardware:** ESP32-CAM (AI-Thinker Model)
**Classes Detected:** Apples, Bananas, Pineapple and Grapes (Customizable)

## ⚡ Features

* **Real-time Inference:** Achieves useable frame rates on the ESP32-CAM.
* **Edge Computing:** All processing happens locally on the chip; no internet connection required for inference.
* **Web Stream:** Includes a built-in web server to view the live video feed and detection results.
* **Centroid Tracking:** Visualizes the center point of detected fruits.

## 🛠 Tech Stack

* **Hardware:** ESP32-CAM (AI-Thinker), FTDI Programmer.
* **Platform:** Arduino IDE / PlatformIO.
* **ML Backend:** Edge Impulse (Data ingestion, labeling, training, and C++ library export).
* **Model Architecture:** FOMO (MobileNetV2 0.35 alpha).

## 📊 Model Performance

* **Input Resolution:** 96x96 (Grayscale/RGB)
* **Inference Time:** ~150ms per frame (approximate, dependent on clock speed)
* **RAM Usage:** < 250KB peak
* **Flash Usage:** < 100KB

## 🔌 Hardware Pinout (Camera Config)

Standard AI-Thinker Pin definition used in `camera_pins.h`:

| Pin Name | ESP32 GPIO |
| :--- | :--- |
| CAM_PIN_PWDN | 32 |
| CAM_PIN_RESET | -1 |
| CAM_PIN_XCLK | 0 |
| CAM_PIN_SIOD | 26 |
| CAM_PIN_SIOC | 27 |
| CAM_PIN_D7 | 35 |
| CAM_PIN_D6 | 34 |
| CAM_PIN_D5 | 39 |
| CAM_PIN_D4 | 36 |
| CAM_PIN_D3 | 21 |
| CAM_PIN_D2 | 19 |
| CAM_PIN_D1 | 18 |
| CAM_PIN_D0 | 5 |
| CAM_PIN_VSYNC | 25 |
| CAM_PIN_HREF | 23 |
| CAM_PIN_PCLK | 22 |

## 🚀 Installation & Setup

### 1. Prerequisites
* Install **Arduino IDE**.
* Install **ESP32 Board Manager** (Expressif Systems).
* Download your custom C++ library from your Edge Impulse project dashboard (Deployment -> Arduino Library).

### 2. Library Import
1.  Open Arduino IDE.
2.  Go to `Sketch` -> `Include Library` -> `Add .ZIP Library`.
3.  Select the downloaded Edge Impulse ZIP file.

### 3. Code Configuration
1.  Clone this repository.
2.  Open the `.ino` file.
3.  Ensure `#define CAMERA_MODEL_AI_THINKER` is uncommented.

### 4. Flashing
1.  Connect GPIO 0 to GND.
2.  Select board: `AI Thinker ESP32-CAM`.
3.  Upload code.
4.  Remove GPIO 0 from GND and press the Reset button.

## 🖥️ Usage

1.  Open the Serial Monitor (Baud Rate: 115200).
2.  The Serial Monitor will reflect the predictions

## Confusion Matrix
<img width="609" height="538" alt="image" src="https://github.com/user-attachments/assets/682f0014-f92b-44a1-a23b-fa28bc64b88d" />

## 🤝 Contributing

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/NewFeature`)
3.  Commit your Changes (`git commit -m 'Add some NewFeature'`)
4.  Push to the Branch (`git push origin feature/NewFeature`)
5.  Open a Pull Request

## 📄 License

Distributed under the Apache License 2.0. See `LICENSE` for more information.

*Note: The machine learning model and inference SDK are provided by Edge Impulse under the Apache License 2.0.*
