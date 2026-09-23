# Maintenance Inventory System

Sistema de inventarios desarrollado en **AppSheet** para el departamento de mantenimiento, utilizando **Google Sheets** como base de datos central.

La solución permite registrar productos, controlar entradas, salidas y préstamos, consultar el stock disponible y mantener trazabilidad sobre los movimientos realizados entre personal, unidades y departamentos.

## Objetivo

Digitalizar el control de inventario del departamento de mantenimiento mediante una solución en la nube que pueda ser utilizada tanto dentro de las instalaciones como durante trabajos en campo.

El sistema busca centralizar:

* Herramientas.
* Consumibles.
* Piezas y refacciones.
* Entradas y salidas.
* Préstamos.
* Responsables de entrega y recepción.
* Evidencias y firmas.
* Historial de movimientos.

## Arquitectura general

La solución utiliza principalmente:

* **AppSheet** — Interfaz de operación.
* **Google Sheets** — Base de datos.
* **AppSheet Automation** — Procesamiento automático de movimientos y generación de reportes.
* **PDF** — Evidencia documental de altas y movimientos.
* **Email** — Distribución automática de comprobantes y reportes.

## Funcionalidades principales

### Productos

Permite consultar y registrar nuevos productos o activos.

Cada registro puede incluir:

* Nombre.
* Descripción.
* Imagen.
* Número de serie.
* Tipo de activo.
* Firma de alta.

El sistema genera automáticamente la fecha de registro y un identificador único para cada producto.

### Movimientos

Permite registrar:

* Entradas.
* Salidas.
* Préstamos.

Cada movimiento puede involucrar uno o varios productos con cantidades independientes.

También se registran datos como:

* Origen.
* Destino.
* Motivo.
* Observaciones.
* Responsables.
* Evidencias.
* Factura o ticket.
* Firmas.

Cada operación recibe automáticamente un **ID de movimiento** y una fecha y hora de registro.

### Stock

Vista de consulta que permite conocer los productos y cantidades asignadas a:

* Personal.
* Unidades.
* Departamentos.

Desde esta vista no se realizan movimientos.

## Automatizaciones

El sistema cuenta con automatizaciones para:

* Generar un movimiento al registrar un nuevo producto.
* Actualizar automáticamente el inventario del origen y destino.
* Crear registros individuales por producto dentro de cada movimiento.
* Generar comprobantes en PDF.
* Enviar notificaciones por correo electrónico.
* Generar un reporte semanal consolidado de movimientos.

## Base de datos

La información se almacena en Google Sheets mediante las siguientes tablas principales:

```text
Items mantenimiento
Movimientos Mantenimiento
Detalle Movimientos Mantenimiento
Solicitud de mantenimiento
Facturas mantenimiento
Tarjetas Mantenimiento
Departamentos
Personal
Unidades
```

## Documentación

La documentación técnica del proyecto se encuentra en:

```text
docs/
├── architecture/
├── appsheet/
├── database/
└── automation/
```

Dentro de estas carpetas se documentan la arquitectura, flujo de datos, estructura de la base de datos, funcionamiento de las vistas y automatizaciones implementadas.

