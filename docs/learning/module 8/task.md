# Module 8 – Tasks Breakdown v1 (Resilience, Rate Limiting & Compliance – HMRC POC Context)

## Goal

Harden the system so it behaves **predictably and safely** under real‑world conditions:

* partial failures (timeouts, 5xx)
* rate limiting (429)
* intermittent network issues
* compliance requirements (HMRC fraud prevention headers)
* safe logging (no tokens/PII)

This module upgrades Modules 6–7 (READ/WRITE) from “works” to **production‑grade behavior**.

---

## Coverage Map (what is here vs later)

**Covered in Module 8 (here):**

* Retry policy design (READ vs WRITE)
* Backoff with jitter + retry budget
* Rate-limit handling and UI messaging
* Timeouts and cancellation patterns
* Circuit breaker intro (minimal)
* HMRC fraud prevention headers (Gov-Client-*)
* Redaction rules for logs
* Operational config knobs (env-driven)

**Covered later:**

* Full test pyramid + E2E (Module 9) will extend tests to these behaviors
* Deployment concerns (Module 10 if you add it)

---

## Task 8.0 – Failure modes catalog (project-specific)

**Description**
Create a short catalog of failure modes we must handle for HMRC calls:

* 401/403 (auth/permissions)
* 429 (rate limit)
* 408/timeout + network errors
* 5xx (HMRC unavailable)
* invalid/malformed response

Map each to:

* retry? (yes/no)
* user-facing message
* log level

**Deliverables**

* `docs/hmrc-failure-modes.md`

**Acceptance criteria**

* Team can explain why each case is retried or not

---

## Task 8.1 – Define retry policy (READ vs WRITE)

**Description**
Define explicit retry rules:

* READ endpoints: retry on transient failures (timeouts, some 5xx)
* WRITE endpoints: retry **only if idempotency is guaranteed** (Module 7)
* never retry on 4xx (except 429)

**Deliverables**

* `docs/retry-policy.md` (short)

**Acceptance criteria**

* Policy is clear, minimal, and implementable

---

## Task 8.2 – Implement retry + backoff (with jitter) in one place

**Description**
Implement a single reusable mechanism (preferably inside `hmrc-client`):

* exponential backoff
* jitter
* max attempts
* max total retry time (budget)

**Deliverables**

* `packages/hmrc-client` retry wrapper (or shared `packages/shared/async` extension)

**Acceptance criteria**

* Retries are bounded (no infinite loops)
* Correct classification of retryable vs non-retryable errors

---

## Task 8.3 – Timeouts and abort/cancellation

**Description**
Add timeouts to HMRC calls:

* per-request timeout
* abort ongoing request when timeout triggers

**Deliverables**

* Timeout support in HMRC HTTP layer

**Acceptance criteria**

* Timeouts are configurable
* Timeout errors map to stable error codes

---

## Task 8.4 – Rate limiting: handle 429 responsibly

**Description**
Implement 429 handling:

* parse `Retry-After` if present
* backoff and retry according to policy
* surface user-friendly message to UI

**Deliverables**

* 429-aware handling in HMRC call pipeline

**Acceptance criteria**

* System does not hammer HMRC
* UI gets `RATE_LIMITED` with suggested wait time (if available)

---

## Task 8.5 – Minimal circuit breaker (intro)

**Description**
Implement a minimal circuit breaker for HMRC base URL:

* track recent failures
* open circuit for a cool-down period
* allow half-open probes

**Deliverables**

* Circuit breaker wrapper around HMRC calls

**Acceptance criteria**

* Repeated failures do not cascade into request storms

---

## Task 8.6 – HMRC fraud prevention headers (Gov-Client-*)

**Description**
Implement compliance headers generation and injection:

* central generator module
* inject into every HMRC request
* ensure values are environment-aware and consistent

**Deliverables**

* `packages/hmrc-client` header injection
* `docs/fraud-prevention-headers.md`

**Acceptance criteria**

* Headers are present on all HMRC requests (stub/fixture validated)
* No sensitive data leaks via headers

---

## Task 8.7 – Logging redaction + safe observability

**Description**
Define and implement redaction rules:

* never log access/refresh tokens
* never log full HMRC payloads
* store hashes/summaries instead

Enhance logs for HMRC calls:

* requestId
* submissionId (WRITE)
* endpoint name
* duration
* outcome category

**Deliverables**

* Redaction utilities + logging guidelines `docs/logging-redaction.md`

**Acceptance criteria**

* Logs are helpful for debugging without leaking sensitive data

---

## Task 8.8 – Config knobs for resilience (env-driven)

**Description**
Add config for:

* timeouts
* retry attempts
* backoff base/max
* circuit breaker thresholds
* enable/disable fraud headers (for local stub)

**Deliverables**

* Config schema + `.env.example` updates

**Acceptance criteria**

* System behavior can be tuned per environment

---

## Task 8.9 – UI behavior for resilience states

**Description**
Update React UI to handle:

* RATE_LIMITED (show wait suggestion)
* HMRC_UNAVAILABLE (try later)
* AUTH_REQUIRED (reconnect)
* WRITE: differentiate Rejected vs Failed

**Deliverables**

* UI error mapping updates

**Acceptance criteria**

* User sees actionable messages and next steps

---

## Task 8.10 – Minimal tests for resilience layer

**Description**
Add deterministic tests (prefer stub/fixtures):

* retry/backoff behavior
* timeout behavior
* 429 handling
* circuit breaker opening
* fraud headers present

**Deliverables**

* Test suite covering resilience behaviors

**Acceptance criteria**

* Tests do not require live HMRC sandbox

---

## Module 8 Definition of Done (final)

* Retries are policy-driven and bounded
* Timeouts and cancellation work
* 429 rate limiting handled responsibly
* Circuit breaker prevents cascading failures
* Fraud prevention headers are consistently applied
* Logs are safe (redacted) and traceable (requestId/submissionId)
* Resilience knobs are configurable via env
* UI surfaces actionable resilience states
* Minimal resilience tests pass locally
