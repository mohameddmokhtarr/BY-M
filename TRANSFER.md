# Transfer Context — AI Hub by M

This file gives a fresh Claude Code session on the VPS everything it needs to continue work without prior conversation history.

---

## Who You Are Working With

**Mohamed** — co-founder of AI Hub by M (50/50 with Mohammed). Mohamed handles tech and Instagram; Mohammed handles sales. First client is Al Camilon Studio (Zeyad, clothing brand, Egypt).

---

## VPS

| Item | Value |
|---|---|
| Provider | Hostinger KVM 2 |
| IP | 187.7.26.39 |
| OS | Ubuntu 26.04 LTS |
| SSH | `ssh root@187.7.26.39` |
| Non-root user | `claude` (uid=1000, no sudo) |
| Coolify | https://app.coolify.io |
| Hostinger panel | https://hpanel.hostinger.com |

---

## Services Running on VPS

| Service | URL | Purpose |
|---|---|---|
| Plane | http://plane-btel0u75m9ovjpvwazm0pdbz.187.7.26.39.sslip.io | Task management |
| n8n | http://n8n-om25jcjupbzmk71jvbtuqmfr.187.7.26.39.sslip.io | Workflow automation |
| Evolution API v2.3.7 | http://evo-ci9o7vbjcmbmbbvgetkl0fn4.187.7.26.39.sslip.io | WhatsApp messaging |
| Uptime Kuma | http://uptimekuma-hxlocdduy2za0yxx9jq4ltzr.187.7.26.39.sslip.io | Monitoring |

---

## Paseo (Remote Agent Daemon)

- Installed globally at `/usr/bin/paseo`
- Runs as `claude` user (non-root) — required for `--dangerously-skip-permissions`
- Managed by systemd: `systemctl status paseo`
- Server ID: `srv_0A1slqcuqaI0`
- Daemon home: `/home/claude/.paseo/`
- Daemon logs: `/home/claude/.paseo/daemon.log`
- GitHub CLI authenticated as `mohameddmokhtarr` for the `claude` user

### Key systemd commands
```bash
systemctl status paseo
systemctl restart paseo
systemctl stop paseo
```

---

## Active Automation (Al Camilon Studio)

**Flow:** Plane task status change → n8n webhook → Evolution API → WhatsApp to Zeyad

### n8n Workflow
- Webhook: POST `/webhook/plane-update`
- HTTP Request to Evolution API: `/message/sendText/{instance}`
- Body fields: `number` (fixed), `text` (expression with task name + status)
- Body mode: **Using Fields Below** (not JSON mode — causes parse errors)

### Evolution API
- Manager UI: `http://evo-ci9o7vbjcmbmbbvgetkl0fn4.187.7.26.39.sslip.io/manager`
- Each client gets their own instance
- WhatsApp must be connected via QR scan per instance

---

## Monitoring

- Uptime Kuma monitors: Evolution API, n8n, Plane — all 100% uptime
- Mobile app: Uptime Kuma Manager (iOS)
- Plan: create a group per client in Uptime Kuma

---

## Adding a New Client

1. Create project in Plane
2. Copy Al Camilon n8n workflow, update phone number and Evolution API instance
3. Create new Evolution API instance, scan WhatsApp QR
4. Add Uptime Kuma monitors under a new group named after client
5. Invite client team to Plane project
6. Change WhatsApp notification number in n8n to client's number

---

## Pending Items

- [ ] Change Al Camilon WhatsApp notification number from `201229588884` to Zeyad's number
- [ ] Invite Zeyad and team to Plane
- [ ] Set up Uptime Kuma groups per client
- [ ] Push project files to GitHub so they're accessible on VPS

---

## Project Files (on Mac)

```
/Users/mohamedmokhtar/Downloads/BY M/
├── TRANSFER.md          ← this file
├── stack.md             ← full tech stack
├── operations.md        ← how to access and operate everything
├── session-log.md       ← full session history
├── al_camilon_demo.html ← client demo page
└── clients/
    └── al-camilon.md   ← Al Camilon setup and handoff guide
```

---

## Memory Location (Mac)

```
/Users/mohamedmokhtar/.claude/projects/-Users-mohamedmokhtar-Downloads-BY-M/memory/
```
