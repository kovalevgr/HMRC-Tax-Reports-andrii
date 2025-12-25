# HMRC Third‑Party API – Overview (for HMRC POC)

> This document describes the **external HMRC Developer Hub APIs** used by our HMRC POC, and the key integration rules we must follow.

---

## 1. What is HMRC Developer Hub?

HMRC Developer Hub is HMRC’s public API platform that provides:

* API documentation for HMRC services (REST APIs)
* Sandbox environment for development and testing
* OAuth 2.0 flows for **user‑restricted** access
* Versioning, testing scenarios, error reference guides, and fraud prevention requirements

For our POC we focus on **Income Tax (Making Tax Digital)** (MTD IT) APIs.

---

## 2. Environments

Most HMRC APIs provide two base URLs:

* **Sandbox:** `https://test-api.service.hmrc.gov.uk`
* **Production:** `https://api.service.hmrc.gov.uk`

> In this POC we use **Sandbox** only.

---

## 3. Authentication & Access Model (High-Level)

HMRC uses OAuth 2.0 for user‑restricted endpoints.

Key concepts:

* Our software is registered as an **HMRC application** (client id/secret)
* A user must complete the **OAuth authorisation journey** (HMRC sign-in)
* After successful auth, we receive and store:

    * access token
    * refresh token
    * expiry metadata
* Backend calls HMRC APIs using the access token

Important note:

* **Frontend must not call HMRC directly.** All HMRC calls go through our backend.

---

## 4. Fraud Prevention Headers

For many HMRC APIs, HMRC requires **fraud prevention headers** (Gov-Client-*) on requests.

We will:

* implement header generation in the backend integration layer
* validate our headers during development using HMRC’s **Test Fraud Prevention Headers API**
* treat header generation as a cross-cutting concern (not business logic)

### Test Fraud Prevention Headers API

Purpose:

* validate the **value and format** of fraud prevention headers
* get feedback/warnings during development

Usage pattern:

* `validate` endpoint for immediate feedback
* `validation-feedback` endpoint to inspect the last request made to each endpoint

---

## 5. Creating Sandbox Users for OAuth

Sandbox user‑restricted endpoints require test users.

### Create Test User API

Purpose:

* create **temporary sandbox test users** (individual, organisation, agent)
* includes:

    * HMRC user ID + password (for OAuth sign‑in)
    * service enrolments and tax identifiers

Operational note:

* test users not used for **90 days** may be deleted

---

## 6. Main MTD Income Tax APIs we use in the POC

> Exact endpoint paths are defined in each API’s "Endpoints" section on the Developer Hub.
> Our POC code will wrap these APIs in a dedicated `hmrc-client` integration module.

### 6.1 Business Details (MTD) API

Use cases:

* retrieve detailed info about a customer’s **self‑employment or property business**
* manage / adjust **quarterly reporting period type**

Why we use it:

* discover income sources and business identifiers
* support “quarterly reporting type” scenarios in the UI

### 6.2 Business Income Source Summary (MTD) API (BISS)

Use cases:

* retrieve a year‑to‑date summary of **income and expenditure**

Why we use it:

* show summary views in the UI
* validate internal draft totals vs HMRC-reported aggregates (where applicable)

### 6.3 Self Employment Business (MTD) API

Use cases:

* submit / edit / retrieve a customer’s **annual and quarterly self‑employment summaries**

Why we use it:

* supports our core flow: preparing quarterly data and submitting updates

---

## 7. Testing & Sandbox Behaviour

HMRC Sandbox supports simulation features:

* using **Gov-Test-Scenario** header to force specific behaviours
* some APIs support **stateful and dynamic testing** (per endpoint “Test data” sections)

In our POC we:

* implement “test scenario injection” in `hmrc-client` (dev-only)
* document the scenarios used for happy path and failure path (429, 401, validation errors)

---

## 8. Versioning & Change Management

HMRC APIs are versioned.

* Backwards-incompatible changes result in a **new API version**
* Some versions can be marked as **beta** or **deprecated**

In our POC we:

* pin to specific API versions in the client layer
* isolate HMRC DTO mapping so upgrades do not leak across the codebase
* treat HMRC responses as untrusted inputs (defensive parsing + runtime validation)

---

## 9. Integration Rules in Our Architecture

### The `hmrc-client` boundary

All HMRC calls go through a dedicated integration module responsible for:

* auth headers and token injection
* fraud prevention headers
* retries / timeouts
* idempotency strategy for write flows (if applicable)
* mapping external errors → internal `AppError` model

### Security / Compliance

* never log tokens
* never log sensitive personal data
* include correlation IDs in logs for traceability

---

## 10. Links

* HMRC API Documentation Hub: [https://developer.service.hmrc.gov.uk/api-documentation/docs/api](https://developer.service.hmrc.gov.uk/api-documentation/docs/api)
* Income Tax (MTD) end-to-end service guide: (linked from HMRC hub)
* APIs used in this POC (linked from HMRC hub):

    * Business Details (MTD)
    * Business Income Source Summary (MTD)
    * Self Employment Business (MTD)
    * Create Test User
    * Test Fraud Prevention Headers
