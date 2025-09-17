# Phase 1: Problem Understanding & Industry Analysis

## Project Title
**EventEase – Smart Event & Venue Management CRM**

## Industry
Event Management & Hospitality

## Problem Statement
Event management companies face frequent challenges such as venue double-bookings, inefficient vendor assignments, delayed payment tracking, and complicated client coordination. These challenges lead to operational inefficiencies, revenue loss, and client dissatisfaction. EventEase aims to address these gaps by creating a Salesforce CRM platform that integrates venue management, vendor assignment, client invoicing, and payment processing with automation and role-based access controls.

## Requirement Gathering

| Stakeholder    | Needs / Pain Points                                                                                          |
| -------------- | ------------------------------------------------------------------------------------------------------------|
| Event Managers | Need real-time venue booking conflict alerts, vendor assignment automation, and event overview              |
| Clients       | Desire transparent booking processes, easy invoice access, and prompt communication                          |
| Vendors        | Require clear event assignments, contract tracking, and performance feedback                                |
| Finance Team   | Require accurate invoicing, payment status tracking, and financial reporting                                 |

## Stakeholder Analysis

| Role           | Description                              | Access Level                                   | Interaction Model                             |
| -------------- | -------------------------------------- | ----------------------------------------------| ---------------------------------------------|
| Event Manager  | Oversees all event logistics            | Full CRUD on Event, Booking, Vendor, Client   | Creates, manages bookings; assigns vendors   |
| Clients        | Book events and services                | Limited to own event and invoice records       | Views bookings, pays invoices                  |
| Vendors        | Service providers (catering, sound, etc.) | Read own assignments and event details         | Updates service status, submits contracts      |
| Finance Team   | Manages invoices and payments           | Read/write on financial objects                 | Generates reports, sends payment reminders    |
| Admin          | System configuration                   | Full admin privileges                           | Manages users, security, and data integrity   |

## Business Process Mapping

1. Inquiry: Client inquiries about event booking.
2. Availability Check: Event Manager checks venue calendar.
3. Booking Creation: Event booked with venue and client info.
4. Vendor Selection: Vendors assigned based on event type.
5. Invoice Generation: Invoice sent post booking confirmation.
6. Payment Tracking: Finance tracks payment status, sends reminders.
7. Event Execution: Event day coordination by Event Manager.
8. Post-Event Closure: Feedback collection and payment closure.

## Industry-Specific Use Case Analysis

- Event management involves complex scheduling, diverse vendor ecosystems, and demanding client expectations.
- Venue double-bookings cause 15-20% revenue loss.
- Vendor mismanagement increases costs by up to 30%.
- Clients demand transparent communications and prompt payments.

## AppExchange Exploration & Justification

| App Name                    | Functionality                     | Limitation for EventEase           |
|-----------------------------|---------------------------------|----------------------------------|
| Event Management by CloudSherpas | Event scheduling and vendor management | Enterprise license cost, complexity |
| Payment Gateway Plugins      | Online payments integration       | Mostly paid, limited customizability  |
| Vendor Management Packages   | Vendor assignments and contracts  | Non-specific to event industry     |

**Justification:** No available apps fully cover EventEase requirements specific to event types, complex vendor relationships, and advanced payment workflows within Salesforce Developer Edition constraints. Custom CRM is necessary.

## Attachments

- Stakeholder_Analysis.pdf: Detailed roles, responsibilities, access needs.
- Business_Process_Maps.pdf: Visual process flow diagrams.
- AppExchange_Review.xlsx: Detailed app assessment and decision matrix.
- Requirement_Gathering_Summary.docx: Consolidated business requirements and pain points.

---
