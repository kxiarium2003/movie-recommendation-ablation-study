# Movie Recommendation Ablation Study

> 2025-2 빅데이터알고리즘 팀 프로젝트  
> MovieLens 기반 Item-based Collaborative Filtering 추천 시스템 성능 개선 및 Ablation Study

최종 발표 과정에서 핀다(Finda) 소속 박사님의 피드백 및 평가를 받았습니다.

---

## 프로젝트 개요

본 프로젝트는 MovieLens 데이터셋 기반의 추천 시스템 성능 개선 프로젝트입니다.

단순 추천 시스템 구현에 그치지 않고,
다양한 전처리 및 similarity 계산 전략이 추천 품질에 어떤 영향을 미치는지 분석하기 위해 Ablation Study 형태로 실험을 진행했습니다.

또한 RMSE 비교뿐 아니라 실제 추천 결과 품질을 확인하기 위해 persona user 기반 평가를 함께 수행했습니다.

---

## 주요 목표

* Item-based Collaborative Filtering 성능 개선
* 사용자 rating bias 완화
* Similarity 계산 최적화
* Cold-start 문제 대응
* Metadata 기반 추천 성능 향상
* Ablation Study 기반 실험 분석

---

## 사용 데이터셋

### MovieLens Dataset

추천 시스템의 기본 rating 데이터로 MovieLens 데이터셋을 사용했습니다.

사용 파일:

* ratings.csv
* movies.csv
* tags.csv
* links.csv

추가적으로:

* TMDB metadata
* IMDB linkage data

를 활용한 metadata 실험도 수행했습니다.

---

## 주요 실험 내용

### 1. Z-score Normalization

사용자별 rating 편향을 줄이기 위해 Z-score normalization을 적용했습니다.

* 사용자 평균 및 표준편차 기반 정규화
* 사용자별 rating scale 차이 완화

---

### 2. Persona User Evaluation

단순 metric 기반 평가뿐 아니라 실제 추천 품질을 확인하기 위해 persona user 기반 inference를 수행했습니다.

#### Persona Users

Heavy User: 다양한 장르를 폭넓게 소비하는 사용자

Specialist User: 특정 장르를 집중적으로 소비하는 사용자

---

### 3. Positive Similarity without KNN

기존 Item-based CF에서 자주 사용하는 KNN 기반 filtering 대신,
양수 유사도를 가진 모든 item similarity를 활용하는 방식을 실험했습니다.

이를 통해:

* 정보 손실 감소
* 미세한 성능 향상
* 계산 효율 유지

를 확인했습니다.

---

### 4. Significance Weighting

공통 평가 수가 적은 item similarity의 신뢰도를 보정하기 위해 Significance Weighting을 적용했습니다.

또한 threshold 및 weighting 값 변화에 따른 성능 차이를 비교했습니다.

---

### 5. Metadata Vectorization

MovieLens 외부 metadata를 활용하기 위해 다음과 같은 실험을 진행했습니다.

* Genre vectorization
* Tag vectorization
* TMDB metadata 활용
* IMDB linkage 활용

---

### 6. Cold-start Fallback Strategy

훈련 범위를 벗어난 사용자 및 영화 데이터 처리 시 fallback 전략을 적용했습니다.

#### User Cold-start

* Global Mean 사용

#### Item Cold-start / Prediction Failure

* User Mean 사용

---

## 실험 흐름

| Experiment | Description                      |
| ---------- | -------------------------------- |
| exp01      | Z-score baseline                 |
| exp02      | Persona user evaluation          |
| exp03      | Remove KNN / positive similarity |
| exp04      | Genre vectorization              |
| exp05      | Apply significance weighting     |
| exp06      | Tag vectorization                |
| exp07      | Rating + tag + genre combination |
| exp08      | Significance weighting tuning    |
| exp09      | TMDB metadata experiment         |
| exp10      | TMDB + significance weighting    |
| exp11      | IMDB integration                 |
| exp12      | Duplicate / homonym checking     |
| exp13      | Final recommendation model       |

---

## 디렉토리 구조

```text
movie-recommendation-ablation-study/
│
├── data/
│   ├── ratings.csv
│   ├── movies.csv
│   ├── tags.csv
│   ├── links.csv
│   └── tmdb_metadata.csv
│
├── EDA/
│   ├── eda01.ipynb
│   ├── eda02.ipynb
│   └── eda03.ipynb
│
├── experiments/
│   ├── exp01_zscore_baseline.ipynb
│   ├── ...
│   └── exp13_final_model.ipynb
│
└── README.md
```

---

## 최종 결과

최종 모델은:

* RMSE 약 0.84 수준 달성
* 빠른 예측 속도 유지
* Normalization 및 fallback 전략을 통한 추천 안정성 향상

을 확인했습니다.

---

## 기술 스택

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Jupyter Notebook

---

## 참고

본 레포지토리는 학부 전공 팀 프로젝트의 실험 과정을 정리 및 기록하기 위해 작성되었습니다.