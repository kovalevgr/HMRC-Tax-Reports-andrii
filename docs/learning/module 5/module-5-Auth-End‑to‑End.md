# Module 5 – OAuth 2.0 End‑to‑End Flow (React + Node.js)

## Purpose

The purpose of this module is to **implement a real OAuth 2.0 Authorization Code flow end‑to‑end**, covering both frontend and backend responsibilities.

This module is critical because OAuth is:

* conceptually simple but implementation‑heavy
* a common source of security bugs
* frequently misunderstood by Middle developers

The goal is not just to “make OAuth work”, but to **understand why each step exists and where it belongs**.

---

## Task Description

You are integrating **user‑restricted HMRC APIs**, which require OAuth 2.0 Authorization Code flow.

In this module you will:

* Implement the full connect flow (UI → backend → HMRC → backend → UI)
* Store and refresh tokens securely
* Expose a clean, minimal authentication surface to the frontend

At the end of this module, a user can **connect their HMRC account** and the system can reliably obtain and refresh access tokens.

---

## What We Cover

### 1. OAuth 2.0 Fundamentals (Practical)

* Roles: resource owner, client, authorization server, resource server
* Authorization Code flow (why not implicit)
* Access token vs refresh token
* Token lifetime and rotation

### 2. OAuth Flow Architecture

* Why OAuth logic must live in the backend
* Frontend responsibilities vs backend responsibilities
* Redirect‑based flows and state handling
* Preventing CSRF in OAuth flows

### 3. Backend OAuth Implementation

* `/auth/hmrc/start` endpoint
* `/auth/hmrc/callback` endpoint
* Exchanging authorization code for tokens
* Refresh token handling
* Token expiry tracking

### 4. Token Storage Strategy

* Why tokens must not be stored in frontend
* Database schema for OAuth tokens
* Minimal encryption / protection strategy
* Token lifecycle management

### 5. Frontend OAuth Integration

* Initiating OAuth flow from UI
* Handling redirects and temporary state
* Reflecting connection status in UI
* Handling OAuth errors gracefully

### 6. Error Handling & Security Considerations

* Denied consent
* Expired authorization code
* Invalid or revoked tokens
* Logging without leaking secrets

---

## Practical Assignments

### Assignment 1 – OAuth Flow Skeleton

* Implement backend endpoints:

  * `GET /auth/hmrc/start`
  * `GET /auth/hmrc/callback`
* Generate and validate OAuth `state`
* Redirect user correctly through the flow

---

### Assignment 2 – Token Exchange & Storage

* Exchange authorization code for tokens
* Persist tokens securely in database
* Track token expiration

---

### Assignment 3 – Token Refresh Logic

* Implement token refresh mechanism
* Ensure refresh happens transparently
* Handle refresh failures predictably

---

### Assignment 4 – Frontend Integration

* Add "Connect HMRC" action in UI
* Show connection status
* Handle OAuth success and failure states

---

## Questions We Want to Answer

### OAuth Concepts

* Why is Authorization Code flow preferred?
* What problems does the `state` parameter solve?
* Why are refresh tokens sensitive?

### Architecture & Security

* Why should OAuth never be implemented fully in frontend?
* Where should token refresh logic live?
* How do we avoid token leakage?

### Error Handling

* How do OAuth errors differ from business errors?
* What information can safely be shown to users?
* How should errors be logged?

### Engineering Mindset

* Why is OAuth a cross‑cutting concern?
* How do we keep OAuth logic isolated from business logic?
* What would change if we integrated another OAuth provider later?

---

## Deliverables

* Fully working OAuth 2.0 flow
* Token storage schema
* Frontend connect flow
* Clear documentation of OAuth sequence

---

## Definition of Done

* User can successfully connect HMRC account
* Access tokens are obtained and stored securely
* Refresh tokens are handled correctly
* Frontend reflects connection status
* No sensitive data is exposed or logged

---

## Common Pitfalls (Mentor Notes)

* Implementing OAuth logic in the frontend
* Ignoring token refresh until it breaks
* Logging tokens accidentally
* Hard‑coding redirect URLs
* Treating OAuth as "just authentication"

---

## Outcome

After this module, the developer should:

* Clearly understand OAuth 2.0 flows
* Confidently implement secure OAuth integrations
* Be ready to call HMRC APIs in READ/WRITE modules
* Explain OAuth design decisions during interviews
