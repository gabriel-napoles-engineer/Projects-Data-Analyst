# Emergency Service Report Prefill

Este repositorio documenta una solución desarrollada para automatizar el prellenado de reportes de servicios de emergencia de Bomberos Querétaro.

El objetivo principal es reducir el tiempo que el personal operativo dedica a recopilar información desde diferentes plataformas antes de completar un reporte de servicio.

## Descripción

Cada servicio de emergencia es despachado mediante **Active911**, plataforma que contiene la información inicial del incidente.

Cuando se genera una alarma, Active911 envía automáticamente un correo electrónico con los datos del servicio. Un escenario desarrollado en **Make** procesa esta información y la combina con el último **estado de fuerza** registrado por la estación correspondiente.

Posteriormente, se genera un enlace de **ArcGIS Survey123** con campos previamente llenados, permitiendo que el personal operativo únicamente complete la información relacionada con las actividades realizadas durante la atención del servicio.

## Flujo general

```text
Active911
    ↓
Correo de alarma
    ↓
Make
    ↓
Procesamiento con IA
    ↓
Extracción de datos del incidente
    ↓
Consulta del estado de fuerza
    ↓
Generación de enlace Survey123
    ↓
Envío del formulario prellenado
    ↓
Personal operativo
```

## Tecnologías utilizadas

* Active911
* Make
* Inteligencia Artificial
* ArcGIS Survey123
* Correo electrónico
* Base de datos de estados de fuerza

## Información procesada

El modelo de IA extrae del correo de Active911 información como:

* Correo
* Estación
* Folio Active911
* Folio CECOM
* Calle
* Colonia
* Incidente
* Giro
* Unidades

Esta información se complementa con los datos del último estado de fuerza disponible.

## Survey123 Prefill

Survey123 permite enviar información directamente a campos específicos mediante parámetros incluidos en la URL del formulario.

Ejemplo:

```text
https://survey123.arcgis.com/share/XXXX?field:correo_electr_nico=example@gmail.com&field:folio_active_911=000010
```

El escenario genera dinámicamente este enlace utilizando la información obtenida durante el proceso.

## Resultado

La implementación permitió automatizar aproximadamente el **80 % del llenado de los reportes de servicios de emergencia**, reduciendo la captura manual y centralizando información que anteriormente debía consultarse en diferentes plataformas.

## Estructura del repositorio

```text
emergency-service-report-prefill/
│
├── README.md
│
├── docs/
├── examples/
└── evidence/
```

La carpeta `docs/` contiene la documentación técnica del flujo, `examples/` incluye ejemplos sanitizados de los datos procesados y `evidence/` contiene evidencia visual del funcionamiento del sistema.

## Privacidad

Los ejemplos y evidencias incluidos en este repositorio deben mantenerse sanitizados.

No se incluyen datos personales, información sensible de emergencias, credenciales, tokens, direcciones reales, correos privados ni configuraciones internas de los sistemas utilizados.

