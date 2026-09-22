# Certificate Validation Automation

Automated system for generating and validating training certificates using **Google Sheets**, **Google Apps Script**, and **QR codes**.

## Description

This project was developed to improve the management and validation of certificates issued for Civil Protection training courses.

Previously, each certificate was created manually. This resulted in two main issues:

* The process required approximately **6 minutes per certificate**.
* Some certificates were later modified, mainly by changing participant names while retaining existing certificate numbers, causing inconsistencies between submitted documents and internal records.

To address these issues, an automated workflow based on **Google Sheets and Google Apps Script** was developed.

## Implemented Solution

Google Sheets serves as the database for storing participant information.

Based on these records, a script developed in Google Apps Script automatically performs the following tasks:

1. Reads the participant data.
2. Assigns the corresponding certificate number.
3. Generates a validation document as a supporting record.
4. Generates a QR code through an API.
5. Links the QR code to the validation document.
6. Generates the certificate.
7. Adds the QR code to the certificate.

This allows the QR code to provide access to the information associated with the certificate and verify that the data matches the record originally generated.

## Certificate Information

Each certificate contains:

* Participant name
* Course
* Company
* Expiration date
* Unique certificate number
* Training hours
* QR code

## Validation Document

The QR code redirects to an automatically generated validation document containing:

* Participant name
* Course
* Company
* Expiration date
* Unique certificate number
* Training hours

The certificate number and the information contained in the validation document make it possible to verify that they correspond to
