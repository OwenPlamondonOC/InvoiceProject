# Feature: Maintain Customers
**Feature ID:** MC
**Branch pattern:** `feature/ME-maintain-customer`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Add Customer
**As a** Company Manager
**I want to** input the id, name, address, number, main contact, and billing terms of a new Customer
**So that** this Customer's id, name, address, number, main contact, and billing terms gets added to the company
**Priority:** P1
**Independent test:** add a new customer and see it appear on the company's customer list screen
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Customer
**As a** Company Manager
**I want to** select a Customer for removal
**So that** the company no longer tracks this customer's id, name, address, number, main contact, and billing terms
**Priority:** P1
**Independent test:** remove a customer and see it no longer appear on the company's customer list screen
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Customer
**As a** Company Manager
**I want to** input new id, name, address, number, main contact, and billing terms for an existing customer
**So that** this Customer's id, name, address, number, main contact, and billing terms in the company is updated
**Priority:** P1
**Independent test:** change an existing customer's information and see it changed on the company's customer list screen
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit a customer's id, name, address, number, main contact, and billing terms
- **FR-002**: System MUST store the customer's id, name, address, number, main contact, and billing terms in a company

---
## Key Entities
- **User**: Company Manager; maintains customers
- **Customer**: Entity to send invoices to
- **Company**: stores the id, name, address, number, main contact, and billing terms of customers
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Add Customer
#### Scenario: Manager adds a new Customer
* **Given** I am prompted to enter id, name, address, number, main contact, and billing terms for a new customer
* **When** I enter id, name, address, number, main contact, and billing terms for the new customer
* **Then** The customer gets added to the provided company

### US-N.2 - Remove Customer
#### Scenario: Manager removes a Customer
* **Given** I am prompted to select a customer for removal
* **When** I select the customer I wish to remove
* **Then** That customer is removed from the company and the database

### US-N.3 - Edit Customer
#### Scenario: Manager changes a Customer's id, name, address, number, main contact, and billing terms
* **Given** I am prompted to select a customer and enter new id, name, address, number, main contact, and billing terms
* **When** I select a customer in the company's customer list
* **And** enter new id, name, address, number, main contact, and billing terms for the customer
* **Then** The customer's new id, name, address, number, main contact, and billing terms is updated in the database

## Data Ownership & Isolation
Invenotry data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see customer information  |
| **Write scope** | Only logged in Company Managers can edit or remove id, name, address, number, main contact, and billing terms of a customer if the customer exists `id` and `req.user.id` |
| **Create scope** | Only logged in Company Managers can create customers |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/customer/read` | Yes | Read a customer's information |
| `POST` | `/customer/edit` | Yes | Change a customer's information |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "id": 1,
  "name": "Customer",
  "address": "09876 example ln.",
  "number": "999-888-7777",
  "contact": "customer@example.com",
  "billing terms": "$$$"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays customer id, name, address, number, main contact, and billing terms

### [View: Edit Page] — route name `edit`
*   Fields: id, name, address, number, main contact, and billing terms
*   Primary action: **Edit Customer**.
*   Buttons to save or cancel editing of customer
*   Verify pressing of save or cancel button

---

## Definition of Done

*   [ ] Backend and frontend implemented per this spec (**FR-00N** satisfied)
*   [ ] **Success Criteria (SC-00N)** met
*   [ ] `features/reference/data-model.md` updated (if schema changed)
*   [ ] `features/reference/api.md` updated (if API changed)
*   [ ] `features/reference/behavior.md` updated (if product rules changed)

---

## Out of Scope

*   User Authorization
* Adding, editing, or deleting any data not listed