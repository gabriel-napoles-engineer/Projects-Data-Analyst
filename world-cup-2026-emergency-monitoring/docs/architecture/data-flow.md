# Data Flow

The system processes each record from field capture through visualization and notification.

## Main Flow

```text
Operational Personnel
        │
        ▼
ArcGIS QuickCapture
        │
        ▼
Feature Layer ES
        │
        ├──► Web Map ES ──► Dashboard ES
        │
        ▼
     Webhook
        │
        ▼
       Make
        │
        ├──► Google Sheets
        ├──► Gemini
        │       │
        │       ▼
        │  EN Translation
        │       │
        │       ▼
        │  ArcGIS REST API
        │       │
        │       ▼
        │ Feature Layer EN
        │       │
        │       ▼
        │   Web Map EN
        │       │
        │       ▼
        │ Dashboard EN
        │
        └──► WhatsApp
```

## Sequence

1. Operational personnel record an incident or inspection using QuickCapture.
2. The information is stored in the Spanish Feature Layer.
3. The record triggers a webhook.
4. Make receives and processes the information.
5. The data is recorded in Google Sheets.
6. The required fields are translated into English using Gemini.
7. Make sends the translated record to ArcGIS through the REST API.
8. The information is stored in the English Feature Layer.
9. Both layers feed their respective Web Maps and Dashboards.
10. Make sends the configured notifications through WhatsApp.

## Distribution by Host City

The same workflow was used for all three host cities:

* Mexico City.
* Guadalajara.
* Monterrey.

Each host city used one QuickCapture application for incidents and one for inspections, each with its own webhook and Make scenario.

## Note

This document represents the general system workflow. Production endpoints, tokens, webhooks, credentials, and real production data are not included.
