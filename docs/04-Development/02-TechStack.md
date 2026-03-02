# 기술 스택

## Backend

| 영역 | 기술 | 버전 | 용도 |
|------|------|------|------|
| Framework | FastAPI | 0.100+ | REST API |
| SNMP | asyncio + pysnmp | - | SNMP 에이전트 |
| ORM | SQLAlchemy | 2.0+ | 데이터베이스 접근 |
| Database | SQLite | 3 | 데이터 저장 |
| Validation | Pydantic | 2.0+ | 요청/응답 검증 |

## Frontend

| 영역 | 기술 | 버전 | 용도 |
|------|------|------|------|
| Framework | React | 18 | UI 라이브러리 |
| Build | Vite | 5+ | 빌드 도구 |
| UI Library | shadcn/ui | - | 컴포넌트 라이브러리 |
| CSS | Tailwind CSS | 3+ | 스타일링 |
| State | Zustand | 4+ | 상태 관리 |
| HTTP | Axios | - | API 통신 |

## Infrastructure

| 영역 | 기술 | 용도 |
|------|------|------|
| OS | Ubuntu 22.04 LTS | VM 기반 OS |
| 배포 | OVA / QCOW2 | VM 이미지 |
| 서비스 | systemd | 프로세스 관리 |

## 개발 도구

| 영역 | 기술 | 용도 |
|------|------|------|
| 언어 | Python 3.11+ | 백엔드 |
| 언어 | TypeScript | 프론트엔드 |
| 테스트 | pytest | 백엔드 테스트 |
| 테스트 | Vitest | 프론트엔드 테스트 |
| 린트 | Ruff | Python 린터 |
| 린트 | ESLint | TypeScript 린터 |
