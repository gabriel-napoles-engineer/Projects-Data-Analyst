# Flujo de datos del sistema

## Descripción general

Este documento describe el recorrido de la información desde que un registro es generado por el personal operativo en campo hasta que los datos son almacenados, procesados, traducidos, visualizados y distribuidos mediante los diferentes componentes de la solución.

El flujo fue diseñado para operar de manera automatizada y reducir al mínimo la intervención manual durante el procesamiento de los registros.

La arquitectura general del flujo puede resumirse de la siguiente manera:

```text
QuickCapture
     │
     ▼
Feature Layer ES
     │
     ├──────────────► Web Map ES
     │                    │
     │                    ▼
     │               Dashboard ES
     │
     ▼
  Webhook
     │
     ▼
    Make
     │
     ├──────────────► Google Sheets
     │
     ├──────────────► Gemini
     │                    │
     │                    ▼
     │             Traducción al inglés
     │                    │
     │                    ▼
     │              ArcGIS REST API
     │                    │
     │                    ▼
     │             Feature Layer EN
     │                    │
     │                    ▼
     │                Web Map EN
     │                    │
     │                    ▼
     │              Dashboard EN
     │
     └──────────────► WhatsApp
                           │
                           ▼
                  Personal autorizado
```

---

# 1. Generación del registro

El flujo comienza cuando un integrante del personal operativo utiliza **ArcGIS QuickCapture** para registrar una atención, incidente o inspección.

Cada aplicación QuickCapture contiene botones configurados para representar diferentes tipos de registros.

Cuando el operador selecciona uno de estos botones, la aplicación genera un nuevo evento con los atributos asociados.

Dependiendo de la configuración del registro, la información puede incluir campos como:

* Identificador o nombre del personal.
* Corporación.
* Fecha.
* Hora.
* Latitud.
* Longitud.
* Altitud.
* Tipo de incidente.
* Sede.
* Información operativa adicional.

De forma simplificada:

```text
Personal operativo
        │
        ▼
ArcGIS QuickCapture
        │
        ▼
Nuevo registro
```

---

# 2. Captura geoespacial

Uno de los elementos principales del registro es la información geográfica.

QuickCapture permite asociar automáticamente la ubicación del dispositivo al momento de generar el registro.

Conceptualmente:

```text
Dispositivo móvil
       │
       ▼
Ubicación del dispositivo
       │
       ▼
QuickCapture
       │
       ▼
Coordenadas del registro
```

Esto permite que cada evento pueda posteriormente representarse espacialmente dentro de los Web Maps y Dashboards.

La documentación pública de este repositorio no contiene coordenadas reales de incidentes ni ubicaciones sensibles.

---

# 3. Almacenamiento en Feature Layer ES

Después de generar el registro, la información se almacena en la **Feature Layer en español**.

Esta capa funciona como repositorio geoespacial principal de los datos originales generados desde campo.

```text
QuickCapture
     │
     ▼
Feature Layer ES
```

El registro queda disponible para los servicios de ArcGIS que consumen la información de esta capa.

Entre ellos:

```text
Feature Layer ES
       │
       ▼
   Web Map ES
       │
       ▼
 Dashboard ES
```

Esto permite que los registros generados desde campo puedan reflejarse dentro del entorno de visualización correspondiente.

---

# 4. Activación del webhook

Además del almacenamiento del registro, cada QuickCapture estaba asociado a un webhook encargado de iniciar el proceso de automatización.

El webhook actuaba como mecanismo de integración entre el entorno de captura de ArcGIS y Make.

```text
Nuevo registro
      │
      ▼
   Webhook
      │
      ▼
Make Scenario
```

Cada proyecto QuickCapture disponía de su propio flujo de automatización.

Debido a que se utilizaron seis aplicaciones QuickCapture, la solución contó con seis escenarios de Make.

---

# 5. Separación de flujos por sede

La solución fue implementada para tres sedes:

* Ciudad de México.
* Guadalajara.
* Monterrey.

Cada sede utilizaba:

* Un QuickCapture para incidentes.
* Un QuickCapture para inspecciones.

Por lo tanto:

```text
CDMX
 ├── QuickCapture Incidentes
 │         │
 │         ▼
 │       Make
 │
 └── QuickCapture Inspecciones
           │
           ▼
         Make
```

La misma estructura se replicó para Guadalajara y Monterrey.

En total:

```text
3 QuickCapture de incidentes
+
3 QuickCapture de inspecciones
=
6 aplicaciones QuickCapture
```

y:

```text
6 QuickCapture
=
6 webhooks
=
6 escenarios de Make
```

---

# 6. Recepción de datos en Make

Una vez activado el webhook, Make recibe la información correspondiente al registro.

A partir de este punto comienza el procesamiento automatizado.

```text
Webhook
   │
   ▼
 Make
   │
   ▼
Procesamiento del registro
```

Make funciona como el componente de orquestación de la solución.

Su responsabilidad es coordinar la comunicación entre las distintas plataformas involucradas.

---

# 7. Registro en Google Sheets

Después de recibir la información, uno de los primeros pasos del escenario consiste en registrar los datos en Google Sheets.

```text
Make
  │
  ▼
Google Sheets
```

Esta etapa permite mantener una representación tabular de la información procesada.

El registro se realiza automáticamente, por lo que no requiere una nueva captura manual de los datos.

La estructura real de las hojas utilizadas en producción no forma parte de este repositorio.

---

# 8. Preparación de información para traducción

Posteriormente, Make identifica los campos que requieren procesamiento para generar la versión en inglés.

No todos los atributos necesitan traducción.

Por ejemplo, determinados campos pueden conservarse sin modificaciones:

```text
Fecha
Hora
Latitud
Longitud
Altitud
Identificadores
Valores técnicos
```

Mientras que campos descriptivos pueden requerir traducción:

```text
Tipo de incidente
Comentarios
Descripción
Información operativa
```

La selección específica depende de la estructura utilizada por cada tipo de registro.

---

# 9. Traducción mediante Gemini

Los campos que requieren traducción son enviados desde Make hacia un módulo de **Gemini**.

El proceso puede representarse de la siguiente manera:

```text
Datos en español
      │
      ▼
     Make
      │
      ▼
    Gemini
      │
      ▼
Datos traducidos
```

Gemini devuelve el contenido procesado en inglés.

Posteriormente, Make integra la información traducida con los campos que no requieren transformación.

---

# 10. Reconstrucción del registro en inglés

Después de obtener la traducción, Make genera un nuevo objeto de datos.

Este registro mantiene la misma estructura lógica que el registro original, pero contiene los campos correspondientes en inglés.

Ejemplo conceptual:

```text
Registro ES
   │
   ├── Fecha
   ├── Hora
   ├── Coordenadas
   ├── Tipo de incidente ES
   └── Comentarios ES
```

después del procesamiento:

```text
Registro EN
   │
   ├── Fecha
   ├── Hora
   ├── Coordenadas
   ├── Tipo de incidente EN
   └── Comentarios EN
```

De esta manera se mantiene una correspondencia entre ambas estructuras.

---

# 11. Inserción mediante ArcGIS REST API

Una vez construido el registro en inglés, Make lo envía a ArcGIS mediante la **ArcGIS REST API**.

Conceptualmente:

```text
Make
  │
  ▼
Registro EN
  │
  ▼
ArcGIS REST API
  │
  ▼
Feature Layer EN
```

La REST API permite insertar el registro de manera programática en la segunda Feature Layer.

La documentación pública del proyecto no incluye:

* URLs reales de servicios.
* Tokens.
* Credenciales.
* IDs privados.
* Parámetros de autenticación.
* Endpoints de producción.

---

# 12. Almacenamiento en Feature Layer EN

Después de la operación realizada mediante REST API, el registro traducido queda almacenado en la **Feature Layer en inglés**.

En este punto existen dos representaciones equivalentes del evento.

```text
              MISMO EVENTO
                   │
          ┌────────┴────────┐
          │                 │
          ▼                 ▼
Feature Layer ES     Feature Layer EN
```

El objetivo es mantener información equivalente para los dos entornos de visualización.

---

# 13. Flujo hacia Web Map ES

La Feature Layer en español alimenta al Web Map correspondiente.

```text
Feature Layer ES
       │
       ▼
    Web Map ES
```

El Web Map permite representar espacialmente los registros generados durante la operación.

La configuración del mapa puede utilizar atributos como:

* Tipo de incidente.
* Sede.
* Categoría.
* Estado.
* Clasificación operativa.

La simbología y configuración exactas del entorno productivo no se incluyen en este repositorio.

---

# 14. Flujo hacia Dashboard ES

El Web Map en español es utilizado posteriormente dentro del Dashboard correspondiente.

```text
Feature Layer ES
       │
       ▼
    Web Map ES
       │
       ▼
 Dashboard ES
```

El Dashboard permite concentrar información operacional y geoespacial en una única interfaz.

Dependiendo de la configuración implementada, puede contener:

* Mapa de incidentes.
* Indicadores.
* Contadores.
* Distribución por tipo de evento.
* Información de personal.
* Información por sede.
* Filtros.
* Elementos interactivos.

---

# 15. Flujo hacia Web Map EN

La Feature Layer en inglés sigue el mismo principio.

```text
Feature Layer EN
       │
       ▼
    Web Map EN
```

Este mapa utiliza los registros generados automáticamente por el proceso de traducción.

---

# 16. Flujo hacia Dashboard EN

Posteriormente:

```text
Feature Layer EN
       │
       ▼
    Web Map EN
       │
       ▼
 Dashboard EN
```

Esto permite contar con dos entornos de visualización separados:

```text
Español                    Inglés

Feature Layer ES           Feature Layer EN
       │                          │
       ▼                          ▼
   Web Map ES                 Web Map EN
       │                          │
       ▼                          ▼
 Dashboard ES               Dashboard EN
```

---

# 17. Flujo de notificaciones mediante WhatsApp

Los escenarios de Make también incorporaban módulos destinados al envío de notificaciones.

Una vez procesada la información correspondiente, determinadas novedades podían ser distribuidas al personal autorizado mediante WhatsApp.

```text
Registro
   │
   ▼
Webhook
   │
   ▼
 Make
   │
   ▼
Procesamiento
   │
   ▼
WhatsApp
   │
   ▼
Personal autorizado
```

Este mecanismo permitía complementar el Dashboard con un canal de notificación directa.

La visualización mediante Dashboard requiere que el usuario consulte activamente el sistema.

El mecanismo de WhatsApp permite que determinadas novedades lleguen directamente a los destinatarios definidos.

---

# 18. Flujo paralelo de la información

Es importante señalar que el registro original y el flujo de automatización cumplen funciones distintas.

La información no depende de la traducción para existir en español.

El flujo puede representarse de esta manera:

```text
                        QuickCapture
                             │
                  ┌──────────┴──────────┐
                  │                     │
                  ▼                     ▼
          Feature Layer ES          Webhook
                  │                     │
                  ▼                     ▼
             Web Map ES               Make
                  │                     │
                  ▼          ┌──────────┼──────────┐
            Dashboard ES     │          │          │
                             ▼          ▼          ▼
                         Sheets      Gemini     WhatsApp
                                        │
                                        ▼
                                 ArcGIS REST API
                                        │
                                        ▼
                                Feature Layer EN
                                        │
                                        ▼
                                    Web Map EN
                                        │
                                        ▼
                                  Dashboard EN
```

Esta separación permite que el almacenamiento del registro original y los procesos adicionales de integración funcionen como componentes diferenciados.

---

# 19. Flujo completo de un incidente

El recorrido completo de un registro puede resumirse en los siguientes pasos:

### Paso 1

El operador identifica una atención o incidente que debe registrarse.

### Paso 2

El operador selecciona el botón correspondiente dentro de QuickCapture.

### Paso 3

QuickCapture genera el registro con los atributos configurados.

### Paso 4

Se incorporan los datos geoespaciales disponibles.

### Paso 5

El registro se almacena en la Feature Layer en español.

### Paso 6

La nueva información queda disponible para el Web Map y Dashboard en español.

### Paso 7

El evento activa el webhook asociado.

### Paso 8

El webhook inicia el escenario correspondiente en Make.

### Paso 9

Make recibe los datos del registro.

### Paso 10

La información se almacena en Google Sheets.

### Paso 11

Make identifica los campos que requieren traducción.

### Paso 12

Los campos correspondientes son enviados a Gemini.

### Paso 13

Gemini devuelve el contenido traducido al inglés.

### Paso 14

Make reconstruye el registro con la estructura requerida para la capa de destino.

### Paso 15

Make realiza la solicitud correspondiente mediante ArcGIS REST API.

### Paso 16

El registro traducido se almacena en la Feature Layer en inglés.

### Paso 17

La información queda disponible para el Web Map en inglés.

### Paso 18

El Dashboard en inglés utiliza dicha información para actualizar sus elementos de visualización.

### Paso 19

El escenario ejecuta los módulos de notificación configurados.

### Paso 20

La novedad es distribuida mediante WhatsApp al personal autorizado correspondiente.

---

# 20. Flujo de inspecciones

Las inspecciones utilizan una arquitectura similar.

```text
Personal autorizado
        │
        ▼
QuickCapture de inspección
        │
        ▼
Feature Layer
        │
        ▼
Webhook
        │
        ▼
Make
```

La principal diferencia se encuentra en los campos utilizados y en el propósito del registro.

Mientras los QuickCapture operativos estaban orientados principalmente al registro de atenciones e incidentes, los QuickCapture de inspección permitían registrar información asociada a procesos de supervisión.

Ambos tipos de aplicaciones formaban parte de la misma infraestructura general.

---

# 21. Arquitectura de datos centralizada

Aunque las aplicaciones estaban distribuidas por sede, la información convergía en una infraestructura común.

```text
             CDMX
              │
              ▼
         QuickCapture
              │
              │
             GDL
              │
              ▼
         QuickCapture
              │
              │
             MTY
              │
              ▼
         QuickCapture
              │
              ▼
       Infraestructura
          central
              │
       ┌──────┴──────┐
       ▼             ▼
Feature Layer ES Feature Layer EN
```

Esto permitía que los Dashboards concentraran información proveniente de las tres sedes.

---

# 22. Relación entre eventos y automatizaciones

Cada aplicación QuickCapture tenía asociada una automatización independiente.

```text
QuickCapture 1 ───► Make 1
QuickCapture 2 ───► Make 2
QuickCapture 3 ───► Make 3
QuickCapture 4 ───► Make 4
QuickCapture 5 ───► Make 5
QuickCapture 6 ───► Make 6
```

Esta separación permitía mantener flujos específicos para cada origen de datos, conservando una lógica de procesamiento común.

---

# 23. Ejemplo conceptual de payload

Un registro enviado dentro del flujo podría representarse conceptualmente de la siguiente forma:

```json
{
  "personal": "OPERADOR_001",
  "corporacion": "CORPORACION_A",
  "fecha": "2026-06-15",
  "hora": "14:35:00",
  "latitud": 0.000000,
  "longitud": 0.000000,
  "altitud": 0,
  "tipo_incidente": "ATENCION_MEDICA",
  "sede": "SEDE_A",
  "comentarios": "REGISTRO_DE_DEMOSTRACION"
}
```

Este ejemplo utiliza exclusivamente información ficticia.

No representa la estructura exacta de los datos utilizados en producción.

---

# 24. Transformación conceptual del registro

El proceso de transformación puede representarse como:

```text
INPUT
│
├── Datos geoespaciales
├── Datos operativos
├── Campos descriptivos ES
└── Metadatos
        │
        ▼
       Make
        │
        ├── Registro auxiliar
        │
        ├── Selección de campos
        │
        ▼
      Gemini
        │
        ▼
Campos descriptivos EN
        │
        ▼
Reconstrucción del registro
        │
        ▼
ArcGIS REST API
        │
        ▼
OUTPUT
```

---

# 25. Flujo lógico de traducción

El proceso de traducción no debe entenderse como una traducción completa de todos los datos.

La lógica general consiste en conservar los datos estructurales y traducir únicamente los campos definidos para ello.

Por ejemplo:

| Campo                 | Acción            |
| --------------------- | ----------------- |
| Fecha                 | Conservar         |
| Hora                  | Conservar         |
| Latitud               | Conservar         |
| Longitud              | Conservar         |
| Altitud               | Conservar         |
| Identificador         | Conservar         |
| Tipo de incidente     | Traducir o mapear |
| Comentarios           | Traducir          |
| Descripción           | Traducir          |
| Información narrativa | Traducir          |

La selección real dependía de la configuración implementada.

---

# 26. Flujo de visualización

El proceso de captura y el proceso de visualización pueden verse como dos capas distintas.

```text
CAPTURA

QuickCapture
     │
     ▼
Feature Layer
```

y:

```text
VISUALIZACIÓN

Feature Layer
     │
     ▼
  Web Map
     │
     ▼
 Dashboard
```

Esto permite separar la generación del dato de su representación visual.

---

# 27. Flujo de notificación

De manera similar, las notificaciones funcionan como una salida adicional del proceso.

```text
DATOS
  │
  ▼
Make
  │
  ├────────► ArcGIS
  │
  ├────────► Google Sheets
  │
  └────────► WhatsApp
```

De esta forma, un mismo evento puede ser utilizado simultáneamente para almacenamiento, visualización, procesamiento y comunicación.

---

# 28. Consideraciones de seguridad

El flujo documentado en este repositorio es una representación conceptual de la arquitectura.

Por motivos de seguridad no se incluyen:

* Payloads reales.
* Datos médicos.
* Nombres reales.
* Coordenadas operativas.
* Números telefónicos.
* URLs de webhooks.
* URLs de Feature Services.
* Tokens.
* Credenciales.
* API keys.
* ArcGIS Item IDs sensibles.
* Identificadores de conexiones de Make.
* Documentos reales de Google Sheets.
* Configuraciones privadas de WhatsApp.
* Endpoints productivos.

Cualquier ejemplo utilizado en esta documentación debe contener únicamente datos ficticios o sanitizados.

---

# 29. Diagrama simplificado del flujo completo

```text
                         ┌───────────────────────┐
                         │   Personal en campo   │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │ ArcGIS QuickCapture   │
                         └───────────┬───────────┘
                                     │
                    ┌────────────────┴────────────────┐
                    │                                 │
                    ▼                                 ▼
          ┌──────────────────┐              ┌──────────────────┐
          │ Feature Layer ES │              │     Webhook      │
          └────────┬─────────┘              └────────┬─────────┘
                   │                                 │
                   ▼                                 ▼
          ┌──────────────────┐              ┌──────────────────┐
          │    Web Map ES    │              │       Make       │
          └────────┬─────────┘              └────────┬─────────┘
                   │                                 │
                   ▼                   ┌─────────────┼─────────────┐
          ┌──────────────────┐         │             │             │
          │   Dashboard ES   │         ▼             ▼             ▼
          └──────────────────┘   Google Sheets    Gemini       WhatsApp
                                                  │              │
                                                  ▼              ▼
                                           Traducción EN   Notificación
                                                  │
                                                  ▼
                                          ArcGIS REST API
                                                  │
                                                  ▼
                                         Feature Layer EN
                                                  │
                                                  ▼
                                             Web Map EN
                                                  │
                                                  ▼
                                           Dashboard EN
```

---

# 30. Resumen

El flujo de datos fue diseñado para transformar un registro realizado en campo en múltiples salidas operativas.

A partir de una única captura mediante QuickCapture, la información puede participar en diferentes procesos:

```text
Registro en campo
      │
      ├──► Almacenamiento geoespacial
      │
      ├──► Visualización en mapa
      │
      ├──► Visualización en dashboard
      │
      ├──► Registro auxiliar
      │
      ├──► Traducción automática
      │
      ├──► Replicación bilingüe
      │
      └──► Notificación automatizada
```

La utilización de QuickCapture, Feature Layers, Make, Gemini, ArcGIS REST API, Web Maps, Dashboards, Google Sheets y WhatsApp permitió construir un flujo integrado para la captura, procesamiento y distribución de información operativa.

---

## Documentación relacionada

* [`README.md`](README.md) — Descripción general de la arquitectura.
* `../quickcapture/` — Documentación de las aplicaciones de captura.
* `../automation/` — Documentación detallada de los escenarios de Make.
* `../dashboards/` — Documentación de los Web Maps y Dashboards.
* `../security/` — Consideraciones de seguridad y privacidad.
* `../../diagrams/` — Diagramas gráficos del sistema.

---

## Nota

Los diagramas, ejemplos y estructuras presentados en este documento tienen fines exclusivamente técnicos y documentales.

No contienen información suficiente para acceder o reproducir la infraestructura de producción y no incluyen datos operativos reales.

