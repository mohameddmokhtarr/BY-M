# Operations Guide — AI Hub by M

## Accessing the Server
- **Hostinger panel:** https://hpanel.hostinger.com
- **Coolify:** https://app.coolify.io
- **SSH:** `ssh root@187.7.26.39`

## Monitoring
- **Uptime Kuma app (iOS):** Shows live status of all services
- **Uptime Kuma web:** http://uptimekuma-hxlocdduy2za0yxx9jq4ltzr.187.7.26.39.sslip.io
- Monitors: Evolution API, n8n, Plane

## Paseo (Remote Agent Daemon)
- Running on VPS at port 6767
- Password: stored securely
- Connected via Paseo Mac app as "My VPS" host
- Use to run AI agents on the server 24/7

## Adding a New Client
1. Create a new project in Plane
2. Set up an n8n workflow (copy existing Al Camilon workflow)
3. Create a new Evolution API instance for the client
4. Add monitors in Uptime Kuma under a new group named after the client
5. Invite client to Plane

## n8n Workflow Structure (Al Camilon)
- Node 1: Webhook (POST /webhook/plane-update)
- Node 2: HTTP Request → Evolution API /message/sendText/{instance}
  - Body: number (fixed), text (expression with task name + status)

## Evolution API
- Manager UI: http://evo-ci9o7vbjcmbmbbvgetkl0fn4.187.7.26.39.sslip.io/manager
- Each client gets their own instance
- WhatsApp must be connected (scan QR) per instance
