# Module 4 – External API Integration Setup (HMRC Sandbox)

## Purpose

The purpose of this module is to **prepare the system for external API integration** before writing any OAuth or business logic.

This module is about **engineering readiness**, not features. We establish contracts, boundaries, documentation, and integration discipline so that adding OAuth and HMRC API calls in later modules does **not** require refactoring the core system.

After this module, the codebase should be *integration‑ready*.

---

## Task Description

You are preparing the application to integrate with a **government‑grade external API (HMRC)**.

At this stage:

* No OAuth flow is implemented yet
* No real HMRC API calls are made from the application
* The focus is on **setup, isolation, and contracts**

The objective is to ensure that when OAuth and API calls are added later, they fit naturally into the existing architecture.

---

## What We Cover

### 1. External API Integration Mindset

* Differences between internal APIs and external APIs
* Why external APIs must be treated as unreliable
* Contract‑first thinking
* Versioning and backward compatibility concerns

### 2. HMRC Developer Hub & Sandbox

* Creating an application in HMRC Developer Hub
* Understanding sandbox vs production environments
* HMRC test users and test data
* Scopes and permissions overview

### 3. API Discovery & Contract Definition

* Reviewing HMRC API catalogue
* Selecting required endpoints for the POC
* Understanding request/response schemas
* Identifying required headers and metadata

### 4. Integration Boundaries

* Why direct calls from controllers are a bad idea
* Designing an external API client boundary
* Responsibilities of the HMRC client module
* Avoiding vendor lock‑in in application core

### 5. Error & Failure Modeling

* Common failure modes of external APIs
* Network errors, timeouts, rate limits
* Mapping external errors to internal domain errors
* Preparing error categories without implementation

### 6. Configuration & Environment Separation

* Base URLs per environment
* Feature flags for integration enablement
* Safe handling of external credentials
* Configuration validation at startup

---

## Practical Assignments

### Assignment 1 – HMRC App & Sandbox Setup

* Create HMRC Developer Hub application
* Enable sandbox access
* Generate test user credentials
* Document all required setup steps

---

### Assignment 2 – Integration Contract Definition

* Identify HMRC endpoints required for:

    * Obligations (READ)
    * Income sources (READ)
    * Quarterly submission (WRITE)
* Capture request/response shapes (schemas or examples)
* List required headers and query parameters

---

### Assignment 3 – HMRC Client Skeleton

Create `packages/hmrc-client` with:

* Clear public interface (methods, inputs, outputs)
* No HTTP implementation yet
* Typed DTOs and error placeholders

This module must not depend on framework‑specific code.

---

## Questions We Want to Answer

### External Integration

* Why should external APIs be isolated from core logic?
* What happens if an external API changes or is unavailable?
* How do we protect our system from external instability?

### Contracts & Boundaries

* What should the HMRC client expose to the rest of the system?
* What should remain hidden inside the integration layer?
* How do we test integration logic without real API calls?

### Configuration & Security

* Which values are environment‑specific?
* How do we avoid leaking credentials?
* How do we make integration configuration explicit and safe?

### Engineering Mindset

* Why is integration setup a separate module?
* What risks are reduced by doing this work early?
* How does this module reduce future refactoring cost?

---

## Deliverables

* HMRC Developer Hub application (sandbox)
* Documented setup steps (`docs/hmrc-setup.md`)
* Documented API contracts (`docs/hmrc-contracts.md`)
* HMRC client module skeleton
* Configuration placeholders for integration

---

## Definition of Done

* HMRC sandbox app is created and documented
* Required HMRC endpoints are clearly defined
* HMRC client boundary exists in codebase
* No application code depends directly on HMRC details
* System is ready for OAuth implementation

---

## Common Pitfalls (Mentor Notes)

* Mixing integration setup with OAuth logic
* Calling external APIs directly from controllers
* Hard‑coding sandbox URLs
* Treating external APIs as reliable
* Skipping documentation because "it’s just setup"

---

## Outcome

After this module, the developer should:

* Understand how to prepare for external API integration
* Design clean integration boundaries
* Be ready to implement OAuth and HMRC API calls confidently
* Think defensively about third‑party dependencies
