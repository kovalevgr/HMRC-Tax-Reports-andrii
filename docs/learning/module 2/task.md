# Module 2 – Tasks Breakdown v3 (HMRC POC – Node.js Runtime, HTTP, Data Access)

## Goal

Build an **integration-ready Node.js backend** for the HMRC POC with:

* solid runtime fundamentals (event loop, non-blocking I/O)
* predictable configuration and dependency management
* a clean HTTP API foundation (routing, middleware, validation, error handling)
* a real data-access layer (SQL baseline + optional NoSQL/Redis overview)

> No HMRC calls yet. This module prepares the backend for OAuth + HMRC integration in later modules.

---

## Coverage Map (what is here vs later)

**Covered in Module 2 (here):**

* Node runtime fundamentals (event loop, libuv, blocking pitfalls)
* CommonJS vs ES Modules in Node (repo decision + practical usage)
* Environment variables & config patterns
* Package/dependency management essentials
* HTTP server foundations: native `http` overview + framework-based API (Express/Fastify)
* Routing, middleware, error middleware
* Request validation
* Data access baseline: relational DB connection + transactions + repository pattern
* ORM/ODM survey (Prisma/TypeORM/Sequelize/Mongoose) with trade-offs
* NoSQL intro: MongoDB + Redis (concepts + when to use)

**Covered later:**

* OAuth endpoints and token storage details (Module 5)
* HMRC client boundary implementation (Modules 4, 6–8)
* NestJS-specific architecture and DI (NestJS module)

---

## Task 2.0 – Backend baseline decisions (runtime + modules)

**Description**

* Confirm Node version baseline for the repo.
* Confirm module system for backend (ESM preferred) and document constraints.
* Define project structure conventions for the backend app.

**Deliverables**

* `docs/backend-baseline.md` (short decisions + rationale)

**Acceptance criteria**

* Team can explain how code is executed (ESM/CJS + TS compilation strategy if used)

**Questions to discuss**

* ESM vs CJS in Node: what breaks (tests, tooling), what improves?

---

## Task 2.1 – Runtime fundamentals kata pack (Node-specific)

**Description**
Create small runnable katas/tests inside `apps/api` (or a dedicated `katas/` folder) that demonstrate:

* event loop + libuv conceptually
* non-blocking I/O vs blocking code
* pitfalls: CPU-heavy loops, sync fs calls, JSON parse on huge payload

**Deliverables**

* `katas/node-runtime.*` + tests

**Acceptance criteria**

* Katas prove behavior (timing/ordering) deterministically

**Questions to discuss**

* What kinds of code block Node and why?
* What should be offloaded (worker threads / queue) vs optimized?

---

## Task 2.2 – Environment configuration (12-factor friendly)

**Description**
Implement environment configuration that will support HMRC later:

* `.env.example` for backend
* config loader (dotenv or native) + validation (Zod)
* required variables: `PORT`, `DATABASE_URL`, `LOG_LEVEL` (placeholders for future: `HMRC_*`)

**Deliverables**

* `config/` module with typed config

**Acceptance criteria**

* App fails fast with clear error if config missing/invalid

**Questions to discuss**

* What belongs in env vars vs code?
* What should never be logged?

---

## Task 2.3 – Package & dependency management hygiene

**Description**

* Standardize dependency rules:

    * direct vs transitive
    * devDependencies boundaries
    * workspace version policy
* Add scripts:

    * `dev`, `build` (if TS), `lint`, `test`

**Deliverables**

* Documented dependency policy (`docs/deps-policy.md`)

**Acceptance criteria**

* Reproducible installs and deterministic lockfile

**Questions to discuss**

* How do dependency upgrades become risky in production?

---

## Task 2.4 – HTTP server baseline: native `http` overview

**Description**

* Implement a tiny demo server using Node’s `http` module:

    * `GET /health`
    * basic request parsing

Purpose: understand fundamentals before using frameworks.

**Deliverables**

* `examples/native-http/` (or `katas/native-http.*`)

**Acceptance criteria**

* Team can explain request lifecycle without framework vocabulary

**Questions to discuss**

* What does a framework actually add on top of `http`?

---

## Task 2.5 – Choose and implement web framework (Express vs Fastify)

**Description**

* Choose Express or Fastify for the API (recommend Fastify for speed + schema-first DX).
* Implement app bootstrap:

    * `/health`
    * base middleware
    * request id

**Deliverables**

* `apps/api` running server

**Acceptance criteria**

* `/health` works
* Request ID present in response headers

**Questions to discuss**

* Express vs Fastify: perf, ecosystem, validation story
* Where does NestJS fit later and why we avoid it now?

---

## Task 2.6 – Routing + middleware + error handling middleware

**Description**
Establish the middleware pipeline:

* request logging (sanitized)
* correlation/request id
* centralized error handler

Define stable error response shape compatible with later HMRC integration.

**Deliverables**

* `middleware/` + error handler

**Acceptance criteria**

* All errors return consistent shape
* No stack traces or secrets in responses

**Questions to discuss**

* What belongs to middleware vs controller vs service?

---

## Task 2.7 – Request validation (schema-first)

**Description**

* Add request validation using Zod (or Fastify schema if chosen).
* Validate:

    * params
    * query
    * body

**Deliverables**

* Validation layer with reusable schemas

**Acceptance criteria**

* Invalid input returns predictable 400 with field details

**Questions to discuss**

* TS types vs runtime validation: why both matter?

---

## Task 2.8 – Data Access: relational DB baseline (PostgreSQL recommended)

**Description**

* Connect to Postgres (or MySQL if preferred).
* Implement migrations.
* Create `draft_reports` table with minimal future-proof fields:

    * `id`, `periodKey` (or dates), `currency`, `lineItems` (JSON), `status`, timestamps

**Deliverables**

* DB setup + migration scripts

**Acceptance criteria**

* App starts and can read/write drafts

**Questions to discuss**

* JSON column vs normalization: what’s the trade-off for this POC?

---

## Task 2.9 – ORM/Query layer decision + implementation

**Description**
Pick one approach (explicitly document why):

* **Prisma** (recommended for DX)
* TypeORM / Sequelize (overview only unless chosen)

Implement repository layer around chosen tool:

* `DraftRepository`
* service uses repository, not ORM directly

**Deliverables**

* Repository interfaces + implementations

**Acceptance criteria**

* Controllers/services have no ORM-specific code

**Questions to discuss**

* Why repository pattern matters before external integrations?

---

## Task 2.10 – Transactions & consistency (submission-ready thinking)

**Description**
Implement at least one transaction example:

* create draft + audit record (or status change + history)

Purpose: prepare for Module 7 submissions and idempotency.

**Deliverables**

* Transaction helper and example usage

**Acceptance criteria**

* Transaction rollback works on failure

**Questions to discuss**

* What operations must be atomic in our future submission flow?

---

## Task 2.11 – NoSQL overview (MongoDB) – optional hands-on

**Description**

* Short architecture review: where Mongo fits vs Postgres in this POC.
* Optional: implement a tiny Mongo-backed repository for a non-critical entity (e.g., “integration logs”)

**Deliverables**

* `docs/nosql-mongo.md` (+ optional code)

**Acceptance criteria**

* Clear decision: use/not use in POC

**Questions to discuss**

* When does document DB outperform relational for our case?

---

## Task 2.12 – Redis overview (caching, rate limiting, idempotency support)

**Description**

* Explain Redis use cases we will need later:

    * caching obligations
    * rate limiting tokens
    * idempotency keys
* Optional: add Redis client wiring and a tiny cache wrapper (no real usage yet)

**Deliverables**

* `docs/redis-use-cases.md` (+ optional wiring)

**Acceptance criteria**

* Team can justify Redis use (or not) before Module 8

**Questions to discuss**

* Cache invalidation risks and ownership

---

## Task 2.13 – Draft Reports CRUD endpoints (API contract)

**Description**
Implement endpoints powering React UI:

* `POST /drafts`
* `GET /drafts`
* `GET /drafts/:id`
* `PUT /drafts/:id`

Include:

* validation
* consistent errors
* repository usage

**Deliverables**

* Working Drafts API

**Acceptance criteria**

* Stable DTOs for frontend
* Correct status codes

**Questions to discuss**

* PUT vs PATCH now vs later

---

## Task 2.14 – Local API tests (contract-focused)

**Description**
Create a minimal integration test suite:

* happy path CRUD
* validation failures
* not found

**Deliverables**

* `apps/api` test suite

**Acceptance criteria**

* Deterministic, fast enough for local dev

---

## Task 2.15 – Backend docs for frontend + future integration

**Description**
Document:

* API endpoints + examples
* error shapes/codes
* config variables
* how to run DB locally

**Deliverables**

* `docs/drafts-api.md`
* `docs/backend-config.md`

**Acceptance criteria**

* Frontend can implement without reading backend internals

---

## Module 2 Definition of Done (final)

* Team can explain Node runtime pitfalls (blocking vs non-blocking)
* Backend has stable HTTP foundation (routing, middleware, errors, validation)
* Relational DB connected, migrations exist, repository pattern implemented
* Transactions demonstrated with a realistic example
* Draft CRUD endpoints implemented and documented
* Minimal API integration tests pass locally
* Mongo/Redis/ORM landscape understood (docs + optional wiring)
