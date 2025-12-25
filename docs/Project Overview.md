# HMRC POC – Project Description

## Overview

**HMRC POC** is a **production-like full-stack Proof of Concept** that demonstrates how to integrate a custom application with **HMRC Making Tax Digital (MTD) for Income Tax APIs** for **UK sole traders**.

The project simulates a real business scenario where a user:

1. Connects their HMRC account via OAuth 2.0
2. Reads tax obligations and income sources from HMRC
3. Prepares quarterly income & expense reports
4. Submits reports to HMRC
5. Tracks submission status and audit history

This is **not a demo app**. It is designed to reflect **real integration constraints**, error cases, and compliance requirements.

---

## Business Problem

UK sole traders are required to:

* Submit **quarterly income tax updates** under MTD
* Follow strict API contracts, security rules, and audit requirements
* Handle failures, retries, and idempotency correctly

HMRC APIs:

* Are external and rate-limited
* Require OAuth 2.0 user-restricted access
* Enforce fraud-prevention headers
* Return complex, sometimes non-obvious error responses

The POC addresses these challenges end-to-end.

---

## Scope of the POC

### In Scope

* HMRC OAuth 2.0 Authorization Code flow
* HMRC Sandbox integration
* READ APIs (Obligations, Income Sources)
* WRITE APIs (Quarterly submissions)
* Draft report management
* Submission lifecycle & idempotency
* Error handling, retries, rate-limit handling
* Basic security & audit logging

### Out of Scope (for now)

* Annual / end-of-period submissions
* Multi-taxpayer support
* Production HMRC onboarding
* Accounting system integrations

---

## High-Level Architecture

```
┌───────────────────┐
│   Web Frontend    │
│   (React)         │
└─────────▲─────────┘
          │ REST API
┌─────────┴─────────┐
│   Backend API     │
│   (Node.js /      │
│    later NestJS)  │
├─────────┬─────────┤
│ Domain  │ HMRC    │
│ Logic   │ Client  │
└────┬────┴────┬────┘
     │         │ HTTPS
┌────▼────┐ ┌──▼────────────────┐
│ Database│ │ HMRC Sandbox API  │
│ (Drafts │ │ (MTD for Income  │
│ Tokens  │ │  Tax)             │
│ Logs)   │ └───────────────────┘
└─────────┘
```

---

## Key Components

### Frontend (React)

* User interface for managing draft reports
* HMRC connection flow initiation
* Obligations & submission status views
* Form validation and error UX

Frontend **never talks to HMRC directly**.

---

### Backend API (Node.js → NestJS)

Responsibilities:

* API contract enforcement
* Request validation
* Domain orchestration
* Security & resilience

Key flows:

* `/auth/hmrc/*` – OAuth connect / callback
* `/drafts` – local draft management
* `/hmrc/obligations` – READ APIs
* `/hmrc/submissions` – WRITE APIs

---

### HMRC Client Module

A dedicated integration layer that:

* Encapsulates all HMRC HTTP calls
* Handles authentication headers
* Applies retry & timeout policies
* Maps HMRC errors to internal error models

This module isolates external complexity from the rest of the system.

---

### Data Storage (Conceptual)

* **DraftReport**

    * period
    * income & expenses
    * status

* **HMRCConnection**

    * access token
    * refresh token
    * expiry

* **SubmissionLog**

    * idempotency key
    * HMRC correlation ID
    * state
    * timestamps

No PII is logged.

---

## Key Technical Concerns

### Security

* OAuth 2.0 user-restricted flow
* Secure token storage
* Fraud-prevention headers (Gov-Client-*)
* No sensitive data in logs

### Resilience

* Retry with exponential backoff
* Graceful handling of 401 / 422 / 429 errors
* Idempotent submissions

### Observability

* Correlation IDs propagated end-to-end
* Structured logs
* Clear audit trail for submissions

---

## Why This POC Matters

This project mirrors **real enterprise HMRC integrations**:

* External system you don’t control
* Strict contracts & compliance
* Failure-heavy flows
* Need for correctness over convenience

It demonstrates the ability to:

* Design safe integrations
* Build maintainable full-stack systems
* Evolve architecture (Node → NestJS) without rewrites

---

## Outcome

At the end of the POC, the system:

* Successfully connects to HMRC Sandbox
* Reads real obligations
* Submits quarterly reports
* Handles failures correctly
* Is ready to be extended toward production

This POC represents **production thinking in a controlled environment**.
