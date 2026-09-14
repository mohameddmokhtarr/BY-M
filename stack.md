# Tech Stack — AI Hub by M

## Infrastructure
- **VPS** — Hostinger KVM 2, IP: 187.7.26.39, Ubuntu 26.04 LTS, 2 CPU cores, 7.7GB RAM, 100GB disk
- **Coolify** — self-hosted deployment platform running on the VPS, manages all services via Docker

## Services Running on VPS
| Service | URL | Purpose |
|---|---|---|
| Plane | http://plane-btel0u75m9ovjpvwazm0pdbz.187.7.26.39.sslip.io | Project/task management |
| n8n | http://n8n-om25jcjupbzmk71jvbtuqmfr.187.7.26.39.sslip.io | Workflow automation |
| Evolution API v2.3.7 | http://evo-ci9o7vbjcmbmbbvgetkl0fn4.187.7.26.39.sslip.io | WhatsApp messaging |
| Uptime Kuma | http://uptimekuma-hxlocdduy2za0yxx9jq4ltzr.187.7.26.39.sslip.io | Service monitoring |
| Paseo | 187.7.26.39:6767 | Remote agent/coding daemon |

## Automation Flow (Al Camilon Studio)
Plane (task status change) → n8n webhook → Evolution API → WhatsApp notification

## Monitoring
- Uptime Kuma monitors all 3 client services (Plane, n8n, Evolution API)
- Mobile app: Uptime Kuma Manager (iOS)
- All services show 100% uptime

## Remote Access
- Paseo daemon running on VPS (port 6767, password protected)
- Connected to Mac Paseo app as remote host
- GitHub CLI installed and authenticated on VPS
