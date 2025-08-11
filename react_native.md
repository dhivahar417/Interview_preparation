## 📘 React Native Interview Q&A (3 to 6 Years Experience)

## 🟢 Beginner React Native Questions

### 1. **What is React Native and how is it different from React?**

**Answer:**

- **React** is a JavaScript library for building user interfaces on the web, rendering to HTML elements in the browser.
- **React Native** is a framework for building native mobile applications using React, rendering to native UI components (View, Text, Image) on iOS and Android.
- **Key Differences:**
  - React renders to DOM, React Native renders to native components
  - React Native has platform-specific APIs and components
  - Styling in React Native uses StyleSheet instead of CSS
  - React Native apps can access device features (camera, GPS, etc.)

---

### 2. **What are components in React Native?**

**Answer:**
Components are reusable pieces of UI that can be composed together. In React Native:

- **Functional Components:** Use hooks and return JSX
- **Class Components:** Use lifecycle methods and render method
- **Built-in Components:** View, Text, Image, ScrollView, etc.
- **Custom Components:** User-defined components for specific functionality

---

### 3. **What is the difference between View, Text, and Image in React Native?**

**Answer:**

- **View:** A container component (similar to div in HTML) - used for layout and grouping other components
- **Text:** Displays text content - only component that can contain text directly
- **Image:** Displays images from local assets or network URLs - supports various resize modes and caching

---

### 4. **How do you apply styling in React Native?**

**Answer:**

- Use **StyleSheet.create()** for better performance and validation
- Apply styles via the `style` prop
- Styles are JavaScript objects with camelCase properties
- No CSS - all styling is done through JavaScript objects
- Support for flexbox, positioning, colors, typography, etc.

---

### 5. **What is the use of StyleSheet.create()?**

**Answer:**

- **Performance:** Optimizes style objects for better rendering performance
- **Validation:** Provides runtime validation of style properties
- **Code organization:** Groups related styles together
- **Reusability:** Allows styles to be shared between components

---

### 6. **What are props and state in React Native?**

**Answer:**

- **Props:** Immutable data passed from parent to child components (read-only)
- **State:** Mutable data managed within a component that triggers re-renders when changed
- **Props** are used for configuration and data flow
- **State** is used for component-specific data that changes over time

---

### 7. **What are the lifecycle methods of a class component?**

**Answer:**

- **Mounting:** `constructor()`, `render()`, `componentDidMount()`
- **Updating:** `render()`, `componentDidUpdate()`
- **Unmounting:** `componentWillUnmount()`
- **Error Handling:** `componentDidCatch()`
- **Note:** Modern React Native development prefers functional components with hooks

---

### 8. **How do you handle button presses or touch events?**

**Answer:**

- Use **TouchableOpacity**, **TouchableHighlight**, or **Pressable** components
- Handle events with `onPress`, `onLongPress`, `onPressIn`, `onPressOut`
- For custom touch handling, use **PanGestureHandler** or **GestureResponder**
- Example: `<TouchableOpacity onPress={() => handlePress()}>`

---

### 9. **How do you navigate between screens in React Native?**

**Answer:**

- Use **React Navigation** library (most popular)
- Configure navigation stack, tabs, or drawer
- Navigate using `navigation.navigate('ScreenName')`
- Pass parameters: `navigation.navigate('Screen', { param: value })`
- Handle back navigation and screen lifecycle

---

### 10. **How to handle forms and text inputs in React Native?**

**Answer:**

- Use **TextInput** component for text entry
- Manage input values with **useState** (controlled components)
- Handle form submission with **Button** or **TouchableOpacity**
- Validate inputs before submission
- Use **KeyboardAvoidingView** to handle keyboard appearance

---

## 🟡 Intermediate React Native Questions

### 11. **Difference between FlatList, ScrollView, and SectionList**

**Answer:**

- **ScrollView:** Renders all items at once - good for small, static content
- **FlatList:** Renders items on-demand with virtualization - optimal for large lists
- **SectionList:** Similar to FlatList but with section headers - good for categorized data
- **Performance:** FlatList and SectionList are much better for large datasets

---

### 12. **How do you optimize performance in large lists?**

**Answer:**

- Use **FlatList** instead of ScrollView
- Implement **getItemLayout** for fixed-height items
- Use **initialNumToRender** and **maxToRenderPerBatch**
- Implement **keyExtractor** for stable keys
- Use **React.memo** and **useCallback** to prevent unnecessary re-renders
- Implement **windowSize** optimization

---

### 13. **How do you handle different screen sizes and pixel densities?**

**Answer:**

- Use **Dimensions API** to get screen dimensions
- Implement responsive design with **react-native-responsive-dimensions**
- Use **PixelRatio** for device-specific scaling
- Create adaptive layouts with flexbox and percentage-based dimensions
- Test on various device sizes and orientations

---

### 14. **Difference between useState and setState**

**Answer:**

- **useState:** Hook for functional components, returns current state and setter function
- **setState:** Method for class components, can accept function or object
- **useState** is more predictable and easier to use
- **setState** can batch updates and accepts callback functions

---

### 15. **What are controlled vs uncontrolled components?**

**Answer:**

- **Controlled:** Component state is managed by React (useState), input value is tied to state
- **Uncontrolled:** Component manages its own internal state, values accessed via refs
- **Controlled** is preferred in React Native for better state management and validation
- **Uncontrolled** is less common but can be useful for simple forms

---

### 16. **Explain useEffect and its cleanup behavior**

**Answer:**

- **useEffect** runs side effects in functional components
- **Cleanup function** runs before component unmounts or before next effect runs
- Useful for subscriptions, timers, and event listeners
- **Dependency array** controls when effect runs
- Example: `useEffect(() => { /* effect */ return () => { /* cleanup */ } }, [deps])`

---

### 17. **How do you use async/await with useEffect?**

**Answer:**

- Create async function inside useEffect
- Call the async function immediately
- Handle errors with try-catch blocks
- Use cleanup to cancel ongoing operations
- Be careful with dependency arrays to prevent infinite loops

---

### 18. **What is the difference between React Navigation and React Native Navigation?**

**Answer:**

- **React Navigation:** JavaScript-based, easier setup, good performance, highly customizable
- **React Native Navigation:** Native-based, better performance, more complex setup, requires native code changes
- **React Navigation** is more popular and easier to maintain
- **React Native Navigation** provides native-level performance but more complex implementation

---

### 19. **How do you debug a React Native app?**

**Answer:**

- Use **React Native Debugger** or **Flipper**
- Enable **Hot Reloading** for development
- Use **console.log** and **console.warn**
- Implement **Error Boundaries** for crash handling
- Use **Reactotron** for state inspection
- Enable **Performance Monitor** for performance debugging

---

## 🔴 Advanced React Native Questions

### 20. **What is the React Native bridge?**

**Answer:**

- **Bridge** is the communication layer between JavaScript and native code
- **Asynchronous** communication using message queue system
- **Serialization** of data between JS and native threads
- **Performance bottleneck** - can cause delays in UI updates
- **New Architecture** (Fabric) aims to replace the bridge with direct communication

---

### 21. **How do native modules work in React Native?**

**Answer:**

- **Native modules** allow calling native code from JavaScript
- **iOS:** Written in Objective-C/Swift, exposed via RCTBridgeModule
- **Android:** Written in Java/Kotlin, exposed via ReactContextBaseJavaModule
- **Auto-linking** automatically connects native modules
- **Manual linking** required for older React Native versions

---

### 22. **What is JSI (JavaScript Interface)?**

**Answer:**

- **JSI** is part of the new React Native architecture
- **Direct communication** between JavaScript and native code
- **Synchronous calls** possible (unlike the bridge)
- **Better performance** and reduced latency
- **Foundation** for the new Fabric renderer

---

### 23. **How does Hermes improve React Native performance?**

**Answer:**

- **Hermes** is a JavaScript engine optimized for React Native
- **Faster app startup** time
- **Reduced memory usage** and smaller app size
- **Better performance** for JavaScript execution
- **Pre-compiles** JavaScript to bytecode
- **Enabled by default** in newer React Native versions

---

### 24. **What are performance bottlenecks in React Native and how do you solve them?**

**Answer:**

- **Bridge communication:** Use native modules for heavy operations
- **Large lists:** Implement FlatList with proper optimization
- **Memory leaks:** Clean up listeners, timers, and subscriptions
- **Image rendering:** Use react-native-fast-image and proper caching
- **Navigation:** Use react-native-screens for better performance
- **Animations:** Use react-native-reanimated for 60fps animations

---

### 25. **How do you implement background tasks in React Native?**

**Answer:**

- Use **react-native-background-fetch** for periodic background tasks
- Implement **Headless JS** for background processing
- Use **WorkManager** (Android) via native modules
- Handle **battery optimization** and OS restrictions
- Consider **Push notifications** for triggering background work

---

### 26. **What are memory leaks and how do you avoid them?**

**Answer:**

- **Memory leaks** occur when objects are not properly garbage collected
- **Common causes:** Unsubscribed listeners, uncleared timers, navigation state issues
- **Prevention:** Clean up in useEffect cleanup function, unsubscribe from events
- **Tools:** Use Flipper or React Native Debugger to monitor memory usage
- **Best practices:** Avoid global variables, clear intervals, remove event listeners

---

### 27. **How do you handle deep linking in React Native?**

**Answer:**

- Configure **URL schemes** in iOS and **intent filters** in Android
- Use **react-navigation** linking configuration
- Handle incoming links with **Linking API**
- Implement **universal links** for iOS
- Test deep linking on both platforms thoroughly

---

### 28. **Explain gesture handling and animations using react-native-reanimated**

**Answer:**

- **react-native-reanimated** provides 60fps animations on the UI thread
- **Gesture handling** with PanGestureHandler, PinchGestureHandler
- **Shared element transitions** between screens
- **Layout animations** for smooth UI changes
- **Worklet functions** run on UI thread for better performance

---

### 29. **How would you integrate react-query or redux-toolkit in a React Native setup?**

**Answer:**

- **React Query:** For server state management, caching, and synchronization
- **Redux Toolkit:** For client state management with simplified Redux setup
- **Integration:** Use both together - React Query for server state, Redux for app state
- **Benefits:** Better data fetching, caching, offline support, and state management

---

### 30. **What is Fabric in React Native and how does it work?**

**Answer:**

- **Fabric** is the new rendering system replacing the old bridge architecture
- **Concurrent rendering** support for better user experience
- **Direct communication** between JavaScript and native code via JSI
- **Better performance** and reduced memory usage
- **Suspense** support for loading states

---

### 31. **What is concurrent rendering and how does it affect React Native?**

**Answer:**

- **Concurrent rendering** allows React to interrupt and resume rendering work
- **Better user experience** during heavy computations
- **Priority-based updates** for more responsive UI
- **Suspense** integration for better loading states
- **Performance improvements** on lower-end devices

---

### 32. **What is TurboModules and how does it enhance performance?**

**Answer:**

- **TurboModules** is part of the new React Native architecture
- **Lazy loading** of native modules
- **Better startup performance** by loading only required modules
- **Reduced memory footprint** and faster app launch
- **Automatic linking** without manual configuration

---

### 33. **How would you structure a large-scale React Native application?**

**Answer:**

- **Feature-based architecture** with clear separation of concerns
- **Shared components** and utilities in common directories
- **State management** with Redux Toolkit or Zustand
- **Navigation** with react-navigation and proper screen organization
- **Testing** strategy with Jest and React Native Testing Library
- **Code splitting** and lazy loading for better performance

---

### 34. **How would you design a cross-platform architecture (Android, iOS, Web) using React Native?**

**Answer:**

- **React Native Web** for web platform support
- **Platform-specific code** using Platform.OS checks
- **Shared business logic** and state management
- **Platform-specific UI components** when necessary
- **Unified API layer** for consistent data handling
- **Common design system** with platform adaptations

---

### 35. **How would you architect a scalable navigation system?**

**Answer:**

- **Nested navigation** with proper screen hierarchy
- **Deep linking** configuration for all major screens
- **Authentication flow** with protected routes
- **Tab navigation** for main app sections
- **Modal presentations** for overlays and forms
- **Navigation state persistence** for better UX

---

### 36. **What is the MVVM pattern and how would you apply it in a React Native app?**

**Answer:**

- **MVVM** separates View, ViewModel, and Model
- **View:** React Native components (UI layer)
- **ViewModel:** Business logic and state management (hooks, context, Redux)
- **Model:** Data layer (API calls, local storage)
- **Benefits:** Better separation of concerns, testability, maintainability
- **Implementation:** Use custom hooks for ViewModels, services for Models

---

### 37. **How do you implement feature flagging in a React Native application?**

**Answer:**

- **Remote config** services like Firebase Remote Config
- **Feature flags** for A/B testing and gradual rollouts
- **Local fallbacks** for offline scenarios
- **Environment-specific** configurations
- **Dynamic updates** without app store releases
- **Analytics integration** for feature usage tracking

---

### 38. **How do you handle environment-specific configurations in a mobile app?**

**Answer:**

- **Environment files** (.env.development, .env.production)
- **Build-time configuration** with different schemes/configurations
- **Runtime configuration** for dynamic settings
- **Platform-specific** configurations (iOS vs Android)
- **Secure storage** for sensitive configuration data
- **Over-the-air updates** for configuration changes

---

### 39. **What are the benefits and challenges of using monorepos in React Native projects?**

**Answer:**

- **Benefits:** Shared code, consistent tooling, easier dependency management
- **Challenges:** Build complexity, larger repository size, team coordination
- **Tools:** Lerna, Nx, or Yarn workspaces for monorepo management
- **Structure:** Separate packages for shared libraries, apps, and tools
- **CI/CD:** Unified build and deployment pipelines
- **Versioning:** Coordinated releases across packages

---
