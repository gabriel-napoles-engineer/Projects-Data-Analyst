# Incident QuickCapture

Three **ArcGIS QuickCapture** applications were implemented, one for each host city:

* Mexico City
* Guadalajara
* Monterrey

Their purpose was to allow operational personnel to quickly record medical assistance cases and emergency incidents that occurred during operations.

## Recorded Information

Each record could include:

* Responsible personnel
* Organization
* Date and time
* Geographic location
* Altitude
* Incident type
* Host city
* Comments or additional information

## Workflow

```text
Operational Personnel
        │
        ▼
ArcGIS QuickCapture
        │
        ▼
Incident Record
        │
        ▼
Feature Layer ES
        │
        ▼
Webhook
        │
        ▼
Make
```

Each QuickCapture application was associated with its own webhook and automation scenario.

## Evidence

Sanitized screenshots of the applications are available at:

```text
/screenshots/quickcapture/
```

The published evidence does not contain personal data, real coordinates, or identifiable medical information.
