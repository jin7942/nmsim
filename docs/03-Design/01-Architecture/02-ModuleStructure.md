# 모듈 구조

## 디렉터리 구조

```
nmsim/
├── src/
│   ├── main.py                    # FastAPI 앱 엔트리포인트
│   ├── config.py                  # 환경 설정
│   │
│   ├── core/
│   │   ├── device_manager.py      # 장비 CRUD
│   │   ├── mib_manager.py         # MIB 정의 관리
│   │   ├── network_manager.py     # IP 할당/해제
│   │   └── value_engine.py        # 동적 값 계산 엔진
│   │
│   ├── snmp/
│   │   ├── agent.py               # SNMP 에이전트
│   │   ├── protocol.py            # SNMP 프로토콜 처리
│   │   ├── v3_security.py         # SNMPv3 보안
│   │   └── data_store.py          # OID-값 저장소
│   │
│   ├── mib/
│   │   ├── standard/              # 표준 MIB 구현
│   │   │   ├── system.py
│   │   │   ├── interfaces.py
│   │   │   ├── ip.py
│   │   │   └── ...
│   │   ├── vendor/                # 벤더 MIB
│   │   │   └── evertz/
│   │   └── loader.py              # MIB 파일 로더
│   │
│   ├── api/
│   │   ├── devices.py             # 장비 관리 API
│   │   ├── oids.py                # OID 편집 API
│   │   ├── test.py                # SNMP 테스트 API
│   │   └── logs.py                # 요청 로그 API
│   │
│   ├── web/
│   │   └── static/                # React 빌드 결과물
│   │
│   └── db/
│       ├── models.py              # SQLAlchemy 모델
│       └── repository.py          # 데이터 접근 계층
│
├── frontend/                      # React 소스
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── hooks/
│   │   └── api/
│   └── package.json
│
├── data/
│   └── nmsim.db                   # SQLite 데이터베이스
│
├── scripts/
│   ├── install.sh                 # 설치 스크립트
│   └── build-vm.sh                # VM 이미지 빌드
│
└── docs/                          # 문서
```

## 모듈별 책임

| 모듈 | 책임 |
|------|------|
| `core/device_manager` | 장비 CRUD, 활성화/비활성화 |
| `core/network_manager` | IP 할당/해제 (`ip addr add/del`) |
| `core/mib_manager` | MIB 정의 로드, OID 검증 |
| `core/value_engine` | 동적 값 계산 (카운터, 게이지 등) |
| `snmp/agent` | SNMP 요청 수신/응답 |
| `snmp/protocol` | SNMP 패킷 파싱/생성 |
| `snmp/data_store` | 장비별 OID-값 저장 |
| `api/*` | REST API 엔드포인트 |
| `db/*` | 데이터베이스 접근 |
