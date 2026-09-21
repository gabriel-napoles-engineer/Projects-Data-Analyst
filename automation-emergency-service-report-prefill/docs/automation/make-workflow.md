# Make Workflow

Este documento describe el escenario desarrollado en **Make** para automatizar el prellenado de reportes de servicios de emergencia.

## Flujo del escenario

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

El escenario revisa periódicamente el buzón de correo en busca de mensajes no leídos provenientes de **Active911**.

La ejecución se realiza aproximadamente cada **45 minutos**.

## 2. Mark as Read

Cuando se identifica un correo válido, el mensaje se marca como leído para evitar que vuelva a ser procesado en ejecuciones posteriores.

## 3. AI Extraction

El contenido del correo se envía a un modelo de inteligencia artificial.

El modelo analiza el mensaje y devuelve la información del incidente en formato JSON.

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

El módulo **Search Rows** consulta el último estado de fuerza disponible.

Esta información permite obtener datos relacionados con:

* Personal operativo en turno.
* Unidades activas.
* Asignación de personal por unidad.
* Estación correspondiente.

## 5. Set Variables

El módulo **Set Variables** organiza la información obtenida del correo y del estado de fuerza en variables reutilizables.

Estas variables se utilizan para construir el registro y el enlace prellenado de Survey123.

## 6. Add a Row

El módulo **Add a Row** registra la información procesada y genera el enlace correspondiente al formulario de Survey123.

El enlace incluye parámetros para prellenar automáticamente los campos disponibles.

Ejemplo:

```text
https://survey123.arcgis.com/share/XXXX?field:correo_electr_nico=example@gmail.com&field:folio_active_911=000010
```

## 7. Send an Email

Finalmente, el escenario envía un correo electrónico a la estación correspondiente.

El mensaje contiene el enlace al formulario de **Survey123** con la información previamente cargada.

## Resultado

El escenario integra datos provenientes de **Active911** y del **estado de fuerza** para generar automáticamente un formulario prellenado.

Esto reduce aproximadamente un **80 %** del trabajo manual requerido para completar los reportes de servicios de emergencia.

