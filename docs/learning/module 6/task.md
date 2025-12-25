# Module 6 – Tasks Breakdown v1 (HMRC READ APIs – Real Data, Real Errors)

## Goal

Implement **HMRC READ** capabilities end-to-end using the OAuth tokens from Module 5 and the `hmrc-client` boundary from Module 4.

Outcome:

* Backend can call HMRC sandbox READ endpoints reliably
* Errors are mapped predictably (401/403/429/timeouts)
* React UI displays obligations (and optionally income sources)

---

## Coverage Map (what is here vs later)

**Covered in Module 6 (here):**

* Implement HTTP calls inside `packages/hmrc-client`
* Token injection via backend TokenService
* Backend READ endpoints exposing stable DTOs
* UI pages for obligations/income sources
* Failure modes and error UX for READ flows

**Covered later:**

* WRITE submission flow (Module 7)
* Compliance headers, retries, rate limiting hardening (Module 8)
* Full test strategy (Module 9)

---

## Task 6.0 – Confirm contracts & fixtures

**Description**

* Verify selected READ endpoints and contracts captured in Module 4.
* Ensure fixture examples exist for:

    * success response
    * 401/403
    * 429
    * timeout/5xx

**Deliverables**

* Updated `docs/contracts/hmrc/*` (if needed)

**Acceptance criteria**

* Contracts are ready to implement without guessing

---

## Task 6.1 – Implement HMRC HTTP client (inside `packages/hmrc-client`)

**Description**
Add real HTTP implementation for selected READ methods:

* `getObligations(...)`
* `getIncomeSources(...)` (optional)

Requirements:

* base URL configurable
* request headers prepared (leave compliance headers for Module 8)
* no token storage here

**Deliverables**

* `packages/hmrc-client` with HTTP implementation

**Acceptance criteria**

* Client returns stable internal DTOs (no raw HMRC payloads exposed)

---

## Task 6.2 – Integrate TokenService (access token injection)

**Description**
In backend:

* Use TokenService from Module 5 to obtain valid access token
* Inject token into hmrc-client calls

**Deliverables**

* `HmrcService` (backend) using TokenService + hmrc-client

**Acceptance criteria**

* READ calls succeed without frontend knowing about tokens

---

## Task 6.3 – Error mapping for READ flows

**Description**
Map hmrc-client errors into stable backend errors:

* 401/403 → `AUTH_REQUIRED` / `FORBIDDEN`
* 429 → `RATE_LIMITED`
* timeout/network → `HMRC_UNAVAILABLE`
* validation errors → `HMRC_BAD_RESPONSE`

**Deliverables**

* Shared error mapping logic (backend)

**Acceptance criteria**

* Frontend gets consistent error codes and messages

---

## Task 6.4 – Backend endpoints: obligations + income sources

**Description**
Implement stable backend endpoints:

* `GET /hmrc/obligations`
* `GET /hmrc/income-sources` (optional)

Rules:

* require OAuth connection (status check)
* never expose raw tokens

**Deliverables**

* Working READ endpoints

**Acceptance criteria**

* Endpoints return stable DTOs consumable by React

---

## Task 6.5 – React UI: obligations page

**Description**
Implement UI page:

* `ObligationsPage`
* fetch from backend
* show list/table of deadlines
* handle states: loading / empty / error

**Deliverables**

* Obligations UI

**Acceptance criteria**

* UI handles RATE_LIMITED and AUTH_REQUIRED explicitly

---

## Task 6.6 – React UI: income sources page (optional)

**Description**
If included in POC:

* implement `IncomeSourcesPage`
* render list
* consistent error handling

**Deliverables**

* Income sources UI

**Acceptance criteria**

* Uses shared error UX patterns from Module 3

---

## Task 6.7 – Observability: correlation IDs through HMRC calls

**Description**

* Ensure correlation/request ID is included in logs for HMRC calls.
* Log:

    * endpoint name
    * timing
    * status category

No sensitive data.

**Deliverables**

* Improved logs around HMRC calls

**Acceptance criteria**

* A failing HMRC call is traceable by requestId

---

## Task 6.8 – Minimal tests for READ integration

**Description**
Add tests that protect:

* error mapping behavior
* token injection behavior
* hmrc-client parsing for fixtures (contract-level)

Implementation options:

* mock HTTP with fixtures
* or use stub server from Module 4

**Deliverables**

* Minimal test suite for READ flows

**Acceptance criteria**

* Tests are deterministic and do not require live sandbox

---

## Module 6 Definition of Done (final)

* `hmrc-client` can call HMRC sandbox READ endpoints
* Backend exposes stable READ endpoints (obligations/income sources)
* TokenService provides access tokens transparently
* Errors are mapped into stable codes
* React UI displays obligations with correct UX states
* Logs are safe and traceable
* Minimal READ tests exist and pass
