# Module 10 – NestJS Migration (Standardization & Comparison)

## Purpose

The purpose of this module is to **migrate the existing backend (built “by hand”) into NestJS** to demonstrate:

* How a framework standardizes known concepts (DI, modules, interceptors)
* How the same architecture maps into NestJS primitives
* What improves (DX, structure) and what can get worse (magic, hidden coupling)

This is not a “learn NestJS from zero” module. It is a **comparative engineering module**:

> You already understand the fundamentals. Now you evaluate NestJS as an architectural tool.

---

## Task Description

You already have a working system with:

* Local Draft Reports API
* OAuth integration
* HMRC READ/WRITE
* Resilience & compliance behaviors

Your task is to **preserve the same functionality** while migrating the backend to NestJS.

The migration must:

* Keep API contracts stable (frontend should not require changes)
* Keep integration boundary (`hmrc-client`) intact
* Reuse existing domain logic and DTOs

---

## What We Cover

### 1. Mapping Existing Architecture to NestJS

* Routes → Controllers
* Controllers → Providers (services)
* Repositories as providers
* Config as injectable provider
* Shared code remains framework‑agnostic

### 2. Dependency Injection (DI)

* DI container responsibilities
* Provider lifecycles (singleton vs request scope)
* Managing third‑party clients (HTTP, HMRC client)
* Testing with DI

### 3. Cross‑Cutting Concerns in NestJS

* Middleware vs guards vs interceptors vs pipes
* Validation pipes and schema validation integration
* Exception filters for consistent error format
* Request correlation IDs in interceptors

### 4. Modules and Boundaries

* Feature modules (drafts, auth, hmrc)
* Avoiding "everything in AppModule"
* Exports/imports and dependency direction
* Preventing circular dependencies

### 5. HTTP Client & External Integration

* NestJS HttpModule / custom providers
* Keeping `hmrc-client` isolated
* Retry/backoff and compliance headers via interceptors or wrappers

### 6. Testing in NestJS

* Unit testing providers
* Integration testing controllers
* Overriding providers in tests
* E2E tests using Nest testing utilities

### 7. DX & Operational Considerations

* Logging integration (pino/winston)
* Config validation at bootstrap
* Health checks
* Graceful shutdown hooks

---

## Practical Assignments

### Assignment 1 – NestJS Skeleton

* Create `apps/api-nest` or replace `apps/api`
* Bootstrap NestJS app
* Implement `/health` endpoint

---

### Assignment 2 – Drafts Module Migration

* Create `DraftsModule`
* Implement controller + service + repository providers
* Keep DTOs in `packages/shared`

---

### Assignment 3 – Auth Module Migration

* Create `AuthModule`
* Implement OAuth endpoints
* Store tokens via existing persistence layer

---

### Assignment 4 – HMRC Module Migration

* Create `HmrcModule`
* Integrate `hmrc-client` as provider
* Implement READ/WRITE endpoints
* Apply resilience and compliance behaviors

---

### Assignment 5 – Cross-Cutting Infrastructure

* Implement:

  * global exception filter
  * validation pipeline
  * request correlation interceptor
  * logging integration

---

## Questions We Want to Answer

### Framework Evaluation

* What does NestJS give us that we didn’t have?
* What are the trade-offs of decorator-driven frameworks?
* Where does NestJS hide complexity vs expose it?

### Architecture & Boundaries

* How do we keep the domain framework‑agnostic?
* What boundaries become easier in NestJS?
* Where do circular dependencies appear and why?

### Testing & Maintainability

* Does DI help testing or make it harder?
* What becomes easier/harder with NestJS testing utilities?
* How do we prevent “module explosion”?

### Engineering Mindset

* When should you choose NestJS?
* When is a lighter framework (Fastify/Express) better?
* How do you justify the framework choice to a team?

---

## Deliverables

* NestJS backend implementation
* Stable API contracts (frontend unchanged)
* Feature modules: drafts, auth, hmrc
* Cross-cutting infrastructure (validation, errors, logging)
* Short comparison doc: "Before vs After"

---

## Definition of Done

* All existing flows work with NestJS backend:

  * Draft CRUD
  * OAuth connect + refresh
  * HMRC READ (obligations)
  * HMRC WRITE (submission)
* Error format consistent
* Logging and correlation IDs present
* Tests still pass (at least critical set)
* Frontend does not require API changes

---

## Common Pitfalls (Mentor Notes)

* Rewriting domain logic instead of reusing it
* Putting everything into a single module
* Overusing request-scoped providers
* Creating circular dependencies between modules
* Letting NestJS decorators leak into shared packages

---

## Outcome

After this module, the developer should:

* Understand NestJS deeply (not just usage)
* Map architecture concepts to framework primitives
* Make informed framework choices
* Explain NestJS trade-offs at Middle+/Senior interviews
