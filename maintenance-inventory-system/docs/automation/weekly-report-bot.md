# Weekly Report Bot

This document describes the scheduled automation used to generate a consolidated weekly report of inventory movements.

## Purpose

The **Weekly Report Bot** provides management with a summarized record of the inventory activity performed during the previous week.

Its main functions are:

* Review weekly inventory movements.
* Consolidate the movement information.
* Generate a PDF report.
* Send the report automatically to management.

## Schedule

The bot runs automatically every:

```text
Monday at 09:00
```

This schedule allows the previous week's inventory activity to be reviewed at the beginning of each new week.

## General Processing Flow

```text
Scheduled Trigger
      |
      v
Monday 09:00
      |
      v
Retrieve Weekly Movements
      |
      v
Compile Movement Information
      |
      v
Generate Consolidated PDF
      |
      v
Send Report to Management
```

## Data Source

The automation retrieves the movement records stored in:

```text
Movimientos Mantenimiento
```

These records contain the general information for each inventory transaction, including:

* Movement ID.
* Date and time.
* Movement type.
* Origin.
* Destination.
* Responsible personnel.
* Reason.
* Observations.
* Supporting documentation.

When required, related product information can also be obtained from the movement detail records.

## Weekly Filtering

The bot filters the movement records according to the reporting period.

Only movements registered within the corresponding weekly range are included in the report.

```text
Movimientos Mantenimiento
          |
          v
Filter by Reporting Period
          |
          v
Weekly Movement Dataset
```

This prevents historical records outside the reporting period from being included in the weekly document.

## Report Content

The generated PDF consolidates the activity performed during the week.

The report can include information such as:

| Field                 | Description                                          |
| --------------------- | ---------------------------------------------------- |
| Movement ID           | Unique identifier of the transaction.                |
| Date and Time         | Date when the movement occurred.                     |
| Movement Type         | Entry, exit, or loan.                                |
| Origin                | Department, unit, or employee providing the product. |
| Destination           | Department, unit, or employee receiving the product. |
| Products              | Products involved in the transaction.                |
| Quantities            | Quantities associated with each product.             |
| Delivery Responsible  | Person responsible for delivering the products.      |
| Receiving Responsible | Person responsible for receiving the products.       |
| Reason                | Reason for the inventory movement.                   |
| Observations          | Additional information related to the transaction.   |

## PDF Generation

Once the weekly records have been collected, the bot generates a consolidated PDF.

```text
Weekly Movements
       |
       v
Report Template
       |
       v
PDF Generation
       |
       v
Weekly Inventory Report
```

The report acts as a centralized record of the inventory activity performed during the reporting period.

## Email Distribution

After the PDF is generated, the bot automatically sends the report to the designated management recipients.

```text
Weekly Inventory Report
          |
          v
Email Distribution
          |
          v
Management
```

This process ensures that management receives periodic visibility into inventory activity without requiring manual report preparation.

## Traceability

Because every record included in the report maintains its original Movement ID, each transaction can be reviewed individually when additional details are required.

```text
Weekly Report
     |
     +-- Movement ID 001
     |
     +-- Movement ID 002
     |
     +-- Movement ID 003
     |
     +-- Movement ID ...
```

Each Movement ID can be used to trace the original movement, associated products, responsible personnel, evidence, and inventory impact.

## Automation Benefits

The Weekly Report Bot provides several operational benefits:

* Eliminates manual weekly report preparation.
* Provides management with regular inventory visibility.
* Consolidates movement activity into a single document.
* Maintains consistent reporting periods.
* Improves auditability of inventory transactions.
* Supports operational and administrative review.

## Final Result

At the end of each weekly execution, the system generates:

```text
Weekly Movement Records
        +
Consolidated PDF Report
        +
Automatic Email Distribution
```

This automation provides a recurring summary of inventory activity and complements the real-time traceability maintained by the inventory system.
::

