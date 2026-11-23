# Software Requirements Specification (SRS)
## AutoCare — Automotive Workshop Management System
**Version:** 1.0 | **Date:** 18 November 2026 | **Status:** Draft for team validation

## 1. Introduction
### 1.1 Purpose
This SRS defines the requirements for AutoCare, a small web application supporting a campus or community automotive repair workshop.
### 1.2 Scope
AutoCare records customers and vehicles, creates repair job cards, tracks job progress, records invoices/payment entries, and sends customer status notifications through an SMS adapter. It is not a full accounting package and does not process live payments.
### 1.3 Intended users
Workshop administrator/receptionist, mechanic, cashier, and project evaluator.
### 1.4 Definitions
- Job card: record of a repair request and its work status.
- SMS adapter: software component that sends or simulates a text notification.
- SQLite: embedded relational database.

## 2. Overall description
### 2.1 Product perspective
A browser-based application with Flask server, SQLite persistence, HTML interface, and optional Twilio SMS service.
### 2.2 User classes
Administrator/receptionist manages customers and vehicles; mechanic updates diagnosis/status; cashier records payments.
### 2.3 Operating environment
Python 3.10+, modern browser, local computer or campus network. Internet is needed only for CDN styling and live Twilio SMS.
### 2.4 Constraints
Small student project; no real payment processing; mock SMS is default; production deployment requires authentication, HTTPS, secret management, backups and security review.
### 2.5 Assumptions
Workshop staff have basic computer skills; customer phone numbers are supplied with consent; each vehicle registration is unique.

## 3. Functional requirements
- **FR-01 Customer registration:** system shall save a customer name and phone number; email is optional.
- **FR-02 Vehicle registration:** system shall associate a vehicle registration, make, model and optional year with a customer.
- **FR-03 Job-card creation:** system shall create a job card for a registered vehicle with complaint and non-negative labour/parts costs.
- **FR-04 Job tracking:** system shall allow a job to move among Received, Diagnosing, In Progress, Ready and Collected.
- **FR-05 Payment recording:** system shall record positive payment amount, method and optional reference against a job.
- **FR-06 Notification:** after a status update, system shall invoke the SMS adapter for the vehicle owner's phone number.

## 4. Non-functional requirements
- **NFR-01 Usability:** common tasks should be accessible from the dashboard in three clicks or fewer.
- **NFR-02 Performance:** dashboard should load within 3 seconds for up to 500 job records on a typical laptop.
- **NFR-03 Data integrity:** registration numbers are unique; required fields cannot be blank; costs and payment amounts cannot be negative/zero respectively.
- **NFR-04 Maintainability:** application logic is separated into routes, models and notification adapter.
- **NFR-05 Portability:** application shall run on Windows, macOS and Linux with Python.
- **NFR-06 Security:** production deployment must use a strong secret, authentication, role-based access, HTTPS, CSRF protection and restricted database access. These controls are identified as production hardening, not fully implemented in this classroom prototype.

## 5. External interface requirements
- User interface: responsive browser UI.
- Database: SQLite relational database.
- External service: Twilio SMS API, enabled only with explicit environment configuration; mock mode is default.
- Payment: records payment method/reference only; no payment gateway call is made.

## 6. Data requirements
Customer(id, name, phone, email); Vehicle(id, registration, make, model, year, customer_id); Job(id, vehicle_id, complaint, diagnosis, status, labour_cost, parts_cost, created_at); Payment(id, job_id, amount, method, reference, paid_at).

## 7. Acceptance criteria
A user can register a customer and vehicle, create a job, update its status, see a notification handled in mock mode, and record a payment. Automated tests pass. Team verifies the system with realistic but non-sensitive sample data.
