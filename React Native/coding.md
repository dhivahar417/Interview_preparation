## **1. useMemo Example**

```jsx
import React, { useMemo, useState } from "react";

export default function App() {
  const [count, setCount] = useState(0);
  const expensiveValue = useMemo(() => {
    console.log("Calculating...");
    return count * 2;
  }, [count]);

  return (
    <div>
      <p>{expensiveValue}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

---

## **2. useCallback Example**

```jsx
import React, { useCallback, useState } from "react";

export default function App() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount((prev) => prev + 1);
  }, []);

  return <button onClick={increment}>Count: {count}</button>;
}
```

---

## **3. Context API Example**

```jsx
import React, { createContext, useContext, useState } from "react";

const MyContext = createContext();

function Child() {
  const { value } = useContext(MyContext);
  return <p>{value}</p>;
}

export default function App() {
  const [value] = useState("Hello from Context");
  return (
    <MyContext.Provider value={{ value }}>
      <Child />
    </MyContext.Provider>
  );
}
```

---

## **4. Passing Props Between Components**

```jsx
function Child({ name }) {
  return <p>{name}</p>;
}

export default function Parent() {
  return <Child name="Dhivahar" />;
}
```

---

## **5. Navigation Params (React Native)**

```jsx
// Screen1
navigation.navigate("Screen2", { userId: 123 });

// Screen2
const { userId } = route.params;
```

---

## **6. Basic Submit Form**

```jsx
import React, { useState } from "react";

export default function Form() {
  const [name, setName] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(name);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

---

## **7. Controlled Component**

```jsx
<input value={text} onChange={(e) => setText(e.target.value)} />
```

---

## **8. Fetch API Data**

```jsx
useEffect(() => {
  fetch("https://api.example.com/data")
    .then((res) => res.json())
    .then((data) => setData(data));
}, []);
```

---

## **9. Axios POST Request**

```jsx
axios.post("/api/user", { name: "John" }).then((res) => console.log(res.data));
```

---

## **10. useEffect with Cleanup**

```jsx
useEffect(() => {
  const interval = setInterval(() => console.log("Tick"), 1000);
  return () => clearInterval(interval);
}, []);
```

---

## **11. FlatList in React Native**

```jsx
<FlatList
  data={[{ id: "1", name: "Item 1" }]}
  renderItem={({ item }) => <Text>{item.name}</Text>}
  keyExtractor={(item) => item.id}
/>
```

---

## **12. Conditional Rendering**

```jsx
{
  isLoggedIn ? <p>Welcome</p> : <p>Please Login</p>;
}
```

---

## **13. Reusable Button Component**

```jsx
function Button({ label, onClick }) {
  return <button onClick={onClick}>{label}</button>;
}
```

---

## **14. Styling in React Native**

```jsx
const styles = StyleSheet.create({
  container: { padding: 20, backgroundColor: "#fff" },
});
```

---

## **15. State Lifting**

```jsx
function Child({ onValueChange }) {
  return <input onChange={(e) => onValueChange(e.target.value)} />;
}

function Parent() {
  const [val, setVal] = useState("");
  return <Child onValueChange={setVal} />;
}
```

---

## **16. React Navigation Stack**

```jsx
const Stack = createNativeStackNavigator();
<Stack.Navigator>
  <Stack.Screen name="Home" component={HomeScreen} />
</Stack.Navigator>;
```

---

## **17. Form Validation**

```jsx
if (!email.includes("@")) alert("Invalid email");
```

---

## **18. Map Through Array**

```jsx
data.map((item) => <p key={item.id}>{item.name}</p>);
```

---

## **19. useReducer Example**

```jsx
const reducer = (state, action) => {
  if (action.type === "increment") return state + 1;
  return state;
};
const [count, dispatch] = useReducer(reducer, 0);
```

---

## **20. LocalStorage Save & Load**

```jsx
localStorage.setItem("name", "Dhivahar");
const name = localStorage.getItem("name");
```

---
