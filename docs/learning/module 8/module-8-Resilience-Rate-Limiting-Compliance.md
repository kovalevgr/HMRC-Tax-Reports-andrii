# Module 8 – Resilience, Rate Limiting & Compliance

## Purpose

The purpose of this module is to **harden the system** against real‑world operational risks and bring the solution closer to **production‑grade engineering**.

This module focuses on:

* Defensive engineering for external dependencies
* Correct handling of rate limits and retries
* Compliance‑driven requirements (HMRC‑specific but generally applicable)
* Designing systems that fail **predictably and safely**

After this module, the system should behave responsibly under stress, partial failures, and external constraints.

---

## Task Description

You are improving the system to operate safely when:

* External APIs throttle requests
* Network calls fail intermittently
* Requests must include compliance‑specific metadata

No new business features are added. The goal is to **strengthen existing flows** (READ and WRITE) so they are robust and compliant.

---

## What We Cover

### 1. Resilience Engineering Fundamentals

* Why external APIs must be assumed unreliable
* Fail fast vs fail safe
* Retry vs no‑retry decisions
* Cascading failures and how to avoid them

### 2. Rate Limiting & Throttling

* Understanding HMRC rate limits (429 semantics)
* Differentiating client‑side vs server‑side limits
* Backoff strategies (exponential, jitter)
* When to retry and when to stop

### 3. Retry Strategy Design

* Retrying READ vs WRITE operations
* Idempotency as a prerequisite for retries
* Handling partial and unknown states
* Circuit breaker concept (introductory)

### 4. Fraud Prevention & Compliance Headers

* Purpose of HMRC fraud prevention headers
* Required Gov‑Client headers (overview)
* Generating and injecting headers centrally
* Keeping compliance logic isolated

### 5. Logging, Redaction & Data Safety

* What must be logged for troubleshooting
* What must never be logged (PII, tokens)
* Log redaction strategies
* Correlation across retries and submissions

### 6. Configuration & Feature Control

* Tuning retry and timeout parameters
* Environment‑specific limits
* Feature flags for compliance features
* Safe defaults

---

## Practical Assignments

### Assignment 1 – Retry & Backoff Middleware

* Implement retry wrapper for HMRC client calls
* Apply exponential backoff with jitter
* Respect HTTP status codes (do not retry blindly)

---

### Assignment 2 – Rate Limit Handling

* Detect and handle 429 responses
* Surface meaningful messages to the UI
* Ensure system does not hammer HMRC

---

### Assignment 3 – Fraud Prevention Headers

* Implement centralized generation of Gov‑Client headers
* Inject headers into all HMRC requests
* Validate presence and format locally

---

### Assignment 4 – Logging & Redaction

* Review all logs touching HMRC flows
* Remove or redact sensitive data
* Ensure correlation IDs flow across retries

---

## Questions We Want to Answer

### Resilience & Reliability

* Which failures should be retried and which should not?
* How do we prevent retry storms?
* How do we design for unknown external states?

### Compliance & Security

* Why are fraud prevention headers mandatory?
* How do we keep compliance logic out of business code?
* What are the risks of leaking metadata?

### Engineering Mindset

* What does "production‑safe" mean for integrations?
* How do we balance resilience with simplicity?
* Which protections are essential vs optional at this stage?

---

## Deliverables

* Retry & backoff implementation
* Rate‑limit aware HMRC client
* Fraud prevention header support
* Sanitized logging
* Configuration options for resilience

---

## Definition of Done

* System respects HMRC rate limits
* Retries behave predictably
* No sensitive data is logged
* Compliance headers are consistently applied
* Failures are visible and actionable

---

## Common Pitfalls (Mentor Notes)

* Retrying WRITE calls without idempotency
* Infinite retry loops
* Logging tokens or personal data
* Spreading compliance logic across the codebase
* Ignoring 429 semantics

---

## Outcome

After this module, the developer should:

* Design resilient integrations
* Handle rate limits correctly
* Implement compliance requirements safely
* Think operationally about system behavior under stress
