# Validation Process

Este documento describe el proceso utilizado para validar la autenticidad de los certificados mediante el código QR incorporado en cada constancia.

## Objetivo

El mecanismo de validación permite comprobar que la información presentada en un certificado coincida con el documento de evidencia generado originalmente por el sistema.

Esto ayuda a detectar certificados modificados, datos alterados o folios utilizados de forma incorrecta.

## Proceso de validación

```text
Certificado
     ↓
Escaneo del código QR
     ↓
URL de validación
     ↓
Documento de evidencia en Google Drive
     ↓
Comparación de información
```

## 1. Escaneo del código QR

Cada certificado contiene un código QR generado durante el proceso de automatización.

El usuario puede escanearlo utilizando un dispositivo móvil o cualquier lector compatible.

## 2. Acceso al documento de evidencia

El código QR contiene la dirección electrónica del documento de evidencia almacenado en Google Drive.

Al escanearlo, el usuario es dirigido directamente a dicho documento.

## 3. Información disponible para validación

El documento de evidencia contiene los principales datos asociados al certificado:

* Nombre
* Curso
* Empresa

