## **1. What is Context in React?**

In React, **Context** is a way to **share data between components** without having to pass props manually through every level of the component tree.

Normally, if you have deeply nested components, passing data through each level using props can become cumbersome. Context solves this problem.

**Example of what Context is for:**

* Theme (dark/light)
* Authenticated user info
* Language settings

---

## **2. What is `useContext()`?**

`useContext()` is a **React hook** that lets you **consume context values** in a functional component.

**Syntax:**

```javascript
const value = useContext(MyContext);
```

Where `MyContext` is a context created using `React.createContext()`.

---

## **3. Why and When to Use Context**

**Why use it?**

* To avoid “prop drilling” (passing props through many layers).
* To share global state like theme, auth, or settings.

**When to use it?**

* When multiple components need the same data.
* When the data is **global** to the app (not specific to just one component).

**Note:** Don’t overuse Context for everything—props are still simpler for local state.

---

## **4. Simple Example**

We’ll create a small React app with:

1. `App.jsx` → main component
2. `ThemeContext.jsx` → define context
3. `Header.jsx` → nested component consuming the context

---

### **ThemeContext.jsx**

```javascript
import React, { createContext, useState } from "react";

// 1. Create Context
export const ThemeContext = createContext();

export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState("light");

  const toggleTheme = () => {
    setTheme(prev => (prev === "light" ? "dark" : "light"));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};
```

---

### **Header.jsx**

```javascript
import React, { useContext } from "react";
import { ThemeContext } from "./ThemeContext";

const Header = () => {
  const { theme, toggleTheme } = useContext(ThemeContext);

  return (
    <header style={{ 
      background: theme === "light" ? "#eee" : "#333",
      color: theme === "light" ? "#000" : "#fff",
      padding: "10px"
    }}>
      <h1>Current Theme: {theme}</h1>
      <button onClick={toggleTheme}>Toggle Theme</button>
    </header>
  );
};

export default Header;
```

---

### **App.jsx**

```javascript
import React from "react";
import { ThemeProvider } from "./ThemeContext";
import Header from "./Header";

function App() {
  return (
    <ThemeProvider>
      <div>
        <Header />
        <p>This is the app content.</p>
      </div>
    </ThemeProvider>
  );
}

export default App;
```

---

### ✅ **How it works**

1. `ThemeContext` provides the theme state to the entire tree.
2. `App.jsx` wraps everything inside `ThemeProvider`.
3. `Header.jsx` uses `useContext(ThemeContext)` to **read the current theme** and **toggle it**.
4. No need to pass props from App → Header.

---


Do you want me to do that?
