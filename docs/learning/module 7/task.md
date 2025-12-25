# Module 7 – Tasks Breakdown v1 (HMRC WRITE APIs – Submission Flow)

## Goal

Implement **HMRC WRITE** (quarterly submission) end‑to‑end.

Outcome:

* A Draft Report can be transformed into an HMRC submission payload
* Submission is **safe** (idempotent, stateful, auditable)
* React UI supports submit with confirmation + status
* Backend exposes stable submission endpoints and persists lifecycle

---

## Coverage Map (what is here vs later)

**Covered in Module 7 (here):**

* Draft → HMRC payload mapping + validation
* Submission persistence + lifecycle/state machine
* Idempotency strategy
* Backend submission endpoints
* UI submission UX + history

**Covered later:**

* Hardening retries/rate limiting/compliance headers (Module 8)
* Full test pyramid & E2E (Module 9)

---

## Task 7.0 – Confirm WRITE contracts & invariants

**Description**

* Verify selected WRITE endpoints and contract fixtures (Module 4).
* Identify required fields, rounding rules, and error responses.
* Define Draft invariants for submission (what must be present to submit).

**Deliverables**

* Updated contract fixtures + `docs/submission-invariants.md`

**Acceptance criteria**

* Team can list what makes a Draft "submittable"

---

## Task 7.1 – Domain types: SubmissionState & SubmissionRecord

**Description**
Define domain types in `packages/shared`:

* `SubmissionState` discriminated union:

    * `NotSubmitted` | `Submitting` | `Submitted` | `Accepted` | `Rejected` | `Failed`
* `SubmissionRecord` DTO:

    * `id`, `draftId`, `state`, `idempotencyKey`, timestamps
    * safe error details (if rejected)

**Deliverables**

* Shared DTOs and types

**Acceptance criteria**

* Types prevent invalid state transitions at compile time (as much as possible)

---

## Task 7.2 – Persistence: submissions + (optional) submission_events

**Description**
Create DB schema:

* `hmrc_submissions`

    * `id`, `draftId`, `idempotencyKey`
    * `state`, `hmrcCorrelationId` (if provided)
    * `requestPayloadHash` (optional)
    * `responseSummary` (sanitized)
    * timestamps

Optional:

* `hmrc_submission_events` to track transitions and debugging

**Deliverables**

* Migrations + repositories

**Acceptance criteria**

* Submission state is persisted and queryable

---

## Task 7.3 – Payload builder: Draft → HMRC submission payload

**Description**
Implement mapping layer:

* Build payload from Draft domain model
* Apply rounding/format rules
* Validate output against contract (Zod schema)

**Deliverables**

* `buildHmrcSubmissionPayload(draft)` + tests

**Acceptance criteria**

* Payload is deterministic
* Validation failures produce actionable errors

---

## Task 7.4 – Idempotency strategy

**Description**
Define and implement idempotency:

* generate idempotency key per (draftId + stable payload hash)
* persist key with submission record
* ensure resubmission returns existing result if already submitted

**Deliverables**

* Idempotency helper + repository integration

**Acceptance criteria**

* Duplicate submit requests do not create duplicate submissions

**Questions to discuss**

* What happens if HMRC accepted but our response was lost?

---

## Task 7.5 – Submission service (state machine + orchestration)

**Description**
Implement `SubmissionService`:

* validate draft is submittable
* create or fetch submission record (idempotency)
* transition state: NotSubmitted → Submitting
* call `hmrc-client.submitQuarterlyUpdate(...)` with valid access token
* map response into:

    * Submitted/Accepted/Rejected
    * Failed (transport errors)
* persist final state + summary

**Deliverables**

* SubmissionService + state transition helpers

**Acceptance criteria**

* State transitions are explicit and persisted
* Failures do not leave system in ambiguous state without record

---

## Task 7.6 – Backend endpoints: submit + status + history

**Description**
Implement endpoints:

* `POST /hmrc/submissions/:draftId` (submit)
* `GET /hmrc/submissions/:draftId` (latest status)
* `GET /hmrc/submissions?draftId=...` (history)

Rules:

* require OAuth connected
* never expose raw HMRC payloads or tokens

**Deliverables**

* Working submission endpoints

**Acceptance criteria**

* Frontend can submit and poll status

---

## Task 7.7 – Error mapping for WRITE flows (user-actionable)

**Description**
Implement error mapping for submission:

* HMRC validation errors → show user what to fix (field-level, sanitized)
* 401/403 → re-connect
* 429 → wait and retry (later hardening in Module 8)
* unknown → show requestId and generic message

**Deliverables**

* Consistent backend error codes for WRITE

**Acceptance criteria**

* UI can display actionable messaging

---

## Task 7.8 – React UI: submission UX

**Description**
Implement in UI:

* Submit button on Draft page
* Confirmation modal (explicit irreversible action)
* Submission status panel:

    * current state
    * last attempt time
    * rejected reason summary (safe)
* History view (optional)

**Deliverables**

* Submit UX + status UI

**Acceptance criteria**

* User cannot submit silently (must confirm)
* UI handles rejected vs failed differently

---

## Task 7.9 – Observability: audit trail + correlation

**Description**

* Ensure submission logs contain requestId + submissionId
* Save audit event per transition (if events table exists)
* Sanitize payloads (store hashes/summaries, not full payload)

**Deliverables**

* Audit-friendly submission tracking

**Acceptance criteria**

* A submission can be traced end-to-end without storing sensitive data

---

## Task 7.10 – Minimal tests for submission flow

**Description**
Add tests for:

* payload builder validation
* idempotency behavior
* state transitions
* error mapping (rejected vs failed)

Prefer fixtures/stub over live HMRC.

**Deliverables**

* Minimal submission test suite

**Acceptance criteria**

* Deterministic tests

---

## Module 7 Definition of Done (final)

* Draft can be submitted exactly once (idempotent)
* Submission state is persisted and visible
* HMRC validation errors are mapped safely
* UI supports confirm + status
* Audit/correlation is available
* Minimal submission tests pass locally
