# System Design Document
## 1. Architecture
AutoCare uses a simple three-layer structure:
1. **Presentation:** Flask/Jinja templates and Bootstrap responsive styling.
2. **Application:** Flask routes validate input and coordinate workflows.
3. **Data/integration:** SQLAlchemy models persist data in SQLite; notification adapter selects mock or Twilio mode.

## 2. Design decisions
- Flask chosen for a lightweight Python web application suitable for a small team.
- SQLite chosen to minimise setup and provide relational persistence.
- SQLAlchemy provides model abstraction and relationship handling.
- Twilio integration is isolated in `app/notifications.py`; mock mode avoids accidental messages during development.
- Payments are records only. No live financial transaction is performed.

## 3. Main workflows
**Register customer and vehicle:** receptionist enters customer details, then vehicle details; vehicle is linked to customer.
**Create job:** receptionist selects a vehicle, records complaint and estimated labour/parts costs.
**Update job:** mechanic selects a valid workflow status; system saves it and calls notification adapter.
**Record payment:** cashier records amount and method; the system stores the entry against the job.

## 4. Database design
Customer 1—many Vehicle; Vehicle 1—many Job; Job 1—many Payment.
Primary keys are integer IDs. Vehicle registration is unique. Foreign keys enforce relationships.

## 5. Security and limitations
Prototype has no login/role-based access, CSRF protection, audit log or production backup mechanism. Do not deploy with real customer data until these are implemented. Change the development secret, enable HTTPS, apply access control and validate deployment configuration before any public hosting.
