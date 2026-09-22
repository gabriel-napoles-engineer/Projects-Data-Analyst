# Emergency Service Report Prefill

This repository documents a solution developed to automate the prefill process for emergency service reports used by Bomberos Querétaro.

The main objective is to reduce the time operational personnel spend collecting information from different platforms before completing a service report.

## Description

Each emergency service is dispatched through **Active911**, a platform that contains the initial incident information.

When an alarm is generated, Active911 automatically sends an email containing the service details. A scenario developed in **Make** processes this information and combines it with the latest **personnel and resource status** submitted by the corresponding station.

An **ArcGIS Survey123** link is then generated with predefined fields already completed, allowing operational personnel to enter only the information related to the activities performed during the emergency response.

## General Flow

```text
Active911
    ↓
Alarm email
    ↓
Make
    ↓
AI processing
    ↓
Incident data extraction
    ↓
Personnel and resource status lookup
    ↓
Survey123 link generation
    ↓
Prefilled form delivery
    ↓
Operational personnel
```

## Technologies Used

* Active911
* Make
* Artificial Intelligence
* ArcGIS Survey123
* Email
* Personnel and resource status database

## Processed Information

The AI model extracts information from the Active911 email such as:

* Email
* Station
* Active911 reference number
* CECOM reference number
* Street
* Neighborhood
* Incident
* Incident category
* Units

This information is combined with the data from the latest available personnel and resource status record.

## Survey123 Prefill

Survey123 allows information to be passed directly into specific fields using parameters included in the form URL.

Example:

```text
https://survey123.arcgis.com/share/XXXX?field:correo_electr_nico=example@gmail.com&field:folio_active_911=000010
```

The scenario dynamically generates this link using the information obtained during the process.

## Result

The implementation automated approximately **80% of the emergency service report completion process**, reducing manual data entry and centralizing information that previously had to be retrieved from multiple platforms.

## Repository Structure

```text
emergency-service-report-prefill/
│
├── README.md
│
├── docs/
├── examples/
└── evidence/
```

The `docs/` directory contains the technical workflow documentation, `examples/` includes sanitized examples of the processed data, and `evidence/` contains visual evidence of the system's operation.

## Privacy

All examples and evidence included in this repository must remain sanitized.

The repository does not include personal data, sensitive emergency information, credentials, tokens, real addresses, private email addresses, or internal system configurations.
