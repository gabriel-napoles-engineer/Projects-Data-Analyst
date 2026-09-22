# Data Flow

This document describes the information flow used to generate prefilled links for emergency service reports.

## General Flow

```text
Active911
    ↓
Alarm email
    ↓
Make
    ↓
Unread email detection
    ↓
AI processing
    ↓
Incident data extraction
    ↓
Latest personnel and resource status lookup
    ↓
Variable assignment
    ↓
Survey123 link generation
    ↓
Information logging
    ↓
Link delivery to the corresponding station
```

## 1. Alarm Generation

When an emergency service is generated in **Active911**, the platform automatically sends an email containing the available incident information.

## 2. Email Detection

A scenario in **Make** periodically checks the email inbox.

When it identifies a new message from Active911:

* It verifies that the message has not already been processed.
* It marks the message as read.
* It sends the content to the artificial intelligence module.

## 3. Information Extraction

The AI model interprets the email content and generates a JSON structure containing the main service information.

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

## 4. Personnel and Resource Status Lookup

Using a **Search Rows** module, the scenario retrieves the latest personnel and resource status record corresponding to the station.

This source provides information related to:

* Operational personnel on duty.
* Active units.
* Personnel assigned to each unit.

## 5. Variable Preparation

The **Set Variables** module organizes the information obtained from the email and the personnel and resource status record so it can be used in the following steps of the scenario.

## 6. Prefilled Form Generation

The processed data is added as parameters to the **ArcGIS Survey123** URL.

Example:

```text
https://survey123.arcgis.com/share/XXXX?field:correo_electr_nico=example@gmail.com&field:folio_active_911=000010
```

This allows the corresponding fields to be populated automatically when operational personnel open the form.

## 7. Information Logging

Using **Add a Row**, the scenario stores the processed information together with the generated link for the service report.

## 8. Delivery to the Station

Finally, the **Send an Email** module sends the prefilled link to the corresponding station.

Operational personnel open the form and mainly complete the description of the activities performed during the emergency response.

## Result

The workflow automatically integrates information from **Active911** and the **personnel and resource status** records, reducing the manual data entry required to generate emergency service reports by approximately **80%**.
