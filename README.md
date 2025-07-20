# 🚛 Intelligence Cargo System (ICS)

AI 기반 트렁크 모니터링 시스템  
Raspberry Pi + DINOv2 기반 추론을 통해 적재물의 **이동/추락 이벤트**를 감지하고,  
중앙 서버로 전송하여 Web UI에서 실시간으로 시각화합니다.

---

## 📦 프로젝트 구조

```
Intelligence-Cargo-System/
├── backend/               # FastAPI 기반 API 서버
├── frontend/              # React 기반 CMS/시각화 대시보드
├── edge/                  # Raspberry Pi (AI 추론, 센서 이벤트)
├── .github/workflows/     # GitHub Actions CI/CD
├── docker-compose.local.yml     # 전체 로컬 테스트용
├── docker-compose.dev.yml       # 개발 환경용 (Pi 분리)
├── deploy_edge.sh         # 라즈베리파이 배포 스크립트
└── .env                   # 공통 환경변수 파일
```

---

## ⚙️ 환경별 세팅 가이드

### 🧪 1. 로컬 환경 (전체 컴포넌트 실행)

> **모든 컴포넌트 (백엔드, 프론트엔드, edge) 를 현재 PC에서 실행하여 통합 테스트할 수 있습니다.**

#### ✅ 준비물
- Docker / Docker Compose
- Python 3.10+
- Node.js 18+
- `.env` 파일 생성

#### ✅ 실행 방법

```bash
docker-compose -f docker-compose.local.yml up --build
```

- 🔗 `http://localhost:8000` → FastAPI
- 🔗 `http://localhost:3000` → React UI
- 🤖 `edge/run.py` → 로컬 AI/센서 이벤트 시뮬레이션 가능

---

### 🧪 2. 개발 환경 (Raspberry Pi 실기기 포함)

> 실제 Pi 장비에서 Edge 추론 실행, 나머지는 로컬 또는 EC2에서 실행

#### ✅ 백엔드/프론트 도커 실행

```bash
docker-compose -f docker-compose.dev.yml up --build
```

#### ✅ 라즈베리파이 구성

```bash
# Pi에 Docker 설치 후 SSH로 배포
ssh pi@<RPI_IP> 'bash -s' < ./deploy_edge.sh
```

또는 직접 실행:

```bash
cd ~/trunkai/edge
git pull origin main
source venv/bin/activate
python3 run.py
```


