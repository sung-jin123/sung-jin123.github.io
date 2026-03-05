---
layout: project
title: "Automated Logistics Management System for Unmanned Convenience Store Using 4-DOF Robot Arm"
description: "A 4-DOF robot arm system that automatically restocks unmanned convenience store walk-in shelves using YOLO V4 object detection and inverse kinematics."
date: 2023-08-01
categories: [Robotics, Arduino, Computer Vision, Mechatronics]
featured_image: "/assets/images/projects/capstone-design-4dof/featured.jpg"
github_url: ""
demo_url: ""

# Components List
components:
  - name: "Dynamixel AX-12A"
    quantity: 6
    description: "Smart servo motors for robot arm joints (Base, Shoulder x2, Elbow x2, Wrist)"
    link: "https://www.robotis.com/shop/item.php?it_id=902-0003-001"
  - name: "Arduino Mega 2560 Rev3"
    quantity: 1
    description: "Main microcontroller for robot arm control"
  - name: "Dynamixel Shield"
    quantity: 1
    description: "Arduino shield for Dynamixel motor control via TTL communication"
  - name: "HC-SR04 Ultrasonic Sensor"
    quantity: 1
    description: "Detects when cans are missing from the showcase"
  - name: "USB Camera"
    quantity: 1
    description: "Real-time object detection for can type classification"
  - name: "PLA Filament"
    quantity: 1
    description: "3D-printed structural parts for gripper, links, and base"
---

## Overview

This project was developed as a **2023 Capstone Design** at Hansung University (한성대학교), in collaboration with team members 정낙형 and 김다윤 under Professor 최재봉.

The goal was to design an **automated logistics restocking system** for unmanned convenience store walk-in refrigerators. Unmanned convenience stores have grown rapidly (208 → 2,783 stores from 2019–2022), yet their inventory management remains manual. Our system automates this by detecting empty spots via ultrasonic sensor and using a 4-DOF robot arm to restock cans automatically.

---

## System Architecture

The overall system consists of three main parts:

1. **Object Detection (PC + Camera)** — YOLO V4 identifies the type of can (Coca-Cola or Pepsi) and calculates its 2D coordinates.
2. **Communication Pipeline** — Coordinates are sent from Python → Arduino Uno → Arduino Mega via serial (57600 baud rate).
3. **Robot Arm Control (Arduino Mega + Dynamixel Shield)** — Inverse kinematics converts 3D target positions into joint angles, then Dynamixel AX-12A motors execute the motion.

```
YOLO V4 (Python) → Arduino Uno → Arduino Mega → Dynamixel Shield → 4-DOF Robot Arm
                                                     ↑
                                             HC-SR04 Ultrasonic Sensor
```

---

## Hardware Design

### Robot Arm Structure

The manipulator is a **planar RRR configuration (4-DOF total)** with:

| Joint | Motor | Count |
|-------|-------|-------|
| Base (rotation) | AX-12A | 1 |
| Shoulder | AX-12A | 2 (parallel) |
| Elbow | AX-12A | 2 (parallel) |
| Wrist / Gripper | AX-12A | 1 |

All structural parts were **3D-printed in PLA** using a custom design in UG NX. The shoulder and elbow each use two motors in parallel to meet the required torque budget.

### Torque Calculation

Assuming the manipulator is horizontal (worst case):

$$\tau_{total} = 4.36\,\text{N} \times 0.518\,\text{m} + 0.589\,\text{N} \times 0.363\,\text{m} + 1.079\,\text{N} \times 0.214\,\text{m} + 0.686\,\text{N} \times 0.154\,\text{m} = 2.81\,\text{N·m}$$

The AX-12A provides **1.50 N·m stall torque at 12V**, so two motors per joint satisfies the requirement.

### Gripper

A 3-finger open-source gripper compatible with AX-12A was adapted. Gripper length is **8.2 cm** — designed to accommodate standard beverage cans (avg. diameter ~5 cm). All finger joints use worm-gear mechanisms printed in PLA for compact, reliable gripping.

### Showcase & Storage

- **Showcase**: UG NX–modeled with a **10° draft angle** so cans slide forward automatically when one is removed. Holds 6 cans.
- **Storage unit**: Modeled and fabricated by a carpentry workshop from CAD drawings.

---

## Software Design

### YOLO V4 Object Detection

YOLO V4 was selected for its real-time performance on a single consumer GPU. The model identifies can types (Coca-Cola / Pepsi) with >90% confidence and outputs bounding box center coordinates `(center_x, center_y)`.

To improve detection accuracy, the green conveyor belt background was converted to white using HSV color masking in OpenCV before feeding frames to the detector.

### Inverse Kinematics

3D Cartesian target positions were simplified to a **2D planar problem** based on a referenced paper (DBpia, 2014). The equations implemented in MATLAB and then ported to Arduino are:

$$R' = R - L_4 \cdot \cos(\Phi)$$

$$Z' = Z - h_{base} + L_4 \cdot \sin(\Phi)$$

$$A = \frac{\sqrt{Z'^2 + R'^2}}{2}$$

| Joint | Equation |
|-------|----------|
| **θ₁** (Base) | $\theta_1 = \text{atan2}(Y,\, X)$ |
| **θ₃** (Elbow) | $\theta_3 = \arcsin\!\left(\dfrac{A}{L_3}\right) \times 2$ |
| **θ₂** (Shoulder) | $\theta_2 = \text{atan2}(Z',\, R') + \dfrac{180° - \theta_3}{2}$ |
| **θ₄** (Wrist) | $\theta_4 = 180° - \Phi - \theta_2 - \theta_3$ |

**12 waypoints** were pre-calculated in MATLAB and hardcoded as motion sequences in Arduino.

### System Flow

```mermaid
flowchart TD
    A([🟢 Start]) --> B[Conveyor ON]
    B --> C{Ultrasonic Sensor\nDetects Can?}
    C -- No --> B
    C -- Yes --> D[Conveyor OFF]
    D --> E{Robot Arm\nReceives Coordinates?}
    E -- No --> E
    E -- Yes --> F[Execute Pick-and-Place]
    F --> G[Conveyor OFF]
    G --> H([🔴 End])

    style A fill:#2ecc71,color:#fff
    style H fill:#e74c3c,color:#fff
    style C fill:#3498db,color:#fff
    style E fill:#3498db,color:#fff
    style F fill:#9b59b6,color:#fff
```

---

## Results

The system successfully demonstrated automatic can grasping and restocking in a mock walk-in environment. The robot arm moved cans from the storage unit to the showcase reliably within the predefined 12-path trajectory.

**Known Issue:** Real-time coordinate data transmission from OpenCV (Python) to the Arduino failed during the final demo. The robot therefore operated on pre-defined fixed coordinates rather than live detection feedback.

**Planned Improvements:**
- PID control for smoother, safer motor actuation
- Higher-torque motors to support camera mounting at a better viewpoint
- Reliable serial communication protocol to close the YOLO → robot arm loop

---

## References

- Blog Series: [studypenggu.tistory.com](https://studypenggu.tistory.com/2)
- Inverse Kinematics Reference: DBpia NODE06603273 (이경문, 이강희, 2014)
- Dynamixel AX-12A: [emanual.robotis.com](https://emanual.robotis.com/docs/kr/dxl/ax/ax-12a/)
