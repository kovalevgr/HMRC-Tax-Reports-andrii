# POC Learning Plan: HMRC Tax Reports (JS + Node.js + React)

## Goal

Build a **production‑like Full‑Stack POC** integrating with HMRC APIs and use it as a practical vehicle to grow **Middle → Middle+** skills in:

- Modern JavaScript
- Node.js backend engineering
- React frontend
- Architecture, security, resilience, testing

The final output is a **working solution**, not just completed lessons.

---

## Deliverables

- Monorepo with:
    - `apps/api` – Node.js backend
    - `apps/web` – React frontend
    - `packages/hmrc-client` – HMRC SDK/client
    - `packages/shared` – DTOs, validation, utilities
    - `docs/` – architecture, flows, ADRs
- Working flows:
    1. HMRC OAuth connect
    2. Read obligations / income sources
    3. Prepare & submit quarterly report
    4. Submission status & audit history

Quality bar:

- Validation, logging, error handling
- Basic security & resilience
- Automated tests
- CI pipeline

---

## Repository Structure (suggested)

```
/apps
  /api
  /web
/packages
  /hmrc-client
  /shared
/docs
/infra
```

---

# Modules

## Module 0 – Project Bootstrap & Dev Environment

**Purpose:** Fast start with production‑like discipline.

**Covers**

- Monorepo setup (workspaces)
- ESLint, Prettier, formatting rules
- Environment configuration strategy
- API skeleton + React skeleton
- Optional Docker Compose (Postgres)

**Deliverables**

- `/health` endpoint
- React app calling backend
- One‑command local startup
- Minimal CI (lint + tests)

**Definition of Done**

- Project runs locally
- No secrets in repo
- Consistent formatting enforced

---

## Module 1 – Modern JavaScript Essentials (Through Code)

**Purpose:** Refresh and align JS fundamentals using real tasks.

**Covers**

- ES modules, imports/exports
- async/await, Promise patterns
- Error propagation
- Functional patterns for data mapping

**Deliverables**

- `packages/shared`:
    - Income & expenses mapping utilities
    - Money normalization helpers
    - Unit tests

**Definition of Done**

- Mapping logic is pure & tested
- Edge cases covered

---

## Module 2 – Node.js Backend Fundamentals (Without NestJS)

**Purpose:** Understand backend architecture and HTTP pipeline.

**Covers**

- Fastify/Express fundamentals
- Layered architecture
- Request validation (Zod)
- Centralized error handling
- Structured logging + correlation IDs
- Basic security hardening

**Deliverables**

- CRUD for "Local Report Drafts"
- Consistent API error format

**Definition of Done**

- Validation errors are predictable
- Logs contain request context
- No unhandled promise rejections

---

## Module 3 – React Fundamentals (POC UI)

**Purpose:** Build a UI that supports the real business flow.

**Covers**

- Routing & layouts
- Server state (TanStack Query)
- Loading / error UX
- Forms & validation

**Deliverables**

- Pages:
    - Dashboard
    - Draft reports list
    - Draft editor

**Definition of Done**

- UI handles errors gracefully
- Frontend validation matches backend

---

## Module 4 – HMRC Sandbox & App Setup

**Purpose:** Prepare stable integration foundation.

**Covers**

- HMRC Developer Hub setup
- Sandbox test users
- API scopes & endpoints selection
- Integration documentation

**Deliverables**

- `docs/hmrc.md` with setup steps

**Definition of Done**

- Any developer can reproduce setup

---

## Module 5 – OAuth2 End‑to‑End Flow

**Purpose:** Implement real‑world authorization flow.

**Covers**

- Authorization Code flow
- Token exchange & refresh
- Secure token storage strategy
- Frontend ↔ backend session model

**Deliverables**

- Auth endpoints (`/auth/hmrc/*`)
- DB schema for HMRC connections

**Definition of Done**

- Token refresh works
- Consent errors handled

---

## Module 6 – HMRC READ APIs

**Purpose:** Provide real value to the user.

**Covers**

- HMRC client abstraction
- Typed DTOs & error mapping
- Caching (optional)
- Rate‑limit friendly calls

**Deliverables**

- Obligations page in UI
- Backend read endpoints

**Definition of Done**

- Clear error mapping to UI
- Upstream correlation IDs logged

---

## Module 7 – HMRC WRITE APIs (Submission Flow)

**Purpose:** Core business functionality.

**Covers**

- Draft → HMRC payload mapping
- Idempotency
- Submission state machine
- Audit logging (no PII)

**Deliverables**

- Submit endpoint
- Submission history
- UI confirmation & status

**Definition of Done**

- End‑to‑end submission works
- No duplicate submissions

---

## Module 8 – Resilience, Security & Compliance

**Purpose:** Practice senior‑level concerns.

**Covers**

- Fraud prevention headers
- Retry & backoff strategies
- Rate limiting
- Secrets & logging hygiene

**Deliverables**

- Middleware/interceptors
- `docs/security.md`

**Definition of Done**

- 429 handled correctly
- Logs sanitized

---

## Module 9 – Testing Strategy

**Purpose:** Build correct test pyramid.

**Covers**

- Unit tests
- Integration tests
- API tests
- Optional E2E flows

**Deliverables**

- Structured test suites
- CI integration

**Definition of Done**

- Deterministic tests
- Clear test ownership

---

## Module 10 – Migration to NestJS

**Purpose:** Show how framework standardizes known concepts.

**Covers**

- Controllers / Providers / Modules
- Guards & Interceptors
- HMRC client as provider

**Definition of Done**

- Same functionality preserved
- Clear comparison with non‑Nest approach

---

## General Rules

- Practice > theory
- Each module ends with working code
- Documentation updated incrementally
- Every feature justified by real use case

