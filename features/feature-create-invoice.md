# Feature: Create Invoice
**Feature ID:** CI
**Branch pattern:** `feature/CI-create-invoice`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Create Invoice
**As a** Company Manager
**I want to** input the term of invoices for a project
**So that** the system automatically creates an invoice when the term ends
**Priority:** P1
**Independent test:** set a test term and see the invoice list be populated
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Populate Invoice
**As a** Company Manager
**I want to** have the workers input their times and work
**So that** the invoice automatically gets populated with invoice line items based on the data
**Priority:** P1
**Independent test:** input a time and description for an invoice and see the list get populated
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST automatically create invoices at given intervals
- **FR-002**: System MUST automatically create invoice line items based on inputted data

---
## Key Entities
- **User**: Company Manager
- **Invoice**: the product; is created by the system
- **Invoice Line Item**: information that goes on an invoice
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Create Invoice
#### Scenario: Invoice is created
* **Given** There is an active project
* **When** The term threshold is reached
* **Then** The system creates an invoice using information from the project

### US-N.2 - Populate Invoice
#### Scenario: Invoice is populated
* **Given** There is an active project
* **When** An invoice is created
* **Then** The logs made by the workers are converted to Invoice Line Items and put on the Invoice

## Data Ownership & Isolation
Invoice data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see Invoice information  |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/<entity>/read` | Yes | Read an Invoice's information |

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays Invoice creation information

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
*   Sending Invoices
*   Contacting anybody