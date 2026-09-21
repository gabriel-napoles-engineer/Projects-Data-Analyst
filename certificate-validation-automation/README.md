# Certificate Validation Automation

Sistema automatizado para la generación y validación de certificados de capacitación mediante **Google Sheets**, **Google Apps Script** y códigos **QR**.

## Descripción

El proyecto surge de la necesidad de mejorar el control de los certificados emitidos para cursos de combate contra incendios.

Anteriormente, cada certificado era elaborado de forma manual. Esto generaba dos problemas principales:

* El proceso requería aproximadamente **6 minutos por certificado**.
* Algunos certificados eran modificados posteriormente, principalmente cambiando nombres mientras se conservaban folios existentes, provocando inconsistencias entre los documentos presentados y los registros internos.

Para solucionar esta situación se desarrolló un flujo automatizado basado en **Google Sheets y Google Apps Script**.

## Solución implementada

Google Sheets funciona como base de datos para almacenar la información de los participantes.

A partir de estos registros, un script desarrollado en Google Apps Script realiza automáticamente:

1. Lectura de los datos del participante.
2. Generación del certificado.
3. Asignación del folio correspondiente.
4. Generación de un código QR mediante una API.
5. Incorporación del código QR al certificado.
6. Generación de un documento de respaldo para validación.
7. Vinculación del QR con dicho documento.

De esta manera, el código QR permite consultar la información asociada al certificado y comprobar que los datos coincidan con el registro generado originalmente.

## Información del certificado

Cada certificado contiene:

* Nombre del participante
* Curso
* Empresa
* Fecha de expiración
* Folio único
* Horas de capacitación
* Código QR

## Documento de validación

El código QR dirige a un documento de respaldo generado automáticamente que contiene:

* Nombre del participante
* Curso
* Empresa
* Fecha de expiración
* Folio único
* Horas de capacitación

El folio y los datos del documento de validación permiten comprobar la correspondencia con el certificado presentado.

## Tecnologías

* Google Sheets
* Google Apps Script
* Google Drive
* API para generación de códigos QR
* Documentos y plantillas de Google

## Resultados

Antes de la automatización, la elaboración manual de un certificado requería aproximadamente **6 minutos**.

Con el nuevo flujo, el proceso completo tarda aproximadamente **20 segundos por certificado**, incluyendo la generación del código QR y del documento de respaldo.

Esto representa una reducción aproximada del **94.4 % en el tiempo de generación**.

Además de reducir considerablemente el trabajo manual, el sistema proporciona un mecanismo adicional para validar la autenticidad y trazabilidad de los certificados emitidos.

## Estructura del repositorio

```text
certificate-validation-automation/
│
├── README.md
├── docs/
├── src/
├── samples/
├── screenshots/
├── appsscript.json
├── .gitignore
└── LICENSE
```

La documentación técnica, arquitectura, flujo de datos y ejemplos sanitizados se encuentran en las carpetas correspondientes.

## Seguridad y privacidad

Los archivos publicados en este repositorio utilizan información de ejemplo.

No se incluyen:

* Datos personales reales
* Certificados reales
* Credenciales
* API keys
* Tokens
* IDs privados de Google Drive
* URLs privadas
* Información confidencial de participantes o empresas

