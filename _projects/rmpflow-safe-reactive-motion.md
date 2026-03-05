---
layout: project
title: "RMPflow-Based Safe Reactive Motion Planning Using Proximity Sensors for Human-Robot Interaction"
description: "벤더블 정전용량 근접 센서의 단계별 개발과 RMPflow 기반 실시간 반응형 안전 제어 프레임워크 연구 (석사 세미나 1~4차)"
date: 2026-01-30
categories: [Robotics, HRI, Sensor, ROS, RMPflow]
featured_image: "/assets/images/projects/rmpflow-hri/featured.png"
github_url: ""
demo_url: ""
---

## 연구 개요

본 연구는 **인간-로봇 상호작용(HRI)** 환경의 안전한 협동 작업을 위해, 평면 및 곡면 모두에 부착 가능한 **벤더블 정전용량 근접 센서**를 단계적으로 개발하고, 최종적으로 **RMPflow** 기반 반응형 모션 제어 프레임워크와 통합한 석사과정 연구입니다.

사람과 로봇의 협업의 레벨이 높아질수록 신뢰할 수 있는 HRC 기술 개발이 필수적입니다. 따라서 로봇이 외부 환경을 인식할 수 있는 센서 기술이 강조되고 있습니다. 
기존 안전 센서들은 사각지대, 근거리 감지 한계, 곡면 부착 불가 등의 문제를 갖습니다. 
---

## 1. Mechanically Bendable Sensor Structure (Planar + Planar) 개발

### 설계 배경

정전용량형 센서는 전기장을 이용해 물체의 접근을 감지합니다. Self-Capacitance 방식의 원리는 아래와 같습니다:

$$C \approx \varepsilon_0 \varepsilon_r \frac{2 A_1 A_2}{A_1 + A_2} \cdot \frac{1}{d}$$

<figure>
  <img src="/assets/images/projects/rmpflow-hri/capacitive-principle.png" alt="Single-Ended Capacitance Principle">
  <figcaption>Single-Ended Capacitance Principle</figcaption>
</figure>

거리 $d$가 감소할수록 정전용량 $C$가 증가합니다. 여기에 **Kerf 패턴**을 전극에 적용해 Flat ↔ Bending 자유 변환이 가능한 벤더블 구조를 최초 설계했습니다.

### 구조 구성

- **Electrode (1)**: Planar-Type (상단)
- **Electrode (2)**: Planar-Type (하단)
- **Shield Electrode**: 외부 노이즈 차폐
- **ToF Sensor × 2**: 거리 보정용 융합 센서
- **MCU + FDC2214**: 정전용량 측정 및 CAN 전송

<figure>
  <img src="/assets/images/projects/rmpflow-hri/capacitive-principle.png" alt="Single-Ended Capacitance Principle">
  <figcaption>Single-Ended Capacitance Principle</figcaption>
</figure>

### 한계점

두 전극이 동일한 Planar 구조이므로 Bending 시 전극 간 **정전용량 불균형(Capacitance Imbalance)** 이 발생하여 정확한 거리 추정이 어려웠습니다.

| 지표 | Planar | Loop |
|------|--------|------|
| 표준 편차 | 104.3 mm | 120.2 mm |
| RMSE | 111.0 mm | 154.8 mm |
| 최대 감지 범위 | 100 mm | 100 mm |

---

## 2. Mechanically Bendable Sensor Structure (Planar + Loop) 개발

### 전극 설계 변경

Planar + Planar 구조의 불균형 문제를 해결하기 위해 하단 전극을 **Loop-Type**으로 교체했습니다. Loop 전극은 중앙이 비어 있어 상단 Planar 전극과의 전기장 중첩 면적이 줄고, 두 전극 간 정전용량 불균형이 감소합니다.

### ToF 커버 고정 방식 비교

Loop-Type 전극 도입과 함께 ToF 센서 고정 구조도 3종 비교·검증했습니다:

| 방식 | 특징 |
|------|------|
| Horizontal Fix Type | 가로 방향 고정, 안정적 |
| Line Fix Type | 선형 고정, 경량 |
| Vertical Fix Type | 세로 방향 고정 |

### 검증 결과 및 한계

두 전극(Planar / Loop)의 응답 경향이 정합적으로 동작함을 확인했으나, Bending 시 **전극 형상 변화에 따른 재보정**이 필요하고 **전극 적층으로 인한 단거리 정확도 저하** 문제가 남았습니다.

---

## 3. [GEN3] Bendable Sensor 개발

### 개선 목표

| 항목 | 이전 세대 한계 | Gen3 개선 방향 |
|------|--------------|--------------|
| 전극 중첩 | 단거리 정확도 저하 | 전극 분리 재설계 |
| 제조성 | 1 mm 간격 패턴 제조 불가 | 제조 가능 패턴으로 수정 |
| 크기 | 150×150 mm (로봇 통합 불가) | **190×80 mm** 로 최적화 |
| Kerf 구조 | 유지 필요 | Flat-Bending 구조 보존 |

### 전극 면적 최적화

다양한 샘플 비교를 통해 감지 성능과 제조성을 동시에 만족하는 **190×80 mm** 크기를 최종 선정했습니다.

### UR10 전신 통합

UR10의 **상완(Upper Arm)** 과 **하완(Lower Arm)** 에 각 4개씩 총 **8개의 Gen3 센서 모듈**을 장착해 전방위 근접 감지 커버리지를 구축했습니다.

### 성능 비교 (이전 세대 대비)

| 지표 | 이전 세대 | **Gen3** | 개선 |
|------|----------|---------|------|
| 표준 편차 | ~104–120 mm | **~35 mm** | ~70% ↑ |
| RMSE | ~111–155 mm | **~35–37 mm** | ~75% ↑ |
| 최대 감지 범위 | 100 mm | **200 mm** | 2배 ↑ |

---

## 4. Real-Time Adaptive Measurement Model

### 정전용량-거리 비선형성 문제

정전용량 센서는 거리와 정전용량 간 **비선형 관계**를 가져 정확한 거리 추정이 어렵습니다. ToF 센서는 정확도가 높지만 시야각이 좁고 근거리 사각지대가 존재합니다. 두 센서를 융합해 비선형성을 실시간으로 보정하는 모델을 제안합니다.

### 융합 보정 알고리즘

두 센서의 중첩 시야각에서 수집한 데이터 쌍 $(X_{ToF},\, C)$ 를 **이중 지수 방정식**으로 근사합니다:

$$\hat{d} = a \cdot e^{\,b \cdot C} + c \cdot e^{\,d' \cdot C}$$

최소제곱법으로 계수 $a, b, c, d'$ 를 **동적으로 추정**하며, Bending 등 구조 변화 시에도 자동 재보정됩니다.

### 시스템 파이프라인

```
FDC2214 (정전용량 측정)
        ↓
   STM32 MCU (100 Hz, CAN 전송)
        ↓
ROS Distance Fitting Node
(ToF 융합 + 적응형 계수 추정)
        ↓
  선형화된 거리 데이터 출력
```

---

## 5. RMPflow Based Control Framework with Proximity Sensor

### RMPflow 개요

**RMPflow** (Riemannian Motion Policy flow)는 복수의 반응형 정책을 Computational Graph로 합성하여 **실시간 단일 관절 가속도 명령**을 생성하는 프레임워크입니다.

> *Cheng et al., RMPflow: A Computational Graph for Automatic Motion Policy Generation, WAFR 2019*

### 적용 정책 구성

| 정책 | 역할 |
|------|------|
| **Target RMP** | 목표 지점 도달 |
| **Obstacle Avoidance RMP** | 장애물 회피 |
| **Joint Limit RMP** | 관절 한계 보호 |
| **Joint Velocity Limit RMP** | 속도 제한 |
| **Magnetic RMP** | 경로 유도 |

RMPflow는 위 5개 정책을 합성하여 단일 관절 가속도 명령으로 해석하고, 이를 Position-Controlled System에 전달합니다.

### 제어 아키텍처

```
근접 센서 8모듈 (UR10 상완/하완)
        ↓  CAN Bus (100 Hz)
     STM32 MCU
        ↓  ROS Topic
 Distance Fitting Node
 (ToF 융합 + 적응형 선형화)
        ↓
 3D Point Transformation
        ↓
    RMPflow Engine
 (5개 정책 합성 → 단일 가속도)
        ↓
 Position-Controlled System (UR10)
```

### 실험 결과

- 2개 센서 모듈 기반 RMPflow 실험에서 **장애물 회피 반응 동작** 확인
- 장애물 접근 시 임계값 이내 거리가 감지되는 순간 **모든 관절 속도가 즉각 0으로 수렴**하는 비상정지 동작 검증

---

## 6. Self-Detection Effects Before and After Compensation

### 문제 정의

로봇이 움직일 때 **관절 회전에 의한 전기장 변화**가 센서 값에 노이즈로 유입됩니다. 이 **자기 감지(Self-Detection)** 노이즈는 실제 장애물 신호와 혼동되어 오작동을 유발할 수 있습니다.

### 딥러닝 기반 보상 모델

- **입력**: 관절 각도 $q \in \mathbb{R}^{16}$, 관절 속도 $\dot{q} \in \mathbb{R}^{16}$
- **구조**: FC 128 → 256 → 256 → 16 (활성화: ReLU)
- **출력**: 예측된 자기 감지 값 $\hat{y}_{pred}$

보상 공식:

$$y_{comp} = y_{raw} - (\hat{y}_{pred} - \text{BASE})$$

데이터셋은 **10개의 계획 궤적 × 3가지 속도 설정** 조합으로 수집했습니다.

### 보상 전후 성능 비교

| 지표 | 보상 전 | 보상 후 | 개선율 |
|------|--------|--------|--------|
| 표준 편차 | 4,003.86 | 710.53 | **82.25% ↑** |
| RMSE | 5,146.29 | 3,712.88 | 27.85% ↑ |
| Peak-to-Peak | 13,372.00 | 5,656.00 | **57.70% ↑** |

로봇 자체 동작에 의해 유발된 자기 감지 노이즈가 보상 후 **효과적으로 제거**됨을 확인했습니다.

---

## 향후 연구 계획

- 근접 센서 특성에 맞는 **RMP 파라미터 튜닝** 최적화
- Radar 및 Vision 센서 추가 융합을 통한 **End-Effector 반응 모션 강화**
- 인간과 안전 거리를 유지하며 작업을 지속하는 **Avoidance Control 프레임워크** 확장

---

## 참고문헌

- Han, S., Kang, H., Sung, H., Song, Y., & Choi, H. R. (2025). A Real-Time Adaptive Reactive Control Framework Using a Bendable Capacitive Proximity Sensor. *한국로봇학회 (KROC)*.
- Cheng, C.-A., et al. (2019). RMPflow: A Computational Graph for Automatic Motion Policy Generation. *WAFR*.
- Wang, R., et al. (2024). A Smooth Velocity Transition Framework Based on Hierarchical Proximity Sensing for Safe HRI. *IEEE RA-L*.
- Navarro, S., et al. (2022). Proximity Perception in Human-Centered Robotics: A Survey. *IEEE TRO, 38*(3), 1599–1620.
