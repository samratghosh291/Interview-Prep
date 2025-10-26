# 📝 React + ES6/ES7 Mini Cheat Sheet

A concise guide to essential **ES6/ES7 concepts** used in React development with **practical examples**. Perfect for quick reference while coding.

---

## 1️⃣ Arrow Functions (`=>`)

* Short syntax for functions.
* Lexical `this` — avoids `.bind(this)` in class components.

```jsx
// Functional component with arrow function
const Button = ({ onClick, label }) => (
  <button onClick={onClick}>{label}</button>
);

// Arrow function inside component
const Counter = () => {
  const [count, setCount] = React.useState(0);
  const increment = () => setCount(count + 1);
  return <button onClick={increment}>{count}</button>;
};
```

---

## 2️⃣ Destructuring

* Extract props, state, or array elements cleanly.

```jsx
const UserCard = ({ user }) => {
  const { name, age, email } = user;
  return (
    <div>
      <h2>{name}</h2>
      <p>{age} years old</p>
      <p>{email}</p>
    </div>
  );
};

// Array destructuring with useState
const Counter = () => {
  const [count, setCount] = React.useState(0);
};
```

---

## 3️⃣ Modules (`import` / `export`)

* Organize components and reuse code.

```jsx
// MyComponent.js
export default function MyComponent() {
  return <h1>Hello Module</h1>;
}

// App.js
import MyComponent from './MyComponent';
const App = () => <MyComponent />;
```

---

## 4️⃣ Classes (Class Components)

* Still common in legacy React codebases.
* Works with `this.state` and lifecycle methods.

```jsx
class Counter extends React.Component {
  state = { count: 0 };

  increment = () => this.setState({ count: this.state.count + 1 });

  render() {
    return <button onClick={this.increment}>{this.state.count}</button>;
  }
}
```

---

## 5️⃣ Template Literals

* Embed variables in strings or classNames dynamically.

```jsx
const UserGreeting = ({ name }) => <h1>{`Hello, ${name}!`}</h1>;

const Button = ({ size }) => {
  const className = `btn btn-${size}`;
  return <button className={className}>Click Me</button>;
};
```

---

## 6️⃣ Spread (`...`) & Rest (`...`) Operators

* Spread: clone objects/arrays or pass props.
* Rest: extract remaining properties.

```jsx
// Spread example
const oldState = { a: 1, b: 2 };
const newState = { ...oldState, b: 3 }; // { a: 1, b: 3 }

// Props spreading
const UserCard = ({ name, age, ...rest }) => (
  <div {...rest}>{name} - {age}</div>
);

// Rest example
const { id, ...userData } = { id: 1, name: 'Sam', age: 25 };
// userData = { name: 'Sam', age: 25 }
```

---

## 7️⃣ Array Methods (map, filter, reduce)

* Essential for rendering lists or transforming data.

```jsx
const users = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" }
];

const UserList = () => (
  <ul>
    {users.map(user => (
      <li key={user.id}>{user.name}</li>
    ))}
  </ul>
);

// Filter example
const adults = users.filter(u => u.age >= 18);

// Reduce example
const totalAge = users.reduce((sum, u) => sum + (u.age || 0), 0);
```

---

## 8️⃣ Let and Const

* `const` for variables that don’t change.
* `let` for reassignable variables.
* Prevents bugs with accidental reassignment.

```jsx
const name = "React";
// name = "Vue"; // ❌ Error

let count = 0;
count += 1; // ✅ Reassignable
```

---

## 9️⃣ Promises & Async/Await

* Used for fetching data inside `useEffect`.

```jsx
import { useEffect, useState } from 'react';

const DataFetcher = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      const res = await fetch('https://jsonplaceholder.typicode.com/users');
      const json = await res.json();
      setData(json);
    };
    fetchData();
  }, []);

  return <pre>{JSON.stringify(data, null, 2)}</pre>;
};
```

---

## 🔟 Default Parameters

* Avoids undefined values in functions/components.

```jsx
const Greeting = ({ name = "Guest" }) => <h1>Hello, {name}!</h1>;

// Usage
<Greeting />          // Hello, Guest!
<Greeting name="Sam"/> // Hello, Sam!
```

---

## ⭐ Bonus ES7+ Features

### Optional Chaining (`?.`)

```jsx
const username = user?.profile?.name; // safe access
```

### Nullish Coalescing (`??`)

```jsx
const displayName = name ?? "Anonymous";
```

### Object Shorthand

```jsx
const age = 25;
const name = "Sam";
const user = { name, age }; // same as { name: name, age: age }
```

---

## ✅ Top 5 Must-Know for React

1. **Arrow Functions** → Event handlers, concise JSX.
2. **Destructuring** → Cleaner props/state access.
3. **Spread/Rest** → Immutability, props forwarding.
4. **Modules** → Component organization.
5. **Promises/Async-Await** → Data fetching.

---

