<div align="left">

<img src="https://raw.githubusercontent.com/26-phishing-scam/.github/main/profile/assets/peace-logo.png" width="180"/>

<br>
</div>

<h1>🐱 피스냥 | PEACE-NYANG</h1>

<h3>브라우저 행동 분석 + AI 기반 피싱 URL 탐지</h3>

<p>
사용자의 브라우저 행동 이벤트를 수집하고 분석하여<br>
피싱·스캠 위험 상황을 탐지하고 경고하는 서비스입니다.
</p>

<br/>

<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
<img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white"/>
<img src="https://img.shields.io/badge/Chrome_Extension-4285F4?style=for-the-badge&logo=googlechrome&logoColor=white"/>
<img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black"/>
<img src="https://img.shields.io/badge/Security-222222?style=for-the-badge&logo=hackthebox&logoColor=white"/>

</div>

---

## 🎥 Demo Video

<div align="center">

<a href="https://www.youtube.com/watch?v=VPThtO3gyV8">
  <img src="https://img.youtube.com/vi/VPThtO3gyV8/maxresdefault.jpg" width="800"/>
</a>

<br/>

<b>▲ 클릭하여 시연 영상 보기</b>

</div>

---

## 📄 Presentation

<div align="center">

<a href="https://github.com/26-phishing-scam/.github/blob/main/profile/docs/피스냥_발표자료.pdf">
  <img src="https://img.shields.io/badge/Presentation-PDF-red?style=for-the-badge&logo=adobeacrobatreader&logoColor=white"/>
</a>

</div>

---

## 📌 About Project

**피스냥(PEACE-NYANG)** 은 사용자의 웹 브라우저 행동을 분석하여 피싱·스캠 위험 상황을 탐지하는 보안 서비스입니다.

Chrome Extension에서 수집한 URL, 개인정보 입력, 결제, 다운로드, 로그인, 클립보드, 리다이렉트, 폼 제출 이벤트를 FastAPI 서버로 전송하고, 서버는 이벤트 유형과 메타데이터를 기반으로 위험 사유를 분석합니다.

---

## ✨ Key Features

<table>
<tr>
<td width="50%">

### 🔍 URL 및 행동 이벤트 분석

- 접속 URL 수집
- 이벤트 유형 분류
- 이벤트별 메타데이터 분석
- 위험 사유 반환

</td>
<td width="50%">

### 🛡 개인정보 입력 감지

- 이메일 입력 감지
- 전화번호 입력 감지
- 주소 입력 감지
- 주민등록번호 패턴 감지

</td>
</tr>

<tr>
<td width="50%">

### 📥 다운로드 위험 감지

- 다운로드 파일명 분석
- 파일 확장자 확인
- 실행 파일 계열 탐지
- 신규 도메인 다운로드 감지

</td>
<td width="50%">

### 💳 결제 및 폼 제출 감지

- 결제 정보 입력 감지
- 카드 정보 입력 감지
- 폼 제출 도메인 불일치 탐지
- 파일 업로드 감지

</td>
</tr>

<tr>
<td width="50%">

### 🔐 로그인 / 비밀번호 입력 감지

- 로그인 이벤트 감지
- 비밀번호 입력 감지
- Form Action 도메인 검사
- 페이지 도메인과 전송 도메인 비교

</td>
<td width="50%">

### 📊 이벤트 요약 제공

- 이벤트 타입별 카운트
- 위험 사유별 카운트
- 최근 이벤트 목록 조회
- 요약 정보 API 제공

</td>
</tr>
</table>

---

## 🏗️ System Architecture

```text
┌──────────────────────────┐
│     Chrome Extension      │
│  - URL 감지               │
│  - 입력 이벤트 감지        │
│  - 다운로드 이벤트 감지     │
│  - 결제 / 로그인 감지       │
└─────────────┬────────────┘
              │ REST API
              ▼
┌──────────────────────────┐
│       FastAPI Server      │
│  - 이벤트 수신             │
│  - 이벤트 검증             │
│  - 위험 사유 분석          │
│  - 요약 데이터 제공        │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│    In-Memory Storage      │
│  - 최근 이벤트 저장        │
│  - 최근 도메인 저장        │
│  - 요약 정보 생성          │
└──────────────────────────┘
```

---

## 🔄 Service Flow

```text
사용자가 웹사이트 접속
        │
        ▼
Chrome Extension이 행동 이벤트 수집
        │
        ▼
FastAPI 서버로 이벤트 전송
        │
        ▼
서버에서 이벤트 타입 및 메타데이터 검증
        │
        ▼
위험 사유 분석
        │
        ▼
분석 결과 및 요약 정보 반환
```

---

## 🧠 Detection Logic

피스냥 백엔드는 이벤트 유형별 메타데이터를 확인하여 위험 사유를 생성합니다.

| Event Type | Detection Point |
|---|---|
| `pii_input` | 개인정보 필드, 이메일, 전화번호, 주소, 주민등록번호 여부 |
| `payment` | 결제 금액, 카드 입력, 카드 BIN, 결제 도메인 |
| `download` | 파일명, 확장자, 위험 확장자, 신규 도메인 다운로드 |
| `login` | 사용자명 입력 여부, Form Action 도메인 불일치 |
| `password_input` | 비밀번호 입력 여부, 전송 도메인 불일치 |
| `clipboard` | 클립보드 쓰기, 암호화폐 주소 포함 여부 |
| `redirect` | 리다이렉트 체인 길이, 최종 도메인 |
| `form_submit` | 파일 업로드, 결제 필드, 전송 도메인 불일치 |

---

## 🛠️ Tech Stack

<table>
<tr>
<td align="center" width="33%">
<b>Frontend</b>
<br><br>
<img src="https://skillicons.dev/icons?i=html,css,javascript" />
<br>
Chrome Extension
</td>

<td align="center" width="33%">
<b>Backend</b>
<br><br>
<img src="https://skillicons.dev/icons?i=python,fastapi" />
<br>
FastAPI REST API
</td>

<td align="center" width="25%">
<b>AI Server</b>
<br><br>

<img src="https://camo.githubusercontent.com/e86689bd81b55698b150eccfcf6efc6f52cf07b7ea91560ec4177a30ca7ee3f6/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f41492d5363696b69745f5f4c6561726e2d6f72616e67653f6c6f676f3d7363696b69742d6c6561726e266c6f676f436f6c6f723d7768697465"/>

<br>

Random Forest
</td>

<td align="center" width="40%">
<b>Data</b>
<br><br>
<img src="https://img.shields.io/badge/Whois-Analysis-blue?style=for-the-badge"/>
<br>
Whitelist/Blacklist
</td>

---

## 📂 Repositories

<table>
<tr>
<th>Repository</th>
<th>Description</th>
<th>Link</th>
</tr>

<tr>
<td><b>Backend</b></td>
<td>FastAPI 기반 이벤트 분석 및 저장 API 서버</td>
<td><a href="https://github.com/26-phishing-scam/Backend">Repository</a></td>
</tr>

<tr>
<td><b>Server</b></td>
<td>피스냥 AI 서버</td>
<td><a href="https://github.com/26-phishing-scam/PeaceCat_Server">Server</a></td>
</tr>
</table>

---

## 🔗 API Overview

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/health` | 서버 상태 확인 |
| `GET` | `/schema` | 이벤트 타입 및 요청 예시 확인 |
| `POST` | `/analyze/event` | 단일 이벤트 위험 사유 분석 |
| `POST` | `/analyze/batch` | 여러 이벤트 일괄 분석 및 요약 |
| `POST` | `/events` | 이벤트 저장 |
| `GET` | `/events` | 저장된 이벤트 목록 조회 |
| `POST` | `/domains` | 도메인 저장 |
| `GET` | `/domains` | 저장된 도메인 목록 조회 |
| `GET` | `/summary` | 최근 이벤트 요약 조회 |

---

## 👥 Team

<table>
<tr>
<td align="center" width="33%">
<img src="https://github.com/hoo-ing.png" width="120"/>
<br/>
<h3>이호성</h3>
<b>PM / Backend</b>
<br/><br/>
<a href="https://github.com/hoo-ing">
<img src="https://img.shields.io/badge/GitHub-hoo--ing-181717?style=flat-square&logo=github&logoColor=white"/>
</a>
</td>

<td align="center" width="33%">
<img src="https://github.com/hae-mil.png" width="120"/>
<br/>
<h3>박성민</h3>
<b>Frontend</b>
<br/><br/>
<a href="https://github.com/hae-mil">
<img src="https://img.shields.io/badge/GitHub-hae--mil-181717?style=flat-square&logo=github&logoColor=white"/>
</a>
</td>

<td align="center" width="33%">
<img src="https://github.com/sanghyuk.png" width="120"/>
<br/>
<h3>표상혁</h3>
<b>Detection Logic / AI</b>
<br/><br/>
<a href="https://github.com/sanghyuk">
<img src="https://img.shields.io/badge/GitHub-sanghyuk-181717?style=flat-square&logo=github&logoColor=white"/>
</a>
</td>
</tr>
</table>

---

## 📋 Roles & Contributions

<table>
<tr>
<th>Member</th>
<th>Role</th>
<th>Contributions</th>
</tr>

<tr>
<td><b>이호성</b></td>
<td>PM / Backend</td>
<td>
프로젝트 기획 및 총괄<br/>
FastAPI 서버 개발<br/>
API 라우터 구성<br/>
이벤트 저장 API 구현<br/>
분석 결과 요약 API 구현
</td>
</tr>

<tr>
<td><b>박성민</b></td>
<td>Frontend</td>
<td>
Chrome Extension 개발<br/>
사용자 행동 이벤트 수집<br/>
UI / UX 구현<br/>
대시보드 화면 구성
</td>
</tr>

<tr>
<td><b>표상혁</b></td>
<td>AI</td>
<td>
Random Forest 기반 피싱 URL 탐지 모델 학습<br/>
URL 특징 추출<br/>
3단계 하이브리드 탐지 구조 설<br/>
Whois 도메인 생성 분석<br/>
피싱 URL 데이터 자동 갱신
</td>
</tr>
</table>

---

## 🚀 Expected Effects

- 피싱·스캠 피해 사전 예방
- 개인정보 입력 및 위험 다운로드 상황 조기 탐지
- 사용자 보안 인식 향상
- 브라우저 기반 보안 경고 자동화
- 행동 이벤트 기반 보안 서비스 확장 가능성 확보

---

## 🔮 Future Work

- 실제 DB 연동
- 사용자별 이벤트 이력 관리
- 악성 URL 데이터셋 기반 모델 고도화
- 이메일 피싱 탐지 연동
- 메신저 링크 분석 기능 확장
- 기업용 보안 대시보드 확장

---

<div align="center">

<br/>

## 🐱 PEACE-NYANG

<b>피싱과 스캠으로부터 사용자를 지키는 브라우저 행동 기반 보안 서비스</b>

<br/>

<img src="https://capsule-render.vercel.app/api?type=waving&height=180&section=footer&color=0:FF7A00,100:F9A826"/>

</div>
