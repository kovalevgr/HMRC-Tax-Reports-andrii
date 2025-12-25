# Module 11 – Interview Questions (Software Architecture)

> Scope: **Middle+ → Senior / Lead**
> Focus: architectural thinking, trade-offs, system design, and evolution of backend systems.

> Assumption: candidate has solid backend experience (Node/Nest/DBs).

---

## Software Architecture – Fundamentals

1. What is software architecture?
2. How does architecture differ from design?
3. What problems does architecture try to solve?
4. What makes an architecture “good” or “bad”?
5. How do non-functional requirements influence architecture?
6. Can architecture be changed later? At what cost?

---

## Layered Architecture

1. What is layered architecture?
2. Typical layers in a backend system.
3. What dependencies are allowed between layers?
4. Why should dependencies point inward?
5. What problems arise when layers are bypassed?
6. Can layered architecture become rigid?
7. How does layered architecture scale with team size?

---

## Clean Architecture

1. What is Clean Architecture?
2. How does it differ from classic layered architecture?
3. What is the Dependency Rule?
4. What belongs to the domain layer?
5. What should never depend on frameworks?
6. How do controllers fit into Clean Architecture?
7. Pros and cons of Clean Architecture.

---

## Domain-Driven Design (DDD)

### Core Concepts

1. What is Domain-Driven Design?
2. What problem does DDD try to solve?
3. What is a domain?
4. Difference between domain and application logic.

---

### Tactical DDD

1. What is an Entity?
2. What is a Value Object?
3. What is an Aggregate?
4. What is an Aggregate Root?
5. Why are invariants important?
6. What is a Repository in DDD?
7. How does DDD repository differ from ORM repositories?

---

### Strategic DDD

1. What is a Bounded Context?
2. Why are bounded contexts critical in large systems?
3. What is a Context Map?
4. How do teams communicate across bounded contexts?
5. What problems arise when bounded contexts are ignored?

---

## Monolith Architecture

1. What is a monolith?
2. What are the advantages of a monolith?
3. Common myths about monoliths.
4. When is a monolith the best choice?
5. What is a modular monolith?
6. What problems appear as monoliths grow?
7. How do you prevent monoliths from becoming “big balls of mud”?

---

## Microservices Architecture

1. What is a microservice?
2. What problems do microservices solve?
3. What new problems do microservices introduce?
4. How do microservices communicate?
5. What is service discovery?
6. How do you handle data consistency across services?
7. When should you *not* use microservices?

---

## Monolith vs Microservices

1. Compare monolith vs microservices.
2. How do team size and organization affect this choice?
3. How does deployment differ?
4. How does observability differ?
5. How do you migrate from monolith to microservices safely?

---

## Event-Driven Architecture

1. What is event-driven architecture?
2. Commands vs events — what’s the difference?
3. What problems does event-driven architecture solve?
4. What is eventual consistency?
5. How do you handle failures in event-driven systems?
6. What is idempotency and why is it critical?
7. How do you version events?

---

## Architecture Decision Making

1. How do you evaluate architectural trade-offs?
2. What is YAGNI and how does it apply to architecture?
3. How do you document architectural decisions?
4. What is an ADR?
5. How do you know when architecture needs to evolve?

---

## Senior / Lead Level Discussion

1. What was the biggest architectural mistake you’ve seen?
2. How do you balance long-term architecture with short-term delivery?
3. How do you introduce architecture changes to an existing system?
4. How do you ensure architecture is understood by the team?
5. How do you prevent over-engineering?

---

> ✅ This file can be used as:
>
> * Architecture interview question bank
> * Senior / Lead readiness assessment
> * Architecture mentoring discussion guide
