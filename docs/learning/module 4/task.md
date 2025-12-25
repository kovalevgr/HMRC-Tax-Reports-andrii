# Module 4 – Tasks Breakdown v1 (HMRC Integration Readiness)

## Goal

Prepare the system for HMRC integration **before** writing OAuth logic or real HMRC calls.

Outcome:

* HMRC sandbox app exists and is documented
* API contracts are captured and versioned
* `hmrc-client` package exists with a clean boundary (no HTTP implementation yet)
* Configuration and error categories are ready for OAuth + READ/WRITE modules

---

## Coverage Map (what is here vs later)

**Covered in Module 4 (here):**

* HMRC Developer Hub setup (sandbox)
* Selecting endpoints and defining contracts
* Creating `packages/hmrc-client` boundary (interfaces, DTOs)
* Error/failure modeling and response mapping plan
* Config placeholders + validation rules for future secrets
* Local “fake HMRC” stub server for development/testing (optional but recommended)

**Covered later:**

* OAuth 2.0 end-to-end implementation (Module 5)
* Real HTTP calls to HMRC READ/WRITE endpoints (Modules 6–7)
* Retries, rate limiting, compliance headers (Module 8)

---

## Task 4.0 – HMRC sandbox setup + documentation

**Description**

* Create an app in HMRC Developer Hub.
* Enable sandbox access.
* Generate test users / credentials.
* Document setup steps for a new developer.

**Deliverables**

* `docs/hmrc-setup.md`

**Acceptance criteria**

* Any dev can reproduce sandbox setup from docs

**Questions to discuss**

* What differs between sandbox and production?

---

## Task 4.1 – Identify POC flows and required HMRC endpoints

**Description**
Define the POC flows and map them to HMRC endpoints:

* Connect account (OAuth – later)
* Read obligations
* Read income sources (if needed)
* Submit quarterly update

Capture:

* HTTP method + path
* required scopes
* required headers
* query params

**Deliverables**

* `docs/hmrc-endpoints.md`

**Acceptance criteria**

* Endpoints list is complete for Modules 5–7

**Questions to discuss**

* Which endpoints are “must have” vs “nice to have”?

---

## Task 4.2 – Contract capture (request/response examples)

**Description**
For each selected endpoint, capture:

* example request
* example response (success)
* known error responses

Store contracts in a versioned location:

* `docs/contracts/hmrc/*.md` or JSON fixtures

**Deliverables**

* Contract docs/fixtures

**Acceptance criteria**

* Frontend and backend can rely on stable shapes

**Questions to discuss**

* How do we keep contracts updated if HMRC changes?

---

## Task 4.3 – Design the integration boundary (`packages/hmrc-client`)

**Description**
Create `packages/hmrc-client` with:

* public interface methods:

    * `getObligations(...)`
    * `getIncomeSources(...)` (optional)
    * `submitQuarterlyUpdate(...)`
* input/output DTOs (no raw HMRC payloads exposed)
* typed error model aligned with shared `AppError` categories

**Deliverables**

* `packages/hmrc-client` skeleton

**Acceptance criteria**

* No framework imports (no Express/Fastify)
* No HTTP implementation yet

**Questions to discuss**

* What belongs in the client boundary vs application services?

---

## Task 4.4 – Error and failure modeling (integration-first)

**Description**
Define error taxonomy for external calls:

* auth problems (401/403)
* rate limiting (429)
* validation errors returned by HMRC
* network/timeout
* unknown/unexpected

Map them to internal stable codes.

**Deliverables**

* `docs/hmrc-errors.md` + typed error union in `hmrc-client`

**Acceptance criteria**

* Every failure mode has a predictable category

**Questions to discuss**

* What can be shown to users vs only logged?

---

## Task 4.5 – Configuration plan (safe defaults)

**Description**
Add config placeholders (no secrets committed):

* sandbox base URL
* OAuth client id/secret placeholders (later)
* required scopes list

Add validation rules for config to fail fast.

**Deliverables**

* `docs/hmrc-config.md`
* config schema placeholders (Zod) in backend

**Acceptance criteria**

* Missing config causes clear startup error

---

## Task 4.6 – Optional: local fake HMRC stub server

**Description**
Create a small local stub server that mimics HMRC:

* endpoints return fixture responses
* can simulate:

    * 401/403
    * 429
    * timeout

Purpose: enable development without relying on sandbox availability.

**Deliverables**

* `apps/hmrc-stub` (optional)

**Acceptance criteria**

* Backend can switch to stub via env var

**Questions to discuss**

* Why are stubs useful even with a sandbox?

---

## Task 4.7 – Integration readiness checklist

**Description**
Create a checklist for Module 5–7 work:

* contracts captured
* error taxonomy defined
* hmrc-client boundary exists
* config placeholders exist

**Deliverables**

* `docs/integration-readiness-checklist.md`

**Acceptance criteria**

* Checklist is actionable and short

---

## Module 4 Definition of Done (final)

* HMRC sandbox setup is documented
* Required endpoints are identified
* Contracts (examples/fixtures) are captured
* `hmrc-client` boundary package exists (interfaces + DTOs)
* Error taxonomy and config plan exist
* (Optional) stub server exists and can simulate failures
* Integration readiness checklist is complete
