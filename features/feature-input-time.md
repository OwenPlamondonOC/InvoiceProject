# Feature: Input Time
**Feature ID:** IT
**Branch pattern:** `feature/IT-input-time`
**Status:** Draft
**Created:** 2026-11-18

---
## User Stories
### US-N.1: Input Time
**As a** Employee
**I want to** input my time and description for my work
**So that** the system automatically creates an invoice with the data I entered when the term ends
**Priority:** P1
**Independent test:** set a test term and see the invoice list be populated
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

---
## Requirements
### Functional Requirements
- **FR-001**: System MUST accept information from the user
- **FR-002**: System MUST save inputted data

---
## Key Entities
- **User**: Employee
- **Invoice**: the product; is created by the system
- **Invoice Line Item**: information that goes on an invoice
- **Database**: information storage; holds all information

---
## Acceptance Criteria
### US-N.1 - Input Time
#### Scenario: Worker inputs time
* **Given** There is an active project
* **And** A worker has worked on it
* **When** The worker inputs what they worked on and for how long
* **Then** The system saves that data for use in invoice creation

## Data Ownership & Isolation
Invoice data is shared between users
| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see Invoice information  |
| **Create scope** | Only logged in Company Managers and Employees can enter time  |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/<entity>/read` | Yes | Read an Invoice's information |
| `POST` | `/<entity>/create` | Yes | Input time data for an Invoice Line Item |

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`
*   Uses a `MenuBar` to quickly leave page.
*   No text fields
*   Displays Invoice creation information

### [View: Create Page] — route name `create`
*   Uses a `MenuBar` to quickly leave page.
*   Text fields for Type, Description, and Quantity
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
*   Creating Invoices
*   Contacting anybody