# Module 1 – Interview Questions (JavaScript & TypeScript)

> Scope: **Middle → Middle+ / Senior** JavaScript & TypeScript
> Focus: language fundamentals, runtime model, async behavior, patterns, and practical TS usage.

---

## Language Fundamentals

### Execution Context, Call Stack, Scope, Hoisting

1. What is an execution context in JavaScript? What types exist?
2. How is the call stack related to execution contexts?
3. Explain lexical scope vs dynamic scope. Why does JS use lexical scope?
4. What is hoisting? Which declarations are hoisted and how?
5. Why do `let` and `const` behave differently from `var` during hoisting?
6. What happens when a stack overflow occurs?
7. How do closures relate to execution context and scope?
8. Can you explain a real bug caused by misunderstanding scope or hoisting?

---

### `this`, `call`, `apply`, `bind`

1. How is `this` determined in JavaScript?
2. What is the value of `this` in:

    * a regular function
    * an arrow function
    * a method call
    * a detached method reference
3. How do `call`, `apply`, and `bind` differ?
4. When would you use `bind` instead of `call`?
5. Why does `this` often break in callbacks?
6. How does `this` behave in strict mode?
7. How does `this` work inside classes vs functions?

---

### Primitives vs Reference Types, Immutability

1. Which types are primitives in JavaScript?
2. How are objects and arrays passed to functions?
3. What is the difference between value equality and reference equality?
4. Explain a bug caused by unintended mutation.
5. What does immutability mean in practice?
6. How do spread operators help with immutability?
7. When is mutation acceptable?

---

### ES Modules vs CommonJS

1. What are the main differences between ES Modules and CommonJS?
2. How does static vs dynamic import affect bundling and tree‑shaking?
3. Why are ES Modules preferred in modern Node.js?
4. What problems occur when mixing ESM and CJS?
5. How does module resolution work in Node.js?

---

## Asynchronous JavaScript

### Event Loop, Microtasks vs Macrotasks

1. What is the JavaScript event loop?
2. Explain the difference between microtasks and macrotasks.
3. Where do Promises and `async/await` callbacks run?
4. In what order will logs execute in mixed Promise / setTimeout code?
5. Why can long synchronous code block async execution?
6. How does the browser event loop differ from Node.js?

---

### Callbacks, Promises, async/await

1. What problem do Promises solve compared to callbacks?
2. What is callback hell?
3. How does `async/await` work under the hood?
4. Can `async` functions return non‑Promise values?
5. What happens if you forget to `await` a Promise?
6. How do you run async operations in parallel vs sequentially?

---

### Error Handling in Async Code

1. Why doesn’t `try/catch` catch all async errors?
2. How do you handle errors with Promises?
3. What happens with unhandled Promise rejections?
4. How should errors propagate in async pipelines?
5. How do you design safe async APIs?

---

## Modern JavaScript (ES6+)

### Syntax & Language Features

1. Explain destructuring and give a real use case.
2. What are rest and spread operators and how do they differ?
3. Why are template literals preferred over string concatenation?
4. What are default parameters useful for?
5. Differences between `var`, `let`, and `const`.

---

### Iterators & Generators (Advanced)

1. What is an iterator in JavaScript?
2. What problem do generators solve?
3. Have you ever used generators in real projects? Why or why not?

---

### Map, Set, WeakMap, WeakSet

1. Differences between `Map` and plain objects.
2. When should you use `Set`?
3. What makes `WeakMap` and `WeakSet` special?
4. Why can’t WeakMaps be iterated?
5. Memory‑related use cases for WeakMap.

---

## Functional & Object‑Oriented Patterns

### Functional Programming

1. What is a pure function?
2. What are side effects? Why are they dangerous?
3. What is referential transparency?
4. Explain `map`, `filter`, `reduce`, `flatMap` with examples.
5. Why is function composition useful?
6. How does immutability simplify reasoning about code?

---

### Object‑Oriented Patterns in JS

1. Composition vs inheritance — which do you prefer and why?
2. What is a factory function?
3. What are mixins and when are they useful?
4. Why deep inheritance hierarchies are problematic in JS?
5. When do classes make sense in JavaScript?

---

## Error Handling

### try / catch / finally

1. How does `try/catch` work?
2. What does `finally` guarantee?
3. Should you catch errors at low levels or propagate them?

---

### Custom Error Types

1. Why create custom error classes?
2. What information should an error object contain?
3. How do error codes differ from messages?
4. How do you design user‑safe vs internal errors?

---

## Tooling & Ecosystem

### Package Managers & Bundlers

1. Differences between npm, yarn, and pnpm.
2. What problem does pnpm solve?
3. What is a lockfile and why is it important?
4. Vite vs Webpack — when would you choose each?
5. What is tree‑shaking?

---

## TypeScript

### Basics

1. Difference between `interface` and `type`.
2. When should you use `type` aliases?
3. What are union and intersection types?

---

### Generics & Utility Types

1. Why are generics useful?
2. Explain `Partial`, `Pick`, `Omit`, `Record`.
3. How do generics improve API safety?

---

### Narrowing & Discriminated Unions

1. What is type narrowing?
2. How do discriminated unions work?
3. Why are discriminated unions powerful for state machines?

---

### TypeScript in Node.js & React

1. What does `strict` mode enable?
2. Why is `any` dangerous?
3. How do path aliases work?
4. Differences in TS usage between backend and frontend.
5. Where does TypeScript stop and runtime validation begin?

---

## Senior‑Level Meta Questions

1. What JavaScript concept caused you the biggest production issue?
2. How do you decide between FP and OO in JS?
3. What JS feature do you consider most misunderstood?
4. How do you keep JS/TS codebases maintainable long‑term?

---

> ✅ This file can be used as:
>
> * interview question bank
> * mentoring discussion guide
> * self‑assessment checklist
