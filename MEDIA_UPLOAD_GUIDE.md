# Media Upload Guide (미디어 업로드 가이드)

이 가이드는 논문 및 포스터와 관련된 사진, 동영상, 문서를 어디에 추가해야 하는지 설명합니다.

This guide explains where to add photos, videos, and documents related to your papers and posters.

---

## 📂 Directory Structure (디렉토리 구조)

```
assets/
├── images/
│   └── projects/
│       └── proximity-reactive-control/
│           ├── featured.jpg              # 프로젝트 대표 이미지
│           ├── gallery/                  # 📸 사진들을 여기에 추가
│           │   ├── sensor_flat_vs_bending.jpg
│           │   ├── sensor_close_up.jpg
│           │   ├── sensor_mounting.jpg
│           │   ├── experimental_setup.jpg
│           │   ├── framework_architecture.png
│           │   ├── distance_plot.png
│           │   ├── velocity_response.png
│           │   └── coverage_map.jpg
│           └── demo/                     # 🎥 동영상들을 여기에 추가
│               ├── estop_demo.mp4
│               ├── approach_detection.mp4
│               ├── reactive_avoidance.mp4
│               └── sensor_response.mp4
├── documents/                            # 📄 PDF 문서들을 여기에 추가
│   ├── krcc2026_poster.pdf
│   └── thesis_abstract.pdf
└── models/
    └── proximity-reactive-control/       # 🎨 3D 모델들을 여기에 추가
        ├── sensor_assembly.stl
        └── mounting_bracket.stl
```

---

## 📸 1. Photos/Images (사진/이미지)

### Location (위치):
```
/assets/images/projects/proximity-reactive-control/gallery/
```

### Recommended Files to Add (추가 권장 파일):

#### Sensor Design (센서 디자인)
- ✅ `sensor_flat_vs_bending.jpg` - 평평한 상태와 구부러진 상태의 센서
  - Shows the bendable sensor in flat and curved configurations
  - Demonstrates kerf-pattern flexibility

- 📷 `sensor_close_up.jpg` - 센서의 상세 클로즈업
  - Close-up of the kerf pattern electrode design
  - Shows the bendable structure details

- 📷 `sensor_mounting.jpg` - 로봇에 장착된 센서
  - Sensor mounted on robot manipulator
  - Shows integration on robot surface

#### Experimental Setup (실험 설정)
- 📷 `experimental_setup.jpg` - 전체 실험 장치
  - Complete test setup with robot and sensors
  - Overview of the experimental environment

- 📷 `multi_angle_test.jpg` - 다양한 각도에서의 테스트
  - Testing sensor from multiple approach angles
  - Shows sensor coverage testing

#### System Architecture (시스템 구조)
- ✅ `framework_architecture.png` - 시스템 아키텍처 다이어그램
  - Complete control architecture (CAN → ROS → Safety Logic)
  - Already referenced in project file

- 📷 `state_machine.png` - 안전 상태 머신
  - Safety state machine diagram
  - Shows NORMAL → WARNING → EMERGENCY transitions

#### Data & Results (데이터 및 결과)
- 📷 `distance_plot.png` - 거리 추정 정확도
  - Calibration curve (capacitive reading vs. actual distance)
  - Shows exponential model fit

- 📷 `velocity_response.png` - E-stop 시 속도 응답
  - Joint velocity vs. time during emergency stop
  - Demonstrates rapid deceleration

- 📷 `coverage_map.jpg` - 센서 커버리지 맵
  - Visualization of sensor coverage on robot
  - Shows detection zones

---

## 🎥 2. Videos/Demos (동영상/데모)

### Location (위치):
```
/assets/images/projects/proximity-reactive-control/demo/
```

### Recommended Files to Add (추가 권장 파일):

#### Safety Demonstrations (안전 기능 시연)
- ✅ `estop_demo.mp4` - 긴급 정지 데모
  - Emergency stop triggered by proximity threshold
  - Shows joint velocity converging to zero
  - Already referenced in project file

- 🎬 `approach_detection.mp4` - 접근 감지
  - Human hand or object approaching sensor
  - Real-time proximity detection response

- 🎬 `reactive_avoidance.mp4` - 반응형 회피
  - Robot avoiding detected obstacle
  - Demonstrates reactive safety behavior

#### System Operation (시스템 동작)
- 🎬 `sensor_response.mp4` - 실시간 센서 출력
  - Real-time visualization of sensor readings
  - Distance estimation in action

- 🎬 `multi_sensor_demo.mp4` - 다중 센서 동작
  - Multiple sensors working together
  - Coordinated proximity detection

- 🎬 `can_bus_monitor.mp4` - CAN 버스 모니터링
  - CAN message stream visualization
  - Shows real-time data communication

### Video Specifications (동영상 사양):
- **Format (포맷):** MP4 (H.264 codec preferred)
- **Resolution (해상도):** 1080p or 720p
- **File Size (파일 크기):** < 100MB per video
- **Duration (길이):** 10-60 seconds for demos

### Encoding Tips (인코딩 팁):
```bash
# Convert to web-optimized MP4
ffmpeg -i input.mov -c:v libx264 -preset medium -crf 23 -c:a aac -b:a 128k output.mp4

# Reduce file size if needed
ffmpeg -i input.mp4 -vf scale=1280:720 -c:v libx264 -crf 28 output_small.mp4
```

---

## 📄 3. Documents/PDFs (문서/PDF)

### Location (위치):
```
/assets/documents/
```

### Recommended Files to Add (추가 권장 파일):

#### Conference Materials (학회 자료)
- 📄 `krcc2026_poster.pdf` - KRcC 2026 포스터
  - Conference poster: "A Real-Time Adaptive Reactive Control Framework..."
  - High-resolution PDF for download

- 📄 `krcc2026_platform_poster.pdf` - KRcC 2026 플랫폼 포스터
  - Related poster: "Development of a Non-Contact Capacitive Proximity Sensor Platform..."

#### Thesis Materials (논문 자료)
- 📄 `thesis_abstract.pdf` - 석사 논문 초록
  - M.S. thesis abstract in English
  - Summary of research contributions

- 📄 `thesis_abstract_kr.pdf` - 석사 논문 초록 (한글)
  - Korean version of thesis abstract

#### Technical Documentation (기술 문서)
- 📄 `technical_specifications.pdf` - 기술 사양서
  - Detailed sensor specifications
  - Hardware and software requirements

- 📄 `user_manual.pdf` - 사용자 매뉴얼
  - Installation and operation guide
  - Troubleshooting information

---

## 🎨 4. 3D Models (3D 모델)

### Location (위치):
```
/assets/models/proximity-reactive-control/
```

### Recommended Files to Add (추가 권장 파일):

#### Sensor Design Models (센서 디자인 모델)
- 🎨 `sensor_assembly.stl` - 센서 조립체
  - Complete sensor assembly 3D model
  - For 3D printing or visualization

- 🎨 `sensor_assembly.gltf` - 센서 조립체 (웹용)
  - Web-optimized GLTF format
  - Interactive 3D viewer on website

#### Mounting Hardware (장착 하드웨어)
- 🎨 `mounting_bracket.stl` - 장착 브래킷
  - Bracket for mounting sensor to robot
  - 3D printable design

- 🎨 `robot_with_sensors.gltf` - 센서가 장착된 로봇
  - Complete robot assembly with sensors
  - Shows sensor placement

### 3D Model Conversion (3D 모델 변환):
```bash
# Convert STL to GLTF for web viewing
conda run -n mesgro python scripts/cad_to_gltf.py -i sensor.stl -o sensor.gltf

# Or use online converters:
# - https://products.aspose.app/3d/conversion/stl-to-gltf
# - https://www.greentoken.de/onlineconv/
```

---

## 📝 5. Featured Image (대표 이미지)

### Current Featured Image (현재 대표 이미지):
```
/assets/images/projects/proximity-reactive-control/featured.jpg
```

This image appears on:
- Project listing page (프로젝트 목록 페이지)
- Home page portfolio showcase (홈페이지 포트폴리오)
- Project header (프로젝트 헤더)

### Recommendations (권장 사항):
- **Resolution (해상도):** 1200x800 pixels or similar 3:2 aspect ratio
- **File size (파일 크기):** < 2MB (optimize for web)
- **Content (내용):** 
  - Show the robot with sensors clearly visible
  - Professional lighting and composition
  - Captures the essence of the project

---

## 🚀 After Adding Files (파일 추가 후)

### Step 1: Update Project File (프로젝트 파일 업데이트)
Edit `/home/runner/work/sung-jin123.github.io/sung-jin123.github.io/_projects/proximity-reactive-control.md`

The `gallery` section in the front matter already references these files:
```yaml
gallery:
  - type: "image"
    file: "/assets/images/projects/proximity-reactive-control/gallery/sensor_close_up.jpg"
    description: "Close-up view of bendable sensor"
  - type: "video"
    file: "/assets/images/projects/proximity-reactive-control/demo/approach_detection.mp4"
    description: "Object approach detection demo"
```

### Step 2: Test Locally (로컬 테스트)
```bash
cd /home/runner/work/sung-jin123.github.io/sung-jin123.github.io
bundle exec jekyll serve
# Visit: http://localhost:4000/projects/proximity-reactive-control/
```

### Step 3: Commit and Push (커밋 및 푸시)
```bash
git add assets/
git commit -m "Add media files for proximity-reactive-control project"
git push origin main
```

### Step 4: Verify on GitHub Pages (GitHub Pages 확인)
- Wait 2-3 minutes for GitHub Pages to rebuild
- Visit: https://sung-jin123.github.io/projects/proximity-reactive-control/
- Check that all media displays correctly

---

## 📐 File Size Guidelines (파일 크기 가이드라인)

| File Type | Maximum Size | Recommended Size |
|-----------|--------------|------------------|
| **Images (JPEG/PNG)** | 20MB | 2-4MB (1200px width) |
| **Videos (MP4)** | 100MB | 10-30MB (1080p, compressed) |
| **PDFs** | 50MB | 2-10MB |
| **3D Models (STL)** | 50MB | 5-20MB |
| **3D Models (GLTF)** | 20MB | 2-10MB (web-optimized) |

---

## 🔧 Optimization Tools (최적화 도구)

### Image Compression (이미지 압축)
```bash
# Install ImageMagick
sudo apt-get install imagemagick

# Compress JPEG
convert input.jpg -quality 85 -resize 1200x output.jpg

# Compress PNG
optipng -o5 input.png
```

### Video Compression (동영상 압축)
```bash
# Install FFmpeg
sudo apt-get install ffmpeg

# Compress video
ffmpeg -i input.mp4 -c:v libx264 -crf 23 -preset medium -c:a aac -b:a 128k output.mp4
```

### PDF Compression (PDF 압축)
```bash
# Install Ghostscript
sudo apt-get install ghostscript

# Compress PDF
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook \
   -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf
```

---

## ❓ FAQ (자주 묻는 질문)

### Q1: 파일을 업로드했는데 사이트에 표시되지 않습니다
**A:** GitHub Pages는 빌드하는 데 2-3분이 걸립니다. 기다린 후 새로고침하세요.

### Q2: 비디오가 재생되지 않습니다
**A:** MP4 형식(H.264 코덱)을 사용하세요. 다른 형식은 모든 브라우저에서 작동하지 않을 수 있습니다.

### Q3: 이미지가 너무 큽니다
**A:** 위의 이미지 압축 도구를 사용하여 파일 크기를 줄이세요.

### Q4: 3D 모델이 표시되지 않습니다
**A:** GLTF 형식을 사용하고 파일이 `/assets/models/` 디렉토리에 있는지 확인하세요.

---

## 📧 Contact (연락처)

If you need help with media upload:
미디어 업로드에 도움이 필요하시면:

**Sungjin Han**  
📧 Email: sungjinhan@g.skku.edu  
🔗 GitHub: [@sung-jin123](https://github.com/sung-jin123)

---

## ✅ Checklist (체크리스트)

Before finalizing your portfolio (포트폴리오를 완성하기 전에):

- [ ] Add featured image (`featured.jpg`)
- [ ] Add sensor design photos (minimum 2-3 photos)
- [ ] Add experimental setup photo
- [ ] Add at least 1 demo video (e.g., `estop_demo.mp4`)
- [ ] Add conference poster PDF (`krcc2026_poster.pdf`)
- [ ] Add system architecture diagram
- [ ] Add data visualization plots (optional but recommended)
- [ ] Update project file gallery section
- [ ] Test locally with `bundle exec jekyll serve`
- [ ] Commit and push to GitHub
- [ ] Verify on live site

---

**Last Updated:** 2026-02-07  
**Version:** 1.0
