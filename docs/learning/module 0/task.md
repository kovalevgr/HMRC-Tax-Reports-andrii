# Module 0 – Tasks Breakdown

## Goal

Bootstrap the repo and local dev environment (no CI). Outcome: **one-command local run**, backend `/health`, frontend calls it, quality gates enforced locally.

---

## Task 0.1 – Initialize repository & workspace

**Description**

* Create monorepo folder structure (`apps/*`, `packages/*`, `docs/*`, `infra/*`).
* Pick workspace tool (pnpm or npm workspaces) and lock it.

**Deliverables**

* Repo initialized
* Workspace config present

**Acceptance criteria**

* Root install works
* Dependencies are hoisted/managed predictably

**Questions to discuss**

* Why monorepo here?
* Where does shared code live and why?

---

## Task 0.2 – Define scripts (DX contract)

**Description**
Add predictable scripts at root:

* `dev` (starts api + web)
* `lint` (checks formatting + lint rules)
* `format` (optional)
* `test` (runs unit tests)

**Deliverables**

* Root `package.json` scripts

**Acceptance criteria**

* `dev` works on a clean clone
* Script names are consistent across packages

**Questions to discuss**

* What must be one command vs per-app?
* What belongs in root vs app scripts?

---

## Task 0.3 – Tooling: ESLint + Prettier + EditorConfig

**Description**

* Add ESLint config (root + per-package overrides as needed).
* Add Prettier config.
* Resolve ESLint↔Prettier conflicts.
* Add `.editorconfig`.

**Deliverables**

* `.eslintrc*`, `.prettierrc*`, `.editorconfig`

**Acceptance criteria**

* `lint` fails on broken rules
* Auto-formatting is deterministic

**Questions to discuss**

* Lint vs format: what’s the boundary?
* Which rules are team-style vs correctness?

---

## Task 0.4 – Git hygiene & repo safety

**Description**

* Add `.gitignore` and ignore local artifacts.
* Add `.env.example` files and ensure `.env` is ignored.

**Deliverables**

* `.gitignore`
* `.env.example` placeholders

**Acceptance criteria**

* No secrets can be committed accidentally (basic hygiene)
* New dev can copy `.env.example` → `.env` and run

**Questions to discuss**

* What is safe to store in `.env` locally?
* What should never appear in logs/commits?

---

## Task 0.5 – Backend skeleton (API)

**Description**

* Create `apps/api`.
* Implement minimal HTTP server.
* Add `/health` endpoint returning `{ status: "ok" }`.
* Add basic startup logging (no sensitive info).

**Deliverables**

* Running backend

**Acceptance criteria**

* `GET /health` returns 200
* Server port configurable via env

**Questions to discuss**

* Where should bootstrap/startup logic live?
* How do we prepare for middleware/logging later?

---

## Task 0.6 – Frontend skeleton (Web)

**Description**

* Create `apps/web` (React).
* Add a simple page that calls backend `/health` and renders status.
* Add API base URL configuration via env.

**Deliverables**

* Running frontend

**Acceptance criteria**

* UI shows "API: ok" when backend is running
* No hard-coded backend URL in code

**Questions to discuss**

* Build-time vs runtime config in frontend?
* What error/empty states should exist even now?

---

## Task 0.7 – Local tests (minimal)

**Description**

* Add at least 1 minimal test (example: shared util or simple health-response contract).

**Deliverables**

* `test` script passes

**Acceptance criteria**

* Tests run locally in <10s (target)

**Questions to discuss**

* What’s worth testing at Module 0?
* How do we keep tests fast from day 1?

---

## Task 0.8 – Documentation

**Description**
Create minimal docs:

* `README.md` with setup + run commands
* `docs/structure.md` explaining folders & boundaries

**Deliverables**

* README + docs

**Acceptance criteria**

* A new dev can run project in 5–10 minutes from README

**Questions to discuss**

* What is "production-like" for a POC?
* Which shortcuts are acceptable now vs later?

---

## Module 0 Definition of Done (final)

* One-command local start (`dev`)
* Backend `/health` works
* Frontend calls backend and renders status
* ESLint/Prettier enforced locally
* Minimal tests runnable locally
* No secrets committed
* README/docs exist
