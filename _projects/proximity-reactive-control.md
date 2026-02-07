---
layout: project
title: "Proximity Reactive Control"
description: "Real-time adaptive reactive safety control using a bendable capacitive proximity sensor."
date: 2026-01-30
categories: [Robotics, HRI, Proximity Sensing, ROS2]
featured_image: "/assets/images/projects/proximity-reactive-control/featured.jpg"

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

## Motivation 
Conventional safety sensing has limitations for pre-contact HRI:
- **Tactile/force sensors** detect state changes **after contact**
- **Vision sensors** may suffer from occlusion and blind spots in collaborative environments.

This work targets a practical, robot-mounted sensing layer that supports **pre-contact perception** and **immediate safety intervention**.

---

## Sensor Design: Bendable Capacitive Proximity Sensor
### 1) kerf-pattern electrode
Each capacitive sensing layer uses a **kerf pattern** so the same sensor can be mounted on both **flat and curved robot surfaces** without redesign.

### 2) Dual-sensor fusion for distance estimation
While **capacitive sensing** offers high **near field sensitivity** and a **wide field of view (FoV)**, it exhibits a **nonlinear** relationship with distance. Conversely, **ToF sensors** allow for **long range measurement** despite having a **narrow FoV**. To address these characteristics, the two sensors are fused to **linearize and denoise the signal**.

- Model fitting:  $X = a \cdot e^{bY}$
- Distance inference: $Y = \frac{\ln X - \ln a}{b}$

where $X$ is the capacitive measurement and $Y$ is the distance.

### 3) Embedded processing + CAN streaming
The FDC2214 capacitive ASIC signals are processed by the **MCU** via I2C, with the final distance data transmitted via the **CAN** bus at **100 Hz**.

---

## Real-Time Control Architecture
The control pipeline is:
1. Robot executes a planned trajectory (quintic polynomial trajectory planning)
2. Proximity distance is streamed via CAN and monitored in ROS
3. **Safety State Logic** compares distance to thresholds
4. If the condition is satisfied, it **cancels active trajectory goals** and stops the robot (E-stop)

This architecture provides a practical safety layer and is designed to be extendable to distance-keeping / reactive obstacle behaviors.

---

## Experimental Validation (Real Robot)
Experiments with quintic-polynomial trajectories show that when an obstacle approaches the sensor:
- The **E-stop flag** is triggered by the distance threshold
- **Joint velocities rapidly converge to zero**

---

## Publications / Poster
- **KROC 2026 (Poster)**: *A Real-Time Adaptive Reactive Control Framework Using a Bendable Capacitive Proximity Sensor*

---

## Future Work
- Extend the safety layer from **Emergency Stop** to **continuous avoidance / distance-keeping control**
- Improve robustness for deployment (sensor mounting stability, wiring/noise, real-world repeatability)
