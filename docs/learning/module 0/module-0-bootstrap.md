# Module 0 – Project Bootstrap & Dev Environment

## Purpose

The purpose of this module is to **bootstrap the project from scratch** and establish a solid, production‑like development foundation.

This module intentionally avoids business logic. The focus is on **engineering discipline**, tooling, structure, and developer experience. Everything built here will be reused in all following modules.

At the end of this module, the repository should feel like a real project that a new developer can clone, run locally, and immediately understand.

---

## Task Description

You are starting a new Full‑Stack project that will later integrate with external government APIs (HMRC). Before writing any business logic, you must:

* Decide how the project is structured
* Set up tooling that enforces consistency
* Define how configuration and environments are handled
* Create minimal but correct backend and frontend skeletons

The goal is **not speed**, but **correct foundations** that make future development cheaper and safer.

---

## What We Cover

### 1. Repository & Project Structure

* Why we use a monorepo for this POC
* Separation between applications and shared packages
* Folder naming conventions and boundaries
* How this structure scales when the project grows

### 2. Tooling & Code Quality

* ESLint: what problems it solves
* Prettier: formatting vs linting responsibilities
* Resolving ESLint ↔ Prettier conflicts
* EditorConfig for editor‑agnostic consistency
* Git ignore rules and repo hygiene

### 3. Environment & Configuration

* Difference between configuration and code
* Environment variables strategy
* `.env` vs `.env.example`
* What is allowed in local env files
* What must never be committed
* How configuration flows to backend and frontend

### 4. Backend Skeleton

* Minimal Node.js HTTP server
* Application bootstrap sequence
* `/health` endpoint design
* Where startup logic belongs
* Preparing the codebase for middleware, logging, validation

### 5. Frontend Skeleton

* React application bootstrap
* Environment‑specific configuration
* API base URL strategy
* First backend call (`/health`)
* Handling async calls and basic error states

### 6. Local Development Experience (DX)

* Single command to start backend + frontend
* Clear and predictable npm scripts
* Fast feedback loops
* Optional Docker Compose setup (Postgres placeholder)

### 7. Local Quality Gates (No CI Yet)

* Linting and formatting enforced locally
* Tests runnable locally (even if minimal)
* Clear developer scripts

CI/CD is intentionally **out of scope** for this module and will be introduced later, once core JavaScript, Node.js, and React topics are covered.

---

## Questions We Want to Answer

### Architecture & Structure

* Why is a monorepo a good choice here?
* Where should shared code live?
* How do we avoid tight coupling between frontend and backend?

### Tooling Decisions

* What value do ESLint and Prettier provide beyond "style"?
* Who owns code quality: tooling or developers?
* What checks belong locally vs in CI?

### Configuration & Environments

* What is configuration and what is code?
* Which values should be environment‑specific?
* How do we make the project reproducible for another developer?

### Backend Fundamentals

* What is the minimal viable HTTP server?
* Where does application startup logic live?
* How do we prepare for future cross‑cutting concerns?

### Frontend Fundamentals

* How does the frontend know where the backend is?
* How do we avoid hard‑coded environment URLs?

### Engineering Mindset

* What does "production‑like" mean at POC stage?
* Which shortcuts are acceptable now, and which are not?
* How do early decisions affect future refactoring cost?

---

## Deliverables

* Monorepo initialized and documented
* Backend running with `/health` endpoint
* Frontend running and calling backend
* Environment configuration in place
* Linting and formatting enforced
* Local quality gates (linting & tests only)

---

## Definition of Done

* Project starts locally with a single command
* Frontend successfully calls backend `/health`
* ESLint and Prettier are enforced locally
* No secrets committed to the repository
* Repository structure is documented and understandable

---

## Common Pitfalls (Mentor Notes)

* Over‑engineering too early
* Skipping tooling because "it slows us down"
* Mixing configuration with code
* Hard‑coding environment‑specific values
* Treating POC as a throwaway project
