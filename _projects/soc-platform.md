---
layout: project
title: "로봇충돌 안전용 SoC 통합플랫폼 개발"
date: 2025-01-01
categories: [Robotics, Sensor, PCB, ROS2]
featured: true
published: true
featured_image: "/assets/images/projects/soc-platform/featured.png"
excerpt: "실시간 충돌상황 감지 및 회피 지능이 탑재된 로봇충돌 안전용 SoC 통합플랫폼 개발 프로젝트 (산업통상자원부, 2024.04 ~ 2026.12)"

schematics:
  - file: "/assets/images/projects/soc-platform/sensor_structure.png"
    title: "Proximity Sensor Module Structure"
    description: "근접센서 통합 플랫폼 기본 구조 및 Layer 구성"
  - file: "/assets/images/projects/soc-platform/asic_hw.png"
    title: "ASIC-Applied Sensor H/W Prototype"
    description: "개발 ASIC(NXA3110)을 적용한 모바일 로봇용 및 매니퓰레이터용 근접센서 모듈 H/W 시작품"

video: "/assets/videos/soc-platform/demo.mp4"
---

## Project Overview

본 프로젝트는 산업통상자원부 차세대지능형반도체기술개발 사업의 일환으로, **실시간 충돌상황 감지 및 회피 지능이 탑재된 로봇충돌 안전용 SoC 통합플랫폼**을 개발하는 연구입니다.

- **과제 기간:** 2024년 4월 1일 ~ 2026년 12월 31일 (총 2년 9개월)
- **참여 기관:** 에이딘로보틱스(주관), 넥스트랩㈜, 성균관대학교
- **담당 역할:** 충돌안전 intelligence 알고리즘 개발 및 로봇 어플리케이션 실증 (성균관대학교)

---

## Background & Motivation

협업 서비스 로봇 산업의 확대로 사람과 로봇이 같은 작업공간을 공유하는 환경이 증가함에 따라, **안전성과 기능성**에 대한 요구가 높아지고 있습니다. 기존 산업용 로봇은 안전펜스로 작업자와 분리되었으나, 협동로봇은 안전펜스 없이 사람과 함께 동작해야 하므로 실시간 충돌 감지 및 회피를 위한 **안전용 센서**의 필요성이 대두되었습니다.

### Why Capacitive Proximity Sensor?

정전용량형 근접센서는 기존 ToF, 라이다, 비전, 레이더 센서 대비 다음과 같은 강점을 가집니다.

- **넓은 FoV**: 하나의 센서로 넓은 면적을 커버 가능
- **빠른 반응 속도**: 별도의 신호처리 PC 없이 실시간 처리
- **저렴한 비용**: 소수의 센서로 로봇 전체를 커버 가능, 시스템 구성 비용 낮음

---

## Development Goals

### 충돌 안전센서 기반 기술 개발 (에이딘로보틱스 / 넥스트랩)

근접감지가 가능한 로봇 충돌 안전용 SoC를 개발하고, 모바일 로봇 및 매니퓰레이터에 적용 가능한 근접센서 모듈 기구부를 설계합니다.

- 정전용량 측정 ASIC(NXA3110) 개발 및 적용
- I2C / CAN Interface 기반 실시간 데이터 취득 시스템 구성
- 모바일 로봇용 및 매니퓰레이터용 두 가지 형태의 시작품 제작

### 충돌안전 Intelligence 알고리즘 개발 (성균관대학교)

- **접촉/비접촉 상황 인식 알고리즘**: Curve fitting으로 센서 rawdata를 거리값으로 선형화
- **환경 보상 알고리즘**: Twin Circuit 기반 온도 드리프트 실시간 보정 (변동성 98.83% 개선)
- **Intelligence Safety Framework**: Precaution / Warning / Emergency Stop 3단계 위험도 판단 및 로봇 속도 제어

---

## ASIC Performance Results (2nd Year)

개발 ASIC(NXA3110)과 기존 상용칩(TI사 FDC2214)을 동일 환경에서 비교 테스트한 결과:

| 항목 | FDC2214 (상용) | NXA3110 (개발) |
|---|---|---|
| 해상도 | 28 bit | 24 bit |
| 변환속도 | 1,000 Hz | 1,000 Hz |
| 노이즈 [code] | 737.4 | **176.05** |
| SNR | 49.84 | **61.58** |
| 최대 감지거리 | 15 cm | **22 cm** |

- SNR 기준 **23% 향상**, 최대 감지거리 **47% 증가 (15cm → 22cm)**
- 100번 반복 성능 테스트에서 **98% 성공률** 확인
- 충돌 감지 속도 **10ms 이내** 확인

---

## Intelligence Safety Framework

로봇의 실시간 장애물 대응을 위한 3단계 safety framework를 개발하였습니다.

- **Precaution (25cm 이상):** 정상 속도 주행 (`q_command`)
- **Warning (10~25cm):** 속도 절반으로 감속 (`½ q_command`)
- **Emergency Stop (10cm 이하):** 즉시 정지 (`0`)

센서의 근거리 sensing intelligence 알고리즘이 수신한 거리값을 Variable Speed Scaling을 통해 Position Control로 전달하며, 매니퓰레이터 및 모바일 로봇 양쪽에 적용 검증을 진행 중입니다.

---

## Acknowledgement

본 연구는 산업통상자원부의 차세대지능형반도체기술개발 사업(과제번호: RS-2024-00407393)의 지원을 받아 수행되었습니다.
