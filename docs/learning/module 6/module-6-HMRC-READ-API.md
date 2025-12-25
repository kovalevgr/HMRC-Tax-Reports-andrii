# Module 6 – HMRC READ APIs (Real Data, Real Errors)

## Purpose

The purpose of this module is to implement the first **real integration calls** to HMRC APIs in a safe, structured way.

This module focuses on:

* Turning OAuth tokens into real API calls
* Designing a robust integration layer
* Handling real-world failures (timeouts, 401/403, 429, schema drift)
* Delivering visible value in the UI (obligations + income sources)

After this module, the system should be able to **read data from HMRC reliably** and present it to the user.

---

## Task Description

You are implementing **READ endpoints** against HMRC APIs.

The application must:

* Use the stored OAuth tokens (from Module 5)
* Call HMRC endpoints via the `hmrc-client` boundary
* Map external responses into internal DTOs
* Provide stable REST endpoints for the frontend

At this stage:

* No submissions are made (WRITE comes later)
* The priority is correct integration patterns and error handling

---

## What We Cover

### 1. Integration Layer Implementation

* Implement HTTP client inside `packages/hmrc-client`
* Base URL configuration per environment
* Default headers and request signing requirements (as applicable)
* Timeouts and basic retry policy (placeholder; advanced in later module)

### 2. Contracts & Mapping

* Mapping HMRC payloads to internal DTOs
* Defensive parsing and optional fields
* Schema evolution awareness
* Keeping external models out of application core

### 3. Token Usage & Authorization

* Injecting access tokens into requests
* Handling expired tokens (refresh flow integration)
* Avoiding token leakage in logs

### 4. Failure Modes & Error Handling

* Network failures, timeouts
* 401/403: auth and scope issues
* 404: missing resource vs wrong endpoint
* 429: rate limiting (correct UI message + retry guidance)
* Mapping external errors to internal error categories

### 5. Backend API Design for Frontend

* Stable endpoints:

  * `/hmrc/obligations`
  * `/hmrc/income-sources` (if used)
* Response shaping for UI needs
* Pagination and filtering (optional, as needed)

### 6. UI Integration

* React pages/components to display obligations
* Handling loading / empty / error states
* Error messaging that is useful but safe

---

## Practical Assignments

### Assignment 1 – HMRC Client: HTTP Implementation

Implement HTTP layer inside `packages/hmrc-client`:

* `getObligations()`
* `getIncomeSources()` (if required)

Include:

* Base URL config
* Access token injection
* Timeouts

---

### Assignment 2 – Backend Endpoints

Implement backend endpoints:

* `GET /hmrc/obligations`
* `GET /hmrc/income-sources`

Each endpoint must:

* Validate connection status
* Handle and map errors consistently
* Return stable DTOs for the frontend

---

### Assignment 3 – React UI: Obligations View

Implement UI page:

* Show list of obligations (deadlines)
* Show relevant details in user-friendly format
* Display proper states:

  * Loading
  * Empty
  * Error

---

## Questions We Want to Answer

### Integration & Boundaries

* Why keep HMRC client in a separate package?
* What should the client expose vs hide?
* How do we prevent external schema from leaking into core?

### Authorization & Token Handling

* Where should token refresh happen?
* How do we avoid leaking tokens in logs or errors?
* How do we handle partial failures (some calls succeed, some fail)?

### Error Handling

* How should 401/403 be communicated to the UI?
* How should 429 be handled in UX?
* What is safe to show to users vs only log for developers?

### Engineering Mindset

* What makes an integration “reliable enough” for POC?
* Which failure modes must be handled now vs later?
* How do we keep integration testable?

---

## Deliverables

* Working `hmrc-client` HTTP implementation
* Backend READ endpoints
* UI obligations page
* Documented mapping and error categories

---

## Definition of Done

* User can fetch obligations from HMRC sandbox
* Tokens are used securely
* Errors are handled predictably
* UI displays obligations with correct states
* Integration boundary remains clean

---

## Common Pitfalls (Mentor Notes)

* Calling HMRC directly from controllers
* Returning raw HMRC payloads to frontend
* Logging tokens or sensitive identifiers
* Treating 429 as a generic error
* Hard-coding sandbox URLs and assumptions

---

## Outcome

After this module, the developer should:

* Confidently call external APIs via a clean boundary
* Handle real-world error conditions
* Deliver stable backend contracts to frontend
* Be ready for HMRC WRITE submissions in the next module
