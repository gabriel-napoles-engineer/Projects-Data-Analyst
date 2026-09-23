# Stock View

This document describes how the current inventory is displayed within the maintenance inventory system.

## Purpose

The **Stock** view in AppSheet provides a read-only representation of the products currently assigned to different locations or responsible entities.

Users can review inventory associated with:

* Departments.
* Units.
* Personnel.

No inventory movements can be created or modified from this view.

## Stock Information

The Stock view displays the current quantity of each product assigned to a specific entity.

A typical record can include:

| Field       | Description                                        |
| ----------- | -------------------------------------------------- |
| Product     | Product or asset being tracked.                    |
| Item ID     | Unique identifier of the product.                  |
| Assigned To | Department, unit, or employee holding the product. |
| Quantity    | Current calculated quantity.                       |
| Asset Type  | Fixed asset or consumable.                         |

Additional product information can be retrieved from the `Items mantenimiento` table when required.

## Stock Calculation

The system does not maintain stock through manual quantity updates.

Instead, the current stock is calculated using the records stored in:

```text
Detalle Movimientos Mantenimiento
```

Each inventory movement generates positive and negative quantity records.

```text
Origin       -> Negative Quantity
Destination  -> Positive Quantity
```

The accumulated result of these records represents the current quantity assigned to each department, unit, or employee.

## Example

If the following movements exist:

```text
Product: Extension Cable

Maintenance Department  +10
Maintenance Department   -3
Unit 05                  +3
```

The resulting stock is:

```text
Maintenance Department   7
Unit 05                   3
```

This calculation is based entirely on the movement history.

## Data Flow

```text
Movimientos Mantenimiento
          |
          v
Movement Processing Bot
          |
          v
Detalle Movimientos Mantenimiento
          |
          v
Aggregate Quantities
          |
          v
Current Inventory
          |
          v
AppSheet Stock View
```

## Inventory by Location

The Stock view allows users to identify where products are currently assigned.

### Departments

Displays products and quantities associated with each company department.

### Units

Displays the inventory currently assigned to company vehicles or operational units.

### Personnel

Displays tools, equipment, or products assigned directly to individual employees.

## Read-Only Access

The Stock view is designed exclusively for inventory consultation.

Users cannot:

* Add stock manually.
* Remove stock manually.
* Transfer products.
* Modify quantities directly.

Any inventory change must be performed through the **Movements** module.

```text
Stock View
   |
   +-- View Products
   |
   +-- View Quantities
   |
   +-- View Assignments
   |
   +-- No Direct Editing
```

This ensures that every inventory change generates a corresponding movement record and maintains the integrity of the transaction history.

## Traceability

Because stock is calculated from movement records, every displayed quantity can be linked to its transaction history.

This makes it possible to review:

* How the product entered the inventory.
* Previous locations or assignments.
* Current location.
* Quantity transferred.
* Personnel involved.
* Date and time of each movement.

The Stock view therefore provides the current inventory status, while the movement tables maintain the historical traceability behind each quantity.

