# Feature: Send Invoice
**Feature ID:** SI
**Branch pattern:** `feature/SI-send-invoice`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Send Invoice
**As a** Company Manager
**I want to** do nothing as the system creates invoices for me
**So that** the system automatically sends the invoice to the correct customer
**Priority:** P1
**Independent test:** set a test term and see the invoice list be populated
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST automatically create invoices at given intervals
- **FR-002**: System MUST automatically send invoices to the customers

---
## Key Entities
- **User**: Company Manager
- **Invoice**: the product; is created by the system
- **Customer**: person who the invoice is being sent to
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Send Invoice
#### Scenario: Invoice is created
* **Given** There is an existing invoice
* **When** The invoice has been filled out fully
* **Then** The system automatically sends it to the associated customer

## Data Ownership & Isolation
Invoice data is shared between users
| Rule | Requirement |
|------|-------------|
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
*   Creating Invoices
*   Editing Data