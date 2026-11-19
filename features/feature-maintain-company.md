# Feature: Maintain Companies

**Feature ID:** MC
**Branch pattern:** `feature/MC-maintain-company`
**Status:** Draft
**Created:** 2026-11-18

---

## User Stories

### US-N.1: Add Company

**As a** System Admin
**I want to** input the id, name, address, website, phone number, email, and banking information of a new Company
**So that** this Company's id, name, address, website, phone number, email, and banking information gets added to the database
**Priority:** P1
**Independent test:** add a new company and see it appear on the database's company list screen
**Acceptance scenarios:** see ### US-N.1 under Acceptance Criteria

### US-N.2: Remove Company

**As a** System Admin
**I want to** select a Company for removal
**So that** the database no longer tracks this company's id, name, address, website, phone number, email, and banking information
**Priority:** P1
**Independent test:** remove a company and see it no longer appear on the database's company list screen
**Acceptance scenarios:** see ### US-N.2 under Acceptance Criteria

### US-N.3: Edit Company

**As a** Company Manager
**I want to** input new id, name, address, website, phone number, email, and banking information for an existing company
**So that** this Company's id, name, address, website, phone number, email, and banking information in the database is updated
**Priority:** P1
**Independent test:** change an existing company's information and see it changed on the database's company list screen
**Acceptance scenarios:** see ### US-N.3 under Acceptance Criteria

---

## Requirements

### Functional Requirements

- **FR-001**: System MUST allow users to add, remove, and edit a company's id, name, address, website, phone number, email, and banking information
- **FR-002**: System MUST store the company's id, name, address, website, phone number, email, and banking information in a database

---

## Key Entities

- **User**: System Admin; maintains companies
- **Company**: holds and manages information for all other entities involved with the company
- **Database**: information storage; holds all information

---

## Acceptance Criteria

### US-N.1 - Add Company

#### Scenario: Admin adds a new Company

* **Given** I am prompted to enter id, name, address, website, phone number, email, and banking information for a new company
* **When** I enter id, name, address, website, phone number, email, and banking information for the new company
* **Then** The company gets added to the provided database

### US-N.2 - Remove Company

#### Scenario: Admin removes a Company

* **Given** I am prompted to select a company for removal
* **When** I select the company I wish to remove
* **Then** That company is removed from the database

### US-N.3 - Edit Company

#### Scenario: Admin changes a Company's id, name, address, website, phone number, email, banking information

* **Given** I am prompted to select a company and enter new id, name, address, website, phone number, email, and banking information
* **When** I select a company in the database's company list
* **And** enter new id, name, address, website, phone number, email, and banking information for the company
* **Then** The company's new id, name, address, website, phone number, email, and banking information is updated in the database

## Data Ownership & Isolation

Invenotry data is shared between users

| Rule | Requirement |
|------|-------------|
| **Read scope** | Only logged in Company Managers can see company information  |
| **Write scope** | Only logged in Company Managers can edit or remove id, name, address, website, phone number, email, and banking information of a company if the company exists `id` and `req.user.id` |
| **Create scope** | Only logged in System Admins can create companies |
| **Cross-user access** | Accessing data without sufficient permission levels returns a `404` |
| **UI scope** | UI shows only data returned for the signed-in user |
| **Implementation** | Shared helper in `app/authorization/` — do not duplicate scope in every controller |

## API Requirements

| Method | Endpoint | Auth | Purpose |
|--------|----------|------|---------|
| `POST` | `/company/read` | Yes | Read a company's information |
| `POST` | `/company/edit` | Yes | Change a company's information |

**Create / edit success response** (flat JSON, no envelope):

```json
{
  "id": 1,
  "name": "example",
  "address": "12345 example st.",
  "website": "example.com",
  "phone": "111-222-3333",
  "email": "jdoe@example.com",
  "banking info": "¯\_(ツ)_/¯"
}
```

**Error response:** `{ "message": "Human-readable explanation." }` with appropriate HTTP status.

---

## Screen Requirements

### [View: Read Page] — route name `read`

* Uses a `MenuBar` to quickly leave page.
* No text fields
* Displays company id, name, address, website, phone number, email, and banking information

### [View: Edit Page] — route name `edit`

* Fields: id, name, address, website, phone number, email, and banking information
* Primary action: **Edit Company**.
* Buttons to save or cancel editing of company
* Verify pressing of save or cancel button

---

## Definition of Done

- [ ] Backend and frontend implemented per this spec (**FR-00N** satisfied)
- [ ] **Success Criteria (SC-00N)** met
- [ ] `features/reference/data-model.md` updated (if schema changed)
- [ ] `features/reference/api.md` updated (if API changed)
- [ ] `features/reference/behavior.md` updated (if product rules changed)

---

## Out of Scope

* User Authorization
* Adding, editing, or deleting any data not listed