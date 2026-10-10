# 📅 Yandex Calendar Events via CalDAV

> Create or update events in Yandex Calendar from a plain HTTP request - no OAuth app, no Google account.

## ✨ Core features

- **Create or update**: sending the same `uid` overwrites the existing event, so retries never duplicate entries.
- **Credential-based auth**: HTTP Basic Auth with a Yandex CalDAV app password, plus Header Auth for the webhook. Nothing is hardcoded in the workflow.
- **Portable**: change the base URL in the Set node and the same workflow talks to any CalDAV server (Nextcloud, iCloud, Fastmail).
- **Readable result**: a small Code node turns CalDAV status codes into JSON (201 created, 204 updated, 401/403/404 explained).

## 📥 Workflow file

- `yandex-calendar-caldav.json` - import with **Workflow menu → Import from File**.

## 🛠 Dependencies

- n8n with built-in nodes: Webhook, Set, Convert to File, HTTP Request, Code (no community nodes)
- A Yandex account with a CalDAV app password: Yandex ID → **Security → App passwords → Calendars**

## 🔧 Setup

1. Create the CalDAV app password in Yandex ID.
2. In n8n add an **HTTP Basic Auth** credential (Yandex login + that app password) and select it in **Upload to Yandex Calendar**.
3. Add a **Header Auth** credential with the header `x-webhook-token` and select it in **Event Request**.
4. Open **Set Calendar Options** and set `calendarPath`, for example `/calendars/user@yandex.ru/events/`.

## 🎬 Demo

```bash
curl -X POST https://your-n8n.example.com/webhook/yandex-calendar-event \
  -H 'Content-Type: application/json' \
  -H 'x-webhook-token: YOUR_SECRET' \
  -d '{"title":"Team sync","start":"2026-11-12T09:00:00+03:00","end":"2026-11-12T09:30:00+03:00","allDay":false,"uid":"team-sync-2026-11-12"}'
```

Response:

```json
{
  "uid": "team-sync-2026-11-12",
  "title": "Team sync",
  "start": "2026-11-12T09:00:00+03:00",
  "end": "2026-11-12T09:30:00+03:00",
  "allDay": false,
  "calendarPath": "/calendars/user@yandex.ru/events/",
  "status": 201,
  "ok": true,
  "note": "Event created"
}
```

---

Template maintained in the [Bowhard n8n templates](https://github.com/VavilkinAlex/n8n-bowhard-templates) repository.
