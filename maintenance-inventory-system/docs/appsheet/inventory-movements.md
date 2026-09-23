# Inventory Movements

This document describes how inventory movements are registered and processed within the maintenance inventory system.

## Purpose

The **Movements** view in AppSheet is used to register and review inventory transactions.

The system supports three main movement types:

* Entry.
* Exit.
* Loan.

Each movement creates a traceable record between an origin and a destination.

## Movement Registration

When a new movement is created, the user must provide the following information:

| Field                 | Description                                                   |
| --------------------- | ------------------------------------------------------------- |
| Movement Type         | Entry, exit, or loan.                                         |
| Origin                | Department, unit, or employee providing the product.          |
| Destination           | Department, unit, or employee receiving the product.          |
| Product(s)            | One or more products included in the movement.                |
| Quantity              | Quantity assigned to each selected product.                   |
| Observations          | Additional information related to the transaction.            |
| Reason                | Reason for the movement.                                      |
| Invoice or Ticket     | Supporting purchase or transaction document, when applicable. |
| Delivery Responsible  | Person responsible for delivering the products.               |
| Receiving Responsible | Person responsible for receiving the products.                |
| Receiving Email       | Email address of the receiving person.                        |
| Evidence              | Supporting image or document.                                 |
| Delivery Signature    | Signature of the person delivering the products.              |
| Receiving Signature   | Signature of the person receiving the products.               |

## Automatically Generated Information

The system automatically assigns:

| Field         | Description                                 |
| ------------- | ------------------------------------------- |
| Movement ID   | Unique identifier for the transaction.      |
| Date and Time | Timestamp when the movement was registered. |

## Main Movement Record

Each transaction creates only one main record in the `Movimientos Mantenimiento` table.

This record stores the general information associated with the complete transaction, even when multiple products are included.

```text
AppSheet Movement Form
        |
        v
Validate Information
        |
        v
Movimientos Mantenimiento
        |
        v
Single Movement Record
```

## Multiple Products

A single movement can contain multiple products with independent quantities.

For example:

```text
Movement ID: MOV-00125

Origin: Maintenance Department
Destination: Unit 03

Products:
- Hydraulic Tool: 1
- Extension Cable: 2
- Safety Cone: 4
```

The general transaction is stored once in `Movimientos Mantenimiento`, while each product is processed separately in the movement detail table.

## Movement Processing

After the main movement is saved, an AppSheet automation processes every selected product.

For each product, two detail records are generated:

* A negative quantity for the origin.
* A positive quantity for the destination.

Example:

```text
Product: Hydraulic Tool
Quantity: 2

Origin:
Maintenance Department | -2

Destination:
Unit 03 | +2
```

These records are stored in:

```text
Detalle Movimientos Mantenimiento
```

## Processing Flow

```text
Movement Registration
        |
        v
Movimientos Mantenimiento
        |
        v
Movement Processing Bot
        |
        v
Process Each Product
        |
   +----+----+
   |         |
   v         v
 Origin   Destination
  -Qty       +Qty
   |         |
   +----+----+
        |
        v
Detalle Movimientos Mantenimiento
```

## Inventory Update

The system does not directly modify a single stock value.

Instead, inventory quantities are calculated from the accumulated movement detail records.

This allows the system to determine how many units of each product are currently assigned to:

* Departments.
* Units.
* Personnel.

This transaction-based approach maintains a complete movement history and improves inventory traceability.

## Movement Documentation

Once the movement has been processed, the system automatically generates a PDF containing the transaction information.

The document can include:

* Movement ID.
* Date and time.
* Movement type.
* Origin.
* Destination.
* Products and quantities.
* Responsible personnel.
* Observations.
* Evidence.
* Signatures.

## Email Notification

The generated PDF is automatically distributed by email to:

* Warehouse administrators.
* Receiving personnel.

The receiving person is included using the email address registered during the movement.

```text
Movement Completed
        |
        v
PDF Generation
        |
        v
Email Notification
       / \
      /   \
     v     v
Warehouse  Receiving
Admins     Personnel
```

## Traceability

The movement structure provides a complete audit trail for every inventory transaction.

Each movement can be traced through:

```text
Movement ID
   |
   +-- Origin
   |
   +-- Destination
   |
   +-- Products
   |
   +-- Quantities
   |
   +-- Responsible Personnel
   |
   +-- Evidence
   |
   +-- Signatures
   |
   +-- Movement Details
```

This makes it possible to identify where a product came from, where it was assigned, who participated in the transaction, and when the movement occurred.

