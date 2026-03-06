---
layout: project
title: "SoC Integrated Platform for Robot Collision Safety"
description: "Development of an SoC integrated platform for robot collision safety with real-time collision detection and avoidance intelligence (Ministry of Trade, Industry and Energy, Apr 2024 ~ Present)"
date: 2025-01-01
categories: [Robotics, Sensor, PCB, ROS2]
featured: true
published: true
featured_image: "/assets/images/projects/soc-platform/featured.png"

schematics:
  - file: "/assets/images/projects/soc-platform/sensor_structure.png"
    title: "Proximity Sensor Module Structure"
    description: "Integrated proximity sensor platform base structure and layer composition (Capacitive Electrode, Active Shield, Dielectric Layer, Grounded Shield)"
  - file: "/assets/images/projects/soc-platform/asic_hw.png"
    title: "ASIC-Applied Sensor H/W Prototype"
    description: "Proximity sensor module H/W prototypes with developed ASIC (NXA3110) for mobile robot and manipulator applications"

video: "/assets/videos/soc-platform/demo.mp4"
---

## Project Overview

This project is part of the Next-Generation Intelligent Semiconductor Technology Development program funded by the **Ministry of Trade, Industry and Energy (MOTIE)**, focusing on the development of an **SoC integrated platform for robot collision safety** with real-time collision detection and avoidance intelligence.

- **Project Period:** April 1, 2024 ~ Present
- **Participating Institutions:** AIDIN Robotics (Lead), NEXTLab Inc., Sungkyunkwan University
- **Role:** Development of collision safety intelligence algorithm and robot application validation (Sungkyunkwan University)

---

## Assigned Tasks

- **MCU Firmware Development for Sensor Signal Processing**
- **Contact/Non-contact State Recognition & Proximity Sensing Intelligence Algorithm Development**
- **Real-time Obstacle Response Intelligence Safety Framework Algorithm Development**
- **Real-time Obstacle Avoidance Experiment Validation on UR-10**

---


## Background & Motivation

As collaborative service robots become more prevalent in shared human-robot workspaces, the demand for **safety and functionality** has grown significantly. Unlike traditional industrial robots that operate behind safety fences, collaborative robots must work alongside humans without physical barriers — making **real-time collision detection and avoidance sensors** essential.

### Why Capacitive Proximity Sensor?

Capacitive proximity sensors offer key advantages over conventional ToF, LiDAR, vision, and radar sensors:

- **Wide FoV**: A single sensor can cover a large surface area
- **Fast Response**: Real-time processing without a dedicated signal processing PC
- **Low Cost**: A small number of sensors can cover an entire robot, reducing system cost

---

## Development Goals

### Collision Safety Sensor Core Technology

Developing a robot collision safety SoC with proximity sensing capability, along with proximity sensor module housings applicable to both mobile robots and manipulators.

- Development and integration of capacitance measurement ASIC (NXA3110)
- Real-time data acquisition system via I2C / CAN Interface
- Fabrication of two prototype form factors: mobile robot type and manipulator type

### Collision Safety Intelligence Algorithm

- **Contact/Non-contact Recognition**: Curve fitting to linearize raw capacitance data into distance values
- **Environmental Compensation**: Real-time temperature drift correction via Twin Circuit (98.83% variability improvement)
- **Intelligence Safety Framework**: Three-level risk assessment (Precaution / Warning / Emergency Stop) with robot speed control

---

## ASIC Performance Results 

Comparative testing of the developed ASIC (NXA3110) against the commercial chip (TI FDC2214) under identical conditions:

| Metric | FDC2214 (Commercial) | NXA3110 (Developed) |
|---|---|---|
| Resolution | 28 bit | 24 bit |
| Conversion Rate | 1,000 Hz | 1,000 Hz |
| Noise [code] | 737.4 | **176.05** |
| SNR | 49.84 | **61.58** |
| Max Detection Range | 15 cm | **22 cm** |

- **23% improvement** in SNR, **47% increase** in detection range (15cm → 22cm)
- **98% success rate** confirmed over 100 repeated performance tests
- Collision detection latency confirmed within **10ms**

---

## Intelligence Safety Framework

A three-level safety framework was developed for real-time obstacle response:

- **Precaution (≥ 25cm):** Full speed operation ($\dot{q}_{command}$)
- **Warning (10~25cm):** Deceleration to half speed ($\frac{1}{2}\dot{q}_{command}$)
- **Emergency Stop (≤ 10cm):** Immediate halt ($0$)

Distance values from the proximity sensing intelligence algorithm are passed through Variable Speed Scaling to the Position Controller, with validation ongoing on both manipulator and mobile robot platforms.

---

## Acknowledgement

본 연구는 산업통상자원부의 차세대지능형반도체기술개발 사업(과제번호: RS-2024-00407393)의 지원을 받아 수행되었습니다.
