# **Props in React (Beginner Notes)**

## **1. What are Props?**

* **Props** (short for **properties**) are a way to pass **data from a parent component to a child component** in React.
* They are **read-only**, which means the child component **cannot modify them**.

Think of props as **parameters** in a function.

---

## **2. How to Use Props**

### **Step 1: Parent Component passes props**

```jsx
import React from 'react';
import Child from './Child';

function Parent() {
  return (
    <div>
      <h1>Welcome to React Props!</h1>
      <Child name="John" age={25} />
    </div>
  );
}

export default Parent;
```

### **Step 2: Child Component receives props**

```jsx
import React from 'react';

function Child(props) {
  return (
    <div>
      <p>Name: {props.name}</p>
      <p>Age: {props.age}</p>
    </div>
  );
}

export default Child;
```

**Explanation:**

* `Parent` passes `name` and `age` to `Child`.
* `Child` accesses them using `props.name` and `props.age`.

---

## **3. Default Props**

* You can define **default values** for props if the parent doesn’t pass them.

```jsx
function Child(props) {
  return (
    <div>
      <p>Name: {props.name}</p>
      <p>Age: {props.age}</p>
    </div>
  );
}

// Default props
Child.defaultProps = {
  name: "Anonymous",
  age: 18
};

export default Child;
```

**Explanation:**
If `Parent` doesn’t pass `name` or `age`, `Child` will use the default values.

---

## **4. Prop Types**

* Prop types help **check the type of props** and show a warning if it’s the wrong type.
* You need to install `prop-types` first:

```bash
npm install prop-types
```

```jsx
import React from 'react';
import PropTypes from 'prop-types';

function Child(props) {
  return (
    <div>
      <p>Name: {props.name}</p>
      <p>Age: {props.age}</p>
    </div>
  );
}

// Prop type checking
Child.propTypes = {
  name: PropTypes.string,
  age: PropTypes.number
};

export default Child;
```

**Explanation:**

* `PropTypes.string` → expects a string.
* `PropTypes.number` → expects a number.
* If a wrong type is passed, React will show a **warning in the console**.

---

## **5. Key Points to Remember**

1. Props are **read-only**.
2. Passed from **Parent → Child**.
3. Can have **default values** using `defaultProps`.
4. Can **check type** using `PropTypes`.

---


## **1. App.jsx (Parent Component)**

```jsx
import React from 'react';
import Child from './Child';

function App() {
  return (
    <div>
      <h1>React Props Example</h1>
      
      {/* Passing props to Child */}
      <Child name="Alice" age={20} />
      <Child name="Bob" age={25} />
      
      {/* Child without props will use default props */}
      <Child />
    </div>
  );
}

export default App;
```

---

## **2. Child.jsx (Child Component)**

```jsx
import React from 'react';
import PropTypes from 'prop-types';

function Child(props) {
  return (
    <div style={{border: "1px solid black", margin: "10px", padding: "10px"}}>
      <p>Name: {props.name}</p>
      <p>Age: {props.age}</p>
    </div>
  );
}

// Default props
Child.defaultProps = {
  name: "Anonymous",
  age: 18
};

// Prop types
Child.propTypes = {
  name: PropTypes.string,
  age: PropTypes.number
};

export default Child;
```

---

## **3. Output**

When you run the app, you’ll see:

```
React Props Example
-------------------
Name: Alice
Age: 20

Name: Bob
Age: 25

Name: Anonymous
Age: 18
```

---

✅ **Explanation:**

1. `App.jsx` passes props (`name` and `age`) to `Child.jsx`.
2. `Child.jsx` displays the props using `{props.name}` and `{props.age}`.
3. If props are missing, default values (`Anonymous`, `18`) are used.
4. `PropTypes` ensure the props have the correct data type.

---
