# 개발 로드맵

## 전체 일정

| Phase | 기간 | 목표 |
|-------|------|------|
| Phase 1 | 2주 | 표준 MIB 확장 |
| Phase 2 | 3주 | 웹 UI 구현 |
| Phase 3 | 2주 | 고급 기능 |
| Phase 4 | 1주 | 안정화 및 배포 |

---

## Phase 1: 표준 MIB 확장 (2주)

### Week 1
- [ ] RFC1213-MIB 전체 구현
  - [ ] ip 그룹 (ipAddrTable, ipRouteTable, ipNetToMediaTable)
  - [ ] tcp 그룹 (tcpConnTable)
  - [ ] udp 그룹 (udpTable)
  - [ ] snmp 그룹 (통계 카운터)
- [ ] SNMP 요청 로깅 기반 구현

### Week 2
- [ ] IF-MIB 확장 (ifXTable)
- [ ] ENTITY-MIB 기본 구현
- [ ] 단위 테스트 작성

---

## Phase 2: 웹 UI 구현 (3주)

### Week 3
- [ ] React 프로젝트 셋업
- [ ] shadcn/ui + Tailwind 설정
- [ ] 레이아웃 컴포넌트
- [ ] 장비 관리 화면 (목록, CRUD)

### Week 4
- [ ] OID 편집기 구현
- [ ] 동적 규칙 설정 UI
- [ ] 실시간 값 미리보기

### Week 5
- [ ] SNMP 테스트 콘솔
- [ ] 요청 로그 뷰어
- [ ] WebSocket 실시간 업데이트

---

## Phase 3: 고급 기능 (2주)

### Week 6
- [ ] 응답 제어 기능 (지연, 에러, 타임아웃)
- [ ] SNMPv3 기본 지원 (인증만)

### Week 7
- [ ] MIB 파일 import 기능
- [ ] 프로젝트 저장/불러오기
- [ ] NetworkManager 모듈 (IP 자동 관리)

---

## Phase 4: 안정화 (1주)

### Week 8
- [ ] 통합 테스트
- [ ] 문서화
- [ ] 성능 최적화
- [ ] VM 이미지 빌드 (OVA/QCOW2)
- [ ] 릴리스
