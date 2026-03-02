# 설치 가이드

## VM 이미지 설치

### 1. 이미지 다운로드

- OVA (VMware, VirtualBox): `nmsim-v2.0.0.ova`
- QCOW2 (KVM, Proxmox): `nmsim-v2.0.0.qcow2`

### 2. 하이퍼바이저별 임포트

#### VMware
1. File > Open
2. OVA 파일 선택
3. Import

#### VirtualBox
1. File > Import Appliance
2. OVA 파일 선택
3. Import

#### Proxmox
```bash
# QCOW2 이미지 업로드
qm importdisk <vmid> nmsim-v2.0.0.qcow2 local-lvm

# 또는 직접 생성
qm create <vmid> --memory 4096 --cores 2 --name nmsim
qm set <vmid> --scsi0 local-lvm:vm-<vmid>-disk-0
```

### 3. 네트워크 설정

- **브릿지 모드** 권장
- NMS 서버와 통신 가능한 네트워크에 연결

### 4. VM 부팅

- 기본 계정: `nmsim` / `nmsim`
- NMSIM 서비스 자동 시작

### 5. 웹 UI 접속

```
http://{VM_IP}:8080
```

---

## 수동 설치 (개발용)

### 요구사항

- Ubuntu 22.04 LTS
- Python 3.11+
- Node.js 18+
- root 권한 (IP 관리용)

### 설치 단계

```bash
# 1. 저장소 클론
git clone https://github.com/xxx/nmsim.git
cd nmsim

# 2. Python 가상환경
python3 -m venv venv
source venv/bin/activate

# 3. 의존성 설치
pip install -r requirements.txt

# 4. 프론트엔드 빌드
cd frontend
npm install
npm run build
cd ..

# 5. 실행
sudo python -m uvicorn src.main:app --host 0.0.0.0 --port 8080
```

---

## 설정 파일

### 환경 변수

```bash
# .env
NMSIM_HOST=0.0.0.0
NMSIM_PORT=8080
NMSIM_SNMP_PORT=161
NMSIM_DB_PATH=./data/nmsim.db
NMSIM_NETWORK_INTERFACE=eth0
NMSIM_DEBUG=false
```

### systemd 서비스

```ini
# /etc/systemd/system/nmsim.service
[Unit]
Description=NMSIM SNMP Simulator
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/opt/nmsim
ExecStart=/opt/nmsim/venv/bin/python -m uvicorn src.main:app --host 0.0.0.0 --port 8080
Restart=always

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable nmsim
sudo systemctl start nmsim
```
