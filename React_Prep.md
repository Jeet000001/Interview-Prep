# React Fundamentals

## 1. What is React?

React is an open-source JavaScript library used for building fast and interactive user interfaces, especially for Single Page Applications (SPAs). It was developed and is maintained by Meta

React follows a component-based architecture, which means the UI is divided into small, reusable, and independent components. This makes applications easier to develop, maintain, and scale.

One of React's key features is the Virtual DOM. Instead of updating the real DOM directly, React first updates a virtual representation of the DOM, compares the changes, and then updates only the necessary parts of the real DOM. This improves performance and provides a better user experience.

## 2. Why is React called a library and not a framework?

React is called a library because it primarily focuses on building the UI (View Layer) of an application. It doesn't provide a complete solution for application development out of the box.

A framework, on the other hand, provides a complete structure and set of rules for building an application, including routing, state management, form handling, HTTP requests, and more.

With React, developers have the freedom to choose additional libraries according to their project's needs. For example:

- Routing → React Router
- State Management → Redux or Zustand
- Data Fetching → TanStack Query
  This flexibility is why React is considered a library rather than a framework.

## 3. What is SPA (Single Page Application)?

A Single Page Application (SPA) is a web application that loads a single HTML page initially and then dynamically updates the content without reloading the entire page.

Instead of requesting a new page from the server on every navigation, the SPA uses JavaScript to update only the necessary parts of the UI. This creates a faster and smoother user experience.

React is commonly used to build SPAs because it efficiently updates the UI using the Virtual DOM.

### Advantages -

- Faster user experience after initial load
- Less server load because only data is exchanged
- Smooth navigation without full page refresh
- Better for highly interactive applications
- Easier to create app-like experiences

### Disadvantages -

- Initial bundle size can be large
- SEO can be challenging without SSR
- First page load may be slower
- Requires JavaScript to function properly

## 4. What is Virtual DOM?

The Virtual DOM (VDOM) is a lightweight copy of the actual DOM maintained by React.

When the state or props of a component change, React does not directly update the real DOM. Instead, it first updates the Virtual DOM, compares it with the previous Virtual DOM version, identifies the changes, and then updates only the affected parts of the real DOM.

This process makes UI updates more efficient and improves application performance.

### How Virtual DOM Works

1. Initial render creates a Virtual DOM tree.
2. State or props change.
3. React creates a new Virtual DOM tree.
4. React compares the new tree with the previous tree (Diffing).
5. React identifies the minimum required changes.
6. React updates only those parts in the real DOM (Reconciliation).

### Why Not Update the Real DOM Directly?

Direct DOM manipulation is expensive because:

- Browser needs to recalculate layout.
- Browser may repaint elements.
- Frequent updates can affect performance.

The Virtual DOM minimizes unnecessary DOM operations.

#### Diffing

The process of comparing the old Virtual DOM with the new Virtual DOM.

#### Reconciliation

The process of updating the real DOM based on the differences found during diffing.

## 5. What is JSX?

JSX (JavaScript XML) is a syntax extension for JavaScript that allows us to write HTML-like code inside JavaScript.

React uses JSX to describe what the UI should look like. JSX makes component code more readable and easier to write compared to using pure JavaScript functions like React.createElement().

Browsers do not understand JSX directly. During the build process, tools like Babel conert JSX into regular JavaScript.

JSX

```js
const element = <h1>Hello, React!</h1>;
```

Converted JavaScript

```js
const element = React.createElement("h1", null, "Hello, React!");
```

## What are components in React?

Components are the building blocks of a React application. A component is a reusable, independent piece of UI that contains its own structure, logic, and behavior.

Instead of creating an entire page as one large file, React encourages breaking the UI into smaller reusable components, making the application easier to develop, maintain, and scale.

## Difference between functional and class components?

In React, both Functional Components and Class Components are used to create UI components. However, modern React development primarily uses Functional Components because they are simpler, easier to read, and support Hooks.

Class Components were the standard way to manage state and lifecycle methods before Hooks were introduced in React 16.8.

### Functional Component -

```js
const Welcome = () => {
  return <h1>Hello World</h1>;
};
```

### Clss Component -

```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello World</h1>;
  }

```

## 6. What is component reusability?

Component Reusability is the ability to create a component once and use it multiple times in different parts of an application by passing different data through props.

Instead of writing the same UI and logic repeatedly, we create a reusable component and customize its behavior using props. This reduces code duplication, improves maintainability, and makes applications easier to scale.

# Props & State

## 7. What are props?

Props (short for Properties) are used to pass data from a parent component to a child component in React.

They allow components to be dynamic and reusable by receiving different values instead of hardcoding data.

Props are read-only (immutable), which means a child component cannot directly modify the props it receives.

### example :

Parent Component -

```js
function App() {
  return <User name="John" />;
}
```

Child Component -

```js
function User(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

## 8. What is state?

State is a built-in React feature used to store and manage data that can change over time within a component.

When the state changes, React automatically re-renders the component and updates the UI to reflect the new state.

Unlike props, which are passed from a parent component and are read-only, state is managed and updated by the component itself.

### Example -

```js
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
}
```

## 9. State vs Props

Props are used to pass data from parent components to child components and are read-only. State is used to manage dynamic data within a component and can be updated using React's state management functions.

## 10. What is lifting state up?

Lifting State Up is a React pattern where state is moved from a child component to the closest common parent component so that multiple child components can share and synchronize the same data.

When two or more components need access to the same state, instead of maintaining separate copies of that state, we "lift" the state to their common parent and pass it down through props.

## 11. What is prop drilling?

Prop Drilling is a situation in React where props are passed through multiple intermediate components just to reach a deeply nested child component that actually needs the data.

The intermediate components do not use the props themselves; they only forward them to the next component.

This can make the code harder to read, maintain, and scale.

## 12. How do you avoid prop drilling?

Prop Drilling can be avoided by using state-sharing techniques that allow components to access data directly without passing props through multiple intermediate components.

The most common solutions are:

1. Context API
2. State Management Libraries (Redux, Zustand, Jotai, etc.)
3. Component Composition
4. Keeping State Close to Where It's Needed

## 13. What are controlled components?

A Controlled Component is a form element whose value is controlled by React state rather than the DOM itself.

In a controlled component, React becomes the single source of truth for the form data. The input value is stored in state, and every change updates the state using an event handler.

### Example -

```js
import { useState } from "react";

function LoginForm() {
  const [username, setUsername] = useState("");

  return (
    <input
      type="text"
      value={username}
      onChange={(e) => setUsername(e.target.value)}
    />
  );
}
```

### How It Works -

1. User types in the input.
2. onChange event fires.
3. React updates the state.
4. Updated state is assigned back to value.
5. UI re-renders with the new value.

## 14. What are uncontrolled components?

Uncontrolled Components are form elements where the DOM itself manages the form data, instead of React state.

In uncontrolled components, React does not control the input value through useState. Instead, we use a ref to directly access the value from the DOM when needed.

### Example -

```js
import { useRef } from "react";

function LoginForm() {
  const usernameRef = useRef();

  const handleSubmit = (e) => {
    e.preventDefault();

    console.log(usernameRef.current.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" ref={usernameRef} />

      <button type="submit">Submit</button>
    </form>
  );
}
```

## 15. Difference between controlled and uncontrolled components

In React, the main difference between Controlled and Uncontrolled Components is who manages the form data.

- In a Controlled Component, React state manages the input value.
- In an Uncontrolled Component, the DOM manages the input value.

A simple way to remember:

Controlled = React controls the form data.
Uncontrolled = DOM controls the form data.

## 16. What happens when state changes?

When a state changes, React schedules a re-render of the component. During this process, React creates a new Virtual DOM, compares it with the previous Virtual DOM, identifies the differences, and updates only the necessary parts of the real DOM.

This ensures that the UI stays synchronized with the latest state while minimizing expensive DOM updates.
