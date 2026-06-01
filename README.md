# 🏠 Homelab Project — <user>@pilab

> A three-machine home lab stack built for learning, monitoring, and virtualization.

---

## 📐 Architecture Overview

```
Internet
    │
    ▼
TP-Link Archer AXE7800 (Router)
    │
    ▼
TP-Link TL-SG108E (8-port managed switch)
    ├── 🍓 Raspberry Pi 5 8GB  →  pilab (<pi-ip>)
    ├── 💻 ASUS Q550LF         →  file server (TBD)
    ├── 🖥️  Lenovo ThinkCentre M720s  →  Proxmox (TBD)
    └── 🖥️  Main PC
```

---

## 🖥️ Machine Specs

### 🍓 Raspberry Pi 5 — `pilab`
| Component | Spec |
|-----------|------|
| Board | Raspberry Pi 5 8GB |
| OS | Raspberry Pi OS 64-bit |
| Storage | SanDisk Extreme 64GB microSD |
| Hostname | pilab |
| User | <user> |
| IP | <pi-ip> |
| Role | Monitoring + Docker services |

### 💻 ASUS Q550LF — File Server
| Component | Spec |
|-----------|------|
| CPU | Intel i7-4500U (2C/4T) |
| RAM | 16GB DDR3L 1600MHz (Transcend 2×8GB) |
| OS Drive | 120GB mSATA SSD (pending) |
| Storage | 1TB Crucial MX500 2.5" SATA (pending) |
| Role | NAS / File Server (OpenMediaVault or Samba) |

### 🖥️ Lenovo ThinkCentre M720s — Proxmox
| Component | Spec |
|-----------|------|
| CPU | Intel i7-8700 (6C/12T) @ 3.20GHz |
| RAM | 16GB DDR4 |
| Storage | 256GB SSD |
| OS | Proxmox VE (replacing Win 11 Pro) |
| VT-x / VT-d | ✅ / ✅ |
| Role | VM Lab (AD, Wazuh, Kali, LXC containers) |

---

## 🐳 Docker Stack — pilab

### Running containers

| Container | Port | Status |
|-----------|------|--------|
| Uptime Kuma | 3001 | ✅ running |

### Planned containers

| Container | Port | Purpose |
|-----------|------|---------|
| Pi-hole | 80, 53 | Network-wide DNS + ad blocking |
| Vaultwarden | 8080 | Self-hosted password manager |
| Grafana | 3000 | Monitoring dashboards |
| WireGuard VPN | 51820 | Remote access VPN |

---

## 🚀 Setup Log

### ✅ Phase 1 — Hardware acquisition
- [x] 16GB DDR3L SODIMM (Transcend 2×8GB) — ~$16
- [x] Lenovo ThinkCentre M720s i7-8700 — $145
- [x] TP-Link TL-SG108E 8-port switch — $24
- [x] Raspberry Pi 5 8GB CanaKit Essentials — $209
- [x] SanDisk Extreme 64GB microSD — $27
- [ ] 120GB mSATA SSD — waiting for price drop
- [ ] Crucial MX500 1TB 2.5" SATA — pending

### ✅ Phase 2 — Pi setup
- [x] Flash Raspberry Pi OS 64-bit
- [x] Configure hostname (pilab), user (<user>), SSH
- [x] First boot + SSH access confirmed
- [x] System update (apt update && apt upgrade)
- [x] Docker installed
- [x] Uptime Kuma deployed

### ⬜ Phase 3 — Pi services
- [ ] Pi-hole
- [ ] Vaultwarden
- [ ] Grafana
- [ ] WireGuard VPN

### ⬜ Phase 4 — Proxmox setup
- [ ] Install Proxmox VE on M720s
- [ ] Configure networking
- [ ] First VM (Ubuntu Server)
- [ ] Active Directory DC
- [ ] Wazuh SIEM

### ⬜ Phase 5 — NAS setup
- [ ] Install drives in ASUS Q550LF
- [ ] Install OpenMediaVault
- [ ] Configure Samba shares
- [ ] Mount shares on main PC

---

## 🔌 Network

| Device | IP | Notes |
|--------|-----|-------|
| Router | <router-ip> | TP-Link AXE7800 |
| pilab (Pi 5) | <pi-ip> | Static IP recommended |
| M720s (Proxmox) | TBD | |
| ASUS Q550LF | TBD | |

> ⚠️ **TODO:** Set static IPs for all homelab devices via router DHCP reservation

---

## 🔐 Access

```bash
# SSH into pilab
ssh <user>@<pi-ip>

# Uptime Kuma dashboard
http://<pi-ip>:3001
```

---

## 📦 Useful commands

```bash
# Check running containers
docker ps

# View container logs
docker logs uptime-kuma

# Restart a container
docker restart uptime-kuma

# Update a container
docker pull louislam/uptime-kuma:1
docker restart uptime-kuma

# Check disk usage
df -h

# Check memory usage
free -h

# Check CPU temp
vcgencmd measure_temp
```
