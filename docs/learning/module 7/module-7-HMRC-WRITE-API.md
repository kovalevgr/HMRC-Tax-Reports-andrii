# Module 7 – HMRC WRITE APIs (Submission Flow)

## Purpose

The purpose of this module is to implement **WRITE operations** against HMRC APIs — the most critical and risk‑sensitive part of the integration.

This module focuses on:

* Turning local draft data into valid HMRC submission payloads
* Designing a **safe submission flow** (no duplicates, no partial state)
* Handling idempotency, retries, and submission lifecycle
* Providing full transparency via audit and status tracking

After this module, the system should be able to **submit quarterly data to HMRC reliably** and report the result back to the user.

---

## Task Description

You are implementing the **quarterly submission flow**.

The application must:

* Take a locally prepared Draft Report
* Validate and map it into an HMRC‑compatible payload
* Submit it via HMRC WRITE APIs
* Track submission state and history

This module introduces **irreversible operations**, so correctness and safety are more important than speed.

---

## What We Cover

### 1. Submission Flow Architecture

* Difference between READ and WRITE integrations
* Why submissions must be explicit and controlled
* Designing a submission pipeline
* Avoiding side effects and partial writes

### 2. Data Mapping & Validation

* Mapping Draft Report → HMRC submission payload
* Monetary rounding rules and currency handling
* Final validation before submission
* Guarding against malformed or incomplete drafts

### 3. Idempotency Strategy

* Why idempotency is required
* Client‑generated submission identifiers
* Handling retries without duplicate submissions
* Persisting idempotency keys

### 4. Submission State Machine

* Draft → Submitted → Accepted / Rejected / Failed
* Persisted submission state
* Handling in‑progress submissions
* Recovering from failures

### 5. Error Handling & Recovery

* Network and timeout failures
* HMRC validation errors
* Partial failures and unknown states
* When to retry vs when to stop

### 6. Audit Logging & Traceability

* What must be auditable
* Who submitted what and when
* Correlation between draft, submission, and HMRC response
* Avoiding sensitive data in audit logs

### 7. UI Integration

* Submit action in UI
* Submission confirmation
* Submission status and history
* Error feedback that guides user action

---

## Practical Assignments

### Assignment 1 – Submission Payload Builder

* Implement mapping from Draft Report to HMRC payload
* Enforce required fields
* Apply currency and rounding rules

---

### Assignment 2 – Backend Submission Endpoint

Implement backend endpoint:

* `POST /hmrc/submit/:draftId`

The endpoint must:

* Validate draft state
* Generate idempotency key
* Call HMRC WRITE API via `hmrc-client`
* Persist submission record and status

---

### Assignment 3 – Submission State Tracking

* Create submission storage schema
* Track submission lifecycle
* Expose submission status endpoint

---

### Assignment 4 – UI Submission Flow

* Add submit action to Draft UI
* Show confirmation step
* Display submission result and history

---

## Questions We Want to Answer

### WRITE Integration

* Why are WRITE operations more dangerous than READ?
* What happens if submission succeeds but response is lost?
* How do we avoid duplicate submissions?

### Idempotency & State

* What should be idempotent and why?
* How do we design a reliable state machine?
* What is the source of truth for submission state?

### Error Handling

* How do HMRC validation errors differ from transport errors?
* What errors can the user fix vs not fix?
* How do we recover from unknown submission states?

### Engineering Mindset

* Why is explicit submission confirmation important?
* What audit requirements exist even in a POC?
* How do we design this flow so it scales to production?

---

## Deliverables

* Submission payload mapping
* Backend WRITE endpoint
* Submission persistence and state tracking
* UI submission flow and history
* Documented submission lifecycle

---

## Definition of Done

* Draft can be submitted exactly once
* Duplicate submissions are prevented
* Submission state is persisted and visible
* Errors are handled predictably
* Audit trail exists for submissions

---

## Common Pitfalls (Mentor Notes)

* Treating WRITE calls like READ calls
* Ignoring idempotency
* Losing submission state on failures
* Returning raw HMRC errors to users
* Logging sensitive financial data

---

## Outcome

After this module, the developer should:

* Confidently implement irreversible external API operations
* Design idempotent and resilient submission flows
* Handle real‑world failure scenarios
* Be ready to harden the system with resilience and compliance in later modules
