# Self-Hosted n8n Webhook Starter Pack

A bundle of 5 self-hosted n8n workflows built exclusively with built-in n8n nodes (no community-node installation required). Every workflow reads configuration and secrets strictly from `$env.*` environment variables, enforces webhook authentication or Telegram chat allowlists before downstream calls, and returns deterministic JSON payloads for automation clients and AI agents.

## Included Workflows

| # | File | Trigger | Purpose | Environment Variables |
|---|---|---|---|---|
| 01 | [`01_vietqr_sepay_sheets_telegram.json`](./01_vietqr_sepay_sheets_telegram.json) | `POST /webhook/sepay-vietqr-webhook` | Validates `Authorization: Apikey <key>`, extracts order codes (`DH`/`ORD`/`INV`), logs inbound payments to Google Sheets, sends a Telegram alert, and responds with structured JSON (`200` / `401`). | `SEPAY_WEBHOOK_API_KEY`, `GOOGLE_SHEET_ID`, `TELEGRAM_BOT_TOKEN`, `TELEGRAM_CHAT_ID` |
| 02 | [`02_ai_seo_research_notion.json`](./02_ai_seo_research_notion.json) | `POST /webhook/ai-seo-brief-vn` | Calls any OpenAI-compatible LLM API (DeepSeek, Gemini OpenAI bridge, OpenAI, or local gateway) to generate a JSON SEO brief, creates a Notion database page, logs to Google Sheets, and returns JSON. | `LLM_API_BASE_URL`, `LLM_API_KEY`, `LLM_MODEL`, `NOTION_API_KEY`, `NOTION_DATABASE_ID`, `GOOGLE_SHEET_ID` |
| 03 | [`03_openclaw_telegram_assistant.json`](./03_openclaw_telegram_assistant.json) | Telegram Trigger | 24/7 private Telegram assistant gated by owner chat ID allowlist (`ALLOWED_TELEGRAM_CHAT_ID`), routing `/tomtat` (`summarize`), `/tacvu` (`agent_task`), and general messages to an OpenClaw or OpenAI-compatible gateway. | `ALLOWED_TELEGRAM_CHAT_ID`, `OPENCLAW_GATEWAY_URL`, `OPENCLAW_GATEWAY_TOKEN`, `OPENCLAW_MODEL`, `TELEGRAM_BOT_TOKEN` |
| 04 | [`04_uptime_ssl_price_watcher.json`](./04_uptime_ssl_price_watcher.json) | Schedule (15 min) | Probes a comma-separated URL list for HTTP downtime (`<200` or `>=400`), TLS/HTTPS issues, high latency, and optional regex price patterns; sends Telegram alerts only when an issue is detected. | `WATCH_TARGET_URLS`, `WATCH_MAX_LATENCY_MS`, `WATCH_PRICE_REGEX`, `TELEGRAM_BOT_TOKEN`, `TELEGRAM_ALERT_CHAT_ID` |
| 05 | [`05_shop_cskh_rag_bot.json`](./05_shop_cskh_rag_bot.json) | `POST /webhook/shop-cskh-rag-webhook` | Loads an FAQ JSON endpoint, ranks matching policy items, flags complaint terms, drafts a grounded LLM response, and applies a `>= 0.75` confidence gate before auto-replying or escalating to a Telegram support group. | `FAQ_API_ENDPOINT`, `LLM_API_BASE_URL`, `LLM_API_KEY`, `LLM_MODEL`, `TELEGRAM_BOT_TOKEN`, `CSKH_TELEGRAM_GROUP_ID` |

## Architecture

```text
Webhook / Telegram / Schedule Trigger
        │
        ▼
Auth & Allowlist Gate (Apikey header / Chat ID allowlist / Input parser)
        │
        ▼
Processing Layer (OpenAI-compatible LLM / HTTP Probe / FAQ Ranker)
        │
        ▼
Deterministic Decision Branch (IF: valid inbound payment / alert / confidence >= 0.75)
        ├── Pass Branch ──► Google Sheets / Notion / Structured Auto-Reply JSON (200)
        └── Alert / Escalation Branch ──► Telegram Bot API / Rejected JSON (401 / 200)
```

## Prerequisites

- Self-hosted n8n `v1.94+` (`executionOrder: "v1"`, built-in nodes only: `webhook`, `respondToWebhook`, `scheduleTrigger`, `telegramTrigger`, `httpRequest`, `code`, `if`, `googleSheets`).
- `N8N_BLOCK_ENV_ACCESS_IN_NODE=false` if supplying runtime configuration via environment variables (alternatively map them to n8n Variables/Credentials).
- No secrets or API tokens are embedded in any workflow export (`templateCredsSetupCompleted: false`).

## Environment Variables

```env
# Telegram
TELEGRAM_BOT_TOKEN=your_telegram_bot_token
TELEGRAM_CHAT_ID=your_default_chat_id
TELEGRAM_ALERT_CHAT_ID=your_alerts_chat_id
CSKH_TELEGRAM_GROUP_ID=your_support_group_chat_id
ALLOWED_TELEGRAM_CHAT_ID=123456789

# OpenAI-Compatible LLM & OpenClaw Gateway
LLM_API_BASE_URL=https://api.deepseek.com/v1
LLM_API_KEY=your_llm_api_key
LLM_MODEL=deepseek-chat
OPENCLAW_GATEWAY_URL=http://openclaw:18789/v1/chat/completions
OPENCLAW_GATEWAY_TOKEN=your_openclaw_gateway_token
OPENCLAW_MODEL=openclaw-default

# Workflow Integrations
SEPAY_WEBHOOK_API_KEY=your_sepay_webhook_key
GOOGLE_SHEET_ID=your_google_spreadsheet_id
NOTION_API_KEY=your_notion_integration_token
NOTION_DATABASE_ID=your_notion_database_id
WATCH_TARGET_URLS=https://example.com,https://n8n.example.com
WATCH_MAX_LATENCY_MS=2500
WATCH_PRICE_REGEX=
FAQ_API_ENDPOINT=https://api.example.com/faq.json
```

## Setup Instructions

1. Add the required environment variables to your self-hosted n8n `.env` or Docker Compose service definition and restart n8n.
2. In n8n, open **Workflows → Import from File** and import any JSON file (`01`–`05`).
3. Attach your Google Sheets OAuth2 credential (`01`, `02`) or Telegram Bot credential (`03`) on the respective nodes.
4. Verify each endpoint using the `curl` commands in [`DEMO.md`](./DEMO.md) against `/webhook-test/...`, then activate for `/webhook/...`.

## AI-First JSON Schema & Reliability Notes

- **Deterministic Webhook Contracts**: All HTTP webhook workflows (`01`, `02`, `05`) use `responseMode: "responseNode"` to return stable JSON fields (`success`, `ok`, `mode`, `confidence`, `orderCode`, `txId`).
- **Fail-Closed Auth**: Workflow `01` rejects unauthorized or non-inbound payloads with HTTP `401` (`{ "success": false, "ignored": true }`). Workflow `03` drops non-allowlisted Telegram chat IDs before reaching the gateway.
- **Confidence-Gated Escalation**: Workflow `05` requires structured LLM JSON (`reply`, `confidence`, `needHuman`) and escalates to Telegram whenever complaint keywords match, JSON parsing fails, or `confidence < 0.75`.

## License & Attribution

MIT License. Upstream self-hosted Docker Compose stack and companion workflows: [tunguyen1993/vn-ai-vps-stack](https://github.com/tunguyen1993/vn-ai-vps-stack).
