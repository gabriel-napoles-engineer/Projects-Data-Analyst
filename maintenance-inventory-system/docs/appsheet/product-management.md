# Product Management

This document describes how products are registered and managed within the maintenance inventory system.

## Purpose

The **Products** view in AppSheet is used to:

* Search registered products.
* Review product information.
* Register new tools, equipment, consumables, parts, and spare parts.

Each product is stored in the `Items mantenimiento` table in Google Sheets.

## Product Registration

When a new product is added, the user must provide the following information:

| Field                  | Description                                                |
| ---------------------- | ---------------------------------------------------------- |
| Product Name           | Name of the tool, equipment, part, or consumable.          |
| Description            | General description of the product.                        |
| Image                  | Product reference image.                                   |
| Serial Number          | Manufacturer or equipment serial number, when available.   |
| Asset Type             | Defines whether the item is a fixed asset or a consumable. |
| Registration Signature | Signature of the person registering the product.           |

## Automatically Generated Information

The system automatically assigns:

| Field             | Description                                |
| ----------------- | ------------------------------------------ |
| Registration Date | Date when the product was created.         |
| Item ID           | Unique identifier assigned to the product. |

The **Item ID** is used as the main reference for identifying the product throughout the inventory system.

## Product Registration Flow

```text
User
 |
 v
AppSheet Products View
 |
 v
New Product Form
 |
 v
Product Information Validation
 |
 v
Items mantenimiento
 |
 v
Item ID + Registration Date
 |
 v
Product Registration Bot
```

## Automatic Registration Movement

After the product is created, an AppSheet automation is triggered.

The automation generates a corresponding registration movement in the `Movimientos Mantenimiento` table.

This creates a traceable record of the initial product registration and associates the product with its inventory history.

```text
New Product
    |
    v
Items mantenimiento
    |
    v
AppSheet Automation
    |
    v
Registration Movement
    |
    v
Movimientos Mantenimiento
```

## PDF Generation

After the registration process is completed, the system automatically generates a PDF containing the relevant product information.

The PDF serves as documentation and evidence of the product registration.

The document is automatically sent by email to the warehouse administrators.

```text
Product Registration
        |
        v
Generate PDF
        |
        v
Email Notification
        |
        v
Warehouse Administrators
```

## Product Traceability

Each registered product is associated with a unique `Item ID`.

This identifier allows the system to maintain traceability across:

* Product registration.
* Inventory movements.
* Assigned locations.
* Departments.
* Units.
* Personnel.
* Movement history.

The product record acts as the master reference, while all inventory changes are registered through the movement system.

