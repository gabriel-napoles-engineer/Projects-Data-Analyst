# Movement Processing Bot

This document describes the automation executed after a new inventory movement is registered in AppSheet.

## Purpose

The **Movement Processing Bot** is responsible for converting a general movement into individual inventory detail records.

Its main functions are:

* Process each product included in a movement.
* Subtract quantities from the origin.
* Add quantities to the destination.
* Generate movement detail records.
* Create a PDF with the transaction information.
* Send email notifications.

## Trigger

The bot is triggered automatically after a new record is created in:

```text
Movimientos Mantenimiento
```

Each movement can contain one or multiple products with their corresponding quantities.

## General Processing Flow

```text
New Movement
     |
     v
Movimientos Mantenimiento
     |
     v
Movement Processing Bot
     |
     v
Process Selected Products
     |
     v
Create Movement Details
     |
     v
Update Inventory Calculation
     |
     v
Generate PDF
     |
     v
Send Email Notifications
```

## Product Processing

The bot processes each selected product independently.

For every product, two records are created in:

```text
Detalle Movimientos Mantenimiento
```

The first record represents the quantity removed from the origin.

The second record represents the quantity added to the destination.

```text
Product Quantity
      |
      +----------------+
      |                |
      v                v
Origin Record     Destination Record
   -Quantity          +Quantity
```

## Example

A movement is created with the following information:

```text
Movement ID: MOV-00125
Origin: Maintenance Department
Destination: Unit 03

Product: Hydraulic Tool
Quantity: 2
```

The automation generates:

```text
MOV-00125 | Maintenance Department | Hydraulic Tool | -2
MOV-00125 | Unit 03                | Hydraulic Tool | +2
```

Both records remain associated with the same Movement ID.

## Multiple Products

If a movement contains several products, the bot repeats the same process for each one.

Example:

```text
Product A | Quantity: 2
Product B | Quantity: 5
Product C | Quantity: 1
```

The bot generates:

```text
Origin      | Product A | -2
Destination | Product A | +2

Origin      | Product B | -5
Destination | Product B | +5

Origin      | Product C | -1
Destination | Product C | +1
```

A movement containing three products therefore generates six detail records.

## Stock Impact

The bot does not directly overwrite a stock value.

Instead, each generated detail record contributes to the inventory calculation.

```text
Negative Records
       +
Positive Records
       |
       v
Quantity Aggregation
       |
       v
Current Stock
```

This approach maintains the complete history of inventory transactions.

## PDF Generation

After all products have been processed, the bot generates a PDF containing the main movement information.

The document can include:

* Movement ID.
* Date and time.
* Movement type.
* Origin.
* Destination.
* Products.
* Quantities.
* Reason.
* Observations.
* Delivery responsible.
* Receiving responsible.
* Evidence.
* Signatures.

The PDF acts as the digital record of the transaction.

## Email Distribution

After the PDF is generated, the bot sends an automatic email notification.

The notification is distributed to:

* Warehouse administrators.
* Receiving personnel.

The receiving person is copied using the email address entered during the movement registration.

```text
Movement PDF
     |
     v
Email Notification
    / \
   /   \
  v     v
Warehouse      Receiving
Administrators Personnel
```

## Traceability

All generated detail records maintain a reference to the original Movement ID.

This relationship allows the system to reconstruct the complete transaction from the general movement and its individual product records.

```text
Movement ID
    |
    +-- General Movement Data
    |
    +-- Product 1 Detail
    |
    +-- Product 2 Detail
    |
    +-- Product 3 Detail
    |
    +-- PDF Record
    |
    +-- Email Notification
```

This automation ensures that every inventory change is documented, traceable, and reflected correctly in the Stock view.

