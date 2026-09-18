# Automatización con Make

Make fue utilizado como plataforma de integración para procesar automáticamente los registros generados desde ArcGIS QuickCapture.

Se implementaron seis escenarios:

* 3 para incidentes.
* 3 para inspecciones.

Cada QuickCapture utilizaba su propio webhook y escenario.

## Flujo general

```text
Webhook
   │
   ▼
  Make
   │
   ├──► Google Sheets
   │
   ├──► Gemini
   │
   ├──► ArcGIS REST API
   │
   └──► WhatsApp
```

## Proceso

1. El webhook recibe el nuevo registro desde QuickCapture.
2. Make procesa la información recibida.
3. Los datos se almacenan en Google Sheets.
4. Los campos necesarios se envían a Gemini para su traducción.
5. Make construye el registro en inglés.
6. El registro traducido se envía mediante ArcGIS REST API.
7. La información se almacena en la Feature Layer en inglés.
8. Se generan las notificaciones configuradas mediante WhatsApp.

## Evidencias

Las capturas sanitizadas de los escenarios se encuentran en:

```text
/screenshots/make/
```

No se publican webhooks, tokens, credenciales, IDs de conexiones ni endpoints reales.

