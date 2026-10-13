# n8n workflow templates (demo projects)

Two importable n8n workflows that cover the patterns most small-business automation jobs ask for.
Import: n8n → Workflows → Import from file → pick the JSON → set the credentials marked `PASTE_...`.

## 1. `lead-form-to-sheets-telegram.json`
**Website form → validate → Google Sheets row → Telegram alert → JSON response**

- Webhook `POST /webhook/lead` accepts `{name, email, phone, message, source}`.
- Normalizes fields (trim, lowercase email, strip spaces in phone, timestamp).
- Rejects invalid emails with HTTP 400, appends valid leads to a sheet named `Leads`, pings Telegram.
- Swap Telegram for WhatsApp (Twilio/Meta), Slack or email by replacing one node.

Test with:
```bash
curl -X POST http://localhost:5678/webhook/lead -H "Content-Type: application/json" \
  -d '{"name":"Test Client","email":"test@example.com","phone":"+32 470 00 00 00","message":"Hello","source":"demo"}'
```

## 2. `api-monitor-to-slack.json`
**Schedule → fetch any REST API → compare with last run → alert only on change**

- Runs weekdays at 17:00, calls a public API (no key needed for the demo).
- Keeps the previous values in workflow static data, flags moves above a threshold.
- Posts to a Slack or Discord incoming webhook only when something changed.
- Same skeleton serves: supplier price lists, stock levels, order counts, competitor prices.

## For the Upwork portfolio
Open each workflow in n8n, run it once, take a screenshot of the canvas with green execution ticks, and upload it as the portfolio image. Describe both as demo projects.
