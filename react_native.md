## 📘 React Native Interview Q\&A (3 to 6 Years Experience)

### 1. **What is the difference between React and React Native?**

**Answer:**

- **React** is used for building web applications; it renders HTML in the browser.
- **React Native** is used for building mobile applications; it renders native components using a bridge.

---

### 2. **How does the React Native bridge work?**

**Answer:**
React Native uses a **JavaScript bridge** to communicate between the JavaScript thread and the native thread (Objective-C/Swift for iOS and Java/Kotlin for Android). The bridge is asynchronous and enables the two threads to talk using a message queue system.

---

### 3. **How do you handle performance optimization in React Native apps?**

**Answer:**

- Use **FlatList** instead of ScrollView for large lists.
- Use **useMemo**, **useCallback**, and **React.memo** to avoid unnecessary re-renders.
- Avoid unnecessary state changes.
- Use **native modules** when performance-intensive operations are required.
- Use libraries like **Reanimated** and **React Native Screens** for smoother navigation.

---

### 4. **What is the role of Metro Bundler?**

**Answer:**
Metro is the JavaScript bundler used by React Native. It:

- Transforms JS code into a bundle that can be loaded by the mobile app.
- Watches files and provides hot reloading during development.

---

### 5. **What are some common performance bottlenecks in React Native?**

**Answer:**

- Unoptimized images and animations.
- Inefficient list rendering (ScrollView with large data).
- Excessive re-renders due to poor state management.
- Unbatched updates and expensive layout calculations.

---

### 6. **How do you handle deep linking in React Native?**

**Answer:**
Use the `react-navigation` library along with the `Linking` module:

- Define route prefixes.
- Handle incoming links in the `Linking.addEventListener` or `useLinking` hooks.
- Configure for both Android (intent filters) and iOS (URL schemes or universal links).

---

### 7. **How do you persist user login/session in a React Native app?**

**Answer:**

- Use `AsyncStorage`, `MMKV`, or secure storage libraries to persist tokens.
- Implement an **auth context** or Redux to manage global login state.
- Check token validity on app launch (e.g., in a splash screen).

---

### 8. **How do you secure API communication in React Native?**

**Answer:**

- Use HTTPS.
- Store sensitive data securely using `react-native-encrypted-storage`.
- Implement token refresh and expiration handling.
- Use **JWT**, and verify signatures on the server.

---

### 9. **What is the difference between controlled and uncontrolled components in React Native forms?**

**Answer:**

- **Controlled**: The value is tied to state (`useState`), updated on every keystroke.
- **Uncontrolled**: Uses refs to get input values only when needed (less common in RN).

---

### 10. **How do you handle background tasks in React Native?**

**Answer:**

- Use libraries like `react-native-background-fetch` or `react-native-background-task`.
- On Android, use **WorkManager** via native modules.
- Be mindful of **battery optimizations** and **OS-level restrictions**.

---

### 11. **Can you explain a real-time push notification implementation in React Native?**

**Answer:**

- Use **Firebase Cloud Messaging (FCM)** with `@react-native-firebase/messaging`.
- Request notification permissions.
- Handle messages with:

  - `onMessage` (foreground),
  - `setBackgroundMessageHandler` (background),
  - Notification tap actions.

- Integrate with Laravel/Node backend using FCM tokens.

---

### 12. **Real-Time Scenario: App crashing on launch in Android release build – how would you debug it?**

**Answer:**

- Use `adb logcat` to check native crash logs.
- Verify if ProGuard rules are misconfigured.
- Check for missing native dependencies.
- Test with `./gradlew assembleRelease` and install APK manually.

---

### 13. **How do you handle image caching in React Native?**

**Answer:**

- Use libraries like `react-native-fast-image` for better caching support.
- Use proper `resizeMode` and `imageCache` headers.
- Avoid loading large images in high-resolution devices unnecessarily.

---

### 14. **How do you implement offline support in a React Native app?**

**Answer:**

- Use libraries like:

  - `react-native-netinfo` to detect connectivity.
  - `redux-persist` or `realm`/`watermelondb` for local data storage.

- Queue offline actions and sync when online.

---

### 15. **How do you monitor crashes and performance in production React Native apps?**

**Answer:**

- Use tools like:

  - **Sentry** or **Firebase Crashlytics** for crash reports.
  - **Reactotron** (for dev).
  - **Flipper** with plugins for state inspection, performance.

---

### 16. **How do you handle offline data in React Native apps?**

**Answer:**
Use libraries like `redux-persist` or `AsyncStorage` to cache app data locally. For complex needs (e.g., syncing when online), use offline-first DBs like **Realm** or **WatermelonDB**, combined with background sync logic.

---

### 17. **Real-Time Scenario: How would you handle a mobile chat application?**

**Answer:**

- Use **WebSockets** or libraries like `Socket.IO` for real-time communication.
- Store recent chats using **local DB** (e.g., Realm).
- Use **push notifications** for new messages.
- Render messages using `FlatList`, optimizing with `keyExtractor`, `inverted`, and `initialNumToRender`.

---

### 18. **How do you optimize performance in large lists?**

**Answer:**
Use `FlatList` or `SectionList` with:

- `initialNumToRender`
- `maxToRenderPerBatch`
- `windowSize`
- Memoization via `React.memo()` or `useCallback`
- Avoid anonymous functions inside render.

---

### 19. **How do you implement dark mode?**

**Answer:**

- Use `useColorScheme()` from `react-native`.
- Integrate with a `ThemeProvider` (e.g., via `styled-components` or `react-native-paper`).
- Create dynamic themes and switch styles conditionally based on theme mode.

---

### 20. **What are the common causes of memory leaks in React Native apps?**

**Answer:**

- Unsubscribed listeners (e.g., event or socket listeners).
- Not clearing intervals or timers.
- Holding references to large objects in closures or global scope.
- Incorrect navigation state handling (not unmounting screens).

---

### 21. **Real-Time Scenario: App is crashing randomly in production. How would you debug it?**

**Answer:**

- Integrate **Sentry** or **Firebase Crashlytics** to capture errors.
- Analyze logs and crash traces.
- Test using similar devices or conditions.
- Reproduce and patch with CodePush or a new build.

---

### 22. **What’s your approach for deep linking in React Native?**

**Answer:**

- Use `react-navigation`’s **Linking configuration**.
- On iOS: Configure `CFBundleURLTypes`.
- On Android: Update `AndroidManifest.xml` with intent filters.
- Use `Linking.getInitialURL()` and `Linking.addEventListener()` to handle links.

---

### 23. **Explain the difference between React Navigation and React Native Navigation.**

**Answer:**

| Feature       | React Navigation | React Native Navigation (Wix) |
| ------------- | ---------------- | ----------------------------- |
| Type          | JS-based         | Native-based                  |
| Ease of Setup | Easy             | More complex                  |
| Performance   | Good             | Excellent (native-level)      |
| Customization | High             | Requires native code changes  |

---

### 24. **How do you handle authentication in React Native?**

**Answer:**

- Use secure storage (e.g., `react-native-keychain`, `SecureStore`, or `AsyncStorage` with encryption).
- For login flows, use `Context API` or `Redux`.
- Persist tokens and check on app start.
- Use refresh tokens and interceptors for token expiry.

---

### 25. **How do you manage themes and responsive design in React Native?**

**Answer:**

- Themes: Use `ThemeProvider` and `useColorScheme()` for light/dark mode.
- Responsive UI: Use `Dimensions`, `react-native-responsive-dimensions`, or `react-native-size-matters`.
- Consider `react-native-paper` or `NativeBase` for built-in theming.

---
