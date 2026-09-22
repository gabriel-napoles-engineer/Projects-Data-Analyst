# Make Workflow

This document describes the scenario developed in **Make** to automate the prefill process for emergency service reports.

## Scenario Flow

```text
Check Inbox
    ↓
Mark as Read
    ↓
AI Extraction
    ↓
Search Rows
    ↓
Set Variables
    ↓
Add a Row
    ↓
Send an Email
```

## 1. Check Inbox

The scenario periodically checks the email inbox for unread messages from **Active911**.

The scenario runs approximately every **45 minutes**.

## 2. Mark as Read

When a valid email is identified, the message is marked as read to prevent it from being processed again during subsequent executions.

## 3. AI Extraction

The email content is sent to an artificial intelligence model.

The model analyzes the message and returns the incident information in JSON format.

```json
{
  "correo": "",
  "estacion": "",
  "active911": "",
  "Cecom": "",
  "calle": "",
  "Colonia": "",
  "Incidente": "",
  "giro": "",
  "Unidades": ""
}
```

## 4. Search Rows

The **Search Rows** module retrieves the latest available personnel and resource status record.

This information provides data related to:

* Operational personnel on duty.
* Active units.
* Personnel assigned to each unit.
* Corresponding station.

## 5. Set Variables

The **Set Variables** module organizes the information obtained from
