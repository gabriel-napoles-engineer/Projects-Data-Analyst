# Maintenance Inventory System

Inventory management system developed in **AppSheet** for the maintenance department, using **Google Sheets** as the central database.

The solution allows users to register products, manage entries, exits, and loans, review available stock, and maintain traceability of movements between personnel, units, and departments.

## Objective

Digitize the maintenance department's inventory management through a cloud-based solution that can be used both within the facilities and during field operations.

The system is designed to centralize:

* Tools.
* Consumables.
* Parts and spare parts.
* Entries and exits.
* Loans.
* Delivery and receiving personnel.
* Evidence and signatures.
* Movement history.

## General Architecture

The solution mainly uses:

* **AppSheet** — Operational interface.
* **Google Sheets** — Database.
* **AppSheet Automation** — Automatic movement processing and report generation.
* **PDF** — Documentary evidence for registrations and movements.
* **Email** — Automatic distribution of receipts and reports.

## Main Features

### Products

Allows users to review and register new products or assets.

Each record can include:

* Name.
* Description.
* Image.
* Serial number.
* Asset type.
* Registration signature.

The system automatically generates the registration date and a unique identifier for each product.

### Movements

Allows users to register:

* Entries.
* Exits.
* Loans.

Each movement can include one or multiple products with independent quantities.

Additional information can also be recorded, such as:

* Origin.
* Destination.
* Reason.
* Observations.
* Responsible personnel.
* Evidence.
* Invoice or ticket.
* Signatures.

Each transaction automatically receives a **Movement ID** and a registration date and time.

### Stock

Read-only view that allows users to review the products and quantities assigned to:

* Personnel.
* Units.
* Departments.

No inventory movements can be performed from this view.

## Automations

The system includes automations to:

* Generate a movement when a new product is registered.
* Automatically update inventory between the origin and destination.
* Create individual product records for each movement.
* Generate PDF receipts.
* Send email notifications.
* Generate a consolidated weekly movement report.

## Database

The information is stored in Google Sheets using the following main tables:

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

## Documentation

The project's technical documentation is located in:

```text
docs/
├── architecture/
├── appsheet/
├── database/
└── automation/
```

These folders document the system architecture, data flow, database structure, view functionality, and implemented automations.
