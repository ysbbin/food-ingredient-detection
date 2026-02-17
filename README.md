# Food Ingredient Detection

YOLO 기반 식재료 객체 탐지 프로젝트입니다. YOLOv5와 YOLOv8 모델을 비교 실험하여 최적의 식재료 탐지 모델을 선정합니다.

## 프로젝트 개요

- **목표**: 이미지에서 한국 식재료를 자동으로 탐지하고 분류
- **모델**: YOLOv5m, YOLOv5s, YOLOv8m, YOLOv8s 비교 실험
- **데이터셋**: 31종 한국 식재료 (Roboflow)
- **최종 모델**: YOLOv8m (100 epoch)

## 데이터셋

### 주요 데이터셋 (food_data_3) - 31 클래스

| 카테고리 | 클래스 |
|---------|--------|
| 곡류/면류 | 밥(bab), 빵(bread) |
| 채소류 | 배추(baechu), 양배추(cabbage), 당근(carrot), 오이(cucumber), 가지(eggplant), 마늘(garlic), 마늘쪽(garlic_clove), 생강(ginger), 대파(leek), 양파(onion), 파프리카(paprika), 깻잎(perilla), 감자(potato), 무(radish), 호박(squash), 고구마(sweet_potato) |
| 육류 | 소고기(beef), 닭고기(chicken), 돼지고기(pork) |
| 해산물 | 고등어(mackerel), 손질고등어(cut_mackerel), 새우(shrimp), 깐새우(peeled_shrimp), 오징어(squid) |
| 가공식품 | 두부(dubu), 어묵(fishcake), 김치(kimchi) |
| 기타 | 숙주(bean_sprouts), 계란(eggs) |

### 학습 데이터 통계

- **총 바운딩 박스 수**: 31,329개
- **클래스당 이미지 수**: 129~618장
- **클래스당 바운딩 박스 수**: 216~1,887개

## 실험 결과

### 모델 비교 (30 epoch)

| 모델 | Precision | Recall | mAP50 | mAP50-95 |
|------|-----------|--------|-------|----------|
| **YOLOv5m** | 84.34% | 80.57% | 86.21% | 64.04% |
| YOLOv5s | 81.83% | 78.47% | 83.87% | 60.24% |
| **YOLOv8m** | 84.90% | 78.46% | 85.63% | **64.91%** |
| YOLOv8s | 82.45% | 76.71% | 83.58% | 61.30% |

### 최종 모델 성능 (YOLOv8m, 100 epoch)

| 지표 | 값 |
|------|-----|
| **Precision** | 93.75% |
| **Recall** | 79.21% |
| **mAP50** | 85.95% |
| **mAP50-95** | 63.46% |

### 학습 설정

| 항목 | 값 |
|------|-----|
| Pretrained | YOLOv8m (COCO) |
| Epochs | 100 |
| Batch Size | 16 |
| Image Size | 640 |
| Optimizer | SGD (auto) |
| Learning Rate | 0.01 |
| Momentum | 0.937 |
| Augmentation | Mosaic, RandAugment, HSV, Flip |

## 프로젝트 구조

```
food-ingredient-detection/
├── data/                          # 데이터셋 설정
│   ├── food_data_1_config.yaml    # 47클래스 (채소/과일 통합)
│   ├── food_data_3_config.yaml    # 31클래스 (한국 식재료)
│   └── train_class_stats.csv      # 클래스별 학습 데이터 통계
├── notebooks/                     # 실험 노트북
│   ├── yolov5m최종학습.ipynb       # YOLOv5m 최종 학습
│   ├── yolov8m최종학습.ipynb       # YOLOv8m 최종 학습
│   ├── 최적모델선정(08.16).ipynb   # 최적 모델 선정 분석
│   ├── 최적의 모델 탐색.ipynb      # 모델 간 성능 비교
│   ├── v5m,v8m 100epoch그래프뽑기.ipynb  # v5m vs v8m 학습 곡선 비교
│   ├── yolov5m_data_3_hypertunning.ipynb # 하이퍼파라미터 튜닝
│   ├── yolov5m_data3_tunning.ipynb       # 추가 튜닝 실험
│   ├── yolo_v5m.ipynb             # YOLOv5m 초기 학습
│   ├── yolo_v8.ipynb              # YOLOv8 초기 학습
│   └── food_data_2.ipynb          # 데이터 분석
├── results/                       # 실험 결과
│   ├── training_logs/             # 학습 로그 (CSV)
│   ├── yolov8m_final/             # YOLOv8m 최종 결과
│   ├── model_compare/             # 모델 비교 결과
│   │   ├── data1/                 # 데이터셋 1 기준
│   │   └── data2/                 # 데이터셋 2 기준
│   ├── hyperparameter_tuning/     # 하이퍼파라미터 탐색 결과
│   └── plots/                     # 비교 그래프
└── test_images/                   # 외부 테스트 이미지
    ├── external_test/             # 한국 식재료 테스트 이미지
    └── external_food_data/        # 채소/과일 테스트 이미지
```

## 사용 기술

- **Python**
- **YOLOv5** (Ultralytics)
- **YOLOv8** (Ultralytics)
- **PyTorch**
- **Roboflow** (데이터셋)
- **Jupyter Notebook**

## 데이터셋 출처

- [Food Ingredients Dataset](https://universe.roboflow.com/yolov5-rznzw/food-ingredients-7txer/dataset/5) - 31 클래스 한국 식재료 (CC BY 4.0)
- [Combined Vegetables & Fruits](https://universe.roboflow.com/yolo-jpkho/combined-vegetables-fruits/dataset/8) - 47 클래스 채소/과일 (CC BY 4.0)
