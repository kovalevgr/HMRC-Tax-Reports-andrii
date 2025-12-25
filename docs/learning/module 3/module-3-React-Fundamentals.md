# Module 3 – React Fundamentals (Through Real UI)

## Purpose

The purpose of this module is to **build a real, minimal, but production‑minded React UI** that supports the backend API and real user flows.

This is **not a React theory module**. The focus is on:

* Thinking in terms of data flow, not components
* Correct separation between UI state and server state
* Predictable side effects and error handling

After this module, the developer should be able to design React applications that are **maintainable, debuggable, and backend‑friendly**.

---

## Task Description

You are implementing the **frontend application** for the POC.

At this stage, the frontend:

* Works only with the local backend API (no HMRC yet)
* Focuses on CRUD flows for Draft Reports
* Acts as a real client, not a demo UI

The goal is to build a UI that clearly reflects backend behavior, handles errors gracefully, and prepares the ground for OAuth and external integrations.

---

## What We Cover

### 1. React Mental Model

* React as a state machine
* Render cycle and re‑render triggers
* Props vs state
* Why "thinking in components" is not enough

### 2. Application Structure

* Folder structure and responsibilities
* Pages vs components vs hooks
* Feature‑based organization
* Avoiding deeply nested component trees

### 3. Routing & Layout

* Client‑side routing
* Layout components
* Error boundaries at page level
* Navigation as part of state

### 4. Server State Management

* Difference between UI state and server state
* Data fetching patterns
* Caching, refetching, and invalidation
* Handling loading, empty, and error states

### 5. Forms & Validation

* Controlled vs uncontrolled inputs
* Form state management
* Client‑side validation strategy
* Keeping frontend validation aligned with backend rules

### 6. Error Handling & UX

* API error mapping
* Global vs local error handling
* User‑friendly error messages
* Avoiding silent failures

### 7. Performance Fundamentals

* Avoiding unnecessary re‑renders
* Stable references and memoization
* When optimization actually matters

---

## Practical Assignments

### Assignment 1 – Application Skeleton

* Set up React application
* Define routing and layout
* Configure environment variables

---

### Assignment 2 – Draft Reports UI

Implement pages:

* Draft reports list
* Create draft
* Edit draft

Each page must:

* Fetch data from backend
* Handle loading, empty, and error states
* Use consistent UI patterns

---

### Assignment 3 – Forms & Validation

* Implement draft form
* Client‑side validation
* Display backend validation errors

---

## Questions We Want to Answer

### React Fundamentals

* When does React re‑render and why?
* What should be stored in state?
* What belongs outside React state?

### Data & Side Effects

* How do we avoid duplicating server state?
* When should data be refetched?
* How do we keep UI consistent with backend state?

### UX & Error Handling

* How should the UI react to backend errors?
* What makes an error message useful?
* How do we avoid confusing UX states?

### Architecture & Design

* How do frontend and backend contracts align?
* How do we prepare UI for future OAuth flow?
* How do we prevent tight coupling to backend implementation?

### Engineering Mindset

* What makes a frontend "production‑ready"?
* Which shortcuts are acceptable at this stage?
* How do UI decisions affect backend evolution?

---

## Deliverables

* React application with clear structure
* Draft Reports CRUD UI
* Consistent data fetching and error handling
* Basic performance hygiene

---

## Definition of Done

* UI works end‑to‑end with backend Draft Reports API
* Loading, empty, and error states handled
* Forms validated and errors shown correctly
* No unnecessary state duplication
* Code is readable and structured

---

## Common Pitfalls (Mentor Notes)

* Treating React as a templating engine
* Duplicating backend logic on the frontend
* Overusing global state
* Ignoring error and empty states
* Premature performance optimization

---

## Outcome

After this module, the developer should:

* Confidently build real React applications
* Correctly manage server state
* Design predictable UI flows
* Be ready for OAuth and external API integration in the next modules
