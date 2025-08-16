# ✅ **20 Common React Native Code Questions (Day 1–3 Practice)**

---

### **1. Basic `useState` counter**

```jsx
import React, { useState } from "react";
import { View, Text, Button } from "react-native";

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

---

### **2. `useEffect` for fetching data**

```jsx
import React, { useState, useEffect } from "react";
import { View, Text } from "react-native";

export default function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((data) => setUsers(data));
  }, []);

  return (
    <View>
      {users.map((u) => (
        <Text key={u.id}>{u.name}</Text>
      ))}
    </View>
  );
}
```

---

### **3. `useMemo` for expensive calculation**

```jsx
import React, { useState, useMemo } from "react";
import { View, TextInput, Text } from "react-native";

export default function Factorial() {
  const [num, setNum] = useState(5);

  const factorial = useMemo(() => {
    console.log("Calculating...");
    return num <= 1 ? 1 : num * (num - 1);
  }, [num]);

  return (
    <View>
      <TextInput
        keyboardType="numeric"
        value={String(num)}
        onChangeText={(val) => setNum(+val)}
      />
      <Text>Factorial: {factorial}</Text>
    </View>
  );
}
```

---

### **4. `useCallback` for stable function reference**

```jsx
import React, { useState, useCallback } from "react";
import { View, Text, Button } from "react-native";

function Child({ onPress }) {
  console.log("Child rendered");
  return <Button title="Click Me" onPress={onPress} />;
}

export default function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Clicked");
  }, []);

  return (
    <View>
      <Text>Count: {count}</Text>
      <Button title="Increase" onPress={() => setCount(count + 1)} />
      <Child onPress={handleClick} />
    </View>
  );
}
```

---

### **5. Context API (create + use)**

```jsx
import React, { createContext, useContext, useState } from "react";
import { View, Text } from "react-native";

const UserContext = createContext();

function Child() {
  const user = useContext(UserContext);
  return <Text>Hello {user}</Text>;
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

---

### **6. Pass props between components**

```jsx
import React from "react";
import { Text } from "react-native";

function Child({ message }) {
  return <Text>{message}</Text>;
}

export default function Parent() {
  return <Child message="Hello from Parent" />;
}
```

---

### **7. Navigation param passing (React Navigation)**

```jsx
// ScreenA.js
navigation.navigate("ScreenB", { name: "Dhivahar" });

// ScreenB.js
const { name } = route.params;
<Text>{name}</Text>;
```

---

### **8. Controlled form with `useState`**

```jsx
import React, { useState } from "react";
import { View, TextInput, Button, Alert } from "react-native";

export default function Form() {
  const [name, setName] = useState("");

  const handleSubmit = () => {
    Alert.alert(`Hello ${name}`);
  };

  return (
    <View>
      <TextInput placeholder="Enter name" value={name} onChangeText={setName} />
      <Button title="Submit" onPress={handleSubmit} />
    </View>
  );
}
```

---

### **9. List rendering with `map`**

```jsx
import { View, Text } from "react-native";

const items = ["Apple", "Banana", "Cherry"];

export default function ListExample() {
  return (
    <View>
      {items.map((i, idx) => (
        <Text key={idx}>{i}</Text>
      ))}
    </View>
  );
}
```

---

### **10. Conditional rendering**

```jsx
{
  isLoggedIn ? <Text>Welcome</Text> : <Text>Please login</Text>;
}
```

---

### **11. Simple `FlatList`**

```jsx
import { FlatList, Text } from "react-native";

const data = [
  { id: "1", name: "Apple" },
  { id: "2", name: "Banana" },
];

export default function App() {
  return (
    <FlatList
      data={data}
      keyExtractor={(item) => item.id}
      renderItem={({ item }) => <Text>{item.name}</Text>}
    />
  );
}
```

---

### **12. Button click**

```jsx
import { Button, Alert } from "react-native";

<Button title="Click" onPress={() => Alert.alert("Hello!")} />;
```

---

### **13. Style in React Native**

```jsx
import { StyleSheet, Text } from "react-native";

const styles = StyleSheet.create({
  redText: { color: "red", fontSize: 20 },
});

<Text style={styles.redText}>Hello</Text>;
```

---

### **14. API POST call**

```jsx
fetch("https://example.com/api", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ name: "Dhivahar" }),
});
```

---

### **15. Lifting state up**

```jsx
import React from "react";
import { View, Button, Alert } from "react-native";

function Child({ onSend }) {
  return <Button title="Send" onPress={() => onSend("Hello Parent")} />;
}

export default function Parent() {
  const handleReceive = (msg) => Alert.alert(msg);
  return (
    <View>
      <Child onSend={handleReceive} />
    </View>
  );
}
```

---

### **16. `useReducer` example**

```jsx
import React, { useReducer } from "react";
import { View, Text, Button } from "react-native";

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
    <View>
      <Text>{state.count}</Text>
      <Button title="+" onPress={() => dispatch({ type: "inc" })} />
    </View>
  );
}
```

---

### **17. AsyncStorage**

```jsx
import AsyncStorage from "@react-native-async-storage/async-storage";

await AsyncStorage.setItem("name", "Dhivahar");
const name = await AsyncStorage.getItem("name");
```

---

### **18. Simple custom hook**

```jsx
import React, { useState } from "react";
import { Button } from "react-native";

function useCounter() {
  const [count, setCount] = useState(0);
  const inc = () => setCount((c) => c + 1);
  return { count, inc };
}

export default function App() {
  const { count, inc } = useCounter();
  return <Button title={String(count)} onPress={inc} />;
}
```

---

### **19. Debouncing input**

```jsx
import React, { useEffect } from "react";

useEffect(() => {
  const timer = setTimeout(() => console.log(value), 500);
  return () => clearTimeout(timer);
}, [value]);
```

---

### **20. Simple modal**

```jsx
import { Modal, View, Text, Button } from "react-native";

<Modal visible={show} animationType="slide">
  <View>
    <Text>Hello Modal</Text>
    <Button title="Close" onPress={() => setShow(false)} />
  </View>
</Modal>;
```

---
