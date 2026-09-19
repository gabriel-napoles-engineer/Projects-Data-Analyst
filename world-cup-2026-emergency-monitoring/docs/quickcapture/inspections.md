# Inspection QuickCapture

Three **ArcGIS QuickCapture** applications were implemented for inspection records, one for each host city:

* Mexico City
* Guadalajara
* Monterrey

These applications were used by authorized personnel to record operational inspections within the host cities.

## Recorded Information

Records could include:

* Responsible personnel
* Organization
* Date and time
* Geographic location
* Host city
* Inspection type
* Observations
* Additional information

## Workflow

```text
Authorized Personnel
        │
        ▼
ArcGIS QuickCapture
        │
        ▼
Inspection Record
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

Inspection records used the same general system infrastructure but were stored in fields specifically designated for this type of information.

## Evidence

Sanitized screenshots are available at:

```text
/screenshots/quickcapture/
```

The published evidence does not contain personal data, real coordinates, or sensitive operational information.
