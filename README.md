# n8n Workflow Automation — AI-Powered Notifications

Three importable n8n workflow JSONs that demonstrate form submission simulation (Task 1) and AI-powered Google Calendar-to-Telegram/WhatsApp event notifications (Task 2) using OpenRouter GPT-3.5 Turbo for AI message generation.

## What it does

Three workflows importable into any n8n instance:
- **Task 1:** Manual trigger generates 7 hardcoded JSON form submissions (names, emails, preferences), POSTs them to `httpbin.org/post`, and logs name/email/status to Google Sheets.
- **Task 2 (Telegram):** Polls Google Calendar every minute for Create/Update/Cancel/Start events, sends event data to OpenRouter AI (GPT-3.5 Turbo) to generate a friendly message with emojis, delivers it via Telegram Bot API, and logs to Google Sheets.
- **Task 2 (WhatsApp):** Same as Telegram variant but uses Green API for WhatsApp delivery and only handles the "created" event type.

**Note:** No `docker-compose.yml` is provided — n8n must be started manually via `docker run` commands. WhatsApp workflow only processes "created" events (not update/cancel/start like the Telegram version).

## Tech stack

- n8n (workflow automation engine)
- OpenRouter AI (GPT-3.5 Turbo)
- Google Calendar API, Google Sheets API
- Telegram Bot API, Green API (WhatsApp)
- `httpbin.org` (request echo endpoint for Task 1)

## Setup

```bash
# Start n8n locally
docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n

# Import workflows from workflows/ directory via n8n UI
# Configure .env with API keys (see .env.example)
# Start with: docker run ... -v $(pwd)/.env:/home/node/.env -e N8N_ENV_FILE=/home/node/.env ...
```

## Workflows

| File | Trigger | Actions |
|------|---------|---------|
| `Task_1_Workflow.json` | Manual | Generate 7 mock form submissions → POST to httpbin → log to Google Sheets |
| `Task_2_Telegram_AI_Workflow.json` | Google Calendar (poll 1min) | Detect Create/Update/Cancel/Start → OpenRouter AI → Telegram Bot → Google Sheets |
| `Task_2_WhatsApp_AI_Workflow.json` | Google Calendar (poll 1min) | Detect Created events only → OpenRouter AI → Green API WhatsApp → Google Sheets |

## Status

**Academic project — complete.** All three workflows are fully functional n8n export JSONs with proper node configurations and environment variable references. Screenshots show successful execution outputs. No docker-compose.yml is provided despite the "Docker-ready" badge. Task 2 WhatsApp is a subset of the Telegram workflow (only 'created' events).

*Assignment 2 — Tools & Techniques for Data Science, University of Central Punjab*