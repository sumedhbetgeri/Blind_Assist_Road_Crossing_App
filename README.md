# Blind_Assist_Road_Crossing_App

# 🚦 SmartCross AI — Road Crossing Assistance System

> An AI-powered real-time road crossing assistant for visually impaired users.  
> Runs entirely in the browser — no installation, no server, no backend needed.

![SmartCross Banner](https://img.shields.io/badge/SmartCross-AI%20Powered-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![HTML](https://img.shields.io/badge/Built%20With-HTML%2FJS-orange?style=for-the-badge)

---

## 🌐 Live Demo

**[▶ Open SmartCross AI](https://stately-raindrop-49dfdd.netlify.app/)**

---

## 📸 Features

- **Real-Time Vehicle Detection** using TensorFlow.js + COCO-SSD (MobileNetV2)
- **Voice Alerts** via Web Speech API — fully offline, no external TTS service
- **Smart 5-Second Safety Rule** — only announces "Safe to cross" after road is clear for 5 continuous seconds
- **Danger Override** — immediately warns if a fast or close vehicle appears
- **Emergency Alert** — sends your GPS location via WhatsApp, SMS, or Email
- **Works on Mobile** — uses rear camera automatically
- **Zero Dependencies** — single HTML file, no npm, no Python, no server

---

## 🧠 How It Works

```
Camera Feed
    │
    ▼
COCO-SSD Detection (every 350ms)
    │
    ▼
Vehicle Tracker (centroid tracking)
    │
    ▼
Decision Engine
    ├── Vehicle present       → "Caution. Vehicle on road."
    ├── Road clear < 5s       → Silent countdown (visual only)
    ├── Road clear ≥ 5s       → "Road is clear. Safe to cross."
    ├── Vehicle after safe    → "Stop! Vehicle on road."
    └── Fast/close vehicle    → "Danger! Do not cross."
    │
    ▼
Voice Alert (Web Speech API) + Vibration
```

---

## 🗣️ Voice Alert Logic

| Situation | Voice Message |
|-----------|--------------|
| Vehicle detected | *"Caution. Vehicle on road. Please wait."* |
| Still there (every 4s) | *"Still waiting. Vehicle on road."* |
| Road just cleared | *(silence — 5s countdown starts)* |
| 5s clear | *"Road is clear. Safe to cross."* |
| Still clear (every 8s) | *"Still clear. Safe to cross."* |
| Vehicle appears after safe | *"Stop! Vehicle on road. Do not cross."* |
| Fast / very close vehicle | *"Danger! Do not cross."* |

---

## 🚀 Run Locally

No installation needed. Just open the file:

```bash
# Clone the repo
git clone https://github.com/yourusername/smartcross.git

# Open in browser
open index.html
# or just double-click index.html
```

---

## 📁 Project Structure

```
smartcross/
├── index.html       ← Entire application (self-contained)
├── README.md        ← This file
└── LICENSE          ← MIT License
```

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| TensorFlow.js | ML inference in browser |
| COCO-SSD MobileNetV2 | Vehicle object detection |
| Web Speech API | Offline text-to-speech |
| Canvas API | Bounding box rendering |
| Geolocation API | GPS for emergency alerts |
| Web Share / mailto / wa.me | Emergency contact dispatch |

---

## 📱 Best Usage

- Open on **mobile Chrome** for rear camera access
- Works best in **daylight / good lighting**
- Point camera at the **road ahead**
- Fill in emergency contact before starting
- Volume should be **turned up** for voice alerts

---

## ⚙️ Configuration (inside index.html)

```js
const SAFE_CLEAR_MS    = 5000;  // seconds of clear road before "safe"
const RPT_CAUTION_MS   = 4000;  // repeat caution interval
const RPT_SAFE_MS      = 8000;  // repeat safe interval
const RPT_DANGER_MS    = 2000;  // repeat danger interval
const DETECT_MS        = 350;   // detection frequency (ms)
```

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 🙏 Acknowledgements

- [TensorFlow.js](https://www.tensorflow.org/js)
- [COCO-SSD Model](https://github.com/tensorflow/tfjs-models/tree/master/coco-ssd)
- [Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API)
