---
layout: project
title: "Safe E-Stop Motion for HRI Using Proximity Sensor"
description: "A real-time adaptive reactive control framework for safe HRI based on a bendable capacitive proximity sensor that conforms to flat and curved robot surfaces."
date: 2026-02-01
categories: [Robotics, HRI, Sensor, ROS2]
featured_image: "/assets/images/projects/safe-e-stop-hri/featured.png"
github_url: ""
demo_url: ""

featured: true

published: true

schematics:
  - file: "/assets/images/projects/safe-e-stop-hri/sensor_structure.png"
    title: "Bendable Capacitive Proximity Sensor"
    description: "Structure of the bendable capacitive proximity sensor"
  - file: "/assets/images/projects/safe-e-stop-hri/framework.png"
    title: "Adaptive Reactive Control Framework"
    description: "Architecture of adaptive reactive control framework"
  - file: "/assets/images/projects/safe-e-stop-hri/result.png"
    title: "Experimental Results"
    description: "Experimental results - sensor distance and joint velocity response"
---

## Project Overview

We present a real-time adaptive reactive control framework for safe Human–Robot Interaction (HRI) based on a bendable capacitive proximity sensor that conforms to flat and curved robot surfaces. A kerf-patterned electrode enables robust mounting on AMRs (Autonomous Mobile Robots) and Manipulators, while model-based fusion with a ToF (Time-of-Flight) sensor linearizes and denoises distance estimates.

**Presented at:** 한국로봇종합학술대회 (KRcC 2026), Pyeongchang, Korea, Feb. 2026 — Poster

**Authors:** 한성진, 강현창, 성혁제, 송영빈, 최혁렬 (Sungkyunkwan University)

---

## Motivation

Existing sensing approaches for HRI have critical limitations:

- **Tactile / Force sensors** — detect only post-contact state changes; cannot prevent contact before it occurs
- **Vision sensors** — blind spots caused by occlusion from the operator; unsuitable for close-range HRI
- **Conventional sensors** — require individual redesign for each robot platform and mounting location

To address these limitations, we developed a bendable capacitive proximity sensor applicable to diverse robot platforms without hardware modification, combined with a real-time adaptive reactive control framework.

---

## Assigned Tasks

- **Bendable Capacitive Proximity Sensor Design & Fabrication**
- **Capacitive & ToF Sensor Fusion for Distance Estimation**
- **MCU Firmware Development with I2C & CAN Communication**
- **ROS-based Real-Time Emergency Stop (E-stop) Safety Control System Development**

---


## Bendable Capacitive Proximity Sensor

### Structure
The sensor consists of two capacitive sensing layers with a **kerf pattern** applied to each layer, enabling free switching between flat and bending configurations.

| Component | Description |
|---|---|
| Electrode ADC 1 / 2 | Capacitive sensing electrodes |
| ToF Sensor 1 / 2 | Time-of-Flight distance sensors |
| Microcontroller | FDC2214 capacitive ASIC + STM32F7RET6 |
| Shield Electrode | EMI shielding layer |
| Sensor Frame | Structural support frame |

### Key Features
- **Flat ↔ Bending** conversion without additional hardware changes
- Mountable on **AMR** and **Manipulator** surfaces
- Stable sensing range of approximately **200 mm**
- Sensor signals are acquired via the **I2C interface**, converted into distance estimates within the **MCU**, and subsequently streamed to **ROS2** via the **CAN bus**.

---

## Sensor Fusion: Capacitive + ToF

Capacitive sensors have nonlinearity between capacitance and distance. ToF sensors have blind spots at close range. We combine both to resolve each other's weaknesses.

Collected data pairs *(X: capacitance, Y: ToF distance)* are fitted to an double exponential model:

$$X = a \cdot e^{b \cdot Y}$$

The constants *a* and *b* are dynamically estimated using **least squares** on the collected data pairs. Once determined, the inverse formula gives accurate distance:

$$Y = \frac{1}{b} \cdot (\ln X - \ln a)$$

This fusion approach linearizes the capacitive sensor output and eliminates the ToF near-range blind spot.

---

## Adaptive Reactive Control Framework

### Architecture
The framework connects the proximity sensor to the robot's motion controller via ROS2:

1. **Proximity Sensor** — measures distance at **100 Hz** via CAN bus
2. **Distance Fitting Node** — applies the exponential fusion model to linearize distance
3. **Safety State Logic** — compares linearized distance against safety threshold
4. **Planning Node** — generates quintic polynomial trajectories
5. **Position Control** — executes joint trajectories; cancels goals on E-stop signal

### Emergency Stop Logic
When an obstacle enters the safety threshold distance:
- Safety State Logic immediately **cancels all active trajectory goals**
- All joint velocities converge to **zero** within milliseconds
- System returns to monitoring state automatically

---

## Experimental Results

### Platform
- **Robot:** 6-DOF Manipulator (UR series)
- **Trajectory:** Quintic polynomial joint trajectories
- **Communication:** CAN bus at 100 Hz

### Results Summary

| Metric | Result |
|---|---|
| Sensing range | ~200 mm (stable) |
| CAN transmission rate | 100 Hz |
| Emergency stop response | Joint velocities → 0 immediately upon threshold crossing |
| Platform compatibility | Manipulator + AMR |

Experiments with quintic polynomial trajectories confirmed that **joint velocities converged to zero** the moment an obstacle was detected within the threshold distance demonstrating practical real time safety performance for HRI environments.

---

## Publication

> **한성진**, 강현창, 성혁제, 송영빈, 최혁렬,
> "벤더블 정전용량 기반 근접센서 로봇의 실시간 적응형 반응 제어 프레임워크,"
> *한국로봇종합학술대회 (KRcC 2026)*, Pyeongchang, Korea, Feb. 2026 — **Poster**

---

## Future Work

- Extend the framework to **avoidance control** — enabling the robot to maintain a safe distance while continuing its task
- Apply to more complex multi-link robot platforms
- Generalize sensor fusion model for different object materials and surface types