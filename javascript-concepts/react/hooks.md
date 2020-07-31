## Hooks

[Code Sandbox](https://codesandbox.io/s/hooks-state-3e59n)
[Code Sandbox](https://codesandbox.io/s/hooks-lifecycle-d9bn2)

Hooks allow functional components to have state (`useState`) and to respond to lifecycle events (`useEffect`).

### access state

using the `useState()` API, you can create a new state variable and have a way to alter it. `useState()` accepts the initial value of the state item and returns an array containing the state variable and the function you call to alter the state. since it returns an array, we use array destructuring to access each individual item - like: `const [count, setCount] = useState(0)`

```javascript
// Counter.js
import React, { useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You've clicked {count} times!</p>
      <button onClick={() => setCount(count + 1)}>CLICK ME</button>
    </div>
  );
};

export default Counter;
```

### access lifecycle

using the `useEffect()` API, you can access the lifecycle methods - this accepts a function and can be used to initialize variables, make API calls, perform cleanup, and many other use cases.

```javascript
import React, { useState, useEffect } from "react";

const CounterEffect = () => {
  const [count, setCount] = useState(0);
  const [name, setName] = useState("Tim");

  useEffect(() => {
    console.log(`Hey ${name}, you've clicked the button ${count} times.`);
    return () => {
      console.log("UNMOUNTED.");
    };
  }, [count, name]);

  return (
    <div>
      <p>
        Hey {name} - you've clicked {count} times!
      </p>
      <button onClick={() => setCount(count + 1)}>CLICK ME</button>
      <button onClick={() => setName(name === "Tim" ? "Jim" : "Tim")}>
        CHANGE NAME
      </button>
    </div>
  );
};

export default CounterEffect;
```

note that returning a function from the `useEffect` parameter does the same thing as `componentWillUnmount`

by adding an array to the end of `useEffect`, the contents tell react to only re-run the side effect when changes to these items are made. by passing an empty array, it tell react to only execute the side effect once at mount time.

### enable cross-component communication using custom Hooks

custom hooks are bits of code/functionality that can be used throughout components in an app. they can be used to share state and logic between components - this is a better approach, in most use cases, than using higher-order-components and/or render props.
