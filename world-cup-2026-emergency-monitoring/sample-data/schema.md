# Data Schema

This folder contains sanitized examples of the records used by the system.

The available files are:

* `incidents-sample.json` — Example of an incident record.
* `inspections-sample.json` — Example of an inspection record.

## Main Fields

| Field            | Description                                  |
| ---------------- | -------------------------------------------- |
| `Fecha`          | Record date and time                         |
| `Nombre`         | Personnel identifier or name                 |
| `Corporacion`    | Organization the operator belongs to         |
| `Sede`           | Host city where the record was generated     |
| `Latitud`        | Geographic coordinate                        |
| `Longitud`       | Geographic coordinate                        |
| `Altitud`        | Altitude recorded by the device              |
| `Tipo_Incidente` | Incident classification                      |
| `Comentarios`    | Additional information related to the record |

## Medical Fields

Medical assistance records may include additional fields such as:

* Patient age
* Medical assistance summary
* Vital signs
* Treatment
* Hospital transfer
* Emergency category
* Nationality
* Location of medical assistance

## Inspections

Inspection records use the same general structure while incorporating specific fields related to:

* Inspection type
* Identified risks
* Observations

## Privacy

All files included in this folder use fictional or previously sanitized information.

Personal data, real medical information, sensitive coordinates, and production identifiers are not included.
