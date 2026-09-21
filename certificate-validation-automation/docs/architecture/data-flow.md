# Data Flow

Este documento describe el flujo de información utilizado para generar y validar los certificados de capacitación.

## Flujo general

```text
Google Sheets
     ↓
Google Apps Script
     ↓
Lectura de datos del participante
     ↓
Generación del documento de validación
     ↓
Almacenamiento en Google Drive
     ↓
Obtención de la URL del documento
     ↓
Generación del código QR
     ↓
Generación del certificado
     ↓
Inserción del código QR
     ↓
Certificado final
```

## 1. Registro de información

La información de cada participante se almacena en Google Sheets.

Los principales campos utilizados son:

* Nombre
* Curso
* Empresa
* Fecha de expiración
* Folio
* Horas de curso

## 2. Procesamiento con Google Apps Script

Google Apps Script obtiene la información registrada en la hoja de cálculo y ejecuta automáticamente el proceso de generación de documentos.

## 3. Generación del documento de validación

El sistema genera primero un documento de respaldo con la información asociada al certificado:

* Nombre
* Curso
* Empresa
* Fecha de expiración
* Folio único
* Horas de curso

Este documento funciona como evidencia para comprobar posteriormente la información del certificado.

## 4. Almacenamiento en Google Drive

El documento de validación generado se almacena en Google Drive.

Una vez creado, el sistema obtiene la dirección electrónica correspondiente al documento.

```text
Datos del participante
        ↓
Documento de validación
        ↓
Google Drive
        ↓
URL del documento
```

## 5. Generación del código QR

La URL del documento almacenado en Google Drive se utiliza para generar un código QR mediante una API.

```text
URL del documento de validación
              ↓
        API de código QR
              ↓
          Código QR
```

Por lo tanto, cada código QR queda asociado directamente con la evidencia correspondiente a ese certificado.

## 6. Generación del certificado

Posteriormente se genera el certificado con la información del participante y el mismo folio utilizado en el documento de validación.

El certificado contiene:

* Nombre
* Curso
* Empresa
* Fecha de expiración
* Folio único
* Horas de curso
* Código QR

El código QR generado previamente se inserta directamente en el certificado.

## 7. Validación

Cuando se escanea el código QR del certificado, este dirige al documento de validación almacenado en Google Drive.

```text
Certificado
     │
     │ Escaneo del QR
     ↓
Código QR
     ↓
URL de Google Drive
     ↓
Documento de validación
     ↓
Comparación de información
```

Esto permite comprobar que la información presentada en el certificado corresponda con la evidencia generada originalmente por el sistema.

## Resultado

El flujo automatizado permite generar primero la evidencia digital, vincularla mediante un código QR y posteriormente incorporar dicho código al certificado final.

De esta manera, cada certificado mantiene una referencia directa a su documento de validación, mejorando la trazabilidad y facilitando la detección de documentos modificados.

