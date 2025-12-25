# Module 1 – Tasks Breakdown v2 (Modern JavaScript + TypeScript Through Code)

## Goal

Strengthen **JavaScript language fundamentals** (runtime model, `this`, async), modern ES features, functional/OO patterns, and introduce **TypeScript fundamentals** that will be used in both Node.js and React modules.

> This module is still **practice-first**: every topic is covered via small, reusable code artifacts inside `packages/shared`.

---

## Coverage Map (what is here vs later)

**Covered in Module 1 (here):**

* Execution context, call stack, scope, hoisting
* `this`, `call/apply/bind`
* Primitives vs reference types, immutability
* ES Modules vs CommonJS (concept + practical usage in repo)
* Async JS: event loop, microtasks vs macrotasks, promises, async/await, async error handling
* Modern JS (ES6+): destructuring, rest/spread, template literals, arrow funcs, default params, let/const vs var
* Map/Set/WeakMap/WeakSet (practical use cases)
* Functional patterns: pure functions, side effects, HOFs (map/filter/reduce/flatMap), immutability patterns
* OO-in-JS patterns: composition vs inheritance, factory pattern, mixins
* Error modeling (consistent error shapes)
* TypeScript fundamentals (types, interfaces, aliases, generics, utility types, narrowing, discriminated unions)
* TS project setup basics for shared layer (strict mode, path mapping)

**Covered later (where it belongs):**

* TS in Node runtime specifics (Module 2+ / NestJS module) — tsconfig nuances, runtime loaders, build pipeline choices
* TS in React specifics (Module 3) — component props typing, hooks typing patterns
* Advanced generators/iterators (optional) — can be an add-on task or used when building streaming/pagination later

---

## Task 1.0 – Decide JS/TS baseline & module system

**Description**

* Decide: the repo uses **TypeScript** as the primary language or starts as JS and migrates.
* Decide module system for Node projects (ESM preferred for modern Node; document constraints).

**Deliverables**

* Short `docs/js-ts-baseline.md` with decisions and rationale

**Acceptance criteria**

* Team understands how code is authored and executed (TS compile vs runtime)

**Questions to discuss**

* Why choose TS early vs later?
* ESM vs CJS: what breaks, what improves?

---

## Task 1.1 – Set up `packages/shared` structure & exports

**Description**

* Create `packages/shared` structure (`src/`, public exports).
* Keep **zero framework dependencies**.

**Deliverables**

* `packages/shared` created and imported by `apps/api` and `apps/web`

**Acceptance criteria**

* Imports work from both apps

**Questions to discuss**

* What should be shared FE/BE and what should not?

---

## Task 1.2 – Language Fundamentals kata pack (HMRC domain context)

**Description**
Implement runnable katas/tests that demonstrate JavaScript language fundamentals **using HMRC Draft domain examples**:

* execution context, call stack, scope, hoisting (draft validation helpers)
* `this` binding rules + `call/apply/bind` (method extraction from draft services)
* primitives vs references (mutation bugs in line items arrays)

**Deliverables**

* `katas/language-fundamentals.*` + tests using Draft Report–like objects

**Acceptance criteria**

* Each kata reproduces a realistic bug scenario
* Tests clearly demonstrate why behavior occurs

**Questions to discuss**

* Why does `this` break when a method is passed as callback?
* How do reference mutations corrupt draft data?

---

## Task 1.3 – Async model kata pack (event loop, HMRC‑like calls)

**Description**
Create katas/tests that demonstrate async behavior using **simulated HMRC client calls**:

* microtasks vs macrotasks ordering (Promise vs setTimeout)
* callbacks vs promises vs async/await
* common async error pitfalls (forgotten `await`, unhandled rejections)

**Deliverables**

* `katas/async-model.*` + tests

**Acceptance criteria**

* Deterministic tests proving execution order
* Errors fail tests loudly (no silent failures)

**Questions to discuss**

* Why does `try/catch` sometimes not catch async errors?
* How can lost stack traces complicate debugging integrations?

---

## Task 1.4 – Modern JS features through refactoring

**Description**
Refactor earlier katas and utilities to use:

* destructuring
* rest/spread
* template literals
* default params
* let/const vs var

**Deliverables**

* Updated code using ES6+ consistently

**Acceptance criteria**

* Code is more readable without becoming "clever"

**Questions to discuss**

* When do modern features reduce clarity?

---

## Task 1.5 – Collections: Map/Set/WeakMap/WeakSet (domain‑driven)

**Description**
Implement practical utilities tied to HMRC Draft/Obligations domain:

* `Set` → deduplicate obligations by period key
* `Map` → index draft reports by `periodKey`
* `WeakMap` (optional) → cache normalization results for draft objects

**Deliverables**

* `collections.*` + tests

**Acceptance criteria**

* Correct behavior on realistic domain data
* No accidental memory retention

**Questions to discuss**

* Why is Map safer than plain objects here?
* Why does WeakMap require object keys?

---

## Task 1.6 – Functional patterns utilities (submission pipeline)

**Description**
Implement functional helpers that will later be reused in submission flows:

* `pipe`, `compose`
* mapping pipelines: normalize → validate → enrich
* immutability helpers for draft updates

**Deliverables**

* `fp.*` + tests

**Acceptance criteria**

* All helpers are pure and composable
* No hidden side effects

**Questions to discuss**

* How does composition reduce cognitive load?
* Why immutability simplifies retries and audits?

---

## Task 1.7 – OO‑in‑JS patterns (factories & mixins only)

**Description**
Implement **justified** OO patterns using HMRC Draft domain:

* factory function: `createDraftReport()`
* mixins: `withAuditInfo`, `withValidation`
* avoid deep class hierarchies

**Deliverables**

* `patterns.*` + tests

**Acceptance criteria**

* Patterns clearly outperform plain functions in these cases
* No inheritance chains

**Questions to discuss**

* When do classes add clarity vs hide behavior?

---

## Task 1.8 – Error handling & shared error shapes

**Description**
Define stable error model:

* `AppError` base
* `ValidationError`
* `ExternalServiceError`

Include:

* stable `code`
* safe `message`
* optional `details`

**Deliverables**

* `errors.*` + tests

**Acceptance criteria**

* Errors are serializable and safe

**Questions to discuss**

* Throw vs return Result — what are the trade-offs?

---

## Task 1.9 – Money normalization utilities

**Description**
Implement safe money handling:

* parse/normalize
* rounding
* formatting

**Deliverables**

* `money.*` + tests

**Acceptance criteria**

* No float-based money bugs

**Questions to discuss**

* Why store in minor units?

---

## Task 1.10 – Draft normalization (domain mapping)

**Description**
Pure mapping functions for internal DTO:

* normalize draft report
* normalize line items
* normalize date ranges

**Deliverables**

* `draft-normalization.*` + tests

**Acceptance criteria**

* Stable output shape, defensive parsing

**Questions to discuss**

* How do we protect against schema drift?

---

## Task 1.11 – Async utilities (timeout/retry/concurrency)

**Description**
Implement reusable async helpers:

* `withTimeout`
* `retry` (basic)
* `runWithConcurrency`

**Deliverables**

* `async.*` + tests

**Acceptance criteria**

* Predictable behavior, correct error propagation

**Questions to discuss**

* Why controlled concurrency matters?

---

## Task 1.12 – TypeScript fundamentals + strict setup (domain‑first)

**Description**
Introduce TypeScript using **domain‑driven types**:

* DTOs for DraftReport, LineItem, Money
* discriminated unions for DraftStatus / SubmissionState (preview)
* generics and utility types where they add clarity
* strict `tsconfig` with path aliases

**Deliverables**

* `tsconfig` for `packages/shared`
* Domain types used across utilities and errors

**Acceptance criteria**

* Types prevent invalid draft states at compile time
* No `any` in shared domain logic

**Questions to discuss**

* How do discriminated unions replace runtime checks?
* Where does TypeScript end and runtime validation begin?

---

## Task 1.13 – Unit tests (fast & behavioral)

**Description**
Unit tests for:

* katas
* utilities (money, fp, collections)
* async helpers
* errors

**Deliverables**

* Test suite for `packages/shared`

**Acceptance criteria**

* Deterministic, fast

**Questions to discuss**

* How to avoid testing implementation details?

---

## Task 1.14 – Docs for shared layer

**Description**
Add minimal docs:

* how to use shared utilities
* how to extend safely

**Deliverables**

* `packages/shared/README.md`

**Acceptance criteria**

* Another dev can extend without breaking contracts

---

## Module 1 Definition of Done (final)

* Language fundamentals and async katas exist and are tested
* `packages/shared` provides stable, framework-agnostic utilities
* Error model and money utilities exist and are tested
* Functional utilities and collections utilities exist
* TypeScript basics introduced (strict) and used for DTOs/errors
* All tests pass locally and run fast
