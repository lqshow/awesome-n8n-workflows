# Demo & Webhook Test Commands

Exact `curl` requests and expected JSON outputs for testing the workflows on a self-hosted n8n instance (`N8N_BASE_URL`, e.g. `http://localhost:5678` or `https://n8n.example.com`).

> Use `/webhook-test/<path>` during **Test Workflow** in the n8n editor, or `/webhook/<path>` once activated.

## 1. Workflow 01 — SePay / VietQR Payment Webhook (`01_vietqr_sepay_sheets_telegram.json`)

### Valid Authorized Payment (`HTTP 200`)

```bash
curl -sS -X POST "${N8N_BASE_URL}/webhook/sepay-vietqr-webhook" \
  -H "Content-Type: application/json" \
  -H "Authorization: Apikey ${SEPAY_WEBHOOK_API_KEY}" \
  -d '{
    "id": "TX20261121001",
    "gateway": "VCB",
    "transferType": "in",
    "transferAmount": 490000,
    "content": "Thanh toan don hang DH20261121A",
    "transactionDate": "2026-11-21 14:30:00"
  }'
```

Expected JSON output:

```json
{
  "success": true,
  "orderCode": "DH20261121A",
  "txId": "TX20261121001"
}
```

### Unauthorized Request (`HTTP 401`)

```bash
curl -sS -i -X POST "${N8N_BASE_URL}/webhook/sepay-vietqr-webhook" \
  -H "Content-Type: application/json" \
  -H "Authorization: Apikey invalid-key" \
  -d '{
    "id": "TX20261121002",
    "transferType": "in",
    "transferAmount": 100000,
    "content": "ORD998877"
  }'
```

Expected JSON output (`HTTP 401`):

```json
{
  "success": false,
  "ignored": true
}
```

## 2. Workflow 02 — AI SEO Research Agent (`02_ai_seo_research_notion.json`)

```bash
curl -sS -X POST "${N8N_BASE_URL}/webhook/ai-seo-brief-vn" \
  -H "Content-Type: application/json" \
  -d '{
    "keyword": "self-hosted n8n docker compose guide",
    "audience": "DevOps engineers and indie builders",
    "intent": "Commercial Investigation"
  }'
```

Expected JSON output (`HTTP 200`):

```json
{
  "ok": true,
  "keyword": "self-hosted n8n docker compose guide",
  "title": "<LLM-generated SEO title saved to Notion and Google Sheets>"
}
```

## 3. Workflow 03 — OpenClaw Telegram Assistant (`03_openclaw_telegram_assistant.json`)

Triggered via `telegramTrigger` when `message.chat.id` matches an entry in `ALLOWED_TELEGRAM_CHAT_ID`.

Command routing implemented in `Kiem tra Whitelist & Lenh`:
- `/tomtat <text>` → `command: "summarize"`
- `/tacvu <task>` → `command: "agent_task"`
- Any other text → `command: "chat"`

Responses are truncated safely to `3900` characters before sending to Telegram (`sendMessage`). Messages from non-allowlisted chat IDs fail the IF gate (`isAllowed === true`) with zero LLM requests made.

## 4. Workflow 04 — Website Uptime, SSL & Price Watcher (`04_uptime_ssl_price_watcher.json`)

Triggered every 15 minutes (`scheduleTrigger`). Sample environment variables:

```env
WATCH_TARGET_URLS=https://example.com,https://n8n.example.com
WATCH_MAX_LATENCY_MS=2500
WATCH_PRICE_REGEX=\$[0-9]+\.[0-9]{2}
```

Sample Telegram alert sent when an endpoint returns `503` and exceeds `2500ms`:

```text
CANH BAO GIAM SAT WEBSITE / SSL / GIA
URL: https://example.com
Trang thai: HTTP 503 (3120ms)
Van de: HTTP loi (503); Phan hoi cham (3120ms)
Khong cau hinh theo doi gia
Thoi diem: 2026-11-21T14:30:00.000Z
```

## 5. Workflow 05 — AI CSKH RAG Support Bot (`05_shop_cskh_rag_bot.json`)

### High-Confidence FAQ Auto-Reply (`mode: "auto_rag"`)

```bash
curl -sS -X POST "${N8N_BASE_URL}/webhook/shop-cskh-rag-webhook" \
  -H "Content-Type: application/json" \
  -d '{
    "customerName": "Minh",
    "customerId": "cust_1042",
    "message": "Chinh sach bao hanh va doi tra trong bao nhieu ngay?"
  }'
```

Expected JSON output (`HTTP 200`, when `confidence >= 0.75` and `hasComplaint === false`):

```json
{
  "mode": "auto_rag",
  "confidence": 0.91,
  "reply": "<Grounded FAQ answer drafted by LLM>"
}
```

### Complaint or Low-Confidence Escalation (`mode: "escalated_human"`)

```bash
curl -sS -X POST "${N8N_BASE_URL}/webhook/shop-cskh-rag-webhook" \
  -H "Content-Type: application/json" \
  -d '{
    "customerName": "Lan",
    "customerId": "cust_2099",
    "message": "Don hang giao sai va toi muon khieu nai hoan tien ngay"
  }'
```

Expected JSON output (`HTTP 200`, plus Telegram alert dispatched to `CSKH_TELEGRAM_GROUP_ID`):

```json
{
  "mode": "escalated_human",
  "confidence": 0.42,
  "reply": "Da ghi nhan yeu cau cua ban va chuyen ngay cho nhan vien CSKH de ho tro chinh xac nhat trong it phut."
}
```

## Validation Checklist

All 5 workflow JSON exports were verified locally before submission for:
- Valid JSON syntax and n8n `executionOrder: "v1"` schema
- Complete node-to-node connection integrity and `$('Node Name')` expression resolution
- Zero hardcoded API keys, tokens, credentials, or affiliate links
