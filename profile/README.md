# 🐱 피쓰냥 (Peace Cat) - AI 기반 피싱 URL 탐지 서버

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.109-009688?logo=fastapi&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/AI-Scikit__Learn-orange?logo=scikit-learn&logoColor=white)

> **2026 사이버 보안 AI 아이디어 경진대회 출품작 (Backend Server)** > 실시간 화이트리스트/블랙리스트 필터링과 Random Forest AI 모델을 결합한 하이브리드 피싱 탐지 솔루션입니다.

---

## 📌 프로젝트 소개

**피쓰냥(Peace Cat)**은 사용자가 접속하려는 웹 사이트의 URL을 실시간으로 분석하여 피싱(Phishing) 및 스캠 위험도를 판별합니다.
기존의 단순 DB 조회 방식을 넘어, **AI(인공지능)를 활용해 신종 피싱 사이트의 패턴(URL 길이, 특수문자, 도메인 생성일 등)까지 탐지**합니다.

### 🌟 핵심 기능

1.  **3단계 하이브리드 필터링:**
    - **1단계 (Whitelist):** 주요 포털 및 금융기관 등 신뢰 사이트 즉시 통과 (O(1) 속도)
    - **2단계 (Blacklist):** OpenPhish 등 기신고된 피싱 사이트 즉시 차단
    - **3단계 (AI Inference):** 미탐지 URL은 Random Forest 모델이 정밀 분석
2.  **도메인 나이 분석 (Whois):** 생성된 지 14일 미만인 '갓 태어난' 위험 도메인 식별
3.  **자동 데이터 갱신:** 매일 새벽 4시, 최신 피싱/정상 도메인 데이터를 자동 수집 및 서버 갱신
4.  **대용량 트래픽 대응:** In-Memory Set 구조와 SQLite 캐싱을 통한 고성능 처리

---

## 🛠 기술 스택 (Tech Stack)

- **Language:** Python 3.12.10
- **Framework:** FastAPI (Asynchronous Server)
- **AI Model:** Scikit-learn (Random Forest Classifier)
- **Data Management:** \* In-Memory Set (Whitelist/Blacklist)
  - SQLite (Whois Cache)
- **Scheduler:** APScheduler (Background Tasks)
- **Parsing:** `tldextract`, `python-whois`

---

## 📂 디렉토리 구조

```bash
PeaceCat_Server/
├── app/
│   ├── api.py              # API 엔드포인트 (POST /analyze)
│   ├── logger.py           # 프라이버시 보호 로깅 (파라미터 절삭)
│   └── scheduler.py        # 데이터 자동 갱신 스케줄러 (ETL)
├── core/
│   ├── ai_model.py         # AI 모델 로드 및 추론 로직
│   ├── feature_extractor.py # URL 특징 추출 (길이, 특수문자, 도메인 등)
│   ├── data_loader.py      # CSV 데이터 메모리 적재
│   └── whois_handler.py    # Whois 조회 및 SQLite 캐싱
├── data/                   # 데이터 저장소 (Git Ignore 처리됨)
├── train/                  # AI 모델 학습 스크립트
├── main.py                 # 서버 진입점 (Entry Point)
├── config.py               # 환경 설정
└── requirements.txt        # 의존성 패키지 목록
```

---

## 환경설정

# 레포지토리 클론

git clone [https://github.com/YOUR_GITHUB_ID/PeaceCat_Server.git](https://github.com/YOUR_GITHUB_ID/PeaceCat_Server.git)
cd PeaceCat_Server

# 가상환경 생성 및 실행 (Mac/Linux)

python3.12 -m venv venv
source venv/bin/activate

# 의존성 패키지 설치

pip install -r requirements.txt

# 학습 데이터가 train/raw_dataset.csv 에 위치해야 합니다.

python train/train_driver.py

# 실행은 비동기로

uvicorn main:app --reload
