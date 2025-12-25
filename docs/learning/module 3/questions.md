# Module 3 – Interview Questions (React Frontend)

> Scope: **Middle → Middle+ (with Senior discussion depth)**
> Focus: React fundamentals, state management, server state, forms, patterns, performance, and testing.

---

## Fundamentals

### Function Components, JSX, Composition

1. Why are function components the standard in modern React?
2. What is JSX and how does it work under the hood?
3. How do props work and how are they passed?
4. Composition vs inheritance in React — why is composition preferred?
5. What are children props and when are they useful?
6. What is conditional rendering and how do you implement it cleanly?

---

### Hooks Basics: useState, useEffect, useRef

1. What problem do hooks solve compared to class components?
2. How does `useState` work internally?
3. When does a component re-render?
4. What is `useEffect` used for?
5. Explain the dependency array in `useEffect`.
6. Common mistakes with `useEffect`.
7. What is `useRef` used for?
8. Difference between `useRef` and `useState`.

---

## State Management

### Local State

1. When should you use `useState` vs `useReducer`?
2. What is reducer pattern and why is it useful?
3. What is derived state?
4. Why is duplicating derived state an anti-pattern?

---

### Context API

1. What problem does Context API solve?
2. When should you NOT use Context?
3. How does Context affect re-renders?
4. How do you optimize Context usage?
5. Why is Context not a replacement for state management libraries?

---

### Global State (Redux Toolkit / Zustand / Jotai)

1. What problems does global state solve?
2. What are common mistakes when introducing global state?
3. Redux Toolkit vs Zustand vs Jotai — key differences.
4. When is Redux overkill?
5. How do you decide what belongs in global state?

---

## Data Fetching & Server State

### Fetching Basics

1. How do you fetch data in React?
2. Differences between Fetch API and Axios.
3. How do you handle loading and error states?
4. Why is data fetching considered side effect?

---

### React Query / TanStack Query

1. What problem does React Query solve?
2. Difference between server state and client state.
3. What is caching and why is it important?
4. How does invalidation work?
5. When does React Query refetch data?
6. How do mutations differ from queries?
7. What are common mistakes when using React Query?

---

## Forms & Validation

### Controlled vs Uncontrolled Components

1. What is a controlled component?
2. What is an uncontrolled component?
3. Trade-offs between controlled and uncontrolled inputs.
4. When are uncontrolled components preferable?

---

### Form Libraries

1. Why use a form library instead of manual state handling?
2. React Hook Form vs Formik — differences.
3. How does React Hook Form achieve better performance?
4. How do you integrate schema validation with forms?

---

### Schema Validation & UX

1. Zod vs Yup — differences.
2. Where should validation logic live?
3. How do you map backend validation errors to form fields?
4. How do you design good error messages?

---

## Advanced Hooks & Patterns

### Custom Hooks

1. What is a custom hook?
2. When should you extract logic into a custom hook?
3. Rules of hooks — what happens if you break them?
4. How do custom hooks improve reusability and testability?

---

### Memoization & Rendering Control

1. What does `useMemo` do?
2. What does `useCallback` do?
3. When is `React.memo` useful?
4. Why is overusing memoization harmful?

---

### Advanced Patterns

1. What is render props pattern?
2. What are compound components?
3. When are these patterns useful?
4. What problem do portals solve?
5. Examples of portals usage in real applications.

---

## Performance Optimization

### Rendering & Reconciliation

1. What is reconciliation in React?
2. Why are `key` props important?
3. What problems arise from incorrect keys?

---

### Avoiding Unnecessary Re-renders

1. What causes unnecessary re-renders?
2. How do you detect them?
3. How do you prevent them?

---

### Code Splitting & Lazy Loading

1. What is code splitting?
2. How does `React.lazy` work?
3. What is `Suspense` used for?
4. Trade-offs of lazy loading.

---

### Performance Profiling

1. How do you profile a React app?
2. What does React DevTools Profiler show?
3. What performance metrics actually matter?

---

## Frontend Testing

### Unit & Component Testing

1. Difference between unit tests and component tests.
2. Why is React Testing Library preferred over Enzyme?
3. What should you avoid testing in components?
4. How do you test async UI behavior?

---

### Hooks & E2E Testing

1. How do you test custom hooks?
2. When are E2E tests necessary?
3. Playwright vs Cypress — differences.
4. Common causes of flaky frontend tests.

---

## Senior-Level Discussion Questions

1. What was the most difficult React performance issue you solved?
2. How do you decide between local, context, and global state?
3. How do you keep large React codebases maintainable?
4. What React pattern do you consider most overused?

---

> ✅ This file can be used as:
>
> * React interview question bank
> * mentoring discussion guide
> * readiness assessment for advanced frontend work
