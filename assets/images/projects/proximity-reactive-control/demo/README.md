# Demo Videos (데모 동영상)

이 디렉토리에 프로젝트 데모 비디오들을 추가하세요.
Add project demo videos to this directory.

## Recommended Files (권장 파일):

### Safety Demonstrations
- `estop_demo.mp4` - Emergency stop demonstration
- `approach_detection.mp4` - Object/hand approach detection
- `reactive_avoidance.mp4` - Reactive avoidance behavior

### System Operation
- `sensor_response.mp4` - Real-time sensor visualization
- `multi_sensor_demo.mp4` - Multiple sensors working together
- `can_bus_monitor.mp4` - CAN communication monitoring

## File Specifications:
- **Format:** MP4 (H.264 codec)
- **Max Size:** 100MB per video
- **Recommended:** 1080p or 720p, 10-30MB
- **Duration:** 10-60 seconds

## Encoding Command:
```bash
ffmpeg -i input.mov -c:v libx264 -preset medium -crf 23 -c:a aac -b:a 128k output.mp4
```

See `/MEDIA_UPLOAD_GUIDE.md` for detailed instructions.
