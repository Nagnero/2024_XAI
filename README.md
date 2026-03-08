# 2024 XAI Stock Analysis Project

광운대학교 2024 KW-VIP 프로젝트 저장소.  
기술적 지표와 재무제표 데이터를 바탕으로 종목의 미래 수익률을 예측하고, LIME/SHAP 기반 설명가능한 인공지능(XAI) 시각화를 PyQt5 GUI로 제공하는 프로젝트.


## 개발 환경

- Language: Python
- GUI: PyQt5
- Visualization: `matplotlib`, `mplfinance`, `lightweight-charts`
- XAI: `lime`, `shap`
- Data Processing: `pandas`, `numpy`, `scikit-learn`

## 프로젝트 개요

이 프로젝트는 단순한 예측 모델 데모가 아니라, 종목 선택부터 날짜 선택, 예측 결과 시각화, 설명 결과 확인까지 하나의 데스크톱 GUI 안에서 처리하는 구조.

- 주가/재무 데이터 기반 수익률 예측
- 예측 결과를 선형 차트와 캔들 차트로 시각화
- LIME 기반 개별 예측 설명
- SHAP 기반 주요 피처 중요도 설명
- 선택된 피처 설명을 별도 위젯에서 텍스트로 제공

## 지원 종목

현재 GUI에서 선택 가능한 종목은 다음 4개.

- 삼성전자 (`005930`)
- 엔씨소프트 (`036570`)
- SK하이닉스 (`000660`)
- KB금융 (`105560`)

## 디렉터리 구조

| 경로 | 내용 |
| --- | --- |
| `data/` | 전처리 데이터, 라벨 데이터, 종목 코드 목록, 피처 설명 텍스트 |
| `design/` | GUI 아이콘 및 디자인 리소스 |
| `model/` | 종목별 학습 완료 모델 파일 (`*.pkl`) |
| `result/` | 예측 차트, LIME 결과, SHAP 결과 이미지 출력 폴더 |
| `stock_csv/` | 종목별 OHLCV CSV 데이터 |
| `stock_logo/` | 종목 로고 이미지 |
| `main.py` | 프로그램 진입점 |
| `mainWindow.py` | 메인 PyQt GUI 로직 |
| `stock_chart.py` | 예측 차트 및 캔들 차트 생성 |
| `lime_explanation.py` | LIME 설명 생성 및 시각화 |
| `SHAP_explanation.py` | SHAP 설명 생성 및 시각화 |
| `FinDataLoader.py` | 재무/가격 데이터 로딩 및 전처리 유틸리티 |
| `XAI_GUI.ui` | 메인 GUI 레이아웃 |
| `EXP_GUI.ui`, `INFO_GUI.ui` | 설명/정보 서브 윈도우 레이아웃 |

## 주요 기능

### GUI 기능

- 종목 선택 콤보박스 제공
- 기간 직접 선택 및 분기별 빠른 선택 제공
- 로그 위젯, 캘린더 위젯, 정보 위젯, 설명 위젯 분리
- 결과 위젯을 독립 창으로 띄우는 구조

### 시각화 기능

- 실제 종가와 예측 종가를 비교하는 예측 차트 생성
- `lightweight-charts` 기반 인터랙티브 캔들 차트 제공
- 이동평균선(SMA 20, SMA 50) 오버레이
- LIME 설명 이미지 생성
- SHAP bar chart 및 관련 보조 차트 생성

### 설명 기능

- LIME에서 최근 시그널 기준 최대 4개 시점을 설명
- SHAP에서 상위 중요 피처 5개 추출
- `data/feature_explain.csv`를 이용해 피처 의미를 텍스트로 표시
- 설명 결과를 별도 Explanation 위젯에서 확인

## 실행 방법

### 1. 가상환경 생성

```bash
python -m venv .venv
```

### 2. 패키지 설치

```bash
pip install pyqt5 pandas numpy matplotlib mplfinance scikit-learn lightweight-charts lime shap fancyimpute finance-datareader stockstats tqdm
```

### 3. 프로그램 실행

```bash
python main.py
```

실행 후 흐름:

1. 종목 선택
2. 기간 선택
3. `Confirm` 버튼으로 데이터 처리 및 설명 결과 생성
4. `Show` 버튼으로 차트/설명 위젯 출력

## 결과물

실행 과정에서 다음 결과 파일이 `result/` 폴더에 생성되거나 갱신.

- `StockChart.png`
- `lime_explanation.png`
- `SHAP_bar_result.png`
- `SHAP_char_result.png`

## 구현 포인트

- `main.py`에서 PyQt 애플리케이션 시작
- `mainWindow.py`에서 메인 이벤트 처리와 다중 위젯 제어 수행
- `stock_chart.py`에서 예측 종가 계산 후 차트 렌더링
- `lime_explanation.py`에서 시그널 기준 샘플 선택 후 LIME 설명 생성
- `SHAP_explanation.py`에서 SHAP 중요도 계산과 상위 피처 시각화 수행
- `FinDataLoader.py`에서 가격/재무 데이터 로딩, 라벨링, 전처리 지원

## 팀원 및 역할

| 이름 | GitHub | 역할 |
| --- | --- | --- |
| 김다솔 | [@dasolkim7](https://github.com/dasolkim7) | Explanation widget용 feature 설명 생성 |
| 김민재 | [@CanelE452](https://github.com/CanelE452) | SHAP 설명 생성, feature 조사 |
| 김태관 | [@KimTaegwan03](https://github.com/KimTaegwan03) | 기술적 지표 수집, 재무제표/기술지표 전처리, [모델 학습](https://github.com/KimTaegwan03/KW_VIP_Financial_Statements_Analysis.git) |
| 연선우 | [@Nagnero](https://github.com/Nagnero) | Predict chart 생성 |
| 우나륜 | [@M3rcy1028](https://github.com/M3rcy1028) | PyQt GUI 기능 개발 및 디자인 총괄, Candle chart 생성 |
| 이정현 | [@LEEJH1029](https://github.com/LEEJH1029) | LIME 설명 생성, 재무제표 데이터 제공 |

## 한계와 참고 사항

- 모델 학습 전체 코드가 이 저장소 안에 완전히 포함된 구조는 아님.
- 종목 수는 4개로 고정되어 있음.
- 날짜 범위는 보유한 CSV/라벨 데이터 범위에 따라 내부적으로 보정.
- `mainWindow.py`의 분기 선택 로직은 2024년 기준으로 고정.
- GUI 중심 프로젝트라 CLI 사용성이나 배포 패키징은 별도로 정리되어 있지 않음.
- 일부 라이브러리는 설치 환경에 따라 추가 설정이 필요할 수 있음.

