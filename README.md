# voice-recognition
고급웹프로그래밍 수업 과제

# Whisper 기반 실시간 음성 인식 웹 애플리케이션

이 프로젝트는 OpenAI의 Whisper 음성 인식 모델을 활용하여 사용자의 음성을 실시간으로 텍스트로 변환하는 웹 애플리케이션입니다. Google Colab에서 실행되며, ngrok을 통해 외부 접속을 지원합니다.

## 📦 주요 기술 스택

- **프론트엔드**: React (CDN 방식 JSX, Babel)
- **백엔드**: Flask + flask-sock (WebSocket)
- **음성 인식**: OpenAI Whisper (base 모델)
- **환경**: Google Colab + ngrok
- **오디오 처리**: WebSocket을 통한 실시간 전송

## 🧱 시스템 아키텍처

```
브라우저 (React)
 ↕ WebSocket
Flask 서버 (Colab)
 ↕ Whisper 모델
ngrok Public URL
```

## 🔧 실행 방법

### 1. Colab에서 환경 구성
```bash
!pip install flask flask-cors flask-sock openai-whisper pyngrok soundfile
!ngrok authtoken <YOUR_NGROK_TOKEN>
!mkdir -p ./www/static/js ./www/static/css ./www/templates
```

### 2. Flask 서버 (app.py) 작성
- WebSocket 경로 `/audio`를 통해 오디오 수신
- Whisper 모델로 텍스트 인식 후 클라이언트에 전송

### 3. React 프론트엔드 (app.js)
- 마이크 녹음 → WebSocket 전송 → 텍스트 수신
- `window.location`을 기반으로 WebSocket URL 자동 구성

### 4. ngrok 서버 실행
```bash
!python run_server.py
```

### 5. 접속
- 출력된 ngrok URL로 접속하여 녹음 후 실시간 변환 테스트
- 예: `https://abcd1234.ngrok.io`

## ⚙️ 핵심 기능

- WebSocket을 통해 브라우저에서 실시간 오디오 스트리밍
- Whisper 모델로 .wav 오디오를 텍스트로 변환
- React UI에서 인식된 문장을 채팅 형태로 표시

## 🧠 학습 및 적용한 기술

- Whisper 모델 로딩 및 `transcribe()` 사용
- Flask-Sock 기반 WebSocket 구현 방식
- React의 useState/useRef/useEffect 사용법
- WebSocket URL 자동화 (window.location 활용)

## ❗ 문제 해결 경험

- `pyngrok` 모듈 미설치 → `pip install pyngrok`
- ERR_NGROK_8012 → Flask 서버 미실행 상태에서 ngrok 실행
- WebSocket 연결 실패 → 수동 입력 대신 자동 URL 생성 코드 도입

## 🚀 향후 개선 사항

- Whisper large 모델로 전환
- DB 연동 (검색 기록 저장)
- 결과 confidence 표시 및 텍스트 자동 다운로드
- 음성 실시간 스트리밍 분할 인식

## 📂 프로젝트 구조

```
project/
├── app.py              # Flask 서버
├── run_server.py       # ngrok 실행 스크립트
└── www/
    ├── templates/
    │   └── index.html
    ├── static/
    │   ├── js/app.js
    │   └── css/styles.css
```
