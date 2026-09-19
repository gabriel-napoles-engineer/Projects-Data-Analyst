# Automation with Make

Make was used as the integration platform to automatically process records generated from ArcGIS QuickCapture.

Six scenarios were implemented:

* 3 for incidents.
* 3 for inspections.

Each QuickCapture application used its own webhook and scenario.

## General Workflow

```text
Webhook
   │
   ▼
  Make
   │
   ├──► Google Sheets
   │
   ├──► Gemini
   │
   ├──► ArcGIS REST API
   │
   └──► WhatsApp
```

## Process

1. The webhook receives the new record from QuickCapture.
2. Make processes the received information.
3. The data is stored in Google Sheets.
4. The required fields are sent to Gemini for translation.
5. Make builds the English version of the record.
6. The translated record is sent through the ArcGIS REST API.
7. The information is stored in the English Feature Layer.
8. The configured notifications are sent through WhatsApp.

## Evidence

Sanitized screenshots of the scenarios are available at:

```text
/screenshots/make/
```

Webhooks, tokens, credentials, connection IDs, and real endpoints are not published.
