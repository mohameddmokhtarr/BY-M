# Client: Al Camilon Studio

## Overview
- **Client:** Zeyad
- **Business:** Clothing brand, Egypt
- **Status:** First client / demo phase

## What Was Built
A task notification system that fires a WhatsApp message automatically whenever a task changes status in Plane.

## How It Works
1. Zeyad's team uses Plane to manage tasks (shoots, production, logistics, campaigns)
2. When anyone moves a task to a new status, Plane fires a webhook
3. n8n catches the webhook and sends the task name + new status to Evolution API
4. Evolution API delivers a WhatsApp message to the configured phone number

## WhatsApp Message Format
```
🔔 Al Camilon Studio

*[Task Name]* moved to *[New Status]*

View in Plane → [Plane URL]
```

## Setup Details
- **Plane project:** Al Camilon Studio
- **n8n workflow:** "My workflow" (ID: XjIrdhagT6Au61EI)
- **Webhook path:** /webhook/plane-update
- **Evolution API instance:** al-camilon
- **Notification number:** configured in n8n HTTP Request node

## Handoff Steps (to give Zeyad full access)
1. Invite Zeyad to Plane by email (Settings → Members → Invite)
2. Add him to the Al Camilon project
3. Invite his team members and assign tasks to them
4. Change the WhatsApp number in n8n to Zeyad's number
5. Send him the Plane URL

## Demo Page
Published at: https://claude.ai/code/artifact/63f02532-0759-42a7-b792-3c7cbdd6760b
