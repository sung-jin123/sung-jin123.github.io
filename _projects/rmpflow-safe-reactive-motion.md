---
layout: project
title: "RMPflow-Based Safe Reactive Motion Planning Using Proximity Sensors for Human-Robot Interaction"
description: "Step-by-step development of a bendable capacitive proximity sensor and a real-time reactive safety control framework based on RMPflow (M.S. Seminars 1–4)"
date: 2026-01-30
categories: [Robotics, HRI, Sensor, ROS, RMPflow]
featured_image: "/assets/images/projects/rmpflow-hri/featured.png"
github_url: ""
demo_url: ""
---

## Overview

This research develops a **bendable capacitive proximity sensor** that can be mounted on both flat and curved surfaces, and integrates it with an **RMPflow**-based reactive motion control framework for safe **Human-Robot Interaction (HRI)** — conducted throughout M.S. seminars 1 to 4.

As the level of human-robot collaboration increases, the development of reliable HRC technologies becomes essential. Accordingly, sensor technologies that enable robots to perceive their surrounding environment are receiving growing attention.
Conventional safety sensors suffer from blind spots, limited short-range detection, and inability to conform to curved surfaces.

---

## 1. Mechanically Bendable Sensor Structure (Planar + Planar)

### Design Background

Capacitive sensors detect the approach of objects using an electric field. The principle of the Self-Capacitance method is as follows:

$$C \approx \varepsilon_0 \varepsilon_r \frac{2 A_1 A_2}{A_1 + A_2} \cdot \frac{1}{d}$$

<figure>
  <img src="/assets/images/projects/rmpflow-hri/capacitive-principle.png" alt="Single-Ended Capacitance Principle">
  <figcaption>Single-Ended Capacitance Principle</figcaption>
</figure>

As distance $d$ decreases, capacitance $C$ increases.

### Structure

By applying a **Kerf pattern** to the electrodes, the sensor achieves a bendable structure that can freely transition between Flat and Bending configurations.

- **Electrode (1)**: Planar-Type (top)
- **Electrode (2)**: Planar-Type (bottom)
- **Shield Electrode**: External noise shielding
- **ToF Sensor × 2**: Fusion sensor for distance correction
- **MCU + FDC2214**: Capacitance measurement and CAN transmission

<figure>
  <img src="/assets/images/projects/rmpflow-hri/bendable-sensor-pp.png" alt="Mechanically Bendable Sensor Structure (Planar + Planar)">
  <figcaption>Mechanically Bendable Sensor Structure (Planar + Planar)</figcaption>
</figure>

### Limitations

Since both electrodes share the same Planar structure, bending causes **Capacitance Imbalance** between the two electrodes, making accurate distance estimation difficult.

<figure>
  <img src="/assets/images/projects/rmpflow-hri/capacitance-imbalance.png" alt="capacitance-imbalance">
  <figcaption>Capacitance Imbalance</figcaption>
</figure>

---

## 2. Mechanically Bendable Sensor Structure (Planar + Loop)

### Electrode Redesign

To resolve the imbalance of the Planar + Planar structure, the bottom electrode was replaced with a **Loop-Type**. The Loop electrode has an open center, which reduces the overlapping area of the electric field with the top Planar electrode, thereby decreasing the capacitance imbalance between the two electrodes.

<figure>
  <img src="/assets/images/projects/rmpflow-hri/Change-electrode.png" alt="Change-electrode">
  <figcaption>Change Electrode (Planar → Loop)</figcaption>
</figure>

### ToF Cover Fixation Comparison

Since the Loop-Type electrode could not fix the ToF sensor, the top cover was redesigned. Three fixation types were evaluated:

| Type | Description |
|------|-------------|
| Horizontal Fix Type | Horizontal fixation, stable |
| Line Fix Type | Linear fixation, lightweight |
| Vertical Fix Type | Vertical fixation |

<figure>
  <img src="/assets/images/projects/rmpflow-hri/top-cover.png" alt="Design Loop-Type Electrode Top Cover">
  <figcaption>Design Loop-Type Electrode Top Cover</figcaption>
</figure>

### Validation Results and Limitations

Measurement of the capacitance variation confirmed that the Capacitance Imbalance issue was resolved.
However, as shown below, the maximum detection range of approximately 100 mm was insufficient for mounting on a real manipulator to detect and avoid objects, leading to a plan for full redesign.

| Metric | Mechanically Bendable Sensor |
|--------|------------------------------|
| Standard Deviation | ~104–120 mm |
| RMSE | ~111–155 mm |
| Maximum Detection Range | 100 mm |

<figure>
  <img src="/assets/images/projects/rmpflow-hri/Performance-Evaluation-of-Bendable-Sensor.png" alt="Validation Mechanically bendable sensor">
  <figcaption>Validation of Mechanically Bendable Sensor</figcaption>
</figure>

---

## 3. [GEN3] Bendable Sensor Development

### Improvement Goals

| Item | Previous Generation Limitation | Gen3 Improvement |
|------|-------------------------------|------------------|
| Electrode Overlap | Reduced accuracy at short distances | Separated electrode redesign |
| Manufacturability | 1 mm spacing pattern not manufacturable | Modified to manufacturable pattern |
| Size | 150×150 mm (not integrable on robot) | Optimized to **190×80 mm** |
| Kerf Structure | Must be preserved | Flat-Bending structure maintained |

### Electrode Size Optimization

Through comparison of various samples, **190×80 mm** was selected as the final size, satisfying both sensing performance and manufacturability.

<figure>
  <img src="/assets/images/projects/rmpflow-hri/Optimizing-Electrode-Design-via-Area-Comparison.png" alt="Optimizing Electrode Design via Area Comparison">
  <figcaption>Optimizing Electrode Design via Area Comparison</figcaption>
</figure>

### Whole-Body Integration on UR10

A total of **8 Gen3 sensor modules** were mounted on the UR10 — 4 on the **Upper Arm** and 4 on the **Lower Arm** — establishing full-coverage proximity sensing.

<figure>
  <img src="/assets/images/projects/rmpflow-hri/UR10-sensor-integration.png" alt="GEN3 Bendable Sensor Configuration for UR10">
  <figcaption>GEN3 Bendable Sensor Configuration for UR10</figcaption>
</figure>

### Performance Comparison (vs. Previous Generation)

| Metric | Previous Gen | **Gen3** | Improvement |
|--------|-------------|---------|-------------|
| Standard Deviation | ~104–120 mm | **~35 mm** | ~70% ↑ |
| RMSE | ~111–155 mm | **~35–37 mm** | ~75% ↑ |
| Maximum Detection Range | 100 mm | **200 mm** | 2× ↑ |

---

## 4. Real-Time Adaptive Measurement Model

### Nonlinearity Problem and Fusion Correction Algorithm

Capacitive sensors have a **nonlinear relationship** between distance and capacitance, making accurate distance estimation difficult. ToF sensors offer high accuracy but have a narrow field of view and blind spots at short range. A model that fuses both sensors to correct nonlinearity in real time is proposed.

Data is received from both the **capacitive sensor** and the **ToF sensor**, where the ToF distance is used as the reference distance.
A distance conversion model is constructed using **(X: capacitance, Y: ToF distance)** data pairs, and the coefficients $a$, $b$ are updated in real time to output accurate distance values.

$$X = a \cdot e^{b \cdot Y}$$

The degradation in distance measurement reliability as the **S/N ratio** of the capacitive sensor signal decreases is quantified using a first-order Taylor approximation.
The distance uncertainty arising from capacitive sensor noise and measurement variation is computed, and higher weights are assigned to estimates with lower uncertainty, yielding an optimally fused distance value with the ToF sensor.

<figure>
  <img src="/assets/images/projects/rmpflow-hri/Real-Time-Adaptive-Measurement-Model.png" alt="Real-Time Adaptive Measurement Model">
  <figcaption>Real-Time Adaptive Measurement Model</figcaption>
</figure>

---

## 5. RMPflow Based Control Framework with Proximity Sensor

### RMPflow Overview

**RMPflow** (Riemannian Motion Policy flow) is a framework that combines multiple policies to generate **real-time single joint acceleration commands**.

<figure>
  <img src="/assets/images/projects/rmpflow-hri/RMP-FLOW.png" alt="RMP Flow Framework">
  <figcaption>RMP Flow Framework</figcaption>
</figure>

### Applied Policy Composition

| Policy | Role |
|--------|------|
| **Target RMP** | Reaching the target position |
| **Obstacle Avoidance RMP** | Obstacle avoidance |
| **Joint Limit RMP** | Joint limit protection |
| **Joint Velocity Limit RMP** | Velocity limiting |
| **Magnetic RMP** | Path guidance |

RMPflow composes the above 5 policies into a single joint acceleration command and delivers it to the Position-Controlled System.

<figure>
  <img src="/assets/images/projects/rmpflow-hri/RMP-FLOW-Policy.png" alt="RMP Flow Policy">
  <figcaption>RMP Flow Policy</figcaption>
</figure>

---

## 6. Self-Detection Effects Before and After Compensation

### Problem Definition

When the robot moves, changes in the electric field caused by joint rotation introduce noise into the sensor readings. In addition, **Self-Detection** noise arising from mutual detection between adjacent sensors can be mistaken for actual obstacle signals, potentially causing malfunction.

### Learning-Based Compensation Model

- **Input**: Joint angle $q \in \mathbb{R}^{16}$, joint velocity $\dot{q} \in \mathbb{R}^{16}$
- **Architecture**: FC 128 → 256 → 256 → 16 (Activation: ReLU)
- **Output**: Predicted self-detection value $\hat{y}_{pred}$

<figure>
  <img src="/assets/images/projects/rmpflow-hri/SD.png" alt="SD">
  <figcaption>Learning-Based Self-Detection Modeling</figcaption>
</figure>

Compensation formula:

$$y_{comp} = y_{raw} - (\hat{y}_{pred} - \text{BASE})$$

The dataset was collected using **10 planned trajectories × 3 speed settings**.

### Performance Comparison Before and After Compensation

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| Standard Deviation | 4,003.86 | 710.53 | **82.25% ↑** |
| RMSE | 5,146.29 | 3,712.88 | 27.85% ↑ |
| Peak-to-Peak | 13,372.00 | 5,656.00 | **57.70% ↑** |

<figure>
  <img src="/assets/images/projects/rmpflow-hri/SD-RESULT.png" alt="SD-RESULT">
  <figcaption>Self-Detection Compensation Result</figcaption>
</figure>

Self-detection noise induced by the robot's own motion was **effectively eliminated** after compensation.

---

## Future Work

- Optimize **RMP parameter tuning** tailored to proximity sensor characteristics
- Enhance **End-Effector reactive motion** by integrating additional Radar and Vision sensors
- Extend the framework toward an **Avoidance Control framework** that allows the robot to maintain a safe distance from humans while continuing its task

---

## References

- H. Yim, "Reliable Proximity and Tactile Fusion Sensor Utilizing Field Sensing for Physical Human–Robot Interaction," Ph.D. dissertation, Dept. of Mechanical Engineering, Sungkyunkwan University, 2025.
- Cheng, C.-A., et al. (2019). RMPflow: A Computational Graph for Automatic Motion Policy Generation. *WAFR*.
- Wang, R., et al. (2024). A Smooth Velocity Transition Framework Based on Hierarchical Proximity Sensing for Safe HRI. *IEEE RA-L*.
- Navarro, S., et al. (2022). Proximity Perception in Human-Centered Robotics: A Survey. *IEEE TRO, 38*(3), 1599–1620.