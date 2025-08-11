
# React JS Interview Questions and Answers (3 to 6 Years Experience)

---

## 1. What are the key features of React?
- JSX – JavaScript XML for writing HTML in JS.
- Virtual DOM – Efficient diffing and reconciliation.
- Component-Based – Reusable, isolated pieces of UI.
- Unidirectional Data Flow – Predictable state and data handling.
- Declarative UI – Describe *what* UI should look like.
- Hooks – Functional components with local state and side effects.

---

## 2. Difference between functional and class components?

| Feature            | Class Component         | Functional Component         |
|--------------------|--------------------------|------------------------------|
| Syntax             | ES6 Class                | JS Function                  |
| State              | `this.state`             | `useState` hook             |
| Lifecycle Methods  | Yes (e.g. `componentDidMount`) | Yes (via `useEffect`) |
| `this` Binding     | Required                 | Not required                 |
| Performance        | Slightly heavier         | Lighter                      |

---

## 3. What is the Virtual DOM and how does React use it?
Virtual DOM is a lightweight JS object that is a copy of the real DOM. When state changes:
1. React creates a new Virtual DOM.
2. Compares it with the previous one (diffing).
3. Applies only the changed parts to the real DOM (reconciliation).

---

## 4. Explain the lifecycle of a React component.

**Class Component Lifecycle:**
- Mounting: `constructor`, `render`, `componentDidMount`
- Updating: `shouldComponentUpdate`, `componentDidUpdate`
- Unmounting: `componentWillUnmount`

**In Hooks (Functional):**
- Use `useEffect()` to mimic lifecycle:
  - ComponentDidMount → `useEffect(() => {}, [])`
  - ComponentDidUpdate → `useEffect(() => {})`
  - ComponentWillUnmount → `useEffect(() => return () => {})`

---

## 5. What are Hooks? Name some commonly used ones.
Hooks let you use state and lifecycle features in functional components.

**Common Hooks:**
- `useState`
- `useEffect`
- `useContext`
- `useMemo`
- `useCallback`
- `useRef`
- `useReducer`

---

## 6. Difference between useEffect and useLayoutEffect?

| Feature          | `useEffect`                    | `useLayoutEffect`                    |
|------------------|---------------------------------|--------------------------------------|
| Timing           | Runs after paint                | Runs before paint                    |
| Use Case         | API calls, subscriptions        | DOM measurements, synchronously updates |
| Blocking         | No                              | Yes – can block painting             |

---

## 7. How do you optimize performance in React apps?
- Memoization using `React.memo`, `useMemo`, `useCallback`
- Code splitting with React.lazy and Suspense
- Virtualization (e.g., react-window)
- Avoid unnecessary re-renders
- Proper key usage in lists
- Debounce/throttle user input
- Lazy load images/components

---

## 8. What is Redux and when should you use it?
Redux is a predictable state management library.
Use when:
- You have large app with shared state
- Many nested components depend on the same data
- You want centralized debugging/logging tools

**Core Concepts:**
- Store: Single source of truth
- Actions: Describe changes
- Reducers: Update state
- Dispatch: Sends action to reducer

---

## 9. Difference between Context API and Redux?

| Feature        | Context API                  | Redux                           |
|----------------|------------------------------|----------------------------------|
| Use Case       | Light global state           | Complex state & middleware       |
| Boilerplate    | Minimal                      | More setup (reducers/actions)   |
| Performance    | May re-render unnecessarily  | Optimized via selectors/middleware |
| Tooling        | Basic                        | DevTools, middleware, etc.       |

---

## 10. Explain controlled vs uncontrolled components.

**Controlled Component:**
```jsx
<input value={value} onChange={e => setValue(e.target.value)} />
```

**Uncontrolled Component:**
```jsx
<input ref={inputRef} />
```

---

## 11. What is React Suspense and lazy loading?
```jsx
const LazyComponent = React.lazy(() => import('./Component'));
<Suspense fallback={<div>Loading...</div>}>
  <LazyComponent />
</Suspense>
```

---

## 12. Explain useMemo and useCallback with examples.

- **useMemo**: Caches computed values
```js
const memoizedValue = useMemo(() => computeExpensive(a, b), [a, b]);
```

- **useCallback**: Caches functions
```js
const memoizedCallback = useCallback(() => doSomething(a, b), [a, b]);
```

---

## 13. How does reconciliation work in React?
React compares the previous virtual DOM with the new one and applies minimal DOM mutations.

---

## 14. What is the purpose of keys in lists?
Help React identify which items changed, added, or removed.

---

## 15. Explain Prop Drilling. How can it be avoided?
Prop Drilling = passing props through intermediate components.

**Avoid it by:**
- Using Context API
- Using Redux or Zustand or Recoil

---

## 16. What is server-side rendering (SSR) in React?
SSR renders React components on the server and sends HTML to the client.

Framework: **Next.js**

---

## 17. What are Higher Order Components (HOC)?

```js
function withLogger(WrappedComponent) {
  return function Enhanced(props) {
    console.log('Rendering...');
    return <WrappedComponent {...props} />;
  };
}
```

---

## 18. Difference between `useRef` and `createRef`?

| Hook           | `useRef` (Functional)    | `createRef` (Class-based)        |
|----------------|--------------------------|----------------------------------|
| Persistent     | Across re-renders        | Re-created on each render        |
| Usage          | Store DOM or mutable value | DOM access or refs in classes |

---

## 19. How do you handle form validation in React?
**Options:**
- Custom validation using state
- Libraries like:
  - **Formik**
  - **React Hook Form**
  - **Yup** (schema validation)

---

## 20. What are React Portals?
React Portals render children into a DOM node outside the parent’s DOM hierarchy.

```js
ReactDOM.createPortal(child, document.getElementById('modal-root'));
```

---

## 21. What are custom hooks and how do you create one?

**Answer:**
Custom hooks are JavaScript functions that start with `use` and allow you to reuse stateful logic between components.

**Example:**
```js
import { useState, useEffect } from 'react';

function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  return width;
}
```

---

## 22. Explain the concept of lifting state up in React.

**Answer:**
Lifting state up means moving shared state to the closest common ancestor of the components that use it. This allows components to communicate and share the same state via props.

---

## 23. How does React handle forms and what are best practices?

**Answer:**
- Use controlled components where form inputs are tied to React state.
- Use libraries like `Formik` or `React Hook Form` for large forms.
- Validation should be separated using libraries like `Yup`.
- Always provide `name`, `value`, and `onChange` for form fields.

---

## 24. What is reconciliation and how does the diffing algorithm work?

**Answer:**
React’s diffing algorithm compares two virtual DOM trees and tries to find the most efficient way to update the real DOM.

**Rules of optimization:**
- Elements of different types produce different trees.
- Keys help React identify items that changed.

---

## 25. How does `useReducer` work and when should you use it over `useState`?

**Answer:**
`useReducer` is used for complex state logic where state depends on previous state or multiple sub-values.

```js
const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment': return { count: state.count + 1 };
    case 'decrement': return { count: state.count - 1 };
    default: return state;
  }
}

const [state, dispatch] = useReducer(reducer, initialState);
```

Use `useReducer` when:
- You have complex state transitions
- You need to group state logic in one place

---

## 26. Explain React Fiber architecture.

**Answer:**
Fiber is the new reconciliation engine in React from v16 onwards. It enables features like time slicing, suspense, and interruption of rendering.

**Goals of Fiber:**
- Prioritize updates
- Pause work and come back later
- Reuse previously completed work
- Split rendering into chunks

---

## 27. What is Concurrent Mode in React?

**Answer:**
Concurrent Mode allows React to interrupt rendering and work on multiple tasks simultaneously, improving responsiveness.

Features enabled by Concurrent Mode:
- Time slicing
- Suspense for data fetching
- Transitions for smooth UI updates

Use with frameworks like **Next.js** or via `ReactDOM.createRoot`.

---

## 28. How do you handle side effects in React?

**Answer:**
Use `useEffect()` to handle side effects like:
- Data fetching
- Subscriptions
- DOM mutations

**Cleanup:**
Return a function inside `useEffect` for cleanup (e.g., unsubscribing).

---

## 29. How does `React.memo` work?

**Answer:**
`React.memo` is a HOC that memoizes functional components to prevent unnecessary re-renders.

```js
const MyComponent = React.memo(function MyComponent({ value }) {
  return <div>{value}</div>;
});
```

It does a shallow comparison of props.

---

## 30. Explain the role of keys in reconciliation and what happens if keys are not used correctly.

**Answer:**
Keys help React identify which items in a list have changed. Not using keys or using non-unique keys like indexes can cause unexpected behavior and inefficient DOM updates.

---

## 31. How to structure a large-scale React application?

**Answer:**
- Use feature-based folder structure (e.g., `features/`, `components/`, `hooks/`, `utils/`).
- Separate presentational and container components.
- Use state management (Context, Redux, Zustand) based on need.
- Add service layer for API integration.
- Use lazy loading and code splitting.

---

## 32. What are some alternatives to Redux and when should you consider them?

**Answer:**
Alternatives:
- **Context API** – For simple global state.
- **Zustand** – Lightweight and scalable.
- **Recoil** – Fine-grained state management.
- **Jotai** – Primitive and reactive approach.

Use alternatives when Redux introduces too much boilerplate or overengineering.

---

## 33. Explain error boundaries in React.

**Answer:**
Error boundaries catch JavaScript errors in their child component tree and render a fallback UI instead of crashing the app.

```js
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    logErrorToService(error, info);
  }

  render() {
    if (this.state.hasError) return <h1>Something went wrong.</h1>;
    return this.props.children;
  }
}
```

---

## 34. What is the difference between mounting and hydration in SSR?

**Answer:**
- **Mounting**: Initial render on the client (CSR).
- **Hydration**: React attaches event listeners to server-rendered HTML.

Hydration is used in SSR frameworks like **Next.js** to make static HTML interactive.

---

## 35. What is useTransition and when should you use it?

**Answer:**
`useTransition` lets you mark state updates as non-urgent so React can pause them and prioritize user interaction.

```js
const [isPending, startTransition] = useTransition();

startTransition(() => {
  setValue(input); // non-urgent update
});
```

Use it when you want to keep UI responsive during expensive re-renders.

---

---

## 36. How would you handle a slow-rendering component in a large dashboard app?

**Answer:**
- Use `React.memo` to memoize pure components.
- Use `useMemo` to avoid recalculating heavy computations.
- Use virtualization libraries (like `react-window` or `react-virtualized`) for large lists or tables.
- Break large components into smaller ones and lazy-load them.
- Profile using React DevTools to find bottlenecks.

---

## 37. A user types into a search box and you need to fetch suggestions from an API. How would you implement this?

**Answer:**
- Use `useEffect` with a dependency on the input value.
- Debounce the input using `lodash.debounce` or a custom solution.
- Cancel previous requests using `AbortController` or a cleanup function.

**Example:**
```js
useEffect(() => {
  const handler = setTimeout(() => {
    fetchSuggestions(query);
  }, 300);
  return () => clearTimeout(handler);
}, [query]);
```

---

## 38. Your app has a lot of nested prop drilling. How would you refactor it?

**Answer:**
- Use **React Context** to lift state up and share it across multiple components.
- Alternatively, introduce a state management solution like **Redux**, **Zustand**, or **Recoil**.

---

## 39. You are working on a multi-step form with validation and navigation. How would you design it?

**Answer:**
- Maintain a single form state (object) for all steps.
- Track current step index in state.
- Use conditional rendering to show steps.
- Add validation per step using **Yup** or custom logic.
- Disable "Next" until current step passes validation.
- Optionally use **Formik** or **React Hook Form** for advanced handling.

---

## 40. How would you implement a theme switcher (dark/light mode) in React?

**Answer:**
- Store theme in a Context and use a Provider.
- Save preference in `localStorage`.
- Apply a class to `<body>` or `<html>` and toggle styles using CSS variables or class-based themes.

```js
const [theme, setTheme] = useState(localStorage.getItem("theme") || "light");
useEffect(() => {
  document.body.className = theme;
  localStorage.setItem("theme", theme);
}, [theme]);
```

---

## 41. How do you prevent unnecessary re-renders in a component?

**Answer:**
- Use `React.memo()` for pure components.
- Use `useCallback()` for functions passed as props.
- Use `useMemo()` for expensive calculations.
- Use `shouldComponentUpdate()` in class components.
- Proper use of `key` props in lists.

---

## 42. How do you structure an application that uses both public and protected routes?

**Answer:**
- Use **React Router**.
- Create a `PrivateRoute` wrapper component that checks authentication before rendering.

```js
<Route path="/dashboard" element={<PrivateRoute><Dashboard /></PrivateRoute>} />
```

- Store auth token in context or Redux, and validate user in the wrapper.

---

## 43. How would you handle global loading or error state during API calls?

**Answer:**
- Use global state management (Redux or Context).
- Set loading/error flags in reducers or context.
- Show loading spinners or error messages conditionally.
- Optionally create a custom `useApi` hook to handle loading/error logic in one place.

---

## 44. You need to support offline mode and background sync. What tools would you use?

**Answer:**
- Use **Service Workers** with **Workbox**.
- Use `localStorage` or `IndexedDB` (via **idb** or **Dexie.js**) to store data offline.
- Sync in background using Background Sync API or by checking online status (`navigator.onLine`).

---

## 45. How do you handle component state reset when navigating away and coming back?

**Answer:**
- Reset state on component mount using `useEffect(() => { setState(initial) }, [])`.
- If using **React Router**, use route key or remount logic.
- For shared state, reset on route change or unmount.

---
