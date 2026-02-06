---
layout: project
title: "Real-Time Reactive Control Using a Capacitive Proximity Sensor on UR10"
date: 2026-02-10
categories: [Robotics, HRI, Proximity Sensing]
---

## Overview
This project presents a **real-time adaptive reactive control framework** using a
**bendable capacitive proximity sensor** mounted on a collaborative robot manipulator (UR10).

The goal is to enable **pre-contact perception** and **safe human–robot interaction (HRI)**
by detecting nearby objects before physical contact and responding with reactive safety behaviors.

---

## Motivation
Conventional robot safety systems mainly rely on contact-based sensors or vision sensors.
However, these approaches suffer from delayed response or occlusion issues.

To address this limitation, this work focuses on:
- **Field-based proximity sensing** for pre-contact detection
- **Motion-aware signal compensation** to handle robot-induced self-detection
- **Real-time reactive control** for safety-critical scenarios

---

## System Configuration
- **Robot**: UR10 collaborative manipulator  
- **Sensor**: Bendable capacitive proximity sensor (custom-built)  
- **Processing**: Real-time sensor streaming + control loop  
- **Framework**: ROS 2-based control architecture  

Multiple proximity sensor modules were mounted on the robot links to monitor near-field interactions
around the manipulator.

---

## Key Contributions
- Design and integration of **bendable capacitive proximity sensors** on a robot manipulator
- Development of a **learning-based self-detection compensation** method using joint states
- Implementation of **reactive safety behaviors** (emergency stop and avoidance)
- Validation on a real robot system under various motion conditions

---

## Self-Detection Compensation
When the robot moves, proximity sensor signals are affected by **self-detection**
caused by robot motion and structural coupling.

To mitigate this effect:
- Joint positions and velocities were used as inputs
- A regression model predicts motion-induced sensor variations
- The predicted self-detection component is subtracted from raw sensor signals

This significantly improves obstacle detectability during robot motion.

---

## Experimental Results
- Experiments were conducted on a real UR10 manipulator
- **14 out of 16 sensor channels** showed effective self-detection compensation
- Reactive safety behaviors were successfully demonstrated in real time

---

## Publications
- **KRcC 2026 (Poster)**  
  *A Real-Time Adaptive Reactive Control Framework Using a Bendable Capacitive Proximity Sensor*

---

## Ongoing Work
- Robustness analysis with respect to cable-induced noise and sensor mounting stability
- Parameter tuning for smoother and more responsive reactive motions
- Extension from emergency stop to continuous avoidance behaviors

---

## Related Links
- GitHub Repository: https://github.com/sung-jin123  
- Poster / Video: (to be added)
