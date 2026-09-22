# Database Structure

Google Sheets is used as the main database to store participant information and manage the automated certificate generation process.

Each row represents an individual certificate.

## Column Structure

| Column                      | Description                                                                                          |
| --------------------------- | ---------------------------------------------------------------------------------------------------- |
| `FOLIO`                     | Unique identifier assigned to the certificate.                                                       |
| `NOMBRE`                    | Participant's full name.                                                                             |
| `EMPRESA`                   | Company or organization to which the participant belongs.                                            |
| `CORREO`                    | Email address associated with the participant.                                                       |
| `CURSO`                     | Name of the completed course.                                                                        |
| `HORAS`                     | Course duration in hours.                                                                            |
| `INSTRUCTOR`                | Name of the instructor responsible for the course.                                                   |
| `FECHA`                     | Date on which the course was completed or accredited.                                                |
| `VIGENCIA`                  | Certificate expiration date or validity period.                                                      |
| `Fecha Ultimo envio`        | Records the date of the most recent delivery performed by the system.                                |
| `Evidencia`                 | Stores the reference or URL of the validation document generated in Google Drive.                    |
| `QR`                        | Stores the information or reference for the QR code generated from the validation document URL.      |
| `Constancia`                | Stores the reference or URL of the generated certificate.                                            |
| `Fecha ultima modificacion` | Records the most recent date on which the entry was modified.                                        |
| `Generar Carpeta`           | Control field used to trigger the creation of the corresponding folder or structure in Google Drive. |
| `FALSE`                     | Auxiliary field used by the automation process as a Boolean control value.                           |

## Main Data Fields

The fields used directly to generate the documentation are:

```text
FOLIO
NOMBRE
EMPRESA
CORREO
CURSO
HORAS
INSTRUCTOR
FECHA
VIGENCIA
```

These fields represent the original information recorded for each participant.

## Automation Fields

During Google Apps Script execution, additional fields are generated or updated:

```text
Fecha Ultimo envio
Evidencia
QR
Constancia
Fecha ultima modificacion
Generar Carpeta
```

These fields allow the script to track the current process status and retain references to the generated documents.

## Relationship with Generated Documents

The Google Sheets record serves as the central source of information:

```text
Google Sheets
     │
     ├── Participant data
     │
     ├── Unique certificate number
     │
     └── Course information
             ↓
      Google Apps Script
             │
             ├── Validation document
             ├── Validation document URL
             ├── QR code
             └── Certificate
```

The same `FOLIO` is used in both the certificate and the validation document, allowing both documents to be linked to the same record.

## Considerations

The production spreadsheet contains personal information, so any examples published in this repository must use only fictional or sanitized data.

The following information must not be published:

* Real participant names
* Real email addresses
* Private Google Drive URLs
* Certificate numbers associated with real certificates
* Private file or folder IDs
* Credentials or sensitive configuration data
