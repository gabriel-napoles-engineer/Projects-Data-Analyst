# QuickCapture de inspecciones

Se implementaron tres aplicaciones de **ArcGIS QuickCapture** para realizar registros de inspección, una por cada sede:

* Ciudad de México
* Guadalajara
* Monterrey

Estas aplicaciones fueron utilizadas por personal autorizado para registrar inspecciones operativas dentro de las sedes.

## Información registrada

Los registros podían incluir:

* Personal responsable
* Corporación
* Fecha y hora
* Ubicación geográfica
* Sede
* Tipo de inspección
* Observaciones
* Información adicional

## Flujo

```text
Personal autorizado
        │
        ▼
ArcGIS QuickCapture
        │
        ▼
Registro de inspección
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

Los registros de inspección utilizaban la misma infraestructura general del sistema, pero se almacenaban en campos destinados específicamente a este tipo de información.

## Evidencias

Las capturas sanitizadas se encuentran en:

```text
/screenshots/quickcapture/
```

Las evidencias publicadas no contienen datos personales, coordenadas reales ni información operativa sen

