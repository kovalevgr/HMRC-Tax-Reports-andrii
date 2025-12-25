# Module 1 – Modern JavaScript (Through Code)

## Purpose

The purpose of this module is to **align and deepen JavaScript fundamentals** for experienced developers by applying them directly in real project code.

This is **not a theoretical JavaScript course**. Every topic is covered through **practical implementation** that will later be reused in Node.js backend and React frontend modules.

The main goal is to build **correct mental models** around async code, data transformations, and error handling — areas where many Middle developers have gaps.

---

## Task Description

You are implementing the **core shared logic layer** of the POC. This layer is framework‑agnostic and contains:

* Data transformation rules
* Validation helpers
* Utility functions

This code must be:

* Pure
* Predictable
* Testable
* Reusable by both backend and frontend

The focus is not on features, but on **how JavaScript behaves at runtime**.

---

## What We Cover

### 1. JavaScript Execution Model

* Call stack and execution context
* Synchronous vs asynchronous execution
* How `async/await` works under the hood
* Promise resolution order

### 2. Asynchronous JavaScript

* Promises vs async/await
* Error propagation in async code
* Common async anti‑patterns
* Parallel vs sequential execution

### 3. Data Transformation Patterns

* Mapping external API payloads to internal models
* Immutability and pure functions
* Defensive programming for external data
* Handling optional and missing fields

### 4. Functional vs Object‑Oriented Patterns

* When functions are enough
* When objects make sense
* Avoiding unnecessary classes
* Composition over inheritance

### 5. Error Handling Strategy

* Errors vs return values
* Creating domain‑level errors
* Wrapping low‑level errors
* Designing predictable error shapes

### 6. Modern JavaScript Language Features

* Destructuring, spread, rest
* Optional chaining and nullish coalescing
* Default parameters
* ES modules

### 7. Testing as Part of JavaScript

* Unit tests for pure functions
* Testing edge cases
* Writing tests that describe behavior
* Fast feedback loops

---

## Practical Assignments

### Assignment 1 – Data Mapping Utilities

Implement utilities that transform raw HMRC‑like payloads into normalized internal structures:

* Normalize monetary values
* Map income and expense categories
* Handle missing or malformed fields

All logic must be implemented as **pure functions**.

---

### Assignment 2 – Async Utilities

Implement small async helpers:

* Retry wrapper for async functions
* Parallel execution helper with controlled concurrency
* Timeout wrapper for promises

---

### Assignment 3 – Error Modeling

Create a small error hierarchy:

* Base application error
* Validation error
* External service error

Demonstrate how errors are created, wrapped, and consumed.

---

## Questions We Want to Answer

### JavaScript Fundamentals

* How does JavaScript schedule async work?
* What actually happens when `await` is used?
* Why do some errors escape `try/catch`?

### Async Thinking

* When should promises run in parallel?
* How do we avoid hidden race conditions?
* How do we make async code readable?

### Data & Design

* What makes a function predictable?
* Why is immutability important here?
* How do we protect ourselves from external API changes?

### Error Handling

* When should code throw?
* What information should an error carry?
* How do we avoid leaking implementation details?

### Testing Mindset

* What is worth unit‑testing?
* How do tests document behavior?
* Why are fast tests critical at this stage?

---

## Deliverables

* `packages/shared` with:

    * Data mapping utilities
    * Async helpers
    * Error definitions
* Unit tests covering happy paths and edge cases
* Clear module exports and documentation comments

---

## Definition of Done

* All shared logic is framework‑agnostic
* No side effects in mapping logic
* Async helpers behave predictably
* Errors have consistent structure
* Unit tests pass and are readable

---

## Common Pitfalls (Mentor Notes)

* Mixing business logic with framework concerns
* Over‑engineering with classes
* Swallowing errors instead of modeling them
* Writing tests that assert implementation details
* Treating async code as "magic" instead of control flow

---

## Outcome

After this module, the developer should:

* Be confident reasoning about async JavaScript
* Write predictable, testable JS code
* Clearly explain how their code behaves at runtime
* Be ready to move into Node.js backend work with a solid foundation
