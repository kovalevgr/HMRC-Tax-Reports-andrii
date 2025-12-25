# Module 2 – Interview Questions (Node.js Backend)

> Scope: **Middle → Middle+ (with Senior discussion depth)**
> Focus: Node.js runtime, backend architecture, HTTP layer, data access, and ecosystem decisions.

---

## Node.js Runtime & Core Concepts

### Event Loop, Single-Threaded Model, libuv

1. Why is Node.js considered single-threaded?
2. What actually runs on separate threads in Node.js?
3. What is libuv and what responsibilities does it have?
4. How does the event loop work in Node.js?
5. Explain the difference between browser and Node.js event loop.
6. What happens if you run CPU-intensive code in Node.js?
7. How would you handle CPU-bound tasks in a Node application?
8. What is a worker thread and when would you use it?

---

### Non-Blocking I/O vs Blocking Code

1. What does non-blocking I/O mean?
2. Give examples of blocking operations in Node.js.
3. Why is synchronous `fs` usage dangerous in production?
4. How can a single blocking call affect the whole system?
5. How do you detect blocking behavior in a Node app?
6. When is blocking code acceptable?

---

### CommonJS vs ES Modules in Node.js

1. What are the main differences between CommonJS and ES Modules?
2. How does module loading differ between them?
3. Why is ESM the preferred choice for modern Node.js?
4. What issues arise when mixing CJS and ESM?
5. How do `require` and `import` differ in behavior?
6. How does Node resolve modules in each system?

---

### Environment Variables & Configuration

1. Why should configuration not be hard-coded?
2. What problems do environment variables solve?
3. How does `dotenv` work?
4. What are common configuration anti-patterns?
5. How do you validate environment variables on startup?
6. What should never be stored in environment variables?
7. How do configuration strategies differ between dev, staging, and prod?

---

## Package & Dependency Management

### package.json, lockfiles, node_modules

1. What is the role of `package.json`?
2. What information belongs in `dependencies` vs `devDependencies`?
3. Why is a lockfile important?
4. What problems occur without a lockfile?
5. How does Node resolve dependencies in `node_modules`?
6. Why can `node_modules` become very large?

---

### Dev Dependencies vs Prod Dependencies

1. What happens if dev dependencies are installed in production?
2. How do bundlers/build tools affect dependency classification?
3. Can a dependency be both dev and prod?
4. How do dependency choices affect security and performance?

---

## HTTP Servers & Web Frameworks

### Native `http` Module

1. What does Node’s native `http` module provide?
2. What responsibilities must you handle manually when using `http`?
3. Why do most applications use frameworks instead of raw `http`?
4. When might using the native `http` module make sense?

---

### Express vs Fastify vs NestJS

1. What are the core differences between Express and Fastify?
2. Why is Fastify often considered faster than Express?
3. What problems does NestJS try to solve?
4. When is NestJS overkill?
5. How do these frameworks differ in terms of architecture?
6. How do you choose a framework for a new project?

---

### Routing, Middleware, Error Handling

1. What is middleware?
2. How does middleware order affect behavior?
3. What is the responsibility of error-handling middleware?
4. Why should error handling be centralized?
5. How do you prevent leaking sensitive error information?
6. How do request lifecycle and middleware relate?

---

### Request Validation

1. Why is request validation critical in backend systems?
2. Where should validation happen — controller, middleware, service?
3. What is schema-based validation?
4. How do TypeScript types differ from runtime validation?
5. How do you return user-friendly validation errors?

---

## Data Access Layer

### Relational Databases (PostgreSQL / MySQL)

1. How do you connect Node.js to a relational database?
2. What is connection pooling and why is it important?
3. What problems arise from opening a new connection per request?
4. When would you choose PostgreSQL over MySQL (or vice versa)?
5. How do transactions work?
6. What can go wrong if transactions are not used correctly?

---

### NoSQL Databases (MongoDB, Redis)

1. What is the difference between SQL and NoSQL databases?
2. When is MongoDB a good fit?
3. What use cases is Redis best suited for?
4. Why is Redis often used alongside a relational DB?
5. What consistency trade-offs exist in NoSQL systems?

---

### ORM / ODM Overview

1. What problems do ORMs solve?
2. What are the downsides of using an ORM?
3. Prisma vs TypeORM vs Sequelize — key differences.
4. Mongoose vs relational ORMs — conceptual differences.
5. When would you avoid an ORM entirely?

---

### Repository Pattern & Transactions

1. What is the repository pattern?
2. Why is it useful in backend architecture?
3. How does the repository pattern improve testability?
4. How do transactions interact with repositories?
5. What problems arise if business logic leaks into repositories?

---

## Senior-Level Discussion Questions

1. What was the most serious Node.js production issue you encountered?
2. How do you design a backend to remain stable under load?
3. How do you decide between simplicity and architectural rigor?
4. When does adding a framework slow a team down?

---

> ✅ This file can be used as:
>
> * Node.js backend interview checklist
> * mentoring discussion guide
> * readiness assessment for moving to NestJS
