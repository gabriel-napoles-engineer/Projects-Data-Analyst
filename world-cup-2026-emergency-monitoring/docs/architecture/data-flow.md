# Flujo de datos

El sistema procesa cada registro desde su captura en campo hasta su visualización y notificación.

## Flujo principal

```text
Personal operativo
        │
        ▼
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
        ├──► Gemini
        │       │
        │       ▼
        │   Traducción EN
        │       │
        │       ▼
        │  ArcGIS REST API
        │       │
        │       ▼
        │ Feature Layer EN
        │       │
        │       ▼
        │   Web Map EN
        │       │
        │       ▼
        │ Dashboard EN
        │
        └──► WhatsApp
```

## Secuencia

1. El personal registra un incidente o inspección mediante QuickCapture.
2. La información se almacena en la Feature Layer en español.
3. El registro activa un webhook.
4. Make recibe y procesa la información.
5. Los datos se registran en Google Sheets.
6. Los campos necesarios se traducen al inglés mediante Gemini.
7. Make envía el registro traducido a ArcGIS mediante REST API.
8. La información se almacena en la Feature Layer en inglés.
9. Ambas capas alimentan sus respectivos Web Maps y Dashboards.
10. Make envía las notificaciones configuradas mediante WhatsApp.

## Distribución por sede

El mismo flujo se utilizó para las tres sedes:

* Ciudad de México.
* Guadalajara.
* Monterrey.

Cada sede utilizó un QuickCapture de incidentes y uno de inspecciones, cada uno con su propio webhook y escenario de Make.

Nota

Este documento representa el flujo general del sistema. No se incluyen endpoints, tokens, webhooks, credenciales ni datos reales de producción.

