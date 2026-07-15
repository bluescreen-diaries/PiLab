# 🏠 Homelab Project — bluescreen-diaries

> A multi-machine home lab stack built for learning, monitoring, virtualization, and AI-assisted 3D mesh generation.

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
    ├── 🍓 Raspberry Pi 5 8GB     →  pilab       (<pi-ip>)
    ├── 💻 ASUS Q550LF            →  NAS/files   (TBD)
    └── 🖥️  Lenovo ThinkCentre M720s →  Proxmox     (TBD)
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
| Status | ✅ Live |

### 💻 ASUS Q550LF — File Server
| Component | Spec |
|-----------|------|
| CPU | Intel i7-4500U (2C/4T) |
| RAM | 16GB DDR3L 1600MHz (Transcend 2×8GB) |
| OS Drive | 128GB mSATA SSD (bought) |
| Storage | 2.5" SATA drive — SSD or HDD (pending) |
| Role | NAS / File Server (OpenMediaVault) |
| Status | 🔄 Hardware acquired, not yet assembled |

### 🖥️ Lenovo ThinkCentre M720s — Proxmox
| Component | Spec |
|-----------|------|
| CPU | Intel i7-8700 (6C/12T) @ 3.20GHz |
| RAM | 16GB DDR4 |
| Storage | 256GB SSD |
| OS | Proxmox VE (replacing Win 11 Pro) |
| VT-x / VT-d | ✅ / ✅ |
| Role | VM Lab — Wazuh, osTicket, LXC containers |
| Status | 🔄 Hardware acquired, power cable pending |

---

## 🐳 Docker Stack — pilab

### Running containers
| Container | Port | Status |
|-----------|------|--------|
| Uptime Kuma | 3001 | ✅ running |
| Pi-hole | 53, 80 | ✅ running |
| Portainer | 9000 | ✅ running |
| Glance | 8081 | ✅ running |

### Planned containers
| Container | Port | Purpose |
|-----------|------|---------|
| Vaultwarden | 8080 | Self-hosted password manager |
| Grafana | 3000 | Monitoring dashboards |
| Hermes | 8025 | Notification / alerting server |
| WireGuard VPN | 51820 | Remote access VPN |

---

## 🖥️ Dashboards

| Tool | Purpose |
|------|---------|
| **Glance** | Homepage — bookmarks to all services in one place |
| **Portainer** | Docker container management via web UI |
| **Uptime Kuma** | Uptime/health monitoring for all devices and services |

---

## 🖥️ VM Stack — Lenovo M720s (Proxmox)

| VM / Container | Type | Purpose |
|----------------|------|---------|
| Ubuntu Server | VM | General purpose Linux |
| Wazuh | VM | SIEM — security monitoring |
| osTicket | LXC | Helpdesk ticketing system |
| Windows Server / AD | VM | Active Directory lab (future) |
| pfSense | VM | Firewall (future phase) |

### VLAN learning lab (virtual)
Simulating VLANs inside Proxmox using virtual bridges before applying real VLAN configs to the physical TL-SG108E switch.

- [ ] Create multiple virtual bridges (vmbr1, vmbr2, etc.)
- [ ] Assign VMs to simulate VLAN 10 (homelab) / VLAN 20 (personal)
- [ ] Practice inter-VLAN routing concepts
- [ ] Apply learnings to physical switch (optional, future)

---

## 🚀 Setup Log

### ✅ Phase 1 — Hardware acquisition
- [x] 16GB DDR3L SODIMM (Transcend 2×8GB) — ~$16
- [x] Lenovo ThinkCentre M720s i7-8700 — $145
- [x] TP-Link TL-SG108E 8-port switch — $24
- [x] Raspberry Pi 5 8GB CanaKit Essentials — $209
- [x] SanDisk Extreme 64GB microSD — $27
- [x] 128GB mSATA SSD (used, enterprise pull) — $21
- [x] C13 power cable for M720s — $6
- [ ] 2.5" SATA storage drive (SSD or HDD) — pending

### ✅ Phase 2 — Pi setup
- [x] Flash Raspberry Pi OS 64-bit
- [x] Configure hostname (pilab), user (<user>), SSH
- [x] First boot + SSH access confirmed
- [x] System update (apt update && apt upgrade)
- [x] Docker installed
- [x] Uptime Kuma deployed

### ✅ Phase 3 — Pi services & dashboards
- [x] Uptime Kuma
- [x] Pi-hole — network-wide DNS ad blocking, router DNS pointed at Pi
- [x] Portainer — Docker web management UI
- [x] Glance — homepage dashboard
- [ ] Vaultwarden
- [ ] Grafana
- [ ] Hermes
- [ ] WireGuard VPN

### ⬜ Phase 4 — Proxmox setup
- [ ] Install Proxmox VE on M720s
- [ ] Configure networking
- [ ] First VM (Ubuntu Server)
- [ ] Wazuh SIEM
- [ ] osTicket ticketing system
- [ ] VLAN simulation lab (virtual bridges)
- [ ] Active Directory DC (future)
- [ ] pfSense firewall (future)

### ⬜ Phase 5 — NAS setup
- [x] mSATA OS drive acquired
- [ ] 2.5" SATA storage drive
- [ ] Install drives in ASUS Q550LF
- [ ] Install OpenMediaVault
- [ ] Configure Samba shares
- [ ] Mount shares on network

---

## 🔌 Network

| Device | IP | Notes |
|--------|-----|-------|
| Router | <router-ip> | TP-Link AXE7800, DNS → pilab |
| pilab (Pi 5) | <pi-ip> | Primary DNS server for network |
| Lenovo M720s | TBD | |
| ASUS Q550LF | TBD | |

> 🔒 **Gaming consoles (PS5/Xbox):** set DNS manually to 8.8.8.8 to bypass Pi-hole and avoid compatibility issues.
>
> ⚠️ **TODO:** Set static IPs for all homelab devices via router DHCP reservation

---

## 🔐 Access

```bash
# SSH into pilab
ssh <user>@<pi-ip>

# Glance dashboard (homepage)
http://<pi-ip>:8081

# Uptime Kuma dashboard
http://<pi-ip>:3001

# Pi-hole dashboard
http://<pi-ip>/admin

# Portainer dashboard
http://<pi-ip>:9000
```

> 🔑 Passwords are stored securely and not included in this repo.

---

## 📦 Useful commands

```bash
# Check running containers
docker ps

# View container logs
docker logs <container_name>

# Restart a container
docker restart <container_name>

# Check disk usage
df -h

# Check memory usage
free -h

# Check CPU temp (Pi only)
vcgencmd measure_temp

# Edit Glance dashboard config
nano ~/glance/config.yml
docker restart glance
```

---

## 💰 Budget

| Item | Cost |
|------|------|
| 16GB DDR3L SODIMM | ~$16 |
| Lenovo M720s (Proxmox) | $145 |
| TL-SG108E switch | $24 |
| Pi 5 8GB CanaKit kit | $209 |
| SanDisk Extreme 64GB | $27 |
| 128GB mSATA SSD (used) | $21 |
| C13 power cable | $6 |
| 2.5" SATA storage drive | pending |
| **Total (so far)** | **~$448** |

---

## 📬 Secondary Project — Mail Server

A self-hosted mail server for learning email protocols and infrastructure.

### Goals
- Understand SMTP, IMAP, POP3 protocols hands-on
- Learn DNS mail records (MX, SPF, DKIM, DMARC)
- Practice TLS/SSL certificate management
- Understand email security and anti-spam measures

### Planned stack
| Tool | Purpose |
|------|---------|
| Mailcow | Full-featured mail server (Docker-based, web UI) |

> ⚠️ Primarily a learning exercise — residential IPs are typically blacklisted by major providers. Internal lab use only.

**Runs on:** Lenovo M720s (Proxmox VM)

---

⚠️ This project was built collaboratively with Claude (Anthropic) as part of my IT portfolio. The architecture, logic, and learning are mine — Claude assisted with code structure and debugging.
