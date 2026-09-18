# World Cup 2026 Emergency Monitoring

Sistema geoespacial para el registro, procesamiento, visualización y notificación de atenciones médicas, incidentes de emergencia e inspecciones operativas durante el Mundial de la FIFA 2026 en México.

La solución fue implementada para las sedes de:

* Ciudad de México
* Guadalajara
* Monterrey

## Objetivo

Permitir al personal operativo registrar incidentes desde dispositivos móviles y concentrar la información prácticamente en tiempo real para su visualización y seguimiento.

El sistema también generaba una versión de la información en inglés y enviaba notificaciones automáticas al personal autorizado.

## Arquitectura general

El flujo principal del sistema fue:

```text
ArcGIS QuickCapture
        │
        ▼
Feature Layer ES
        │
        ├──► Web Map ES ──► Dashboard ES
        │
        ▼
     Webhook
        │
        ▼
       Make
        │
        ├──► Google Sheets
        ├──► Gemini ──► Traducción al inglés
        ├──► ArcGIS REST API ──► Feature Layer EN
        │                              │
        │                              ▼
        │                         Web Map EN
        │                              │
        │                              ▼
        │                        Dashboard EN
        │
        └──► WhatsApp
```

## Componentes implementados

* 3 QuickCapture para registro de incidentes.
* 3 QuickCapture para inspecciones.
* 6 webhooks.
* 6 escenarios de automatización en Make.
* 2 Feature Layers principales.
* 2 Web Maps.
* 2 ArcGIS Dashboards.
* Traducción automatizada español-inglés.
* Integración mediante ArcGIS REST API.
* Notificaciones mediante WhatsApp.

## Tecnologías utilizadas

* ArcGIS Online
* ArcGIS QuickCapture
* ArcGIS Feature Layers
* ArcGIS Web Maps
* ArcGIS Dashboards
* ArcGIS REST API
* Make
* Google Sheets
* Gemini
* WhatsApp

## Estructura del repositorio

```text
docs/
├── architecture/
├── quickcapture/
├── automation/
├── dashboards/
└── security/

screenshots/
├── quickcapture/
├── dashboards/
├── maps/
└── make/

sample-data/
diagrams/
```

La documentación técnica se encuentra dentro de la carpeta [`docs/`](docs/).

## Documentación

* [`Arquitectura y flujo de datos`](docs/architecture/data-flow.md)
* [`QuickCapture de incidentes`](docs/quickcapture/incidents.md)
* [`QuickCapture de inspecciones`](docs/quickcapture/inspections.md)
* [`Automatización con Make`](docs/automation/make-workflow.md)
* [`Flujo de traducción`](docs/automation/translation-workflow.md)
* [`Dashboards`](docs/dashboards/dashboards.md)
* [`Privacidad y seguridad`](docs/security/data-privacy.md)

## Seguridad y privacidad

Este repositorio contiene únicamente documentación técnica, diagramas, capturas sanitizadas y datos ficticios.

No se incluyen:

* Datos personales.
* Información médica real.
* Coordenadas reales de incidentes.
* Números telefónicos.
* Credenciales.
* Tokens.
* API keys.
* Webhooks reales.
* Endpoints privados.
* URLs de servicios de producción.
* Bases de datos originales.

Los datos incluidos en `sample-data/` tienen únicamente fines demostrativos.

## Alcance

Este repositorio documenta la arquitectura y metodología utilizada durante el desarrollo del sistema.

No contiene la infraestructura de producción ni información suficiente para acceder a los servicios utilizados durante la implementación original.

