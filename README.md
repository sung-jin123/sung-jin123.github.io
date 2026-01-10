# MESGRO - Robotics & Mechatronics Portfolio Template

![Project Page Screenshot](assets/images/project_screenshot.png)

**MESGRO** (Mechatronics Engineering Showcase Gallery for Robotics) is a comprehensive Jekyll template designed specifically for robotics and mechatronics engineers to create stunning portfolios that showcase their technical projects with interactive 3D models, circuit schematics, and detailed documentation.

[![GitHub Pages](https://img.shields.io/badge/GitHub-Pages-green.svg)](https://pages.github.com/)
[![Jekyll](https://img.shields.io/badge/Jekyll-4.3+-red.svg)](https://jekyllrb.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

<a href="https://jekyll-themes.com/[GITHUB USER NAME]/[GITHUB REPOSITORY NAME]">
  <img
    src="https://img.shields.io/badge/featured%20on-JT-red.svg"
    height="20"
    alt="Jekyll Themes Shield"
  />
</a>

## Features

- Modern & Responsive Design
- 3D Model Viewer
- Circuit Schematic Display
- Code Integration
- Rich Media Support
- Interactive Data Visualization

## Cloud Development (No Installation Required)

You can develop and maintain your portfolio completely in the cloud without installing anything on your local machine.

1. **Fork the Repository**: simple click "Fork" on GitHub.
2. **Edit Online**: Use GitHub.dev (press `.` in the repo) to edit files directly in your browser.
3. **Automatic Deployment**: Any change you push to the `main` branch will automatically trigger a GitHub Action to build and deploy your site.
4. **Validation**: Check the "Actions" tab to see if your build passed.

## Quick Start

### 1. Fork & Clone
```bash
git clone https://github.com/yourusername/MESGRO.git
cd MESGRO
```

### 2. Configure Your Site
Edit `_config.yml` to customize your portfolio details.

### 3. Run Locally (Optional)
If you prefer local development:
```bash
bundle install
bundle exec jekyll serve
```

## 📂 Project Structure

```
MESGRO/
├── _config.yml                 # Site configuration
├── _layouts/                   # Page layouts
│   ├── default.html           # Base layout
│   └── project.html           # Project page layout
├── _includes/                  # Reusable components
│   ├── header.html            # Site header
│   ├── footer.html            # Site footer
│   └── interactive-plot.html  # Plotly integration
├── _sass/                      # Sass stylesheets
│   ├── _base.scss             # Base styles and variables
│   ├── _layout.scss           # Layout styles
│   ├── _components.scss       # Component styles
│   ├── _project.scss          # Project-specific styles
│   └── _responsive.scss       # Responsive design
├── _projects/                  # Your project markdown files
├── assets/                     # Static assets
│   ├── css/                   # Compiled CSS
│   ├── js/                    # JavaScript files
│   ├── images/                # Images and photos
│   ├── models/                # 3D model files (STL, GLTF, GLB)
│   └── schematics/            # Circuit diagrams (SVG, PNG)
└── scripts/                    # Utility scripts
```

### Adding Your Project Assets

To add a new project, create the following folder structure:

```bash
assets/
├── images/projects/your-project/
│   ├── featured.jpg           # Main project image
│   └── gallery/               # Additional photos
├── models/your-project/
│   └── model.gltf             # 3D models (use cad_to_gltf.py to convert)
└── schematics/your-project/
    └── circuit.svg            # Circuit diagrams
```

> **💡 Tip:** Use the CAD-to-GLTF converter script to convert your STL/STEP files:
> ```bash
> conda run -n mesgro python scripts/cad_to_gltf.py -i model.stl -o assets/models/your-project/model.gltf
> ```

## 📝 Creating Projects

### Project Front Matter
Each project is a Markdown file in the `_projects/` directory with YAML front matter:

```yaml
---
layout: project
title: "Your Project Title"
description: "Brief project description"
date: 2024-10-30
categories: [Robotics, Arduino, Mechatronics]
featured_image: "/assets/images/projects/your-project/featured.jpg"
github_url: "https://github.com/yourusername/your-project"
demo_url: "https://youtu.be/your-demo-video"

# 3D Models
models:
  - file: "/assets/models/your-project/model.stl"
    description: "Your 3D model description"

# Circuit Schematics
schematics:
  - file: "/assets/schematics/your-project/circuit.png"
    description: "Your circuit description"

# Code Files
code_files:
  - name: "Main Code"
    file: "main.cpp"
    language: "cpp"
    download_url: "https://github.com/yourusername/your-project/blob/main/src/main.cpp"
    content: |
      // Your code here
      #include <Arduino.h>
      
      void setup() {
        Serial.begin(9600);
      }
      
      void loop() {
        // Main loop
      }

# Components List
components:
  - name: "Arduino Uno"
    quantity: 1
    description: "Main microcontroller"
    link: "https://store.arduino.cc/products/arduino-uno-rev3"

# Media gallery with images, videos, and GIFs
gallery:
  - type: "image"
    file: "/assets/images/projects/your-project/photo1.jpg"
    description: "Project photo description"
  - type: "video"
    file: "/assets/images/projects/your-project/demo.mp4"
    description: "Demo video description"
  - type: "image"
    file: "/assets/images/projects/your-project/demo.gif"
    description: "Animated GIF demonstration"
---

Your project content goes here. Use Markdown for formatting.

## Project Overview
Describe your project here...

## Technical Details
Add technical specifications, algorithms, etc...
```

### Supported File Formats

#### 3D Models
- **STL**: Most common 3D printing format
- **OBJ**: Wavefront OBJ files with materials
- **GLTF**: Modern 3D format with PBR materials
- **GLB**: Binary GLTF format

#### Media Gallery
Supports both static and dynamic content:
- **Images**: PNG, JPG, JPEG, GIF, WebP (up to 20 MB per file)
- **Videos**: MP4, WebM, AVI (up to 100 MB per file for smooth streaming)
- **GIFs**: Animated GIFs work perfectly for demonstrations (up to 20 MB)
- **Auto-detection**: File type is automatically detected by extension

**Size Recommendations**:
- Featured images: 800-1200px width (compressed to ~2-4 MB)
- Gallery images: 1000-2000px width (optimized for ~3-8 MB)
- Videos: Encode at H.264 codec, 1080p or lower (target 5-15 MB per minute)
- GIFs: Keep under 10 seconds duration, optimize with tools like giflossy

#### Video Support

Your MESGRO portfolio supports **full video playback** directly in project galleries. Videos are displayed with native HTML5 controls including:
- Play/pause controls
- Volume adjustment
- Fullscreen mode
- Playback speed control
- Progress bar and time display

**Supported Video Formats**:
- **MP4** (H.264/AVC codec) - Most compatible, recommended for all browsers ✅
- **WebM** (VP9/VP8 codec) - Modern browsers, excellent compression
- **AVI** - Legacy format, good for archival

**Adding Videos to Your Projects**:

1. Place your video file in `/assets/images/projects/your-project/`
2. Add to your project's gallery in front matter:

```yaml
gallery:
  - type: "video"
    file: "/assets/images/projects/your-project/demo.mp4"
    description: "Robot in action - Full demonstration video"
  - type: "video"
    file: "/assets/images/projects/your-project/assembly.mp4"
    description: "Assembly process time-lapse"
```

3. The video will render with full controls in the project page

**Video Encoding Best Practices**:

```bash
# Encode MP4 with good quality and compression
ffmpeg -i input.mov -c:v libx264 -preset medium -crf 23 -c:a aac -b:a 128k output.mp4

# Create a WebM version for modern browsers
ffmpeg -i input.mov -c:v libvpx-vp9 -crf 30 -c:a libopus -b:a 128k output.webm

# Optimize an AVI file
ffmpeg -i input.avi -c:v libx264 -crf 23 -c:a aac output.mp4
```

**File Size Guidelines**:
- Small clips (under 30 seconds): 2-8 MB
- Medium clips (30-2 minutes): 8-30 MB
- Longer videos: Split into multiple clips or consider hosting externally

**Performance Tips**:
- Use the `<video>` tag's native controls for best compatibility
- Compress videos before uploading to reduce bandwidth
- Provide both MP4 and WebM for maximum browser support
- For very large videos (>100 MB), consider linking to external hosting

#### Schematics
- **PNG/JPG**: Raster images
- **SVG**: Scalable vector graphics
- **PDF**: Portable document format

#### Code Languages
- C/C++, Arduino, Python, JavaScript, MATLAB, Java, and 15+ more

### Interactive Data Visualization (CSV Plugin)

MESGRO includes a powerful CSV data visualization system using **Plotly.js**. This allows you to display real-time or historical data from your projects with interactive, responsive charts.

#### How the CSV Plugin Works

The CSV visualization system consists of two main components:

**1. Interactive Plot Handler** (`_includes/interactive-plot.html`)
- Loads CSV data files and renders single or multiple plots
- Supports X/Y data correlation
- Automatically parses comma or newline-separated values
- Features loading indicators and error handling
- Perfect for time-series data, sensor readings, or performance metrics

**2. Universal Plot Handler** (`_includes/universal-plot-handler.html`)
- Handles multiple plots with column extraction
- Supports CSV files with headers
- Each plot can reference different columns from the same or different CSV files
- Great for dashboards with multiple metrics

#### Setting Up Data Visualization

**Step 1: Prepare Your CSV Files**

Create CSV files in `assets/data/plots/`:

```csv
# Example: time_data.csv
0
1
2
3
4
5

# Example: temperature_data.csv
22.5
23.1
23.8
24.2
25.1
26.3
```

Or with headers for universal plots:

```csv
time,temperature,humidity,pressure
0,22.5,45.2,1013.2
1,23.1,44.8,1013.5
2,23.8,44.5,1013.8
3,24.2,44.1,1014.2
4,25.1,43.7,1014.5
5,26.3,43.2,1014.8
```

**Step 2: Configure Your Project**

Add to your project's front matter in `_projects/your-project.md`:

```yaml
---
layout: project
title: "Your Project"
interactive_plot: true

# Simple single plot
plot_config:
  title: "Temperature Over Time"
  x_file: "/assets/data/plots/time_data.csv"
  y_file: "/assets/data/plots/temperature_data.csv"
  x_label: "Time (seconds)"
  y_label: "Temperature (°C)"

# Or use universal plots for multiple datasets
plots:
  - title: "Environmental Conditions"
    x_file: "/assets/data/plots/sensor_data.csv"
    x_column: 0
    x_label: "Time (minutes)"
    y_files:
      - file: "/assets/data/plots/sensor_data.csv"
        column: 1
        label: "Temperature (°C)"
      - file: "/assets/data/plots/sensor_data.csv"
        column: 2
        label: "Humidity (%)"
      - file: "/assets/data/plots/sensor_data.csv"
        column: 3
        label: "Pressure (hPa)"
---
```

**Step 3: Data is Automatically Visualized**

When the page renders, the CSV plugin will:
1. Load your CSV files
2. Parse the numeric data
3. Create interactive Plotly.js charts
4. Display responsive visualizations

#### CSV Plugin Features

- ✅ **Responsive Design**: Charts adapt to mobile and desktop screens
- ✅ **Interactive**: Zoom, pan, hover for data inspection
- ✅ **Dark Mode Support**: Automatic theme switching
- ✅ **Error Handling**: Graceful fallbacks if data fails to load
- ✅ **Performance**: Efficient parsing and rendering
- ✅ **No Backend Required**: Pure client-side visualization
- ✅ **Multi-file Support**: Load data from multiple CSV sources
- ✅ **Column Selection**: Choose specific columns from header-based CSVs

#### Example Use Cases

- **Sensor Data Monitoring**: Display real-time or historical readings from IoT devices
- **Performance Metrics**: Visualize robot performance data over test runs
- **Energy Consumption**: Show battery drain or solar charging patterns
- **Control System Analysis**: Plot PID controller parameters and responses
- **Environmental Conditions**: Correlate multiple environmental factors

#### File Size Limits for CSV Data

- **Recommended**: Keep CSV files under 1 MB for optimal performance
- **Soft limit**: Files up to 5 MB will load but may impact page responsiveness
- **Hard limit**: Files over 10 MB may fail to load or cause timeout

For larger datasets, consider:
- Subsampling data (every nth data point)
- Splitting into multiple smaller CSV files
- Using a server-side API instead of static files

## 🎨 Customization

### Themes
The template includes both light and dark themes. Users can toggle between them using the theme switcher in the header.

### Colors
Customize colors by editing the CSS custom properties in `_sass/_base.scss`.

## Author

**Alejandro Ojeda Olarte**

- GitHub: [@aojedao](https://github.com/aojedao)
- Website: [aojedao.github.io](https://aojedao.github.io/neumorphism)

Built with ❤️ for the robotics and mechatronics community.
