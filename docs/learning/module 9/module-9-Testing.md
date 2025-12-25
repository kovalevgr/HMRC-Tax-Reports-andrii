# Module 9 – Testing Strategy (Unit → Integration → E2E)

## Purpose

The purpose of this module is to build a **pragmatic, production‑oriented testing strategy** that supports confident changes, safe refactoring, and reliable integrations.

This module reframes testing from:

> “something we add at the end”

into:

> **an engineering tool for system stability and evolution**.

The focus is not on achieving 100% coverage, but on **testing the right things at the right level**.

---

## Task Description

You are introducing tests into an already working full‑stack system that:

* Integrates with an external API (HMRC)
* Uses OAuth 2.0
* Performs irreversible WRITE operations

Your task is to design and implement a **test pyramid** that:

* Catches bugs early
* Protects critical flows
* Remains fast and maintainable

---

## What We Cover

### 1. Testing Philosophy & Pyramid

* Why the test pyramid exists
* Unit vs integration vs E2E tests
* Cost of tests at different levels
* Avoiding over‑testing and under‑testing

### 2. Unit Testing (Fast & Deterministic)

* What qualifies as a unit test
* Testing pure functions (Module 1)
* Testing error cases and edge cases
* Avoiding mocks where not needed

### 3. Integration Testing (System Boundaries)

* Testing service + repository together
* Testing HTTP endpoints without the frontend
* Database setup and teardown strategies
* Using sandbox / fake external dependencies

### 4. External API Integration Testing

* Testing HMRC client in isolation
* Contract tests vs live sandbox tests
* When to mock and when not to
* Preventing flaky tests

### 5. End‑to‑End (E2E) Testing

* What flows deserve E2E tests
* Happy path vs failure scenarios
* Keeping E2E tests minimal and valuable
* Avoiding UI‑heavy brittle tests

### 6. Testing OAuth Flows

* Testing OAuth callback handling
* Simulating expired tokens
* Verifying refresh logic
* Ensuring secure handling in tests

### 7. Test Data & Isolation

* Managing test data lifecycles
* Avoiding shared state between tests
* Deterministic data generation

---

## Practical Assignments

### Assignment 1 – Unit Test Coverage

* Add unit tests for:

    * Data mapping utilities
    * Validation logic
    * Error modeling

---

### Assignment 2 – Backend Integration Tests

* Test Draft Reports CRUD endpoints
* Validate request/response contracts
* Verify error scenarios

---

### Assignment 3 – HMRC Client Tests

* Test HMRC client behavior with mocked HTTP responses
* Validate error mapping (401, 403, 429)

---

### Assignment 4 – Critical E2E Flow

Implement one E2E test covering:

* OAuth connect (mocked provider)
* Fetch obligations
* Submit draft (mocked WRITE)

---

## Questions We Want to Answer

### Testing Strategy

* What bugs do we want to catch early?
* Which tests protect business‑critical flows?
* What should never be tested at E2E level?

### Reliability & Maintenance

* Why do some test suites become unmaintainable?
* How do we keep tests fast as the system grows?
* How do we prevent flaky tests?

### External Integrations

* How do we test external API logic safely?
* When is sandbox testing justified?
* How do we trust tests without calling real services?

### Engineering Mindset

* How do tests enable refactoring?
* What is the ROI of tests in a POC?
* How do tests support team scalability?

---

## Deliverables

* Unit test suite for shared logic
* Integration tests for backend API
* HMRC client test coverage
* At least one critical E2E flow
* Documented testing strategy

---

## Definition of Done

* Tests are deterministic and repeatable
* Critical flows are protected
* Test pyramid is balanced
* Test suite runs locally without flakiness
* Tests are readable and intentional

---

## Common Pitfalls (Mentor Notes)

* Testing implementation details
* Too many E2E tests
* Mocking everything indiscriminately
* Sharing state between tests
* Treating coverage percentage as a goal

---

## Outcome

After this module, the developer should:

* Design effective testing strategies
* Confidently refactor existing code
* Test complex integrations safely
* Treat tests as a core engineering asset
