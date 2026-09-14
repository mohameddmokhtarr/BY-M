# Session Log — AI Hub by M
Date: September 15, 2026

---

## Earlier Session (summarized — original messages not available)

### Context
Mohamed is co-founding "AI Hub by M" with Mohammed (50/50 partnership). First client is Al Camilon Studio (Zeyad, clothing brand Egypt). The goal was to complete an n8n WhatsApp notification workflow so that when a Plane work item changes state, a WhatsApp message fires automatically to +201229588884.

### What was accomplished before context limit
- Configured n8n Webhook node (POST, path: plane-update)
- Added HTTP Request node to call Evolution API
- Connected Webhook → HTTP Request nodes
- Published workflow
- Added Plane webhook pointing to n8n
- Tested — Plane fired webhook, n8n received it, but HTTP Request node failed with "JSON parameter needs to be valid JSON" error
- Root cause: body was set to "Using JSON" mode with a JS expression. n8n tried to parse it as literal JSON before evaluating, which failed.
- Fix identified: switch "Specify Body" from "Using JSON" to "Using Fields Below" and add separate number and text fields

---

## Continued Session

**Mohamed:** Click "Using Fields Below" in the dropdown.

**Claude:** "Using Fields Below" is now selected. Fill in Name = `number`, Value = `201229588884`. Then add a second field for `text` with expression mode.

**Mohamed:** done sent

**Claude:** The WhatsApp message fired — the workflow is working end-to-end. Plane state change → n8n webhook → Evolution API → WhatsApp. The Al Camilon Studio notification system is live.

---

## Client Demo

**Mohamed:** now add it to the client demo

**Claude:** Asked what format. Recommended a live web page (artifact).

**Mohamed:** forget about the branding

**Claude:** Built a clean demo page showing the workflow in plain language with a WhatsApp message example. Published at: https://claude.ai/code/artifact/63f02532-0759-42a7-b792-3c7cbdd6760b

---

## Understanding the System

**Mohamed:** i dont understand anything on how to present or whats the stack

**Claude:** 
- How to present: "The moment anything moves in your task board, you get a WhatsApp message. Here's what it looks like." Then show the page.
- Stack: Plane (task board) → n8n (automation engine) → Evolution API (WhatsApp sender). All run on your VPS, private, no third-party.

**Mohamed:** if i want to hand it to zeyad how can i handle do it

**Claude:** Two options — share the demo link, or give him real access to Plane (invite by email, add to project, change WhatsApp number in n8n to his).

**Mohamed:** so he opens plane and changes tasks status?

**Claude:** Yes. He logs in, his team manages tasks, WhatsApp fires automatically when anything moves.

**Mohamed:** how to connect the tasks to his team

**Claude:** Invite team to Plane by email. Assign tasks to team members. Notification triggers on any status change by anyone in the project.

**Mohamed:** all the team members have plane and when updated he gets a notification

**Claude:** Exactly. Team uses Plane → Zeyad gets WhatsApp notifications.

---

## Server & Monitoring

**Mohamed:** [showed Hostinger VPS overview — CPU 19%, Memory 30%, Disk 11GB/100GB]

**Claude:** Server is healthy. Everything running fine.

**Mohamed:** if i close terminal everything shuts?

**Claude:** No. Terminal is just a remote connection window. Server keeps running 24/7 whether terminal is open or not.

**Mohamed:** i want an app for server health

**Claude:** Recommended Uptime Kuma — already available in Coolify.

**Mohamed:** [deployed Uptime Kuma, set up mobile app]

**Claude:** Added 3 monitors: Evolution API (100%, 90ms), n8n (100%, 11ms), Plane (100%, 174ms). All green.

**Mohamed:** if i have multiple clients how can i differentiate which one has the problem

**Claude:** Name monitors per client (e.g. "Al Camilon — Plane") and create Groups in Uptime Kuma — one group per client.

---

## Paseo on VPS

**Mohamed:** would it be good to add paseo to this stack?

**Claude:** Not needed for Al Camilon specifically — the stack is complete. Paseo adds value when you need remote agents or changes across multiple clients.

**Mohamed:** i want paseo to be on the server running 24/7

**Claude:** Deployed Paseo via Docker on VPS (port 6767, password protected). Connected Mac Paseo app to VPS as remote host "My VPS".

### Paseo Setup Commands Used
```bash
docker run -d \
  --name paseo \
  --restart always \
  -p 6767:6767 \
  -e PASEO_PASSWORD=Ffcwbam5. \
  -v /root/.paseo:/home/paseo/.paseo \
  -v /usr/bin/gh:/usr/bin/gh \
  -v /root/.config/gh:/home/paseo/.config/gh \
  ghcr.io/getpaseo/paseo:latest

docker exec paseo chown -R paseo:paseo /home/paseo/.config/gh
```

### GitHub CLI Setup on VPS
```bash
# Install GitHub CLI
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
apt install gh -y
gh auth login  # authenticated as mohameddmokhtarr
```

**Mohamed:** [connected VPS as remote host in Paseo Mac app — both Mac and VPS now visible]

---

## Key Concepts Discussed

**What is the VPS?**
A cloud Linux server (Ubuntu). Coolify is the dashboard. Terminal is the engine room. Closing the terminal doesn't shut anything down.

**What is Paseo?**
A remote daemon that manages coding agents and terminals. Running on VPS means agents run 24/7 even when Mac is off.

**Can Zeyad change tasks on Plane?**
Yes — once invited, he can add, edit, delete, and move tasks freely.

**What is the purpose of the WhatsApp message?**
Zeyad is busy and on the go. His team handles production, shooting, logistics. He gets a WhatsApp ping the moment something is done or stuck — no micromanaging needed.

**Does the workflow affect Evolution API if tasks are renamed?**
No. Evolution API only cares about status changes, not task names or content.

**What is Uptime Kuma?**
Service health monitoring. Shows if Plane, n8n, or Evolution API go down. Mobile app available.

**When to use Paseo?**
Complex automations: auto-create tasks from Shopify orders, overdue task alerts, weekly progress reports, etc. Not needed for simple task management.

---

## Files in This Repo
- `stack.md` — full tech stack and service URLs
- `clients/al-camilon.md` — Al Camilon Studio setup and handoff guide
- `operations.md` — how to access server, monitor, add new clients
- `al_camilon_demo.html` — client demo page (also published as artifact)
- `session-log.md` — this file
