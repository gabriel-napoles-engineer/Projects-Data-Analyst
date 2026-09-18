# Flujo de traducción

El sistema generaba una versión en inglés de los registros capturados originalmente en español.

La traducción se realizaba dentro de los escenarios de Make mediante un módulo de **Gemini**.

## Flujo

```text
Registro en español
        │
        ▼
       Make
        │
        ▼
      Gemini
        │
        ▼
Campos traducidos
        │
        ▼
Reconstrucción del registro
        │
        ▼
ArcGIS REST API
        │
        ▼
Feature Layer EN
```

## Proceso

1. Make recibe el registro original.
2. Se identifican los campos que requieren traducción.
3. Los campos seleccionados se envían a Gemini.
4. Gemini devuelve la información en inglés.
5. Make combina los campos traducidos con los datos que no requieren modificación.
6. El nuevo registro se envía a ArcGIS mediante REST API.
7. La información se almacena en la Feature Layer en inglés.

Los datos estructurales, como coordenadas, fechas, horas e identificadores, se conservan sin traducción.

## Resultado

El sistema mantiene dos versiones equivalentes de la información:

```text
Feature Layer ES
        │
        └──► Información original

Feature Layer EN
        │
        └──► Información traducida
```

No se incluyen prompts reales, credenciales, tokens ni configuraciones de producción.

