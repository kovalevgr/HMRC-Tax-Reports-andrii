# Module 5 – Tasks Breakdown v1 (OAuth 2.0 End‑to‑End – HMRC POC Context)

## Goal

Implement a **secure OAuth 2.0 Authorization Code flow** end‑to‑end for HMRC:

* React initiatesction: user starts connect flow
* Backend performs redirect orchestration and code exchange
* Tokens are stored securely and refreshed automatically

Outcome:

* A user can connect their HMRC account
* Backend can obtain and refresh access tokens
* Frontend can show connection status

---

## Coverage Map (what is here vs later)

**Covered in Module 5 (here):**

* OAuth start/callback endpoints
* `state` handling + CSRF protection
* Code exchange + token storage schema
* Refresh token lifecycle
* Minimal UI for connect/disconnect + status
* Safe logging + error mapping

**Covered later:**

* Calling HMRC APIs (Module 6)
* WRITE submission flow (Module 7)
* Retry/rate limiting/compliance headers hardening (Module 8)

---

## Task 5.0 – OAuth design decisions (contracts & boundaries)

**Description**

* Decide where OAuth logic lives (backend only).
* Define what the frontend needs:

    * `GET /auth/hmrc/status`
    * `POST /auth/hmrc/disconnect`
    * a redirect URL to start connect
* Confirm that `hmrc-client` stays independent (no OAuth in the client package).

**Deliverables**

* `docs/oauth-design.md`

**Acceptance criteria**

* OAuth responsibilities are clearly separated across FE/BE

**Questions to discuss**

* Why must OAuth tokens never be stored in the browser?

---

## Task 5.1 – Backend config for OAuth (safe defaults)

**Description**
Add validated config variables:

* `HMRC_AUTH_BASE_URL`
* `HMRC_CLIENT_ID`
* `HMRC_CLIENT_SECRET`
* `HMRC_REDIRECT_URL`
* `HMRC_SCOPES`

**Deliverables**

* Config schema validation (Zod) + `.env.example`

**Acceptance criteria**

* App fails fast if config is missing

---

## Task 5.2 – Token storage schema (DB)

**Description**
Create DB schema for OAuth tokens:

* `hmrc_connections` (per user, or single-user for POC)

    * access token (encrypted/obfuscated strategy)
    * refresh token (encrypted/obfuscated strategy)
    * expiresAt
    * scopes
    * createdAt/updatedAt

**Deliverables**

* Migration + repository

**Acceptance criteria**

* Tokens are persisted and can be refreshed

**Questions to discuss**

* What does “secure storage” mean in a POC vs production?

---

## Task 5.3 – OAuth state management

**Description**
Implement `state` generation and validation:

* generate cryptographically strong state
* bind state to session/user
* enforce TTL

Storage options:

* DB or Redis (if introduced)
* in-memory is acceptable only if explicitly accepted as POC limitation

**Deliverables**

* `OAuthStateRepository`

**Acceptance criteria**

* Callback rejects invalid/expired state

**Questions to discuss**

* What attacks does `state` protect against?

---

## Task 5.4 – Backend endpoint: start connect

**Description**
Implement:

* `GET /auth/hmrc/start`

Responsibilities:

* generate state
* build HMRC authorize URL
* redirect user

**Deliverables**

* Working start endpoint

**Acceptance criteria**

* Redirects to HMRC authorize endpoint with correct params

---

## Task 5.5 – Backend endpoint: callback (code exchange)

**Description**
Implement:

* `GET /auth/hmrc/callback`

Responsibilities:

* validate state
* exchange code for tokens
* store tokens
* redirect back to frontend success route

**Deliverables**

* Working callback endpoint

**Acceptance criteria**

* Tokens are stored and connection is established
* Errors map to safe response/redirect

---

## Task 5.6 – Refresh token flow (transparent)

**Description**
Implement token refresh logic:

* a `TokenService` that:

    * returns a valid access token
    * refreshes if expired/near-expiry
* store updated tokens

**Deliverables**

* `TokenService`

**Acceptance criteria**

* API callers always receive a valid access token without handling refresh

**Questions to discuss**

* Where should refresh happen and why?

---

## Task 5.7 – Auth status + disconnect endpoints

**Description**
Implement:

* `GET /auth/hmrc/status` → connected/disconnected + expiry
* `POST /auth/hmrc/disconnect` → deletes tokens

**Deliverables**

* Status + disconnect endpoints

**Acceptance criteria**

* UI can reliably show connection status

---

## Task 5.8 – Frontend: Connect HMRC UI

**Description**
Implement UI elements:

* “Connect HMRC” button
* Connected status indicator
* “Disconnect” action

Flow:

* UI calls backend `/auth/hmrc/status`
* UI redirects browser to `/auth/hmrc/start`

**Deliverables**

* Connection UI

**Acceptance criteria**

* User can connect and see status update

---

## Task 5.9 – Error handling & safe logging

**Description**

* Ensure no tokens are logged.
* Map OAuth errors:

    * denied consent
    * invalid code
    * invalid/expired state
* Provide safe user-facing messages.

**Deliverables**

* Error mapping + sanitized logs

**Acceptance criteria**

* Errors are actionable and safe

---

## Task 5.10 – Minimal tests for OAuth flow

**Description**
Add tests for:

* state generation/validation
* token refresh logic
* callback error mapping

**Deliverables**

* Test suite (unit/integration depending on setup)

**Acceptance criteria**

* Tests are deterministic

---

## Module 5 Definition of Done (final)

* User can connect HMRC account via OAuth
* Tokens are stored and refresh works
* Frontend shows connection status
* OAuth errors handled safely
* Minimal tests cover state + refresh
