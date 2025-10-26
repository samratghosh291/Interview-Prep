## **1. What is `useEffect`?**

`useEffect` is a **React Hook** that lets you perform **side effects** in your functional components.

> Side effects are actions that affect something outside the function scope, like:

* Fetching data from an API
* Updating the DOM manually
* Setting up subscriptions or timers
* Logging values

In React **functional components**, you can’t directly do these in the main function without causing problems. `useEffect` allows you to safely run them **after the component renders**.

---

## **2. Why do we use `useEffect`?**

* To **run code after the component renders**
* To **avoid running code on every render** unnecessarily
* To **fetch data from APIs**
* To **set up and clean up resources** (like timers, subscriptions)

---

## **3. When should we use `useEffect`?**

* **Fetching data** when a component loads
* **Listening for events** like window resizing
* **Updating the DOM** after state changes
* **Cleaning up resources** when the component unmounts

---

## **4. Syntax of `useEffect`**

```javascript
useEffect(() => {
  // Your side effect code here

  return () => {
    // Optional cleanup code
  };
}, [dependencies]);
```

* The first argument is a **function** where you write your effect
* The second argument is an **array of dependencies**:

  * `[]` → run once on mount
  * `[state]` → run when `state` changes
  * omitted → run after **every render**

---

## **5. Example with App.jsx and another component**

### **Counter.jsx** (child component)

```javascript
import React, { useEffect, useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  // Effect runs when component mounts and when `count` changes
  useEffect(() => {
    console.log("Count changed:", count);
    document.title = `Count: ${count}`;

    return () => {
      console.log("Cleanup if needed before next effect or unmount");
    };
  }, [count]);

  return (
    <div>
      <h2>Counter: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;
```

---

### **App.jsx**

```javascript
import React from "react";
import Counter from "./Counter";

function App() {
  return (
    <div>
      <h1>React useEffect Example</h1>
      <Counter />
    </div>
  );
}

export default App;
```

---

### **Explanation of Example:**

1. The `Counter` component has a **state** `count`.
2. `useEffect` runs **every time `count` changes**.
3. It updates the **document title** with the current count.
4. Cleanup function logs something before the next effect or unmount.

✅ This is a very common pattern in React apps.

---
