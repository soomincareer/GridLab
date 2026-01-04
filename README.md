# Module Grid Generator

명암 차이로 형상을 만드는 그래픽 패턴 생성기

## 🚀 빠른 시작

### 1. 필요한 패키지 설치

```bash
pip install pillow numpy
```

### 2. 폴더 구조 준비

```
project/
├── module_grid_generator.py
├── modules/
│   ├── 01.png  # 가장 밝은 모듈
│   ├── 02.png
│   ├── 03.png
│   ├── ...
│   └── 10.png  # 가장 어두운 모듈
├── horse.jpg   # 형상으로 만들 이미지
└── output.png  # (생성됨)
```

### 3. 실행

**기본 사용:**
```bash
python module_grid_generator.py -m ./modules -t ./horse.jpg
```

**그리드 크기 지정:**
```bash
python module_grid_generator.py -m ./modules -t ./horse.jpg -g 50x70
```

**명암 반전 (밝은 부분에 어두운 모듈):**
```bash
python module_grid_generator.py -m ./modules -t ./horse.jpg -i
```

**고해상도 출력:**
```bash
python module_grid_generator.py -m ./modules -t ./horse.jpg -d 600 -o result_high.png
```

## 📋 모듈 이미지 준비 팁

1. **정사각형으로 만들기**: 모든 모듈을 같은 크기로 (예: 100x100px)
2. **명암 범위**: 가장 밝은 것부터 가장 어두운 것까지 골고루 분포
3. **파일명**: 숫자나 알파벳 순으로 정렬되도록 (01.png, 02.png...)
4. **권장 크기**: 개별 모듈은 50-200px 정도면 충분

## 🎨 엽서 크기 프리셋

### 표준 엽서 (148 x 100mm, 300dpi)
```bash
# 그리드 계산: 148mm = 1748px, 100mm = 1181px (300dpi 기준)
# 모듈 100px이면: 17x11 그리드

python module_grid_generator.py -m ./modules -t ./horse.jpg -g 17x11 -d 300
```

### A6 크기 (148 x 105mm, 300dpi)
```bash
python module_grid_generator.py -m ./modules -t ./horse.jpg -g 17x12 -d 300
```

### 정사각형 (100 x 100mm, 300dpi)
```bash
python module_grid_generator.py -m ./modules -t ./horse.jpg -g 11x11 -d 300
```

## 🔧 고급 옵션

### Python 스크립트로 직접 제어

```python
from module_grid_generator import ModuleGridGenerator

generator = ModuleGridGenerator(
    module_folder="./modules",
    target_image="./horse.jpg",
    grid_size=(50, 70),  # 또는 None으로 자동 계산
    output_dpi=300
)

generator.analyze_modules()
generator.prepare_target_image()
generator.generate("output.png", invert=False)
```

## 💡 팁

1. **첫 테스트**: 그리드 크기를 작게 (20x30 정도)로 빠르게 테스트
2. **명암 확인**: 타겟 이미지의 대비를 먼저 조정하면 결과가 더 좋음
3. **모듈 밝기**: 스크립트 실행 시 각 모듈의 밝기 값을 확인할 수 있음
4. **반전 옵션**: 결과가 반대로 나오면 `-i` 옵션 사용

## 📐 인쇄 크기 계산

출력 시 자동으로 인쇄 크기가 표시됩니다:

```
✅ 완료! 저장됨: output.png
   이미지 크기: 5000 x 7000 픽셀
   DPI: 300
   파일 크기: 15.32 MB
   인쇄 크기: 423.3 x 592.7 mm (300dpi 기준)
```

## ⚠️ 주의사항

- 모든 모듈 이미지는 **같은 크기**여야 합니다
- 모듈이 클수록 최종 파일 크기가 커집니다
- 그리드가 클수록 처리 시간이 오래 걸립니다

## 🐛 문제 해결

**Q: 모듈을 찾을 수 없다고 나와요**
- modules 폴더 경로와 이미지 파일 확인
- PNG, JPG 확장자 확인

**Q: 결과가 너무 밝거나 어두워요**
- `--invert` 옵션 시도
- 타겟 이미지의 대비 조정
- 모듈의 명암 범위 확인

**Q: 형상이 잘 안 보여요**
- 그리드 크기를 크게 (더 많은 셀)
- 타겟 이미지의 대비를 높게
- 모듈의 명암 차이를 크게

**Q: 파일이 너무 커요**
- 모듈 크기를 작게 (50x50px 정도)
- DPI를 낮게 (150-200)
- 그리드 크기를 작게
