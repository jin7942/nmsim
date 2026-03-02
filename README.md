# NMSIM

NMS 개발용 SNMP 시뮬레이터

## 개요

NMSIM은 NMS(Network Management System) 개발 시 실제 네트워크 장비 없이 SNMP 연동을 테스트할 수 있는 시뮬레이터입니다.

## 주요 기능

- **SNMP 프로토콜 지원**: SNMPv1, v2c, v3
- **표준 MIB 지원**: RFC1213-MIB, IF-MIB, ENTITY-MIB, HOST-RESOURCES-MIB 등
- **벤더 MIB 지원**: Evertz (570FC, 570ACO, 570DSK)
- **웹 기반 관리 UI**: 장비 추가/삭제, OID 편집, 테스트 콘솔
- **다중 IP 지원**: 장비별 고유 IP 자동 할당
- **동적 값 엔진**: 카운터 증가, 범위 내 변동, 패턴 반복
- **응답 제어**: 지연, 타임아웃, 에러 시뮬레이션

## 빠른 시작

### VM 설치

1. VM 이미지 다운로드 (OVA/QCOW2)
2. 하이퍼바이저에서 임포트
3. 브릿지 네트워크 설정
4. VM 부팅
5. 웹 UI 접속: `http://{VM_IP}:8080`

### SNMP 테스트

```bash
# 장비 추가 후 NMS 서버에서 테스트
snmpget -v2c -c public 10.0.0.100 sysDescr.0
snmpwalk -v2c -c public 10.0.0.100 ifTable
```

## 기술 스택

| 영역 | 기술 |
|------|------|
| Backend | FastAPI, Python 3.11 |
| Frontend | React 18, shadcn/ui, Tailwind CSS |
| Database | SQLite |
| SNMP | asyncio, pysnmp |
| 배포 | VM (OVA/QCOW2) |

## 문서

자세한 내용은 [docs/](./docs) 디렉터리를 참조하세요.

- [프로젝트 소개](./docs/01-Overview/01-Introduction.md)
- [주요 기능](./docs/01-Overview/02-Features.md)
- [시스템 아키텍처](./docs/03-Design/01-Architecture/01-SystemArchitecture.md)
- [설치 가이드](./docs/05-Deployment/01-Installation.md)
- [빠른 시작](./docs/05-Deployment/02-QuickStart.md)

## 라이선스

MIT License
