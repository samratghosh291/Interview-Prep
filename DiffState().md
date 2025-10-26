## 1. `useState`

**What it is:**

* A hook to **store state in a functional component**.
* Think of state as data that changes over time and affects what is shown on the UI.

**When to use:**

* When you need to **store and update values** in a component.
* Example: input field value, toggle button state, counter, fetched data from an API.

**How to use:**

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0); // 0 is initial value

  const increment = () => setCount(count + 1);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

**Sense behind using it:**

* Without `useState`, functional components can’t "remember" values between renders.
* Makes your component **reactive** to user actions.

---

## 2. `useEffect`

**What it is:**

* A hook to **perform side effects** in functional components.
* Side effects = tasks that happen **outside rendering** like API calls, timers, logging, subscriptions.

**When to use:**

* Fetching data when a component mounts.
* Running code when certain state/props change.
* Cleaning up things like event listeners or timers.

**How to use:**

```javascript
import { useState, useEffect } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(prev => prev + 1);
    }, 1000);

    return () => clearInterval(interval); // cleanup on unmount
  }, []); // empty array => runs once on mount

  return <p>Seconds: {seconds}</p>;
}
```

**Sense behind using it:**

* Allows functional components to **interact with the world outside of React’s render cycle**.
* Think of it like saying: “Do this after render, or when this value changes.”

---

## 3. `useContext`

**What it is:**

* A hook to **access React Context** directly in a functional component.
* Context = a way to **share data globally** without prop drilling (passing props through every intermediate component).

**When to use:**

* You have **data or functions that many components need**.
* Examples: theme (dark/light mode), user authentication info, language settings.

**How to use:**

```javascript
import { createContext, useContext } from "react";

const ThemeContext = createContext("light");

function ThemedButton() {
  const theme = useContext(ThemeContext); // directly get context
  return <button style={{ background: theme === "dark" ? "#333" : "#fff" }}>Click me</button>;
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <ThemedButton />
    </ThemeContext.Provider>
  );
}
```

**Sense behind using it:**

* Avoids passing the same props **through many layers**.
* Makes components **simpler and more reusable**.

---

## 4. `useRef`

**What it is:**

* A hook to **create a reference** to a DOM element or **store mutable value** that persists across renders.
* Unlike `useState`, updating a ref **does not trigger a re-render**.

**When to use:**

* Accessing a DOM element (like input focus, scroll position).
* Storing a value **between renders** without causing re-render.

**How to use:**

```javascript
import { useRef } from "react";

function TextInput() {
  const inputRef = useRef();

  const focusInput = () => inputRef.current.focus();

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

**Sense behind using it:**

* Lets you **directly interact with DOM** or keep a “persistent variable” **without re-rendering** your component unnecessarily.

---

### ✅ Quick Comparison Table

| Hook         | What it does                | When to use                           | Causes re-render?          |
| ------------ | --------------------------- | ------------------------------------- | -------------------------- |
| `useState`   | Store component state       | Dynamic values in component           | Yes                        |
| `useEffect`  | Run side effects            | API calls, timers, subscriptions      | No (runs after render)     |
| `useContext` | Access global/shared data   | Avoid prop drilling, theme, auth info | Yes (when context changes) |
| `useRef`     | Access DOM or persist value | DOM focus, scroll, mutable variable   | No                         |

---

💡 **Mental Tip:**

* **State = “React remembers this and updates UI”**
* **Effect = “React do this after render or when something changes”**
* **Context = “React give me this shared global data”**
* **Ref = “React give me a handle to a DOM element or persistent variable”**



---

## **What is "Mount" in React?**

In React, **mounting** refers to the process when a component is **created and inserted into the DOM for the first time**.

Think of it like **placing a new component on the screen**.

**Lifecycle of a component (simplified):**

1. **Mount** – Component is created and added to the DOM.
2. **Update** – Component updates because state or props changed.
3. **Unmount** – Component is removed from the DOM.

So **“mount” happens only once** at the very beginning.

---

## **Practical Example of Using Mount**

Most commonly, **you use mounting when you want something to happen only once when the component appears**.

### Example: Fetching data from an API when the component loads

```javascript
import { useState, useEffect } from "react";

function UsersList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    // This code runs only once when the component mounts
    fetch("https://jsonplaceholder.typicode.com/users")
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []); // empty dependency array => runs only on mount

  return (
    <div>
      <h2>Users</h2>
      <ul>
        {users.map(user => <li key={user.id}>{user.name}</li>)}
      </ul>
    </div>
  );
}
```

**Explanation:**

* `useEffect(..., [])` → runs **only when the component mounts**.
* Fetches data **once**, not on every re-render.
* Perfect for initialization tasks: API calls, subscriptions, timers, etc.

---

### Another Practical Example: Focusing an input when the component mounts

```javascript
import { useEffect, useRef } from "react";

function LoginForm() {
  const inputRef = useRef();

  useEffect(() => {
    // Focus input when component mounts
    inputRef.current.focus();
  }, []); // empty array => runs only once

  return <input ref={inputRef} placeholder="Enter username" />;
}
```

✅ **Key Idea:**

* Mount = first appearance of component.
* Anything you want to do **only once when the component appears**, do it inside a `useEffect` with an empty dependency array (`[]`).

---

