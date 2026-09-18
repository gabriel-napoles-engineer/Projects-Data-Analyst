## Descripción

Este proyecto documenta la arquitectura de una solución geoespacial desarrollada para el registro, procesamiento, visualización y notificación en tiempo real de atenciones médicas, incidentes de emergencia e inspecciones operativas durante eventos del Mundial 2026 realizados en México.

La solución fue desplegada para tres sedes: Ciudad de México, Guadalajara y Monterrey.

El sistema integró herramientas de ArcGIS, automatización mediante Make, procesamiento mediante inteligencia artificial y servicios de mensajería para proporcionar al personal operativo y directivo una visión centralizada de los eventos registrados en campo.

> **Privacidad y seguridad:** este repositorio contiene únicamente documentación, diagramas, capturas sanitizadas y datos sintéticos. No se incluyen datos personales, información médica, coordenadas operativas, credenciales, tokens, webhooks, endpoints ni información procedente de los sistemas de producción.

## Objetivo

Permitir que el personal operativo pudiera registrar desde dispositivos móviles las atenciones médicas, incidentes de emergencia e inspecciones realizadas dentro de las sedes, haciendo que la información estuviera disponible prácticamente en tiempo real para su consulta mediante mapas, dashboards y mecanismos de notificación.

Adicionalmente, la solución generaba una réplica de la información en inglés mediante un proceso automatizado de traducción.

## Arquitectura general

El sistema se estructuró alrededor de dos repositorios geoespaciales principales:

* Feature Layer en español.
* Feature Layer en inglés.

La información registrada mediante ArcGIS QuickCapture era almacenada inicialmente en la capa correspondiente en español.

Cada registro generaba adicionalmente un webhook que iniciaba un escenario de automatización en Make.

El escenario realizaba las siguientes operaciones:

1. Recepción de la información generada desde QuickCapture.
2. Registro de la información en Google Sheets.
3. Traducción automática de los campos correspondientes del español al inglés mediante Gemini.
4. Construcción del registro traducido.
5. Inserción del nuevo registro en la Feature Layer en inglés mediante ArcGIS REST API.
6. Generación de notificaciones operativas mediante WhatsApp.

De esta manera se mantenían dos conjuntos de información equivalentes, uno en español y otro en inglés.

## Captura en campo

Para las tres sedes se desarrollaron dos tipos de aplicaciones ArcGIS QuickCapture.

### Registro de incidentes

Una aplicación por sede destinada al personal operativo para registrar:

* Atenciones médicas.
* Incidentes de emergencia.
* Tipo de incidente.
* Personal que realizó la atención.
* Corporación.
* Fecha y hora.
* Información geoespacial.
* Sede.

### Inspecciones

Adicionalmente se desarrolló una aplicación QuickCapture para cada sede destinada al registro de inspecciones realizadas por personal autorizado.

Estas aplicaciones utilizaban la misma infraestructura de Feature Layers, almacenando la información en campos específicos destinados al proceso de inspección.

## Automatización

Debido a que cada proyecto de QuickCapture utilizaba su propio webhook, se implementaron seis escenarios independientes en Make:

| Tipo         |  CDMX | Guadalajara | Monterrey |
| ------------ | ----: | ----------: | --------: |
| Incidentes   |     1 |           1 |         1 |
| Inspecciones |     1 |           1 |         1 |
| **Total**    | **2** |       **2** |     **2** |

Esto dio como resultado seis flujos de automatización conectados a una arquitectura de datos centralizada.

## Visualización

Sobre las Feature Layers se desarrollaron dos Web Maps:

* Mapa operativo en español.
* Mapa operativo en inglés.

Cada mapa alimentaba un ArcGIS Dashboard correspondiente, permitiendo consultar y analizar la información registrada en campo prácticamente en tiempo real.

Los dashboards permitían concentrar los registros generados por las diferentes sedes y presentarlos mediante elementos cartográficos e indicadores operativos.

## Notificaciones

Los escenarios de Make incorporaban finalmente módulos de mensajería mediante WhatsApp.

Después del procesamiento de cada registro, determinadas novedades podían enviarse automáticamente al personal directivo, reduciendo el tiempo entre el registro de un incidente en campo y su conocimiento por parte de las áreas responsables.

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

## Alcance de la implementación

La solución estuvo compuesta por:

* 3 aplicaciones QuickCapture para registro de incidentes.
* 3 aplicaciones QuickCapture para inspecciones.
* 6 webhooks.
* 6 escenarios de automatización en Make.
* 2 Feature Layers centrales.
* 2 Web Maps.
* 2 ArcGIS Dashboards.
* Integración de traducción automática español-inglés.
* Integración de notificaciones mediante WhatsApp.

## Seguridad de la información

La versión presentada en este repositorio ha sido sanitizada deliberadamente.

No se publican:

* Datos personales.
* Información médica.
* Coordenadas reales de incidentes.
* Fotografías operativas.
* Credenciales.
* API keys.
* Tokens.
* Webhooks.
* Endpoints privados.
* URLs de servicios internos.
* Números telefónicos.
* Bases de datos de producción.

Los ejemplos incluidos en el repositorio utilizan datos ficticios y tienen únicamente fines de documentación técnica.

