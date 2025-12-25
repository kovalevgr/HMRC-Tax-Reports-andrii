# Module 10 – Tasks Breakdown v1 (NestJS Migration – HMRC POC)

## Goal

Migrate the existing **working Node.js backend** (Modules 2–9) to **NestJS** in a **controlled, low‑risk way**.

This module is **not** about rewriting logic. It is about:

* introducing NestJS concepts (DI, modules, providers)
* preserving existing behavior and contracts
* understanding **when NestJS adds value and when it doesn’t**

Outcome:

* Same API behavior and contracts
* Clear mapping between “plain Node” and NestJS architecture
* Production‑ready NestJS foundation

---

## Coverage Map (what is here vs earlier)

**Covered in Module 10 (here):**

* NestJS project bootstrap
* Mapping existing architecture to NestJS modules
* Dependency Injection with providers
* Controllers, pipes, filters, interceptors
* Config, logging, validation in NestJS way
* Incremental migration strategy

**Already covered earlier:**

* Business logic (Modules 1–8)
* API contracts and tests (Module 9)

---

## Task 10.0 – Migration strategy & success criteria

**Description**
Define migration goals and rules:

* zero behavior change
* no contract changes
* reuse existing domain/services/repositories
* tests must stay green

Define migration order and rollback strategy.

**Deliverables**

* `docs/nestjs-migration-strategy.md`

**Acceptance criteria**

* Team understands *why* we migrate, not just *how*

---

## Task 10.1 – Bootstrap NestJS application

**Description**

* Create `apps/api-nest` using NestJS CLI or manual setup.
* Configure TypeScript, path aliases, eslint.
* Add health endpoint.

**Deliverables**

* Running NestJS app

**Acceptance criteria**

* `/health` endpoint works

---

## Task 10.2 – Map project structure to NestJS modules

**Description**
Create NestJS modules that map 1‑to‑1 with existing bounded contexts:

* DraftsModule
* AuthModule (OAuth)
* HmrcModule (READ/WRITE)
* SubmissionsModule

**Deliverables**

* NestJS module structure

**Acceptance criteria**

* No cross‑module imports of implementation details

---

## Task 10.3 – Dependency Injection with providers

**Description**
Register existing services as NestJS providers:

* repositories
* domain services
* hmrc-client adapter

Avoid rewriting logic — wrap it.

**Deliverables**

* Providers configuration

**Acceptance criteria**

* Services are injectable and testable

---

## Task 10.4 – Controllers migration (HTTP layer)

**Description**
Migrate HTTP endpoints:

* DraftsController
* AuthController
* HmrcReadController
* HmrcWriteController

Ensure:

* same routes
* same DTOs
* same error shapes

**Deliverables**

* NestJS controllers

**Acceptance criteria**

* API contracts identical to pre‑migration version

---

## Task 10.5 – Validation: pipes vs manual validation

**Description**
Introduce NestJS validation layer:

* class‑validator / class‑transformer OR Zod pipe
* map validation errors to existing error format

**Deliverables**

* Validation pipe

**Acceptance criteria**

* Validation behavior unchanged for clients

---

## Task 10.6 – Error handling: filters

**Description**
Replace Express/Fastify error middleware with:

* global ExceptionFilter
* mapping from AppError → HTTP response

**Deliverables**

* Global error filter

**Acceptance criteria**

* Error responses identical to previous backend

---

## Task 10.7 – Middleware → Interceptors

**Description**
Migrate cross‑cutting concerns:

* requestId / correlationId
* logging
* timing

Use NestJS interceptors.

**Deliverables**

* Global interceptors

**Acceptance criteria**

* Logs remain structured and safe

---

## Task 10.8 – Config & secrets management

**Description**
Integrate NestJS ConfigModule:

* env validation
* typed access

Reuse existing config schemas.

**Deliverables**

* ConfigModule setup

**Acceptance criteria**

* App fails fast on invalid config

---

## Task 10.9 – Testing the migration

**Description**
Reuse Module 9 tests:

* integration tests against NestJS app
* contract tests unchanged

No new tests unless needed.

**Deliverables**

* Test suite passing against NestJS backend

**Acceptance criteria**

* Migration confidence backed by tests

---

## Task 10.10 – Performance & DX comparison

**Description**
Evaluate:

* startup time
* request latency
* developer experience

Compare plain Node vs NestJS.

**Deliverables**

* `docs/nestjs-evaluation.md`

**Acceptance criteria**

* Clear understanding of NestJS trade‑offs

---

## Module 10 Definition of Done (final)

* NestJS backend replaces plain Node backend
* All existing API contracts preserved
* Business logic reused, not rewritten
* Tests from Module 9 pass
* Team understands NestJS value and cost
