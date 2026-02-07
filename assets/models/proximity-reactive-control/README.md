# 3D Models (3D 모델)

이 디렉토리에 3D 모델 파일들을 추가하세요.
Add 3D model files to this directory.

## Recommended Files (권장 파일):

### Sensor Design
- `sensor_assembly.stl` - Complete sensor assembly
- `sensor_assembly.gltf` - Web-optimized sensor model
- `mounting_bracket.stl` - Mounting bracket

### Robot Integration
- `robot_with_sensors.gltf` - Robot with sensors mounted

## File Specifications:
- **Formats:** STL, GLTF, GLB, OBJ
- **Max Size:** 50MB for STL, 20MB for GLTF
- **Recommended:** Use GLTF for web viewing

## STL to GLTF Conversion:
```bash
# Using provided script
conda run -n mesgro python scripts/cad_to_gltf.py -i model.stl -o model.gltf

# Or use online converter
# https://products.aspose.app/3d/conversion/stl-to-gltf
```

See `/MEDIA_UPLOAD_GUIDE.md` for detailed instructions.
