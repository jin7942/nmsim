# 주요 기능

## 1. SNMP 프로토콜 지원

### 지원 버전
- SNMPv1
- SNMPv2c
- SNMPv3 (인증/암호화)

### 지원 명령
- GetRequest
- GetNextRequest
- GetBulkRequest
- SetRequest

## 2. 표준 MIB 지원

```
├── RFC1213-MIB (MIB-II)
│   ├── system      (1.3.6.1.2.1.1)
│   ├── interfaces  (1.3.6.1.2.1.2)
│   ├── at          (1.3.6.1.2.1.3)
│   ├── ip          (1.3.6.1.2.1.4)
│   ├── icmp        (1.3.6.1.2.1.5)
│   ├── tcp         (1.3.6.1.2.1.6)
│   ├── udp         (1.3.6.1.2.1.7)
│   └── snmp        (1.3.6.1.2.1.11)
│
├── IF-MIB (1.3.6.1.2.1.31)
├── ENTITY-MIB (1.3.6.1.2.1.47)
├── HOST-RESOURCES-MIB (1.3.6.1.2.1.25)
├── LLDP-MIB (1.0.8802.1.1.2)
├── BRIDGE-MIB (1.3.6.1.2.1.17)
└── Q-BRIDGE-MIB (VLAN)
```

## 3. 벤더 Private MIB 지원

- Evertz (570FC, 570ACO, 570DSK)
- Cisco (확장 예정)
- Juniper (확장 예정)

## 4. 웹 기반 관리 UI

- 장비 추가/삭제/수정
- OID 값 실시간 편집
- SNMP 테스트 콘솔
- 요청 로그 조회

## 5. 동적 값 엔진

| 규칙 유형 | 설명 | 예시 |
|----------|------|------|
| counter | 카운터 증가 | ifInOctets |
| gauge | 범위 내 변동 | CPU 사용률 |
| uptime | 시간 증가 | sysUpTime |
| pattern | 패턴 반복 | 트래픽 시뮬레이션 |

## 6. 응답 제어

- 응답 지연 시뮬레이션
- 타임아웃 시뮬레이션
- 에러 응답 (noSuchObject, genErr 등)
- 간헐적 장애 (확률 기반)

## 7. 다중 IP 지원

- 장비별 고유 IP 할당
- 자동 IP 관리 (할당/해제)
- NMS에서 실제 장비처럼 접근
