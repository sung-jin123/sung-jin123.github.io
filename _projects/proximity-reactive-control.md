---
layout: project
title: "Proximity Reactive Control"
description: "Real-time adaptive reactive safety control using a bendable capacitive proximity sensor (UR10, CAN→ROS, ToF fusion)."
date: 2026-01-30
categories: [Robotics, HRI, Proximity Sensing, ROS2]
featured_image: "/assets/images/projects/proximity-reactive-control/featured.jpg"
github_url: "https://github.com/sung-jin123/sung-jin123.github.io"
# (선택) 유튜브 링크가 있으면 데모 버튼이 생깁니다.
# demo_url: "https://youtu.be/XXXXXXXXXXX"

# (선택) 페이지 상단에 갤러리(이미지/동영상) 자동 노출
gallery:
  - type: "image"
    file: "/assets/images/projects/proximity-reactive-control/gallery/sensor_flat_vs_bending.jpg"
    description: "Kerf-pattern electrode enables flat↔bending configuration."
  - type: "image"
    file: "/assets/images/projects/proximity-reactive-control/gallery/framework_architecture.png"
    description: "Adaptive reactive control architecture (CAN→ROS monitoring + safety state logic)."
  - type: "video"
    file: "/assets/images/projects/proximity-reactive-control/demo/estop_demo.mp4"
    description: "Real robot demo: distance threshold triggers E-stop and joint velocity converges to zero."
---

## Overview
This project presents a **real-time adaptive reactive control framework** for **pre-contact safety** in **Human–Robot Interaction (HRI)** using a **bendable capacitive proximity sensor** mounted on a manipulator (UR10).  
A key goal is to detect nearby objects **before contact** and trigger **reactive safety behaviors** in real time.  
(커프(Kerf) 패턴 전극 + ToF 융합 기반 거리 추정 + CAN→ROS 스트리밍 + Safety State Logic 기반 E-stop 검증) :contentReference[oaicite:4]{index=4}

---

## Motivation (HRI Safety Gap)
Conventional safety sensing has limitations for pre-contact HRI:
- **Tactile/force sensors** detect state changes **after contact**
- **Vision sensors** may suffer from occlusion and blind spots in collaborative environments :contentReference[oaicite:5]{index=5}

This work targets a practical, robot-mounted sensing layer that supports **pre-contact perception** and **immediate safety intervention**.

---

## Sensor Design: Bendable Capacitive Proximity Sensor
### 1) Bendable mounting via kerf-pattern electrode
Each capacitive sensing layer uses a **kerf pattern** so the same sensor can be mounted on both **flat and curved robot surfaces** without redesign. :contentReference[oaicite:6]{index=6}

### 2) Dual-sensor fusion for distance estimation (Capacitive + ToF)
Capacitive sensing provides near-field sensitivity and wide FoV, but its distance relationship is **nonlinear**.  
To address this, a ToF sensor is fused to **linearize/denoise** the distance estimate using an exponential model:

- Model fitting:  \( X = a \cdot e^{bY} \)
- Distance inference:  \( Y = \frac{1}{b}(\ln X - \ln a) \)

where \(X\) is capacitive measurement and \(Y\) is distance. :contentReference[oaicite:7]{index=7}

### 3) Embedded processing + CAN streaming
Signals are preprocessed on the **MCU** and transmitted via **CAN** to the robot software stack (ROS). :contentReference[oaicite:8]{index=8}

---

## Real-Time Control Architecture (CAN → ROS → Safety Logic)
The control pipeline is:
1. Robot executes a planned trajectory (quintic polynomial trajectory planning)
2. Proximity distance is streamed via CAN and monitored in ROS
3. **Safety State Logic** compares distance to thresholds
4. If the condition is satisfied, it **cancels active trajectory goals** and stops the robot (E-stop) :contentReference[oaicite:9]{index=9}

This architecture provides a practical safety layer and is designed to be extendable to distance-keeping / reactive obstacle behaviors. :contentReference[oaicite:10]{index=10}

---

## Experimental Validation (Real Robot)
Experiments with quintic-polynomial trajectories show that when an obstacle approaches the sensor:
- The **E-stop flag** is triggered by the distance threshold
- **Joint velocities rapidly converge to zero** :contentReference[oaicite:11]{index=11} :contentReference[oaicite:12]{index=12}

---

## Publications / Poster
- **KROC 2026 (Poster)**: *A Real-Time Adaptive Reactive Control Framework Using a Bendable Capacitive Proximity Sensor* :contentReference[oaicite:13]{index=13}

---

## Future Work
- Extend the safety layer from **Emergency Stop** to **continuous avoidance / distance-keeping control** :contentReference[oaicite:14]{index=14}
- Improve robustness for deployment (sensor mounting stability, wiring/noise, real-world repeatability)

---

## Media & Resources
- **Project repository:** https://github.com/sung-jin123
- **Poster PDF:** (사이트에 PDF 업로드 후 링크 추가)
- **Demo video:** (YouTube 또는 MP4 업로드 후 연결)
