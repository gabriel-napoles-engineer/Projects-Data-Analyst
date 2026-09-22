# Survey123 Prefilled Form

This document describes how the prefilled link used for emergency service reports is generated in **ArcGIS Survey123**.

## Objective

Prefilling allows incident information to be loaded automatically before operational personnel open the form.

This avoids manually entering data that has already been obtained from **Active911** and the **personnel and resource status** records.

## Link Structure

Survey123 allows values to be assigned to specific fields through parameters included in the URL.

Example:

```text
https://survey123.arcgis.com/share/XXXX?field:correo_electr_nico=example@gmail.com&field:folio_active_911=000010
```

The general structure is:

```text
https://survey123.arcgis.com/share/FORM_ID?field:FIELD_NAME=VALUE
```

Additional fields are added using `&`:

```text
?field:campo1=valor1&field:campo2=valor2&field:campo3=valor3
```

## Data Sources

The link is dynamically generated in Make using information from two main sources.

### Active911

Data extracted from the email using the AI model, including:

* Email
* Station
* Active911 reference number
* CECOM reference number
* Street
* Neighborhood
* Incident
* Incident category
* Units

### Personnel and Resource Status

Information obtained from the latest available record, including:

* Personnel on duty
* Active units
* Personnel assignments
* Station

## Generation in Make

The values obtained during the workflow are converted into variables and then inserted into the Survey123 URL.

Simplified example:

```text
https://survey123.arcgis.com/share/XXXX
?field:folio_active_911={{active911}}
&field:calle={{calle}}
&field:colonia={{Colonia}}
&field:incidente={{Incidente}}
```

The resulting link is stored together with the processed information and is then sent by email to the corresponding station.

## Result

When operational personnel open the link, Survey123 automatically populates the available fields with the service information.

The user only needs to review the data and complete the information that cannot be generated automatically, mainly the description of the activities performed during the emergency response.

## Considerations

The names used in `field:` must exactly match the internal field names configured in Survey123.

Special characters, spaces, and values that could affect the URL structure must also be properly encoded.
