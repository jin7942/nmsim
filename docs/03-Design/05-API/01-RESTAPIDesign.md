# REST API 설계

## 기본 정보

- Base URL: `http://{host}:8080/api/v2`
- Content-Type: `application/json`
- 인증: 기본 인증 (선택)

---

## 장비 관리 API

### 장비 목록 조회
```
GET /devices
GET /devices?type=router&enabled=true
```

**Response:**
```json
{
  "items": [
    {
      "id": "uuid",
      "ip_address": "10.0.0.1",
      "name": "Router-01",
      "device_type": "router",
      "enabled": true
    }
  ],
  "total": 100,
  "page": 1,
  "size": 20
}
```

### 장비 추가
```
POST /devices
```

**Request:**
```json
{
  "ip_address": "10.0.0.100",
  "name": "Server-001",
  "device_type": "server",
  "vendor": "generic",
  "snmp_version": "v2c",
  "community": "public"
}
```

### 장비 수정
```
PUT /devices/{id}
```

### 장비 삭제
```
DELETE /devices/{id}
```

### 장비 활성화/비활성화
```
POST /devices/{id}/enable
POST /devices/{id}/disable
```

---

## OID 관리 API

### OID 목록 조회
```
GET /devices/{id}/oids
GET /devices/{id}/oids?prefix=1.3.6.1.2.1.1
```

### OID 값 수정
```
PUT /devices/{id}/oids/{oid}
```

**Request:**
```json
{
  "value": "208",
  "value_type": "INTEGER",
  "dynamic_rule": {
    "type": "gauge",
    "min": 100,
    "max": 300,
    "interval_sec": 5
  }
}
```

### SNMP WALK 미리보기
```
GET /devices/{id}/oids/walk/{base_oid}
```

---

## SNMP 테스트 API

### GET 요청
```
POST /snmp/get
```

**Request:**
```json
{
  "target": "10.0.0.51",
  "community": "public",
  "version": "v2c",
  "oid": "1.3.6.1.2.1.1.1.0"
}
```

**Response:**
```json
{
  "oid": "1.3.6.1.2.1.1.1.0",
  "type": "STRING",
  "value": "Evertz 570ACO-X19-25G",
  "response_time_ms": 2
}
```

### WALK 요청
```
POST /snmp/walk
```

---

## 로그 API

### 로그 조회
```
GET /logs
GET /logs?device_id=xxx&operation=GET&from=2024-01-01
```

### 로그 통계
```
GET /logs/stats
```

**Response:**
```json
{
  "total_requests": 12345,
  "by_operation": {
    "GET": 5234,
    "GETNEXT": 4567,
    "WALK": 2344,
    "SET": 200
  },
  "top_oids": [
    {"oid": "1.3.6.1.2.1.2.2.1.8", "count": 3421},
    {"oid": "1.3.6.1.2.1.1.3.0", "count": 2134}
  ]
}
```

### 로그 삭제
```
DELETE /logs?before=2024-01-01
```
