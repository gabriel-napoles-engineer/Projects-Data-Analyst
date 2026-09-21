# Data Flow

Este documento describe el flujo de información utilizado para generar enlaces prellenados de reportes de servicios de emergencia.

## Flujo general

```text
Active911
    ↓
Correo electrónico de alarma
    ↓
Make
    ↓
Detección de correo no leído
    ↓
Procesamiento con IA
    ↓
Extracción de datos del incidente
    ↓
Consulta del último estado de fuerza
    ↓
Asignación de variables
    ↓
Generación del enlace Survey123
    ↓
Registro de información
    ↓
Envío del enlace a la estación correspondiente
```

## 1. Generación de la alarma

Cuando se genera un servicio de emergencia en **Active911**, la plataforma envía automáticamente un correo electrónico con la información disponible del incidente.

## 2. Detección del correo

Un escenario en **Make** revisa periódicamente el buzón de correo.

Cuando identifica un mensaje nuevo proveniente de Active911:

* Verifica que no haya sido procesado.
* Lo marca como leído.
* Envía su contenido al módulo de inteligencia artificial.

## 3. Extracción de información

El modelo de IA interpreta el contenido del correo y genera una estructura JSON con los principales datos del servicio.

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

## 4. Consulta del estado de fuerza

Mediante un módulo **Search Rows**, el escenario consulta el último estado de fuerza correspondiente a la estación.

De esta fuente se obtiene información relacionada con:

* Personal operativo en turno.
* Unidades activas.
* Asignación del personal a las unidades.

## 5. Preparación de variables

El módulo **Set Variables** organiza la información obtenida del correo y del estado de fuerza para utilizarla en los siguientes pasos del escenario.

## 6. Generación del formulario prellenado

Los datos procesados se incorporan como parámetros dentro de la URL de **ArcGIS Survey123**.

Ejemplo:

```text
https://survey123.arcgis.com/share/XXXX?field:correo_electr_nico=example@gmail.com&field:folio_active_911=000010
```

De esta forma, los campos correspondientes se cargan automáticamente cuando el personal abre el formulario.

## 7. Registro de información

Mediante **Add a Row**, el escenario almacena la información procesada junto con el enlace generado para el reporte de servicio.

## 8. Envío a la estación

Finalmente, el módulo **Send an Email** envía el enlace prellenado a la estación correspondiente.

El personal operativo abre el formulario y completa principalmente la descripción de las actividades realizadas durante el servicio.

## Resultado

El flujo integra automáticamente la información de **Active911** y del **estado de fuerza**, reduciendo aproximadamente un **80 %** del llenado manual requerido para generar los reportes de servicios de emergencia.

