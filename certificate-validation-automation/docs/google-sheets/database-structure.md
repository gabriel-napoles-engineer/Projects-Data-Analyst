# Database Structure

Google Sheets se utiliza como base de datos principal para almacenar la información de los participantes y controlar el proceso automático de generación de certificados.

Cada fila representa un certificado individual.

## Estructura de columnas

| Columna                     | Descripción                                                                                                      |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `FOLIO`                     | Identificador único asignado al certificado.                                                                     |
| `NOMBRE`                    | Nombre completo del participante.                                                                                |
| `EMPRESA`                   | Empresa u organización a la que pertenece el participante.                                                       |
| `CORREO`                    | Dirección de correo electrónico asociada al participante.                                                        |
| `CURSO`                     | Nombre del curso acreditado.                                                                                     |
| `HORAS`                     | Duración del curso en horas.                                                                                     |
| `INSTRUCTOR`                | Nombre del instructor responsable del curso.                                                                     |
| `FECHA`                     | Fecha en la que se realizó o acreditó el curso.                                                                  |
| `VIGENCIA`                  | Fecha de expiración o periodo de vigencia del certificado.                                                       |
| `Fecha Ultimo envio`        | Registra la fecha del último envío realizado por el sistema.                                                     |
| `Evidencia`                 | Almacena la referencia o URL del documento de validación generado en Google Drive.                               |
| `QR`                        | Almacena la información o referencia del código QR generado a partir de la URL de evidencia.                     |
| `Constancia`                | Almacena la referencia o URL de la constancia generada.                                                          |
| `Fecha ultima modificacion` | Registra la última fecha en la que el registro fue modificado.                                                   |
| `Generar Carpeta`           | Campo de control utilizado para ejecutar la creación de la carpeta o estructura correspondiente en Google Drive. |
| `FALSE`                     | Campo auxiliar utilizado por el proceso de automatización como valor booleano de control.                        |

## Datos principales

Los campos utilizados directamente para generar la documentación son:

```text
FOLIO
NOMBRE
EMPRESA
CORREO
CURSO
HORAS
INSTRUCTOR
FECHA
VIGENCIA
```

Estos datos representan la información original registrada para cada participante.

## Campos de automatización

Durante la ejecución de Google Apps Script se generan o actualizan campos adicionales:

```text
Fecha Ultimo envio
Evidencia
QR
Constancia
Fecha ultima modificacion
Generar Carpeta
```

Estos campos permiten al script conocer el estado del proceso y conservar las referencias a los documentos generados.

## Relación con los documentos

El registro de Google Sheets funciona como origen central de la información:

```text
Google Sheets
     │
     ├── Datos del participante
     │
     ├── Folio único
     │
     └── Datos del curso
             ↓
      Google Apps Script
             │
             ├── Documento de evidencia
             ├── URL de evidencia
             ├── Código QR
             └── Constancia
```

El mismo `FOLIO` se utiliza tanto en la constancia como en el documento de evidencia, permitiendo relacionar ambos documentos.

## Consideraciones

La hoja de cálculo utilizada en producción contiene información personal, por lo que los ejemplos publicados en este repositorio deben utilizar únicamente datos ficticios o sanitizados.

No se deben publicar:

* Nombres reales de participantes
* Correos electrónicos reales
* URLs privadas de Google Drive
* Folios asociados a certificados reales
* IDs de archivos o carpetas privadas
* Credenciales o configuraciones sensibles

