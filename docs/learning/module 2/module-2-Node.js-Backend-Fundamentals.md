# Module 2 – Node.js Backend Fundamentals (Through Real API)

## Purpose

The purpose of this module is to **build a real backend API using Node.js**, focusing on how things work **under the hood**, not on framework magic.

This module intentionally avoids NestJS. The goal is to:

* Understand the Node.js runtime and HTTP lifecycle
* Build a backend "by hand" with clear layers and responsibilities
* Prepare a solid foundation for later HMRC integration

After this module, the developer should feel confident explaining **how a request flows through the system** and where to place logic, validation, and error handling.

---

## Task Description

You are building the **backend API** that will serve the frontend and later act as a gateway to HMRC APIs.

At this stage, the backend:

* Does NOT talk to HMRC yet
* Manages local domain data (draft reports)
* Focuses on correctness, structure, and predictability

The backend must expose a clean REST API and be designed so that external integrations can be added without refactoring core logic.

---

## What We Cover

### 1. Node.js Runtime Fundamentals

* Node.js process lifecycle
* Event loop (conceptual, not academic)
* Asynchronous I/O and non‑blocking execution
* Graceful startup and shutdown

### 2. HTTP Server & Request Lifecycle

* HTTP request → response flow
* Routing fundamentals
* Middleware pattern (what it really is)
* Request context and correlation IDs

### 3. Backend Architecture (Hands‑On)

* Layered architecture:

  * Routes
  * Controllers
  * Services
  * Repositories
* Why boundaries matter
* Where business logic belongs
* Avoiding "fat controllers"

### 4. Validation & Input Handling

* Request validation using schemas (Zod)
* Validation vs business rules
* Consistent validation error responses
* Defensive handling of external input

### 5. Error Handling Strategy

* Centralized error handling
* Domain errors vs technical errors
* Mapping errors to HTTP responses
* Avoiding error leaks

### 6. Logging & Observability Basics

* Why `console.log` is not enough
* Structured logging concepts
* Request‑scoped logging
* Preparing for future observability

### 7. Security Fundamentals (Baseline)

* Basic HTTP security headers
* CORS strategy (what and why)
* Avoiding common Node.js security pitfalls
* Trust boundaries

---

## Practical Assignments

### Assignment 1 – Backend Skeleton

* Set up Node.js server (Fastify or Express)
* Define application bootstrap
* Implement `/health` endpoint

---

### Assignment 2 – Draft Reports API

Implement CRUD endpoints for **Local Draft Reports**:

* Create draft
* Update draft
* Get draft by id
* List drafts

Each endpoint must:

* Validate input
* Use service & repository layers
* Return consistent responses

---

### Assignment 3 – Error & Logging Infrastructure

* Implement centralized error handler
* Define base application error
* Add request correlation ID
* Log requests and errors consistently

---

## Questions We Want to Answer

### Node.js Fundamentals

* What happens when a request hits the server?
* How does Node.js handle concurrent requests?
* Why is Node.js suitable for I/O‑heavy workloads?

### Architecture & Design

* Why not put logic directly in routes?
* Where should validation live?
* How do we keep the codebase flexible for future integrations?

### Error Handling

* What makes an error "domain" vs "technical"?
* How do we design errors for consumers (frontend)?
* How do we avoid leaking sensitive information?

### Logging & Debugging

* What information should be logged per request?
* How do correlation IDs help debugging?
* What should never be logged?

### Engineering Mindset

* What does "production‑ready" mean at this stage?
* Which trade‑offs are acceptable for a POC?
* How do early architecture choices reduce future refactoring?

---

## Deliverables

* Backend API with clear structure
* Draft Reports REST endpoints
* Centralized error handling
* Structured logging in place
* Documentation of API endpoints

---

## Definition of Done

* Backend runs locally and serves requests
* All endpoints validate input
* Errors are handled consistently
* Logs include request context
* Codebase is ready for HMRC integration

---

## Common Pitfalls (Mentor Notes)

* Mixing routing, business logic, and persistence
* Swallowing errors or returning raw exceptions
* Overusing middleware without understanding it
* Treating logging as an afterthought
* Writing "framework‑driven" instead of "problem‑driven" code

---

## Outcome

After this module, the developer should:

* Understand Node.js request handling deeply
* Be able to design clean backend APIs
* Confidently explain architectural decisions
* Be ready to integrate external APIs in the next modules
