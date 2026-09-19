# Translation Workflow

The system generated an English version of the records originally captured in Spanish.

Translation was performed within the Make scenarios using a **Gemini** module.

## Workflow

```text
Record in Spanish
        │
        ▼
       Make
        │
        ▼
      Gemini
        │
        ▼
Translated Fields
        │
        ▼
Record Reconstruction
        │
        ▼
ArcGIS REST API
        │
        ▼
Feature Layer EN
```

## Process

1. Make receives the original record.
2. The fields that require translation are identified.
3. The selected fields are sent to Gemini.
4. Gemini returns the information in English.
5. Make combines the translated fields with the data that does not require modification.
6. The new record is sent to ArcGIS through the REST API.
7. The information is stored in the English Feature Layer.

Structural data, such as coordinates, dates, times, and identifiers, is preserved without translation.

## Result

The system maintains two equivalent versions of the information:

```text
Feature Layer ES
        │
        └──► Original Information

Feature Layer EN
        │
        └──► Translated Information
```

Real prompts, credentials, tokens, and production configurations are not included.
