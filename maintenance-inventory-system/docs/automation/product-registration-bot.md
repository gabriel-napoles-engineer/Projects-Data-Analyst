# Product Registration Bot

This document describes the automation executed after a new product is registered in AppSheet.

## Purpose

The **Product Registration Bot** is responsible for creating the initial traceability record of a newly registered product.

Its main functions are:

* Detect a new product registration.
* Generate an initial inventory movement.
* Associate the new product with a Movement ID.
* Generate a PDF with the registration information.
* Send the document to warehouse administrators.

## Trigger

The bot is triggered automatically after a new record is created in:

```text
Items mantenimiento
```

At this point, the product already contains its manually entered information and the automatically generated values such as:

* Item ID.
* Registration date.

## General Processing Flow

```text
New Product
     |
     v
Items mantenimiento
     |
     v
Product Registration Bot
     |
     v
Create Registration Movement
     |
     v
Movimientos Mantenimiento
     |
     v
Generate PDF
     |
     v
Send Email Notification
```

## Registration Movement

After detecting the new product, the bot creates a corresponding record in:

```text
Movimientos Mantenimiento
```

This movement represents the initial registration of the product within the inventory system.

The purpose of this step is to avoid having products without an associated transaction history.

## Product Traceability

The generated movement creates the first relationship between the product and the movement system.

```text
Item ID
   |
   v
Product Registration
   |
   v
Movement ID
   |
   v
Inventory History
```

From this point forward, future entries, exits, loans, and transfers can be linked to the same product.

## Automated Information

The automation uses the information already stored in the product record, including:

| Field                  | Description                                       |
| ---------------------- | ------------------------------------------------- |
| Item ID                | Unique identifier of the registered product.      |
| Product Name           | Name of the equipment, tool, part, or consumable. |
| Description            | Product description.                              |
| Serial Number          | Manufacturer serial number, when available.       |
| Asset Type             | Fixed asset or consumable.                        |
| Registration Date      | Date when the product was registered.             |
| Registration Signature | Signature of the person who created the record.   |

The system also generates the corresponding movement information required for traceability.

## PDF Generation

After the registration movement is created, the bot automatically generates a PDF containing the relevant product registration information.

The document serves as digital evidence of the product's initial entry into the inventory system.

The PDF can include:

* Item ID.
* Product name.
* Description.
* Serial number.
* Asset type.
* Registration date.
* Product image.
* Registration signature.
* Movement ID.

## Email Notification

Once the PDF is generated, the system automatically sends it to the warehouse administrators.

```text
Product Registration
        |
        v
Registration Movement
        |
        v
PDF Generation
        |
        v
Email Notification
        |
        v
Warehouse Administrators
```

This notification provides immediate evidence that a new product has been added to the inventory.

## Automation Benefits

The Product Registration Bot provides several operational benefits:

* Creates an automatic audit trail for new products.
* Reduces manual movement registration.
* Prevents products from being created without an initial movement.
* Generates standardized documentation.
* Automatically notifies warehouse administrators.
* Maintains consistency between product and movement records.

## Final Result

After the automation finishes, the system contains:

```text
Product Record
     +
Registration Movement
     +
Generated PDF
     +
Email Notification
```

This process ensures that every product starts its lifecycle with a documented and traceable registration event.

