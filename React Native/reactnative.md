Perfect — here’s a **Senior React Native Technical Question Bank** tailored exactly to the JD you shared.
I’ve split it into **Core React Native**, **Advanced Ecosystem**, **Platform Integration**, **Performance/Debugging**, and **Architecture/Scenario** so you can practice systematically over the next 3 days.

---

## **1. Core React Native & React (Fundamentals)**

1. Explain the **React Native rendering process** — how does JS interact with native code?
2. Difference between **React Native old architecture** and **new architecture (Fabric/TurboModules)**.
3. How would you decide between **Zustand**, **Redux Toolkit**, and **Context API** for state management?
4. How does the **useEffect cleanup function** work? Give a real-world RN example.
5. What are **controlled vs uncontrolled components** in RN?
6. Explain **memoization** in RN — when would you use `useMemo` vs `useCallback` vs `React.memo`?
7. How does `FlatList` optimize rendering? How can you improve performance further?
8. What’s the difference between **JS thread**, **UI thread**, and **Shadow thread**?

---

## **2. Advanced React Native Ecosystem**

9. How does **EAS Build** work compared to classic Expo builds?
10. Explain how **over-the-air (OTA) updates** work and their limitations.
11. How would you implement **deep linking** in React Native?
12. What’s the difference between **React Navigation** stack and drawer navigators in terms of rendering & memory usage?
13. How do you implement **feature flags** in RN for remote control of features?
14. Explain **monorepo** setup for RN (Nx or Yarn workspaces) and its benefits.
15. How would you share UI components between RN mobile and **React Native Web**?

---

## **3. Platform Integration**

16. Describe how to set up **push notifications** for both iOS (APNs) and Android (FCM) in an Expo RN app.
17. What’s the process for integrating **In-App Purchases** in RN?
18. How do you write a **native module** in RN? Give an example use case.
19. What’s the difference between **universal links** and **custom URL schemes**?
20. How do you integrate **Firebase Analytics** into a React Native app?

---

## **4) Performance & Debugging**

21. How do you profile **JS thread performance** in RN?
22. Explain how to use **Flipper** to debug network requests and performance.
23. How would you handle **memory leaks** in React Native?
24. How do you optimize **image loading** in RN?
25. What’s the difference between `LayoutAnimation` and **Reanimated** for animations?
26. How would you prevent unnecessary re-renders in a complex RN app?

---

## **5. Architecture & Scenario-Based**

27. Your RN app has **slow startup time** — how do you diagnose and fix it?
28. How would you **architect** an RN app that works offline and syncs data when online?
29. A junior dev wrote code that works but is **unoptimized and repetitive** — how would you refactor it?
30. How do you handle **app version control** when using OTA updates to avoid breaking native features?

---

💡 **How to use this question bank in your 3-day plan:**

- **Day 1:** Questions 1–10 (Core & Advanced Ecosystem)
- **Day 2:** Questions 11–20 (Platform Integration) + 21–26 (Performance)
- **Day 3:** Questions 27–30 (Architecture/Scenario) + timed mock coding challenge

---

---

1. Explain the **React Native rendering process** — how does JS interact with native code?

- **Old arch:** JS runs on the JS thread; RN creates a **shadow tree** (Yoga for layout)) Batched updates cross the **Bridge** (serialized JSON) to the **native UIManager** which commits views on the main/UI thread.
- **New arch:** **JSI** removes JSON serialization; **Fabric** renders synchronously/asynchronously with a shared C++ core; **TurboModules** expose native modules via JSI (direct calls)) This reduces overhead and improves concurrency.

2. Difference between **React Native old architecture** and **new architecture (Fabric/TurboModules)**.

- **Old:** Bridge, async batched messages, UIManager, slow for chatty ops.
- **New:** JSI (direct function pointers), Fabric (new renderer, better diffing, concurrent rendering), TurboModules (on-demand, typed bindings), Codegen (TS/Flow → native stubs), better memory/perf and interoperability with Concurrent React.

3. How would you decide between **Zustand**, **Redux Toolkit**, and **Context API** for state management?

- **Zustand:** Minimal, ergonomic, selector-based subscription, great for **local/business logic** without boilerplate.
- **Redux Toolkit:** Standardized patterns, middleware, devtools; best for **complex/global state**, cross-team consistency, predictability.
- **Context:** Lightweight **dependency injection** (theme, auth object), not for frequently changing/large state (re-render risk).

4. How does the **useEffect cleanup function** work? Give a real-world RN example.

- Cleanup runs before the effect re-runs or on unmount—useful for unsubscribing.

```ts
useEffect(() => {
  const sub = AppState.addEventListener("change", onChange);
  return () => sub.remove(); // prevents leak
}, []);
```

5. What are **controlled vs uncontrolled components** in RN?

- **Controlled:** Value is driven by state (`value` + `onChangeText`). Single source of truth; easy validation.
- **Uncontrolled:** Internal state inside the native view (`defaultValue`, refs). Less re-renders; harder to validate centrally.

6. Explain **memoization** in RN — when would you use `useMemo` vs `useCallback` vs `React.memo`?

- **useCallback(fn, deps):** Memoize function identity → stabilize props to children.
- **useMemo(factory, deps):** Memoize **computed value** (expensive calc, derived lists).
- **React.memo(Component):** Skip re-render if props are shallow-equal. Combine with `useCallback`/`useMemo` to keep props stable.

7. How does `FlatList` optimize rendering? How can you improve performance further?

- Virtualization, windowing, recycling.
- **Do:** `keyExtractor`, `getItemLayout` (fixed height), `removeClippedSubviews`, `initialNumToRender`, `maxToRenderPerBatch`, memoized `renderItem`, `React.memo` row, `shouldComponentUpdate`/`memo`, image caching.
- Avoid inline closures that capture changing deps.

8. What’s the difference between **JS thread**, **UI thread**, and **Shadow thread**?

- **JS thread:** Runs your React/JS logic.
- **Shadow thread:** Computes layout (Yoga), produces shadow tree diffs.
- **UI (main) thread:** Applies view updates, handles gestures, drawing.

---

9. How does **EAS Build** work compared to classic Expo builds?

- **Classic:** Managed workflow only, limited config.
- **EAS Build:** Cloud builds for managed & bare, **profiles via `eas.json`**, custom native code, secrets, reproducible artifacts, support for CI and multiple variants.

10. Explain how **over-the-air (OTA) updates** work and their limitations.

- Deliver **JS + assets** instantly via EAS Update/CodePush; no store review.
- **Limits:** No native binary changes (new native modules, Info.plist/AndroidManifest changes). Use **runtime version**/binary version gating to avoid breaking changes.

11. How would you implement **deep linking** in React Native?

- Choose URL scheme + universal/app links.
- Configure React Navigation linking:

```ts
const linking = {
  prefixes: ["myapp://", "https://myapp.com"],
  config: { screens: { Post: "post/:id" } },
};
```

- iOS: Associated Domains; Android: intent filters.
- Test with `npx uri-scheme open myapp://post/42 --ios`.

12. What’s the difference between **React Navigation** stack and drawer navigators in terms of rendering & memory usage?

- **Stack:** Push/pop screens; inactive screens may stay mounted (configurable). Good for linear flows.
- **Drawer:** Usually keeps screens mounted for instant switching; higher memory footprint, great for lateral navigation.

13. How do you implement **feature flags** in RN for remote control of features?

- Use remote config/flag service (e.g., Firebase RC, LaunchDarkly).
- Boot sequence: fetch → activate → gate UI/logic. Provide **fallbacks** and **kill switches**; cache last good config; log exposures/experiments.

14. Explain **monorepo** setup for RN (Nx or Yarn workspaces) and its benefits.

- Shared **ui**, **utils**, **api** packages; single dependency graph; atomic PRs; consistent tooling.
- Use **TypeScript project references**, Metro config to resolve workspaces, and **babel-plugin-module-resolver**.

15. How would you share UI components between RN mobile and **React Native Web**?

- Use **react-native-web** + universal design system (e.g., Tamagui).
- Avoid platform-specific APIs or guard them (`Platform.select`).
- Centralize responsive styles; test on web build regularly.

---

16. Describe how to set up **push notifications** for both iOS (APNs) and Android (FCM) in an Expo RN app.

- **Server:** FCM (Android), APNs (iOS).
- **Expo managed:** `expo-notifications` to get device push token; send via Expo Push API (maps to FCM/APNs). Configure Apple Key/Team ID and Firebase keys in project; handle permission prompts; implement listeners for receipt/open events.

17. What’s the process for integrating **In-App Purchases** in RN?

- Use **react-native-iap** (bare) or **Expo IAP** (managed/bare).
- Steps: create products in stores → fetch products in app → request purchase → validate receipt **server-side** → unlock content → handle restores, pending/consumed purchases, proration, refunds.

18. How do you write a **native module** in RN? Give an example use case.

- Define TS/Flow spec → **Codegen** generates bindings → implement iOS (Swift/Obj-C) & Android (Kotlin/Java) functions → register module → call from JS.
- Example use: battery level, secure enclave, specialized SDKs.

19. What’s the difference between **universal links** and **custom URL schemes**?

- **Custom schemes:** `myapp://…`, easy, but other apps can claim same scheme; not clickable in some contexts.
- **Universal/App links:** Real HTTPS domains (`https://myapp.com/path`) verified via **apple-app-site-association**/**assetlinks.json**; more trustworthy and web-friendly; recommended.

20. How do you integrate **Firebase Analytics** into a React Native app?

- Bare: `@react-native-firebase/analytics`.
- Expo: `expo-firebase-analytics` or Segment/Amplitude SDKs.
- Log screen views (React Navigation listener) + events with params; respect privacy/consent, disable in dev builds.

---

21. How do you profile **JS thread performance** in RN?

- Enable **Hermes**; use **JS profiler** (Chrome/Hermes profiling via Flipper).
- Measure long tasks, dropped frames; instrument with `performance.now()`; avoid heavy work on startup; move work native/worker when feasible.

22. Explain how to use **Flipper** to debug network requests and performance.

- Install Flipper + RN plugin.
- Use **Network** tab for requests; **React DevTools** for component trees; **Layout/Perf** plugins for FPS & UI freezes; integrate **Crashlytics/Sentry** plugins where applicable.

23. How would you handle **memory leaks** in React Native?

- Cleanup subscriptions/timers in `useEffect`.
- Avoid retaining big objects in closures; null out refs on unmount.
- Debounce throttled listeners; unsubscribe AppState/Dimensions; verify event emitters remove listeners.
- Watch for unmounted setState → guards or `useRef(mounted)`.

24. How do you optimize **image loading** in RN?

- Use proper sizes (no full-res); `resizeMode`, width/height set.
- Cache images (`react-native-fast-image` in bare; CDN with caching headers).
- Use WebP/AVIF where supported; prefetch critical images; avoid large inline base64.

25. What’s the difference between `LayoutAnimation` and **Reanimated** for animations?

- **LayoutAnimation:** Declarative layout transitions for mount/unmount/size changes, limited control, UI thread but simple API.
- **Reanimated 2+:** Shared values, worklets on UI thread, gestures, highly performant for complex, interruptible animations. Preferred for anything beyond basic transitions.

26. How would you prevent unnecessary re-renders in a complex RN app?

- Split large components; memoize children with `React.memo`.
- Stable props via `useCallback`/`useMemo`.
- Zustand/Redux: use **selectors** and shallow compare.
- Avoid inline objects/arrays in JSX; avoid putting frequently changing state into Context.

---

27. Your RN app has **slow startup time** — how do you diagnose and fix it?

**Diagnose:** Profile startup (Time to JS bundle load, native init, first render). Check Flipper perf, Android systrace, iOS Instruments.
**Fixes:**

- Enable **Hermes**, **RAM bundles**/inline requires.
- Defer non-critical imports (lazy), code-split by route.
- Keep splash until app is ready; defer heavy network/analytics; prewarm caches.
- Reduce asset weight; avoid synchronous expensive work in root component.

28. How would you **architect** an RN app that works offline and syncs data when online?

- Local store (SQLite/WatermelonDB/Realm) + normalized cache.
- Queue mutations offline; on reconnect, **sync with conflict resolution** (server wins, client wins, or CRDT/merge policy).
- Show optimistic UI; mark records with `dirty` + `lastUpdated`.
- Background sync (Headless JS/BackgroundFetch/WorkManager); feature flags to disable sync if needed.

29. A junior dev wrote code that works but is **unoptimized and repetitive** — how would you refactor it?

- Identify duplication → extract **custom hooks** and **presentational components**.
- Add typing (TS) + ESLint/Prettier; break side effects into effects with proper deps.
- Introduce state selectors; remove unnecessary re-renders; write tests around refactored units to preserve behavior.

30. How do you handle **app version control** when using OTA updates to avoid breaking native features?

- Use **runtimeVersion** (Expo) or **binary version** targeting (CodePush) so an OTA only applies to compatible binaries.
- Gate code paths with **feature flags**; if native capability absent, hide feature.
- Semantic versioning policy; force store update when native changes are required; maintain backward-compatible JS when rolling out gradually.

---

31. What are the threads available in React Native?\*\*

React Native runs on multiple threads for performance:

| Thread                       | Purpose                                                               | Example Work                                        |
| ---------------------------- | --------------------------------------------------------------------- | --------------------------------------------------- |
| **Main Thread (UI Thread)**  | Handles all native UI rendering and user interactions.                | Drawing components, animations.                     |
| **JavaScript Thread**        | Executes all your JS/React code.                                      | Component logic, state updates.                     |
| **Shadow Thread**            | Layout calculations using Yoga layout engine.                         | Flexbox layout computation before UI update.        |
| **Native Modules Thread(s)** | Background threads for heavy native tasks (network, file operations). | Fetching data from API, reading from local storage. |

🔹 **Tip for interview**:
If asked “why multiple threads?” → Say: _It separates UI rendering from JS logic, ensuring smooth animations even if JS thread is busy._

---

32. What is Prop Drilling?\*\*

**Definition:**
Prop drilling happens when you pass data through multiple nested components that don't directly need it, just so a deeply nested component can use it.

**Example:**

```jsx
function App() {
  const user = { name: "John" };
  return <Parent user={user} />;
}

function Parent({ user }) {
  return <Child user={user} />;
}

function Child({ user }) {
  return <GrandChild user={user} />;
}

function GrandChild({ user }) {
  return <p>{user.name}</p>; // We finally use it here
}
```

Here, `user` is passed through `Parent` and `Child` even though they don't use it.

**Solution:** Use **Context API** to avoid prop drilling.

---

33. What is a React Native Bridge?\*\*

**Definition:**
React Native Bridge is the communication layer between **JavaScript** and **Native code** (Java/Kotlin for Android, Objective-C/Swift for iOS).

**How it works:**

- JS sends a message to Native via the bridge.
- Native executes platform-specific code.
- Native sends the result back via the bridge.

**Example use case:**

- Accessing camera
- Using native SDKs not available in JS

**Simple analogy:**
Think of the bridge like a translator between two people speaking different languages (JS ↔ Native).

---

34. What is State in React/React Native?\*\*

**Definition:**
State is a built-in object that stores **dynamic data** in a component, and triggers a re-render when it changes.

**Example:**

```jsx
import React, { useState } from "react";
import { View, Button, Text } from "react-native";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <View>
      <Text>Count: {count}</Text>
      <Button title="Increase" onPress={() => setCount(count + 1)} />
    </View>
  );
}
```

Here, `count` is **state** — when it changes, the UI automatically updates.

---

### Bonus: 60-second “architect answer” template

“When building for 40k+ users, I focus on **modular architecture** (feature folders), **Zustand/RTK** for predictable state, **React Query** (or custom) for caching/sync, **Reanimated** for 60fps UI, and **EAS** for multi-env builds with **OTA** for safe JS updates (guarded by runtimeVersion). I add **Flipper + Sentry** for observability, **feature flags** for safe rollout, and design **offline-first** with a background sync queue. For performance, I trim the critical path, enable **Hermes**, code-split routes, and profile with Flipper/Instruments.”
