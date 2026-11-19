# Feature: Maintain Invoice line items
**Feature ID:** MILI
**Branch pattern:** `feature/MILI-maintain-invoice-line-item`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Add Invoice line item
**As a** Company Manager
**I want to** input the id, invoice id, type, date, description, quantity, rate, and total of a new Invoice line item
**So that** this Invoice line item's id, invoice id, type, date, description, quantity, rate, and total gets added to the invoice
**Priority:** P1
**Independent test:** add a new invoice line item and see it appear on the invoice's invoice line item list screen
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Invoice line item
**As a** Company Manager
**I want to** select an Invoice line item for removal
**So that** the invoice no longer tracks this invoice line item's id, invoice id, type, date, description, quantity, rate, and total
**Priority:** P1
**Independent test:** remove an invoice line item and see it no longer appear on the invoice's invoice line item list screen
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Invoice line item
**As a** Company Manager
**I want to** input new id, invoice id, type, date, description, quantity, rate, and total for an existing invoice line item
**So that** this Invoice line item's id, invoice id, type, date, description, quantity, rate, and total in the invoice is updated
**Priority:** P1
**Independent test:** change an existing invoice line item's information and see it changed on the invoice's invoice line item list screen
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST allow users to add, remove, and edit an invoice line item's id, invoice id, type, date, description, quantity, rate, and total
- **FR-002**: System MUST store the invoice line item's id, invoice id, type, date, description, quantity, rate, and total in a invoice

---
## Key Entities
- **User**: Company Manager; maintains invoice line items
- **Invoice line item**: Entry on an invoice
- **Invoice**: stores the id, invoice id, type, date, description, quantity, rate, and total of invoice line items
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Add Invoice line item
#### Scenario: Manager adds a new Invoice line item
* **Given** I am prompted to enter id, invoice id, type, date, description, quantity, rate, and total for a new invoice line item
* **When** I enter id, invoice id, type, date, description, quantity, rate, and total for the new invoice line item
* **Then** The invoice line item gets added to the provided invoice

### US-N.2 - Remove Invoice line item
#### Scenario: Manager removes an Invoice line item
* **Given** I am prompted to select an invoice line item for removal
* **When** I select the invoice line item I wish to remove
* **Then** That invoice line item is removed from the invoice and the database

### US-N.3 - Edit Invoice line item
#### Scenario: Manager changes an Invoice line item's id, invoice id, type, date, description, quantity, rate, and total
* **Given** I am prompted to select an invoice line item and enter new id, invoice id, type, date, description, quantity, rate, and total
* **When** I select an invoice line item in the invoice's invoice line item list
* **And** enter new id, invoice id, type, date, description, quantity, rate, and total for the invoice line item
* **Then** The invoice line item's new id, invoice id, type, date, description, quantity, rate, and total is updated in the database

## Data Ownership & Isolation
Invenotry data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see invoice line item information  |
| **Write scope** | Only logged in Company Managers can edit or remove id, invoice id, type, date, description, quantity, rate, and total of an invoice line item if the invoice line item exists `id` and `req.user.id` |
| **Create scope** | Only logged in Company Managers can create invoice line items |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/invoice line item/read` | Yes | Read an invoice line item's information |
| `POST` | `/invoice line item/edit` | Yes | Change an invoice line item's information |

**Create / edit success response** (flat JSON, no envelope):
```json
{
  "id": 1,
  "invoice id": 1,
  "type": "service",
  "date": "1/1/2000",
  "description": "made some stuff",
  "quantity": 1,
  "rate": "$1/hr",
  "total": "$3"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays invoice line item id, invoice id, type, date, description, quantity, rate, and total

### [View: Edit Page] — route name `edit`
*   Fields: id, invoice id, type, date, description, quantity, rate, and total
*   Primary action: **Edit Invoice line item**.
*   Buttons to save or cancel editing of invoice line item
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