# Data Flow

This document describes the main data flow of the maintenance inventory system.

## Product Registration

When a new product is registered in AppSheet, the user provides information such as:

* Product name.
* Description.
* Image.
* Serial number.
* Asset type.
* Registration signature.

The system automatically assigns:

* Registration date.
* Item ID.

After the product is created, an AppSheet bot automatically generates a registration movement in the `Movimientos Mantenimiento` table.

A PDF containing the product information is then generated and sent by email to the warehouse administrators.

```text
AppSheet
   |
   v
Product Registration
   |
   v
Items mantenimiento
   |
   v
Automatic Registration Movement
   |
   v
Movimientos Mantenimiento
   |
   v
PDF Generation
   |
   v
Email Notification
```

## Inventory Movement

Users can register three main types of movement:

* Entry.
* Exit.
* Loan.

Each movement contains general information such as origin, destination, responsible personnel, observations, evidence, signatures, and one or more products with their respective quantities.

AppSheet creates a single record in the `Movimientos Mantenimiento` table for the complete transaction.

```text
AppSheet
   |
   v
Movement Form
   |
   v
Movimientos Mantenimiento
```

## Movement Detail Processing

After the main movement is saved, an automation processes each selected product individually.

For every product included in the movement, two records are created in `Detalle Movimientos Mantenimiento`:

1. A negative quantity is assigned to the origin.
2. A positive quantity is assigned to the destination.

For example:

```text
Movement: Loan

Origin: Maintenance Department
Destination: Vehicle 01

Product: Hydraulic Tool
Quantity: 2
```

The detail table receives:

```text
Maintenance Department | Hydraulic Tool | -2
Vehicle 01              | Hydraulic Tool | +2
```

This structure allows the system to calculate inventory quantities based on the complete movement history.

The processing flow is:

```text
Movimientos Mantenimiento
          |
          v
    AppSheet Bot
          |
          v
Process Products
          |
     +----+----+
     |         |
     v         v
Origin      Destination
  -Qty         +Qty
     |         |
     +----+----+
          |
          v
Detalle Movimientos Mantenimiento
```

## Stock Calculation

The Stock view uses the records stored in `Detalle Movimientos Mantenimiento`.

The accumulated positive and negative quantities determine the current inventory assigned to each:

* Department.
* Vehicle.
* Employee.

```text
Detalle Movimientos Mantenimiento
          |
          v
Quantity Aggregation
          |
          v
Current Stock
          |
          v
AppSheet Stock View
```

The Stock view is read-only and is used only to visualize the current location and quantity of each product.

## Movement Documentation

After a movement is processed, the system automatically generates a PDF containing the transaction information.

The document is sent by email to:

* Warehouse administrators.
* Receiving personnel, when applicable.

```text
Movement Completed
       |
       v
PDF Generation
       |
       v
Email Distribution
```

## Weekly Report

Every Monday at 09:00, an automated process reviews the movements registered during the previous week.

The system generates a consolidated PDF containing the weekly movement history and sends it to management.

```text
Weekly Scheduled Bot
        |
        v
Retrieve Weekly Movements
        |
        v
Generate Consolidated PDF
        |
        v
Send Report to Management
```

## General Data Flow

```text
                +----------------+
                |    AppSheet    |
                +-------+--------+
                        |
          +-------------+-------------+
          |                           |
          v                           v
 Product Registration          Inventory Movement
          |                           |
          v                           v
Items mantenimiento      Movimientos Mantenimiento
          |                           |
          |                           v
          |                    AppSheet Automation
          |                           |
          |                           v
          |              Detalle Movimientos Mantenimiento
          |                           |
          |                           v
          |                     Stock Calculation
          |                           |
          |                           v
          |                    AppSheet Stock View
          |
          +-------------+
                        |
                        v
                 PDF Generation
                        |
                        v
                Email Notification
```

