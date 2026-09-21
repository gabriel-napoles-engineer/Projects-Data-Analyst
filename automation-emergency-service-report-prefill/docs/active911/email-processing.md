# Email Processing

Este documento describe cómo se procesa el correo generado por **Active911** dentro del flujo de automatización.

## Origen del correo

Cada vez que se genera una alarma en **Active911**, la plataforma envía automáticamente un correo electrónico con la información disponible del incidente.

Este correo funciona como fuente de datos para iniciar el proceso de prellenado del reporte de servicio.

## Detección en Make

El escenario en **Make** revisa periódicamente el buzón de correo.

La revisión se ejecuta aproximadamente cada **45 minutos** y busca mensajes no leídos provenientes de la dirección utilizada por Active911.

Cuando se encuentra un correo nuevo:

1. Se identifica como pendiente de procesamiento.
2. Se marca como leído.
3. Su contenido se envía al módulo de inteligencia artificial.

## Procesamiento con IA

El modelo de IA analiza el contenido del correo y extrae la información relevante del servicio.

El resultado se estructura en formato JSON:

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

## Campos extraídos

| Campo      | Descripción                          |
| ---------- | ------------------------------------ |
| `correo`   | Correo asociado al reporte           |
| `estacion` | Estación correspondiente al servicio |
| `acti      |                                      |

