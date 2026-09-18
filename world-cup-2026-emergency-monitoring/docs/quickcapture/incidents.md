# QuickCapture de incidentes

Se implementaron tres aplicaciones de **ArcGIS QuickCapture**, una para cada sede:

* Ciudad de México
* Guadalajara
* Monterrey

Su objetivo fue permitir al personal operativo registrar de forma rápida las atenciones médicas e incidentes de emergencia ocurridos durante la operación.

## Información registrada

Cada marcaje podía incluir:

* Personal responsable
* Corporación
* Fecha y hora
* Ubicación geográfica
* Altitud
* Tipo de incidente
* Sede
* Comentarios o información adicional

## Flujo

```text
Personal operativo
        │
        ▼
ArcGIS QuickCapture
        │
        ▼
Registro del incidente
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

Cada QuickCapture estaba asociado a su propio webhook y escenario de automatización.

## Evidencias

Las capturas sanitizadas de las aplicaciones se encuentran en:

```text
/screenshots/quickcapture/
```

Las evidencias publicadas no contienen datos personales, coordenadas reales ni información médica identificable.

