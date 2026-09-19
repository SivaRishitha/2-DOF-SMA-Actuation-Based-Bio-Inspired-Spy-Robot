# 2-DOF SMA-Actuation Based Bio-Inspired Spy Robot

A motorless, silent 2-DOF surveillance robot using Shape Memory Alloy (SMA) actuation and onboard YOLO-based human detection for compact, low-noise directional monitoring.

![Status](https://img.shields.io/badge/status-complete-brightgreen) ![Platform](https://img.shields.io/badge/platform-ESP32-blue) ![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## Overview

Conventional pan-tilt surveillance systems rely on motors and gears, which add bulk, mechanical noise, and power draw — all liabilities for stealth or space-constrained monitoring. This project replaces motor-driven actuation with **Shape Memory Alloy (SMA) springs**, inspired by the smooth, silent head movements of snakes, to achieve controlled 2-DOF (pitch-yaw) motion with no gears, motors, or rotating shafts.

The robot streams live video via an onboard camera and runs a lightweight **YOLO-based human detection model**, triggering real-time alerts through the Blynk mobile app when a person is detected in frame.

## Key Features

- **Silent, motorless actuation** — SMA springs contract on heating and relax on cooling, producing smooth pitch-yaw motion with zero motor noise
- **2-DOF Cardan-joint mechanism** — 3D-printed, modular frame for easy assembly and actuator replacement
- **Real-time human detection** — YOLO model processes the live video feed and triggers automatic alerts
- **Wireless monitoring & control** — Live video streaming and manual slider-based actuation control via the Blynk app, entirely over Wi-Fi
- **Hardware-PWM actuation** — Four independently driven SMA channels via MOSFET switching circuits

## System Architecture

```
User (Blynk App) → Wi-Fi → ESP32 ──┬─→ ESP32-CAM → YOLO Detection → Blynk Alerts
                                    └─→ PWM (4 channels) → MOSFET Drivers → SMA Springs → Pitch/Yaw Motion
```

## Hardware

| Component | Role |
|---|---|
| ESP32 | Main controller — Wi-Fi, Blynk integration, PWM generation |
| ESP32-CAM | Live video streaming + YOLO human detection |
| MOSFET driver circuits | High-current switching for SMA heating cycles |
| SMA springs (×4) | Thermomechanical actuators for pitch-yaw motion |
| 3D-printed Cardan joint | Mechanical 2-DOF structure |
| Blynk app | Remote control (sliders) + live video + alerts |

## Results

| Test | Result |
|---|---|
| Current draw @ 4V | ~0.75 A – 0.9 A across springs |
| Current draw @ 5V | ~0.9 A – 1.2 A across springs |
| Max yaw deflection | ~40° |
| Max pitch deflection | ~20° (reduced by gravity acting against the vertical actuation axis) |

## Repository Structure

```
├── firmware/           # ESP32 control code (PWM generation, Blynk integration)
├── vision/              # YOLO human detection script for ESP32-CAM feed
├── cad/                 # 3D-printed part designs (Cardan joint, fixtures)
├── testing/              # V-I characterization and angular deflection test data/plots
└── README.md
```

## Limitations & Future Work

- SMA cooling time currently limits actuation speed
- Continuous activation causes thermal accumulation, reducing stroke range over time
- Planned extension: multi-segment, two-way SMA actuation for forward locomotion — enabling a snake-type rescue robot for confined-space search and rescue in post-disaster environments

## Contributors

Built as part of a project under the Mechatronics and Instrumentation Lab, IIT Indore, under the guidance of Prof. I. A. Palani.

## License

MIT
