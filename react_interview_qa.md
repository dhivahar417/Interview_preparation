## **Intermediate React Questions — Answers**

### **Core React Concepts**

**1. Explain the Virtual DOM and how React’s reconciliation algorithm works.**

- **Virtual DOM (VDOM)**: A lightweight in-memory representation of the actual DOM.
- **Workflow**:

  1. On state/prop change, React creates a new VDOM tree.
  2. React **diffs** the new VDOM with the previous one (using the **Reconciliation** algorithm).
  3. Only the changed nodes are updated in the real DOM (**minimal re-rendering**).

- **Reconciliation**: Uses heuristics (like `keys`) to efficiently decide what changes to apply.

---

**2. Differences between controlled and uncontrolled components?**

| Feature     | Controlled Component                              | Uncontrolled Component           |
| ----------- | ------------------------------------------------- | -------------------------------- |
| Data Source | React state                                       | DOM itself                       |
| Updates     | Via `onChange` handler updating state             | DOM changes internally           |
| Example     | `<input value={state} onChange={...} />`          | `<input defaultValue="Hi" />`    |
| When to use | When React needs full control (forms, validation) | Quick/simple forms, minimal code |

---

**3. How does React handle events compared to vanilla JavaScript?**

- Uses **SyntheticEvent**, a wrapper for browser events to ensure **cross-browser compatibility**.
- Event delegation is handled at the root (`document`) for better performance.
- Syntax is camelCase (`onClick` instead of `onclick`) and functions are passed instead of strings.

---

**4. What are keys in React, and why are they important?**

- **Keys** uniquely identify list items for React’s diffing algorithm.
- Helps React determine **which items changed/added/removed** without re-rendering the whole list.
- Bad key choice (like `index`) can cause unnecessary re-renders or bugs.

---

**5. Explain the component lifecycle in class components (and hooks equivalents).**
**Class Lifecycle:**

- **Mounting**: `constructor` → `render` → `componentDidMount`
- **Updating**: `shouldComponentUpdate` → `render` → `componentDidUpdate`
- **Unmounting**: `componentWillUnmount`

**Hooks Equivalents:**

- `useEffect(..., [])` → `componentDidMount`
- `useEffect(..., [deps])` → `componentDidUpdate`
- Cleanup inside `useEffect` → `componentWillUnmount`

---

**6. What are Higher-Order Components (HOCs)? Provide an example.**

- Function that **takes a component and returns a new component** with added props/logic.
- Example:

```jsx
function withAuth(WrappedComponent) {
  return function (props) {
    const isLoggedIn = Boolean(localStorage.getItem("token"));
    return isLoggedIn ? (
      <WrappedComponent {...props} />
    ) : (
      <div>Login Required</div>
    );
  };
}
```

---

**7. How do you optimize React component rendering?**

- `React.memo` → Memoizes functional components.
- `useMemo` → Memoizes computed values.
- `useCallback` → Memoizes function references.
- Avoid anonymous functions inline.
- Use proper `key`s in lists.
- Lazy load components with `React.lazy`.

---

### **State Management**

**8. When to use `useState` vs `useReducer`?**

- `useState`: Simple local state, small updates.
- `useReducer`: Complex state logic, multiple sub-values, predictable updates, or when next state depends on the previous state.

---

**9. How does React Context work, and when should you avoid it?**

- Context provides a way to share data globally without prop drilling.
- **Avoid** when state changes very frequently (can cause unnecessary renders) — use libraries like Redux/Zustand for large-scale state.

---

**10. Implement a custom hook for fetching data (`useFetch`).**

```jsx
import { useState, useEffect } from "react";

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    let ignore = false;
    setLoading(true);
    fetch(url)
      .then((res) => res.json())
      .then((json) => !ignore && setData(json))
      .finally(() => !ignore && setLoading(false));
    return () => {
      ignore = true;
    };
  }, [url]);

  return { data, loading };
}
```

---

**11. Compare Redux, Zustand, and React Context.**

| Feature     | Redux                 | Zustand           | Context             |
| ----------- | --------------------- | ----------------- | ------------------- |
| Boilerplate | High                  | Low               | Low                 |
| DevTools    | Yes                   | Yes               | No (native)         |
| Performance | Good with memoization | Excellent         | Can re-render a lot |
| Use case    | Large apps            | Small/medium apps | Small global state  |

---

**12. How to handle global state without Redux?**

- Use **React Context + useReducer** for predictable state updates.
- Example: Global Auth store via context.
- Or use lightweight state libs like **Zustand** or **Jotai**.

---

### **Hooks**

**13. Explain the rules of hooks and why they exist.**

- Call hooks **only** at the top level of a component.
- Call hooks **only** from React functions (components or custom hooks).
- Ensures consistent hook call order for React’s internal state tracking.

---

**14. How does `useEffect` dependency array work?**

- `[]` → Runs once on mount.
- `[var1, var2]` → Runs when any listed dependency changes.
- No array → Runs after every render.
- React compares dependencies using **Object.is**.

---

**15. Custom `usePrevious` hook.**

```jsx
function usePrevious(value) {
  const ref = React.useRef();
  React.useEffect(() => {
    ref.current = value;
  }, [value]);
  return ref.current;
}
```

---

**16. Implement `useDebounce`.**

```jsx
function useDebounce(value, delay) {
  const [debounced, setDebounced] = React.useState(value);
  React.useEffect(() => {
    const handler = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(handler);
  }, [value, delay]);
  return debounced;
}
```

---

**17. Difference between `useMemo` and `useCallback`?**

- `useMemo(fn, deps)` → Returns **memoized result** of a computation.
- `useCallback(fn, deps)` → Returns **memoized function reference**.

---

### **Performance Optimization**

**18. How does code splitting work in React?**

- Using `React.lazy(() => import('./MyComponent'))` and `<Suspense fallback={<Loader />}>`.
- Loads only when the component is needed (**reduces bundle size**).

---

**19. Purpose of `React.Fragment`?**

- Wraps multiple elements **without adding extra DOM nodes**.
- Syntax: `<React.Fragment>` or shorthand `<>`.

---

**20. How to debug performance issues in React?**

- Use **React DevTools Profiler**.
- Check re-render counts with `why-did-you-render`.
- Use memoization to prevent unnecessary renders.

---

**21. How does `React.memo` work and when to use it?**

- **`React.memo`**: Higher-order component that **skips re-render** if props haven’t changed.
- Use when:

  - Pure functional components
  - Expensive renders
  - Props change infrequently

---

## **Advanced React Questions — Answers**

### **Deep Dive into React**

**22. How React Fiber improves rendering performance**

- **Fiber** is a reimplementation of React’s reconciliation algorithm.
- Enables **incremental rendering**: work can be paused, resumed, or aborted.
- Allows **priority-based updates** (urgent UI vs. background tasks).
- Powers **concurrent features** like `useTransition`.

---

**23. Render Prop pattern vs Hooks**

- **Render Prop**: A component that takes a function as a child.

```jsx
<DataProvider render={(data) => <List data={data} />} />
```

- Hooks achieve similar logic reuse **without nesting** and with better readability.
- Render props can cause **wrapper hell**, hooks avoid that.

---

**24. SSR and Hydration in React**

- **SSR**: Render components to HTML on the server using `renderToString`/`renderToPipeableStream`.
- **Hydration**: React attaches event listeners and makes the server-rendered HTML interactive in the browser.
- Used by frameworks like **Next.js**.

---

**25. Error Boundaries**

- Catch errors in render/ lifecycle methods.
- Implement by extending `React.Component` with `componentDidCatch` + `getDerivedStateFromError`.

```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };
  static getDerivedStateFromError() {
    return { hasError: true };
  }
  componentDidCatch(error, info) {
    console.error(error, info);
  }
  render() {
    return this.state.hasError ? <Fallback /> : this.props.children;
  }
}
```

---

**26. Concurrent Features (`useTransition`, `useDeferredValue`)**

- `useTransition`: Mark updates as non-urgent to avoid blocking UI.
- `useDeferredValue`: Delay updating a value until rendering is less busy.
- Improves perceived performance in slow renders.

---

### **State Management & Advanced Patterns**

**27. Redux-like store with `useReducer` + `useContext`**

```jsx
const StoreContext = React.createContext();
function StoreProvider({ children }) {
  const [state, dispatch] = React.useReducer(reducer, initialState);
  return (
    <StoreContext.Provider value={{ state, dispatch }}>
      {children}
    </StoreContext.Provider>
  );
}
function useStore() {
  return React.useContext(StoreContext);
}
```

---

**28. Handling authentication state in large apps**

- Centralized store (Redux, Zustand) or AuthContext.
- Store JWT/refresh tokens securely (HTTP-only cookies).
- Protect routes via higher-order components or route guards.

---

**29. Compound Components Pattern**

- Allows components to work together without prop drilling.

```jsx
<Tabs>
  <Tabs.List>
    <Tabs.Tab>One</Tabs.Tab>
  </Tabs.List>
  <Tabs.Panel>Content</Tabs.Panel>
</Tabs>
```

- State is shared internally via context.

---

**30. React Query vs Redux for data fetching**

- React Query: **Server state** management (caching, refetching, syncing).
- Redux: General state management, needs manual async logic.
- React Query is **zero-config for fetching** and **auto cache invalidation**.

---

### **Hooks Deep Dive**

**31. `useInterval` hook**

```jsx
function useInterval(callback, delay) {
  const savedCallback = React.useRef();
  React.useEffect(() => {
    savedCallback.current = callback;
  });
  React.useEffect(() => {
    const id = setInterval(() => savedCallback.current(), delay);
    return () => clearInterval(id);
  }, [delay]);
}
```

---

**32. `useLocalStorage` hook**

```jsx
function useLocalStorage(key, initialValue) {
  const [value, setValue] = React.useState(
    () => JSON.parse(localStorage.getItem(key)) || initialValue
  );
  React.useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);
  return [value, setValue];
}
```

---

**33. `useLayoutEffect` vs `useEffect`**

- `useEffect`: Runs **after** paint, non-blocking.
- `useLayoutEffect`: Runs **before** paint, blocking — use for DOM measurements.

---

**34. `useClickOutside` hook**

```jsx
function useClickOutside(ref, handler) {
  React.useEffect(() => {
    const listener = (e) => {
      if (!ref.current.contains(e.target)) handler(e);
    };
    document.addEventListener("mousedown", listener);
    return () => document.removeEventListener("mousedown", listener);
  }, [ref, handler]);
}
```

---

### **Performance & Optimization**

**35. Reconciliation algorithm minimizes re-renders**

- Compares **VDOM trees** using diffing.
- Updates only changed elements.
- Uses keys to avoid re-rendering unchanged list items.

---

**36. Windowing / Virtualization**

- Render **only visible list items** (react-window, react-virtualized).
- Improves performance for huge datasets.

---

**37. Optimizing large list rendering**

- Use virtualization, pagination, `React.memo`, key optimization.
- Avoid inline functions and styles in list items.

---

**38. How React.memo works under the hood**

- Performs **shallow prop comparison**.
- If props are the same, skips rendering and reuses last output.

---

### **Testing & Debugging**

**39. Testing with Jest + React Testing Library**

```jsx
test("renders text", () => {
  render(<MyComponent />);
  expect(screen.getByText(/hello/i)).toBeInTheDocument();
});
```

- Focus on **behavior**, not implementation details.

---

**40. Common pitfalls testing hooks**

- Forgetting to wrap in `act()` for state updates.
- Not cleaning up timers/subscriptions.

---

**41. Debugging memory leaks**

- Use Chrome DevTools Performance tab.
- Check unmounted components still in memory.
- Ensure cleanup in `useEffect` return function.

---

### **React + TypeScript**

**42. Typing props, hooks, events**

```ts
type Props = {
  name: string;
  onClick: (e: React.MouseEvent<HTMLButtonElement>) => void;
};
```

- Hooks: `function useCustomHook<T>(initial: T): T {}`

---

**43. Discriminated Unions**

```ts
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; size: number };
```

- Narrowing via `switch (shape.kind)`.

---

**44. Typing a generic component**

```ts
function List<T>({ items }: { items: T[] }) { return <>{items.map(...)} </>; }
```

---

### **Architecture & Best Practices**

**45. Large-scale React app structure**

```
src/
  components/
  features/
  hooks/
  store/
  pages/
  utils/
```

- Use feature-based folders and clear separation.

---

**46. Common anti-patterns**

- Overusing context for high-frequency updates.
- Inline anonymous functions in render.
- Mutating state directly.

---

**47. Feature flags in React**

- Store flags in context or config.
- Toggle UI/logic based on flags.
- Can integrate with services like **LaunchDarkly**.

---

**48. Micro-frontends with React**

- Multiple independent React apps combined via Module Federation, iframe, or web components.
- Useful for large teams with separate deployments.

---

### **Algorithmic & Problem-Solving**

**49. Drag-and-drop with React DnD** — Use `useDrag` + `useDrop` from react-dnd to reorder list items.

**50. Infinite scroll component** — Listen for scroll position near bottom, trigger data fetch. Use Intersection Observer.

**51. Form validation hook** — Track values, errors, touched state; run validation rules on change/blur.

**52. Debounced search input with API calls** — Combine `useDebounce` hook with `fetch` and cancel previous requests.

---

### **Bonus: System Design**

**53. Real-time chat app**

- WebSocket connection, state store, message queue for ordering, optimistic UI updates.

**54. Offline-first React apps**

- Cache data with IndexedDB or localStorage.
- Service workers for caching assets and API calls.

**55. API rate limiting handling**

- Queue requests, use exponential backoff.
- Respect `Retry-After` headers from the server.

---
