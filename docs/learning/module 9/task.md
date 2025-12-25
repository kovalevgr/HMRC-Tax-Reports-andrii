# Module 9 – Tasks Breakdown v1 (Testing Strategy – HMRC POC)

## Goal

Build a **pragmatic, production‑oriented testing strategy** for the HMRC POC that gives confidence to change, refactor, and extend the system.

This module focuses on **what to test, where to test, and why**, not on chasing coverage numbers.

Outcome:

* Critical business flows are protected
* External integrations are testable without live HMRC dependency
* Tests are fast, deterministic, and maintainable

---

## Coverage Map (what is here vs earlier modules)

**Covered in Module 9 (here):**

* Test pyramid definition and rules
* Unit tests for domain & shared logic
* Integration tests for backend APIs
* Contract tests for HMRC client
* Submission state machine tests
* Minimal E2E tests for critical flows

**Already covered earlier:**

* Basic unit tests for shared utilities (Module 1)
* Minimal API tests introduced in Modules 2, 6, 7

Module 9 consolidates and hardens all testing layers.

---

## Task 9.0 – Testing baseline & pyramid definition

**Description**
Define and document the testing strategy for the project:

* Unit tests → majority
* Integration tests → fewer, but meaningful
* E2E tests → minimal, critical paths only

Define clear rules:

* what must be unit tested
* what must be integration tested
* what must never be E2E tested

**Deliverables**

* `docs/testing-strategy.md`

**Acceptance criteria**

* Team can explain *why* a test belongs to a specific layer

---

## Task 9.1 – Unit tests hardening (packages/shared)

**Description**
Strengthen unit tests for shared/domain logic:

* money normalization edge cases
* immutability/mutation traps (Draft, LineItems)
* async utilities (timeouts, retries)
* error modeling and serialization

**Deliverables**

* Extended unit test suite for `packages/shared`

**Acceptance criteria**

* Tests are fast and deterministic
* No external dependencies

---

## Task 9.2 – Backend test harness (apps/api)

**Description**
Create a reusable test harness for backend tests:

* start/stop API server programmatically
* isolated test database (SQLite or dedicated test schema)
* seed and cleanup helpers

**Deliverables**

* `apps/api/tests/test-harness.*`

**Acceptance criteria**

* Tests do not depend on local developer state

---

## Task 9.3 – Drafts API integration tests

**Description**
Add integration tests for Draft lifecycle:

* create draft
* list drafts
* update draft
* not found
* validation error shapes

Focus on **API contracts**, not implementation.

**Deliverables**

* `apps/api/tests/drafts.*`

**Acceptance criteria**

* DTO shapes and error codes are stable

---

## Task 9.4 – OAuth backend tests

**Description**
Add backend tests for OAuth logic:

* state generation & TTL validation
* callback rejects invalid/expired state
* token refresh logic
* status and disconnect endpoints

No real HMRC calls.

**Deliverables**

* `apps/api/tests/oauth.*`

**Acceptance criteria**

* OAuth logic works independently of UI

---

## Task 9.5 – HMRC client contract tests

**Description**
Implement contract tests for `packages/hmrc-client` using fixtures:

* successful READ responses
* 401/403/429 mapping
* timeout/network error mapping

Ensure:

* raw HMRC payloads never leak outside client

**Deliverables**

* `packages/hmrc-client/tests/contracts.*`

**Acceptance criteria**

* Contract changes break tests immediately

---

## Task 9.6 – READ integration tests (API → HMRC boundary)

**Description**
Add integration tests for READ endpoints:

* `/hmrc/obligations` happy path
* AUTH_REQUIRED when not connected
* RATE_LIMITED handling
* correlationId propagation

Use stub server or mocked HTTP.

**Deliverables**

* `apps/api/tests/hmrc-read.*`

**Acceptance criteria**

* Tests do not depend on live HMRC sandbox

---

## Task 9.7 – WRITE submission tests (state machine + idempotency)

**Description**
Test submission logic deeply:

* Draft → payload validation
* submission state transitions
* idempotency (same draft + payload hash)
* rejected vs failed mapping

**Deliverables**

* `apps/api/tests/hmrc-write.*`

**Acceptance criteria**

* Duplicate submissions are impossible

---

## Task 9.8 – Resilience behavior tests

**Description**
Add deterministic tests for resilience logic:

* retry classification (READ vs WRITE)
* timeout handling
* 429 Retry-After behavior
* circuit breaker open/half-open states

**Deliverables**

* Resilience test suite

**Acceptance criteria**

* No sleeps or real time delays in tests

---

## Task 9.9 – Minimal E2E tests (Playwright)

**Description**
Implement **only critical flows**:

1. Draft create → edit → list
2. OAuth connect simulation → status shows connected
3. Submit draft (stubbed HMRC) → Accepted / Rejected UI

**Deliverables**

* `apps/web/e2e/*`

**Acceptance criteria**

* E2E tests are stable and few

---

## Task 9.10 – Test execution ergonomics

**Description**
Standardize test commands:

* `npm run test` (unit)
* `npm run test:api` (integration)
* `npm run test:e2e`

Document how to run tests locally.

**Deliverables**

* scripts + `docs/how-to-run-tests.md`

**Acceptance criteria**

* New developer can run tests without guidance

---

## Module 9 Definition of Done (final)

* Test pyramid is clearly defined and followed
* Shared/domain logic is covered by unit tests
* Backend APIs are protected by integration tests
* HMRC client has contract tests
* Submission state machine is tested
* Minimal E2E tests cover critical flows
* Tests are deterministic, fast, and maintainable
