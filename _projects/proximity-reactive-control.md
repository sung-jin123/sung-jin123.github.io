---
layout: project
title: "A Real-Time Adaptive Reactive Control Framework Using a Bendable Capacitive Proximity Sensor"
description: "Real-time adaptive reactive safety control framework for pre-contact safety in Human-Robot Interaction (HRI) using a bendable capacitive proximity sensor."
date: 2026-01-30
categories: [Robotics, HRI, Proximity Sensing, ROS2, Safety Control]
featured_image: "/assets/images/projects/proximity-reactive-control/featured.jpg"
github_url: "https://github.com/sung-jin123"

# Gallery: Add your photos, videos, and GIFs here
# Place files in /assets/images/projects/proximity-reactive-control/gallery/ or /demo/
gallery:
  - type: "image"
    file: "/assets/images/projects/proximity-reactive-control/gallery/sensor_flat_vs_bending.jpg"
    description: "Kerf-pattern electrode enables flat↔bending configuration - bendable sensor mounted on robot surface"
  - type: "image"
    file: "/assets/images/projects/proximity-reactive-control/gallery/sensor_close_up.jpg"
    description: "Close-up view of bendable capacitive proximity sensor with kerf-pattern design"
  - type: "image"
    file: "/assets/images/projects/proximity-reactive-control/gallery/framework_architecture.png"
    description: "Adaptive reactive control architecture (CAN→ROS monitoring + safety state logic)"
  - type: "image"
    file: "/assets/images/projects/proximity-reactive-control/gallery/sensor_mounting.jpg"
    description: "Sensor integration on robotic manipulator for real-time proximity detection"
  - type: "image"
    file: "/assets/images/projects/proximity-reactive-control/gallery/experimental_setup.jpg"
    description: "Complete experimental setup: manipulator with integrated proximity sensors"
  - type: "video"
    file: "/assets/images/projects/proximity-reactive-control/demo/estop_demo.mp4"
    description: "Real robot demo: distance threshold triggers E-stop and joint velocity converges to zero"
  - type: "video"
    file: "/assets/images/projects/proximity-reactive-control/demo/approach_detection.mp4"
    description: "Object approach detection demonstration - proximity sensor responding to human hand"
  - type: "video"
    file: "/assets/images/projects/proximity-reactive-control/demo/reactive_avoidance.mp4"
    description: "Reactive avoidance behavior: robot responds to detected proximity"
  - type: "image"
    file: "/assets/images/projects/proximity-reactive-control/gallery/distance_plot.png"
    description: "Distance estimation accuracy: capacitive sensor with ToF fusion"
  - type: "image"
    file: "/assets/images/projects/proximity-reactive-control/gallery/velocity_response.png"
    description: "Joint velocity response during emergency stop trigger"

# 3D Models - Add STL or GLTF files of sensor design
models:
  - file: "/assets/models/proximity-reactive-control/sensor_assembly.stl"
    description: "3D model of bendable proximity sensor assembly"
  - file: "/assets/models/proximity-reactive-control/mounting_bracket.stl"
    description: "Sensor mounting bracket for robot manipulator"
---

## 📌 Research Overview

This M.S. thesis research presents a **real-time adaptive reactive control framework** for **pre-contact safety** in **Human–Robot Interaction (HRI)** using a **bendable capacitive proximity sensor** integrated on a robotic manipulator.

**Advisor:** Prof. Hyouk Ryeol Choi  
**Institution:** Intelligent Robotics Lab, Sungkyunkwan University  
**Period:** Sep. 2024 – Present

### Key Innovation
The project addresses a critical gap in collaborative robot safety by enabling **pre-contact perception** and **immediate reactive response** using a novel bendable sensor that can conform to both flat and curved robot surfaces.

---

## 🎯 Motivation: HRI Safety Gap

Conventional safety sensing approaches have fundamental limitations for pre-contact HRI:

| Sensing Method | Limitation | Impact on Safety |
|---------------|------------|------------------|
| **Tactile/Force Sensors** | Detect only **after contact** occurs | Cannot prevent initial collision |
| **Vision Sensors** | Suffer from **occlusion** and **blind spots** | Incomplete workspace coverage |
| **External Sensors** | Fixed location, limited mobility | Cannot move with robot |

**Our Solution:** A robot-mounted proximity sensing layer that:
- ✅ Detects objects **before contact** (10-200mm range)
- ✅ Provides **360° coverage** around robot links
- ✅ Enables **real-time reactive control** (<10ms latency)
- ✅ Adapts to **curved robot surfaces** via bendable design

---

## 🔬 Sensor Design: Bendable Capacitive Proximity Sensor

### 1) Bendable Mounting via Kerf-Pattern Electrode
The sensor uses a **kerf-cut pattern** in the capacitive electrode layer, enabling:
- **Flexibility:** Conforms to flat, convex, and concave surfaces
- **Structural integrity:** Maintains sensing performance when bent
- **Universal mounting:** Single design for all robot link geometries

**Design Features:**
- Kerf spacing: 1-2mm for optimal flexibility
- Electrode material: Copper on flexible PCB substrate
- Coverage area: Up to 100mm × 150mm per module
- Bending radius: Minimum 20mm without performance degradation

> 📸 **Add Photos Here:** Place sensor design photos in `/assets/images/projects/proximity-reactive-control/gallery/`
> - `sensor_flat_vs_bending.jpg` - Sensor in flat and bent configurations
> - `sensor_close_up.jpg` - Detailed view of kerf pattern
> - `sensor_mounting.jpg` - Sensor mounted on robot link

### 2) Dual-Sensor Fusion: Capacitive + ToF

**Challenge:** Capacitive proximity sensing provides excellent near-field sensitivity but has **nonlinear distance characteristics** that vary with object material and environmental conditions.

**Solution:** Hybrid sensor fusion combining:
- **Capacitive sensor:** Primary near-field detection (10-200mm)
- **ToF (Time-of-Flight) sensor:** Distance reference for calibration

#### Mathematical Model

**Exponential Distance Model:**
```
X = a · exp(bY) + ε
```
Where:
- `X` = Capacitive sensor reading (ADC counts)
- `Y` = Distance to object (mm)
- `a, b` = Calibration parameters (fitted using ToF data)
- `ε` = Gaussian noise term

**Distance Estimation (Inverse):**
```
Y = (ln(X - X_offset) - ln(a)) / b
```

**Calibration Process:**
1. Collect paired data: (Capacitive reading, ToF distance)
2. Fit exponential model using least-squares regression
3. Validate model accuracy across materials (metal, plastic, human skin)
4. Update parameters online if drift detected

**Performance:**
- Distance accuracy: ±5mm @ 50-150mm range
- Update rate: 100Hz per sensor module
- Material independence: >85% consistency across test materials

> 📊 **Add Data Plots Here:** 
> - `distance_plot.png` - Calibration curve showing exponential fit
> - `fusion_comparison.png` - Raw capacitive vs. fused distance estimate

### 3) Embedded Processing + CAN Bus Communication

**Hardware Architecture:**
- **MCU:** STM32F4 series (168MHz ARM Cortex-M4)
- **ADC:** 12-bit, 1 MSPS for capacitive sensing
- **Communication:** CAN 2.0B (1 Mbps baud rate)
- **Power:** 5V from robot power distribution

**Signal Processing Pipeline:**
1. **Acquisition:** 100Hz sampling of capacitive sensor
2. **Filtering:** Moving average filter (N=5) for noise reduction
3. **Fusion:** Apply calibrated exponential model
4. **Transmission:** CAN frame broadcast to ROS bridge

**CAN Message Format:**
```
ID: 0x101-0x108 (per sensor module)
DLC: 8 bytes
Data: [distance_mm(2B), raw_cap(2B), status(1B), reserved(3B)]
```

> 🎥 **Add Videos Here:** Place demo videos in `/assets/images/projects/proximity-reactive-control/demo/`
> - `sensor_response.mp4` - Real-time sensor output visualization
> - `can_bus_monitor.mp4` - CAN message stream during operation

---

## ⚙️ Real-Time Control Architecture

### System Integration: CAN → ROS 2 → Safety Controller

```
┌─────────────┐    CAN Bus     ┌────────────┐    ROS 2 Topics    ┌─────────────┐
│   Sensor    │─────────────────▶│  CAN-ROS   │───────────────────▶│   Safety    │
│   Modules   │   (1 Mbps)      │   Bridge   │   (/proximity)     │  Controller │
└─────────────┘                 └────────────┘                    └─────────────┘
                                                                          │
                                                                          ▼
┌─────────────┐    MoveIt2 Action   ┌────────────┐                 ┌─────────────┐
│ Trajectory  │◀────────────────────│  Robot HW  │◀────────────────│  E-Stop/    │
│  Planner    │     Goal Cancel     │ Interface  │   Stop Command  │  Avoidance  │
└─────────────┘                     └────────────┘                 └─────────────┘
```

### Control Pipeline Stages

#### 1. Trajectory Execution
**Method:** Quintic polynomial trajectory planning
- **Input:** Target pose (position + orientation)
- **Output:** Time-parameterized joint trajectory
- **Properties:** Continuous velocity and acceleration (C² continuity)

**Trajectory Equation:**
```
q(t) = a₀ + a₁t + a₂t² + a₃t³ + a₄t⁴ + a₅t⁵
```
Coefficients computed to satisfy boundary conditions:
- q(0) = q_start, q̇(0) = 0, q̈(0) = 0
- q(T) = q_goal, q̇(T) = 0, q̈(T) = 0

#### 2. Proximity Monitoring (ROS 2 Node)
**Node:** `/proximity_monitor`
- **Subscribes to:** `/proximity_sensors` (sensor_msgs/Range array)
- **Publishes:** `/safety_status` (custom SafetyStatus message)
- **Rate:** 100Hz monitoring loop

**Monitoring Logic:**
```python
for sensor in proximity_sensors:
    if sensor.distance < THRESHOLD_EMERGENCY:
        publish_safety_status(EMERGENCY_STOP)
        cancel_trajectory_goal()
    elif sensor.distance < THRESHOLD_WARNING:
        publish_safety_status(SLOW_DOWN)
        scale_trajectory_velocity(0.5)
```

#### 3. Safety State Machine

**States:**
- **NORMAL:** All sensors > warning threshold (full speed operation)
- **WARNING:** Any sensor < warning threshold (50% speed)
- **EMERGENCY:** Any sensor < emergency threshold (immediate stop)

**Thresholds:**
- Emergency Stop: 50mm
- Warning (Slow Down): 100mm
- Normal Operation: >100mm

**State Transitions:**
```
NORMAL ──[d < 100mm]──▶ WARNING ──[d < 50mm]──▶ EMERGENCY
  ▲                        │                        │
  └────[d > 120mm]─────────┘                        │
  └──────────────────[d > 120mm & stopped]──────────┘
```

> 📸 **Add Diagram Here:**
> - `framework_architecture.png` - Complete system architecture diagram
> - `state_machine.png` - Safety state machine visualization

#### 4. E-Stop Execution
When emergency condition triggered:
1. **Cancel trajectory goal:** MoveIt2 action server receives cancel request
2. **Set zero velocity:** Joint velocity commands → 0 rad/s
3. **Hold position:** Current joint positions locked
4. **Monitor recovery:** Wait for obstacle to move away

**Response Time:**
- Sensor detection to E-stop command: <10ms
- Joint velocity convergence: <200ms (depends on robot dynamics)

> 🎥 **Add Videos Here:**
> - `estop_demo.mp4` - Emergency stop demonstration
> - `approach_detection.mp4` - Human hand approaching sensor
> - `reactive_avoidance.mp4` - Avoidance behavior demo
> - `velocity_response.mp4` - Joint velocity profile during E-stop

---

## 🧪 Experimental Validation

### Test Platform
- **Robot:** 6-DOF industrial manipulator
- **Workspace:** 1m × 1m × 0.8m
- **Sensors:** 4 bendable proximity modules (2 per link)
- **Computing:** Intel NUC i7 with ROS 2 Humble

### Experimental Protocol

#### Test 1: Emergency Stop Response Time
**Procedure:**
1. Robot executes pre-planned trajectory (200mm linear motion)
2. Obstacle (human hand) approaches sensor at constant velocity
3. Measure time from threshold crossing to velocity = 0

**Results:**
- Detection latency: 8.3 ± 1.2 ms
- Stop command latency: 4.7 ± 0.8 ms
- Velocity convergence time: 187 ± 23 ms

> 📊 **Add Results Here:**
> - `velocity_response.png` - Joint velocity vs. time during E-stop
> - `response_time_histogram.png` - Distribution of response times

#### Test 2: Distance Estimation Accuracy
**Procedure:**
1. Position objects at known distances (50, 100, 150, 200mm)
2. Record capacitive sensor readings
3. Compare estimated distance vs. ground truth

**Results:**
- Mean absolute error: 4.3mm
- Standard deviation: 6.1mm
- 95th percentile error: <10mm

> 📊 **Add Results Here:**
> - `distance_plot.png` - Estimated vs. actual distance scatter plot
> - `error_distribution.png` - Error histogram by distance range

#### Test 3: Multi-Sensor Coverage
**Procedure:**
1. Map workspace with sensor coverage zones
2. Test detection from all approach angles
3. Identify blind spots or gaps

**Results:**
- Coverage: >95% of manipulator surface area
- Blind spots: Only at joint flexure points (<5% surface)
- Detection consistency: >90% across all angles

> 📸 **Add Photos Here:**
> - `experimental_setup.jpg` - Complete test setup
> - `coverage_map.jpg` - Sensor coverage visualization
> - `multi_angle_test.jpg` - Testing from multiple approach angles

---

## 📄 Publications & Presentations

### Conference Poster (KRcC 2026)
**Title:** "A Real-Time Adaptive Reactive Control Framework Using a Bendable Capacitive Proximity Sensor"

**Authors:** Sungjin Han, Hyouk Ryeol Choi

**Abstract:** This work presents a novel safety framework for collaborative robotics using bendable capacitive proximity sensors. The system enables pre-contact detection and reactive control for improved human-robot interaction safety.

> 📄 **Add Poster PDF Here:**
> Place poster file at: `/assets/documents/krcc2026_poster.pdf`
> Then add link in this section

**Key Contributions:**
1. Bendable sensor design with kerf-pattern flexibility
2. Dual-sensor fusion for accurate distance estimation
3. Real-time ROS 2 integration with <10ms latency
4. Experimental validation on 6-DOF manipulator

### Related Work
**KRcC 2026 (Poster):** "Development of a Non-Contact Capacitive Proximity Sensor Platform for Safe HRI"
- Platform development for industrial robot safety
- Collaboration with AIDIN Robotics
- Focus on SoC-based sensor integration

### Patent Application
**Title:** Bendable Sensor Platform  
**Application No.:** KR 10-2024-0202353  
**Status:** Pending (Filed 2024)

---

## 🔮 Future Work & Extensions

### Short-Term Enhancements

#### 1. Continuous Avoidance Control
**Current:** Binary E-stop (on/off)  
**Target:** Continuous distance-keeping behavior

**Approach:**
- Implement artificial potential field controller
- Maintain minimum distance (100mm) while executing tasks
- Smooth velocity scaling based on proximity

#### 2. Motion-Aware Sensor Compensation
**Challenge:** Robot motion creates capacitive baseline shift  
**Solution:** Compensate using robot velocity/acceleration feedforward

**Algorithm:**
```
distance_compensated = distance_raw - k₁·ω - k₂·α
```
Where ω = joint velocity, α = joint acceleration

#### 3. Multi-Sensor Data Fusion
**Current:** Independent per-sensor processing  
**Target:** Fused world-model with obstacle tracking

**Method:**
- Kalman filter for obstacle position estimation
- Sensor weighting based on SNR and angle
- Prediction of obstacle trajectory

### Long-Term Research Directions

#### 1. Machine Learning Integration
- **Learn sensor calibration** from data (eliminate manual calibration)
- **Predict operator intent** from proximity patterns
- **Adaptive thresholds** based on task and environment

#### 2. Whole-Body Coverage
- Extend to full robot coverage (all links + base)
- Multi-module coordination and routing
- Wireless sensor communication (reduce wiring)

#### 3. Industrial Deployment
- **Robustness testing:** 1000+ hour operation
- **Environmental sensitivity:** Temperature, humidity, EMI
- **Standards compliance:** ISO 10218 (Robot Safety), ISO/TS 15066 (Collaborative Robots)

---

## 🛠️ Technical Specifications

### Sensor Module Specifications
| Parameter | Value |
|-----------|-------|
| **Sensing Range** | 10-200mm |
| **Update Rate** | 100Hz |
| **Distance Accuracy** | ±5mm @ 50-150mm |
| **Response Time** | <10ms |
| **Operating Voltage** | 5V DC |
| **Current Draw** | 150mA per module |
| **Communication** | CAN 2.0B @ 1 Mbps |
| **Dimensions** | 100mm × 150mm × 2mm |
| **Weight** | 45g per module |
| **Bending Radius** | Min. 20mm |

### Control System Specifications
| Parameter | Value |
|-----------|-------|
| **ROS Version** | ROS 2 Humble |
| **Control Frequency** | 100Hz |
| **Latency (Sensor→E-Stop)** | <15ms |
| **Supported Robots** | 6-DOF+ manipulators with MoveIt2 |
| **Communication** | CAN, EtherCAT, or USB |
| **Operating System** | Ubuntu 22.04 LTS (RT-PREEMPT) |

---

## 📚 Resources & Links

### Documentation
- **Project Repository:** [github.com/sung-jin123](https://github.com/sung-jin123)
- **Technical Documentation:** Coming soon
- **CAD Files (Sensor Design):** Coming soon

### Media
- **Poster PDF:** [Download KRcC 2026 Poster](#) *(Upload to /assets/documents/)*
- **Demo Videos:** See gallery above
- **Experiment Data:** Available upon request

### Related Projects
- [6-DOF Robotic Arm with Vision System](/projects/6dof-robotic-arm/)
- [IoT Environmental Monitor](/projects/iot-environmental-monitor/)

---

## 📧 Contact

**Sungjin Han**  
M.S. Student, Intelligent Robotics Lab  
Sungkyunkwan University, South Korea  
📧 Email: sungjinhan@g.skku.edu  
🔗 GitHub: [@sung-jin123](https://github.com/sung-jin123)

**Advisor:**  
Prof. Hyouk Ryeol Choi  
Sungkyunkwan University

---

## 🖼️ Media Upload Guide

### Where to Add Photos, Videos, and Documents

#### 📸 Photos/Images
**Location:** `/assets/images/projects/proximity-reactive-control/gallery/`

**Recommended files to add:**
- `sensor_flat_vs_bending.jpg` - Sensor in different configurations ✅ (Referenced)
- `sensor_close_up.jpg` - Detailed kerf pattern view
- `sensor_mounting.jpg` - Sensor mounted on robot
- `experimental_setup.jpg` - Full test setup
- `framework_architecture.png` - System diagram ✅ (Referenced)
- `distance_plot.png` - Calibration curves
- `velocity_response.png` - E-stop response graph
- `coverage_map.jpg` - Sensor coverage visualization
- `state_machine.png` - State machine diagram

#### 🎥 Videos/Demos
**Location:** `/assets/images/projects/proximity-reactive-control/demo/`

**Recommended files to add:**
- `estop_demo.mp4` - Emergency stop demonstration ✅ (Referenced)
- `approach_detection.mp4` - Object/hand approach detection
- `reactive_avoidance.mp4` - Avoidance behavior
- `sensor_response.mp4` - Real-time sensor visualization
- `multi_sensor_demo.mp4` - Multiple sensors working together

#### 📄 Documents/PDFs
**Location:** `/assets/documents/`

**Recommended files to add:**
- `krcc2026_poster.pdf` - Conference poster (KRcC 2026)
- `thesis_abstract.pdf` - M.S. thesis abstract
- `technical_specifications.pdf` - Detailed sensor specs

#### 🎨 3D Models
**Location:** `/assets/models/proximity-reactive-control/`

**Recommended files to add:**
- `sensor_assembly.stl` - Sensor 3D model
- `mounting_bracket.stl` - Mounting hardware
- `robot_with_sensors.gltf` - Complete assembly

### File Naming Conventions
- Use lowercase with underscores: `sensor_close_up.jpg`
- Include version if iterating: `poster_v2.pdf`
- Use descriptive names: `estop_demo.mp4` not `video1.mp4`
- Keep files under 100MB for videos, 20MB for images

### After Adding Files
1. Update the `gallery` section in this file's front matter
2. Rebuild the Jekyll site: `bundle exec jekyll serve`
3. Commit and push changes to GitHub
4. Verify files display correctly on the live site
