# 데이터베이스 스키마 설계

## 개요

- DBMS: SQLite
- ORM: SQLAlchemy

## ERD

```
┌─────────────┐       ┌─────────────┐
│   Device    │       │  OIDValue   │
├─────────────┤       ├─────────────┤
│ id (PK)     │───┐   │ id (PK)     │
│ ip_address  │   │   │ device_id   │──┐
│ name        │   └──<│ oid         │  │
│ device_type │       │ value_type  │  │
│ vendor      │       │ static_value│  │
│ snmp_version│       │ dynamic_rule│  │
│ community   │       │ created_at  │  │
│ enabled     │       │ updated_at  │  │
│ created_at  │       └─────────────┘  │
│ updated_at  │                        │
└─────────────┘                        │
                                       │
┌─────────────┐                        │
│ RequestLog  │                        │
├─────────────┤                        │
│ id (PK)     │                        │
│ timestamp   │                        │
│ source_ip   │                        │
│ target_ip   │────────────────────────┘
│ snmp_version│
│ operation   │
│ oid         │
│ response_type│
│ response_ms │
│ error_msg   │
└─────────────┘
```

## 테이블 정의

### Device

```sql
CREATE TABLE device (
    id TEXT PRIMARY KEY,
    ip_address TEXT NOT NULL UNIQUE,
    name TEXT NOT NULL,
    device_type TEXT NOT NULL,
    vendor TEXT DEFAULT 'generic',
    snmp_version TEXT DEFAULT 'v2c',
    community TEXT DEFAULT 'public',
    v3_credentials TEXT,  -- JSON
    enabled BOOLEAN DEFAULT TRUE,
    response_delay_ms INTEGER DEFAULT 0,
    error_mode TEXT DEFAULT 'none',
    error_rate REAL DEFAULT 0.0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### OIDValue

```sql
CREATE TABLE oid_value (
    id TEXT PRIMARY KEY,
    device_id TEXT NOT NULL,
    oid TEXT NOT NULL,
    value_type TEXT NOT NULL,
    static_value TEXT,
    dynamic_rule TEXT,  -- JSON
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (device_id) REFERENCES device(id) ON DELETE CASCADE,
    UNIQUE (device_id, oid)
);

CREATE INDEX idx_oid_value_device ON oid_value(device_id);
CREATE INDEX idx_oid_value_oid ON oid_value(oid);
```

### RequestLog

```sql
CREATE TABLE request_log (
    id TEXT PRIMARY KEY,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    source_ip TEXT NOT NULL,
    target_ip TEXT NOT NULL,
    snmp_version TEXT,
    operation TEXT NOT NULL,
    oid TEXT,
    response_type TEXT,
    response_time_ms INTEGER,
    error_message TEXT
);

CREATE INDEX idx_request_log_timestamp ON request_log(timestamp);
CREATE INDEX idx_request_log_target ON request_log(target_ip);
```

## 동적 규칙 JSON 스키마

```json
// Counter
{
  "type": "counter",
  "increment": 1000,
  "interval_sec": 1
}

// Gauge
{
  "type": "gauge",
  "min": 100,
  "max": 300,
  "variation": 10,
  "interval_sec": 5
}

// Uptime
{
  "type": "uptime",
  "start_value": 0
}

// Pattern
{
  "type": "pattern",
  "values": [10, 20, 30, 40, 30, 20, 10],
  "interval_sec": 60
}
```
