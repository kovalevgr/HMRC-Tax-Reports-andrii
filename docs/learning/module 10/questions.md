# Module 10 – Interview Questions (NestJS Backend)

> Scope: **Middle+ → Senior**
> Focus: NestJS architecture, dependency injection, module design, migration from plain Node.js, and real-world trade-offs.

> Assumption: candidate already understands Node.js fundamentals (Module 2).

---

## NestJS Fundamentals

### What NestJS Is (and Is Not)

1. What problems does NestJS solve compared to Express/Fastify?
2. Why is NestJS often compared to Angular?
3. When does NestJS add real value?
4. When is NestJS overkill?
5. Can NestJS be used without HTTP (e.g. CLI, workers, microservices)?

---

## Architecture & Modules

### Modules

1. What is a NestJS module?
2. Why are modules important for scalability?
3. What should and should not be inside a module?
4. Difference between `imports`, `providers`, `exports`, `controllers`.
5. What happens if a provider is not exported?
6. How do circular dependencies arise between modules?
7. How do you resolve circular dependencies in NestJS?

---

## Dependency Injection (DI)

### Providers & Injection

1. What is dependency injection and why is it useful?
2. How does NestJS DI differ from manual DI in plain Node.js?
3. What is a provider?
4. How does NestJS resolve providers?
5. What is the default provider scope?
6. Difference between `singleton`, `request`, and `transient` scopes.
7. When would you use request-scoped providers?
8. What problems can request-scoped providers introduce?

---

## Controllers & Request Lifecycle

### Controllers

1. What is the responsibility of a controller in NestJS?
2. How should controllers differ from services?
3. Why should controllers be thin?
4. How does NestJS map routes to controllers?

---

### Pipes

1. What are pipes used for?
2. Difference between transformation and validation pipes.
3. How does `ValidationPipe` work internally?
4. Pipes vs middleware — when to use which?

---

### Filters (Error Handling)

1. What is an exception filter?
2. How does NestJS handle thrown exceptions?
3. How do global filters differ from local filters?
4. How do you map domain errors to HTTP responses?
5. How do you prevent leaking internal errors?

---

### Guards

1. What are guards used for?
2. How do guards differ from middleware?
3. Authentication vs authorization — where do guards fit?
4. How do guards integrate with decorators?

---

### Interceptors

1. What problems do interceptors solve?
2. Interceptors vs middleware — key differences.
3. Typical interceptor use cases (logging, timing, mapping responses).
4. How do interceptors affect request/response flow?

---

## Validation, Serialization & DTOs

1. What is a DTO in NestJS?
2. Why are DTOs important even when using TypeScript?
3. class-validator vs schema-based validation (Zod) — trade-offs.
4. How does `class-transformer` work?
5. How do you control what fields are returned to clients?

---

## Configuration & Environment Management

1. What does `@nestjs/config` provide?
2. How do you validate configuration on startup?
3. How do you handle secrets in NestJS?
4. How does configuration differ across environments?

---

## Testing in NestJS

### Unit & Integration Testing

1. How do you unit test a NestJS service?
2. What is `TestingModule`?
3. How do you mock providers?
4. How do you test controllers without starting HTTP server?
5. How do e2e tests work in NestJS?

---

## Performance & Production Concerns

1. What is the startup cost of NestJS?
2. How does DI affect performance?
3. How do you optimize a NestJS app under load?
4. How do you handle graceful shutdown in NestJS?

---

## Migration from Plain Node.js / Express

1. How would you migrate an existing Express app to NestJS?
2. What should be migrated first?
3. What logic should NOT be rewritten during migration?
4. How do you preserve API contracts during migration?
5. What role do tests play in migration?

---

## Common Pitfalls

1. Fat controllers — why are they bad?
2. Overusing request-scoped providers.
3. Leaking framework code into domain logic.
4. Treating NestJS as "magic" instead of explicit architecture.

---

## Senior-Level Discussion Questions

1. When would you explicitly *not* choose NestJS?
2. What NestJS feature do you consider most misunderstood?
3. How do you balance framework conventions with clean architecture?
4. What trade-offs did you encounter using NestJS in production?
5. How do you keep NestJS projects maintainable long-term?

---

> ✅ This file can be used as:
>
> * NestJS interview question bank
> * migration readiness assessment
> * Senior-level discussion guide
