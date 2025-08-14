## **Day 1–3 Practice List: 20 Common React / React Native Code Questions**

---

### **1. Basic `useState` counter**

```jsx
import React, { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </>
  );
}
```

**Explanation:**
`useState` manages state inside functional components. Here, clicking the button updates the state and re-renders the component.

---

### **2. `useEffect` for fetching data**

```jsx
import React, { useState, useEffect } from "react";

export default function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((data) => setUsers(data));
  }, []);

  return (
    <ul>
      {users.map((u) => (
        <li key={u.id}>{u.name}</li>
      ))}
    </ul>
  );
}
```

**Explanation:**
`useEffect` runs after the first render (and when dependencies change). Empty `[]` means run once.

---

### **3. `useMemo` for expensive calculation**

```jsx
import React, { useState, useMemo } from "react";

export default function Factorial() {
  const [num, setNum] = useState(5);
  const factorial = useMemo(() => {
    console.log("Calculating...");
    return num <= 1 ? 1 : num * (num - 1);
  }, [num]);

  return (
    <>
      <input
        type="number"
        value={num}
        onChange={(e) => setNum(+e.target.value)}
      />
      <p>Factorial: {factorial}</p>
    </>
  );
}
```

**Explanation:**
`useMemo` caches results to avoid recalculating unless dependencies change.

---

### **4. `useCallback` for stable function reference**

```jsx
import React, { useState, useCallback } from "react";

function Child({ onClick }) {
  console.log("Child rendered");
  return <button onClick={onClick}>Click Me</button>;
}

export default function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Clicked");
  }, []);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
      <Child onClick={handleClick} />
    </>
  );
}
```

**Explanation:**
`useCallback` returns the same function instance unless dependencies change — avoids unnecessary re-renders of child components.

---

### **5. Context API (create + use)**

```jsx
import React, { createContext, useContext, useState } from "react";

const UserContext = createContext();

function Child() {
  const user = useContext(UserContext);
  return <p>Hello {user}</p>;
}

export default function App() {
  const [name] = useState("Dhivahar");
  return (
    <UserContext.Provider value={name}>
      <Child />
    </UserContext.Provider>
  );
}
```

**Explanation:**
`createContext` and `useContext` allow passing values without prop drilling.

---

### **6. Pass props between components**

```jsx
function Child({ message }) {
  return <p>{message}</p>;
}

export default function Parent() {
  return <Child message="Hello from Parent" />;
}
```

**Explanation:**
Props are passed as function arguments to child components.

---

### **7. Navigation param passing (React Navigation in React Native)**

```jsx
// ScreenA.js
navigation.navigate("ScreenB", { name: "Dhivahar" });

// ScreenB.js
const { name } = route.params;
<Text>{name}</Text>;
```

**Explanation:**
`navigation.navigate` sends data via params, `route.params` receives it.

---

### **8. Controlled form with `useState`**

```jsx
export default function Form() {
  const [name, setName] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Hello ${name}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

**Explanation:**
Controlled form means input value is linked to component state.

---

### **9. List rendering with `map`**

```jsx
const items = ["Apple", "Banana", "Cherry"];
return (
  <ul>
    {items.map((i, idx) => (
      <li key={idx}>{i}</li>
    ))}
  </ul>
);
```

**Explanation:**
`map` creates JSX for each element. Always use a unique `key`.

---

### **10. Conditional rendering**

```jsx
{
  isLoggedIn ? <p>Welcome</p> : <p>Please login</p>;
}
```

**Explanation:**
Use ternary operators or `&&` for conditional display.

---

### **11. Simple `FlatList` in React Native**

```jsx
import { FlatList, Text } from "react-native";

const data = [
  { id: "1", name: "Apple" },
  { id: "2", name: "Banana" },
];

<FlatList
  data={data}
  keyExtractor={(item) => item.id}
  renderItem={({ item }) => <Text>{item.name}</Text>}
/>;
```

**Explanation:**
`FlatList` efficiently renders lists in React Native.

---

### **12. Button click in React Native**

```jsx
import { Button, Alert } from "react-native";
<Button title="Click" onPress={() => Alert.alert("Hello!")} />;
```

**Explanation:**
`Button`'s `onPress` is similar to `onClick` in React.

---

### **13. Style in React Native**

```jsx
import { StyleSheet, Text } from "react-native";

const styles = StyleSheet.create({
  redText: { color: "red", fontSize: 20 },
});

<Text style={styles.redText}>Hello</Text>;
```

**Explanation:**
Styles are created using `StyleSheet.create` and passed via `style` prop.

---

### **14. API POST call**

```jsx
fetch("https://example.com/api", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ name: "Dhivahar" }),
});
```

**Explanation:**
`fetch` sends network requests. Use `POST` for sending data.

---

### **15. Lifting state up**

```jsx
function Child({ onSend }) {
  return <button onClick={() => onSend("Hello Parent")}>Send</button>;
}

function Parent() {
  const handleReceive = (msg) => alert(msg);
  return <Child onSend={handleReceive} />;
}
```

**Explanation:**
Child sends data to parent via a callback function.

---

### **16. `useReducer` example**

```jsx
import React, { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "inc":
      return { count: state.count + 1 };
    default:
      return state;
  }
}

export default function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });
  return (
    <>
      <p>{state.count}</p>
      <button onClick={() => dispatch({ type: "inc" })}>+</button>
    </>
  );
}
```

**Explanation:**
`useReducer` is an alternative to `useState` for complex state logic.

---

### **17. AsyncStorage in React Native**

```jsx
import AsyncStorage from "@react-native-async-storage/async-storage";

await AsyncStorage.setItem("name", "Dhivahar");
const name = await AsyncStorage.getItem("name");
```

**Explanation:**
AsyncStorage stores data locally on the device.

---

### **18. Simple custom hook**

```jsx
function useCounter() {
  const [count, setCount] = useState(0);
  const inc = () => setCount((c) => c + 1);
  return { count, inc };
}

function App() {
  const { count, inc } = useCounter();
  return <button onClick={inc}>{count}</button>;
}
```

**Explanation:**
Custom hooks encapsulate reusable logic.

---

### **19. Debouncing input**

```jsx
useEffect(() => {
  const timer = setTimeout(() => console.log(value), 500);
  return () => clearTimeout(timer);
}, [value]);
```

**Explanation:**
Delays execution until user stops typing.

---

### **20. Simple modal in React Native**

```jsx
import { Modal, View, Text, Button } from "react-native";

<Modal visible={show} animationType="slide">
  <View>
    <Text>Hello Modal</Text>
    <Button title="Close" onPress={() => setShow(false)} />
  </View>
</Modal>;
```

**Explanation:**
`Modal` shows content over other UI.

---
