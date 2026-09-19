# Esquema de datos

Esta carpeta contiene ejemplos sanitizados de los registros utilizados por el sistema.

Los archivos disponibles son:

* `incidents-sample.json` — Ejemplo de registro de incidente.
* `inspections-sample.json` — Ejemplo de registro de inspección.

## Campos principales

| Campo            | Descripción                                |
| ---------------- | ------------------------------------------ |
| `Fecha`          | Fecha y hora del registro                  |
| `Nombre`         | Identificador o nombre del personal        |
| `Corporacion`    | Corporación a la que pertenece el operador |
| `Sede`           | Sede donde se genera el registro           |
| `Latitud`        | Coordenada geográfica                      |
| `Longitud`       | Coordenada geográfica                      |
| `Altitud`        | Altitud registrada por el dispositivo      |
| `Tipo_Incidente` | Clasificación del incidente                |
| `Comentarios`    | Información adicional del registro         |

## Campos médicos

Los registros de atención pueden incluir campos adicionales como:

* Edad del paciente
* Resumen de atención
* Signos vitales
* Tratamiento
* Traslado hospitalario
* Categoría de urgencia
* Nacionalidad
* Ubicación de la atención

## Inspecciones

Los registros de inspección utilizan la misma estructura general, incorporando campos específicos relacionados con:

* Tipo de inspección
* Riesgos identificados
* Observaciones

## Privacidad

Todos los archivos incluidos en esta carpeta utilizan información ficticia o previamente sanitizada.

No se incluyen datos personales, información médica real, coordenadas sensibles ni identificadores de producción.

