# Feature: Maintain Invoices
**Feature ID:** MI
**Branch pattern:** `feature/MI-maintain-invoice`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Add Invoice
**As a** Company Manager
**I want to** input the id, number, date, term, customer id, project id, and status of a new Invoice
**So that** this Invoice's id, number, date, term, customer id, project id, and status gets added to the project
**Priority:** P1
**Independent test:** add a new invoice and see it appear on the project's invoice list screen
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Invoice
**As a** Company Manager
**I want to** select an Invoice for removal
**So that** the project no longer tracks this invoice's id, number, date, term, customer id, project id, and status
**Priority:** P1
**Independent test:** remove an invoice and see it no longer appear on the project's invoice list screen
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Invoice
**As a** Company Manager
**I want to** input new id, number, date, term, customer id, project id, and status for an existing invoice
**So that** this Invoice's id, number, date, term, customer id, project id, and status in the project is updated
**Priority:** P1
**Independent test:** change an existing invoice's information and see it changed on the project's invoice list screen
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit an invoice's id, number, date, term, customer id, project id, and status
- **FR-002**: System MUST store the invoice's id, number, date, term, customer id, project id, and status in a project

---
## Key Entities
- **User**: Company Manager; maintains invoices
- **Invoice**: the product; gets sent to customers
- **Project**: stores the id, number, date, term, customer id, project id, and status of invoices
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Add Invoice
#### Scenario: Manager adds a new Invoice
* **Given** I am prompted to enter id, number, date, term, customer id, project id, and status for a new invoice
* **When** I enter id, number, date, term, customer id, project id, and status for the new invoice
* **Then** The invoice gets added to the provided project

### US-N.2 - Remove Invoice
#### Scenario: Manager removes an Invoice
* **Given** I am prompted to select an invoice for removal
* **When** I select the invoice I wish to remove
* **Then** That invoice is removed from the project and the database

### US-N.3 - Edit Invoice
#### Scenario: Manager changes an Invoice's id, number, date, term, customer id, project id, and status
* **Given** I am prompted to select an invoice and enter new id, number, date, term, customer id, project id, and status
* **When** I select an invoice in the project's invoice list
* **And** enter new id, number, date, term, customer id, project id, and status for the invoice
* **Then** The invoice's new id, number, date, term, customer id, project id, and status is updated in the database

## Data Ownership & Isolation
Invenotry data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see invoice information  |
| **Write scope** | Only logged in Company Managers can edit or remove id, number, date, term, customer id, project id, and status of an invoice if the invoice exists `id` and `req.user.id` |
| **Create scope** | Only logged in Company Managers can create invoices |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/invoice/read` | Yes | Read an invoice's information |
| `POST` | `/invoice/edit` | Yes | Change an invoice's information |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "id": 1,
  "number": 1,
  "date": "01/01/2000",
  "term": "7 days",
  "customer id": 1,
  "project id": 1,
  "status": "pending"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays invoice id, number, date, term, customer id, project id, and status

### [View: Edit Page] — route name `edit`
*   Fields: id, number, date, term, customer id, project id, and status
*   Primary action: **Edit Invoice**.
*   Buttons to save or cancel editing of invoice
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