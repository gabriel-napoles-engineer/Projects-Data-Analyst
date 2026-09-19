# World Cup 2026 Emergency Monitoring

Geospatial system for the registration, processing, visualization, and notification of medical assistance cases, emergency incidents, and operational inspections during the FIFA World Cup 2026 in Mexico.

The solution was implemented for the following host cities:

* Mexico City
* Guadalajara
* Monterrey

## Objective

Enable operational personnel to report incidents from mobile devices and centralize the information in near real time for visualization and monitoring.

The system also generated an English version of the information and sent automated notifications to authorized personnel.

## General Architecture

The main system workflow was:

```text
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
        ├──► Gemini ──► English Translation
        ├──► ArcGIS REST API ──► Feature Layer EN
        │                              │
        │                              ▼
        │                         Web Map EN
        │                              │
        │                              ▼
        │                        Dashboard EN
        │
        └──► WhatsApp
```

## Implemented Components

* 3 QuickCapture applications for incident reporting.
* 3 QuickCapture applications for inspections.
* 6 webhooks.
* 6 automation scenarios in Make.
* 2 main Feature Layers.
* 2 Web Maps.
* 2 ArcGIS Dashboards.
* Automated Spanish-to-English translation.
* Integration through the ArcGIS REST API.
* Notifications through WhatsApp.

## Technologies Used

* ArcGIS Online
* ArcGIS QuickCapture
* ArcGIS Feature Layers
* ArcGIS Web Maps
* ArcGIS Dashboards
* ArcGIS REST API
* Make
* Google Sheets
* Gemini
* WhatsApp

## Repository Structure

```text
docs/
├── architecture/
├── quickcapture/
├── automation/
├── dashboards/
└── security/

screenshots/
├── quickcapture/
├── dashboards/
├── maps/
└── make/

sample-data/
diagrams/
```

Technical documentation is available in the [`docs/`](docs/) directory.

## Documentation

* [`Architecture and Data Flow`](docs/architecture/data-flow.md)
* [`Incident QuickCapture`](docs/quickcapture/incidents.md)
* [`Inspection QuickCapture`](docs/quickcapture/inspections.md)
* [`Make Automation`](docs/automation/make-workflow.md)
* [`Translation Workflow`](docs/automation/translation-workflow.md)
* [`Dashboards`](docs/dashboards/dashboards.md)
* [`Data Privacy and Security`](docs/security/data-privacy.md)

## Security and Privacy

This repository contains only technical documentation, diagrams, sanitized screenshots, and fictional data.

It does not include:

* Personal data.
* Real medical information.
* Real incident coordinates.
* Phone numbers.
* Credentials.
* Tokens.
* API keys.
* Real webhooks.
* Private endpoints.
* Production service URLs.
* Original databases.

The data included in `sample-data/` is provided for demonstration purposes only.

## Scope

This repository documents the architecture and methodology used during the development of the system.

It does not contain the production infrastructure or sufficient information to access the services used during the original implementation.
