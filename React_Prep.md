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

## 6. What are components in React?

Components are the building blocks of a React application. A component is a reusable, independent piece of UI that contains its own structure, logic, and behavior.

Instead of creating an entire page as one large file, React encourages breaking the UI into smaller reusable components, making the application easier to develop, maintain, and scale.

## 7. Difference between functional and class components?

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

## 8. What is component reusability?

Component Reusability is the ability to create a component once and use it multiple times in different parts of an application by passing different data through props.

Instead of writing the same UI and logic repeatedly, we create a reusable component and customize its behavior using props. This reduces code duplication, improves maintainability, and makes applications easier to scale.

# Props & State

## 9. What are props?

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

## 10. What is state?

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

## 11. State vs Props

Props are used to pass data from parent components to child components and are read-only. State is used to manage dynamic data within a component and can be updated using React's state management functions.

## 12. What is lifting state up?

Lifting State Up is a React pattern where state is moved from a child component to the closest common parent component so that multiple child components can share and synchronize the same data.

When two or more components need access to the same state, instead of maintaining separate copies of that state, we "lift" the state to their common parent and pass it down through props.

## 13. What is prop drilling?

Prop Drilling is a situation in React where props are passed through multiple intermediate components just to reach a deeply nested child component that actually needs the data.

The intermediate components do not use the props themselves; they only forward them to the next component.

This can make the code harder to read, maintain, and scale.

## 14. How do you avoid prop drilling?

Prop Drilling can be avoided by using state-sharing techniques that allow components to access data directly without passing props through multiple intermediate components.

The most common solutions are:

1. Context API
2. State Management Libraries (Redux, Zustand, Jotai, etc.)
3. Component Composition
4. Keeping State Close to Where It's Needed

## 15. What are controlled components?

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

## 16. What are uncontrolled components?

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

## 17. Difference between controlled and uncontrolled components

In React, the main difference between Controlled and Uncontrolled Components is who manages the form data.

- In a Controlled Component, React state manages the input value.
- In an Uncontrolled Component, the DOM manages the input value.

A simple way to remember:

Controlled = React controls the form data.
Uncontrolled = DOM controls the form data.

## 18. What happens when state changes?

When a state changes, React schedules a re-render of the component. During this process, React creates a new Virtual DOM, compares it with the previous Virtual DOM, identifies the differences, and updates only the necessary parts of the real DOM.

This ensures that the UI stays synchronized with the latest state while minimizing expensive DOM updates.

# Hooks

## 19. What is useState?

useState is a React Hook that allows functional components to store and manage state.

Before Hooks were introduced, only Class Components could manage state. With useState, Functional Components can now have their own state and re-render when that state changes.

## 20. What is useEffect?

useEffect is a React Hook used to handle side effects such as API calls, subscriptions, timers, and event listeners in functional components.

The dependency array is the second argument of useEffect that controls when the effect should run.

A cleanup function is a function returned from useEffect that React executes before the effect runs again or before the component unmounts. Cleanup functions are used to prevent memory leaks and remove resources that are no longer needed.

## 21. useEffect Vs useLayoutEffect

Both useEffect and useLayoutEffect are React Hooks used to perform side effects, but the key difference is when they run.

- useEffect runs after the browser has painted the updated UI to the screen.
- useLayoutEffect runs synchronously after React updates the DOM but before the browser paints the screen.

Because useLayoutEffect blocks the browser from painting, it should only be used when necessary.

## 22. What is useRef?

useRef is a React Hook that creates a mutable reference object whose value persists across renders. It is commonly used for accessing DOM elements and storing values without causing component re-renders.

Unlike state, updating a ref does not trigger a re-render, making useRef ideal for DOM manipulation, storing previous values, and maintaining mutable data across renders.

### Example :

```js
import { useRef } from "react";

function App() {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus Input</button>
    </>
  );
}
```

### useRef vs useState

The mager difference between useRef & useState is -

1. useRef Does not trigger re-render but useState Triggers re-render
2. useRef use the DOM directly but useState use virtualdom.
3. useRef update the content with the felp of `.current` but useState use `setState`.

## 23. What is React Memo?

Reacrt memo is a higher order component used to prevent unnessary re-render for functional components.

It only re-render the component, when its props are changed.

React memo is used to optimize the performance by memoizing a component and prevent re-render if props remain the same.

### why we need -

when parent component are re-render all the child components which are linked with the parent component are also re-render without any need and reason, so react memo prevent this.child component only re-render when the props are changed.

### Example -

```js
// without memo
function child({ name }) {
  console.log("child re-render");
  return <h1>{name}</h1>;
}

// with memo
const child = React.memo(function child({ name }) {
  console.log("child re-render");
  return <h1>{name}</h1>;
});

function parent() {
  const [count, setCount] = useState(0);
  return (
    <>
      <child name="Jeet" />
      <button onClick={() => setCount(count + 1)}>Increase</button>
      <p>{count}</p>
    </>
  );
}
```

## 24. what is useMemo?

useMemo is a react hook use to memoize a computed/expensive computational value so that it is recalculation only when its dependencies are changed.

useMemo is used to optimize performnce by avoiding expensive recalculation on every re-render

### why we need -

component re-render -> all logics run again and expensive logics also run again and that might be slow down the websit, so preventing thi we use useMemo.

## 25. what is useCallback?

useCallback is a react hook use to mamoize the function so that the same function referance is reused between re-renders unless its dependencies are changed. useCallback is used to prenent unnessary re-creation of function of every re-render

## 26. 33. What is re-rendering in React?

Re-rendering is the process where React executes a component again to generate an updated UI whenever its data changes.

When a component's state, props, or context changes, React re-runs the component function, creates a new Virtual DOM, compares it with the previous Virtual DOM, and updates only the necessary parts of the real DOM.

## 27. How do you optimize React performance?

React performance can be optimized by reducing unnecessary re-renders using React.memo, useMemo, and useCallback, keeping state local, using proper keys, implementing code splitting and lazy loading, virtualizing large lists, and profiling the application to identify bottlenecks.

## 28. What is Memoization?

Memoization is an optimization technique where the result of an expensive operation is cached (stored), so that if the same input occurs again, the cached result is returned instead of recalculating it.

The goal is to improve performance by avoiding unnecessary computations.

## 29. What is lazy loading?

Lazy Loading is a performance optimization technique where components, modules, images, or resources are loaded only when they are actually needed, instead of loading everything during the initial page load.

The main goal is to:

- Reduce initial bundle size
- Improve page load speed
- Improve user experience
- Reduce unnecessary downloads

## 30. What is code splitting?

Code Splitting is a technique used to divide a large JavaScript bundle into smaller chunks that can be loaded on demand.

Instead of downloading the entire application at once, the browser downloads only the code needed for the current page or feature.

This improves:

- Initial load time
- Performance
- User experience
- Bundle size management

## 31. Client-Side Rendering (CSR)

Client-Side Rendering (CSR) is a rendering technique where the browser downloads a minimal HTML file and JavaScript bundle, and then React renders the UI in the browser.

In CSR, most of the rendering work happens on the client (browser) instead of the server.

### Why is CSR Popular?

- Fast client-side navigation
- Rich interactivity
- Smooth user experience
- Reduced server rendering costs

## 32. server-side rendering (SSR)

Server-Side Rendering (SSR) is a technique where the server renders React components into HTML and sends the fully rendered page to the browser. After the page loads, React hydrates it to make it interactive. SSR improves SEO and initial page load performance.

In SSR, the initial rendering happens on the server, not in the browser.
