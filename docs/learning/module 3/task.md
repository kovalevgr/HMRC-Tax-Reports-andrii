# Module 3 – Tasks Breakdown v1 (React UI – HMRC POC Context)

## Goal

Build a **production-minded React UI** for the HMRC POC that:

* consumes the Draft Reports API (Module 2)
* uses correct **server state vs UI state** patterns
* implements forms + validation + error UX
* prepares the UI for OAuth connect flow (Module 5) and HMRC pages (Modules 6–7)

> Practice-first: everything is implemented through the real Draft Reports flow.

---

## Coverage Map (what is here vs later)

**Covered in Module 3 (here):**

* React mental model (rendering, re-renders, state)
* App structure (feature-based)
* Routing + layouts
* Server state (React Query recommended) + caching/invalidation
* Forms (react-hook-form recommended) + client validation + backend error mapping
* Error UX (global vs local, error boundaries)
* TypeScript in React (props, hooks, component contracts)
* Basic performance hygiene

**Covered later:**

* OAuth connect screens and redirect handling (Module 5)
* HMRC obligations/submissions pages (Modules 6–7)
* E2E tests (Module 9)

---

## Task 3.0 – Frontend baseline decisions (stack & structure)

**Description**

* Confirm React app build tool (Vite recommended).
* Confirm UI stack: minimal CSS (Tailwind optional) or plain CSS modules.
* Confirm data layer: React Query recommended for server state.
* Confirm forms: react-hook-form recommended.
* Document folder conventions (feature modules, shared UI, hooks).

**Deliverables**

* `docs/frontend-baseline.md`

**Acceptance criteria**

* Team can explain why each library exists (no “because everyone uses it”)

**Questions to discuss**

* What is server state vs UI state?
* What do we avoid by using React Query?

---

## Task 3.1 – Project skeleton + env config

**Description**

* Create `apps/web` React app.
* Add `.env.example` for frontend.
* Configure API base URL via env (no hard-coded URLs).

**Deliverables**

* Running React app

**Acceptance criteria**

* App runs locally and can call backend `/health`

---

## Task 3.2 – Routing + layout foundation

**Description**

* Add client-side routing (React Router).
* Implement layout:

    * top navigation
    * main container
    * simple “Not Found” route

**Deliverables**

* Routing structure

**Acceptance criteria**

* Drafts pages have stable URLs (list, create, edit)

**Questions to discuss**

* Route-driven state vs component-driven state

---

## Task 3.3 – API client layer (typed, consistent errors)

**Description**

* Implement a small API client wrapper:

    * base URL
    * JSON parsing
    * consistent error mapping (based on backend error shape from Module 2)
    * request id propagation (read requestId from error responses)

**Deliverables**

* `src/shared/api/*`

**Acceptance criteria**

* All API calls share consistent error behavior

**Questions to discuss**

* Why not call `fetch` directly everywhere?

---

## Task 3.4 – Server state setup (React Query)

**Description**

* Configure QueryClient.
* Define query keys and invalidation strategy.
* Add devtools (optional) for learning.

**Deliverables**

* React Query baseline

**Acceptance criteria**

* Queries are cached and invalidated correctly

**Questions to discuss**

* What triggers refetch? How do we control it?

---

## Task 3.5 – Drafts: list page (contracts + states)

**Description**
Implement `DraftsListPage`:

* fetch drafts list
* render table/list
* handle states: loading / empty / error
* navigation to create/edit

**Deliverables**

* Drafts list UI

**Acceptance criteria**

* UI reacts correctly to backend errors
* No duplicated server state in local component state

---

## Task 3.6 – Drafts: create flow (form + validation)

**Description**
Implement `CreateDraftPage`:

* form using react-hook-form
* client validation aligned with backend rules
* submit mutation
* on success: navigate to edit or list + invalidate queries

**Deliverables**

* Create draft UI

**Acceptance criteria**

* Validation errors are user-friendly
* Backend validation errors are mapped to fields

**Questions to discuss**

* Which validation belongs on FE vs BE?

---

## Task 3.7 – Drafts: edit flow (prefill + optimistic UX)

**Description**
Implement `EditDraftPage`:

* fetch draft by id
* prefill form
* update mutation
* handle “not found” and conflict scenarios

**Deliverables**

* Edit draft UI

**Acceptance criteria**

* Form is resilient to slow networks
* Errors do not break the page (safe UX)

---

## Task 3.8 – Backend error UX mapping (global + local)

**Description**

* Define error presentation strategy:

    * global toast/banner for unexpected errors
    * inline field errors for validation
    * page-level error fallback for not found
* Implement Error Boundary at app root.

**Deliverables**

* Consistent error UX

**Acceptance criteria**

* Users get actionable messages
* Debugging info (requestId) is visible (but not sensitive)

---

## Task 3.9 – TypeScript in React (contracts & hooks)

**Description**

* Type API DTOs using `packages/shared`.
* Type React Query hooks:

    * `useDraftsQuery`
    * `useDraftQuery(id)`
    * `useCreateDraftMutation`
    * `useUpdateDraftMutation`
* Type component props deliberately (no `any`).

**Deliverables**

* Typed hooks + typed UI contracts

**Acceptance criteria**

* Type errors prevent invalid UI usage

**Questions to discuss**

* Where does runtime validation still matter in FE?

---

## Task 3.10 – Basic performance hygiene

**Description**

* Avoid unnecessary re-renders:

    * stable callbacks where needed
    * avoid derived state duplication
* Use memoization only when justified.

**Deliverables**

* A short note in code (or docs) explaining what was optimized and why

**Acceptance criteria**

* No premature micro-optimizations

---

## Task 3.11 – Minimal UI docs

**Description**
Document:

* page routes
* how to run frontend
* API base URL config
* how errors are displayed

**Deliverables**

* `docs/frontend.md`

**Acceptance criteria**

* Another dev can extend UI features consistently

---

## Module 3 Definition of Done (final)

* React app consumes Drafts API end-to-end
* Server state handled via React Query with correct invalidation
* Forms implemented with client + backend validation error mapping
* Error UX is consistent and safe
* TypeScript contracts are used (no `any` in core paths)
* Routing is stable and ready for OAuth/HMRC pages
