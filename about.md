---
layout: default
title: About              <!-- 상단 메뉴와 브라우저 탭에 표시되는 제목 -->
<!-- permalink: /about/        <!-- About 페이지 URL --> -->
---

<!-- =======================
     HERO SECTION (페이지 최상단)
     ======================= -->
<div class="hero-section" style="padding: 100px 0; background: var(--background-color); border-bottom: 1px solid var(--border-color); text-align: center;">
    <div class="container">
        <!-- About 페이지 가장 큰 제목 -->
        <h1 style="font-size: var(--font-size-3xl); letter-spacing: -0.02em; color: var(--text-primary);">
            About Me
        </h1>

        <!-- 한 줄 요약 소개 (전공/관심분야) -->
        <p style="color: var(--text-secondary); opacity: 0.7; max-width: 760px; margin: 0 auto; font-weight: 300;">
            Graduate Student in Intelligent Robotics Engineering (SKKU).  
            I work on <strong>capacitive proximity sensing</strong>, 
            <strong>pre-contact safety</strong>, and 
            <strong>reactive robot control</strong> for HRI.
            <!-- ↑ 여기 문장만 바꾸면 최상단 소개 문구 변경됨 -->
        </p>
    </div>
</div>

<div class="about-content">
    <div class="container">

        <!-- =======================
             PROFILE / 자기소개
             ======================= -->
        <section class="about-section">
            <h2>Profile</h2>  <!-- 섹션 제목 -->

            <!-- 자기소개 본문 (누구인지, 연구 방향) -->
            <p>
                I am <strong>Sungjin Han</strong>, a graduate student focusing on safe HRI using proximity sensing.
            </p>

            <p>
                I am currently integrating multiple proximity sensor modules on a collaborative manipulator (UR10)
                and improving signal reliability under robot motion using learning-based compensation.
            </p>

            <!-- ↑ 이 두 문단을 합쳐서
                 "나는 누구이고, 지금 뭘 연구 중인가"를 설명 -->
        </section>

        <!-- =======================
             RESEARCH INTERESTS
             ======================= -->
        <section class="about-section">
            <h2>Research Interests</h2>

            <!-- 카드 형태로 연구 관심사 나열 -->
            <div class="perfect-for-grid">

                <div class="perfect-for-item">
                    <h4>Proximity Sensing</h4>
                    <p>Capacitive proximity sensors, electrode design, shielding, mounting.</p>
                </div>

                <div class="perfect-for-item">
                    <h4>HRI Safety</h4>
                    <p>Pre-contact detection, emergency stop, avoidance behaviors.</p>
                </div>

                <div class="perfect-for-item">
                    <h4>Robot Control</h4>
                    <p>Reactive motion generation and real-time control integration.</p>
                </div>

                <div class="perfect-for-item">
                    <h4>Learning for Sensors</h4>
                    <p>Self-detection compensation using joint-state based prediction.</p>
                </div>

                <!-- 카드 하나 = 관심 주제 하나
                     필요하면 div 하나 복사해서 추가 가능 -->
            </div>
        </section>

        <!-- =======================
             HIGHLIGHTS (핵심 성과)
             ======================= -->
        <section class="about-section">
            <h2>Highlights</h2>

            <!-- 프로젝트/연구 핵심 요약 카드 -->
            <div class="features-list">

                <div class="feature-item">
                    <h3><i class="fas fa-robot"></i> UR10 Proximity Integration</h3>
                    <p>
                        Integrated capacitive proximity sensors on UR10 links for pre-contact safety.
                    </p>
                </div>

                <div class="feature-item">
                    <h3><i class="fas fa-wave-square"></i> Self-Detection Compensation</h3>
                    <p>
                        Learning-based prediction of motion-induced sensor variations.
                    </p>
                </div>

                <div class="feature-item">
                    <h3><i class="fas fa-bolt"></i> Reactive Safety Behaviors</h3>
                    <p>
                        Real-time emergency stop and avoidance experiments.
                    </p>
                </div>

                <div class="feature-item">
                    <h3><i class="fas fa-tools"></i> Hardware Robustness</h3>
                    <p>
                        Cable noise, MCU fixation, and sensor mounting stability analysis.
                    </p>
                </div>

                <!-- 여기 = "내가 실제로 한 일"을 강조하는 부분
                     교수님/기업이 가장 많이 보는 섹션 -->
            </div>
        </section>

        <!-- =======================
             TECH STACK
             ======================= -->
        <section class="about-section">
            <h2>Tech Stack</h2>

            <!-- 사용 기술 아이콘 나열 -->
            <div class="tech-stack">

                <div class="tech-item">
                    <i class="fas fa-code"></i>
                    <span>C++ / Python</span>
                </div>

                <div class="tech-item">
                    <i class="fas fa-robot"></i>
                    <span>ROS2</span>
                </div>

                <div class="tech-item">
                    <i class="fas fa-microchip"></i>
                    <span>MCU + Sensors</span>
                </div>

                <div class="tech-item">
                    <i class="fas fa-chart-line"></i>
                    <span>MATLAB</span>
                </div>

                <div class="tech-item">
                    <i class="fas fa-brain"></i>
                    <span>PyTorch / ONNX</span>
                </div>

                <!-- 아이콘 + 기술명만 바꾸면 됨 -->
            </div>
        </section>

        <!-- =======================
             CONTACT / 링크
             ======================= -->
        <section class="about-section">
            <h2>Contact</h2>

            <div class="getting-started-steps">
                <li><strong>GitHub:</strong> <a href="https://github.com/sung-jin123" target="_blank">github.com/sung-jin123</a></li>
                <li><strong>Email:</strong> your@email.com</li>
                <li><strong>CV:</strong> (PDF 링크 가능)</li>
            </div>

            <!-- 버튼 영역 -->
            <div class="cta-buttons">
                <a href="{{ '/projects/' | relative_url }}" class="btn-primary">
                    View Projects
                </a>
                <a href="https://github.com/sung-jin123" class="btn-secondary" target="_blank">
                    GitHub Profile
                </a>
            </div>
        </section>

    </div>
</div>
